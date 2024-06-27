## QA Report

## [L-01] Attacker can DOS launches completely for all pools

[Link](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/PeripheryPayments.sol#L21)

An attacker can send ETH to the ILOPool.sol contract through self destruct or as coinbase reward recipient. When launch() is called now by admin to launch all ILO pools, liquidity is being added through addLiquidity() [here](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/LiquidityManagement.sol#L41), which ultimately ends up on function pay in the code snippet below when uniswap pool calls the callback [here](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/LiquidityManagement.sol#L20). 

Now since value would be equal to address(this).balance (due to attacker's deposit), we enter the first if block and it would attempt to call deposit() on the WETH contract. On some chains, the WETH contract does not have a deposit()/withdraw() function signature. Example: Polygon, Avalanche, Fantom, ZkSync etc.

Judging as low since protocol functionality is permanently DOSed which can possible brick all ILO pools from launching for a uniswap v3 pool project. But the cost is high for the attacker since they need to equal the launch liquidity amount for WETH.

Likelihood: Low
Impact: Medium

```solidity
File: PeripheryPayments.sol
23:     function pay(
24:         address token,
25:         address payer,
26:         address recipient,
27:         uint256 value
28:     ) internal {
29:         
30:         if (token == WETH9 && address(this).balance >= value) {
31:             // pay with WETH9
32:             IWETH9(WETH9).deposit{value: value}(); // wrap only what is needed to pay
33:         
34:             IWETH9(WETH9).transfer(recipient, value);
35:         } else if (payer == address(this)) {
```

## [L-02] _validateVestSchedule() does not validate start < end for current vest

[Link](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/ILOVest.sol#L35)

Lines 47-48 ensure that the start time for the next linear vest should be greater than equal to the previous linear vest's end. But it does not validate the start time to be less than the end time for the current vest.

This allows overlapping. For example, we could have:
Vest 1 with start = 100 and end = 200 
Vest 2 with start = 200 and end = 180 
Vest 3 with start = 190 and end = 250. 

This allows the admin of a project to bypass the current model and complete the linear vest for specific individuals quicker.
```solidity
File: ILOVest.sol
37:     function _validateVestSchedule(uint64 launchTime, LinearVest[] memory schedule) internal pure {
38:         require(schedule[0].start >= launchTime, "VT");
39:         uint16 BPS = 10000;
40:         uint16 totalShares;
41:         uint64 lastEnd;
42:         uint256 scheduleLength = schedule.length;
43:         
44:         for (uint256 i = 0; i < scheduleLength; i++) {
45:             // vesting schedule must not overlap
46:          
47:             require(schedule[i].start >= lastEnd, "VT");
48:             lastEnd = schedule[i].end;
49:             // we need to subtract fist in order to avoid int overflow
50:             require(BPS - totalShares >= schedule[i].shares, "VS");
51:             totalShares += schedule[i].shares; 
52:         }
53:         // total shares should be exactly equal BPS
54:         require(totalShares == BPS, "VS");
55:     }
```

## [L-03] Attacker can DOS investor from using maxCapPerUser amount in one go

[Link](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L126)

Attacker can deposit 1 wei to recipient by frontrunning recipient. This can DOS investors from passing raiseAmount = maxCapPerUser since it would exceed the limit due to the attacker's move. Another exmaple is in case investor initially bought 80 tokens and now decides to buy 20 tokens to hit the cap but the attacker launches the attack by making the 1 wei deposit again.

Solution: Consider using msg.sender directly and remove the recipient parameter option.
```solidity
File: ILOPool.sol
132:     function buy(uint256 raiseAmount, address recipient)
133:         external override 
134:         returns (
135:             uint256 tokenId,
136:             uint128 liquidityDelta
137:         )
138:     { 
```

## [L-04] Missing slippage protection in function claim()

[Link](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L184)

From the docs [here](https://ilo-docs.krystal.app/for-ilo-participants/sale-and-vesting-structure):
```
The vesting schedule of a Liquidity Position is no different from the vesting schedule of a Token. However, there are a few key notes:

The portion of each token in the Liquidity Position could change over time, based on the current market price of both tokens.

Vesting is made through the whole Liquidity. This means if you could claim 20% of the Liquidity, The exact amount of each token could be different based on the time you actually make the claim.
```

Although the team is aware of this problem, slippage check is not added to the claim function. 

Adding protection would allow users/investors to claim tokens and receive minimumAmount of tokens required by them.

```solidity
File: ILOPool.sol
195:     function claim(uint256 tokenId)
196:         external
197:         payable //@audit Low - user can send eth by mistake, consider removing this
198:         override
199:         isAuthorizedForToken(tokenId)
200:         returns (uint256 amount0, uint256 amount1)
201:     {
```

## [L-05] Rounding down should be performed in _saleAmountNeeded()

We should round down and not up (by passing false and not true) since we should favour the pool over user. This means the raise amount take in should be greater than the saleAmount (VULT) provided to users.

This does not pose a direct risk but would be a good sanity check to add.
```solidity
File: ILOPool.sol
405:         if (_cachedPoolKey.token0 == SALE_TOKEN) {
406:             // liquidity1 raised
407:             liquidity = LiquidityAmounts.getLiquidityForAmount1(SQRT_RATIO_LOWER_X96, SQRT_RATIO_X96, raiseAmount);
408:             
409:             saleAmountNeeded = SqrtPriceMathPartial.getAmount0Delta(SQRT_RATIO_X96, SQRT_RATIO_UPPER_X96, liquidity, true);
410:         } else {
411:             // liquidity0 raised
412:             liquidity = LiquidityAmounts.getLiquidityForAmount0(SQRT_RATIO_X96, SQRT_RATIO_UPPER_X96, raiseAmount);
413:             saleAmountNeeded = SqrtPriceMathPartial.getAmount1Delta(SQRT_RATIO_LOWER_X96, SQRT_RATIO_X96, liquidity, true);
414:         }
```

## [L-06] Protocol does not implement blacklistedCount variable which could pose problems

README mentions "the total whitelisted addresses will be whitelistCount - blacklistedCount". There is no blacklistedCount variable though to track this, which increments or decrements when an address is blacklisted or unblacklisted. This poses a risk since the team cannot track the blacklist count by which the _allowedWhitelistIndex needs to be incremented by (if there is a spam during self-whitelist that requires blacklisting plenty of addresses). There is no mention of this being tracked offchain and rather is expected to be manager onchain as per docs. 

Consider adding the variable.
```solidity
File: Whitelist.sol
183:     function setBlacklisted(address blacklisted, bool flag) external onlyOwner {
184:         _isBlacklisted[blacklisted] = flag;
185:     }
```

## [L-07] Initialize missing access control

In ILOManager.sol, initialize() function below missing access control i.e. only current owner should be able to call it.
```solidity
    function initialize(
        address initialOwner,
        address _feeTaker,
        address iloPoolImplementation,
        address uniV3Factory,
        address weth9,
        uint16 platformFee,
        uint16 performanceFee
    ) external override whenNotInitialized() {
        PLATFORM_FEE = platformFee; 
        PERFORMANCE_FEE = performanceFee;
        FEE_TAKER = _feeTaker;
        transferOwnership(initialOwner);
        UNIV3_FACTORY = uniV3Factory;
        ILO_POOL_IMPLEMENTATION = iloPoolImplementation;
        WETH9 = weth9;
    }
```

## [L-08] Project creator can bypass refund deadline

THis is by setting time in the past.
```solidity
 uint64 refundDeadline = params.launchTime + DEFAULT_DEADLINE_OFFSET;
```