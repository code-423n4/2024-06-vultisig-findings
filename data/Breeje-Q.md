# QA Report

## Low Risk Findings
| Count | Explanation |
|:--:|:-------|
| [L-01] | TWAP Period should be flexible as per market condition. |
| [L-02] | Blacklisted User Can Still Claim Tokens After Being Removed from Whitelist |
| [L-03] | Updating `DEFAULT_DEADLINE_OFFSET` can lead to multiple issues |
| [L-04] | Applying Slippage on Top of TWAP Price Allows users to get more VULT token than allowed | 
| [L-05] | `ILOManager` allows `ILOPools` with `initialPoolPriceX96` > `sqrtRatioUpperX96` | 

| Total Low Risk Findings | 5 |
|:--:|:--:|

### [L-01] TWAP Period should be flexible as per market condition.

#### Bug Description

Uniswap TWAP pricing is highly sensitive to the duration of the TWAP interval, which has both benefits and drawbacks:

1. Short TWAP Interval:

    * Short intervals provide more current and relevant price data, reflecting the latest market conditions.
    * Short intervals can be more susceptible to market volatility and manipulation, as they reflect rapid price changes.

2. Long TWAP Intervals:

    * Long intervals provide a stable price average, minimizing the impact of short-term volatility and market manipulation.
    * Long intervals may lag behind current market conditions, failing to reflect recent price changes accurately.

```solidity

    uint32 public constant PERIOD = 30 minutes;

```

Given VULT/WETH Pricing can be volatile or consistent depending on external environments, the twap `PERIOD` should not be constant. There should be a setter function controlled by owner who can update this value within a range to avoid price being too stale during high volatility & bringing back to longer TWAP Period during consistent pricing.

### [L-02] Blacklisted User Can Still Claim Tokens After Being Removed from Whitelist

#### Bug Description

`ILOWhitelist` couple of functions:

* `batchWhitelist`: To Whitelist Users who can `buy`.
* `batchRemoveWhitelist`: To blacklist or remove already whitelisted users.

Now consider the following Scenario:

1. Alice is initially whitelisted by the project admin.

2. Alice buys a position with `x` amount of RAISE Token.

3. Due to some external circumstances, Project admin removes Alice from the whitelist.

4. Despite being removed from the whitelist, Alice can still claim the tokens once the `ILOPool` launches.

### [L-03] Updating `DEFAULT_DEADLINE_OFFSET` can lead to multiple issues

#### Bug Description

* The `initProject` function uses `DEFAULT_DEADLINE_OFFSET` to set the `refundDeadline` for an `ILOPool`.

```solidity

    function setDefaultDeadlineOffset(uint64 defaultDeadlineOffset) external override onlyOwner() {
        emit DefaultDeadlineOffsetChanged(owner(), DEFAULT_DEADLINE_OFFSET, defaultDeadlineOffset);
        DEFAULT_DEADLINE_OFFSET = defaultDeadlineOffset;
    }

    function initProject(InitProjectParams calldata params) external override afterInitialize() returns(address uniV3PoolAddress) {
@->     uint64 refundDeadline = params.launchTime + DEFAULT_DEADLINE_OFFSET;

        // SNIP
    }

```

However, owner can use `setDefaultDeadlineOffset` function to update the `DEFAULT_DEADLINE_OFFSET` value without any timelock.

Few edge cases needs to be acknowledged here when owner does it:

1. A Project Admin's `initProject` call was pending in the mempool when the `DEFAULT_DEADLINE_OFFSET` got updated. This results in unexpected result for Protocol Admin.

2. Updating `DEFAULT_DEADLINE_OFFSET` will not update the `refundDeadline` of existing `ILOPools`.

3. Centralization Risk exists as there is no cap for `DEFAULT_DEADLINE_OFFSET`, it can be increased to huge value leading to permanent Freezing of buyer's fund in case soft cap wasn't reached.

Similarly, Updating Platform fees and Performance fees will also have implications in `claim` function where claimer might get unexpected result due to transaction being pending in mempool and Owner updating the fees.

### [L-04] Applying Slippage on Top of TWAP Price Allows users to get more VULT token than allowed

* The `peek` function in `UniswapV3Oracle` returns 95% of the `quotedWETHAmount * baseAmount`.

* Applying a 5% slippage on top of the TWAP Pricing unnecessarily allows users to receive more VULT tokens than their limit.

```solidity

    function peek(uint256 baseAmount) external view returns (uint256) {
        uint32 longestPeriod = OracleLibrary.getOldestObservationSecondsAgo(pool);
        uint32 period = PERIOD < longestPeriod ? PERIOD : longestPeriod;
        int24 tick = OracleLibrary.consult(pool, period);
        uint256 quotedWETHAmount = OracleLibrary.getQuoteAtTick(tick, BASE_AMOUNT, baseToken, WETH);
        // Apply 5% slippage
        return (quotedWETHAmount * baseAmount * 95) / 1e20; // 100 / 1e18
    }


```

* Slippage is typically used to account for volatility and market fluctuations during the execution of trades. Applying it on a pre-calculated TWAP does not reflect real-time market conditions accurately.

* The TWAP itself should be trusted as it provides a fair and accurate average price over time, reflecting true market conditions without the need for additional slippage adjustments.

### [L-05] `ILOManager` allows `ILOPools` with `initialPoolPriceX96` > `sqrtRatioUpperX96`

The `initILOPool` function allows Project Admins to intialize `ILOPool`.

Before initialization, it validates the `sqrtRatioLowerX96 < _project.initialPoolPriceX96` and `sqrtRatioLowerX96 < sqrtRatioUpperX96` but fails to validate `initialPoolPriceX96 > sqrtRatioUpperX96`. 

```solidity
File: ILOManager.sol

90:    require(sqrtRatioLowerX96 < _project.initialPoolPriceX96 && sqrtRatioLowerX96 < sqrtRatioUpperX96, "RANGE");


```

In case a Project is created with `initialPoolPriceX96` > `sqrtRatioUpperX96`, then:

* During `launch`, it will call `addLiquidity` function which will call `mint` function in Uniswap V3 Pool.

* `mint` function will call `_modifyPosition` function.

```solidity

    function mint(
        // SNIP
    ) external override lock returns (uint256 amount0, uint256 amount1) {
        require(amount > 0);
        (, int256 amount0Int, int256 amount1Int) =
@->         _modifyPosition(
                ModifyPositionParams({
                    owner: recipient,
                    tickLower: tickLower,
                    tickUpper: tickUpper,
                    liquidityDelta: int256(amount).toInt128()
                })
            );

            // SNIP
    }


```

* As `initialPoolPriceX96` > `sqrtRatioUpperX96`, `_modifyPosition` function execution will reach this else part where only `amount1` will be taken during adding Liquidity.

```solidity

      } else {
          // current tick is above the passed range; liquidity can only become in range by crossing from right to
          // left, when we'll need _more_ token1 (it's becoming more valuable) so user must provide it
          amount1 = SqrtPriceMath.getAmount1Delta(
              TickMath.getSqrtRatioAtTick(params.tickLower),
              TickMath.getSqrtRatioAtTick(params.tickUpper),
              params.liquidityDelta
          );
      }

```
[Link to Code](https://github.com/Uniswap/v3-core/blob/main/contracts/UniswapV3Pool.sol#L362-L369)

This will lead to DoS at `amount0Min` & `amount1Min` validation.

#### Recommendation

Apply changes:

```diff

-90:     require(sqrtRatioLowerX96 < _project.initialPoolPriceX96 && sqrtRatioLowerX96 < sqrtRatioUpperX96, "RANGE");
+90;     require(sqrtRatioLowerX96 < _project.initialPoolPriceX96 && sqrtRatioLowerX96 < sqrtRatioUpperX96 && _project.initialPoolPriceX96 < sqrtRatioUpperX96, "RANGE");

```