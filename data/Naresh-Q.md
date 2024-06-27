Note:
This report includes additional instances of an issue listed in the automated findings report.

## Summary
| |Issue|Instances| 
|-|:-|:-:|
| [[L-01](#l-01)] | Consider adding validation of user inputs | 25| 
| [[L-02](#l-02)] | Array is `push()`ed but not `pop()`ed | 2| 
| [[L-03](#l-03)] | Execution at deadlines should be allowed | 5| 
| [[L-04](#l-04)] | Consider bounding input array length | 8| 
| [[L-05](#l-05)] | Privileged functions can create points of failure | 24| 
| [[L-06](#l-06)] | Code does not follow the best practice of check-effects-interaction | 1| 
| [[L-07](#l-07)] | Constant decimal values | 1| 
| [[L-08](#l-08)] | Do not leave an implementation contract uninitialized | 1| 
| [[L-09](#l-09)] | Consider disabling `renounceOwnership()` | 3| 
| [[L-10](#l-10)] | Events may be emitted out of order due to reentrancy | 9| 
| [[L-11](#l-11)] | External call recipient can consume all remaining gas | 4| 
| [[L-12](#l-12)] | External calls in an unbounded loop can result in a DoS | 4| 
| [[L-13](#l-13)] | `forceApprove` should be used instead of `approve` | 1| 
| [[L-14](#l-14)] | Functions calling contracts/addresses with transfer hooks are missing reentrancy guards | 4| 
| [[L-15](#l-15)] | Initializers can be front-run | 5| 
| [[L-16](#l-16)] | Input array lengths may differ | 4| 
| [[L-17](#l-17)] | Mapping arrays can grow in size without a way to shrink them | 1| 
| [[L-18](#l-18)] | Missing zero address check in constructor | 1| 
| [[L-19](#l-19)] | Missing checks for `address(0x0)` when updating `address` state variables | 13| 
| [[L-20](#l-20)] | Missing contract-existence checks before low-level calls | 5| 
| [[L-21](#l-21)] | Contracts are designed to receive ETH but do not implement function for withdrawal | 2| 
| [[L-22](#l-22)] | `onlyOwner` functions not accessible if owner renounces ownership | 20| 
| [[L-23](#l-23)] | Variables shadowing other definitions | 4| 
| [[L-24](#l-24)] | File allows a version of solidity that is susceptible to an assembly optimizer bug | 4| 
| [[L-25](#l-25)] | Solidity version `0.8.20` may not work on other chains due to `PUSH0` | 4| 
| [[L-26](#l-26)] | State variables not capped at reasonable values | 7| 
| [[L-27](#l-27)] | Consider implementing two-step procedure for updating protocol addresses | 8| 
| [[L-28](#l-28)] | Using zero as a parameter | 1| 
| [[L-29](#l-29)] | Some `ERC20` can revert on a zero value `transfer` | 9| 

### Low Risk Issues

### [L-01]<a name="l-01"></a> Consider adding validation of user inputs

There are no validations done on the arguments below. Consider that the Solidity [documentation](https://docs.soliditylang.org/en/latest/control-structures.html#panic-via-assert-and-error-via-require) states that `Properly functioning code should never create a Panic, not even on invalid external input. If this happens, then there is a bug in your contract which you should fix`. This means that there should be explicit checks for expected ranges of inputs. Underflows/overflows result in panics should not be used as range checks, and allowing funds to be sent to `0x0`, which is the default value of address variables and has many gotchas, should be avoided.

*There are 25 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Vultisig.sol

// @audit missing checks for -->  spender
16:     function approveAndCall(address spender, uint256 amount, bytes calldata extraData) external returns (bool) {

```


*GitHub* : [16](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Vultisig.sol#L16-L16)

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

// @audit missing checks for -->  account
88:     function whitelistIndex(address account) external view returns (uint256) {

// @audit missing checks for -->  account
94:     function isBlacklisted(address account) external view returns (bool) {

// @audit missing checks for -->  to
125:     function contributed(address to) external view returns (uint256) {

// @audit missing checks for -->  newVultisig
148:     function setVultisig(address newVultisig) external onlyOwner {

// @audit missing checks for -->  newOracle
160:     function setOracle(address newOracle) external onlyOwner {

// @audit missing checks for -->  newPool
166:     function setPool(address newPool) external onlyOwner {

// @audit missing checks for -->  blacklisted
173:     function setBlacklisted(address blacklisted, bool flag) external onlyOwner {

// @audit missing checks for -->  whitelisted
185:     function addWhitelistedAddress(address whitelisted) external onlyOwner {

// @audit missing checks for -->  whitelisted
191:     function addBatchWhitelist(address[] calldata whitelisted) external onlyOwner {

// @audit missing checks for -->  from, to
204:     function checkWhitelist(address from, address to, uint256 amount) external onlyVultisig {

```


*GitHub* : [88](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L88-L88), [94](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L94-L94), [125](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L125-L125), [148](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L148-L148), [160](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L160-L160), [166](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L166-L166), [173](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L173-L173), [185](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L185-L185), [191](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L191-L191), [204](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L204-L204)

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

// @audit missing checks for -->  newWhitelistContract
22:     function setWhitelistContract(address newWhitelistContract) external onlyOwner {

```


*GitHub* : [22](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L22-L22)

```solidity
📁 File: src/ILOManager.sol

// @audit missing checks for -->  initialOwner, _feeTaker, iloPoolImplementation, uniV3Factory, weth9
33:     function initialize(
34:         address initialOwner,
35:         address _feeTaker,
36:         address iloPoolImplementation,
37:         address uniV3Factory,
38:         address weth9,
39:         uint16 platformFee,
40:         uint16 performanceFee
41:     ) external override whenNotInitialized() {

// @audit missing checks for -->  uniV3PoolAddress
67:     function project(address uniV3PoolAddress) external override view returns (Project memory) {

// @audit missing checks for -->  _feeTaker
160:     function setFeeTaker(address _feeTaker) external override onlyOwner() {

// @audit missing checks for -->  iloPoolImplementation
164:     function setILOPoolImplementation(address iloPoolImplementation) external override onlyOwner() {

// @audit missing checks for -->  admin, uniV3Pool
169:     function transferAdminProject(address admin, address uniV3Pool) external override onlyProjectAdmin(uniV3Pool) {

// @audit missing checks for -->  uniV3Pool
180:     function setRefundDeadlineForProject(address uniV3Pool, uint64 refundDeadline) external override onlyOwner() {

// @audit missing checks for -->  uniV3PoolAddress
187:     function launch(address uniV3PoolAddress) external override {

// @audit missing checks for -->  uniV3PoolAddress
201:     function claimRefund(address uniV3PoolAddress) external override onlyProjectAdmin(uniV3PoolAddress) returns(uint256 totalRefundAmount) {

```


*GitHub* : [33](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L33-L41), [67](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L67-L67), [160](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L160-L160), [164](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L164-L164), [169](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L169-L169), [180](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L180-L180), [187](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L187-L187), [201](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L201-L201)

```solidity
📁 File: src/ILOPool.sol

// @audit missing checks for -->  recipient
126:     function buy(uint256 raiseAmount, address recipient)
127:         external override 
128:         returns (
129:             uint256 tokenId,
130:             uint128 liquidityDelta
131:         )
132:     {

// @audit missing checks for -->  projectAdmin
363:     function claimProjectRefund(address projectAdmin) external override refundable() OnlyManager() returns(uint256 refundAmount) {

```


*GitHub* : [126](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L126-L132), [363](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L363-L363)

```solidity
📁 File: src/base/ILOWhitelist.sol

// @audit missing checks for -->  user
22:     function isWhitelisted(address user) external override view returns (bool) {

// @audit missing checks for -->  users
27:     function batchWhitelist(address[] calldata users) external override onlyProjectAdmin{

// @audit missing checks for -->  users
34:     function batchRemoveWhitelist(address[] calldata users) external override onlyProjectAdmin{

```


*GitHub* : [22](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L22-L22), [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L27-L27), [34](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L34-L34)

### [L-02]<a name="l-02"></a> Array is `push()`ed but not `pop()`ed

Array entries are added but are never removed. Consider whether this should be the case, or whether there should be a maximum, or whether old entries should be removed. Cases where there are specific potential problems will be flagged separately under a different issue.

*There are 2 instance(s) of this issue:*

```solidity
📁 File: src/ILOPool.sol

93:             _vestingConfigs.push(params.vestingConfigs[index]);

325:                 schedule.push(projectConfig.schedule[i]);

```


*GitHub* : [93](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L93-L93), [325](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L325-L325)

### [L-03]<a name="l-03"></a> Execution at deadlines should be allowed

The condition may be wrong in these cases, as when `block.timestamp` is equal to the compared `>` or `<` variable these blocks will not be executed.

*There are 5 instance(s) of this issue:*

```solidity
📁 File: src/ILOManager.sol

188:         require(block.timestamp > _cachedProject[uniV3PoolAddress].launchTime, "LT");

202:         require(_cachedProject[uniV3PoolAddress].refundDeadline < block.timestamp, "RFT");

```


*GitHub* : [188](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L188-L188), [202](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L202-L202)

```solidity
📁 File: src/ILOPool.sol

134:         require(block.timestamp > saleInfo.start && block.timestamp < saleInfo.end, "ST");

410:             if (block.timestamp < vest.start) {

417:             if (vest.end < block.timestamp) {

```


*GitHub* : [134](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L134-L134), [410](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L410-L410), [417](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L417-L417)

### [L-04]<a name="l-04"></a> Consider bounding input array length

Unbounded array inputs in functions can lead to unintentional excessive gas consumption, potentially causing a transaction to revert after expending substantial gas. To enhance user experience and prevent such scenarios, consider implementing a `require()` statement that limits the array length to a defined maximum. This constraint ensures that transactions won't proceed if they're likely to hit gas limits due to array size, saving users from unnecessary gas costs and offering a more predictable interaction with the contract.

*There are 8 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

//@audit whitelisted.length not bounded 
192:         for (uint i = 0; i < whitelisted.length; i++) {

```


*GitHub* : [192](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L192-L192)

```solidity
📁 File: src/ILOManager.sol

//@audit initializedPools.length not bounded 
204:         for (uint256 i = 0; i < initializedPools.length; i++) {

```


*GitHub* : [204](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L204-L204)

```solidity
📁 File: src/ILOPool.sol

//@audit _vestingConfigs.length not bounded 
311:         for (uint256 index = 1; index < _vestingConfigs.length; index++) {

//@audit vestingSchedule.length not bounded 
405:         for (uint256 index = 0; index < vestingSchedule.length; index++) {

```


*GitHub* : [311](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L311-L311), [405](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L405-L405)

```solidity
📁 File: src/base/ILOVest.sol

//@audit vestingConfigs.length not bounded 
20:         for (uint256 i = 0; i < vestingConfigs.length; i++) {

```


*GitHub* : [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L20-L20)

```solidity
📁 File: src/base/ILOWhitelist.sol

//@audit users.length not bounded 
28:         for (uint256 i = 0; i < users.length; i++) {

//@audit users.length not bounded 
35:         for (uint256 i = 0; i < users.length; i++) {

```


*GitHub* : [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L28-L28), [35](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L35-L35)

```solidity
📁 File: src/base/Multicall.sol

//@audit data.length not bounded 
13:         for (uint256 i = 0; i < data.length; i++) {

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L13-L13)

### [L-05]<a name="l-05"></a> Privileged functions can create points of failure

Ensure such accounts are protected and consider implementing multi sig to prevent a single point of failure

*There are 24 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

136:     function setLocked(bool newLocked) external onlyOwner {

142:     function setMaxAddressCap(uint256 newCap) external onlyOwner {

148:     function setVultisig(address newVultisig) external onlyOwner {

154:     function setIsSelfWhitelistDisabled(bool newFlag) external onlyOwner {

160:     function setOracle(address newOracle) external onlyOwner {

166:     function setPool(address newPool) external onlyOwner {

173:     function setBlacklisted(address blacklisted, bool flag) external onlyOwner {

179:     function setAllowedWhitelistIndex(uint256 newIndex) external onlyOwner {

185:     function addWhitelistedAddress(address whitelisted) external onlyOwner {

191:     function addBatchWhitelist(address[] calldata whitelisted) external onlyOwner {

204:     function checkWhitelist(address from, address to, uint256 amount) external onlyVultisig {

```


*GitHub* : [136](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L136-L136), [142](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L142-L142), [148](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L148-L148), [154](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L154-L154), [160](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L160-L160), [166](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L166-L166), [173](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L173-L173), [179](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L179-L179), [185](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L185-L185), [191](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L191-L191), [204](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L204-L204)

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

22:     function setWhitelistContract(address newWhitelistContract) external onlyOwner {

```


*GitHub* : [22](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L22-L22)

```solidity
📁 File: src/ILOManager.sol

72:     function initILOPool(InitPoolParams calldata params) external override onlyProjectAdmin(params.uniV3Pool) returns (address iloPoolAddress) {

150:     function setPlatformFee(uint16 _platformFee) external onlyOwner() {

155:     function setPerformanceFee(uint16 _performanceFee) external onlyOwner() {

160:     function setFeeTaker(address _feeTaker) external override onlyOwner() {

164:     function setILOPoolImplementation(address iloPoolImplementation) external override onlyOwner() {

169:     function transferAdminProject(address admin, address uniV3Pool) external override onlyProjectAdmin(uniV3Pool) {

175:     function setDefaultDeadlineOffset(uint64 defaultDeadlineOffset) external override onlyOwner() {

180:     function setRefundDeadlineForProject(address uniV3Pool, uint64 refundDeadline) external override onlyOwner() {

201:     function claimRefund(address uniV3PoolAddress) external override onlyProjectAdmin(uniV3PoolAddress) returns(uint256 totalRefundAmount) {

```


*GitHub* : [72](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L72-L72), [150](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L150-L150), [155](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L155-L155), [160](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L160-L160), [164](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L164-L164), [169](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L169-L169), [175](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L175-L175), [180](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L180-L180), [201](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L201-L201)

```solidity
📁 File: src/base/ILOWhitelist.sol

12:     function setOpenToAll(bool openToAll) external override onlyProjectAdmin{

27:     function batchWhitelist(address[] calldata users) external override onlyProjectAdmin{

34:     function batchRemoveWhitelist(address[] calldata users) external override onlyProjectAdmin{

```


*GitHub* : [12](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L12-L12), [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L27-L27), [34](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L34-L34)

### [L-06]<a name="l-06"></a> Code does not follow the best practice of check-effects-interaction

Code should follow the best-practice of [CEI](https://blockchain-academy.hs-mittweida.de/courses/solidity-coding-beginners-to-intermediate/lessons/solidity-11-coding-patterns/topic/checks-effects-interactions/), where state variables are updated before any external calls are made. Doing so prevents a large class of reentrancy bugs

*There are 1 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

// @audit IOracle(_oracle).peek() called on line 221 
226:             _contributed[to] += estimatedETHAmount;

```


*GitHub* : [226](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L226-L226)

### [L-07]<a name="l-07"></a> Constant decimal values

The use of fixed decimal values such as 1e18 or 1e8 in Solidity contracts can lead to inaccuracies, bugs, and vulnerabilities, particularly when interacting with tokens having different decimal configurations. Not all ERC20 tokens follow the standard 18 decimal places, and assumptions about decimal places can lead to miscalculations.

Resolution: Always retrieve and use the `decimals()` function from the token contract itself when performing calculations involving token amounts. This ensures that your contract correctly handles tokens with any number of decimal places, mitigating the risk of numerical errors or under/overflows that could jeopardize contract integrity and user funds.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

18:     uint128 public constant BASE_AMOUNT = 1e18; // VULT has 18 decimals

```


*GitHub* : [18](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L18-L18)

### [L-08]<a name="l-08"></a> Do not leave an implementation contract uninitialized

An uninitialized implementation contract can be taken over by an attacker, which may impact the proxy. To prevent the implementation contract from being used, it's advisable to invoke the `_disableInitializers` function in the constructor to automatically lock it when it is deployed. This should look similar to this:
```solidity
  /// @custom:oz-upgrades-unsafe-allow constructor
  constructor() {
      _disableInitializers();
  }
```

Sources:
- https://docs.openzeppelin.com/contracts/4.x/api/proxy#Initializable-_disableInitializers--
- https://twitter.com/0xCygaar/status/1621417995905167360?s=20

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/ILOManager.sol

29:     constructor () {
30:         transferOwnership(tx.origin);
31:     }

```


*GitHub* : [29](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L29-L31)

### [L-09]<a name="l-09"></a> Consider disabling `renounceOwnership()`

Typically, the contract's owner is the account that deploys the contract. As a result, the owner is able to perform certain privileged activities. The OpenZeppelin's `Ownable` is used in this project contract implements `renounceOwnership`. This can represent a certain risk if the ownership is renounced for any other reason than by design. Renouncing ownership will leave the contract without an owner, thereby removing any functionality that is only available to the owner.

*There are 3 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Vultisig.sol

11: contract Vultisig is ERC20, Ownable {

```


*GitHub* : [11](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Vultisig.sol#L11-L11)

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

16: contract Whitelist is Ownable {

```


*GitHub* : [16](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L16-L16)

```solidity
📁 File: src/ILOManager.sol

15: contract ILOManager is IILOManager, Ownable, Initializable {

```


*GitHub* : [15](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L15-L15)

### [L-10]<a name="l-10"></a> Events may be emitted out of order due to reentrancy

If a reentrancy occurs, some events may be emitted in an unexpected order, and this may be a problem if a third party expects a specific order for these events. Ensure that events are emitted before external calls and follow the best practice of CEI.

*There are 9 instance(s) of this issue:*

```solidity
📁 File: src/ILOManager.sol

197:         emit ProjectLaunch(uniV3PoolAddress);

```


*GitHub* : [197](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L197-L197)

```solidity
📁 File: src/ILOPool.sol

175:         emit Buy(recipient, tokenId, raiseAmount, liquidityDelta);

238:             emit DecreaseLiquidity(tokenId, liquidity2Claim, amount0, amount1);

249:         emit Collect(tokenId, address(this), amountCollected0, amountCollected1);

255:         emit Claim(ownerOf(tokenId), tokenId,liquidity2Claim, amount0, amount1, position.feeGrowthInside0LastX128, position.feeGrowthInside1LastX128);

359:         emit UserRefund(tokenOwner, tokenId,refundAmount);

371:             emit ProjectRefund(projectAdmin, refundAmount);

```


*GitHub* : [175](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L175-L175), [238](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L238-L238), [249](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L249-L249), [255](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L255-L255), [359](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L359-L359), [371](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L371-L371)

```solidity
📁 File: src/base/ILOWhitelist.sol

49:         emit SetWhitelist(user, false);

54:         emit SetWhitelist(user, true);

```


*GitHub* : [49](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L49-L49), [54](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L54-L54)

### [L-11]<a name="l-11"></a> External call recipient can consume all remaining gas

There is no limit specified on the amount of gas used, so the recipient can use up all of the remaining gas(gasleft()), causing it to revert. Therefore, when calling an external contract, it is necessary to specify a limited amount of gas to forward.

*There are 4 instance(s) of this issue:*

```solidity
📁 File: src/libraries/TransferHelper.sol

20:             token.call(abi.encodeWithSelector(IERC20.transferFrom.selector, from, to, value));

34:         (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.transfer.selector, to, value));

48:         (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.approve.selector, to, value));

57:         (bool success, ) = to.call{value: value}(new bytes(0));

```


*GitHub* : [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L20-L20), [34](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L34-L34), [48](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L48-L48), [57](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L57-L57)

### [L-12]<a name="l-12"></a> External calls in an unbounded loop can result in a DoS

Consider limiting the number of iterations in loops that make external calls, as just a single one of them failing will result in a revert.

*There are 4 instance(s) of this issue:*

```solidity
📁 File: src/ILOManager.sol

194:             IILOPool(initializedPools[i]).launch();

```


*GitHub* : [194](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L194-L194)

```solidity
📁 File: src/base/ILOWhitelist.sol

29:             _setWhitelist(users[i]);

36:             _removeWhitelist(users[i]);

```


*GitHub* : [29](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L29-L29), [36](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L36-L36)

```solidity
📁 File: src/base/Multicall.sol

14:             (bool success, bytes memory result) = address(this).delegatecall(data[i]);

```


*GitHub* : [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L14-L14)

### [L-13]<a name="l-13"></a> `forceApprove` should be used instead of `approve`

Code uses the `approve` method to set allowance for ERC20 tokens. This will cause revert if the target ERC20 was a non-standard token that has different function signature for `approve()`.Eg:[USDT](https://etherscan.io/address/0xdac17f958d2ee523a2206206994597c13d831ec7#code#L126)

Use OpenZeppelin’s `SafeERC20:: forceApprove` method instead to support all the ERC20 tokens.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/libraries/TransferHelper.sol

48:         (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.approve.selector, to, value));

```


*GitHub* : [48](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L48-L48)

### [L-14]<a name="l-14"></a> Functions calling contracts/addresses with transfer hooks are missing reentrancy guards

Even if the function follows the best practice of check-effects-interaction, not using a reentrancy guard when there may be transfer hooks will open the users of this protocol up to [read-only reentrancies](https://chainsecurity.com/curve-lp-oracle-manipulation-post-mortem/) with no way to protect against it, except by block-listing the whole protocol.

*There are 4 instance(s) of this issue:*

```solidity
📁 File: src/ILOManager.sol

// @audit function 'initialize()' is missing Reentrancy guard
45:         transferOwnership(initialOwner);

```


*GitHub* : [45](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L45-L45)

```solidity
📁 File: src/ILOPool.sol

// @audit function 'buy()' is missing Reentrancy guard
173:         TransferHelper.safeTransferFrom(RAISE_TOKEN, msg.sender, address(this), raiseAmount);

// @audit function 'claim()' is missing Reentrancy guard
252:         TransferHelper.safeTransfer(_cachedPoolKey.token0, ownerOf(tokenId), amount0);

// @audit function 'claimRefund()' is missing Reentrancy guard
358:         TransferHelper.safeTransfer(RAISE_TOKEN, tokenOwner, refundAmount);

```


*GitHub* : [173](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L173-L173), [252](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L252-L252), [358](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L358-L358)

### [L-15]<a name="l-15"></a> Initializers can be front-run

Initializers could be front-run, allowing an attacker to either set their own values, take ownership of the contract, and in the best case forcing a re-deployment.

*There are 5 instance(s) of this issue:*

```solidity
📁 File: src/ILOManager.sol

33:     function initialize(
34:         address initialOwner,
35:         address _feeTaker,
36:         address iloPoolImplementation,
37:         address uniV3Factory,
38:         address weth9,
39:         uint16 platformFee,
40:         uint16 performanceFee
41:     ) external override whenNotInitialized() {


57:     function initProject(InitProjectParams calldata params) external override afterInitialize() returns(address uniV3PoolAddress) {


72:     function initILOPool(InitPoolParams calldata params) external override onlyProjectAdmin(params.uniV3Pool) returns (address iloPoolAddress) {


109:     function _initUniV3PoolIfNecessary(PoolAddress.PoolKey memory poolKey, uint160 sqrtPriceX96) internal returns (address pool) {


```

*GitHub* : [33](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L33-L49), [57](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L57-L65), [72](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L72-L107), [109](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L109-L122)

```solidity
📁 File: src/ILOPool.sol

61:     function initialize(InitPoolParams calldata params) external override whenNotInitialized() {


```

*GitHub* : [61](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L61-L103)

### [L-16]<a name="l-16"></a> Input array lengths may differ

If the caller makes a copy-paste error, the lengths may be mismatched and an operation believed to have been completed may not in fact have been completed (e.g. if the array being iterated over is shorter than the one being indexed into).

*There are 4 instance(s) of this issue:*

```solidity
📁 File: src/base/ILOVest.sol

// @audit schedule[]
43:             require(schedule[i].start >= lastEnd, "VT");

// @audit schedule[]
44:             lastEnd = schedule[i].end;

// @audit schedule[]
46:             require(BPS - totalShares >= schedule[i].shares, "VS");

// @audit schedule[]
47:             totalShares += schedule[i].shares;

```


*GitHub* : [43](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L43-L43), [44](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L44-L44), [46](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L46-L46), [47](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L47-L47)

### [L-17]<a name="l-17"></a> Mapping arrays can grow in size without a way to shrink them

It's a good practice to maintain control over the size of array mappings in Solidity, especially if they are dynamically updated. If a contract includes a mechanism to push items into an array, it should ideally also provide a mechanism to remove items. This is because Solidity arrays don't automatically shrink when items are deleted - their length needs to be manually adjusted.

Ignoring this can lead to bloated and inefficient contracts. For instance, iterating over a large array can cause your contract to hit the block gas limit. Additionally, if entries are only marked for deletion but never actually removed, you may end up dealing with stale or irrelevant data, which can cause logical errors.

Therefore, implementing a method to 'pop' items from mapping arrays helps manage contract's state, improve efficiency and prevent potential issues related to gas limits or stale data. Always ensure to handle potential underflow conditions when popping elements from the mapping array.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/ILOManager.sol

26:     mapping(address => address[]) private _initializedILOPools; // map uniV3Pool => list of initialized ilo pools

```


*GitHub* : [26](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L26-L26)

### [L-18]<a name="l-18"></a> Missing zero address check in constructor

Constructors often take address parameters to initialize important components of a contract, such as owner or linked contracts. However, without a checking, there's a risk that an address parameter could be mistakenly set to the zero address `(0x0)`. This could be due to an error or oversight during contract deployment. A zero address in a crucial role can cause serious issues, as it cannot perform actions like a normal address, and any funds sent to it will be irretrievable. It's therefore crucial to include a zero address check in constructors to prevent such potential problems. If a zero address is detected, the constructor should revert the transaction.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

// @audit missing checks for -->  _pool, _baseToken, _WETH
27:     constructor(address _pool, address _baseToken, address _WETH) {

```


*GitHub* : [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L27-L27)

### [L-19]<a name="l-19"></a> Missing checks for `address(0x0)` when updating `address` state variables

Explore the imperative need for meticulous checks in smart contract development, specifically addressing the absence of validations for address(0x0) during state variable updates. This concise overview sheds light on the potential risks associated with this omission and offers practical insights into rectifying the vulnerability. Stay vigilant, stay secure.

*There are 13 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

149:         _vultisig = newVultisig;

161:         _oracle = newOracle;

167:         _pool = newPool;

```


*GitHub* : [149](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L149-L149), [161](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L161-L161), [167](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L167-L167)

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

23:         _whitelistContract = newWhitelistContract;

```


*GitHub* : [23](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L23-L23)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

28:         pool = _pool;

29:         baseToken = _baseToken;

30:         WETH = _WETH;

```


*GitHub* : [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L28-L28), [29](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L29-L29), [30](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L30-L30)

```solidity
📁 File: src/ILOManager.sol

44:         FEE_TAKER = _feeTaker;

46:         UNIV3_FACTORY = uniV3Factory;

47:         ILO_POOL_IMPLEMENTATION = iloPoolImplementation;

48:         WETH9 = weth9;

161:         FEE_TAKER = _feeTaker;

166:         ILO_POOL_IMPLEMENTATION = iloPoolImplementation;

```


*GitHub* : [44](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L44-L44), [46](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L46-L46), [47](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L47-L47), [48](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L48-L48), [161](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L161-L161), [166](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L166-L166)

### [L-20]<a name="l-20"></a> Missing contract-existence checks before low-level calls

Low-level calls return success if there is no code present at the specified address.

*There are 5 instance(s) of this issue:*

```solidity
📁 File: src/base/Multicall.sol

14:             (bool success, bytes memory result) = address(this).delegatecall(data[i]);

```


*GitHub* : [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L14-L14)

```solidity
📁 File: src/libraries/TransferHelper.sol

20:             token.call(abi.encodeWithSelector(IERC20.transferFrom.selector, from, to, value));

34:         (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.transfer.selector, to, value));

48:         (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.approve.selector, to, value));

57:         (bool success, ) = to.call{value: value}(new bytes(0));

```


*GitHub* : [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L20-L20), [34](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L34-L34), [48](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L48-L48), [57](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L57-L57)

### [L-21]<a name="l-21"></a> Contracts are designed to receive ETH but do not implement function for withdrawal

The following contracts can receive ETH but can not withdraw, ETH is occasionally sent by users will be stuck in those contracts. This functionality also applies to baseTokens resulting in locked tokens and loss of funds.

*There are 2 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

65:     receive() external payable {
66:         if (_isSelfWhitelistDisabled) {
67:             revert SelfWhitelistDisabled();
68:         }
69:         if (_isBlacklisted[_msgSender()]) {
70:             revert Blacklisted();
71:         }
72:         _addWhitelistedAddress(_msgSender());
73:         payable(_msgSender()).transfer(msg.value);
74:     }

```


*GitHub* : [65](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L65-L74)

```solidity
📁 File: src/base/PeripheryPayments.sol

13:     receive() external payable {
14:         require(msg.sender == WETH9, 'Not WETH9');
15:     }

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L13-L15)

### [L-22]<a name="l-22"></a> `onlyOwner` functions not accessible if owner renounces ownership

The owner is able to perform certain privileged activities, but it's possible to set the owner to address(0). This can represent a certain risk if the ownership is renounced for any other reason than by design.

Renouncing ownership will leave the contract without an owner, therefore limiting any functionality that needs authority.

*There are 20 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

136:     function setLocked(bool newLocked) external onlyOwner {

142:     function setMaxAddressCap(uint256 newCap) external onlyOwner {

148:     function setVultisig(address newVultisig) external onlyOwner {

154:     function setIsSelfWhitelistDisabled(bool newFlag) external onlyOwner {

160:     function setOracle(address newOracle) external onlyOwner {

166:     function setPool(address newPool) external onlyOwner {

173:     function setBlacklisted(address blacklisted, bool flag) external onlyOwner {

179:     function setAllowedWhitelistIndex(uint256 newIndex) external onlyOwner {

185:     function addWhitelistedAddress(address whitelisted) external onlyOwner {

191:     function addBatchWhitelist(address[] calldata whitelisted) external onlyOwner {

204:     function checkWhitelist(address from, address to, uint256 amount) external onlyVultisig {

```


*GitHub* : [136](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L136-L136), [142](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L142-L142), [148](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L148-L148), [154](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L154-L154), [160](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L160-L160), [166](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L166-L166), [173](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L173-L173), [179](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L179-L179), [185](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L185-L185), [191](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L191-L191), [204](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L204-L204)

```solidity
📁 File: src/ILOManager.sol

72:     function initILOPool(InitPoolParams calldata params) external override onlyProjectAdmin(params.uniV3Pool) returns (address iloPoolAddress) {

150:     function setPlatformFee(uint16 _platformFee) external onlyOwner() {

155:     function setPerformanceFee(uint16 _performanceFee) external onlyOwner() {

160:     function setFeeTaker(address _feeTaker) external override onlyOwner() {

164:     function setILOPoolImplementation(address iloPoolImplementation) external override onlyOwner() {

169:     function transferAdminProject(address admin, address uniV3Pool) external override onlyProjectAdmin(uniV3Pool) {

175:     function setDefaultDeadlineOffset(uint64 defaultDeadlineOffset) external override onlyOwner() {

180:     function setRefundDeadlineForProject(address uniV3Pool, uint64 refundDeadline) external override onlyOwner() {

201:     function claimRefund(address uniV3PoolAddress) external override onlyProjectAdmin(uniV3PoolAddress) returns(uint256 totalRefundAmount) {

```


*GitHub* : [72](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L72-L72), [150](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L150-L150), [155](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L155-L155), [160](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L160-L160), [164](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L164-L164), [169](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L169-L169), [175](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L175-L175), [180](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L180-L180), [201](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L201-L201)

### [L-23]<a name="l-23"></a> Variables shadowing other definitions

A variable declaration shadowing any other existing definition is error-prone. It can cause confusion for developers, potentially introduce bugs, and reduce the readability and maintainability.

*There are 4 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

// @audit Shadows state variable  _pool
27:     constructor(address _pool, address _baseToken, address _WETH) {

```


*GitHub* : [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L27-L27)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

// @audit Shadows state variable  pool
14:     function consult(address pool, uint32 period) internal view returns (int24 timeWeightedAverageTick) {

// @audit Shadows state variable  baseToken
36:     function getQuoteAtTick(
37:         int24 tick,
38:         uint128 baseAmount,
39:         address baseToken,
40:         address quoteToken
41:     ) internal pure returns (uint256 quoteAmount) {

// @audit Shadows state variable  pool
61:     function getOldestObservationSecondsAgo(address pool) internal view returns (uint32 secondsAgo) {

```


*GitHub* : [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L14-L14), [36](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L36-L41), [61](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L61-L61)

### [L-24]<a name="l-24"></a> File allows a version of solidity that is susceptible to an assembly optimizer bug

In solidity versions `0.8.13` and `0.8.14`, there is an [optimizer bug](https://github.com/ethereum/solidity-blog/blob/499ab8abc19391be7b7b34f88953a067029a5b45/_posts/2022-06-15-inline-assembly-memory-side-effects-bug.md) where, if the use of a variable is in a separate `assembly` block from the block in which it was stored, the `mstore` operation is optimized out, leading to uninitialized memory. The code currently does not have such a pattern of execution, but it does use `mstore`s in `assembly` blocks, so it is a risk for future changes. The affected solidity versions should be avoided if at all possible.

*There are 4 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Vultisig.sol

2: pragma solidity ^0.8.24;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Vultisig.sol#L2-L2)

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

2: pragma solidity ^0.8.24;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L2-L2)

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

2: pragma solidity ^0.8.24;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L2-L2)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

2: pragma solidity ^0.8.24;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L2-L2)

### [L-25]<a name="l-25"></a> Solidity version `0.8.20` may not work on other chains due to `PUSH0`

In Solidity `0.8.20`'s compiler, the default target EVM version has been changed to Shanghai. This version introducesa new opcode called `PUSH0`. However, not all Layer 2 solutions have implemented this opcode yet, leading to deployment failures on thesechains. To overcome this problem, it is recommended to utilize an earlier EVM version.

*There are 4 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Vultisig.sol

2: pragma solidity ^0.8.24;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Vultisig.sol#L2-L2)

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

2: pragma solidity ^0.8.24;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L2-L2)

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

2: pragma solidity ^0.8.24;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L2-L2)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

2: pragma solidity ^0.8.24;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L2-L2)

### [L-26]<a name="l-26"></a> State variables not capped at reasonable values

Consider adding minimum/maximum value checks to ensure that the state variables below can never be used to excessively harm users, including via griefing

*There are 7 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

// @audit newCap
143:         _maxAddressCap = newCap;

// @audit newIndex
180:         _allowedWhitelistIndex = newIndex;

```


*GitHub* : [143](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L143-L143), [180](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L180-L180)

```solidity
📁 File: src/ILOManager.sol

// @audit platformFee
42:         PLATFORM_FEE = platformFee;

// @audit performanceFee
43:         PERFORMANCE_FEE = performanceFee;

// @audit _platformFee
151:         PLATFORM_FEE = _platformFee;

// @audit _performanceFee
156:         PERFORMANCE_FEE = _performanceFee;

// @audit defaultDeadlineOffset
177:         DEFAULT_DEADLINE_OFFSET = defaultDeadlineOffset;

```


*GitHub* : [42](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L42-L42), [43](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L43-L43), [151](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L151-L151), [156](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L156-L156), [177](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L177-L177)

### [L-27]<a name="l-27"></a> Consider implementing two-step procedure for updating protocol addresses

A copy-paste error or a typo may end up bricking protocol functionality, or sending tokens to an address with no known private key. Consider implementing a two-step procedure for updating protocol addresses, where the recipient is set as pending, and must 'accept' the assignment by making an affirmative call. A straight forward way of doing this would be to have the target contracts implement [EIP-165](https://eips.ethereum.org/EIPS/eip-165), and to have the 'set' functions ensure that the recipient is of the right interface type.

*There are 8 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

148:     function setVultisig(address newVultisig) external onlyOwner {

160:     function setOracle(address newOracle) external onlyOwner {

166:     function setPool(address newPool) external onlyOwner {

173:     function setBlacklisted(address blacklisted, bool flag) external onlyOwner {

```


*GitHub* : [148](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L148-L148), [160](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L160-L160), [166](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L166-L166), [173](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L173-L173)

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

22:     function setWhitelistContract(address newWhitelistContract) external onlyOwner {

```


*GitHub* : [22](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L22-L22)

```solidity
📁 File: src/ILOManager.sol

160:     function setFeeTaker(address _feeTaker) external override onlyOwner() {

164:     function setILOPoolImplementation(address iloPoolImplementation) external override onlyOwner() {

169:     function transferAdminProject(address admin, address uniV3Pool) external override onlyProjectAdmin(uniV3Pool) {

```


*GitHub* : [160](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L160-L160), [164](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L164-L164), [169](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L169-L169)


### [L-28]<a name="l-28"></a> Using zero as a parameter

Passing `0` or `0x0` as a function argument can sometimes result in a security issue(e.g. passing zero as the slippage parameter). A historical example is the infamous 0x0 address bug where numerous tokens were lost. This happens because `0` can be interpreted as an uninitialized address, leading to transfers to the `0x0` address, effectively burning tokens. Moreover, `0` as a denominator in division operations would cause a runtime exception. It's also often indicative of a logical error in the caller's code.

Consider using a constant variable with a descriptive name, so it's clear that the argument is intentionally being used, and for the right reasons.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/ILOPool.sol

147:             tokenId = tokenOfOwnerByIndex(recipient, 0);

```


*GitHub* : [147](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L147-L147)

### [L-29]<a name="l-29"></a> Some `ERC20` can revert on a zero value `transfer`

In spite of the fact that [EIP-20](https://github.com/ethereum/EIPs/blob/46b9b698815abbfa628cd1097311deee77dd45c5/EIPS/eip-20.md?plain=1#L116) states that zero-valued transfers must be accepted, some tokens, such as `LEND` will revert if this is attempted, which may cause transactions that involve other tokens (such as batch operations) to fully revert. Consider skipping the transfer if the amount is zero, which will also save gas.

*There are 9 instance(s) of this issue:*

```solidity
📁 File: src/ILOPool.sol

173:         TransferHelper.safeTransferFrom(RAISE_TOKEN, msg.sender, address(this), raiseAmount);

252:         TransferHelper.safeTransfer(_cachedPoolKey.token0, ownerOf(tokenId), amount0);

253:         TransferHelper.safeTransfer(_cachedPoolKey.token1, ownerOf(tokenId), amount1);

259:         TransferHelper.safeTransfer(_cachedPoolKey.token0, feeTaker, amountCollected0-amount0);

260:         TransferHelper.safeTransfer(_cachedPoolKey.token1, feeTaker, amountCollected1-amount1);

358:         TransferHelper.safeTransfer(RAISE_TOKEN, tokenOwner, refundAmount);

```


*GitHub* : [173](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L173-L173), [252](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L252-L252), [253](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L253-L253), [259](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L259-L259), [260](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L260-L260), [358](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L358-L358)

```solidity
📁 File: src/base/PeripheryPayments.sol

30:             IWETH9(WETH9).transfer(recipient, value);

33:             TransferHelper.safeTransfer(token, recipient, value);

36:             TransferHelper.safeTransferFrom(token, payer, recipient, value);

```


*GitHub* : [30](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L30-L30), [33](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L33-L33), [36](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L36-L36)

