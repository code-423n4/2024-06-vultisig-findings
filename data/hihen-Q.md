# QA Report

## Summary

### Low Issues

Total **89 instances** over **16 issues**:

|ID|Issue|Instances|
|:--:|:---|:--:|
| [[L-01]](#l-01-missing-disallow-list-for-erc721) | Missing disallow list for `ERC721` | 1 |
| [[L-02]](#l-02-upgradable-contracts-need-a-constructor-to-init-and-lock-the-implementation-contract) | Upgradable contracts need a constructor to init and lock the implementation contract | 3 |
| [[L-03]](#l-03-missing-zero-address-check-in-initializer) | Missing zero address check in initializer | 5 |
| [[L-04]](#l-04-using--without-specifying-an-upper-bound-in-version-pragma-is-unsafe) | Using `>`/`>=` without specifying an upper bound in version pragma is unsafe | 10 |
| [[L-05]](#l-05-array-is-pushed-but-not-poped) | Array is `push()`ed but not `pop()`ed | 3 |
| [[L-06]](#l-06-state-variables-not-limited-to-reasonable-values) | State variables not limited to reasonable values | 6 |
| [[L-07]](#l-07-written-only-contract-variables) | Written only contract variables | 3 |
| [[L-08]](#l-08-downcasting-other-types-to-an-address-can-cause-collisions) | Downcasting other types to an address can cause collisions | 1 |
| [[L-09]](#l-09-use-abiencodecall-instead-of-abiencodewithsignatureabiencodewithselector) | Use `abi.encodeCall()` instead of `abi.encodeWithSignature()`/`abi.encodeWithSelector()` | 3 |
| [[L-10]](#l-10-constructor--initialization-function-lacks-parameter-validation) | Constructor / initialization function lacks parameter validation | 5 |
| [[L-11]](#l-11-unsafe-solidity-low-level-call-can-cause-gas-grief-attack) | Unsafe solidity low-level call can cause gas grief attack | 4 |
| [[L-12]](#l-12-functions-calling-contractsaddresses-with-transfer-hooks-should-be-protected-by-reentrancy-guard) | Functions calling contracts/addresses with transfer hooks should be protected by reentrancy guard | 10 |
| [[L-13]](#l-13-critical-functions-should-be-controlled-by-time-locks) | Critical functions should be controlled by time locks | 13 |
| [[L-14]](#l-14-missing-contract-existence-checks-before-low-level-calls) | Missing contract existence checks before low-level calls | 4 |
| [[L-15]](#l-15-tokens-may-be-minted-to-the-zero-address) | Tokens may be minted to the zero address | 4 |
| [[L-16]](#l-16-code-does-not-follow-the-best-practice-of-check-effects-interaction) | Code does not follow the best practice of check-effects-interaction | 14 |

### Non Critical Issues

Total **581 instances** over **52 issues**:

|ID|Issue|Instances|
|:--:|:---|:--:|
| [[N-01]](#n-01-import-declarations-should-import-specific-identifiers-rather-than-the-whole-file) | Import declarations should import specific identifiers, rather than the whole file | 50 |
| [[N-02]](#n-02-visibility-of-state-variables-is-not-explicitly-defined) | Visibility of state variables is not explicitly defined | 4 |
| [[N-03]](#n-03-names-of-privateinternal-functions-should-be-prefixed-with-an-underscore) | Names of `private`/`internal` functions should be prefixed with an underscore | 24 |
| [[N-04]](#n-04-names-of-privateinternal-state-variables-should-be-prefixed-with-an-underscore) | Names of `private`/`internal` state variables should be prefixed with an underscore | 6 |
| [[N-05]](#n-05-redundant-inheritance-specifier) | Redundant inheritance specifier | 2 |
| [[N-06]](#n-06-strings-should-use-double-quotes-rather-than-single-quotes) | Strings should use double quotes rather than single quotes | 11 |
| [[N-07]](#n-07-use-of-override-is-unnecessary) | Use of `override` is unnecessary | 1 |
| [[N-08]](#n-08-consider-providing-a-ranged-getter-for-array-state-variables) | Consider providing a ranged getter for array state variables | 2 |
| [[N-09]](#n-09-assembly-blocks-should-have-extensive-comments) | Assembly blocks should have extensive comments | 31 |
| [[N-10]](#n-10-consider-splitting-complex-checks-into-multiple-steps) | Consider splitting complex checks into multiple steps | 4 |
| [[N-11]](#n-11-complex-casting) | Complex casting | 1 |
| [[N-12]](#n-12-complex-math-should-be-split-into-multiple-steps) | Complex math should be split into multiple steps | 4 |
| [[N-13]](#n-13-consider-adding-a-blockdeny-list) | Consider adding a block/deny-list | 3 |
| [[N-14]](#n-14-convert-simple-if-statements-to-ternary-expressions) | Convert simple `if`-statements to ternary expressions | 3 |
| [[N-15]](#n-15-upper_case-names-should-be-reserved-for-constantimmutable-variables) | UPPER_CASE names should be reserved for `constant`/`immutable` variables | 19 |
| [[N-16]](#n-16-contract-timekeeping-will-break-earlier-than-the-ethereum-network-itself-will-stop-working) | Contract timekeeping will break earlier than the Ethereum network itself will stop working | 1 |
| [[N-17]](#n-17-consider-emitting-an-event-at-the-end-of-the-constructor) | Consider emitting an event at the end of the constructor | 5 |
| [[N-18]](#n-18-events-are-emitted-without-the-sender-information) | Events are emitted without the sender information | 3 |
| [[N-19]](#n-19-inconsistent-floating-version-pragma) | Inconsistent floating version pragma | 7 |
| [[N-20]](#n-20-imports-could-be-organized-more-systematically) | Imports could be organized more systematically | 12 |
| [[N-21]](#n-21-imports-should-use-double-quotes-rather-than-single-quotes) | Imports should use double quotes rather than single quotes | 42 |
| [[N-22]](#n-22-openzeppelincontracts-should-be-upgraded-to-a-newer-version) | @openzeppelin/contracts should be upgraded to a newer version | 6 |
| [[N-23]](#n-23-consider-moving-duplicated-strings-to-constants) | Consider moving duplicated strings to constants | 23 |
| [[N-24]](#n-24-functions-should-be-named-in-mixedcase-style) | Functions should be named in mixedCase style | 2 |
| [[N-25]](#n-25-variable-names-for-immutables-should-use-upper_case_with_underscores) | Variable names for `immutable`s should use UPPER_CASE_WITH_UNDERSCORES | 2 |
| [[N-26]](#n-26-modifiers-should-be-named-in-mixedcase-style) | Modifiers should be named in mixedCase style | 1 |
| [[N-27]](#n-27-named-imports-of-parent-contracts-are-missing) | Named imports of parent contracts are missing | 19 |
| [[N-28]](#n-28-constants-should-be-put-on-the-left-side-of-comparisons) | Constants should be put on the left side of comparisons | 19 |
| [[N-29]](#n-29-large-multiples-of-ten-should-use-scientific-notation) | Large multiples of ten should use scientific notation | 4 |
| [[N-30]](#n-30-high-cyclomatic-complexity) | High cyclomatic complexity | 1 |
| [[N-31]](#n-31-typos) | Typos | 5 |
| [[N-32]](#n-32-consider-bounding-input-array-length) | Consider bounding input array length | 6 |
| [[N-33]](#n-33-unused-function-parameters) | Unused function parameters | 1 |
| [[N-34]](#n-34-unused-named-return) | Unused named return | 11 |
| [[N-35]](#n-35-consider-using-delete-rather-than-assigning-zero-to-clear-values) | Consider using `delete` rather than assigning zero to clear values | 1 |
| [[N-36]](#n-36-use-the-latest-solidity-version) | Use the latest Solidity version | 22 |
| [[N-37]](#n-37-use-a-struct-to-encapsulate-multiple-function-parameters) | Use a struct to encapsulate multiple function parameters | 2 |
| [[N-38]](#n-38-returning-a-struct-instead-of-a-bunch-of-variables-is-better) | Returning a struct instead of a bunch of variables is better | 7 |
| [[N-39]](#n-39-contract-variables-should-have-comments) | Contract variables should have comments | 11 |
| [[N-40]](#n-40-missing-event-when-a-state-variables-is-set-in-constructor) | Missing event when a state variables is set in constructor | 2 |
| [[N-41]](#n-41-empty-bytes-check-is-missing) | Empty bytes check is missing | 2 |
| [[N-42]](#n-42-multiple-mappings-with-same-keys-can-be-combined-into-a-single-struct-mapping-for-readability) | Multiple mappings with same keys can be combined into a single struct mapping for readability | 5 |
| [[N-43]](#n-43-missing-event-for-critical-changes) | Missing event for critical changes | 12 |
| [[N-44]](#n-44-non-assembly-method-available) | Non-assembly method available | 2 |
| [[N-45]](#n-45-consider-adding-emergency-stop-functionality) | Consider adding emergency-stop functionality | 4 |
| [[N-46]](#n-46-avoid-the-use-of-sensitive-terms) | Avoid the use of sensitive terms | 144 |
| [[N-47]](#n-47-missing-checks-for-uint-state-variable-assignments) | Missing checks for uint state variable assignments | 7 |
| [[N-48]](#n-48-use-the-modern-upgradeable-contract-paradigm) | Use the Modern Upgradeable Contract Paradigm | 4 |
| [[N-49]](#n-49-large-or-complicated-code-bases-should-implement-invariant-tests) | Large or complicated code bases should implement invariant tests | 2 |
| [[N-50]](#n-50-the-default-value-is-manually-set-when-it-is-declared) | The default value is manually set when it is declared | 12 |
| [[N-51]](#n-51-contracts-should-have-all-publicexternal-functions-exposed-by-interfaces) | Contracts should have all `public`/`external` functions exposed by `interface`s | 4 |
| [[N-52]](#n-52-use-scopes-sparingly) | Use scopes sparingly | 3 |

## Low Issues

### [L-01] Missing disallow list for `ERC721`

Recently, there has been an increase in the theft of NFTs. These stolen NFTs are then added to platforms where they can be easily converted into liquidity.

Some popular marketplaces(e.g. Opensea), have already taken steps to combat this problem by introducing a disallow list feature. This means that if an NFT is reported as stolen, it won't be listed or sold on their platform.
This may increase the centralization of the project, but it can help solve this problem if it is a concern.

There is 1 instance:

- *ILOPool.sol* ( [24-32](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L24-L32) ):

```solidity
24: contract ILOPool is
25:     ERC721,
26:     IILOPool,
27:     ILOWhitelist,
28:     ILOVest,
29:     Initializable,
30:     Multicall,
31:     ILOPoolImmutableState,
32:     LiquidityManagement
```

### [L-02] Upgradable contracts need a constructor to init and lock the implementation contract

An uninitialized contract can be taken over by an attacker. For an upgradable contract, this applies to both the proxy and its implementation contract, which may impact the proxy.
To prevent the implementation contract from being used, we should trigger the initialization in the constructor to automatically lock it when it is deployed.
For contracts that inherit `Initializable`, the `_disableInitializers()` function [is suggested to do this job](https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/blob/4d9d9073b84f56fe3eea360e5067c6ffd864c43d/contracts/proxy/utils/Initializable.sol#L43-L56).

There are 3 instances:

- *ILOManager.sol* ( [29-29](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L29-L29) ):

```solidity
29:     constructor () {
```

- *ILOPool.sol* ( [49-49](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L49-L49) ):

```solidity
49:     constructor() ERC721('', '') {
```

- *Initializable.sol* ( [5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/Initializable.sol#L5) ):

```solidity
/// @audit Missing constructor to initialize the implementation contract
5: abstract contract Initializable {
```

### [L-03] Missing zero address check in initializer

Consider adding a zero address check for each address type parameter in initializer.

There are 5 instances:

- *ILOManager.sol* ( [33-41](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L33-L41) ):

```solidity
/// @audit `initialOwner not checked`
/// @audit `_feeTaker not checked`
/// @audit `iloPoolImplementation not checked`
/// @audit `uniV3Factory not checked`
/// @audit `weth9 not checked`
33:     function initialize(
34:         address initialOwner,
35:         address _feeTaker,
36:         address iloPoolImplementation,
37:         address uniV3Factory,
38:         address weth9,
39:         uint16 platformFee,
40:         uint16 performanceFee
41:     ) external override whenNotInitialized() {
```

### [L-04] Using `>`/`>=` without specifying an upper bound in version pragma is unsafe

There **will** be breaking changes in future versions of solidity, and at that point your code will no longer be compatible. While you may have the specific version to use in a configuration file, others that include your source files may not.

<details>
<summary>There are 10 instances (click to show):</summary>

- *FullMath.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L2) ):

```solidity
2: pragma solidity >=0.4.0;
```

- *OracleLibrary.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L2) ):

```solidity
2: pragma solidity >=0.5.0;
```

- *TickMath.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L2) ):

```solidity
2: pragma solidity >=0.5.0;
```

- *PeripheryPayments.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L2) ):

```solidity
2: pragma solidity >=0.7.5;
```

- *ChainId.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/ChainId.sol#L2) ):

```solidity
2: pragma solidity >=0.7.0;
```

- *LiquidityAmounts.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/LiquidityAmounts.sol#L2) ):

```solidity
2: pragma solidity >=0.5.0;
```

- *PoolAddress.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/PoolAddress.sol#L2) ):

```solidity
2: pragma solidity >=0.5.0;
```

- *PositionKey.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/PositionKey.sol#L2) ):

```solidity
2: pragma solidity >=0.5.0;
```

- *SqrtPriceMathPartial.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/SqrtPriceMathPartial.sol#L2) ):

```solidity
2: pragma solidity >=0.5.0;
```

- *TransferHelper.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L2) ):

```solidity
2: pragma solidity >=0.6.0;
```

</details>

### [L-05] Array is `push()`ed but not `pop()`ed

Array entries are added but are never removed. Consider whether this should be the case, or whether there should be a maximum, or whether old entries should be removed. Cases where there are specific potential problems will be flagged separately under a different issue.

There are 3 instances:

- *ILOManager.sol* ( [106-106](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L106-L106) ):

```solidity
106:         _initializedILOPools[params.uniV3Pool].push(iloPoolAddress);
```

- *ILOPool.sol* ( [93-93](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L93-L93), [325-325](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L325-L325) ):

```solidity
93:             _vestingConfigs.push(params.vestingConfigs[index]);

325:                 schedule.push(projectConfig.schedule[i]);
```

### [L-06] State variables not limited to reasonable values

Consider adding appropriate minimum/maximum value checks to ensure that the following state variables can never be used to excessively harm users, including via griefing.

There are 6 instances:

- *Whitelist.sol* ( [143-143](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L143-L143) ):

```solidity
143:         _maxAddressCap = newCap;
```

- *ILOManager.sol* ( [42-42](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L42-L42), [43-43](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L43-L43), [151-151](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L151-L151), [156-156](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L156-L156), [177-177](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L177-L177) ):

```solidity
42:         PLATFORM_FEE = platformFee;

43:         PERFORMANCE_FEE = performanceFee;

151:         PLATFORM_FEE = _platformFee;

156:         PERFORMANCE_FEE = _performanceFee;

177:         DEFAULT_DEADLINE_OFFSET = defaultDeadlineOffset;
```

### [L-07] Written only contract variables

Write only contract variables are only written in the contract and are never read and cannot be accessed through an interface.
It is recommended to check if there is a bug causing the missing readings, or if some `view` interfaces should be provided. If not, consider removing them to improve code clarity, avoid confusion, and save gas.

There are 3 instances:

- *ILOPool.sol* ( [62-62](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L62-L62), [144-144](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L144-L144), [315-315](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L315-L315) ):

```solidity
62:         _nextId = 1;

144:             _mint(recipient, (tokenId = _nextId++));

315:             _mint(projectConfig.recipient, (tokenId = _nextId++));
```

### [L-08] Downcasting other types to an address can cause collisions

Downcasting other types to an address will truncates the upper bytes, which means that multiple values can be mapped to an address, i.e. address collisions can occur.

There is 1 instance:

- *PoolAddress.sol* ( [35-46](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/PoolAddress.sol#L35-L46) ):

```solidity
35:         pool = address(
36:             uint256(
37:                 keccak256(
38:                     abi.encodePacked(
39:                         hex'ff',
40:                         factory,
41:                         keccak256(abi.encode(key.token0, key.token1, key.fee)),
42:                         POOL_INIT_CODE_HASH
43:                     )
44:                 )
45:             )
46:         );
```

### [L-09] Use `abi.encodeCall()` instead of `abi.encodeWithSignature()`/`abi.encodeWithSelector()`

Function `abi.encodeCall()` provides [type-safe encode utility](https://github.com/OpenZeppelin/openzeppelin-contracts/issues/3693) comparing with `abi.encodeWithSignature()`/`abi.encodeWithSelector()`.

There are 3 instances:

- *TransferHelper.sol* ( [20-20](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L20-L20), [34-34](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L34-L34), [48-48](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L48-L48) ):

```solidity
20:             token.call(abi.encodeWithSelector(IERC20.transferFrom.selector, from, to, value));

34:         (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.transfer.selector, to, value));

48:         (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.approve.selector, to, value));
```

### [L-10] Constructor / initialization function lacks parameter validation

Constructors and initialization functions play a critical role in contracts by setting important initial states when the contract is first deployed before the system starts. The parameters passed to the constructor and initialization functions directly affect the behavior of the contract / protocol. If incorrect parameters are provided, the system may fail to run, behave abnormally, be unstable, or lack security. Therefore, it's crucial to carefully check each parameter in the constructor and initialization functions. If an exception is found, the transaction should be rolled back.

There are 5 instances:

- *UniswapV3Oracle.sol* ( [27-27](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/UniswapV3Oracle.sol#L27-L27) ):

```solidity
/// @audit `_pool`
/// @audit `_baseToken`
/// @audit `_WETH`
27:     constructor(address _pool, address _baseToken, address _WETH) {
```

- *ILOManager.sol* ( [33-41](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L33-L41) ):

```solidity
/// @audit `platformFee`
/// @audit `performanceFee`
33:     function initialize(
34:         address initialOwner,
35:         address _feeTaker,
36:         address iloPoolImplementation,
37:         address uniV3Factory,
38:         address weth9,
39:         uint16 platformFee,
40:         uint16 performanceFee
41:     ) external override whenNotInitialized() {
```

### [L-11] Unsafe solidity low-level call can cause gas grief attack

Using the low-level calls of a solidity address can leave the contract open to gas grief attacks. These attacks occur when the called contract returns a large amount of data.
So when calling an external contract, it is necessary to check the length of the return data before reading/copying it (using `returndatasize()`).

There are 4 instances:

- *TransferHelper.sol* ( [20-20](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L20-L20), [34-34](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L34-L34), [48-48](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L48-L48), [57-57](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L57-L57) ):

```solidity
20:             token.call(abi.encodeWithSelector(IERC20.transferFrom.selector, from, to, value));

34:         (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.transfer.selector, to, value));

48:         (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.approve.selector, to, value));

57:         (bool success, ) = to.call{value: value}(new bytes(0));
```

### [L-12] Functions calling contracts/addresses with transfer hooks should be protected by reentrancy guard

Even if the function follows the best practice of check-effects-interaction, not using a reentrancy guard when there may be transfer hooks opens the users of this protocol up to [read-only reentrancy vulnerability](https://chainsecurity.com/curve-lp-oracle-manipulation-post-mortem/) with no way to protect them except by block-listing the entire protocol.

<details>
<summary>There are 10 instances (click to show):</summary>

- *Whitelist.sol* ( [73-73](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L73-L73) ):

```solidity
73:         payable(_msgSender()).transfer(msg.value);
```

- *ILOPool.sol* ( [173-173](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L173-L173), [252-252](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L252-L252), [253-253](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L253-L253), [259-259](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L259-L259), [260-260](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L260-L260), [358-358](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L358-L358), [370-370](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L370-L370) ):

```solidity
173:         TransferHelper.safeTransferFrom(RAISE_TOKEN, msg.sender, address(this), raiseAmount);

252:         TransferHelper.safeTransfer(_cachedPoolKey.token0, ownerOf(tokenId), amount0);

253:         TransferHelper.safeTransfer(_cachedPoolKey.token1, ownerOf(tokenId), amount1);

259:         TransferHelper.safeTransfer(_cachedPoolKey.token0, feeTaker, amountCollected0-amount0);

260:         TransferHelper.safeTransfer(_cachedPoolKey.token1, feeTaker, amountCollected1-amount1);

358:         TransferHelper.safeTransfer(RAISE_TOKEN, tokenOwner, refundAmount);

370:             TransferHelper.safeTransfer(SALE_TOKEN, projectAdmin, refundAmount);
```

- *PeripheryPayments.sol* ( [33-33](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L33-L33), [36-36](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L36-L36) ):

```solidity
33:             TransferHelper.safeTransfer(token, recipient, value);

36:             TransferHelper.safeTransferFrom(token, payer, recipient, value);
```

</details>

### [L-13] Critical functions should be controlled by time locks

It is a good practice to give time for users to react and adjust to critical changes. A timelock provides more guarantees and reduces the level of trust required, thus decreasing risk for users. It also indicates that the project is legitimate (less risk of a malicious owner making a sandwich attack on a user).

<details>
<summary>There are 13 instances (click to show):</summary>

- *Whitelist.sol* ( [148-148](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L148-L148), [160-160](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L160-L160), [166-166](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L166-L166), [173-173](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L173-L173), [185-185](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L185-L185) ):

```solidity
148:     function setVultisig(address newVultisig) external onlyOwner {

160:     function setOracle(address newOracle) external onlyOwner {

166:     function setPool(address newPool) external onlyOwner {

173:     function setBlacklisted(address blacklisted, bool flag) external onlyOwner {

185:     function addWhitelistedAddress(address whitelisted) external onlyOwner {
```

- *VultisigWhitelisted.sol* ( [22-22](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L22-L22) ):

```solidity
22:     function setWhitelistContract(address newWhitelistContract) external onlyOwner {
```

- *ILOManager.sol* ( [160-160](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L160-L160), [164-164](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L164-L164), [180-180](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L180-L180) ):

```solidity
160:     function setFeeTaker(address _feeTaker) external override onlyOwner() {

164:     function setILOPoolImplementation(address iloPoolImplementation) external override onlyOwner() {

180:     function setRefundDeadlineForProject(address uniV3Pool, uint64 refundDeadline) external override onlyOwner() {
```

- *ILOWhitelist.sol* ( [12-12](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L12-L12), [34-34](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L34-L34), [47-47](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L47-L47), [52-52](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L52-L52) ):

```solidity
12:     function setOpenToAll(bool openToAll) external override onlyProjectAdmin{

34:     function batchRemoveWhitelist(address[] calldata users) external override onlyProjectAdmin{

47:     function _removeWhitelist(address user) internal {

52:     function _setWhitelist(address user) internal {
```

</details>

### [L-14] Missing contract existence checks before low-level calls

Low-level calls return success if there is no code present at the specified address. In addition to the zero-address checks, add a check to verify that `<address>.code.length > 0`.

There are 4 instances:

- *TransferHelper.sol* ( [20-20](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L20-L20), [34-34](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L34-L34), [48-48](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L48-L48), [57-57](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L57-L57) ):

```solidity
20:             token.call(abi.encodeWithSelector(IERC20.transferFrom.selector, from, to, value));

34:         (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.transfer.selector, to, value));

48:         (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.approve.selector, to, value));

57:         (bool success, ) = to.call{value: value}(new bytes(0));
```

### [L-15] Tokens may be minted to the zero address

Neither the listed functions, nor `_mint()` prevent minting to `address(0x0)`

There are 4 instances:

- *Vultisig.sol* ( [13-13](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Vultisig.sol#L13-L13) ):

```solidity
13:         _mint(_msgSender(), 100_000_000 * 1e18);
```

- *ILOPool.sol* ( [144-144](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L144-L144), [315-315](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L315-L315) ):

```solidity
144:             _mint(recipient, (tokenId = _nextId++));

315:             _mint(projectConfig.recipient, (tokenId = _nextId++));
```

- *LiquidityManagement.sol* ( [48-54](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L48-L54) ):

```solidity
48:         (amount0, amount1) = params.pool.mint(
49:             address(this),
50:             TICK_LOWER,
51:             TICK_UPPER,
52:             params.liquidity,
53:             ""
54:         );
```

### [L-16] Code does not follow the best practice of check-effects-interaction

Code should follow the best-practice of [check-effects-interaction](https://blockchain-academy.hs-mittweida.de/courses/solidity-coding-beginners-to-intermediate/lessons/solidity-11-coding-patterns/topic/checks-effects-interactions/), where state variables are updated before any external calls are made. Doing so prevents a large class of reentrancy bugs.

<details>
<summary>There are 14 instances (click to show):</summary>

- *Whitelist.sol* ( [226-226](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L226-L226) ):

```solidity
/// @audit `peek()` is called on line 221
226:             _contributed[to] += estimatedETHAmount;
```

- *ILOPool.sol* ( [68-68](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L68-L68), [69-69](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L69-L69), [70-70](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L70-L70), [71-71](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L71-L71), [72-72](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L72-L72), [73-73](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L73-L73), [74-74](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L74-L74), [75-75](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L75-L75), [76-76](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L76-L76), [81-88](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L81-L88), [92-92](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L92-L92), [334-334](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L334-L334) ):

```solidity
/// @audit `project()` is called on line 65
68:         RAISE_TOKEN = _project.raiseToken;

/// @audit `project()` is called on line 65
69:         SALE_TOKEN = _project.saleToken;

/// @audit `project()` is called on line 65
70:         _cachedUniV3PoolAddress = params.uniV3Pool;

/// @audit `project()` is called on line 65
71:         _cachedPoolKey = _project._cachedPoolKey;

/// @audit `project()` is called on line 65
72:         TICK_LOWER = params.tickLower;

/// @audit `project()` is called on line 65
73:         TICK_UPPER = params.tickUpper;

/// @audit `project()` is called on line 65
74:         SQRT_RATIO_LOWER_X96 = params.sqrtRatioLowerX96;

/// @audit `project()` is called on line 65
75:         SQRT_RATIO_UPPER_X96 = params.sqrtRatioUpperX96;

/// @audit `project()` is called on line 65
76:         SQRT_RATIO_X96 = _project.initialPoolPriceX96;

/// @audit `project()` is called on line 65
81:         saleInfo = SaleInfo({
82:             hardCap: params.hardCap,
83:             softCap: params.softCap,
84:             maxCapPerUser: params.maxCapPerUser,
85:             start: params.start,
86:             end: params.end,
87:             maxSaleAmount: maxSaleAmount
88:         });

/// @audit `project()` is called on line 65
92:         for (uint256 index = 0; index < params.vestingConfigs.length; index++) {

/// @audit `project()` is called on line 308
334:         _launchSucceeded = true;
```

- *Multicall.sol* ( [25-25](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/Multicall.sol#L25-L25) ):

```solidity
/// @audit `delegatecall()` is called on line 14
25:             results[i] = result;
```

</details>

## Non Critical Issues

### [N-01] Import declarations should import specific identifiers, rather than the whole file

Using import declarations of the form `import {<identifier_name>} from "some/file.sol"` avoids polluting the symbol namespace making flattened files smaller, and speeds up compilation (but does not save any gas).

<details>
<summary>There are 50 instances (click to show):</summary>

- *OracleLibrary.sol* ( [3](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L3), [4](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L4), [5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L5) ):

```solidity
3: import "@uniswap/v3-core/contracts/interfaces/IUniswapV3Pool.sol";

4: import "./FullMath.sol";

5: import "./TickMath.sol";
```

- *ILOManager.sol* ( [5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L5), [6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L6), [7](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L7), [8](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L8), [9](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L9), [10](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L10), [11](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L11), [12](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L12), [13](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L13) ):

```solidity
5: import "./interfaces/IILOManager.sol";

6: import "./interfaces/IILOPool.sol";

7: import "./libraries/ChainId.sol";

8: import './base/Initializable.sol';

9: import '@uniswap/v3-core/contracts/interfaces/IUniswapV3Factory.sol';

10: import '@uniswap/v3-core/contracts/interfaces/IUniswapV3Pool.sol';

11: import '@uniswap/v3-core/contracts/libraries/TickMath.sol';

12: import "@openzeppelin/contracts/access/Ownable.sol";

13: import '@openzeppelin/contracts/proxy/Clones.sol';
```

- *ILOPool.sol* ( [5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L5), [6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L6), [7](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L7), [9](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L9), [11](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L11), [12](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L12), [13](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L13), [14](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L14), [15](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L15), [16](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L16), [17](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L17), [18](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L18), [19](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L19), [20](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L20) ):

```solidity
5: import '@uniswap/v3-core/contracts/interfaces/IUniswapV3Pool.sol';

6: import '@uniswap/v3-core/contracts/libraries/FixedPoint128.sol';

7: import '@uniswap/v3-core/contracts/libraries/FullMath.sol';

9: import '@openzeppelin/contracts/token/ERC721/ERC721.sol';

11: import './interfaces/IILOPool.sol';

12: import './interfaces/IILOManager.sol';

13: import './libraries/PositionKey.sol';

14: import './libraries/SqrtPriceMathPartial.sol';

15: import './base/ILOVest.sol';

16: import './base/LiquidityManagement.sol';

17: import './base/ILOPoolImmutableState.sol';

18: import './base/Initializable.sol';

19: import './base/Multicall.sol';

20: import "./base/ILOWhitelist.sol";
```

- *ILOPoolImmutableState.sol* ( [4](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L4), [5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L5) ):

```solidity
4: import '../interfaces/IILOPoolImmutableState.sol';

5: import '../libraries/PoolAddress.sol';
```

- *ILOVest.sol* ( [5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L5) ):

```solidity
5: import '../interfaces/IILOVest.sol';
```

- *ILOWhitelist.sol* ( [5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L5), [6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L6) ):

```solidity
5: import '@openzeppelin/contracts/utils/EnumerableSet.sol';

6: import '../interfaces/IILOWhitelist.sol';
```

- *LiquidityManagement.sol* ( [5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L5), [6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L6), [7](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L7), [9](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L9), [10](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L10), [12](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L12), [13](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L13) ):

```solidity
5: import '@uniswap/v3-core/contracts/interfaces/IUniswapV3Factory.sol';

6: import '@uniswap/v3-core/contracts/interfaces/IUniswapV3Pool.sol';

7: import '@uniswap/v3-core/contracts/interfaces/callback/IUniswapV3MintCallback.sol';

9: import '../libraries/PoolAddress.sol';

10: import '../libraries/LiquidityAmounts.sol';

12: import './PeripheryPayments.sol';

13: import './ILOPoolImmutableState.sol';
```

- *Multicall.sol* ( [5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/Multicall.sol#L5) ):

```solidity
5: import '../interfaces/IMulticall.sol';
```

- *PeripheryPayments.sol* ( [4](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L4), [6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L6), [8](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L8), [10](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L10) ):

```solidity
4: import '@openzeppelin/contracts/token/ERC20/IERC20.sol';

6: import '../interfaces/external/IWETH9.sol';

8: import '../libraries/TransferHelper.sol';

10: import './ILOPoolImmutableState.sol';
```

- *LiquidityAmounts.sol* ( [4](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/LiquidityAmounts.sol#L4), [5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/LiquidityAmounts.sol#L5), [6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/LiquidityAmounts.sol#L6) ):

```solidity
4: import '@uniswap/v3-core/contracts/libraries/FullMath.sol';

5: import '@uniswap/v3-core/contracts/libraries/FixedPoint96.sol';

6: import '@uniswap/v3-core/contracts/libraries/SqrtPriceMath.sol';
```

- *SqrtPriceMathPartial.sol* ( [4](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/SqrtPriceMathPartial.sol#L4), [5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/SqrtPriceMathPartial.sol#L5), [6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/SqrtPriceMathPartial.sol#L6) ):

```solidity
4: import '@uniswap/v3-core/contracts/libraries/FullMath.sol';

5: import '@uniswap/v3-core/contracts/libraries/UnsafeMath.sol';

6: import '@uniswap/v3-core/contracts/libraries/FixedPoint96.sol';
```

- *TransferHelper.sol* ( [4](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L4) ):

```solidity
4: import '@openzeppelin/contracts/token/ERC20/IERC20.sol';
```

</details>

### [N-02] Visibility of state variables is not explicitly defined

To avoid misunderstandings and unexpected state accesses, it is recommended to explicitly define the visibility of each state variable.

There are 4 instances:

- *ILOPool.sol* ( [34-34](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L34-L34), [48-48](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L48-L48) ):

```solidity
34:     SaleInfo saleInfo;

48:     uint256 totalRaised;
```

- *ILOPoolImmutableState.sol* ( [13-13](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L13-L13) ):

```solidity
13:     uint16 constant BPS = 10000;
```

- *ILOVest.sol* ( [8-8](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L8-L8) ):

```solidity
8:     mapping(uint256=>PositionVest) _positionVests;
```

### [N-03] Names of `private`/`internal` functions should be prefixed with an underscore

It is recommended by the [Solidity Style Guide](https://docs.soliditylang.org/en/v0.8.20/style-guide.html#underscore-prefix-for-non-external-functions-and-variables).

<details>
<summary>There are 24 instances (click to show):</summary>

- *FullMath.sol* ( [14-14](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L14-L14), [109-109](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L109-L109) ):

```solidity
14:     function mulDiv(uint256 a, uint256 b, uint256 denominator) internal pure returns (uint256 result) {

109:     function mulDivRoundingUp(uint256 a, uint256 b, uint256 denominator) internal pure returns (uint256 result) {
```

- *OracleLibrary.sol* ( [14-14](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L14-L14), [36-41](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L36-L41), [61-61](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L61-L61) ):

```solidity
14:     function consult(address pool, uint32 period) internal view returns (int24 timeWeightedAverageTick) {

36:     function getQuoteAtTick(
37:         int24 tick,
38:         uint128 baseAmount,
39:         address baseToken,
40:         address quoteToken
41:     ) internal pure returns (uint256 quoteAmount) {

61:     function getOldestObservationSecondsAgo(address pool) internal view returns (uint32 secondsAgo) {
```

- *TickMath.sol* ( [23-23](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L23-L23), [61-61](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L61-L61) ):

```solidity
23:     function getSqrtRatioAtTick(int24 tick) internal pure returns (uint160 sqrtPriceX96) {

61:     function getTickAtSqrtRatio(uint160 sqrtPriceX96) internal pure returns (int24 tick) {
```

- *LiquidityManagement.sol* ( [41-46](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L41-L46) ):

```solidity
41:     function addLiquidity(AddLiquidityParams memory params)
42:         internal
43:         returns (
44:             uint256 amount0,
45:             uint256 amount1
46:         )
```

- *PeripheryPayments.sol* ( [21-26](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L21-L26) ):

```solidity
21:     function pay(
22:         address token,
23:         address payer,
24:         address recipient,
25:         uint256 value
26:     ) internal {
```

- *ChainId.sol* ( [8-8](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/ChainId.sol#L8-L8) ):

```solidity
8:     function get() internal pure returns (uint256 chainId) {
```

- *LiquidityAmounts.sol* ( [14-14](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/LiquidityAmounts.sol#L14-L14), [24-28](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/LiquidityAmounts.sol#L24-L28), [40-44](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/LiquidityAmounts.sol#L40-L44), [54-58](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/LiquidityAmounts.sol#L54-L58), [74-78](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/LiquidityAmounts.sol#L74-L78) ):

```solidity
14:     function toUint128(uint256 x) private pure returns (uint128 y) {

24:     function getLiquidityForAmount0(
25:         uint160 sqrtRatioAX96,
26:         uint160 sqrtRatioBX96,
27:         uint256 amount0
28:     ) internal pure returns (uint128 liquidity) {

40:     function getLiquidityForAmount1(
41:         uint160 sqrtRatioAX96,
42:         uint160 sqrtRatioBX96,
43:         uint256 amount1
44:     ) internal pure returns (uint128 liquidity) {

54:     function getAmount0ForLiquidity(
55:         uint160 sqrtRatioAX96,
56:         uint160 sqrtRatioBX96,
57:         uint128 liquidity
58:     ) internal pure returns (uint256 amount0) {

74:     function getAmount1ForLiquidity(
75:         uint160 sqrtRatioAX96,
76:         uint160 sqrtRatioBX96,
77:         uint128 liquidity
78:     ) internal pure returns (uint256 amount1) {
```

- *PoolAddress.sol* ( [20-24](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/PoolAddress.sol#L20-L24), [33-33](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/PoolAddress.sol#L33-L33) ):

```solidity
20:     function getPoolKey(
21:         address tokenA,
22:         address tokenB,
23:         uint24 fee
24:     ) internal pure returns (PoolKey memory) {

33:     function computeAddress(address factory, PoolKey memory key) internal pure returns (address pool) {
```

- *PositionKey.sol* ( [6-10](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/PositionKey.sol#L6-L10) ):

```solidity
6:     function compute(
7:         address owner,
8:         int24 tickLower,
9:         int24 tickUpper
10:     ) internal pure returns (bytes32) {
```

- *SqrtPriceMathPartial.sol* ( [20-25](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/SqrtPriceMathPartial.sol#L20-L25), [49-54](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/SqrtPriceMathPartial.sol#L49-L54) ):

```solidity
20:     function getAmount0Delta(
21:         uint160 sqrtRatioAX96,
22:         uint160 sqrtRatioBX96,
23:         uint128 liquidity,
24:         bool roundUp
25:     ) internal pure returns (uint256 amount0) {

49:     function getAmount1Delta(
50:         uint160 sqrtRatioAX96,
51:         uint160 sqrtRatioBX96,
52:         uint128 liquidity,
53:         bool roundUp
54:     ) internal pure returns (uint256 amount1) {
```

- *TransferHelper.sol* ( [13-18](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L13-L18), [29-33](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L29-L33), [43-47](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L43-L47), [56-56](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L56-L56) ):

```solidity
13:     function safeTransferFrom(
14:         address token,
15:         address from,
16:         address to,
17:         uint256 value
18:     ) internal {

29:     function safeTransfer(
30:         address token,
31:         address to,
32:         uint256 value
33:     ) internal {

43:     function safeApprove(
44:         address token,
45:         address to,
46:         uint256 value
47:     ) internal {

56:     function safeTransferETH(address to, uint256 value) internal {
```

</details>

### [N-04] Names of `private`/`internal` state variables should be prefixed with an underscore

It is recommended by the [Solidity Style Guide](https://docs.soliditylang.org/en/v0.8.20/style-guide.html#underscore-prefix-for-non-external-functions-and-variables).

There are 6 instances:

- *ILOManager.sol* ( [19-19](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L19-L19) ):

```solidity
19:     uint64 private DEFAULT_DEADLINE_OFFSET = 7 * 24 * 60 * 60; // 7 days
```

- *ILOPool.sol* ( [34-34](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L34-L34), [48-48](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L48-L48) ):

```solidity
34:     SaleInfo saleInfo;

48:     uint256 totalRaised;
```

- *ILOPoolImmutableState.sol* ( [13-13](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L13-L13), [20-20](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L20-L20), [21-21](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L21-L21) ):

```solidity
13:     uint16 constant BPS = 10000;

20:     uint160 internal SQRT_RATIO_LOWER_X96;

21:     uint160 internal SQRT_RATIO_UPPER_X96;
```

### [N-05] Redundant inheritance specifier

The contracts below already extend the specified contract, so there is no need to list it in the inheritance list again.

There are 2 instances:

- *ILOPool.sol* ( [24-32](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L24-L32) ):

```solidity
/// @audit LiquidityManagement already extends ILOPoolImmutableState
24: contract ILOPool is
25:     ERC721,
26:     IILOPool,
27:     ILOWhitelist,
28:     ILOVest,
29:     Initializable,
30:     Multicall,
31:     ILOPoolImmutableState,
32:     LiquidityManagement
```

- *LiquidityManagement.sol* ( [17-17](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L17-L17) ):

```solidity
/// @audit PeripheryPayments already extends ILOPoolImmutableState
17: abstract contract LiquidityManagement is IUniswapV3MintCallback, ILOPoolImmutableState, PeripheryPayments {
```

### [N-06] Strings should use double quotes rather than single quotes

It is recommended by the [Solidity Style Guide](https://docs.soliditylang.org/en/v0.8.20/style-guide.html#other-recommendations)

<details>
<summary>There are 11 instances (click to show):</summary>

- *ILOPool.sol* ( [49-49](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L49-L49), [54-54](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L54-L54), [58-58](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L58-L58), [179-179](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L179-L179) ):

```solidity
49:     constructor() ERC721('', '') {

54:         return 'KRYSTAL ILOPool V1';

58:         return 'KRYSTAL-ILO-V1';

179:         require(_isApprovedOrOwner(msg.sender, tokenId), 'UA');
```

- *LiquidityManagement.sol* ( [56-56](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L56-L56) ):

```solidity
56:         require(amount0 >= params.amount0Min && amount1 >= params.amount1Min, 'Price slippage check');
```

- *PeripheryPayments.sol* ( [14-14](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L14-L14) ):

```solidity
14:         require(msg.sender == WETH9, 'Not WETH9');
```

- *TransferHelper.sol* ( [21-21](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L21-L21), [35-35](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L35-L35), [49-49](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L49-L49), [58-58](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L58-L58) ):

```solidity
21:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'STF');

35:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'ST');

49:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'SA');

58:         require(success, 'STE');
```

</details>

### [N-07] Use of `override` is unnecessary

[Starting from Solidity 0.8.8](https://docs.soliditylang.org/en/v0.8.20/contracts.html#function-overriding), the override keyword is not required when overriding an interface function, except for the case where the function is defined in multiple bases.

There is 1 instance:

- *VultisigWhitelisted.sol* ( [28-28](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L28-L28) ):

```solidity
28:     function _beforeTokenTransfer(address from, address to, uint256 amount) internal override {
```

### [N-08] Consider providing a ranged getter for array state variables

While the compiler automatically provides a getter for accessing single elements within a public state variable array, it doesn't provide a way to fetch the whole array, or subsets thereof. Consider adding a function to allow the fetching of slices of the array, especially if the contract doesn't already have multicall functionality.

There are 2 instances:

- *ILOManager.sol* ( [26-26](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L26-L26) ):

```solidity
26:     mapping(address => address[]) private _initializedILOPools; // map uniV3Pool => list of initialized ilo pools
```

- *ILOPool.sol* ( [44-44](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L44-L44) ):

```solidity
44:     VestingConfig[] private _vestingConfigs;
```

### [N-09] Assembly blocks should have extensive comments

Assembly blocks take a lot more time to audit than normal Solidity code, and often have gotchas and side-effects that the Solidity versions of the same code do not. Consider adding more comments explaining what is being done in every step of the assembly code, and describe why assembly is being used instead of Solidity.

<details>
<summary>There are 31 instances (click to show):</summary>

- *FullMath.sol* ( [22-26](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L22-L26), [31-33](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L31-L33), [48-50](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L48-L50), [52-55](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L52-L55), [62-64](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L62-L64), [67-69](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L67-L69), [73-75](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L73-L75) ):

```solidity
22:         assembly {
23:             let mm := mulmod(a, b, not(0))
24:             prod0 := mul(a, b)
25:             prod1 := sub(sub(mm, prod0), lt(mm, prod0))
26:         }

31:             assembly {
32:                 result := div(prod0, denominator)
33:             }

48:         assembly {
49:             remainder := mulmod(a, b, denominator)
50:         }

52:         assembly {
53:             prod1 := sub(prod1, gt(remainder, prod0))
54:             prod0 := sub(prod0, remainder)
55:         }

62:         assembly {
63:             denominator := div(denominator, twos)
64:         }

67:         assembly {
68:             prod0 := div(prod0, twos)
69:         }

73:         assembly {
74:             twos := add(div(sub(0, twos), twos), 1)
75:         }
```

- *TickMath.sol* ( [69-73](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L69-L73), [74-78](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L74-L78), [79-83](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L79-L83), [84-88](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L84-L88), [89-93](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L89-L93), [94-98](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L94-L98), [99-103](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L99-L103), [104-107](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L104-L107), [114-119](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L114-L119), [120-125](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L120-L125), [126-131](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L126-L131), [132-137](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L132-L137), [138-143](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L138-L143), [144-149](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L144-L149), [150-155](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L150-L155), [156-161](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L156-L161), [162-167](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L162-L167), [168-173](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L168-L173), [174-179](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L174-L179), [180-185](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L180-L185), [186-191](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L186-L191), [192-196](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L192-L196) ):

```solidity
69:         assembly {
70:             let f := shl(7, gt(r, 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF))
71:             msb := or(msb, f)
72:             r := shr(f, r)
73:         }

74:         assembly {
75:             let f := shl(6, gt(r, 0xFFFFFFFFFFFFFFFF))
76:             msb := or(msb, f)
77:             r := shr(f, r)
78:         }

79:         assembly {
80:             let f := shl(5, gt(r, 0xFFFFFFFF))
81:             msb := or(msb, f)
82:             r := shr(f, r)
83:         }

84:         assembly {
85:             let f := shl(4, gt(r, 0xFFFF))
86:             msb := or(msb, f)
87:             r := shr(f, r)
88:         }

89:         assembly {
90:             let f := shl(3, gt(r, 0xFF))
91:             msb := or(msb, f)
92:             r := shr(f, r)
93:         }

94:         assembly {
95:             let f := shl(2, gt(r, 0xF))
96:             msb := or(msb, f)
97:             r := shr(f, r)
98:         }

99:         assembly {
100:             let f := shl(1, gt(r, 0x3))
101:             msb := or(msb, f)
102:             r := shr(f, r)
103:         }

104:         assembly {
105:             let f := gt(r, 0x1)
106:             msb := or(msb, f)
107:         }

114:         assembly {
115:             r := shr(127, mul(r, r))
116:             let f := shr(128, r)
117:             log_2 := or(log_2, shl(63, f))
118:             r := shr(f, r)
119:         }

120:         assembly {
121:             r := shr(127, mul(r, r))
122:             let f := shr(128, r)
123:             log_2 := or(log_2, shl(62, f))
124:             r := shr(f, r)
125:         }

126:         assembly {
127:             r := shr(127, mul(r, r))
128:             let f := shr(128, r)
129:             log_2 := or(log_2, shl(61, f))
130:             r := shr(f, r)
131:         }

132:         assembly {
133:             r := shr(127, mul(r, r))
134:             let f := shr(128, r)
135:             log_2 := or(log_2, shl(60, f))
136:             r := shr(f, r)
137:         }

138:         assembly {
139:             r := shr(127, mul(r, r))
140:             let f := shr(128, r)
141:             log_2 := or(log_2, shl(59, f))
142:             r := shr(f, r)
143:         }

144:         assembly {
145:             r := shr(127, mul(r, r))
146:             let f := shr(128, r)
147:             log_2 := or(log_2, shl(58, f))
148:             r := shr(f, r)
149:         }

150:         assembly {
151:             r := shr(127, mul(r, r))
152:             let f := shr(128, r)
153:             log_2 := or(log_2, shl(57, f))
154:             r := shr(f, r)
155:         }

156:         assembly {
157:             r := shr(127, mul(r, r))
158:             let f := shr(128, r)
159:             log_2 := or(log_2, shl(56, f))
160:             r := shr(f, r)
161:         }

162:         assembly {
163:             r := shr(127, mul(r, r))
164:             let f := shr(128, r)
165:             log_2 := or(log_2, shl(55, f))
166:             r := shr(f, r)
167:         }

168:         assembly {
169:             r := shr(127, mul(r, r))
170:             let f := shr(128, r)
171:             log_2 := or(log_2, shl(54, f))
172:             r := shr(f, r)
173:         }

174:         assembly {
175:             r := shr(127, mul(r, r))
176:             let f := shr(128, r)
177:             log_2 := or(log_2, shl(53, f))
178:             r := shr(f, r)
179:         }

180:         assembly {
181:             r := shr(127, mul(r, r))
182:             let f := shr(128, r)
183:             log_2 := or(log_2, shl(52, f))
184:             r := shr(f, r)
185:         }

186:         assembly {
187:             r := shr(127, mul(r, r))
188:             let f := shr(128, r)
189:             log_2 := or(log_2, shl(51, f))
190:             r := shr(f, r)
191:         }

192:         assembly {
193:             r := shr(127, mul(r, r))
194:             let f := shr(128, r)
195:             log_2 := or(log_2, shl(50, f))
196:         }
```

- *Multicall.sol* ( [19-21](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/Multicall.sol#L19-L21) ):

```solidity
19:                 assembly {
20:                     result := add(result, 0x04)
21:                 }
```

- *ChainId.sol* ( [9-11](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/ChainId.sol#L9-L11) ):

```solidity
9:         assembly {
10:             chainId := chainid()
11:         }
```

</details>

### [N-10] Consider splitting complex checks into multiple steps

Assign the expression's parts to intermediate local variables, and check against those instead.

There are 4 instances:

- *OracleLibrary.sol* ( [27-27](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L27-L27) ):

```solidity
27:         if (tickCumulativesDelta < 0 && (tickCumulativesDelta % int56(uint56(period)) != 0)) timeWeightedAverageTick--;
```

- *TransferHelper.sol* ( [21-21](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L21-L21), [35-35](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L35-L35), [49-49](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L49-L49) ):

```solidity
21:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'STF');

35:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'ST');

49:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'SA');
```

### [N-11] Complex casting

Consider whether the number of casts is really necessary, or whether using a different type would be more appropriate. Alternatively, add comments to explain in detail why the casts are necessary, and any implicit reasons why the cast does not introduce an overflow.

There is 1 instance:

- *OracleLibrary.sol* ( [24-24](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L24-L24) ):

```solidity
24:         timeWeightedAverageTick = int24(tickCumulativesDelta / int56(uint56(period)));
```

### [N-12] Complex math should be split into multiple steps

Consider splitting long arithmetic calculations into multiple steps to improve the code readability.

There are 4 instances:

- *OracleLibrary.sol* ( [47-49](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L47-L49), [52-54](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L52-L54) ):

```solidity
47:             quoteAmount = baseToken < quoteToken
48:                 ? FullMath.mulDiv(ratioX192, baseAmount, 1 << 192)
49:                 : FullMath.mulDiv(1 << 192, baseAmount, ratioX192);

52:             quoteAmount = baseToken < quoteToken
53:                 ? FullMath.mulDiv(ratioX128, baseAmount, 1 << 128)
54:                 : FullMath.mulDiv(1 << 128, baseAmount, ratioX128);
```

- *TickMath.sol* ( [53-53](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L53-L53) ):

```solidity
53:         sqrtPriceX96 = uint160((ratio >> 32) + (ratio % (1 << 32) == 0 ? 0 : 1));
```

- *ILOPool.sol* ( [424-428](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L424-L428) ):

```solidity
424:                 liquidityUnlocked += uint128(FullMath.mulDiv(
425:                     vest.shares * totalLiquidity, 
426:                     block.timestamp - vest.start, 
427:                     (vest.end - vest.start) * BPS
428:                 ));
```

### [N-13] Consider adding a block/deny-list

Doing so will significantly increase centralization, but will help to prevent hackers from using stolen tokens

There are 3 instances:

- *Whitelist.sol* ( [16](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L16) ):

```solidity
16: contract Whitelist is Ownable {
```

- *ILOPool.sol* ( [24](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L24) ):

```solidity
24: contract ILOPool is
```

- *PeripheryPayments.sol* ( [12](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L12) ):

```solidity
12: abstract contract PeripheryPayments is ILOPoolImmutableState {
```

### [N-14] Convert simple `if`-statements to ternary expressions

Converting some if statements to ternaries (such as `z = (a < b) ? x : y`) can make the code more concise and easier to read.

There are 3 instances:

- *TickMath.sol* ( [109-110](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L109-L110) ):

```solidity
109:         if (msb >= 128) r = ratio >> (msb - 127);
110:         else r = ratio << (127 - msb);
```

- *ILOPool.sol* ( [155-159](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L155-L159), [417-429](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L417-L429) ):

```solidity
155:         if (RAISE_TOKEN == _cachedPoolKey.token0) {
156:             liquidityDelta = LiquidityAmounts.getLiquidityForAmount0(SQRT_RATIO_X96, SQRT_RATIO_UPPER_X96, raiseAmount);
157:         } else {
158:             liquidityDelta = LiquidityAmounts.getLiquidityForAmount1(SQRT_RATIO_LOWER_X96, SQRT_RATIO_X96, raiseAmount);
159:         }

417:             if (vest.end < block.timestamp) {
418:                 liquidityUnlocked += uint128(FullMath.mulDiv(
419:                     vest.shares, 
420:                     totalLiquidity, 
421:                     BPS
422:                 ));
423:             } else {
424:                 liquidityUnlocked += uint128(FullMath.mulDiv(
425:                     vest.shares * totalLiquidity, 
426:                     block.timestamp - vest.start, 
427:                     (vest.end - vest.start) * BPS
428:                 ));
429:             }
```

### [N-15] UPPER_CASE names should be reserved for `constant`/`immutable` variables

If the variable needs to be different based on which class it comes from, a `view`/`pure` _function_ should be used instead (e.g. like [this](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/76eee35971c2541585e05cbf258510dda7b2fbc6/contracts/token/ERC20/extensions/draft-IERC20Permit.sol#L59)).

<details>
<summary>There are 19 instances (click to show):</summary>

- *UniswapV3Oracle.sol* ( [27](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/UniswapV3Oracle.sol#L27) ):

```solidity
27:     constructor(address _pool, address _baseToken, address _WETH) {
```

- *ILOManager.sol* ( [16](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L16), [17](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L17), [19](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L19), [20](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L20), [21](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L21), [22](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L22), [23](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L23) ):

```solidity
16:     address public override UNIV3_FACTORY;

17:     address public override WETH9;

19:     uint64 private DEFAULT_DEADLINE_OFFSET = 7 * 24 * 60 * 60; // 7 days

20:     uint16 public override PLATFORM_FEE;

21:     uint16 public override PERFORMANCE_FEE;

22:     address public override FEE_TAKER;

23:     address public override ILO_POOL_IMPLEMENTATION;
```

- *ILOPoolImmutableState.sol* ( [11](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L11), [14](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L14), [15](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L15), [16](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L16), [17](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L17), [18](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L18), [19](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L19), [20](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L20), [21](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L21) ):

```solidity
11:     address public override WETH9;

14:     address public override MANAGER;

15:     address public override RAISE_TOKEN;

16:     address public override SALE_TOKEN;

17:     int24 public override TICK_LOWER;

18:     int24 public override TICK_UPPER;

19:     uint160 public override SQRT_RATIO_X96;

20:     uint160 internal SQRT_RATIO_LOWER_X96;

21:     uint160 internal SQRT_RATIO_UPPER_X96;
```

- *ILOVest.sol* ( [19](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L19), [37](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L37) ):

```solidity
19:         uint16 BPS = 10000;

37:         uint16 BPS = 10000;
```

</details>

### [N-16] Contract timekeeping will break earlier than the Ethereum network itself will stop working

When a timestamp is downcast from `uint256` to `uint32`, the value will wrap in the year 2106, and the contracts will break. Other downcasts will have different endpoints. Consider whether your contract is intended to live past the size of the type being used.

There is 1 instance:

- *OracleLibrary.sol* ( [75-75](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L75-L75) ):

```solidity
75:         secondsAgo = uint32(block.timestamp) - observationTimestamp;
```

### [N-17] Consider emitting an event at the end of the constructor

This will allow users to easily exactly pinpoint when and by whom a contract was constructed.

There are 5 instances:

- *Vultisig.sol* ( [12-12](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Vultisig.sol#L12-L12) ):

```solidity
12:     constructor() ERC20("Vultisig Token", "VULT") {
```

- *Whitelist.sol* ( [48-48](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L48-L48) ):

```solidity
48:     constructor() {
```

- *UniswapV3Oracle.sol* ( [27-27](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/UniswapV3Oracle.sol#L27-L27) ):

```solidity
27:     constructor(address _pool, address _baseToken, address _WETH) {
```

- *ILOManager.sol* ( [29-29](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L29-L29) ):

```solidity
29:     constructor () {
```

- *ILOPool.sol* ( [49-49](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L49-L49) ):

```solidity
49:     constructor() ERC721('', '') {
```

### [N-18] Events are emitted without the sender information

When an action is triggered based on a user's action, not being able to filter based on who triggered the action makes event processing a lot more cumbersome. Including the `msg.sender` the events of these types of action will make events much more useful to end users, especially when `msg.sender` is not `tx.origin`.

There are 3 instances:

- *ILOManager.sol* ( [64-64](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L64-L64), [197-197](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L197-L197) ):

```solidity
64:         emit ProjectCreated(uniV3PoolAddress, _cachedProject[uniV3PoolAddress]);

197:         emit ProjectLaunch(uniV3PoolAddress);
```

- *ILOPool.sol* ( [175-175](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L175-L175) ):

```solidity
175:         emit Buy(recipient, tokenId, raiseAmount, liquidityDelta);
```

### [N-19] Inconsistent floating version pragma

Source files are using different floating version syntax, this is prone to compilation errors, and is not conducive to the code reliability and maintainability.

<details>
<summary>There are 7 instances (click to show):</summary>

- *Vultisig.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Vultisig.sol#L2) ):

```solidity
2: pragma solidity ^0.8.24;
```

- *FullMath.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L2) ):

```solidity
2: pragma solidity >=0.4.0;
```

- *OracleLibrary.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L2) ):

```solidity
2: pragma solidity >=0.5.0;
```

- *PeripheryPayments.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L2) ):

```solidity
2: pragma solidity >=0.7.5;
```

- *ChainId.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/ChainId.sol#L2) ):

```solidity
2: pragma solidity >=0.7.0;
```

- *LiquidityAmounts.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/LiquidityAmounts.sol#L2) ):

```solidity
2: pragma solidity >=0.5.0;
```

- *TransferHelper.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L2) ):

```solidity
2: pragma solidity >=0.6.0;
```

</details>

### [N-20] Imports could be organized more systematically

The contract's interface should be imported first, followed by each of the interfaces it uses, followed by all other files. The examples below do not follow this layout.

<details>
<summary>There are 12 instances (click to show):</summary>

- *Vultisig.sol* ( [6-6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Vultisig.sol#L6-L6) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
6: import {IApproveAndCallReceiver} from "./interfaces/IApproveAndCallReceiver.sol";
```

- *Whitelist.sol* ( [5-5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L5-L5) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
5: import {IOracle} from "./interfaces/IOracle.sol";
```

- *VultisigWhitelisted.sol* ( [5-5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L5-L5) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
5: import {IWhitelist} from "../interfaces/IWhitelist.sol";
```

- *UniswapV3Oracle.sol* ( [6-6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/UniswapV3Oracle.sol#L6-L6) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
6: import {IOracle} from "../../interfaces/IOracle.sol";
```

- *ILOManager.sol* ( [9-9](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L9-L9) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
9: import '@uniswap/v3-core/contracts/interfaces/IUniswapV3Factory.sol';
```

- *ILOPool.sol* ( [11-11](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L11-L11), [15-15](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L15-L15), [17-17](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L17-L17), [20-20](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L20-L20) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
11: import './interfaces/IILOPool.sol';

/// @audit Out of order with the prev import️ ⬆
15: import './base/ILOVest.sol';

/// @audit Out of order with the prev import️ ⬆
17: import './base/ILOPoolImmutableState.sol';

/// @audit Out of order with the prev import️ ⬆
20: import "./base/ILOWhitelist.sol";
```

- *ILOWhitelist.sol* ( [6-6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L6-L6) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
6: import '../interfaces/IILOWhitelist.sol';
```

- *LiquidityManagement.sol* ( [13-13](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L13-L13) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
13: import './ILOPoolImmutableState.sol';
```

- *PeripheryPayments.sol* ( [10-10](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L10-L10) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
10: import './ILOPoolImmutableState.sol';
```

</details>

### [N-21] Imports should use double quotes rather than single quotes

It is recommended to use double quotes rather than single quotes in imports.

<details>
<summary>There are 42 instances (click to show):</summary>

- *ILOManager.sol* ( [8-8](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L8-L8), [9-9](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L9-L9), [10-10](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L10-L10), [11-11](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L11-L11), [13-13](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L13-L13) ):

```solidity
8: import './base/Initializable.sol';

9: import '@uniswap/v3-core/contracts/interfaces/IUniswapV3Factory.sol';

10: import '@uniswap/v3-core/contracts/interfaces/IUniswapV3Pool.sol';

11: import '@uniswap/v3-core/contracts/libraries/TickMath.sol';

13: import '@openzeppelin/contracts/proxy/Clones.sol';
```

- *ILOPool.sol* ( [5-5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L5-L5), [6-6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L6-L6), [7-7](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L7-L7), [9-9](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L9-L9), [11-11](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L11-L11), [12-12](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L12-L12), [13-13](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L13-L13), [14-14](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L14-L14), [15-15](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L15-L15), [16-16](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L16-L16), [17-17](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L17-L17), [18-18](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L18-L18), [19-19](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L19-L19) ):

```solidity
5: import '@uniswap/v3-core/contracts/interfaces/IUniswapV3Pool.sol';

6: import '@uniswap/v3-core/contracts/libraries/FixedPoint128.sol';

7: import '@uniswap/v3-core/contracts/libraries/FullMath.sol';

9: import '@openzeppelin/contracts/token/ERC721/ERC721.sol';

11: import './interfaces/IILOPool.sol';

12: import './interfaces/IILOManager.sol';

13: import './libraries/PositionKey.sol';

14: import './libraries/SqrtPriceMathPartial.sol';

15: import './base/ILOVest.sol';

16: import './base/LiquidityManagement.sol';

17: import './base/ILOPoolImmutableState.sol';

18: import './base/Initializable.sol';

19: import './base/Multicall.sol';
```

- *ILOPoolImmutableState.sol* ( [4-4](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L4-L4), [5-5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L5-L5) ):

```solidity
4: import '../interfaces/IILOPoolImmutableState.sol';

5: import '../libraries/PoolAddress.sol';
```

- *ILOVest.sol* ( [5-5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L5-L5) ):

```solidity
5: import '../interfaces/IILOVest.sol';
```

- *ILOWhitelist.sol* ( [5-5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L5-L5), [6-6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L6-L6) ):

```solidity
5: import '@openzeppelin/contracts/utils/EnumerableSet.sol';

6: import '../interfaces/IILOWhitelist.sol';
```

- *LiquidityManagement.sol* ( [5-5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L5-L5), [6-6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L6-L6), [7-7](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L7-L7), [9-9](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L9-L9), [10-10](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L10-L10), [12-12](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L12-L12), [13-13](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L13-L13) ):

```solidity
5: import '@uniswap/v3-core/contracts/interfaces/IUniswapV3Factory.sol';

6: import '@uniswap/v3-core/contracts/interfaces/IUniswapV3Pool.sol';

7: import '@uniswap/v3-core/contracts/interfaces/callback/IUniswapV3MintCallback.sol';

9: import '../libraries/PoolAddress.sol';

10: import '../libraries/LiquidityAmounts.sol';

12: import './PeripheryPayments.sol';

13: import './ILOPoolImmutableState.sol';
```

- *Multicall.sol* ( [5-5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/Multicall.sol#L5-L5) ):

```solidity
5: import '../interfaces/IMulticall.sol';
```

- *PeripheryPayments.sol* ( [4-4](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L4-L4), [6-6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L6-L6), [8-8](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L8-L8), [10-10](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L10-L10) ):

```solidity
4: import '@openzeppelin/contracts/token/ERC20/IERC20.sol';

6: import '../interfaces/external/IWETH9.sol';

8: import '../libraries/TransferHelper.sol';

10: import './ILOPoolImmutableState.sol';
```

- *LiquidityAmounts.sol* ( [4-4](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/LiquidityAmounts.sol#L4-L4), [5-5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/LiquidityAmounts.sol#L5-L5), [6-6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/LiquidityAmounts.sol#L6-L6) ):

```solidity
4: import '@uniswap/v3-core/contracts/libraries/FullMath.sol';

5: import '@uniswap/v3-core/contracts/libraries/FixedPoint96.sol';

6: import '@uniswap/v3-core/contracts/libraries/SqrtPriceMath.sol';
```

- *SqrtPriceMathPartial.sol* ( [4-4](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/SqrtPriceMathPartial.sol#L4-L4), [5-5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/SqrtPriceMathPartial.sol#L5-L5), [6-6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/SqrtPriceMathPartial.sol#L6-L6) ):

```solidity
4: import '@uniswap/v3-core/contracts/libraries/FullMath.sol';

5: import '@uniswap/v3-core/contracts/libraries/UnsafeMath.sol';

6: import '@uniswap/v3-core/contracts/libraries/FixedPoint96.sol';
```

- *TransferHelper.sol* ( [4-4](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L4-L4) ):

```solidity
4: import '@openzeppelin/contracts/token/ERC20/IERC20.sol';
```

</details>

### [N-22] @openzeppelin/contracts should be upgraded to a newer version

These contracts import contracts from `@openzeppelin/contracts`, but they are not using [the latest version](https://github.com/OpenZeppelin/openzeppelin-contracts/releases). Using the latest version ensures contract security with fixes for known vulnerabilities, access to the latest feature updates, and enhanced community support and engagement.

The imported version is `^4.9.6`.

<details>
<summary>There are 6 instances (click to show):</summary>

- *ILOManager.sol* ( [12](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L12), [13](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L13) ):

```solidity
12: import "@openzeppelin/contracts/access/Ownable.sol";

13: import '@openzeppelin/contracts/proxy/Clones.sol';
```

- *ILOPool.sol* ( [9](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L9) ):

```solidity
9: import '@openzeppelin/contracts/token/ERC721/ERC721.sol';
```

- *ILOWhitelist.sol* ( [5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L5) ):

```solidity
5: import '@openzeppelin/contracts/utils/EnumerableSet.sol';
```

- *PeripheryPayments.sol* ( [4](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L4) ):

```solidity
4: import '@openzeppelin/contracts/token/ERC20/IERC20.sol';
```

- *TransferHelper.sol* ( [4](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L4) ):

```solidity
4: import '@openzeppelin/contracts/token/ERC20/IERC20.sol';
```

</details>

### [N-23] Consider moving duplicated strings to constants

Moving duplicate strings to constants can improve code maintainability and readability.

<details>
<summary>There are 23 instances (click to show):</summary>

- *ILOManager.sol* ( [52-52](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L52-L52), [119-119](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L119-L119), [190-190](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L190-L190), [202-202](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L202-L202) ):

```solidity
52:         require(_cachedProject[uniV3Pool].admin == msg.sender, "UA");

119:                 require(sqrtPriceX96Existing == sqrtPriceX96, "UV3P");

190:         require(_cachedProject[uniV3PoolAddress].initialPoolPriceX96 == sqrtPriceX96, "UV3P");

202:         require(_cachedProject[uniV3PoolAddress].refundDeadline < block.timestamp, "RFT");
```

- *ILOPool.sol* ( [133-133](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L133-L133), [134-134](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L134-L134), [139-139](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L139-L139), [179-179](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L179-L179), [264-264](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L264-L264), [270-270](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L270-L270), [340-340](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L340-L340), [342-342](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L342-L342), [465-465](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L465-L465) ):

```solidity
133:         require(_isWhitelisted(recipient), "UA");

134:         require(block.timestamp > saleInfo.start && block.timestamp < saleInfo.end, "ST");

139:         require(totalSold() <= saleInfo.maxSaleAmount, "SA");

179:         require(_isApprovedOrOwner(msg.sender, tokenId), 'UA');

264:         require(msg.sender == MANAGER, "UA");

270:         require(!_launchSucceeded, "PL");

340:             require(!_launchSucceeded, "PL");

342:             require(block.timestamp >= _project.refundDeadline, "RFT");

465:         require(msg.sender == _project.admin, "UA");
```

- *ILOVest.sol* ( [22-22](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L22-L22), [24-24](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L24-L24), [27-27](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L27-L27), [32-32](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L32-L32), [36-36](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L36-L36), [43-43](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L43-L43), [46-46](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L46-L46), [50-50](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L50-L50) ):

```solidity
22:                 require (vestingConfigs[i].recipient == address(0), "VR");

24:                 require(vestingConfigs[i].recipient != address(0), "VR");

27:             require(BPS - totalShares >= vestingConfigs[i].shares, "TS");

32:         require(totalShares == BPS, "TS");

36:         require(schedule[0].start >= launchTime, "VT");

43:             require(schedule[i].start >= lastEnd, "VT");

46:             require(BPS - totalShares >= schedule[i].shares, "VS");

50:         require(totalShares == BPS, "VS");
```

- *TransferHelper.sol* ( [35-35](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L35-L35), [49-49](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L49-L49) ):

```solidity
35:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'ST');

49:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'SA');
```

</details>

### [N-24] Functions should be named in mixedCase style

As the [Solidity Style Guide](https://docs.soliditylang.org/en/v0.8.21/style-guide.html#function-names) suggests: functions should be named in mixedCase style.

There are 2 instances:

- *ILOManager.sol* ( [72](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L72), [164](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L164) ):

```solidity
72:     function initILOPool(InitPoolParams calldata params) external override onlyProjectAdmin(params.uniV3Pool) returns (address iloPoolAddress) {

164:     function setILOPoolImplementation(address iloPoolImplementation) external override onlyOwner() {
```

### [N-25] Variable names for `immutable`s should use UPPER_CASE_WITH_UNDERSCORES

For `immutable` variable names, each word should use all capital letters, with underscores separating each word (UPPER_CASE_WITH_UNDERSCORES)

There are 2 instances:

- *UniswapV3Oracle.sol* ( [21-21](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/UniswapV3Oracle.sol#L21-L21), [23-23](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/UniswapV3Oracle.sol#L23-L23) ):

```solidity
21:     address public immutable pool;

23:     address public immutable baseToken;
```

### [N-26] Modifiers should be named in mixedCase style

As the [Solidity Style Guide](https://docs.soliditylang.org/en/latest/style-guide.html#modifier-names) suggests: modifiers should be named in mixedCase style. Use mixedCase. Examples: `onlyBy`, `onlyAfter`, `onlyDuringThePreSale`.

There is 1 instance:

- *ILOPool.sol* ( [263](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L263) ):

```solidity
263:     modifier OnlyManager() {
```

### [N-27] Named imports of parent contracts are missing

Consider adding named imports for all parent contracts.

<details>
<summary>There are 19 instances (click to show):</summary>

- *ILOManager.sol* ( [15-15](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L15-L15) ):

```solidity
/// @audit IILOManager
/// @audit Ownable
/// @audit Initializable
15: contract ILOManager is IILOManager, Ownable, Initializable {
```

- *ILOPool.sol* ( [24-32](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L24-L32) ):

```solidity
/// @audit ERC721
/// @audit IILOPool
/// @audit ILOWhitelist
/// @audit ILOVest
/// @audit Initializable
/// @audit Multicall
/// @audit ILOPoolImmutableState
/// @audit LiquidityManagement
24: contract ILOPool is
25:     ERC721,
26:     IILOPool,
27:     ILOWhitelist,
28:     ILOVest,
29:     Initializable,
30:     Multicall,
31:     ILOPoolImmutableState,
32:     LiquidityManagement
```

- *ILOPoolImmutableState.sol* ( [9-9](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L9-L9) ):

```solidity
/// @audit IILOPoolImmutableState
9: abstract contract ILOPoolImmutableState is IILOPoolImmutableState {
```

- *ILOVest.sol* ( [7-7](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L7-L7) ):

```solidity
/// @audit IILOVest
7: abstract contract ILOVest is IILOVest {
```

- *ILOWhitelist.sol* ( [8-8](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L8-L8) ):

```solidity
/// @audit IILOWhitelist
8: abstract contract ILOWhitelist is IILOWhitelist {
```

- *LiquidityManagement.sol* ( [17-17](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L17-L17) ):

```solidity
/// @audit IUniswapV3MintCallback
/// @audit ILOPoolImmutableState
/// @audit PeripheryPayments
17: abstract contract LiquidityManagement is IUniswapV3MintCallback, ILOPoolImmutableState, PeripheryPayments {
```

- *Multicall.sol* ( [9-9](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/Multicall.sol#L9-L9) ):

```solidity
/// @audit IMulticall
9: abstract contract Multicall is IMulticall {
```

- *PeripheryPayments.sol* ( [12-12](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L12-L12) ):

```solidity
/// @audit ILOPoolImmutableState
12: abstract contract PeripheryPayments is ILOPoolImmutableState {
```

</details>

### [N-28] Constants should be put on the left side of comparisons

Putting constants on the left side of comparison statements is a best practice known as [Yoda conditions](https://en.wikipedia.org/wiki/Yoda_conditions).
Although solidity's static typing system prevents accidental assignments within conditionals, adopting this practice can improve code readability and consistency, especially when working across multiple languages.

<details>
<summary>There are 19 instances (click to show):</summary>

- *Whitelist.sol* ( [216](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L216), [233](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L233) ):

```solidity
/// @audit put `0` on the left
216:             if (_allowedWhitelistIndex == 0 || _whitelistIndex[to] > _allowedWhitelistIndex) {

/// @audit put `0` on the left
233:         if (_whitelistIndex[whitelisted] == 0) {
```

- *VultisigWhitelisted.sol* ( [29](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L29) ):

```solidity
/// @audit put `address(0)` on the left
29:         if (_whitelistContract != address(0)) {
```

- *FullMath.sol* ( [29](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L29) ):

```solidity
/// @audit put `0` on the left
29:         if (prod1 == 0) {
```

- *OracleLibrary.sol* ( [15](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L15) ):

```solidity
/// @audit put `0` on the left
15:         require(period != 0, "BP");
```

- *TickMath.sol* ( [25](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L25), [63](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L63), [109](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L109) ):

```solidity
/// @audit put `uint256(uint24(MAX_TICK))` on the left
25:         require(absTick <= uint256(uint24(MAX_TICK)), "T");

/// @audit put `MIN_SQRT_RATIO` on the left
63:         require(sqrtPriceX96 >= MIN_SQRT_RATIO && sqrtPriceX96 < MAX_SQRT_RATIO, "R");

/// @audit put `128` on the left
109:         if (msb >= 128) r = ratio >> (msb - 127);
```

- *ILOManager.sol* ( [75](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L75), [111](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L111), [116](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L116), [134](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L134) ):

```solidity
/// @audit put `address(0)` on the left
75:             require(_project.uniV3PoolAddress != address(0), "NI");

/// @audit put `address(0)` on the left
111:         if (pool == address(0)) {

/// @audit put `0` on the left
116:             if (sqrtPriceX96Existing == 0) {

/// @audit put `address(0)` on the left
134:         require(_project.uniV3PoolAddress == address(0), "RE");
```

- *ILOPool.sol* ( [386](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L386) ):

```solidity
/// @audit put `0` on the left
386:         if (raiseAmount == 0) return (0, 0);
```

- *ILOVest.sol* ( [21](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L21), [22](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L22), [24](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L24) ):

```solidity
/// @audit put `0` on the left
21:             if (i == 0) {

/// @audit put `address(0)` on the left
22:                 require (vestingConfigs[i].recipient == address(0), "VR");

/// @audit put `address(0)` on the left
24:                 require(vestingConfigs[i].recipient != address(0), "VR");
```

- *TransferHelper.sol* ( [21](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L21), [35](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L35), [49](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L49) ):

```solidity
/// @audit put `0` on the left
21:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'STF');

/// @audit put `0` on the left
35:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'ST');

/// @audit put `0` on the left
49:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'SA');
```

</details>

### [N-29] Large multiples of ten should use scientific notation

Use a scientific notation rather than decimal literals (e.g. `1e6` instead of `1000000`), for better code readability.

There are 4 instances:

- *Vultisig.sol* ( [13-13](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Vultisig.sol#L13-L13) ):

```solidity
/// @audit 100_000_000 -> 1e8
13:         _mint(_msgSender(), 100_000_000 * 1e18);
```

- *ILOPoolImmutableState.sol* ( [13-13](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L13-L13) ):

```solidity
/// @audit 10000 -> 1e4
13:     uint16 constant BPS = 10000;
```

- *ILOVest.sol* ( [19-19](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L19-L19), [37-37](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L37-L37) ):

```solidity
/// @audit 10000 -> 1e4
19:         uint16 BPS = 10000;

/// @audit 10000 -> 1e4
37:         uint16 BPS = 10000;
```

### [N-30] High cyclomatic complexity

Consider breaking down these blocks into more manageable units, by splitting things into utility functions, by reducing nesting, and by using early returns.

<details>
<summary>There is 1 instance (click to show):</summary>

- *TickMath.sol* ( [23-54](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L23-L54) ):

```solidity
23:     function getSqrtRatioAtTick(int24 tick) internal pure returns (uint160 sqrtPriceX96) {
24:         uint256 absTick = tick < 0 ? uint256(-int256(tick)) : uint256(int256(tick));
25:         require(absTick <= uint256(uint24(MAX_TICK)), "T");
26: 
27:         uint256 ratio = absTick & 0x1 != 0 ? 0xfffcb933bd6fad37aa2d162d1a594001 : 0x100000000000000000000000000000000;
28:         if (absTick & 0x2 != 0) ratio = (ratio * 0xfff97272373d413259a46990580e213a) >> 128;
29:         if (absTick & 0x4 != 0) ratio = (ratio * 0xfff2e50f5f656932ef12357cf3c7fdcc) >> 128;
30:         if (absTick & 0x8 != 0) ratio = (ratio * 0xffe5caca7e10e4e61c3624eaa0941cd0) >> 128;
31:         if (absTick & 0x10 != 0) ratio = (ratio * 0xffcb9843d60f6159c9db58835c926644) >> 128;
32:         if (absTick & 0x20 != 0) ratio = (ratio * 0xff973b41fa98c081472e6896dfb254c0) >> 128;
33:         if (absTick & 0x40 != 0) ratio = (ratio * 0xff2ea16466c96a3843ec78b326b52861) >> 128;
34:         if (absTick & 0x80 != 0) ratio = (ratio * 0xfe5dee046a99a2a811c461f1969c3053) >> 128;
35:         if (absTick & 0x100 != 0) ratio = (ratio * 0xfcbe86c7900a88aedcffc83b479aa3a4) >> 128;
36:         if (absTick & 0x200 != 0) ratio = (ratio * 0xf987a7253ac413176f2b074cf7815e54) >> 128;
37:         if (absTick & 0x400 != 0) ratio = (ratio * 0xf3392b0822b70005940c7a398e4b70f3) >> 128;
38:         if (absTick & 0x800 != 0) ratio = (ratio * 0xe7159475a2c29b7443b29c7fa6e889d9) >> 128;
39:         if (absTick & 0x1000 != 0) ratio = (ratio * 0xd097f3bdfd2022b8845ad8f792aa5825) >> 128;
40:         if (absTick & 0x2000 != 0) ratio = (ratio * 0xa9f746462d870fdf8a65dc1f90e061e5) >> 128;
41:         if (absTick & 0x4000 != 0) ratio = (ratio * 0x70d869a156d2a1b890bb3df62baf32f7) >> 128;
42:         if (absTick & 0x8000 != 0) ratio = (ratio * 0x31be135f97d08fd981231505542fcfa6) >> 128;
43:         if (absTick & 0x10000 != 0) ratio = (ratio * 0x9aa508b5b7a84e1c677de54f3e99bc9) >> 128;
44:         if (absTick & 0x20000 != 0) ratio = (ratio * 0x5d6af8dedb81196699c329225ee604) >> 128;
45:         if (absTick & 0x40000 != 0) ratio = (ratio * 0x2216e584f5fa1ea926041bedfe98) >> 128;
46:         if (absTick & 0x80000 != 0) ratio = (ratio * 0x48a170391f7dc42444e8fa2) >> 128;
47: 
48:         if (tick > 0) ratio = type(uint256).max / ratio;
49: 
50:         // this divides by 1<<32 rounding up to go from a Q128.128 to a Q128.96.
51:         // we then downcast because we know the result always fits within 160 bits due to our tick input constraint
52:         // we round up in the division so getTickAtSqrtRatio of the output price is always consistent
53:         sqrtPriceX96 = uint160((ratio >> 32) + (ratio % (1 << 32) == 0 ? 0 : 1));
54:     }
```

</details>

### [N-31] Typos

All typos should be corrected.

There are 5 instances:

- *ILOPool.sol* ( [36](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L36), [163](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L163), [169](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L169), [339](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L339) ):

```solidity
/// @audit lauch
36:     /// @dev when lauch successfully we can not refund anymore

/// @audit recieve
163:         // calculate amount of share liquidity investor recieve by INVESTOR_SHARES config

/// @audit assiging
169:         // update total liquidity locked for vest and assiging vesing schedules

/// @audit lauch
/// @audit sucessfully
339:             // if ilo pool is lauch sucessfully, we can not refund anymore
```

### [N-32] Consider bounding input array length

The functions below take in an unbounded array, and make function calls for entries in the array. While the function will revert if it eventually runs out of gas, it may be a nicer user experience to require() that the length of the array is below some reasonable maximum, so that the user doesn't have to use up a full transaction's gas only to see that the transaction reverts.

There are 6 instances:

- *Whitelist.sol* ( [192](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L192) ):

```solidity
192:         for (uint i = 0; i < whitelisted.length; i++) {
```

- *ILOVest.sol* ( [20](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L20), [41](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L41) ):

```solidity
20:         for (uint256 i = 0; i < vestingConfigs.length; i++) {

41:         for (uint256 i = 0; i < scheduleLength; i++) {
```

- *ILOWhitelist.sol* ( [28](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L28), [35](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L35) ):

```solidity
28:         for (uint256 i = 0; i < users.length; i++) {

35:         for (uint256 i = 0; i < users.length; i++) {
```

- *Multicall.sol* ( [13](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/Multicall.sol#L13) ):

```solidity
13:         for (uint256 i = 0; i < data.length; i++) {
```

### [N-33] Unused function parameters

Function parameters that are defined but not used may be logical errors and need to be checked to see if any logic is missing.
If the parameter is not really needed, it should be removed, otherwise it will repeatedly cause confusion and make code maintenance difficult.
If the parameter cannot be removed directly (for example, if it is an override function), its name should be removed and some comment can be appended.

There is 1 instance:

- *LiquidityManagement.sol* ( [20-24](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L20-L24) ):

```solidity
/// @audit data
20:     function uniswapV3MintCallback(
21:         uint256 amount0Owed,
22:         uint256 amount1Owed,
23:         bytes calldata data
24:     ) external override {
```

### [N-34] Unused named return

Declaring named returns, but not using them, is confusing to the reader. Consider either completely removing them (by declaring just the type without a name), or remove the return statement and do a variable assignment. This would improve the readability of the code, and it may also help reduce regressions during future code refactors.

<details>
<summary>There are 11 instances (click to show):</summary>

- *ILOPool.sol* ( [106-115](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L106-L115), [363-363](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L363-L363) ):

```solidity
/// @audit liquidity
/// @audit raiseAmount
/// @audit feeGrowthInside0LastX128
/// @audit feeGrowthInside1LastX128
106:     function positions(uint256 tokenId)
107:         external
108:         view
109:         override
110:         returns (
111:             uint128 liquidity,
112:             uint256 raiseAmount,
113:             uint256 feeGrowthInside0LastX128,
114:             uint256 feeGrowthInside1LastX128
115:         )

/// @audit refundAmount
363:     function claimProjectRefund(address projectAdmin) external override refundable() OnlyManager() returns(uint256 refundAmount) {
```

- *LiquidityAmounts.sol* ( [24-28](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/LiquidityAmounts.sol#L24-L28), [40-44](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/LiquidityAmounts.sol#L40-L44), [54-58](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/LiquidityAmounts.sol#L54-L58), [74-78](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/LiquidityAmounts.sol#L74-L78) ):

```solidity
/// @audit liquidity
24:     function getLiquidityForAmount0(
25:         uint160 sqrtRatioAX96,
26:         uint160 sqrtRatioBX96,
27:         uint256 amount0
28:     ) internal pure returns (uint128 liquidity) {

/// @audit liquidity
40:     function getLiquidityForAmount1(
41:         uint160 sqrtRatioAX96,
42:         uint160 sqrtRatioBX96,
43:         uint256 amount1
44:     ) internal pure returns (uint128 liquidity) {

/// @audit amount0
54:     function getAmount0ForLiquidity(
55:         uint160 sqrtRatioAX96,
56:         uint160 sqrtRatioBX96,
57:         uint128 liquidity
58:     ) internal pure returns (uint256 amount0) {

/// @audit amount1
74:     function getAmount1ForLiquidity(
75:         uint160 sqrtRatioAX96,
76:         uint160 sqrtRatioBX96,
77:         uint128 liquidity
78:     ) internal pure returns (uint256 amount1) {
```

- *SqrtPriceMathPartial.sol* ( [20-25](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/SqrtPriceMathPartial.sol#L20-L25), [49-54](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/SqrtPriceMathPartial.sol#L49-L54) ):

```solidity
/// @audit amount0
20:     function getAmount0Delta(
21:         uint160 sqrtRatioAX96,
22:         uint160 sqrtRatioBX96,
23:         uint128 liquidity,
24:         bool roundUp
25:     ) internal pure returns (uint256 amount0) {

/// @audit amount1
49:     function getAmount1Delta(
50:         uint160 sqrtRatioAX96,
51:         uint160 sqrtRatioBX96,
52:         uint128 liquidity,
53:         bool roundUp
54:     ) internal pure returns (uint256 amount1) {
```

</details>

### [N-35] Consider using `delete` rather than assigning zero to clear values

The `delete` keyword more closely matches the semantics of what is being done, and draws more attention to the changing of state, which may lead to a more thorough audit of its associated logic.

There is 1 instance:

- *OracleLibrary.sol* ( [19-19](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L19-L19) ):

```solidity
19:         secondAgos[1] = 0;
```

### [N-36] Use the latest Solidity version

Upgrading to the [latest solidity version](https://github.com/ethereum/solc-js/tags) (0.8.19 for L2s) can optimize gas usage, take advantage of new features and improve overall contract efficiency. Where possible, based on compatibility requirements, it is recommended to use newer/latest solidity version to take advantage of the latest optimizations and features.

<details>
<summary>There are 22 instances (click to show):</summary>

- *Vultisig.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Vultisig.sol#L2) ):

```solidity
2: pragma solidity ^0.8.24;
```

- *Whitelist.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L2) ):

```solidity
2: pragma solidity ^0.8.24;
```

- *VultisigWhitelisted.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L2) ):

```solidity
2: pragma solidity ^0.8.24;
```

- *UniswapV3Oracle.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/UniswapV3Oracle.sol#L2) ):

```solidity
2: pragma solidity ^0.8.24;
```

- *FullMath.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L2) ):

```solidity
2: pragma solidity >=0.4.0;
```

- *OracleLibrary.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L2) ):

```solidity
2: pragma solidity >=0.5.0;
```

- *TickMath.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L2) ):

```solidity
2: pragma solidity >=0.5.0;
```

- *ILOManager.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L2) ):

```solidity
2: pragma solidity =0.7.6;
```

- *ILOPool.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L2) ):

```solidity
2: pragma solidity =0.7.6;
```

- *ILOPoolImmutableState.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L2) ):

```solidity
2: pragma solidity =0.7.6;
```

- *ILOVest.sol* ( [3](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L3) ):

```solidity
3: pragma solidity =0.7.6;
```

- *ILOWhitelist.sol* ( [3](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L3) ):

```solidity
3: pragma solidity =0.7.6;
```

- *Initializable.sol* ( [3](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/Initializable.sol#L3) ):

```solidity
3: pragma solidity =0.7.6;
```

- *LiquidityManagement.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L2) ):

```solidity
2: pragma solidity =0.7.6;
```

- *Multicall.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/Multicall.sol#L2) ):

```solidity
2: pragma solidity =0.7.6;
```

- *PeripheryPayments.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/PeripheryPayments.sol#L2) ):

```solidity
2: pragma solidity >=0.7.5;
```

- *ChainId.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/ChainId.sol#L2) ):

```solidity
2: pragma solidity >=0.7.0;
```

- *LiquidityAmounts.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/LiquidityAmounts.sol#L2) ):

```solidity
2: pragma solidity >=0.5.0;
```

- *PoolAddress.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/PoolAddress.sol#L2) ):

```solidity
2: pragma solidity >=0.5.0;
```

- *PositionKey.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/PositionKey.sol#L2) ):

```solidity
2: pragma solidity >=0.5.0;
```

- *SqrtPriceMathPartial.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/SqrtPriceMathPartial.sol#L2) ):

```solidity
2: pragma solidity >=0.5.0;
```

- *TransferHelper.sol* ( [2](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/TransferHelper.sol#L2) ):

```solidity
2: pragma solidity >=0.6.0;
```

</details>

### [N-37] Use a struct to encapsulate multiple function parameters

If a function has too many parameters, replacing them with a struct can improve code readability and maintainability, increase reusability, and reduce the likelihood of errors when passing the parameters.

There are 2 instances:

- *ILOManager.sol* ( [33-41](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L33-L41), [124-132](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L124-L132) ):

```solidity
33:     function initialize(
34:         address initialOwner,
35:         address _feeTaker,
36:         address iloPoolImplementation,
37:         address uniV3Factory,
38:         address weth9,
39:         uint16 platformFee,
40:         uint16 performanceFee
41:     ) external override whenNotInitialized() {

124:     function _cacheProject(
125:         address uniV3PoolAddress,
126:         address saleToken,
127:         address raiseToken,
128:         uint24 fee,
129:         uint160 initialPoolPriceX96,
130:         uint64 launchTime,
131:         uint64 refundDeadline
132:     ) internal {
```

### [N-38] Returning a struct instead of a bunch of variables is better

If a function returns [too many variables](https://docs.soliditylang.org/en/v0.8.21/contracts.html#returning-multiple-values), replacing them with a struct can improve code readability, maintainability and reusability.

<details>
<summary>There are 7 instances (click to show):</summary>

- *ILOPool.sol* ( [106-115](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L106-L115), [126-131](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L126-L131), [184-189](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L184-L189), [382-385](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L382-L385), [438-442](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L438-L442), [448-451](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L448-L451) ):

```solidity
106:     function positions(uint256 tokenId)
107:         external
108:         view
109:         override
110:         returns (
111:             uint128 liquidity,
112:             uint256 raiseAmount,
113:             uint256 feeGrowthInside0LastX128,
114:             uint256 feeGrowthInside1LastX128
115:         )

126:     function buy(uint256 raiseAmount, address recipient)
127:         external override 
128:         returns (
129:             uint256 tokenId,
130:             uint128 liquidityDelta
131:         )

184:     function claim(uint256 tokenId)
185:         external
186:         payable
187:         override
188:         isAuthorizedForToken(tokenId)
189:         returns (uint256 amount0, uint256 amount1)

382:     function _saleAmountNeeded(uint256 raiseAmount) internal view returns (
383:         uint256 saleAmountNeeded,
384:         uint128 liquidity
385:     ) {

438:     function _deductFees(uint256 amount0, uint256 amount1, uint16 feeBPS) internal pure 
439:         returns (
440:             uint256 amount0Left, 
441:             uint256 amount1Left
442:         ) {

448:     function vestingStatus(uint256 tokenId) external view override returns (
449:         uint128 unlockedLiquidity,
450:         uint128 claimedLiquidity
451:     ) {
```

- *LiquidityManagement.sol* ( [41-46](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L41-L46) ):

```solidity
41:     function addLiquidity(AddLiquidityParams memory params)
42:         internal
43:         returns (
44:             uint256 amount0,
45:             uint256 amount1
46:         )
```

</details>

### [N-39] Contract variables should have comments

Consider adding some comments on non-public contract variables to explain what they are supposed to do. This will help for future code reviews.

<details>
<summary>There are 11 instances (click to show):</summary>

- *ILOPool.sol* ( [34-34](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L34-L34), [44-44](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L44-L44), [48-48](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L48-L48) ):

```solidity
34:     SaleInfo saleInfo;

44:     VestingConfig[] private _vestingConfigs;

48:     uint256 totalRaised;
```

- *ILOPoolImmutableState.sol* ( [20-20](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L20-L20), [21-21](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L21-L21), [23-23](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L23-L23), [24-24](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOPoolImmutableState.sol#L24-L24) ):

```solidity
20:     uint160 internal SQRT_RATIO_LOWER_X96;

21:     uint160 internal SQRT_RATIO_UPPER_X96;

23:     PoolAddress.PoolKey internal _cachedPoolKey;

24:     address internal _cachedUniV3PoolAddress;
```

- *ILOVest.sol* ( [8-8](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L8-L8) ):

```solidity
8:     mapping(uint256=>PositionVest) _positionVests;
```

- *ILOWhitelist.sol* ( [9-9](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L9-L9), [40-40](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L40-L40) ):

```solidity
9:     bool private _openToAll;

40:     EnumerableSet.AddressSet private _whitelisted;
```

- *Initializable.sol* ( [6-6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/Initializable.sol#L6-L6) ):

```solidity
6:     bool private _initialized;
```

</details>

### [N-40] Missing event when a state variables is set in constructor

The initial states set in a constructor are important and should be recorded in the event.

There are 2 instances:

- *Whitelist.sol* ( [49](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L49), [50](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L50) ):

```solidity
49:         _maxAddressCap = 3 ether;

50:         _locked = true; // Initially, liquidity will be locked
```

### [N-41] Empty bytes check is missing

Passing empty bytes to a function can cause unexpected behavior, such as certain operations failing, producing incorrect results, or wasting gas. It is recommended to check that all byte parameters are not empty.

There are 2 instances:

- *Vultisig.sol* ( [16-16](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Vultisig.sol#L16-L16) ):

```solidity
/// @audit extraData
16:     function approveAndCall(address spender, uint256 amount, bytes calldata extraData) external returns (bool) {
```

- *LiquidityManagement.sol* ( [20-24](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/LiquidityManagement.sol#L20-L24) ):

```solidity
/// @audit data
20:     function uniswapV3MintCallback(
21:         uint256 amount0Owed,
22:         uint256 amount1Owed,
23:         bytes calldata data
24:     ) external override {
```

### [N-42] Multiple mappings with same keys can be combined into a single struct mapping for readability

Well-organized data structures make code reviews easier, which may lead to fewer bugs. Consider combining related mappings into mappings to structs, so it's clear what data is related.

There are 5 instances:

- *Whitelist.sol* ( [41-41](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L41-L41), [43-43](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L43-L43), [45-45](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L45-L45) ):

```solidity
41:     mapping(address => uint256) private _whitelistIndex;

43:     mapping(address => bool) private _isBlacklisted;

45:     mapping(address => uint256) private _contributed;
```

- *ILOManager.sol* ( [25-25](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L25-L25), [26-26](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L26-L26) ):

```solidity
25:     mapping(address => Project) private _cachedProject; // map uniV3Pool => project (aka projectId => project)

26:     mapping(address => address[]) private _initializedILOPools; // map uniV3Pool => list of initialized ilo pools
```

### [N-43] Missing event for critical changes

Events should be emitted when critical changes are made to the contracts.

<details>
<summary>There are 12 instances (click to show):</summary>

- *Whitelist.sol* ( [136-138](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L136-L138), [142-144](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L142-L144), [148-150](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L148-L150), [154-156](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L154-L156), [160-162](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L160-L162), [166-168](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L166-L168), [173-175](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L173-L175), [179-181](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L179-L181) ):

```solidity
136:     function setLocked(bool newLocked) external onlyOwner {
137:         _locked = newLocked;
138:     }

142:     function setMaxAddressCap(uint256 newCap) external onlyOwner {
143:         _maxAddressCap = newCap;
144:     }

148:     function setVultisig(address newVultisig) external onlyOwner {
149:         _vultisig = newVultisig;
150:     }

154:     function setIsSelfWhitelistDisabled(bool newFlag) external onlyOwner {
155:         _isSelfWhitelistDisabled = newFlag;
156:     }

160:     function setOracle(address newOracle) external onlyOwner {
161:         _oracle = newOracle;
162:     }

166:     function setPool(address newPool) external onlyOwner {
167:         _pool = newPool;
168:     }

173:     function setBlacklisted(address blacklisted, bool flag) external onlyOwner {
174:         _isBlacklisted[blacklisted] = flag;
175:     }

179:     function setAllowedWhitelistIndex(uint256 newIndex) external onlyOwner {
180:         _allowedWhitelistIndex = newIndex;
181:     }
```

- *VultisigWhitelisted.sol* ( [22-24](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L22-L24) ):

```solidity
22:     function setWhitelistContract(address newWhitelistContract) external onlyOwner {
23:         _whitelistContract = newWhitelistContract;
24:     }
```

- *ILOManager.sol* ( [150-152](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L150-L152), [155-157](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L155-L157), [160-162](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L160-L162) ):

```solidity
150:     function setPlatformFee(uint16 _platformFee) external onlyOwner() {
151:         PLATFORM_FEE = _platformFee;
152:     }

155:     function setPerformanceFee(uint16 _performanceFee) external onlyOwner() {
156:         PERFORMANCE_FEE = _performanceFee;
157:     }

160:     function setFeeTaker(address _feeTaker) external override onlyOwner() {
161:         FEE_TAKER = _feeTaker;
162:     }
```

</details>

### [N-44] Non-assembly method available

There are some automated tools that will flag a project as having higher complexity if there is inline-assembly, so it's best to avoid using it where it's not necessary. In addition, most assembly methods can be replaced by non-assembly methods, for example:
- `assembly{ g := gas() }` => `uint256 g = gasleft()`
- `assembly{ id := chainid() }` => `uint256 id = block.chainid`
- `assembly { r := mulmod(a, b, d) }` => `uint256 m = mulmod(x, y, k)`
- `assembly { size := extcodesize() }` => `uint256 size = address(a).code.length`
- etc.

There are 2 instances:

- *FullMath.sol* ( [49-49](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L49-L49) ):

```solidity
49:             remainder := mulmod(a, b, denominator)
```

- *ChainId.sol* ( [10-10](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/libraries/ChainId.sol#L10-L10) ):

```solidity
10:             chainId := chainid()
```

### [N-45] Consider adding emergency-stop functionality

Adding a way to quickly halt protocol functionality in an emergency, rather than having to pause individual contracts one-by-one, will make in-progress hack mitigation faster and much less stressful.

There are 4 instances:

- *Vultisig.sol* ( [11-11](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Vultisig.sol#L11-L11) ):

```solidity
11: contract Vultisig is ERC20, Ownable {
```

- *Whitelist.sol* ( [16-16](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L16-L16) ):

```solidity
16: contract Whitelist is Ownable {
```

- *VultisigWhitelisted.sol* ( [12-12](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L12-L12) ):

```solidity
12: contract VultisigWhitelisted is Vultisig {
```

- *ILOManager.sol* ( [15-15](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L15-L15) ):

```solidity
15: contract ILOManager is IILOManager, Ownable, Initializable {
```

### [N-46] Avoid the use of sensitive terms

Use [alternative variants](https://www.zdnet.com/article/mysql-drops-master-slave-and-blacklist-whitelist-terminology/), e.g. allowlist/denylist instead of whitelist/blacklist.

<details>
<summary>There are 144 instances (click to show):</summary>

- *Whitelist.sol* ( [8](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L8), [10](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L10), [11](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L11), [14](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L14), [16](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L16), [17](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L17), [20](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L20), [21](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L21), [28](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L28), [29](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L29), [36](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L36), [37](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L37), [39](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L39), [40](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L40), [41](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L41), [42](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L42), [43](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L43), [61](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L61), [62](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L62), [63](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L63), [66](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L66), [67](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L67), [69](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L69), [70](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L70), [72](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L72), [86](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L86), [88](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L88), [89](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L89), [92](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L92), [94](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L94), [95](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L95), [98](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L98), [99](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L99), [100](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L100), [113](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L113), [114](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L114), [115](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L115), [118](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L118), [119](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L119), [120](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L120), [152](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L152), [153](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L153), [154](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L154), [155](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L155), [170](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L170), [171](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L171), [173](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L173), [174](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L174), [177](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L177), [178](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L178), [179](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L179), [180](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L180), [183](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L183), [184](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L184), [185](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L185), [186](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L186), [189](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L189), [190](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L190), [191](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L191), [192](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L192), [193](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L193), [197](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L197), [202](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L202), [204](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L204), [212](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L212), [213](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L213), [216](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L216), [217](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L217), [230](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L230), [231](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L231), [232](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L232), [233](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L233), [234](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L234) ):

```solidity
8:  * @title The contract handles whitelist related features

10:  * - Self whitelist by sending ETH to this contract(only when self whitelist is allowed - controlled by _isSelfWhitelistDisabled flag)

11:  * - Ownable: Add whitelisted/blacklisted addresses

14:  * - Vultisig contract `_beforeTokenTransfer` hook will call `checkWhitelist` function and this function will check if buyer is eligible

16: contract Whitelist is Ownable {

17:     error NotWhitelisted();

20:     error SelfWhitelistDisabled();

21:     error Blacklisted();

28:     /// @notice Flag for self whitelist period

29:     bool private _isSelfWhitelistDisabled;

36:     /// @notice Total number of whitelisted addresses

37:     uint256 private _whitelistCount;

39:     uint256 private _allowedWhitelistIndex;

40:     /// @notice Whitelist index for each whitelisted address

41:     mapping(address => uint256) private _whitelistIndex;

42:     /// @notice Mapping for blacklisted addresses

43:     mapping(address => bool) private _isBlacklisted;

61:     /// @notice Self-whitelist using ETH transfer

62:     /// @dev reverts if whitelist is disabled

63:     /// @dev reverts if address is already blacklisted

66:         if (_isSelfWhitelistDisabled) {

67:             revert SelfWhitelistDisabled();

69:         if (_isBlacklisted[_msgSender()]) {

70:             revert Blacklisted();

72:         _addWhitelistedAddress(_msgSender());

86:     /// @notice Returns the whitelisted index. If not whitelisted, then it will be 0

88:     function whitelistIndex(address account) external view returns (uint256) {

89:         return _whitelistIndex[account];

92:     /// @notice Returns if the account is blacklisted or not

94:     function isBlacklisted(address account) external view returns (bool) {

95:         return _isBlacklisted[account];

98:     /// @notice Returns if self-whitelist is allowed or not

99:     function isSelfWhitelistDisabled() external view returns (bool) {

100:         return _isSelfWhitelistDisabled;

113:     /// @notice Returns current whitelisted address count

114:     function whitelistCount() external view returns (uint256) {

115:         return _whitelistCount;

118:     /// @notice Returns current allowed whitelist index

119:     function allowedWhitelistIndex() external view returns (uint256) {

120:         return _allowedWhitelistIndex;

152:     /// @notice Setter for self-whitelist period

153:     /// @param newFlag New flag for self-whitelist period

154:     function setIsSelfWhitelistDisabled(bool newFlag) external onlyOwner {

155:         _isSelfWhitelistDisabled = newFlag;

170:     /// @notice Setter for blacklist

171:     /// @param blacklisted Address to be added

173:     function setBlacklisted(address blacklisted, bool flag) external onlyOwner {

174:         _isBlacklisted[blacklisted] = flag;

177:     /// @notice Setter for allowed whitelist index

178:     /// @param newIndex New index for allowed whitelist

179:     function setAllowedWhitelistIndex(uint256 newIndex) external onlyOwner {

180:         _allowedWhitelistIndex = newIndex;

183:     /// @notice Add whitelisted address

184:     /// @param whitelisted Address to be added

185:     function addWhitelistedAddress(address whitelisted) external onlyOwner {

186:         _addWhitelistedAddress(whitelisted);

189:     /// @notice Add batch whitelists

190:     /// @param whitelisted Array of addresses to be added

191:     function addBatchWhitelist(address[] calldata whitelisted) external onlyOwner {

192:         for (uint i = 0; i < whitelisted.length; i++) {

193:             _addWhitelistedAddress(whitelisted[i]);

197:     /// @notice Check if address to is eligible for whitelist

202:     /// @dev Revert if locked, not whitelisted, blacklisted or already contributed more than capped amount

204:     function checkWhitelist(address from, address to, uint256 amount) external onlyVultisig {

212:             if (_isBlacklisted[to]) {

213:                 revert Blacklisted();

216:             if (_allowedWhitelistIndex == 0 || _whitelistIndex[to] > _allowedWhitelistIndex) {

217:                 revert NotWhitelisted();

230:     /// @notice Internal function used for whitelisting. Only increase whitelist count if address is not whitelisted before

231:     /// @param whitelisted Address to be added

232:     function _addWhitelistedAddress(address whitelisted) private {

233:         if (_whitelistIndex[whitelisted] == 0) {

234:             _whitelistIndex[whitelisted] = ++_whitelistCount;
```

- *VultisigWhitelisted.sol* ( [5](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L5), [8](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L8), [9](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L9), [10](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L10), [12](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L12), [13](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L13), [14](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L14), [16](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L16), [17](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L17), [18](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L18), [21](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L21), [22](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L22), [23](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L23), [27](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L27), [29](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L29), [30](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L30) ):

```solidity
5: import {IWhitelist} from "../interfaces/IWhitelist.sol";

8:  * @title Extended Vultisig token contract with whitelist contract interactions

9:  * @notice During whitelist period, `_beforeTokenTransfer` function will call `checkWhitelist` function of whitelist contract

10:  * @notice If whitelist period is ended, owner will set whitelist contract address back to address(0) and tokens will be transferred freely

12: contract VultisigWhitelisted is Vultisig {

13:     /// @notice whitelist contract address

14:     address private _whitelistContract;

16:     /// @notice Returns current whitelist contract address

17:     function whitelistContract() external view returns (address) {

18:         return _whitelistContract;

21:     /// @notice Ownable function to set new whitelist contract address

22:     function setWhitelistContract(address newWhitelistContract) external onlyOwner {

23:         _whitelistContract = newWhitelistContract;

27:     /// @dev It will call `checkWhitelist` function and if it's succsessful, it will transfer tokens, unless revert

29:         if (_whitelistContract != address(0)) {

30:             IWhitelist(_whitelistContract).checkWhitelist(from, to, amount);
```

- *UniswapV3Oracle.sol* ( [11](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/UniswapV3Oracle.sol#L11) ):

```solidity
11:  * @dev This price will be used in whitelist contract to calculate the ETH tokenIn amount.
```

- *ILOPool.sol* ( [20](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L20), [27](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L27), [133](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L133) ):

```solidity
20: import "./base/ILOWhitelist.sol";

27:     ILOWhitelist,

133:         require(_isWhitelisted(recipient), "UA");
```

- *ILOWhitelist.sol* ( [6](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L6), [8](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L8), [11](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L11), [16](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L16), [21](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L21), [22](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L22), [23](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L23), [26](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L26), [27](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L27), [29](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L29), [33](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L33), [34](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L34), [36](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L36), [40](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L40), [47](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L47), [48](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L48), [49](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L49), [52](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L52), [53](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L53), [54](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L54), [57](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L57), [58](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L58) ):

```solidity
6: import '../interfaces/IILOWhitelist.sol';

8: abstract contract ILOWhitelist is IILOWhitelist {

11:     /// @inheritdoc IILOWhitelist

16:     /// @inheritdoc IILOWhitelist

21:     /// @inheritdoc IILOWhitelist

22:     function isWhitelisted(address user) external override view returns (bool) {

23:         return _isWhitelisted(user);

26:     /// @inheritdoc IILOWhitelist

27:     function batchWhitelist(address[] calldata users) external override onlyProjectAdmin{

29:             _setWhitelist(users[i]);

33:     /// @inheritdoc IILOWhitelist

34:     function batchRemoveWhitelist(address[] calldata users) external override onlyProjectAdmin{

36:             _removeWhitelist(users[i]);

40:     EnumerableSet.AddressSet private _whitelisted;

47:     function _removeWhitelist(address user) internal {

48:         EnumerableSet.remove(_whitelisted, user);

49:         emit SetWhitelist(user, false);

52:     function _setWhitelist(address user) internal {

53:         EnumerableSet.add(_whitelisted, user);

54:         emit SetWhitelist(user, true);

57:     function _isWhitelisted(address user) internal view returns(bool) {

58:         return _openToAll || EnumerableSet.contains(_whitelisted, user);
```

</details>

### [N-47] Missing checks for uint state variable assignments

Consider whether reasonable bounds checks for variables would be useful.

There are 7 instances:

- *Whitelist.sol* ( [143-143](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L143-L143), [180-180](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L180-L180) ):

```solidity
143:         _maxAddressCap = newCap;

180:         _allowedWhitelistIndex = newIndex;
```

- *ILOManager.sol* ( [42-42](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L42-L42), [43-43](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L43-L43), [151-151](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L151-L151), [156-156](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L156-L156), [177-177](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L177-L177) ):

```solidity
42:         PLATFORM_FEE = platformFee;

43:         PERFORMANCE_FEE = performanceFee;

151:         PLATFORM_FEE = _platformFee;

156:         PERFORMANCE_FEE = _performanceFee;

177:         DEFAULT_DEADLINE_OFFSET = defaultDeadlineOffset;
```

### [N-48] Use the Modern Upgradeable Contract Paradigm

Modern smart contract development often employs upgradeable contract structures, utilizing proxy patterns like OpenZeppelin’s Upgradeable Contracts. This paradigm separates logic and state, allowing developers to amend and enhance the contract's functionality without altering its state or the deployed contract address. Transitioning to this approach enhances long-term maintainability.
Resolution: Adopt a well-established proxy pattern for upgradeability, ensuring proper initialization and employing transparent proxies to mitigate potential risks. Embrace comprehensive testing and audit practices, particularly when updating contract logic, to ensure state consistency and security are preserved across upgrades. This ensures your contract remains robust and adaptable to future requirements.

There are 4 instances:

- *Vultisig.sol* ( [11](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Vultisig.sol#L11) ):

```solidity
11: contract Vultisig is ERC20, Ownable {
```

- *Whitelist.sol* ( [16](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L16) ):

```solidity
16: contract Whitelist is Ownable {
```

- *VultisigWhitelisted.sol* ( [12](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L12) ):

```solidity
12: contract VultisigWhitelisted is Vultisig {
```

- *UniswapV3Oracle.sol* ( [14](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/UniswapV3Oracle.sol#L14) ):

```solidity
14: contract UniswapV3Oracle is IOracle {
```

### [N-49] Large or complicated code bases should implement invariant tests

This includes: large code bases, or code with lots of inline-assembly, complicated math, or complicated interactions between multiple contracts.
Invariant fuzzers such as Echidna require the test writer to come up with invariants which should not be violated under any circumstances, and the fuzzer tests various inputs and function calls to ensure that the invariants always hold.
Even code with 100% code coverage can still have bugs due to the order of the operations a user performs, and invariant fuzzers may help significantly.

There are 2 instances:

- Global finding

- Global finding

### [N-50] The default value is manually set when it is declared

In instances where a new variable is defined, there is no need to set it to it's default value.

<details>
<summary>There are 12 instances (click to show):</summary>

- *Whitelist.sol* ( [192-192](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L192-L192) ):

```solidity
192:         for (uint i = 0; i < whitelisted.length; i++) {
```

- *TickMath.sol* ( [67-67](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L67-L67) ):

```solidity
67:         uint256 msb = 0;
```

- *ILOManager.sol* ( [193-193](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L193-L193), [204-204](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L204-L204) ):

```solidity
193:         for (uint256 i = 0; i < initializedPools.length; i++) {

204:         for (uint256 i = 0; i < initializedPools.length; i++) {
```

- *ILOPool.sol* ( [92-92](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L92-L92), [324-324](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L324-L324), [405-405](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L405-L405) ):

```solidity
92:         for (uint256 index = 0; index < params.vestingConfigs.length; index++) {

324:             for (uint256 i = 0; i < projectConfig.schedule.length; i++) {

405:         for (uint256 index = 0; index < vestingSchedule.length; index++) {
```

- *ILOVest.sol* ( [20-20](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L20-L20), [41-41](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOVest.sol#L41-L41) ):

```solidity
20:         for (uint256 i = 0; i < vestingConfigs.length; i++) {

41:         for (uint256 i = 0; i < scheduleLength; i++) {
```

- *ILOWhitelist.sol* ( [28-28](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L28-L28), [35-35](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/ILOWhitelist.sol#L35-L35) ):

```solidity
28:         for (uint256 i = 0; i < users.length; i++) {

35:         for (uint256 i = 0; i < users.length; i++) {
```

- *Multicall.sol* ( [13-13](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/base/Multicall.sol#L13-L13) ):

```solidity
13:         for (uint256 i = 0; i < data.length; i++) {
```

</details>

### [N-51] Contracts should have all `public`/`external` functions exposed by `interface`s

All `external`/`public` functions should extend an `interface`. This is useful to ensure that the whole API is extracted and can be more easily integrated by other projects.

There are 4 instances:

- *Vultisig.sol* ( [11](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Vultisig.sol#L11) ):

```solidity
11: contract Vultisig is ERC20, Ownable {
```

- *Whitelist.sol* ( [16](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/Whitelist.sol#L16) ):

```solidity
16: contract Whitelist is Ownable {
```

- *VultisigWhitelisted.sol* ( [12](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/./contracts/extensions/VultisigWhitelisted.sol#L12) ):

```solidity
12: contract VultisigWhitelisted is Vultisig {
```

- *ILOManager.sol* ( [15](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L15) ):

```solidity
15: contract ILOManager is IILOManager, Ownable, Initializable {
```

### [N-52] Use scopes sparingly

The use of scoped blocks, denoted by `{}` without a preceding control structure like `if`, `for`, etc., allows for the creation of isolated scopes within a function. While this can be useful for managing memory and preventing naming conflicts, it should be used sparingly. Excessive use of these scope blocks can obscure the code's logic flow and make it more difficult to understand, impeding code maintainability. As a best practice, only employ scoped blocks when necessary for memory management or to avoid clear naming conflicts. Otherwise, aim for clarity and simplicity in your code structure for optimal readability and maintainability.

There are 3 instances:

- *ILOManager.sol* ( [74-75](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOManager.sol#L74-L75) ):

```solidity
74:         {
75:             require(_project.uniV3PoolAddress != address(0), "NI");
```

- *ILOPool.sol* ( [198-199](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L198-L199), [277-278](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/./src/ILOPool.sol#L277-L278) ):

```solidity
198:         {
199:             IILOManager.Project memory _project = IILOManager(MANAGER).project(address(pool));

277:         {
278:             uint256 amount0;
```
