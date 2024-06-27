# EPSec Report

This report was created by EPSec.

# Summary

## Issue Summary

| Category | No. of Issues |
| -------- | ------------- |
| Low      | 34            |
| Info     | 7             |

# Low Issues

First 20 issues are found by manual review and the next 14 are found by Aderyn. 

## L-1: Missing address(0) checks

In the `Whitelist::setOracle`, `Whitelist::setPool` and `Whitelist::setVultisig` functions, there is currently no check to ensure that the new oracle address is not the zero address (`address(0)`). This omission can lead to potential issues because setting the oracle to the zero address can result in unintended behavior or vulnerabilities within the contract.
## Impact

This omission can lead to potential issues because setting the oracle to the zero address can result in unintended behavior or vulnerabilities within the contract.

## Recommended Mitigation Steps

Add this line multiple time for the apropariate address `require(addr != address(0), "Some Error");` to
`Whitelist::setOracle`

## L-2: BPS should be defined on one place

In `ILOVest`, `BPS` is redundantly defined and should be referenced from `ILOPoolImmutableState` for consistency and clarity.

## Impact

Duplicate declarations of `BPS` across contracts can lead to confusion and maintenance challenges.

## Recommended Mitigation Steps

**Reference from `ILOPoolImmutableState`**: Instead of declaring `BPS` in `ILOVest`, reference it directly from `ILOPoolImmutableState` to ensure consistency and avoid redundancy.

## L-3: Use initializable by open zeppelin

In `ILOWhitelist`, instead of using a custom `Initializable`, consider using OpenZeppelin's `Initializable` contract available [here](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/proxy/utils/Initializable.sol).

## Impact

1. **Security and Reliability**: Custom initialization logic can introduce bugs and vulnerabilities that have been mitigated in the well-audited OpenZeppelin contracts.
2. **Maintenance and Upgrades**: Using a widely adopted library like OpenZeppelin ensures better support, updates, and community trust.

## Recommended Mitigation Steps

1. **Adopt OpenZeppelin's Initializable**: Replace the custom `Initializable` contract with OpenZeppelin's implementation to leverage its security and reliability benefits.
2. **Review and Test**: Thoroughly review and test the integration to ensure compatibility and correct functionality within your contract.
## L-4: Use uniswap libraries

Currently, files such as `ChainId.sol` and others are copied from Uniswap. Instead, consider using `PoolAddress.sol`, `ChainId.sol`, and all related files from the Uniswap v3-periphery library available [here](https://github.com/Uniswap/v3-periphery/blob/main/contracts/libraries/PoolAddress.sol).

## Impact

1. **Consistency**: Using the latest version from the official Uniswap library ensures consistency with the most recent and supported implementations.
2. **Security and Reliability**: The Uniswap v3-periphery library is well-audited and widely trusted, reducing the risk of bugs and vulnerabilities.

## Recommended Mitigation Steps

Replace the current copied files with the corresponding files from the Uniswap v3-periphery library.

## L-5: ILOManager missing zero checks

The `ILOManager::initialize` function should include checks to ensure that no critical addresses are set to the zero address (`address(0)`). Omitting these checks can lead to unintended behavior or vulnerabilities in the contract.

## Impact

- **Zero Address Risk**: If any address parameters are inadvertently set to the zero address, it can lead to potential security risks, including loss of funds, inability to interact with critical contract functions, and unintended contract behavior.
## Recommended Mitigation Steps

Introduce checks to ensure that all critical addresses are not zero addresses before assignment.
Add this block of code: 

```solidity
require(initialOwner != address(0), "Invalid address: initialOwner"); require(_feeTaker != address(0), "Invalid address: feeTaker"); require(iloPoolImplementation != address(0), "Invalid address: iloPoolImplementation"); require(uniV3Factory != address(0), "Invalid address: uniV3Factory"); require(weth9 != address(0), "Invalid address: weth9");
```
## L-6: Use newer version of solidity

Currently in the protocol is used a older version of solidity `0.7.6`, I would suggest in terms of safety to use a newer version.

## Impact 

Older versions of Solidity may contain known security vulnerabilities that have been patched in later versions. Using version 0.7.6 exposes the protocol to potential exploits that have been identified and mitigated in newer releases.

## Recommended Mitigation Steps

Upgrade to the latest stable version of Solidity to ensure access to the latest security patches, features, and optimizations.

## L-7: Missing Check

The `ILOManager::initProject` function initializes a project based on parameters provided (`params`). It calculates a `refundDeadline` which determines until when certain operations can be performed. However, there was a concern that there might be a missing check to ensure `refundDeadline` is correctly set after the current block timestamp (`block.timestamp`).

Not having a check to ensure `refundDeadline > block.timestamp` could lead to potential issues:

## Impact

Without the check, the project could be initialized even after the intended deadline, leading to unexpected behavior.

## Recommended Mitigation Steps 

Add this line to the beginning of 
`require(refundDeadline > block.timestamp, "Refund deadline must be after current time");`

## L-8: Fees need to be less than BPS

The `initialize` function initializes parameters including `PLATFORM_FEE` and `PERFORMANCE_FEE`, which are represented in basis points (BPS). It's crucial to verify that these fees do not exceed the maximum allowed BPS value to prevent unexpected behavior or errors in fee calculations.

## Impact

Exceeding the maximum BPS value for fees can lead to:

- **Incorrect Fee Calculation:** Fees could be calculated incorrectly if they exceed the expected BPS range.
- **Contract Vulnerability:** Unexpected behavior due to incorrect fee calculations might expose the contract to vulnerabilities.

## Recommended Mitigation Steps 

To mitigate risks associated with fees exceeding BPS, implement the following:

```diff
function initialize(
    address initialOwner,
    address _feeTaker,
    address iloPoolImplementation,
    address uniV3Factory,
    address weth9,
    uint16 platformFee,
    uint16 performanceFee
) external override whenNotInitialized {
+    require(platformFee < 10000, "PLATFORM_FEE must be less than 10000 BPS (100%)");
+    require(performanceFee < 10000, "PERFORMANCE_FEE must be less than 10000 BPS (100%)");

     PLATFORM_FEE = platformFee;
     PERFORMANCE_FEE = performanceFee;
```
## L-9: Redundant if block

The `buy` function in the `ILOPool` contract currently lacks `payable` functionality, making it unable to receive Ether (ETH) directly. This limitation impacts the ability to participate in initial liquidity offerings (ILOs) using ETH. Additionally, the `PeripheryPayments::pay` function includes ETH handling, which may need adjustment to accommodate ETH transactions seamlessly. In the current implementation, the result of the `transfer` function is not checked after token transfers, which can lead to potential issues and vulnerabilities. It's crucial to verify the success of these transfers to ensure the integrity and reliability of transactional operations within the smart contract.

## Impact

The absence of ETH support in the `buy` function and potential unnecessary handling in `PeripheryPayments::pay` can lead to malicious user send enough ETH using `selfDescruct`, and this could lead to stucked WETH tokens in the contract. Also if you decide to leave it as it is, you should probably fix the `transfer` function call handling. 

## Recommended Mitigation Steps 

To address these issue, consider removing thus if block:

```
if (token == WETH9 && address(this).balance >= value) {
            // check here
            // pay with WETH9
            IWETH9(WETH9).deposit{value: value}();
            IWETH9(WETH9).transfer(recipient, value);
}
```

## L-10: Add zero check for shares

Lack of zero check in `ILOVest::_validateSharesAndVests` and `ILOVest::_validateVestSchedule` for the `shares`. This variable is used for computation in 
`ILOPool` and it can lead to wrong computation and vesting. 

## Impact
The absence of checks for zero values in `shares` within the `ILOVest::_validateSharesAndVests` and `ILOVest::_validateVestSchedule` functions can have significant implications for the integrity and accuracy of computations within the `ILOPool` contract.

## Recommended Mitigation Steps  

Add a check to ensure that `shares` are greater than zero.

## L-11: minAmount0 or minAmount1 could be zero

Within the `ILOPool::launch`, there exists a potential risk where the minimum acceptable amounts (`amount0Min` and `amount1Min`) might inadvertently be set to zero. 

## Impact 

If you take a look at the below check, you will see that one of the check will be always true, it should be assigned a value to prevent this to happen.
```
function addLiquidity(AddLiquidityParams memory params)
        internal
        returns (
            uint256 amount0,
            uint256 amount1
        )
    {
        (amount0, amount1) = params.pool.mint(
            address(this),
            TICK_LOWER,
            TICK_UPPER,
            params.liquidity,
            ""
        );

        require(amount0 >= params.amount0Min && amount1 >= params.amount1Min, 'Price slippage check');
    }
```

## L-12: Pausable tokens could brake the protocol

Pausable tokens could break the protocol.
## Impact
If a token is paused before launch:

- The protocol cannot commence as planned.
- Users will be unable to withdraw their tokens from the pool, potentially disrupting planned activities and causing dissatisfaction among users.
## Recommended Mitigation Steps  
Consider not creating pools with pausable tokens.

## L-13: setWhitelistContract

The current implementation of `VultisigWhitelisted::setWhitelistContract` assigns the `whiteListContract` to `VultisigWhitelisted`, but fails to reciprocally assign `VultisigWhitelisted` to the `whitelistContract`. This reciprocal assignment is crucial for ensuring mutual functionality and can be achieved within the same function and transaction.

## Impact

Without both contracts referencing each other, certain operations or interactions between them may not function as intended, potentially leading to operational inconsistencies or errors.
By including the reciprocal assignment in the same function and transaction, efficiency is improved as it reduces the need for separate transactions and ensures atomicity, thereby minimizing potential for discrepancies. I will suggest to also clear the configuration of the whitelist. 

## Recommended Mitigation Steps  
To enhance the functionality and efficiency of `VultisigWhitelisted::setWhitelistContract`, ensure the following steps are taken:

```diff
function setWhitelistContract(address newWhitelistContract) external onlyOwner {     
   _whitelistContract = newWhitelistContract;
+   WhitelistContract(newWhitelistContract).setVultisig(address(this)); }
```

## L-14: Transfer ownership in two steps

The current implementation of `ILOManager::transferAdminProject` allows the adminOfProject to transfer ownership and critical privileges in a single step. This approach poses significant risks, including the potential for transferring ownership to incorrect addresses due to human error or malicious activities like clipboard replacement attacks.

## Impact:

The risks associated with the current implementation include:

- **Human Error:** Mistakes in entering recipient addresses during ownership transfers can lead to critical privileges being transferred to unintended or incorrect accounts.
- **Clipboard Replacement Attacks:** Malicious software can replace the intended recipient address on the clipboard with an attacker-controlled address. When the owner pastes this address into `ILOManager::transferAdminProject`, ownership privileges can unknowingly transfer to the attacker.
- **Protocol Compromise:** If ownership privileges are transferred to an incorrect account, the entire protocol could be compromised, leading to operational disruptions or misuse of protocol resources.
## Recommended Mitigation Steps:

To mitigate these risks and enhance the security of ownership transfers within the protocol, it is recommended to implement a two-step process for transferring critical privileges. This approach introduces additional verification steps to ensure the accuracy and validity of ownership transfers.

## L-15: Missing event emission on changes

`ILOManager::setPlatformFee`, `ILOManager::setPerformanceFee` and `ILOManager::setFeeTaker` modify critical state variables, but no events are defined and emitted to broadcast the changes. This is also applicable for all set methods in `Whitelist.sol`.

## Impact

1. Reduced transparency
2. Difficulty to track changes
3. Inefficient or impossible integration with other contracts and services

## Recommended Mitigation Steps

Define and emit events for critical changes performed in `ILOManager::setPlatformFee`, `ILOManager::setPerformanceFee` and `ILOManager::setFeeTaker`. This is also applicable for all set methods in `Whitelist.sol`.

## L-16: Some files are copied from uniswap v3

In the directory `/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8` files are copied from here [https://github.com/Uniswap/v3-core/pull/525](https://github.com/Uniswap/v3-core/pull/525 "https://github.com/Uniswap/v3-core/pull/525"). The files are almost indentical and the problem is that the files in uniswap are caped to <0.8.0, but the files in the project are >0.8.0.

## Impact

In the pull request above, the uniswap decided  to cap the version of these libraries to <0.8.0 due to the fact that they rely on `overflow` and `underflow`.

## L-17: Start and end should be after the current timestamp

The `ILOManager::initIPool` function is responsible for initializing an Initial Liquidity Offering (ILO) pool with specified parameters. Currently, it does not include a check to ensure that the current block timestamp is less than the specified start time for the pool. This missing validation step could lead to the pool being initialized after the intended start time, which is not ideal for the buy operation, which depend on start and end time.

## Impact

This will result in a shorter time period for the `buy` function, limiting the window in which users can make purchases.

## Recommended 

```diff
function initILOPool(
        InitPoolParams calldata params
    )
        external
        override
        onlyProjectAdmin(params.uniV3Pool)
        returns (address iloPoolAddress)
    {
        Project storage _project = _cachedProject[params.uniV3Pool];
        {
            require(_project.uniV3PoolAddress != address(0), "NI");
            // validate time for sale start and end compared to launch time
+            require(
+                params.start > block.timestamp && params.start < params.end && params.end < _project.launchTime,
+                "PT"
+            );
-            require(
-                params.start < params.end && params.end < _project.launchTime,
-                "PT"
-            );
```

## L-18: Pool can be created after initialization of project

In the current implementation of our project management system, it is possible to create a pool for a project even after the project has been launched. This occurs because there is no check to verify if the project is already initialized when attempting to create a new pool. The only condition that is verified is:

```solidity
require(params.start < params.end && params.end < _project.launchTime, "PT");
```

This requirement ensures that the start time of the pool is before its end time and that the end time is before the project's launch time, but it does not prevent pool creation after the project has been launched.

## Impact

Allowing the creation of pools after a project has been launched can lead to several issues:

1. **Integrity and Consistency:** Post-launch modifications can lead to data inconsistency and undermine the integrity of the project management system.
2. **Security Risks:** Unauthorized or unintended modifications post-launch can introduce vulnerabilities and potential exploits.
3. **User Trust:** Users and stakeholders may lose trust in the system if post-launch changes are possible, leading to doubts about the reliability and stability of the project.
4. **Operational Issues:** Unintended pool creations can interfere with the project's operations and planned activities, causing disruptions.

## Recommended Mitigation Steps

To mitigate these risks and enhance the robustness of the system, the following steps are recommended:

 **Check for Initialization:** Introduce a check to verify whether the project has already been initialized before allowing pool creation. This can be done by adding a new condition in the pool creation logic.
```solidity
require(!_project.initialized, "Project already launched");`
```

## L-19: Precision loss

In the buy function, liquidity is computed for each user, but instead of storing this liquidity as a state variable, it is recomputed during the launch, specifically when adding liquidity. This approach can lead to rounding errors.

## Impact

The recomputation of liquidity during the launch phase can result in slight discrepancies due to rounding errors. These discrepancies might cause:

1. **Inconsistent Liquidity Allocation:** Users might receive a different amount of liquidity than initially computed, leading to potential disputes and a lack of trust in the system.
2. **Financial Losses:** Even minor rounding errors can accumulate, resulting in significant financial losses over numerous transactions.
3. **Inefficiency:** Recomputing liquidity multiple times introduces inefficiencies and increases the complexity of the codebase.

## L-20: Buy execution

In the `ILOPool::buy` function, there is a potential issue related to the refund mechanism. Specifically, if the refund process has already started, it should be checked before allowing new purchases. The presence of the `ILOManager::setRefundDeadlineForProject` function, which can set the refund deadline to a time between the start and end of the sale period, creates a scenario where users might be able to buy and immediately request a refund.

### Impact

**Financial Loss:** Users unfamiliar with the protocol could lose funds if they unknowingly purchase tokens during a refund period. This can lead to unexpected financial consequences and diminished trust in the platform.

### Recommended Mitigation Steps

**Implement Refund Status Check:** Ensure that the `buy` function includes a check to verify whether the refund process has already started before allowing any new purchases. 

```diff
function buy(
        uint256 raiseAmount,
        address recipient
    ) external override returns (uint256 tokenId, uint128 liquidityDelta) {
        require(_isWhitelisted(recipient), "UA");
        require(
            block.timestamp > saleInfo.start && block.timestamp < saleInfo.end,
            "ST"
        );
+       require(!_refundTriggered);
        require(saleInfo.hardCap - totalRaised >= raiseAmount, "HC");
        totalRaised += raiseAmount;
```
## L-21: Centralization Risk for trusted owners

Contracts have owners with privileged rights to perform admin tasks and need to be trusted to not perform malicious updates or drain funds.

<details><summary>7 Found Instances</summary>


- Found in src/ILOManager.sol [Line: 15](src/ILOManager.sol#L15)

	```solidity
	contract ILOManager is IILOManager, Ownable, Initializable {
	```

- Found in src/ILOManager.sol [Line: 216](src/ILOManager.sol#L216)

	```solidity
	    function setPlatformFee(uint16 _platformFee) external onlyOwner {
	```

- Found in src/ILOManager.sol [Line: 221](src/ILOManager.sol#L221)

	```solidity
	    function setPerformanceFee(uint16 _performanceFee) external onlyOwner {
	```

- Found in src/ILOManager.sol [Line: 226](src/ILOManager.sol#L226)

	```solidity
	    function setFeeTaker(address _feeTaker) external override onlyOwner {
	```

- Found in src/ILOManager.sol [Line: 232](src/ILOManager.sol#L232)

	```solidity
	    ) external override onlyOwner {
	```

- Found in src/ILOManager.sol [Line: 251](src/ILOManager.sol#L251)

	```solidity
	    ) external override onlyOwner {
	```

- Found in src/ILOManager.sol [Line: 263](src/ILOManager.sol#L263)

	```solidity
	    ) external override onlyOwner {
	```

</details>

## L-22: Solidity pragma should be specific, not wide

Consider using a specific version of Solidity in your contracts instead of a wide version. For example, instead of `pragma solidity ^0.8.0;`, use `pragma solidity 0.8.0;`

<details><summary>13 Found Instances</summary>


- Found in src/base/PeripheryPayments.sol [Line: 2](src/base/PeripheryPayments.sol#L2)

	```solidity
	pragma solidity >=0.7.5;
	```

- Found in src/interfaces/IILOManager.sol [Line: 2](src/interfaces/IILOManager.sol#L2)

	```solidity
	pragma solidity >=0.7.5;
	```

- Found in src/interfaces/IILOPool.sol [Line: 2](src/interfaces/IILOPool.sol#L2)

	```solidity
	pragma solidity >=0.7.5;
	```

- Found in src/interfaces/IILOPoolImmutableState.sol [Line: 2](src/interfaces/IILOPoolImmutableState.sol#L2)

	```solidity
	pragma solidity >=0.5.0;
	```

- Found in src/interfaces/IMulticall.sol [Line: 2](src/interfaces/IMulticall.sol#L2)

	```solidity
	pragma solidity >=0.7.5;
	```

- Found in src/interfaces/external/IERC1271.sol [Line: 2](src/interfaces/external/IERC1271.sol#L2)

	```solidity
	pragma solidity >=0.5.0;
	```

- Found in src/interfaces/external/IERC20PermitAllowed.sol [Line: 2](src/interfaces/external/IERC20PermitAllowed.sol#L2)

	```solidity
	pragma solidity >=0.5.0;
	```

- Found in src/libraries/ChainId.sol [Line: 2](src/libraries/ChainId.sol#L2)

	```solidity
	pragma solidity >=0.7.0;
	```

- Found in src/libraries/LiquidityAmounts.sol [Line: 2](src/libraries/LiquidityAmounts.sol#L2)

	```solidity
	pragma solidity >=0.5.0;
	```

- Found in src/libraries/PoolAddress.sol [Line: 2](src/libraries/PoolAddress.sol#L2)

	```solidity
	pragma solidity >=0.5.0;
	```

- Found in src/libraries/PositionKey.sol [Line: 2](src/libraries/PositionKey.sol#L2)

	```solidity
	pragma solidity >=0.5.0;
	```

- Found in src/libraries/SqrtPriceMathPartial.sol [Line: 2](src/libraries/SqrtPriceMathPartial.sol#L2)

	```solidity
	pragma solidity >=0.5.0;
	```

- Found in src/libraries/TransferHelper.sol [Line: 2](src/libraries/TransferHelper.sol#L2)

	```solidity
	pragma solidity >=0.6.0;
	```

</details>

## L-23: Missing checks for `address(0)` when assigning values to address state variables

Check for `address(0)` when assigning values to address state variables.

<details><summary>7 Found Instances</summary>


- Found in src/ILOManager.sol [Line: 44](src/ILOManager.sol#L44)

	```solidity
	        FEE_TAKER = _feeTaker;
	```

- Found in src/ILOManager.sol [Line: 46](src/ILOManager.sol#L46)

	```solidity
	        UNIV3_FACTORY = uniV3Factory;
	```

- Found in src/ILOManager.sol [Line: 47](src/ILOManager.sol#L47)

	```solidity
	        ILO_POOL_IMPLEMENTATION = iloPoolImplementation;
	```

- Found in src/ILOManager.sol [Line: 48](src/ILOManager.sol#L48)

	```solidity
	        WETH9 = weth9;
	```

- Found in src/ILOManager.sol [Line: 227](src/ILOManager.sol#L227)

	```solidity
	        FEE_TAKER = _feeTaker;
	```

- Found in src/ILOManager.sol [Line: 237](src/ILOManager.sol#L237)

	```solidity
	        ILO_POOL_IMPLEMENTATION = iloPoolImplementation;
	```

- Found in src/ILOPool.sol [Line: 85](src/ILOPool.sol#L85)

	```solidity
	        _cachedUniV3PoolAddress = params.uniV3Pool;
	```

</details>

## L-24: `public` functions not used internally could be marked `external`

Instead of marking a function as `public`, consider marking it as `external` if it is not used internally.

<details><summary>2 Found Instances</summary>


- Found in src/ILOPool.sol [Line: 54](src/ILOPool.sol#L54)

	```solidity
	    function name()
	```

- Found in src/ILOPool.sol [Line: 63](src/ILOPool.sol#L63)

	```solidity
	    function symbol()
	```

</details>

## L-25: Define and use `constant` variables instead of using literals

If the same constant literal value is used multiple times, create a constant state variable and reference it throughout the contract.

<details><summary>2 Found Instances</summary>


- Found in src/base/ILOVest.sol [Line: 26](src/base/ILOVest.sol#L26)

	```solidity
	        uint16 BPS = 10000;
	```

- Found in src/base/ILOVest.sol [Line: 47](src/base/ILOVest.sol#L47)

	```solidity
	        uint16 BPS = 10000;
	```

</details>

## L-26: Event is missing `indexed` fields

Index event fields make the field more quickly accessible to off-chain tools that parse events. However, note that each index field costs extra gas during emission, so it's not necessarily best to index the maximum allowed per event (three fields). Each event should use three indexed fields if there are three or more fields, and gas usage is not particularly of concern for the events in question. If there are fewer than three fields, all of the fields should be indexed.

<details><summary>17 Found Instances</summary>


- Found in src/interfaces/IILOManager.sol [Line: 10](src/interfaces/IILOManager.sol#L10)

	```solidity
	    event ProjectCreated(address indexed uniV3PoolAddress, Project project);
	```

- Found in src/interfaces/IILOManager.sol [Line: 11](src/interfaces/IILOManager.sol#L11)

	```solidity
	    event ILOPoolCreated(address indexed uniV3PoolAddress, address indexed iloPoolAddress, uint256 index);
	```

- Found in src/interfaces/IILOManager.sol [Line: 13](src/interfaces/IILOManager.sol#L13)

	```solidity
	    event ProjectAdminChanged(address indexed uniV3PoolAddress, address oldAdmin, address newAdmin);
	```

- Found in src/interfaces/IILOManager.sol [Line: 14](src/interfaces/IILOManager.sol#L14)

	```solidity
	    event DefaultDeadlineOffsetChanged(address indexed owner, uint64 oldDeadlineOffset, uint64 newDeadlineOffset);
	```

- Found in src/interfaces/IILOManager.sol [Line: 15](src/interfaces/IILOManager.sol#L15)

	```solidity
	    event RefundDeadlineChanged(address indexed project, uint64 oldRefundDeadline, uint64 newRefundDeadline);
	```

- Found in src/interfaces/IILOManager.sol [Line: 17](src/interfaces/IILOManager.sol#L17)

	```solidity
	    event ProjectRefund(address indexed project, uint256 refundAmount);
	```

- Found in src/interfaces/IILOPool.sol [Line: 29](src/interfaces/IILOPool.sol#L29)

	```solidity
	    event IncreaseLiquidity(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);
	```

- Found in src/interfaces/IILOPool.sol [Line: 36](src/interfaces/IILOPool.sol#L36)

	```solidity
	    event DecreaseLiquidity(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);
	```

- Found in src/interfaces/IILOPool.sol [Line: 44](src/interfaces/IILOPool.sol#L44)

	```solidity
	    event Collect(uint256 indexed tokenId, address recipient, uint256 amount0, uint256 amount1);
	```

- Found in src/interfaces/IILOPool.sol [Line: 46](src/interfaces/IILOPool.sol#L46)

	```solidity
	    event ILOPoolInitialized(address indexed univ3Pool, int32 tickLower, int32 tickUpper, SaleInfo saleInfo, VestingConfig[] vestingConfig);
	```

- Found in src/interfaces/IILOPool.sol [Line: 48](src/interfaces/IILOPool.sol#L48)

	```solidity
	    event Claim(address indexed user, uint256 tokenId,uint128 liquidity, uint256 amount0, uint256 amount1, uint256 feeGrowthInside0LastX128, uint256 feeGrowthInside1LastX128);
	```

- Found in src/interfaces/IILOPool.sol [Line: 49](src/interfaces/IILOPool.sol#L49)

	```solidity
	    event Buy(address indexed investor, uint256 tokenId, uint256 raiseAmount, uint128 liquidity);
	```

- Found in src/interfaces/IILOPool.sol [Line: 50](src/interfaces/IILOPool.sol#L50)

	```solidity
	    event PoolLaunch(address indexed project, uint128 liquidity, uint256 token0, uint256 token1);
	```

- Found in src/interfaces/IILOPool.sol [Line: 51](src/interfaces/IILOPool.sol#L51)

	```solidity
	    event UserRefund(address indexed user, uint256 tokenId, uint256 raiseTokenAmount);
	```

- Found in src/interfaces/IILOPool.sol [Line: 52](src/interfaces/IILOPool.sol#L52)

	```solidity
	    event ProjectRefund(address indexed projectAdmin, uint256 saleTokenAmount);
	```

- Found in src/interfaces/IILOWhitelist.sol [Line: 7](src/interfaces/IILOWhitelist.sol#L7)

	```solidity
	    event SetWhitelist(address indexed user, bool isWhitelist);
	```

- Found in src/interfaces/IILOWhitelist.sol [Line: 8](src/interfaces/IILOWhitelist.sol#L8)

	```solidity
	    event SetOpenToAll(bool openToAll);
	```

</details>

## L-27: Empty `require()` / `revert()` statements

Use descriptive reason strings or custom errors for revert paths.

<details><summary>8 Found Instances</summary>


- Found in src/ILOPool.sol [Line: 241](src/ILOPool.sol#L241)

	```solidity
	            require(positionLiquidity >= liquidity2Claim);
	```

- Found in src/base/Initializable.sol [Line: 13](src/base/Initializable.sol#L13)

	```solidity
	        require(!_initialized);
	```

- Found in src/base/Initializable.sol [Line: 18](src/base/Initializable.sol#L18)

	```solidity
	        require(_initialized);
	```

- Found in src/base/LiquidityManagement.sol [Line: 25](src/base/LiquidityManagement.sol#L25)

	```solidity
	        require(msg.sender == _cachedUniV3PoolAddress);
	```

- Found in src/base/Multicall.sol [Line: 18](src/base/Multicall.sol#L18)

	```solidity
	                if (result.length < 68) revert();
	```

- Found in src/libraries/LiquidityAmounts.sol [Line: 15](src/libraries/LiquidityAmounts.sol#L15)

	```solidity
	        require((y = uint128(x)) == x);
	```

- Found in src/libraries/PoolAddress.sol [Line: 34](src/libraries/PoolAddress.sol#L34)

	```solidity
	        require(key.token0 < key.token1);
	```

- Found in src/libraries/SqrtPriceMathPartial.sol [Line: 32](src/libraries/SqrtPriceMathPartial.sol#L32)

	```solidity
	        require(sqrtRatioAX96 > 0);
	```

</details>

## L-28: Using `ERC721::_mint()` can be dangerous

Using `ERC721::_mint()` can mint ERC721 tokens to addresses which don't support ERC721 tokens. Use `_safeMint()` instead of `_mint()` for ERC721.

<details><summary>2 Found Instances</summary>


- Found in src/ILOPool.sol [Line: 161](src/ILOPool.sol#L161)

	```solidity
	            _mint(recipient, (tokenId = _nextId++));
	```

- Found in src/ILOPool.sol [Line: 404](src/ILOPool.sol#L404)

	```solidity
	            _mint(projectConfig.recipient, (tokenId = _nextId++));
	```

</details>

## L-29: Modifiers invoked only once can be shoe-horned into the function

<details><summary>1 Found Instances</summary>


- Found in src/base/Initializable.sol [Line: 17](src/base/Initializable.sol#L17)

	```solidity
	    modifier afterInitialize() {
	```

</details>

## L-30: Large literal values multiples of 10000 can be replaced with scientific notation

Use `e` notation, for example: `1e18`, instead of its full numeric value.

<details><summary>3 Found Instances</summary>


- Found in src/base/ILOPoolImmutableState.sol [Line: 13](src/base/ILOPoolImmutableState.sol#L13)

	```solidity
	    uint16 constant BPS = 10000;
	```

- Found in src/base/ILOVest.sol [Line: 26](src/base/ILOVest.sol#L26)

	```solidity
	        uint16 BPS = 10000;
	```

- Found in src/base/ILOVest.sol [Line: 47](src/base/ILOVest.sol#L47)

	```solidity
	        uint16 BPS = 10000;
	```

</details>

## L-31: Internal functions called only once can be inlined

Instead of separating the logic into a separate function, consider inlining the logic into the calling function. This can reduce the number of function calls and improve readability.

<details><summary>1 Found Instances</summary>


- Found in src/base/LiquidityManagement.sol [Line: 41](src/base/LiquidityManagement.sol#L41)

	```solidity
	    function addLiquidity(AddLiquidityParams memory params)
	```

</details>

## L-32: Contract still has TODOs

Contract contains comments with TODOS

<details><summary>2 Found Instances</summary>


- Found in src/interfaces/IILOManager.sol [Line: 8](src/interfaces/IILOManager.sol#L8)

	```solidity
	interface IILOManager {
	```

- Found in src/interfaces/IILOPool.sol [Line: 16](src/interfaces/IILOPool.sol#L16)

	```solidity
	interface IILOPool is
	```
</details>

## L-33: Unused Custom Error

it is recommended that the definition be removed when custom error is unused

<details><summary>1 Found Instances</summary>


- Found in src/interfaces/IILOWhitelist.sol [Line: 16](src/interfaces/IILOWhitelist.sol#L16)

	```solidity
	    modifier onlyProjectAdmin virtual;
	```

</details>

## L-34: Unprotected initializer

Consider protecting the initializer functions with modifiers.

<details><summary>5 Found Instances</summary>


- Found in src/base/Initializable.sol [Line: 8](src/base/Initializable.sol#L8)

	```solidity
	    function _disableInitialize() internal {
	```

- Found in src/interfaces/IILOManager.sol [Line: 52](src/interfaces/IILOManager.sol#L52)

	```solidity
	    function initProject(InitProjectParams calldata params) external returns(address uniV3PoolAddress);
	```

- Found in src/interfaces/IILOManager.sol [Line: 72](src/interfaces/IILOManager.sol#L72)

	```solidity
	    function initILOPool(InitPoolParams calldata params) external returns(address iloPoolAddress);
	```

- Found in src/interfaces/IILOManager.sol [Line: 86](src/interfaces/IILOManager.sol#L86)

	```solidity
	    function initialize(
	```

- Found in src/interfaces/IILOPool.sol [Line: 103](src/interfaces/IILOPool.sol#L103)

	```solidity
	    function initialize(InitPoolParams calldata initPoolParams) external;
	```

</details>


# Informationals

## Informational-01: ILOManager should use days

In the `ILOManager` DEFAULT_DEADLINE_OFFSET should be defined with small letters, because it's not a constant or immutable value.

## Impact

Using all uppercase letters for `DEFAULT_DEADLINE_OFFSET` can imply that it is a constant or immutable value. This can lead to confusion among developers, who may mistakenly believe that this value should not be changed during runtime.

## Recommended Mitigation Steps

Consider writing the name as defaultDeadlineOffset and also assign the value to `7days`. 

## Informational-02: Eth is send using transfer

In the `Whitelist::receive` function, ETH is returned to the user using the `transfer` function.

## Impact

Using `transfer` for sending ETH has inherent risks of reentrancy vulnerabilities. It is recommended to use `send` in combination with a reentrancy guard. More details on safer practices can be found [here](https://solidity-by-example.org/sending-ether/).

## Recommended Mitigation Steps

Consider employing the `call` function with a reentrancy guard to securely manage ETH transactions.

## Informational-03: No documentation

In `ILOWhitelist`, it is noted that documentation for the methods in `IILOWhitelist` is missing.

## Impact

Lack of documentation for interface methods (`IILOWhitelist`) can lead to ambiguity and misunderstanding among developers who utilize or implement these methods. This can result in inefficient integration, potential errors, or insecure implementations.

## Recommended Mitigation Steps

Add documentation in `IILOWhitelist`.

## Informational-04: State varaibles names

In `ILOPoolImmutableState`, all variables are in capital letters despite not being immutable or constant, which contradicts Solidity best practices.

## Impact

Capitalized variable names suggest immutability or constant values, potentially misleading developers and complicating code understanding.

## Recommended Mitigation Steps

Adopt Solidity's naming conventions: use lowercase (camelCase) for state variables, all caps (UPPER_CASE) for constants, and camelCase for immutable variables.

## Informational-05: Enumerable set

In `ILOWhitelist`, the use of `EnumerableSet` for managing sets implies that add and remove operations will return false if the entry is not already present in the set. 

## Impact

1. **Return Behavior**: Operations like adding or removing entries from the set will return false if the entry does not exist, impacting the control flow and error handling in your contract.
    
2. **Enumeration Complexity**: Elements in `EnumerableSet` are enumerated in O(n) time complexity. The ordering of elements is not guaranteed.

## Informational-06: Safe transfer will not work with tether gold

The `safeTransferFrom` function, designed for safe token transfers, encounters issues with tokens such as Tether Gold. These tokens declare a `bool` return type but inconsistently return `false` even when transfers are successful. This inconsistency poses a challenge for the function's reliability and requires a special case to ensure proper handling.

## Impact

The current implementation's inability to handle tokens like Tether Gold results in:

- **Incorrect Transfer Handling:** Tokens that return `false` on successful transfers may lead the function to incorrectly assume a transfer failed, impacting transaction outcomes.
- **Contract Interoperability:** Inconsistent token behavior can affect how smart contracts interact with various tokens, potentially causing unexpected errors or failures.
- **User Experience:** Users relying on `safeTransferFrom` may experience failed transactions or delays due to incorrect assumptions about transfer success.

## Recommended Mitigation Steps

To address the issue, implement a special case for tokens like Tether Gold in the `safeTransferFrom` function:

```solidity
if (address(token) == address(tetherGoldToken)) { 
  require(token.balanceOf(to) >= amount, "Transfer did not succeed"); 
}
```

## Informational-07: Multicall can be more safer

To improve the safety and functionality of your `multicall` function, consider reviewing this blog post: [https://matink.me/solidity/2023/10/01/multicall-in-solidity/](https://matink.me/solidity/2023/10/01/multicall-in-solidity/). This resource provides valuable insights into optimizing `multicall` implementations in Solidity.

## Impact
The blog post outlines crucial strategies for enhancing the security and reliability of `multicall` functions. It discusses potential vulnerabilities and suggests best practices to mitigate risks associated with batch transactions.

## Recommended Mitigation Steps
Implement the recommended techniques from the blog post. These steps can significantly reduce the likelihood of errors and improve the overall robustness of your smart contract.

## Informational-08: Claim function is payable in the interface

`IILOPool::claim` is declared as payable in the interface, but in the implementation is not payable, which is the expected behaviour stated by team. Consider removing the payable keyword from the interface.
