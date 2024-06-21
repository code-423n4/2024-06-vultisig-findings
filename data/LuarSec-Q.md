## Missing sanity checks for hardcap >= softcap >= maxCapPerUser when initializing ILOPools in ILOManager.initILOPool
### Impact
There is a of effective validation of parameters when calling the `initILOPool` function when creating a new pool. This can allow for pool managers to initialize unfavorable or maliciously misleading pools through the system

**initILOPool():**
```solidity
function initILOPool(InitPoolParams calldata params) external override onlyProjectAdmin(params.uniV3Pool) returns (address iloPoolAddress) {
        Project storage _project = _cachedProject[params.uniV3Pool];
	[...]

        IILOPool.InitPoolParams memory initParams = IILOPool.InitPoolParams({
            uniV3Pool: params.uniV3Pool,
            tickLower: params.tickLower,
            tickUpper: params.tickUpper,
            sqrtRatioLowerX96: sqrtRatioLowerX96,
            sqrtRatioUpperX96: sqrtRatioUpperX96,
            hardCap: params.hardCap,
            softCap: params.softCap,
            maxCapPerUser: params.maxCapPerUser,
            start: params.start,
            end: params.end,
            vestingConfigs: params.vestingConfigs
        });
        IILOPool(iloPoolAddress).initialize(initParams);
        _initializedILOPools[params.uniV3Pool].push(iloPoolAddress);
    }
    [...]
```

**Remediation:**
Implement sanity checking of init parameters by adding a check that values passed to the function map to a sane range within the `ILOManager.initILOPool()` function, for example
`require(params.hardCap > params.softCap && params.softCap >= _params.maxCapPerUser, "PC");`  ("PC" - "parameter cap"). 
  
  Adjust >= or > accordingly, e.g. if softcap canot be equal to maxCapPerUser