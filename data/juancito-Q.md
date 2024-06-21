# QA Report

## L-1 - Pools can be initialized with a price outside of the expected tick ranges

There is a wrong check in `initILOPool()` here: `sqrtRatioLowerX96 < sqrtRatioUpperX96`.

```solidity
require(sqrtRatioLowerX96 < _project.initialPoolPriceX96 && sqrtRatioLowerX96 < sqrtRatioUpperX96, "RANGE");
```

https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOManager.sol#L90

This means that an ILO Pool can be initialized with a price outside of the tick range, and it will be impossible for users to buy liquidity in the ILO Pool as the slippage check in `buy()` will revert.

It can be tested by replacing [this line](https://github.com/code-423n4/2024-06-vultisig/blob/main/test/IntegrationTestBase.sol#L81) to `tickUpper: MIN_TICK_500 + 10` and run any test that launches a pool.

### Recommendation

```diff
-   require(sqrtRatioLowerX96 < _project.initialPoolPriceX96 && sqrtRatioLowerX96 < sqrtRatioUpperX96, "RANGE");
+   require(sqrtRatioLowerX96 < _project.initialPoolPriceX96 && _project.initialPoolPriceX96 < sqrtRatioUpperX96, "RANGE");
```

## L-2 - Vestings can be created with end time lower than their start time

There is no check in [`_validateVestSchedule()`](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/base/ILOVest.sol#L35) to prevent setting an `end` date before the `start` date.

This could potentially be dangerous as it could cause an [underflow](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L427) when calculating the unlocked liquidity. 

Note: With the [current implementation](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L410-L417) the underflow is not possible as it would either `break`, or return the full amount of `shares`.

### Recommendation

Verify that the `end` time for each vesting is greater than its `start` time:

```diff
    function _validateVestSchedule(uint64 launchTime, LinearVest[] memory schedule) internal pure {
        require(schedule[0].start >= launchTime, "VT");
        uint16 BPS = 10000;
        uint16 totalShares;
        uint64 lastEnd;
        uint256 scheduleLength = schedule.length;
        for (uint256 i = 0; i < scheduleLength; i++) {
            // vesting schedule must not overlap
+           require(schedule[i].end >= schedule[i].start, "VT");
            require(schedule[i].start >= lastEnd, "VT");
            lastEnd = schedule[i].end;
            // we need to subtract fist in order to avoid int overflow
            require(BPS - totalShares >= schedule[i].shares, "VS");
            totalShares += schedule[i].shares;
        }
        // total shares should be exactly equal BPS
        require(totalShares == BPS, "VS");
    }
```

## L-3 - Adversary can squat whitelist spots

`checkWhitelist()` verifies that `_whitelistIndex[to] > _allowedWhitelistIndex`:

```solidity
    if (_allowedWhitelistIndex == 0 || _whitelistIndex[to] > _allowedWhitelistIndex) {
        revert NotWhitelisted();
    }
```

https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/Whitelist.sol#L216

This works correctly while an admin whitelist is currently running.

But the problem arrives when the whitelist is disabled, and allows anyone to register as a whitelisted user:

```solidity
    receive() external payable {
@>      if (_isSelfWhitelistDisabled) {
            revert SelfWhitelistDisabled();
        }
        if (_isBlacklisted[_msgSender()]) {
            revert Blacklisted();
        }
        _addWhitelistedAddress(_msgSender());
        payable(_msgSender()).transfer(msg.value);
    }
```

https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/Whitelist.sol#L66

This allows an attacker to squat whitelist spots, as the `_allowedWhitelistIndex` may not have been updated, not allowing more users to register as whitelist addresses.

### Recommendation

Depending on the intention of the protocol, one option is to take some fee for public whitelisting, or make sure that `_allowedWhitelistIndex` is increased to its max value when setting `_isSelfWhitelistDisabled` as `false`.

## L-4 - New ILO Pools can be created and initialized after a previous launch with the same Uniswap Pool

[`ILOManager::initILOPool()`](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOManager.sol#L72) lets project owners create and initiate new ILO Pools after a successful previous launch.

Note that `launch()` requires that [all pools are launched successfully](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOManager.sol#L193-L195), which won't be possible for the new one.

## Recommendation

Prevent project owners from calling `initILOPool()` after a successful launch.

## L-5 - launchTime and refundDeadline can be initialized in the past

`launchTime` can be set to a value `< block.timestamp`, and so `refundDeadline` as well in `initProject()`. Although note that `launchTime` is validated against the `project.end` value in `ILOManager::initILOPool()` and against the vesting `start` in `ILOVest::_validateVestSchedule()`.

Also note that `refundDeadline` can overflow (as Solidity v0.7.6 is used). So a `launchTime` can be set into the far future, and overflow `refundDeadline` to be in the past.

```solidity
uint64 refundDeadline = params.launchTime + DEFAULT_DEADLINE_OFFSET;
```

https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOManager.sol#L58

### Recommendation

Validate that the launch time is in the future and that the refund deadline doesn't overflow.

## L-6 - Identical name and symbol for all pools

All ILO Pools have the same `name` and `symbol` which makes it less user friendly to navigate on offchain tools / explorers:

```solidity
function name() public pure override(ERC721, IERC721Metadata) returns (string memory) {
    return 'KRYSTAL ILOPool V1';
}

function symbol() public pure override(ERC721, IERC721Metadata) returns (string memory) {
    return 'KRYSTAL-ILO-V1';
}
```

https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L53-L59

### Recommendation

Append the name of the `SALE_TOKEN` and `RAISE_TOKEN` to them.

## L-7 - Unchecked transfer call

Note: This is different than the bot finding in [L-13](https://github.com/code-423n4/2024-06-vultisig/blob/main/4naly3er-report.md#l-13-unsafe-erc20-operations) as it mistakenly treats the `msgSender()` as an ERC20 token.

`.transfer()` might fail silently and the `msg.value` will remain in the `Whitelist` contract as its return value is not checked:

```solidity
    receive() external payable {
        if (_isSelfWhitelistDisabled) {
            revert SelfWhitelistDisabled();
        }
        if (_isBlacklisted[_msgSender()]) {
            revert Blacklisted();
        }
        _addWhitelistedAddress(_msgSender());
@>      payable(_msgSender()).transfer(msg.value);
    }
```

### Recommendation

One option can be to check the returned value. But since the contract is always returning all the `msg.value` sent, a better approach could be remove the `payable` and the `transfer`, and let users register just by calling the contract with no data `""`.

## L-8 - Sale Tokens with transfer callbacks can be used to launch refundable pools

The `ILOPOOL` contract doesn't follow the Checks-Effects-Interactions pattern, and this could be abused by a pool creator.

1. Call `launch()` with a Sale Token with callback
2. This will cal `_refundProject()` and transfer the remaining Sale Tokens to the pool creator
3. On the callback, call `claimRefund()` with a tokenId previously used to buy some tokens
4. `_refundTriggered` will be set to true in the `refundable()` modifier
5. `_launchSucceeded` will be set to true in `launch()`
6. The launched pool is now both refundable and claimable

Ref: https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L332-L334

### Recommendation

Move the `_launchSucceeded` line before the token transfer:

```diff
+   _launchSucceeded = true;

    // transfer back leftover sale token to project admin
    _refundProject(_project.admin);

-   _launchSucceeded = true;
```

## L-9 - Re-entrant implementation of whenNotInitialized

By setting `_initialized = true` below `_;`, it allows functions with the `whenNotInitialized` modifier to be re-entered, since the re-entered functions will be all executed, until all set `_initialized = true` at the end:

```solidity
    modifier whenNotInitialized() {
        require(!_initialized);
        _;
@>      _initialized = true;
    }
```

https://github.com/code-423n4/2024-06-vultisig/blob/main/src/base/Initializable.sol#L13

### Recommendation

```diff
    modifier whenNotInitialized() {
        require(!_initialized);
+       _initialized = true;
        _;
-       _initialized = true;
    }
```

## L-10 - payable modifier on a function that shouldn't receive native tokens

The `claim()` function has a `payable` modifier despite it doesn't use `msg.value`, and the contract shouldn't receive native tokens. This may lead to user errors and lost ETH, as it can't be recovered.

```solidity
    function claim(uint256 tokenId)
        external
@>      payable
        override
        isAuthorizedForToken(tokenId)
        returns (uint256 amount0, uint256 amount1)
    {
```

https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L186

### Recommendation

Consider removing the `payable` modifier

## L-11 - Missing function to calculate how much liquidity a user will get on buy() and tokens on claim()

[`buy()`](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L126) operations involve some complex [calculations](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L155-L159) to get the returned liquidity.

[`claim()`](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L184) operations depend on [how many tokens the Uniswap pool will return](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L205-L224). And also [platform fees](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L208), and [performance fees](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L227).

### Recommendation

Create view functions for users to know before hand how much liquidity or tokens they would obtain before they commit to a `buy()` or `claim()` operation blindly.

## L-12 - maxCapPerUser limit should not be enforced in public sales

A `maxCapPerUser` limit is always enforced when buying the initial liquidity via `buy()`, but this is only useful [during the whitelist period](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L133).

Once the whitelist is [Open for All](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/base/ILOWhitelist.sol#L58C15-L58C16), anyone would be able to "bypass" this limit by using another account, so the check doesn't add any protection. In fact, it is counter-productive, as it limits the operations of the users.

https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L151

### Recommendation

Change the visibility of the `_openToAll` variable to `internal` and only validate the `maxCapPerUser` when it is not open for all:

```diff
+   if (!_openToAll) {
        require(raiseAmount <= saleInfo.maxCapPerUser - _position.raiseAmount, "UC");
+   }
```