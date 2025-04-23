# FeeReceiver

## Overview

#### License: GPL-3.0

```solidity
contract FeeReceiver is AccessControlUpgradeable
```


## Structs info

### RewardData

```solidity
struct RewardData {
	address user;
	uint256 amount;
}
```


## Events info

### EventDistributeFee

```solidity
event EventDistributeFee(uint256 indexed rewardIdx, uint256 totalReward)
```


### EventDistributeFeeList

```solidity
event EventDistributeFeeList(uint256 indexed rewardIdx, FeeReceiver.RewardData[] infoList)
```


## State variables info

### sellFee (0x2b14ca56)

```solidity
uint256 sellFee
```


### rewardIsSend (0x558da71b)

```solidity
mapping(uint256 => bool) rewardIsSend
```


## Modifiers info

### onlyManager

```solidity
modifier onlyManager()
```


## Functions info

### initialize (0x8129fc1c)

```solidity
function initialize() public initializer
```


### triggerSwap (0xf8e5884b)

```solidity
function triggerSwap(uint256 amount) external
```


### distributeRewards (0xf0ab029d)

```solidity
function distributeRewards(
    uint256 rewardIdx_,
    FeeReceiver.RewardData[] calldata infoList_
) external onlyManager
```

手续费分发


Parameters:

| Name       | Type                            | Description                                      |
| :--------- | :------------------------------ | :----------------------------------------------- |
| rewardIdx_ | uint256                         | 奖励唯一id, 同一id不可重复分发                               |
| infoList_  | struct FeeReceiver.RewardData[] | 奖励信息。RewardData( address user; uint256 amount; ) |

### setRewardToken (0x8aee8127)

```solidity
function setRewardToken(address csm_) external onlyManager
```


### transferTokenOut (0xc15ded67)

```solidity
function transferTokenOut(
    address token_,
    address addr_,
    uint256 amount
) external onlyManager
```


### transferTokenOut (0x002e0ae7)

```solidity
function transferTokenOut(
    address payable account_,
    uint256 amount_
) external onlyManager
```

