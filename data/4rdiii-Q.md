
# [L-01] Potential Risk of ETH Deposits Being Compromised Due to Centralization Risks

## Impact 
If the amount of VULT tokens deposited into the liquidity pool is less than half of the total supply, the owner of the remaining VULT tokens (the token contract owner) could potentially deposit a large amount of VULT tokens into the pool, effectively draining the deposited ETH from users.

## Proof of Concept
An example using values from the `Whitelist.ts` test:
- Initial pool values: 10 million VULT tokens, 26 ETH, and assuming 1000 participants.
- Each address can purchase up to 3 ETH worth of VULT tokens, resulting in a maximum of 3000 ETH deposited into the pool.
- After transactions, assuming the Uniswap liquidity invariant x * y = k:
  - \( 4000 \cdot y_{\text{new}} = 26 \cdot 10,000,000 \)
  - \( y_{\text{new}} = 65,000 \) VULT tokens

- If the VULT token owner deposits an additional 10 million VULT tokens to drain the ETH:
  - \( x_{\text{new}} \cdot 100,650,000 = 4000 \cdot 65,000 \)
  - \( x_{\text{new}} = 25.83 \) ETH

## Tools Used
Manual Review

## Recommended Mitigation Steps
To mitigate the risk of a potential rug pull or unauthorized draining of ETH:
- Implement a time lock mechanism on the remaining VULT token supply.
- Consider a transparent distribution model for the remaining tokens.
- Increase the amount of VULT tokens deposited by the protocol into the liquidity pool (more than 3 * numberOfWhitelistedAddress ETH).

# [L-02] Functions which do not expect ether should be non-payable or check for msg.value sent
A function which doesn’t expect ether should not be marked payable, In `ILOPool::claim` and `ILOPool::multicall` both are marked as payable, but the contracts are designed so no functions needs paying native token to function, so both of them should not be marked payable or implement a check to revert in case native token was sent to them.

## Impact
Since there is no sweep function also, all ETH sent to the contract will be lost forever.

## Proof of Concept
`Multical.sol`:
```javascript
@>  function multicall(bytes[] calldata data) public payable override returns (bytes[] memory results)
```
`ILOPool.sol`:
```javascript
    function claim(
        uint256 tokenId
    )
        external
@>      payable
        override
        isAuthorizedForToken(tokenId)
        returns (uint256 amount0, uint256 amount1)
```
## Tools Used
Manual Review
## Recommended Mitigation Steps
Remove `payable` keyword or add a check for `msg.value`.

```diff
    function claim(
        uint256 tokenId
    )
        external
        payable
        override
        isAuthorizedForToken(tokenId)
        returns (uint256 amount0, uint256 amount1)
    {
+   require(msg.value == 0, "ETH Sent!");
    .
    .
    .

```
# [L-03] No input Validation for `ILOManager::initProject`  and `setRefundDeadlineForProject`
The `initProject` function receives the `IILOManager::InitProjectParams` struct as input parameters, which calculates `refundDeadline` from the provided `params.launchTime`. However, the input for this value is not checked to ensure it is in the future. Setting this incorrectly may cause multiple methods of `ILOManager` or `ILOPool` to malfunction.

```solidity
function initProject(
        InitProjectParams calldata params
    ) external override afterInitialize returns (address uniV3PoolAddress) {
@>      uint64 refundDeadline = params.launchTime + DEFAULT_DEADLINE_OFFSET;
        .
        .
        .
    }
```

Similarly, the same checks are not implemented for the `setRefundDeadlineForProject` method. Although this method is only accessible by the owner, mistakes can still happen. If a mistake occurs, it may cause a working project to reach the `RefundDeadline` suddenly and stop working, which could have severe consequences.

```solidity
    function setRefundDeadlineForProject(
        address uniV3Pool,
        uint64 refundDeadline
    ) external override onlyOwner {
        Project storage _project = _cachedProject[uniV3Pool];
        emit RefundDeadlineChanged(
            uniV3Pool,
            _project.refundDeadline,
            refundDeadline
        );
@>      _project.refundDeadline = refundDeadline;
    }

```
## Impact
1. initProject:
If launchTime is set incorrectly to a past time, the refundDeadline may also be set to a past or very near future time, causing immediate or premature refund conditions.This can disrupt the normal flow of project lifecycle events and lead to unintended consequences, such as early termination of projects or blocking project initialization.

2. setRefundDeadlineForProject:
If the owner mistakenly sets a refundDeadline to a past time or an unreasonable future time, it can cause the project to reach the refund deadline immediately. This would result in operational issues and potentially halt a functioning project, affecting all stakeholders involved.

## Tools Used
Manual review

## Recommended Mitigation Steps
1. Add a check to ensure `params.launchTime` is set to a future time before calculating the `refundDeadline`.
```diff
+       require(params.launchTime > block.timestamp, "Launch time must be in the future");
```

2. Add a check to ensure  `refundDeadline` is set to a future time.
```diff
+       require(refundDeadline > block.timestamp, "Refund deadline must be in the future");
```

# [L-04] `ILOManager::initProject` Can Be Front-run to Prevent ILO Providers' Access to Contract
Anyone can call the `initProject` method, and if there is an existing project linked to a liquidity pool, `initProject` will revert. Therefore, `initProject` can be front-run or simply called before the actual ILO providers if they discover that an ILO is imminent.

## Impact
This vulnerability prevents the project owner from creating new ILO Pools and utilizing the contract indefinitely, unless they establish a new Uniswap Pool.

## Proof of Concept
To demonstrate this issue, incorporate the following into the existing test suite:

```javascript
    function testInitProjectFrontRunned() external {
        vm.prank(griefer);
        iloManager.initProject(
            IILOManager.InitProjectParams({
                saleToken: mockProject().saleToken,
                raiseToken: mockProject().raiseToken,
                fee: 10000,
                initialPoolPriceX96: mockProject().initialPoolPriceX96 + 1,
                launchTime: mockProject().launchTime
            })
        );
        vm.expectRevert(bytes("RE"));
        iloManager.initProject(
            IILOManager.InitProjectParams({
                saleToken: mockProject().saleToken,
                raiseToken: mockProject().raiseToken,
                fee: 10000,
                initialPoolPriceX96: mockProject().initialPoolPriceX96 + 1,
                launchTime: mockProject().launchTime
            })
        );
    }
```
## Tools Used
Manual Review
## Recommended Mitigation Steps
1. Implement extra access control mechanisms, such as whitelists.
2. Put a function in place so owner can remove malicous and empty projects.


# [NC-01] Critical Privilages are Transferred in One Step Instead of Two

`owner` has critical privilages in the protocol. `Whitelist::transferOwnership` allows the owner to transfer ownership (and associated critical privilages) in a one-step process.
```javascript
@>  function transferOwnership(address newOwner) public virtual onlyOwner {
        require(newOwner != address(0), "Ownable: new owner is the zero address");
        emit OwnershipTransferred(_owner, newOwner);
@>      _owner = newOwner;
    }
```
## Impact

Critical owner priviliges could be transferred to an incorrect address e.g. if
- owner mistakenly inputs an incorrect address when calling `Whitelist::transferOwnership`,
- the protocol becomes the victim of a Clipboard Replacement Attack: protocol owner copies the address that ownership is supposed to be transferred to, but a malware replaces the address on the clipboard with a different, attacker-controlled address that the protocol owner will eventually end of pasting when preparing to call `Whitelist::transferOwnership`
With the ownership privilages transferred to an incorrect account, the whole protocol will be compromised/unusable.


## Recommended Mitigation Steps
Transfer critical priviliges in a 2-step process. Modify PrelaunchPoints as follows:

```diff
+   address private _newOwner;
    function transferOwnership(address newOwner) public virtual onlyOwner {
        require(newOwner != address(0), "Ownable: new owner is the zero address");
-       emit OwnershipTransferred(_owner, newOwner);
-       _owner = newOwner;
+       _newOwner = newOwner;

    }

+    function acceptOwnership() external {
+        require(msg.sender == _newOwner, "Not the proposed owner");
+        emit OwnershipTransferred(owner, _newOwner);
+        owner = _newOwner;
+        _newOwner = address(0);
+    }
```
# [NC-02] No Event Emissions for Critical State Changes in `Whitelist.sol` contract
`Whitelist::_maxAddressCap` ,`Whitelist::_locked`, `Whitelist::_isSelfWhitelistDisabled`, `Whitelist::_allowedWhitelistIndex` and many other important state variables can be changed via setter functions in this contract but no events are defined and no emissions are done when the changes are implemented.

## Impact
Reduced transparency
Difficulty to track changes
Inefficient or impossible integration with other contracts and services

## Recommended Mitigation Steps
Define and emit events for critical changes performed 


# [NC-03] Excessive Setter Functions Increase Risk of Uninitialization or Incorrect Data Input

## Impact
The `Whitelist` contract currently contains 8 individual setter functions. This design could lead to variables being left uninitialized or increase the risk of incorrect data input. A more efficient approach would be to consolidate these setters into a single initializer function, which can set multiple variables in one operation. This method is particularly beneficial for variables that are likely to be set only once during the contract's lifecycle.

For instance, the following variables are prime candidates for batch initialization:
- `Whitelist::setAllowedWhitelistIndex`
- `Whitelist::setPool`
- `Whitelist::setOracle`
- `Whitelist::setVultisig`
- `Whitelist::setMaxAddressCap`

## Recommended Mitigation Steps
Implement an initializer function within the `Whitelist` contract to streamline the initialization process. This function should allow for the simultaneous setting of several key variables, thereby reducing complexity and potential points of failure.

Below is an example implementation of such an initializer function:
```javascript
 // Event to emit when initialization is successful
    event InitializationSuccessful(address indexed oracle, address indexed vultisig);

    // Modifier to restrict initializer function to be called only once
    modifier initializer() {
        require(_initialized == false, "Contract is already initialized");
        _initialized = true;
        _;
    }

    bool private _initialized = false;

    // Function to initialize contract settings
    function initialize(
        uint256 allowedWhitelistIndex,
        address pool,
        address oracle,
        address vultisig,
        uint256 maxAddressCap
    ) public initializer {
        _allowedWhitelistIndex = allowedWhitelistIndex;
        _pool = pool;
        _oracle = oracle;
        _vultisig = vultisig;
        _maxAddressCap = maxAddressCap;

        emit InitializationSuccessful(_oracle, _vultisig);
    }
```

# [NC-04] Lack of State variable for `blacklistedCount`

## Impact
The current implementation lacks a dedicated state variable or getter function to track the count of blacklisted addresses (`blacklistedCount`). While invariants suggest that administrators might adjust the `_allowedWhitelistIndex` based on the number of blacklisted addresses, managing this becomes increasingly challenging as the number of blacklisted addresses grows. The absence of a straightforward way to obtain this count complicates administrative tasks and decision-making processes.


## Recommended Mitigation Steps
To enhance manageability and facilitate administrative decisions, it is recommended to introduce either a `blacklistedCount` state variable or a getter function that dynamically calculates the length of blacklisted users. Below is an example of how to implement a `blacklistedCount` state variable along with an update mechanism within the `setBlacklisted` function:
```diff
+   uint256 public _blacklistedCount;
.
.
.
    function setBlacklisted(address blacklisted, bool flag) external onlyOwner {
+       if (flag) {
+           _blacklistedCount++;
+       } else {
+           _blacklistedCount--;
+       }
        _isBlacklisted[blacklisted] = flag;
    }
```

