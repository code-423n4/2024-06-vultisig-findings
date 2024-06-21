# QA

# QA-1 Missing events for critical functions
- `VultiSigWhitelisted#setWhitelistContract()`
- `Whitelist#setPool()`
- `Whitelist#setLocked()`
- `Whitelist#setMaxAddressCap()`
- `Whitelist#setVultisig()`
- `Whitelist#setIsSelfWhitelistDisabled()`
- `Whitelist#setOracle()`
- `Whitelist#setPool()`
- `Whitelist#setBlacklisted()`
- `Whitelist#setAllowedWhitelistIndex()`
- `Whitelist#addWhitelistedAddress()`
- `Whitelist#addBatchWhitelist()`

# QA-2 Use immutables in ILOPoolImmutableState
The following can be made immutable by using the Solady clone library, rather than OZ. Solady implements "Clone With Immutable Args" (CWIA), which allows passing args to the constructor.

```solidity
/// @inheritdoc IILOPoolImmutableState
address public override WETH9;

uint16 constant BPS = 10000;
address public override MANAGER;
address public override RAISE_TOKEN;
address public override SALE_TOKEN;
int24 public override TICK_LOWER;
int24 public override TICK_UPPER;
uint160 public override SQRT_RATIO_X96;
uint160 internal SQRT_RATIO_LOWER_X96;
uint160 internal SQRT_RATIO_UPPER_X96;

PoolAddress.PoolKey internal _cachedPoolKey;
address internal _cachedUniV3PoolAddress;
```

# QA-3 `ILOPool#claim()` does not need to be payable
This function does not require ether payment yet is marked payable.
```solidity
function claim(uint256 tokenId)
        external
        payable
        override
        isAuthorizedForToken(tokenId)
        returns (uint256 amount0, uint256 amount1)
    {
```

# QA-4 Centralization risk
The contract owners have the ability to lock all funds, change key parameters, change whitelist contracts. The contract owners are heavily trusted actors in the system.

# QA-5 Unecessary oracle check
The `Whitelist#checkWhitelist` function could get the amount of RAISE_TOKEN contributed from the ILOPool directly, rather than the current oracle check + slippage calculation, which is slightly awkward and inherently inaccurate.

# QA-6 Current whitelist would block large buys in the pool (>3Eth), but would allow large sells (impacts token price)