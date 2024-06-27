# QA for Vultisig

## Table of Contents

| Issue ID | Description |
| -------- | ----------- |
| [QA-01](#qa-01-potential-eth-lockup-in-whitelist-contract-due-to-insufficient-gas-forwarding-with-transfer) | Potential ETH Lockup in Whitelist Contract Due to Insufficient Gas Forwarding with `transfer()` |
| [QA-02](#qa-02-uniswapv3oracle-is-to-be-deployed-on-multiple-chains-but-does-not-consider-the-sequencer-going-down) | `UniswapV3Oracle` is to be deployed on multiple chains but does not consider the sequencer going down |
| [QA-03](#qa-03-vesting-schedule-assignment-in-buy-function-leads-to-all-new-positions-having-the-same-vesting-schedule) | Vesting schedule assignment in `buy` function leads to all new positions having the same vesting schedule |
| [QA-04](#qa-04-wrap-the-addliquidity-call-in-a-trycatch-block) | Wrap the `addLiquidity` call in a try/catch block |
| [QA-05](#qa-05-absence-of-proper-validation-in-_validatevestschedule-function-allows-empty-vesting-schedule-leading-to-revert) | Absence of Proper Validation in `_validateVestSchedule` Function Allows Empty Vesting Schedule, Leading to Revert |
| [QA-06](#qa-06-missing-return-value-in-multicall-function-causes-loss-of-results) | Missing Return Value in `multicall` Function Causes Loss of Results |
| [QA-07](#qa-07-newly-minted-positions-lack-initialized-fee-growth-values-leading-to-incorrect-fee-calculations-during-token-claims) | Newly minted positions lack initialized fee growth values, leading to incorrect fee calculations during token claims |
| [QA-08](#qa-08-vesting-schedule-validation-logic-issue-allowing-invalid-schedules) | Vesting Schedule Validation Logic Issue Allowing Invalid Schedules |
| [QA-09](#qa-09-transfers-might-fail-silently) | Transfers might fail silently |
| [QA-10](#qa-10-exact-pool-price-match-requirement-in-launch-function-may-prevent-project-launch-due-to-market-price-fluctuations) | Exact pool price match requirement in `launch` function may prevent project launch due to market price fluctuations |
| [QA-11](#qa-11-some-erc20-tokens-have-implementations-only-on-part-of-the-target-chains) | Some ERC20 tokens have implementations only on part of the target chains |
| [QA-12](#qa-12-inefficient-handling-of-weth9-payments-due-to-overlooked-token-balance-check) | Inefficient Handling of `WETH9` Payments Due to Overlooked Token Balance Check |
| [QA-13](#qa-13-unchecked-arithmetic-operations-in-fullmath-and-tickmath-libraries-leading-to-potential-overflows-and-unexpected-behavior) | Unchecked Arithmetic Operations in FullMath and TickMath Libraries Leading to Potential Overflows and Unexpected Behavior |
| [QA-14](#qa-14-incorrect-order-of-token-transfers-in-the-claim-function-may-lead-to-stuck-fees) | Incorrect order of token transfers in the `claim` function may lead to stuck fees |
| [QA-15](#qa-15-pausable-and-blacklistable-tokens-like-usdc-usdt-can-disrupt-critical-ilopool-functions) | Pausable and Blacklistable Tokens like USDC & USDT Can Disrupt Critical `ILOPool` Functions |
| [QA-16](#qa-16-duplicate-addresses-in-batchremovewhitelist-may-lead-to-inconsistent-event-emission-and-unnecessary-gas-consumption) | Duplicate Addresses in `batchRemoveWhitelist` May Lead to Inconsistent Event Emission and Unnecessary Gas Consumption |
| [QA-17](#qa-17-potential-logic-issue-in-_addwhitelistedaddress-function-allowing-blacklisted-addresses-to-be-whitelisted) | Potential Logic Issue in `_addWhitelistedAddress` Function Allowing Blacklisted Addresses to be Whitelisted |
| [QA-18](#qa-18-misleading-comment-regarding-slippage-calculation-in-uniswapv3oracle-contract) | Misleading Comment Regarding Slippage Calculation in UniswapV3Oracle Contract |
| [QA-19](#qa-19-vesting-schedule-overlap-issue-in-_validatevestschedule-function) | Vesting Schedule Overlap Issue in `_validateVestSchedule` Function |




## [QA-01] Potential ETH Lockup in Whitelist Contract Due to Insufficient Gas Forwarding with `transfer()`

### Impact
The `Whitelist` contract uses `transfer()` to send back ETH to users who self-whitelist. `transfer()` only forwards 2300 gas, which is insufficient for contracts with non-trivial `receive()` or `fallback` functions. This can cause ETH transfers to fail and result in funds being locked in the contract, especially for users interacting via multisig wallets or other smart contracts.

### Proof of Concept
The `receive()` function in the `Whitelist` contract sends back ETH using `transfer()`:

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L65-L73

```solidity
receive() external payable {
    if (_isSelfWhitelistDisabled) {
        revert SelfWhitelistDisabled();
    }
    if (_isBlacklisted[_msgSender()]) {
        revert Blacklisted();
    }
    _addWhitelistedAddress(_msgSender());
    payable(_msgSender()).transfer(msg.value);
}
```
If the recipient contract requires more than 2300 gas, the transfer will fail, locking the ETH in the `Whitelist` contract.

### Recommended Mitigation Steps
Replace `.transfer` with `.call` to forward all available gas, ensuring the recipient contract can execute its logic.




## [QA-02] `UniswapV3Oracle` is to be deployed on multiple chains but does not consider the sequencer going down

### Proof of Concept
First note that the protocol, including the `ILOManager` and other related contracts, is to be deployed on multiple chains as hinted by the sponsor in the general Discord channel:

**Question asked by a warden:**
```
Is ILOManager and other related contracts going to be deployed in different chains? For example, the chains that have UniSwap in them:

Ethereum
Arbitrum
Optimism
Polygon
Base
BNB
Avalanche C-Chain
CELO
Blast
```

**Sponsor's reply:**
```
Yes, would be all of them
```

This list includes multiple optimistic L2s, and with optimistic L2s like Arbitrum, Optimism, Base, and Blast, the sequencer could indeed go down, which then leads us to the issue with the timing logics across the protocol.

This in short breaks multiple/any timing logics for the L2 to-deploy contracts, keep in mind that in instances where the L2 goes down, the time still counts.

Take a look at this: [`UniswapV3Oracle.sol`](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L39-L46)

```solidity
    function peek(uint256 baseAmount) external view returns (uint256) {
        // Check if the sequencer is up
        (, int256 answer, uint256 startedAt, , ) = sequencerUptimeFeed.latestRoundData();
        require(answer == 0, "Sequencer is down");

        uint32 longestPeriod = OracleLibrary.getOldestObservationSecondsAgo(pool);
        uint32 period = PERIOD < longestPeriod ? PERIOD : longestPeriod;
        int24 tick = OracleLibrary.consult(pool, period);
        uint256 quotedWETHAmount = OracleLibrary.getQuoteAtTick(tick, BASE_AMOUNT, baseToken, WETH);
        // Apply 5% slippage
        return (quotedWETHAmount * baseAmount * 95) / 1e20; // 100 / 1e18
    }
}
```

We can see that this is the logic for getting the `TWAP` price and it queries prices from the Uniswap V3 pool. However, one thing with using Uniswap V3 on L2 chains is that there is a need to check if the sequencer is down to avoid prices from looking like they are fresh although they are not. The bug could be leveraged by malicious actors to take advantage of the sequencer downtime.

### Impact
Core functionalities across the protocol would be broken on L2 chains where the networks could be down for a while. This could lead to incorrect price calculations and potential exploitation by malicious actors.

### Recommended Mitigation Steps
Consider reimplementing the timing logics on the L2 side of the protocol to take into account the fact that the sequencer could indeed be down. Add a grace time after the L2 sequencer comes back online for core functions.

Additionally, since Chainlink recommends that all Optimistic L2 oracles consult the Sequencer Uptime Feed to ensure that the sequencer is live before trusting the data returned by the oracle, introduce a sequencer check to ensure that the sequencer is active and prices returned are accurate. See here: https://docs.chain.link/data-feeds#l2-sequencer-uptime-feeds



## [QA-03] Vesting schedule assignment in `buy` function leads to all new positions having the same vesting schedule

### Impact
>Borderline Medium/Low. This could be upgraded if the judge deems it fit.

All new investor positions will be assigned the same vesting schedule, regardless of the investor or the current state of the sale. This may lead to incorrect vesting allocations and could potentially cause issues.

### Proof of Concept
In the `buy` function, when a new position is minted for an investor who doesn't already have a position, the vesting schedule is assigned using `_vestingConfigs[0]` without considering any investor-specific criteria:

Take a look at this part of the code: https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L143-L148

```solidity
        if (balanceOf(recipient) == 0) {
            _mint(recipient, (tokenId = _nextId++));
@>            _positionVests[tokenId].schedule = _vestingConfigs[0].schedule;
        } else {
            tokenId = tokenOfOwnerByIndex(recipient, 0);
        }
```

This means that all new positions will be assigned the same vesting schedule, which is likely not the intended behavior. 
Instead, the vesting schedule should probably be determined based on some criteria specific to the investor or the current state of the sale. For example, there could be different vesting schedules based on the amount raised, the time of the purchase, or the investor's tier.

Additionally, the function doesn't check if `_vestingConfigs` is empty before accessing `_vestingConfigs[0]`, which could lead to an index out of bounds error if `_vestingConfigs` is empty.

### Recommended Mitigation Steps
1. Update the logic for assigning the vesting schedule to consider appropriate criteria (e.g., amount raised, time of purchase, investor tier) and select the correct vesting schedule from `_vestingConfigs`.
2. Add a check to ensure `_vestingConfigs` is not empty before accessing its elements to get rid of potential index out of bounds errors.




## [QA-04] Wrap the `addLiquidity` call in a try/catch block

### Impact
If the `addLiquidity` call fails during launch, the contract state will still be updated as if the launch succeeded, minting NFTs, assigning vesting, and marking the launch status as succeeded despite no liquidity being added. This could lead to incorrect accounting and distribution of tokens.

### Proof of Concept
In the `launch` function, after the `addLiquidity` call, the following code is executed regardless of whether `addLiquidity` succeeded or not:

Look at this part of the code: https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L309-L336
```solidity
// assigning vests for the project configuration
for (uint256 index = 1; index < _vestingConfigs.length; index++) {
    uint256 tokenId;
    VestingConfig memory projectConfig = _vestingConfigs[index];
    // mint nft for recipient
    _mint(projectConfig.recipient, (tokenId = _nextId++));
    uint128 liquidityShares = uint128(FullMath.mulDiv(liquidity, projectConfig.shares, BPS));

    Position storage _position = _positions[tokenId];
    _position.liquidity = liquidityShares;
    _positionVests[tokenId].totalLiquidity = liquidityShares;

    // assign vesting schedule 
    LinearVest[] storage schedule = _positionVests[tokenId].schedule;
    for (uint256 i = 0; i < projectConfig.schedule.length; i++) {
        schedule.push(projectConfig.schedule[i]);
    }

    emit Buy(projectConfig.recipient, tokenId, 0, liquidityShares);
}

// transfer back leftover sale token to project admin
_refundProject(_project.admin);

_launchSucceeded = true;
```
This will mint NFTs, assign vesting, refund the project, and mark the launch as succeeded, even if no liquidity was actually added to the Uniswap pool.

### Recommended Mitigation Steps
Wrap the `addLiquidity` call in a `try/catch` block. Only if `addLiquidity` succeeds should the subsequent launch logic (minting NFTs, assigning vesting, updating launch status) be executed. If `addLiquidity` fails, the function should revert without updating any other contract state.




## [QA-05] Absence of Proper Validation in `_validateVestSchedule` Function Allows Empty Vesting Schedule, Leading to Revert

### Impact
The `_validateVestSchedule` function allows the possibility of having a vesting schedule with no shares at all. This can cause the function to revert, preventing the contract from functioning properly.

### Proof of Concept
The issue lies in the `_validateVestSchedule` function. If the `schedule` array is empty, the loop will not execute, and `totalShares` will remain 0. The final requirement `require(totalShares == BPS, "VS");` will always fail because `totalShares` is 0 and `BPS` is 10000.

Look at this part of the code: https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/ILOVest.sol#L35-L53

```solidity
function _validateVestSchedule(uint64 launchTime, LinearVest[] memory schedule) internal pure {
    require(schedule[0].start >= launchTime, "VT");
    uint16 BPS = 10000;
    uint16 totalShares;
    uint64 lastEnd;
    uint256 scheduleLength = schedule.length;
    for (uint256 i = 0; i < scheduleLength; i++) {
        // vesting schedule must not overlap
        require(schedule[i].start >= lastEnd, "VT");
        lastEnd = schedule[i].end;
        // we need to subtract first in order to avoid int overflow
        require(BPS - totalShares >= schedule[i].shares, "VS");
        totalShares += schedule[i].shares;
    }
    // total shares should be exactly equal BPS
    require(totalShares == BPS, "VS");
}
```

Scenario:
1. Call `_validateVestSchedule` with an empty `schedule` array.
2. The loop will not execute, and `totalShares` will remain 0.
3. The final requirement `require(totalShares == BPS, "VS");` will fail, causing the function to revert.

### Recommended Mitigation Steps
Add a check at the beginning of the `_validateVestSchedule` function to ensure that the `schedule` array is not empty.

```diff
function _validateVestSchedule(uint64 launchTime, LinearVest[] memory schedule) internal pure {
+    require(schedule.length > 0, "Empty vesting schedule");
    require(schedule[0].start >= launchTime, "VT");
    uint16 BPS = 10000;
    uint16 totalShares;
    uint64 lastEnd;
    uint256 scheduleLength = schedule.length;
    for (uint256 i = 0; i < scheduleLength; i++) {
        // vesting schedule must not overlap
        require(schedule[i].start >= lastEnd, "VT");
        lastEnd = schedule[i].end;
        // we need to subtract first in order to avoid int overflow
        require(BPS - totalShares >= schedule[i].shares, "VS");
        totalShares += schedule[i].shares;
    }
    // total shares should be exactly equal BPS
    require(totalShares == BPS, "VS");
}
```






## [QA-06] Missing Return Value in `multicall` Function Causes Loss of Results

### Impact
The `multicall` function executes multiple method calls in a single transaction and return the results of these calls. However, the current implementation does not return the `results` array, causing the caller to lose access to the results of the executed calls. This can lead to significant issues, especially if the caller relies on the results for further processing or decision-making.

### Proof of Concept
Look at this part of the code: https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/Multicall.sol#L11-L29

```solidity
function multicall(bytes[] calldata data) public payable override returns (bytes[] memory results) {
    results = new bytes[](data.length);
    for (uint256 i = 0; i < data.length; i++) {
        (bool success, bytes memory result) = address(this).delegatecall(data[i]);

        if (!success) {
            if (result.length < 68) revert();
            assembly {
                result := add(result, 0x04)
            }
            revert(abi.decode(result, (string)));
        }

        results[i] = result;
    }
@>    // Missing return statement
}
```

The `multicall` function initializes an array `results` to store the results of each call. It then iterates over the input `data` array, performing a `delegatecall` for each item and storing the result in the `results` array. However, the function does not include a `return results;` statement at the end, which means the `results` array is never returned to the caller.


### Recommended Mitigation Steps
Add a `return results;` statement at the end of the `multicall` function to ensure the results are returned to the caller. 

```diff
function multicall(bytes[] calldata data) public payable override returns (bytes[] memory results) {
    results = new bytes[](data.length);
    for (uint256 i = 0; i < data.length; i++) {
        (bool success, bytes memory result) = address(this).delegatecall(data[i]);

        if (!success) {
            if (result.length < 68) revert();
            assembly {
                result := add(result, 0x04)
            }
            revert(abi.decode(result, (string)));
        }

        results[i] = result;
    }
+   return results;
}
```





## [QA-07] Newly minted positions lack initialized fee growth values, leading to incorrect fee calculations during token claims

### Impact
Users who receive newly minted positions during the `launch` function may experience incorrect fee calculations when they claim their tokens. This can result in users receiving inaccurate amounts of fees and potentially losing out on earned rewards.

### Proof of Concept
In the `launch` function, when new NFTs are minted and vesting schedules are assigned for the project configuration, the `feeGrowthInside0LastX128` and `feeGrowthInside1LastX128` values are not initialized for these newly minted positions.

Look at this part of the code:

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L310-L329

```solidity
// assigning vests for the project configuration
for (uint256 index = 1; index < _vestingConfigs.length; index++) {
    uint256 tokenId;
    VestingConfig memory projectConfig = _vestingConfigs[index];
    // mint nft for recipient
    _mint(projectConfig.recipient, (tokenId = _nextId++));
    uint128 liquidityShares = uint128(FullMath.mulDiv(liquidity, projectConfig.shares, BPS));

    Position storage _position = _positions[tokenId];
    _position.liquidity = liquidityShares;
    _positionVests[tokenId].totalLiquidity = liquidityShares;

    // assign vesting schedule
    LinearVest[] storage schedule = _positionVests[tokenId].schedule;
    for (uint256 i = 0; i < projectConfig.schedule.length; i++) {
        schedule.push(projectConfig.schedule[i]);
    }

    emit Buy(projectConfig.recipient, tokenId, 0, liquidityShares);
}
```

In the `claim` function, the `feeGrowthInside0LastX128` and `feeGrowthInside1LastX128` values are used to calculate the amount of fees generated by a position. If these values are not initialized correctly for the newly minted positions, the fee calculations will be incorrect.

Consider a scenario;
1. The `launch` function is called, and new NFTs are minted for project recipients with vesting schedules.
2. The `feeGrowthInside0LastX128` and `feeGrowthInside1LastX128` values are not initialized for these newly minted positions.
3. Users with these newly minted positions call the `claim` function to claim their tokens and fees.
4. The `claim` function calculates the fees based on the uninitialized `feeGrowthInside0LastX128` and `feeGrowthInside1LastX128` values, resulting in incorrect fee amounts.
5. Users receive inaccurate fees.

### Recommended Mitigation Steps
Retrieve the current values of `feeGrowthInside0LastX128` and `feeGrowthInside1LastX128` from the Uniswap V3 pool and assign them to the newly minted positions during the `launch` function. Thiswill make sure that the fee calculations are accurate when users claim their tokens. The `launch` function should be updated to include the initialization of these values for each newly minted position.






## [QA-08] Vesting Schedule Validation Logic Issue Allowing Invalid Schedules

### Impact
The current implementation of the `_validateVestSchedule` function in the `ILOVest` contract allows for the creation of invalid vesting schedules where the start time of a vesting period can be greater than its end time. This can lead to incorrect vesting calculations and distribution of tokens, potentially resulting in financial losses for users and damage to the project's reputation.

### Proof of Concept
Take a look at the `_validateVestSchedule` function:

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/ILOVest.sol#L35-L51

```solidity
function _validateVestSchedule(uint64 launchTime, LinearVest[] memory schedule) internal pure {
    require(schedule[0].start >= launchTime, "VT");
    uint16 BPS = 10000;
    uint16 totalShares;
    uint64 lastEnd;
    uint256 scheduleLength = schedule.length;
    for (uint256 i = 0; i < scheduleLength; i++) {
        // vesting schedule must not overlap
        require(schedule[i].start >= lastEnd, "VT");
        lastEnd = schedule[i].end;
        // ...
    }
    // ...
}
```
The function checks if each vesting schedule's start time is greater than or equal to the previous schedule's end time. However, it doesn't validate if the start time of the current schedule is less than its own end time. This allows for the creation of vesting schedules where the start time is greater than the end time, which is logically incorrect.

For example, a vesting schedule with the following values would pass the current validation:
```solidity
LinearVest[] memory schedule = [
    LinearVest({start: 1000, end: 500, shares: 5000}),
    LinearVest({start: 1500, end: 2000, shares: 5000})
];
```
In this case, the first vesting period has a start time (1000) greater than its end time (500), which is invalid but passes the current validation.

### Recommended Mitigation Steps
Consider adding an additional check within the `_validateVestSchedule` function to ensure that each vesting schedule's start time is less than or equal to its end time. By adding the line `require(schedule[i].start <= schedule[i].end, "VT");`, the function will prevent the creation of invalid vesting schedules where the start time is greater than the end time.


```diff
function _validateVestSchedule(uint64 launchTime, LinearVest[] memory schedule) internal pure {
    require(schedule[0].start >= launchTime, "VT");
    uint16 BPS = 10000;
    uint16 totalShares;
    uint64 lastEnd;
    uint256 scheduleLength = schedule.length;
    for (uint256 i = 0; i < scheduleLength; i++) {
        // vesting schedule must not overlap
        require(schedule[i].start >= lastEnd, "VT");
+       require(schedule[i].start <= schedule[i].end, "VT");
        lastEnd = schedule[i].end;
        // ...
    }
    // ...
}
```





## [QA-09] Transfers might fail silently


### Impact
Failed transfers would be assume as not failed.

### Proof of Concept

The protocol in `safeTransferETH` function attempts to transfer ETH to a recipient address using the `call` method, but it does not check if the recipient address is valid or has code before making the transfer.

Take a loot at this part of the code:

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/libraries/TransferHelper.sol#L52-L59

```solidity
/// @notice Transfers ETH to the recipient address
    /// @dev Fails with `STE`
    /// @param to The destination of the transfer
    /// @param value The value to be transferred
    function safeTransferETH(address to, uint256 value) internal {
        (bool success, ) = to.call{value: value}(new bytes(0));
        require(success, 'STE');
    }
```

As you can see, it directly calls `to.call{value: value}(new bytes(0))` without verifying if the `to` address is a valid, non-zero address or if it has any code. If the `to` address is invalid or doesn't have code, the transfer will fail silently, and the function will continue execution.

 Below is a minimalistic POC to prove this bug case:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.21;
import "hardhat/console.sol";
contract test {
constructor() {
bytes memory txData*; (bool success,) = payable(address(0)).call{ value: 0 }(txData*); console.log("success",success);
}
}
```

### Recommended Mitigation Steps
Consider introducing a valid address checker before the transfers are executed.




## [QA-10] Exact pool price match requirement in `launch` function may prevent project launch due to market price fluctuations

### Impact
The current implementation of the `launch` function requires an exact match between the current pool price and the initial pool price. This strict requirement may prevent the project from being launched if the pool price has deviated even slightly from the initial price due to market activities or price fluctuations. As a result, the project may fail to launch even if all other conditions are met, causing inconvenience and potential loss of opportunities for the project administrators and participants.


### Proof of Concept
Look at this part of the code:
https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L187-L198

```solidity
function launch(address uniV3PoolAddress) external override {
    require(block.timestamp > _cachedProject[uniV3PoolAddress].launchTime, "LT");
    (uint160 sqrtPriceX96, , , , , , ) = IUniswapV3Pool(uniV3PoolAddress).slot0();
    require(_cachedProject[uniV3PoolAddress].initialPoolPriceX96 == sqrtPriceX96, "UV3P");
    // ...
}
```

Most especially in this line: `require(_cachedProject[uniV3PoolAddress].initialPoolPriceX96 == sqrtPriceX96, "UV3P");`, which requires an exact match between the current pool price (`sqrtPriceX96`) and the initial pool price (`initialPoolPriceX96`).

Let's imagine:
1. A protocol is initialized with an initial pool price of 1000 (in terms of `sqrtPriceX96`).
2. Between the protocol initialization and the intended launch time, the pool price fluctuates due to market activities and reaches 1005.
3. When the admin attempts to launch the project using the `launch` function, it fails because the current pool price (1005) does not exactly match the initial pool price (1000), even though the price deviation is relatively small.

### Recommended Mitigation Steps
Instead of requiring an exact match, introduce an acceptable price range or tolerance for the pool price at the time of launching the project. Something like a minimum and maximum acceptable prices based on the initial pool price and a predefined deviation percentage (e.g., ±1%).





## [QA-11] Some ERC20 tokens have implementations only on part of the target chains

### Impact
Though the likelihood of unsupported implementations appearing is low the potential impact, e.g. asset losses, is high.


### Proof of Concept
As hinted by the sponsor in the general discord channel, `ILOManager`  and other related contracts going to be deployed on different chains.

Question asked by a warden: 

```
Is ILOManager  and other related contracts going to be deployed in different chains? For example, the chains that have UniSwap in them:

Ethereum
Arbitrum
Optimism
Polygon
Base
BNB
Avalanche C-Chain
CELO
Blast
```

And the sponsor replied:

```
Yes, would be all of them
```

Now, it's worthy to note that the [READMe](https://github.com/code-423n4/2024-06-vultisig#general-questions) explicitly states that the protocol will make use of all ERC20 tokens such as USDT, USDC, LINK and WETH, and target deployment chains listed above.

Unfortunately only WETH token has implementations on all listed chains currently.

In turn LINK and USDC have no implementations on Blast chain (https://docs.chain.link/resources/link-token-contracts, https://www.circle.com/en/multi-chain-usdc).

USDT has no trusted implementations on Base and Blast chains (https://basescan.org/tokens , https://blastscan.io/tokens).

Since the implementations are absent no one can guarantee the protocol can integrate with them.

### Recommended Mitigation Steps
Consider crosschecking the list of supported tokens on Base and Blast chains according to the provided information before deployment.





## [QA-12] Inefficient Handling of `WETH9` Payments Due to Overlooked Token Balance Check

### Impact
The current implementation of the `pay` function may lead to inefficient use of WETH9 tokens, potentially causing unnecessary reverts or additional gas costs when the contract has sufficient WETH9 tokens but not enough Ether.

### Proof of Concept
Look at this part of the code: https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/PeripheryPayments.sol#L21-L40
```solidity
function pay(
    address token,
    address payer,
    address recipient,
    uint256 value
) internal {
    if (token == WETH9 && address(this).balance >= value) {
        // pay with WETH9
        IWETH9(WETH9).deposit{value: value}(); // wrap only what is needed to pay
        IWETH9(WETH9).transfer(recipient, value);
    } else if (payer == address(this)) {
        // pay with tokens already in the contract (for the exact input multihop case)
        TransferHelper.safeTransfer(token, recipient, value);
    } else {
        // pull payment
        TransferHelper.safeTransferFrom(token, payer, recipient, value);
    }
}
```

The condition `address(this).balance >= value` checks if the contract's balance in Ether is sufficient to cover the payment when dealing with WETH9. Albeit, this does not account for the scenario where the contract might have WETH9 tokens already available. If the contract has WETH9 tokens but not enough Ether, the function will not use the available WETH9 tokens and will instead attempt to pull the payment from the payer.


### Recommended Mitigation Steps
Update the `pay` function to also check the contract's balance of WETH9 tokens. If the contract has enough WETH9 tokens, it should use those tokens to make the payment. 





## [QA-13] Unchecked Arithmetic Operations in FullMath and TickMath Libraries Leading to Potential Overflows and Unexpected Behavior

### Impact

First of all, take a look at the `diffChecker` of the implementation in UniswapV3 and Vultisig here: 
- [FullMath](https://www.diffchecker.com/trLT0sGx/)
- [TickMath](https://www.diffchecker.com/dAA6bmXo/)

As seen in both links above, the `UniswapV3` contracts are wrapped in `Unchecked` blocks.

Now, the `FullMath` and `TickMath` libraries are used extensively throughout the protocol, including in critical contracts such as SqrtPriceMathPartial, LiquidityAmounts, ILOPool, OracleLibrary, and ILOManager. The lack of unchecked arithmetic operations in these libraries can lead to potential overflows, resulting in incorrect calculations.

In [`SqrtPriceMathPartial`](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/libraries/SqrtPriceMathPartial.sol#L4) and [`LiquidityAmounts`](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/libraries/LiquidityAmounts.sol#L4), the `FullMath` library is used for various calculations involving token amounts and liquidity. If an overflow occurs due to the absence of unchecked blocks, it could result in incorrect token amounts being transferred or liquidity being allocated, potentially leading to loss of funds or unfair distribution of tokens.

The [`ILOPool`](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L7) contract also relies on `FullMath` for calculations related to vesting, fee deductions, and liquidity management. Overflows in these calculations could cause incorrect vesting schedules, inaccurate fee deductions, and improper liquidity tracking, impacting the overall functionality and fairness of the ILO process.

In [`OracleLibrary`](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L4-L5), both `FullMath` and `TickMath` are used for price calculations and conversions. Overflows in these operations could lead to incorrect price quotes and oracle data.

The [`ILOManager`](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L11) contract uses `TickMath` for initializing ILO pools and validating price ranges. If overflows occur in these calculations, it could possible result in the creation of ILO pools with incorrect parameters or the acceptance of invalid price ranges, potentially affecting the logic of the ILO process.

### Proof of Concept
Here are a few relevant code snippets that demonstrate the issue:

In FullMath.sol:
```solidity
function mulDiv(uint256 a, uint256 b, uint256 denominator) internal pure returns (uint256 result) {
    // ...
    uint256 prod0; // Least significant 256 bits of the product
    uint256 prod1; // Most significant 256 bits of the product
    assembly {
        let mm := mulmod(a, b, not(0))
        prod0 := mul(a, b)
        prod1 := sub(sub(mm, prod0), lt(mm, prod0))
    }
    // ...
}
```

In TickMath.sol:
```solidity
function getSqrtRatioAtTick(int24 tick) internal pure returns (uint160 sqrtPriceX96) {
    // ...
    uint256 absTick = tick < 0 ? uint256(-int256(tick)) : uint256(int256(tick));
    // ...
    if (absTick & 0x1 != 0) ratio = (ratio * 0xfffcb933bd6fad37aa2d162d1a594001) >> 128;
    if (absTick & 0x2 != 0) ratio = (ratio * 0xfff97272373d413259a46990580e213a) >> 128;
    // ...
}
```

As seen above, arithmetic operations such as `mul`, `sub`, and `>>` are used without being wrapped in unchecked blocks. This can lead to overflows if the intermediate results exceed the maximum value representable by uint256.

### Recommended Mitigation Steps

Wrap `FullMath` and `TickMath` libraries operations with unchecked block, similar to https://github.com/Uniswap/v3-core/blob/6562c52e8f75f0c10f9deaf44861847585fc8129/contracts/libraries/FullMath.sol and https://github.com/Uniswap/v3-core/blob/6562c52e8f75f0c10f9deaf44861847585fc8129/contracts/libraries/TickMath.sol respectively






## [QA-14] Incorrect order of token transfers in the `claim` function may lead to stuck fees

### Impact
If there is an issue whatsoever with the fee taker address or the transfer to the fee taker fails, the fees will be stuck in the contract, leading to incorrect fee distribution and potential loss of funds.

### Proof of Concept
In the `claim` function, the contract transfers the tokens to the user before transferring the fees to the fee taker:

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L251-L261

```solidity
// transfer token for user
TransferHelper.safeTransfer(_cachedPoolKey.token0, ownerOf(tokenId), amount0);
TransferHelper.safeTransfer(_cachedPoolKey.token1, ownerOf(tokenId), amount1);

emit Claim(ownerOf(tokenId), tokenId,liquidity2Claim, amount0, amount1, position.feeGrowthInside0LastX128, position.feeGrowthInside1LastX128);

address feeTaker = IILOManager(MANAGER).FEE_TAKER();
// transfer fee to fee taker
TransferHelper.safeTransfer(_cachedPoolKey.token0, feeTaker, amountCollected0-amount0);
TransferHelper.safeTransfer(_cachedPoolKey.token1, feeTaker, amountCollected1-amount1);
```

If the transfer to the fee taker fails or there is an issue with the fee taker address, the fees (represented by `amountCollected0-amount0` and `amountCollected1-amount1`) will remain in the contract, while the user will still receive their tokens.

### Recommended Mitigation Steps
Prioritise fee transfers before user transfers. The contract should transfer the fees to the fee taker first, and then transfer the remaining tokens to the user. This ensures that the fee taker receives the correct amount, and any remaining tokens are then transferred to the user, preventing the fees from getting stuck in the contract if there's an issue with the user's transfer.









## [QA-15] Pausable and Blacklistable Tokens like USDC & USDT Can Disrupt Critical `ILOPool` Functions

### Impact
If tokens like USDC are paused, it can block key liquidity management functions in the ILOPool contract, causing failed transactions and disrupting operations. This affects the `buy`, `claim`, and `launch` functions.

### Proof of Concept
https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol

1. In `buy`, token transfers fail if `RAISE_TOKEN` is paused, preventing participation. 
2. In `claim`, token transfers fail if pool tokens are paused or addresses are blacklisted, preventing token/liquidity claims.
3. In `launch`, adding liquidity fails if tokens are paused, preventing successful ILO launch.

### Recommended Mitigation Steps:
Add checks to ensure tokens aren't paused before transfers/approvals/liquidity ops. Consider fallbacks like transaction queuing to handle paused tokens.





## [QA-16] Duplicate Addresses in `batchRemoveWhitelist` May Lead to Inconsistent Event Emission and Unnecessary Gas Consumption

### Impact
If the `users` array passed to the `batchRemoveWhitelist` function contains duplicate addresses, the function will attempt to remove the same address from the whitelist multiple times. This can lead to inconsistent event emission, where the `SetWhitelist` event is only emitted once for each unique address, even if it appears multiple times in the `users` array. Additionally, this can result in unnecessary gas consumption, as the function will perform redundant operations for each duplicate address.

### Proof of Concept

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/ILOWhitelist.sol#L34-L37

```solidity
function batchRemoveWhitelist(address[] calldata users) external override onlyProjectAdmin {
    for (uint256 i = 0; i < users.length; i++) {
        _removeWhitelist(users[i]);
    }
}

function _removeWhitelist(address user) internal {
    EnumerableSet.remove(_whitelisted, user);
    emit SetWhitelist(user, false);
}
```

If the `users` array contains duplicate addresses, the `_removeWhitelist` function will be called multiple times for each duplicate address. However, the `EnumerableSet.remove` function only removes the address from the whitelist set once, and the `SetWhitelist` event is only emitted if the address was actually removed from the set.

### Recommended Mitigation Steps
Add a check inside the loop to only call `_removeWhitelist` if the address is currently whitelisted:

```diff
function batchRemoveWhitelist(address[] calldata users) external override onlyProjectAdmin {
    for (uint256 i = 0; i < users.length; i++) {
+       if (_isWhitelisted(users[i])) {
            _removeWhitelist(users[i]);
+       }
    }
}
```

This will ensure that the `_removeWhitelist` function is only called once for each unique whitelisted address in the `users` array.





## [QA-17] Potential Logic Issue in `_addWhitelistedAddress` Function Allowing Blacklisted Addresses to be Whitelisted

### Impact
The `_addWhitelistedAddress` function in the `Whitelist` contract does not check if an address is blacklisted before adding it to the whitelist. This could allow blacklisted addresses to be whitelisted, which contradicts the intended behavior of the contract and undermines the security and integrity of the whitelist mechanism.

### Proof of Concept
https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L232-L236

```solidity
function _addWhitelistedAddress(address whitelisted) private {
    if (_whitelistIndex[whitelisted] == 0) {
        _whitelistIndex[whitelisted] = ++_whitelistCount;
    }
}
```

The issue is that the function does not check if the address being added is blacklisted. This could allow blacklisted addresses to bypass restrictions by getting whitelisted.

### Recommended Mitigation Steps
Add a check in the `_addWhitelistedAddress` function to ensure that the address is not blacklisted before adding it to the whitelist. This will prevent blacklisted addresses from being whitelisted and maintain the integrity of the whitelist functionality.





## [QA-18] Misleading Comment Regarding Slippage Calculation in UniswapV3Oracle Contract

### Impact
The misleading code comment leads to misunderstandings about how slippage is applied to the pricing of the VULT token in terms of WETH. While the calculation itself is correct, the comment causes confusion among developers reviewing or maintaining the code. `100/1e18` will give `1e-16` not `1e20`

### Proof of Concept
Take a look at the `peek` function of the `UniswapV3Oracle` contract: https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L45

```solidity
      function peek(uint256 baseAmount) external view returns (uint256) {
          uint32 longestPeriod = OracleLibrary.getOldestObservationSecondsAgo(pool);
          uint32 period = PERIOD < longestPeriod? PERIOD : longestPeriod;
          int24 tick = OracleLibrary.consult(pool, period);
          uint256 quotedWETHAmount = OracleLibrary.getQuoteAtTick(tick, BASE_AMOUNT, baseToken, WETH);
          // Apply 5% slippage
@>       return (quotedWETHAmount * baseAmount * 95) / 1e20; // 100 / 1e18  
}
```

- The intention behind the code is to apply a 5% slippage to the quoted WETH amount for 1 VULT and then normalize the result.
- The formula `(quotedWETHAmount * baseAmount * 95) / 1e20` correctly applies the slippage and normalizes the value. However, the comment `// 100 / 1e18` is misleading and does not accurately describe the operation being performed.
- The comment suggests a division by `1e18` which is part of the normalization process but is presented in a way that could be interpreted as the entire operation, overshadowing the slippage application step.

### Recommended Mitigation Steps
The comment should be revised for accuracy and clarity.




## [QA-19] Vesting Schedule Overlap Issue in `_validateVestSchedule` Function

### Impact
The current implementation allows for contiguous vesting schedules, which may lead to unintended overlaps if the schedules are meant to be strictly non-overlapping.

### Proof of Concept
Look at the following line of the `_validateVestSchedule` function: https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/ILOVest.sol#L43
```solidity
require(schedule[i].start >= lastEnd, "VT");
```

This line enforces that each vesting schedule's start time must be greater than or equal to the end time of the previous schedule. However, this condition should be a strict inequality (`>`) instead of a greater than or equal to (`>=`) comparison.

If the start time of a vesting schedule is allowed to be equal to the end time of the previous schedule, it could lead to an overlap between the vesting schedules. This violates the comment above the line which states "vesting schedule must not overlap".

### Recommended Mitigation Steps
To fix this issue, the line should be modified to:
```solidity
require(schedule[i].start > lastEnd, "VT");
```

Using a strict inequality (`>`) ensures that each vesting schedule starts strictly after the end time of the previous schedule, preventing any overlap or contiguous schedules.
