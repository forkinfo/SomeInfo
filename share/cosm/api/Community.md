# Community

## Overview

#### License: GPL-3.0

```solidity
contract Community is Initializable
```


## Events info

### EventAddReferrer

```solidity
event EventAddReferrer(address user, address referrer)
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

