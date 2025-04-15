# Community

## Overview

#### License: GPL-3.0

```solidity
contract Community is OwnableUpgradeable
```


## Events info

### EventAddReferrer

```solidity
event EventAddReferrer(uint256 indexed uid, address indexed user, address referrer)
```


## Constants info

### ROOT (0x5909c12f)

```solidity
address constant ROOT = address(0x01)
```


## State variables info

### referrer (0x230dc74c)

```solidity
mapping(uint256 => mapping(address => address)) referrer
```


## Functions info

### initialize (0x8129fc1c)

```solidity
function initialize() public initializer
```


### referrerOf (0xabdc887b)

```solidity
function referrerOf(
    uint256 uid_,
    address account_
) external view returns (address)
```


### getReferrers (0x607f2666)

```solidity
function getReferrers(
    uint256 uid_,
    address[] calldata accountList_
) external view returns (address[] memory referrerList_)
```


### addReferrer (0x63bc0557)

```solidity
function addReferrer(uint256 uid_, address referrer_) external
```


### updateReferrer (0x7b12319f)

```solidity
function updateReferrer(
    uint256 uid_,
    address[2][] calldata referers_
) external onlyOwner
```

