# Summary

* ## Low Severity Issues

  * **[[L-01] 24-hour whitelisted-only period could be violated](#l-01-24-hour-whitelisted-only-period-could-be-violated)**
  * **[[L-02] No minimum boundary for DEFAULT_DEADLINE_OFFSET](#l-02-no-minimum-boundary-for-default_deadline_offset)**
  * **[[L-03] Incompatible with Fee-on-transfer token](#l-03-incompatible-with-fee-on-transfer-token)**
  * **[[L-04] whitelistCount may not return the actual whitelisted number](#l-04-whitelistcount-may-not-return-the-actual-whitelisted-number)**
  * **[[L-05] The vesting allows for instant unlock](#l-05-the-vesting-allows-for-instant-unlock)**
  * **[[L-06] All Capital Letters will Cause Confusion](#l-06-all-capital-letters-will-cause-confusion)**
  * **[[L-07] whenNotInitialized Naming is inaccurate](#l-07-whennotinitialized-naming-is-inaccurate)**
  * **[[L-08] If one pool fails to raise enough funds, the whole project will fail](#l-08-if-one-pool-fails-to-raise-enough-funds-the-whole-project-will-fail)**
  * **[[L-09] Launch Time should include `launchTime`](#l-09-launch-time-should-include-launchtime)**
  * **[[L-10] initializedPools can only be added](#l-10-initializedpools-can-only-be-added)**
  * **[[L-11] getOldestObservationSecondsAgo could be small after initialization](#l-11-getoldestobservationsecondsago-could-be-small-after-initialization)**

## **[L-01] 24-hour whitelisted-only period could be violated**

- The contract tries to enforce `a 24-hour whitelisted (WL) trade-only period will be the next phase (first come, first served among the WL addresses)` according to the [doc](https://docs.vultisig.com/vultisig-token/launch#launch-liquidity). However, the contract does not trace the other pools that could be created by whitelisted buyers. In this way, the check `from == _pool` could be bypassed, and others could freely trade in other pools.

```solidity
    function checkWhitelist(address from, address to, uint256 amount) external onlyVultisig {
        if (from == _pool && to != owner()) {
        ...
        } 
}
```

### **Links to affected code**

- [Whitelist.sol#L205](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L205)


### **Recommended Mitigation Steps**

- To mitigate this issue, it is recommended to add an array to keep track of all pools, or even temporarily disable any token transfer except `from == _pool`.


## **[L-02] No minimum boundary for DEFAULT_DEADLINE_OFFSET**

- The `refundDeadline` is always set to be `params.launchTime + DEFAULT_DEADLINE_OFFSET`. However, there is no lower boundary for `DEFAULT_DEADLINE_OFFSET`. If it is set to a small value, the project may not have enough time to launch the project before a malicious user calls `claimRefund` to prevent the project from launching. Similarly, `setRefundDeadlineForProject` should also be called with care as this would trigger the same issues.

```solidity
    function setDefaultDeadlineOffset(uint64 defaultDeadlineOffset) external override onlyOwner() {
        emit DefaultDeadlineOffsetChanged(owner(), DEFAULT_DEADLINE_OFFSET, defaultDeadlineOffset);
        DEFAULT_DEADLINE_OFFSET = defaultDeadlineOffset;
    }
```

### **Links to affected code**

- [ILOManager.sol#L175-L178](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L175-L178)
- [ILOManager.sol#L58](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L58)

### **Recommended Mitigation Steps**

- To mitigate this issue, it is recommended to set a lower boundary in the function `setDefaultDeadlineOffset`.


## **[L-03] Incompatible with Fee-on-transfer token**

- The design of `ILOPool` is incompatible with Fee-on-transfer or rebasing tokens. Since the accounting for `raiseAmount`, `amount0`, `amount1`, `amountCollected0`, and `amountCollected1` doesn't consider the case that the amount will be changed due to FOT or REBASE issues.


### **Links to affected code**

- [ILOPool.sol#L242C18-L260](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L242C18-L260)


### **Recommended Mitigation Steps**

- If Fee-on-transfer or rebasing tokens are to be used, try use `balanceOf(address(this))` to calculate the received amount.


## **[L-04] whitelistCount may not return the actual whitelisted number**

- According to the function `checkWhitelist`, if `_allowedWhitelistIndex == 0`, no one is allowed. If `_whitelistIndex[to] > _allowedWhitelistIndex`, the `to` address is not allowed.

```solidity

            if (_allowedWhitelistIndex == 0 || _whitelistIndex[to] > _allowedWhitelistIndex) {
                revert NotWhitelisted();
            }
```

- However, according to this, the function `whitelistCount` does not accurately reflect how many addresses are whitelisted. It should be `0` if `_allowedWhitelistIndex == 0` and be `_allowedWhitelistIndex` otherwise.

```solidity
    /// @notice Returns current whitelisted address count
    function whitelistCount() external view returns (uint256) {
        return _whitelistCount;
    }
```

### **Links to affected code**

- [Whitelist.sol#L113C1-L116C6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L113C1-L116C6)
- [Whitelist.sol#L216-L218](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L216-L218)


### **Recommended Mitigation Steps**

- `whitelistCount` should return `0` if `_allowedWhitelistIndex == 0` and return `_allowedWhitelistIndex` otherwise.


## **[L-05] The vesting allows for instant unlock**

- In the `_validateVestSchedule` function, the function doesn't check if `schedule[i].start` < `schedule[i].end`. If `schedule[i].start == schedule[i].end`, the amount is unlocked instantly.

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
            // we need to subtract fist in order to avoid int overflow
            require(BPS - totalShares >= schedule[i].shares, "VS");
            totalShares += schedule[i].shares;
        }
        // total shares should be exactly equal BPS
        require(totalShares == BPS, "VS");
    }
}
```

### **Links to affected code**

- [ILOVest.sol#L35-L52](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/ILOVest.sol#L35-L52)


### **Recommended Mitigation Steps**

- Add relevant check `schedule[i].start` < `schedule[i].end` or set a minimum duration of a schedule.

## **[L-06] All Capital Letters will Cause Confusion**

- In Solidity, variables with all capital letters in naming are considered to be constant or immutable. However, in the current contract, variables with all capital letters can be changed. This may cause confusion in variable usage and violates the best practices.

```solidity
    uint64 private DEFAULT_DEADLINE_OFFSET = 7 * 24 * 60 * 60; // 7 days
    uint16 public override PLATFORM_FEE;
    uint16 public override PERFORMANCE_FEE;
    address public override FEE_TAKER;
    address public override ILO_POOL_IMPLEMENTATION;
```

### **Links to affected code**

- [ILOManager.sol#L19-L23](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L19-L23)


### **Recommended Mitigation Steps**

- Follow naming conventions instead of using all capital letters directly.

## **[L-07] whenNotInitialized Naming is inaccurate**

- In the `Initializable` contract, the `whenNotInitialized` modifier will work why the contract is not initialized and it will set `_initialized` to `true`. According to its function(changing the state) and common practice, it is better to rename it to `initializer` instead of `whenNotInitialized`.

```solidity
    modifier whenNotInitialized() {
        require(!_initialized);
        _;
        _initialized = true;
    }
```

### **Links to affected code**

- [Initializable.sol#L10-L14](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/Initializable.sol#L10-L14)


### **Recommended Mitigation Steps**

- Rename the modifier to `initializer` instead of `whenNotInitialized`. 

## **[L-08] If one pool fails to raise enough funds, the whole project will fail**

- In the `ILOManager::launch` function, all `IILOPool` will be launched. If we have only 1 pool that fails to raise enough funds, the whole project would be unable to launch due to the check `require(totalRaised >= saleInfo.softCap, "SC")`. This reduces the funds efficiency as the pool could not be removed from `initializedPools`.

```solidity
        for (uint256 i = 0; i < initializedPools.length; i++) {
            IILOPool(initializedPools[i]).launch();
        }
```

### **Links to affected code**

- [ILOManager.sol#L193C1-L195C10](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L193C1-L195C10)
- [ILOPool.sol#L274](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L274)


### **Recommended Mitigation Steps**

- Add a way to remove a `IILOPool` from `initializedPools` which hasn't raised enough funds.


## **[L-09] Launch Time should include `launchTime`**

- In `ILOManager::launch` function, it is required that `require(block.timestamp > _cachedProject[uniV3PoolAddress].launchTime, "LT")`. However, it should include the `_cachedProject[uniV3PoolAddress].launchTime` so that when `_cachedProject[uniV3PoolAddress].launchTime` reaches, one is also able to launch the project at that time. This is also consistent with "LT" error message.

```solidity
        require(block.timestamp > _cachedProject[uniV3PoolAddress].launchTime, "LT");
```

### **Links to affected code**

- [ILOManager.sol#L188](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L188)


### **Recommended Mitigation Steps**

- Change the check to `require(block.timestamp >= _cachedProject[uniV3PoolAddress].launchTime, "LT");`


## **[L-10] initializedPools can only be added**

- In the `ILOManager::launch` function, `initializedPools` will be iterated to launch them all. However, this array(`_initializedILOPools[uniV3PoolAddress]`) can only be added(`push`) but never be reduced(`pop`). When there are so many pools in `initializedPools`, this will cause an Out-of-gas error.

```solidity
        for (uint256 i = 0; i < initializedPools.length; i++) {
            IILOPool(initializedPools[i]).launch();
        }
```

### **Links to affected code**

- [ILOManager.sol#L193-L195](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L193-L195)
- [ILOManager.sol#L106](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L106C9-L106C29)

### **Recommended Mitigation Steps**

- Find a way to remove unused pools from `_initializedILOPools[uniV3PoolAddress]`.


## **[L-11] getOldestObservationSecondsAgo could be small after initialization**

- `UniswapV3Oracle::peek` queries `TWAP` for Oracle. But the `getOldestObservationSecondsAgo` could return a small value after initialization as `observationCardinality` is still small and has not been extended yet. In this situation, the `TWAP` response could be manipulated during this period.

```solidity
        (uint32 observationTimestamp, , , bool initialized) = IUniswapV3Pool(pool).observations(
            (observationIndex + 1) % observationCardinality
        );
```

```solidity
    /// @notice Returns TWAP price for 1 VULT for the last 30 mins
    function peek(uint256 baseAmount) external view returns (uint256) {
        uint32 longestPeriod = OracleLibrary.getOldestObservationSecondsAgo(pool);
        uint32 period = PERIOD < longestPeriod ? PERIOD : longestPeriod;
        int24 tick = OracleLibrary.consult(pool, period);
        uint256 quotedWETHAmount = OracleLibrary.getQuoteAtTick(tick, BASE_AMOUNT, baseToken, WETH);
        // Apply 5% slippage
        return (quotedWETHAmount * baseAmount * 95) / 1e20; // 100 / 1e18
    }
```

### **Links to affected code**

- [UniswapV3Oracle.sol#L38](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L38C1-L47)


### **Recommended Mitigation Steps**

- Ensure that there is enough `observationCardinality` before the trading starts.

