# Community

## Overview

#### License: GPL-3.0

```solidity
contract Community is OwnableUpgradeable
```


## Events info

### EventAddReferrer

```solidity
event EventAddReferrer(address user, address referrer)
```


## Constants info

### ROOT (0x5909c12f)

```solidity
address constant ROOT = address(0x01)
```


## State variables info

### referrer (0x2cf003c2)

```solidity
mapping(address => address) referrer
```


## Functions info

### initialize (0x8129fc1c)

```solidity
function initialize() public initializer
```


### referrerOf (0xd21cacdf)

```solidity
function referrerOf(address account_) external view returns (address)
```


### addReferrer (0xfefa9bb1)

```solidity
function addReferrer(address referrer_) external
```

