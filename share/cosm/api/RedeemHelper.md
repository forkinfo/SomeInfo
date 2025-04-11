# RedeemHelper

## Overview

#### License: AGPL-3.0-or-later

```solidity
contract RedeemHelper is OwnableUpgradeable
```


## State variables info

### bonds (0x5f1c17c0)

```solidity
address[] bonds
```


## Functions info

### initialize (0x8129fc1c)

```solidity
function initialize() public initializer
```


### redeemAll (0x502a7ee6)

```solidity
function redeemAll(
    uint256 _uid,
    address _recipient,
    uint256[] memory _ids,
    bool _stake,
    bool _invite
) external
```


### addBondContract (0x0a6d1860)

```solidity
function addBondContract(address _bond) external onlyOwner
```


### removeBondContract (0xb1e59ab7)

```solidity
function removeBondContract(uint256 _index) external onlyOwner
```

