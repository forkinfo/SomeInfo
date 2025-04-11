# Distributor

## Overview

#### License: AGPL-3.0-or-later

```solidity
contract Distributor is OwnableUpgradeable
```


## Structs info

### Info

```solidity
struct Info {
	uint256 rate;
	address recipient;
}
```


### Adjust

```solidity
struct Adjust {
	bool add;
	uint256 rate;
	uint256 target;
}
```


## State variables info

### sCSM (0x63032870)

```solidity
address immutable sCSM
```


### treasury (0x61d027b3)

```solidity
address immutable treasury
```


### epochTimeLength (0x4a25447a)

```solidity
uint256 immutable epochTimeLength
```


### nextEpochBlockTime (0xabaffe9b)

```solidity
uint256 nextEpochBlockTime
```


### adjustments (0xbc3b2b12)

```solidity
mapping(uint256 => struct Distributor.Adjust) adjustments
```


### info (0x2e340599)

```solidity
struct Distributor.Info[] info
```


## Functions info

### constructor

```solidity
constructor(address _treasury, address _scsm, uint256 _epochTimeLength)
```


### initialize (0xfe4b84df)

```solidity
function initialize(uint256 _nextEpochBlockTime) public initializer
```


### getRecipientRate (0x23aacbaa)

```solidity
function getRecipientRate(address recipient) external view returns (uint256)
```


### distribute (0xe4fc6b6d)

```solidity
function distribute() external returns (bool)
```

send epoch reward to staking contract
### nextRewardAt (0xc9fa8b2a)

```solidity
function nextRewardAt(uint256 _rate) public view returns (uint256)
```

view function for next reward at given rate
        @param _rate uint
        @return uint
### nextRewardFor (0x36d33f44)

```solidity
function nextRewardFor(address _recipient) public view returns (uint256 reward)
```

view function for next reward for specified address
        @param _recipient address
        @return reward
### addRecipient (0xf7982243)

```solidity
function addRecipient(
    address _recipient,
    uint256 _rewardRate
) external onlyOwner
```

adds recipient for distributions
        @param _recipient address
        @param _rewardRate uint
### removeRecipient (0xfe3fbbad)

```solidity
function removeRecipient(uint256 _index, address _recipient) external onlyOwner
```

removes recipient for distributions
        @param _index uint
        @param _recipient address
### setAdjustment (0x5db854b0)

```solidity
function setAdjustment(
    uint256 _index,
    bool _add,
    uint256 _rate,
    uint256 _target
) external onlyOwner
```

set adjustment info for a collector's reward rate
        @param _index uint
        @param _add bool
        @param _rate uint
        @param _target uint