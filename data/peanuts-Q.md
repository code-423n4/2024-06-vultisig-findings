### [L-01] If the investor is a smart contract address, it cannot interact with the code if it has no onERC721Received callback.

When an investor calls `buy()` and deposits some `RAISE_TOKEN`, an NFT will be minted to the recipient. If the recipient happens to be a smart contract, the recipient will not be able to get the NFT token without `onERC721Received`. This means that their `RAISE_TOKEN` will be effectively locked in the contract.

```
  if (balanceOf(recipient) == 0) {
            _mint(recipient, (tokenId = _nextId++));
            _positionVests[tokenId].schedule = _vestingConfigs[0].schedule;
```

Consider using safeMint instead of mint(), or check if the invesotr is a smart contract recipient.

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L144

### [L-02] There can be a point in time where the sale ends but saleInfo.softCap is not reached, resulting in pool being unable to launch

In the `ILOPool.launch()` function, there is a check that `totalRaised >= saleInfo.softCap`. This check is intended so that there is a decent amount of liquidity in the pool.

```
  function launch() external override OnlyManager() {
        require(!_launchSucceeded, "PL");
        // when refund triggered, we can not launch pool anymore
        require(!_refundTriggered, "IRF");
        // make sure that soft cap requirement match
>       require(totalRaised >= saleInfo.softCap, "SC");
```

If the sale ends and `saleInfo.softCap` is not reached, the only thing that can happen is to extend the refund deadline and allow every investor to get refunds, which is quite troublesome if the difference between `totalRaised` and `softCap` is extremely small.

A possible solution will be to have the capability to extend the saleTime so that saleInfo.softCap can be reached, or allow the admin to increase the `totalRaised`.

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L274

### [L-03] 1 person calling refund will render the whole pool unable to launch

When the ILO is still in the pre-launch refund window, any investors can call refund to get back their RAISE_TOKEN. The moment someone calls `claimRefund`, the whole pool cannot be launched because `_refundTriggered = true`.

Consider changing the implementation of refund such that one investor cannot prevent the whole pool from launching.

```
  modifier refundable() {
        if (!_refundTriggered) {
            // if ilo pool is lauch sucessfully, we can not refund anymore
            require(!_launchSucceeded, "PL");
            IILOManager.Project memory _project = IILOManager(MANAGER).project(_cachedUniV3PoolAddress);
            require(block.timestamp >= _project.refundDeadline, "RFT");

>           _refundTriggered = true;
        }
```

### [L-04] The way the schedule is stored for recipients can be simplified

The current way to store the schedule is as such:

```
            LinearVest[] storage schedule = _positionVests[tokenId].schedule;
            for (uint256 i = 0; i < projectConfig.schedule.length; i++) {
                schedule.push(projectConfig.schedule[i]);
            }
```

Instead of creating the loop, simply point the schedule to the index of the projectConfig


```
            LinearVest[] storage schedule = _positionVests[tokenId].schedule;
            _positionVests[tokenId].schedule = projectConfig.schedule;
```

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L317-L326

### [L-05] There is no need for payable when calling claim() to prevent loss of native tokens

ILOPool.claim() has a payable modifier, but does not interact with native tokens.

```
 function claim(uint256 tokenId)
        external
        payable
        override
        isAuthorizedForToken(tokenId)
        returns (uint256 amount0, uint256 amount1)
    {
```

If a user calls claim() and attaches native inside, it will be stuck in contract. Suggest removing the payable modifier

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L186

### [L-06] Fees are not checked to be below BPS

Ensure that the platformFee and performance fee is below a certain threshold (eg 10%). 

```
    function setPlatformFee(uint16 _platformFee) external onlyOwner() {
        PLATFORM_FEE = _platformFee;
    }

    /// @notice set platform fee for decrease liquidity. Platform fee is imutable among all project's pools
    function setPerformanceFee(uint16 _performanceFee) external onlyOwner() {
        PERFORMANCE_FEE = _performanceFee;
    }
```

Add a check like this:

```
require(_platformFee < 1000, "Fee is below 10%");
```

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L151

### [L-07] Have two-step ownership transfers for important functions and check for zero address()

When transferring access control, it is best practice to check for address zero and implement two-step transfers.

```
    function transferAdminProject(address admin, address uniV3Pool) external override onlyProjectAdmin(uniV3Pool) {
        Project storage _project = _cachedProject[uniV3Pool];
        _project.admin = admin;
        emit ProjectAdminChanged(uniV3Pool, msg.sender, admin);
    }
```

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L169