
## L-01 The `ILOVest._validateVestSchedule()` function does not check whether the end time is after the start time for each `schedule`.

There should be a check to ensure that `schedule[i].end` is greater than `schedule[i].start` for each `schedule`. If `schedule[i].end <= schedule[i].start` for a `schedule`, then the `ILOPool._unlockedLiquidity()` function will be reverted at [L427](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L427).

https://github.com/code-423n4/2024-06-vultisig/blob/main/src/base/ILOVest.sol#L35-L51

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
+           require(schedule[i].end > schedule[i].start, "VT");
            lastEnd = schedule[i].end;
            // we need to subtract fist in order to avoid int overflow
            require(BPS - totalShares >= schedule[i].shares, "VS");
            totalShares += schedule[i].shares;
        }
        // total shares should be exactly equal BPS
        require(totalShares == BPS, "VS");
    }
```


## L-02 Ethers sent to `ILOPool` contract are locked.

As [ILOPool.claim](https://github.com/code-423n4/2024-06-vultisig/blob/0957ff9e50441cd6de6b4f6e28c7ea93f5cffa85/src/ILOManager.sol#L184-L261) is a payable function, ethers can be sent to this contract. As there is no method to withdraw it, ethers are locked in this contract. So the payable modifier should be removed as follows.

```diff
File: src\ILOPool.sol
184:     function claim(uint256 tokenId)
185:         external
-            payable
187:         override
188:         isAuthorizedForToken(tokenId)
189:         returns (uint256 amount0, uint256 amount1)
```