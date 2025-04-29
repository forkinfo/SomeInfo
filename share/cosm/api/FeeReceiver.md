# FeeReceiver

## Overview

#### License: GPL-3.0

```solidity
contract FeeReceiver is AccessControlUpgradeable
```


## Structs info

### DistributedReward

```solidity
struct DistributedReward {
	uint256 distributedIdx;
	uint256 distributedTime;
	uint256 distributedAmount;
	uint256 recycleAmount;
}
```


## Events info

### EventDistributeRewards

```solidity
event EventDistributeRewards(uint256 rewardIdx, uint256 totalReward)
```


### EventDistributeRewardsWithPartners

```solidity
event EventDistributeRewardsWithPartners(uint256 rewardIdx, uint256 percent, uint256 rewardV, address[] partners)
```


### EventTriggerSwap

```solidity
event EventTriggerSwap(uint256 csmAmount, uint256 usdtAmount)
```


## Constants info

### PRECISION (0xaaf5eb68)

```solidity
uint256 constant PRECISION = 100
```


### RISING_PARTNER (0x95ada6c5)

```solidity
uint256 constant RISING_PARTNER = 6
```

四种Partner瓜分5%手续费的一半，就是USDT余额的50%
### VANGUARD_PARTNER (0xdc0be886)

```solidity
uint256 constant VANGUARD_PARTNER = 10
```


### CORE_PARTNER (0x467ba88e)

```solidity
uint256 constant CORE_PARTNER = 14
```


### ALPHA_PARTNER (0xa72aba9f)

```solidity
uint256 constant ALPHA_PARTNER = 20
```


## State variables info

### UNISWAPV2ROUTER (0xa8b62f7b)

```solidity
contract IUniswapV2Router immutable UNISWAPV2ROUTER
```


### USDT (0xc54e44eb)

```solidity
address immutable USDT
```


### sellFee (0x2b14ca56)

```solidity
uint256 sellFee
```


### rewardIsSend (0x558da71b)

```solidity
mapping(uint256 => bool) rewardIsSend
```


### receiverWallet (0x677342ab)

```solidity
address receiverWallet
```


### lastDistributedReward (0xac3b9d37)

```solidity
struct FeeReceiver.DistributedReward lastDistributedReward
```


## Modifiers info

### onlyManager

```solidity
modifier onlyManager()
```


## Functions info

### constructor

```solidity
constructor(address USDT_, address uniswapV2Router_)
```


### initialize (0xc4d66de8)

```solidity
function initialize(address receiverWallet_) public initializer
```


### triggerSwap (0xf8e5884b)

```solidity
function triggerSwap(uint256 amount_) external
```


### swapTokenBalance (0xdeb629de)

```solidity
function swapTokenBalance(address token_) external onlyManager
```


### distributeRewards (0x83cf2562)

```solidity
function distributeRewards(
    uint256 rewardIdx_,
    address[] calldata risingPartners_,
    address[] calldata vanguardPartners_,
    address[] calldata corePartners_,
    address[] calldata alphaPartners_
) external onlyManager
```

手续费分发
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


### setReceiverWallet (0x22912cb2)

```solidity
function setReceiverWallet(address receiverWallet_) external onlyManager
```

