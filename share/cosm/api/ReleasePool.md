# ReleasePool

## Overview

#### License: AGPL-3.0-or-later

```solidity
contract ReleasePool is OwnableUpgradeable
```


## Enums info

### CONTRACTS

```solidity
enum CONTRACTS {
	 STAKING,
	 DESTRUCTION_RECEIVER
}
```


## Structs info

### DestructionConfig

```solidity
struct DestructionConfig {
	uint256 duration;
	uint256 ratio;
}
```


### Record

```solidity
struct Record {
	uint64 startTime;
	uint64 endTime;
	uint64 claimedTime;
	uint64 releaseLevel;
	uint256 idx;
	address destructionToken;
	uint256 destructionAmt;
	uint256 interestAmt;
	uint256 claimedAmt;
}
```


### RetDestruction

```solidity
struct RetDestruction {
	uint256 duration;
	uint256 destructionAmt;
}
```


## Events info

### EventStartRelease

```solidity
event EventStartRelease(address indexed user, uint256 amount, uint64 releaseLevel, uint256 index, ReleasePool.Record record)
```


### EventLevelup

```solidity
event EventLevelup(address indexed user, uint64 now, uint64 releaseLevel, uint256 destructionAmt, ReleasePool.Record record)
```


### EventClaimInterest

```solidity
event EventClaimInterest(address indexed user, uint256 index, uint256 claimableAmt_, ReleasePool.Record record)
```


### EventClaimInterestAll

```solidity
event EventClaimInterestAll(address indexed user, uint256 claimableAmt, ReleasePool.Record[] record)
```


## Constants info

### PRECISION (0xaaf5eb68)

```solidity
uint256 constant PRECISION = 100e3
```


### STAKE_BASE_MULTI (0x72252782)

```solidity
uint256 constant STAKE_BASE_MULTI = 5
```


## State variables info

### MAX_STAKE_PRINCIPAL (0x9e1d50c3)

```solidity
uint256 immutable MAX_STAKE_PRINCIPAL
```


### UNISWAPV2ROUTER (0xa8b62f7b)

```solidity
address immutable UNISWAPV2ROUTER
```


### WBNB (0x8dd95002)

```solidity
address immutable WBNB
```


### CSM (0x8de2b272)

```solidity
address immutable CSM
```


### USDT (0xc54e44eb)

```solidity
address immutable USDT
```


### destructionReceiver (0xc8f5351b)

```solidity
address destructionReceiver
```


### stakingContract (0xee99205c)

```solidity
address stakingContract
```


### interestDestructionConfig (0x5fca0e83)

```solidity
struct ReleasePool.DestructionConfig[] interestDestructionConfig
```


### userClaimedReward (0xac682488)

```solidity
mapping(address => uint256) userClaimedReward
```


### userBurned (0x562904e9)

```solidity
mapping(address => uint256) userBurned
```


### recordLength (0x8fdade05)

```solidity
uint256 recordLength
```


### recordList (0x19da83a8)

```solidity
mapping(uint256 => struct ReleasePool.Record) recordList
```


## Modifiers info

### onlyStaking

```solidity
modifier onlyStaking()
```


## Functions info

### constructor

```solidity
constructor(
    address _WBNB,
    address _CSM,
    address _USDT,
    address _uniswapv2Router
)
```


### initialize (0xc4d66de8)

```solidity
function initialize(address _destructionReceiver) public initializer
```


### getInfo (0xffdd5cf1)

```solidity
function getInfo(
    address user_
) external view returns (uint256 stakeBase_, uint256 contributorFactor_)
```

获取社区信息


Parameters:

| Name  | Type    | Description |
| :---- | :------ | :---------- |
| user_ | address | 用户地址        |


Return values:

| Name               | Type    | Description |
| :----------------- | :------ | :---------- |
| stakeBase_         | uint256 | 质押基数        |
| contributorFactor_ | uint256 | 能量因子        |

### startRelease (0xb9f6d694)

```solidity
function startRelease(
    address user_,
    uint256 amount_,
    uint256 burnAmt_,
    uint64 releaseLevel_
) external payable onlyStaking
```

Claim interest with release duration.
### levelup (0x31490e2f)

```solidity
function levelup(
    uint256 index_,
    uint256 burnAmt_,
    uint64 releaseLevel_
) external payable
```

为释放中的收益，提高释放等级。


Parameters:

| Name          | Type    | Description       |
| :------------ | :------ | :---------------- |
| index_        | uint256 | 收益序号              |
| burnAmt_      | uint256 | 释放收益所需要销毁的数量      |
| releaseLevel_ | uint64  | 释放等级。1~5对应150天到7天 |

### claim (0xaad3ec96)

```solidity
function claim(address user_, uint256 index_) external
```

领取释放结束的收益


Parameters:

| Name   | Type    | Description |
| :----- | :------ | :---------- |
| user_  | address | 用户地址        |
| index_ | uint256 | 收益序号        |

### claimAll (0xd1058e59)

```solidity
function claimAll() external
```

领取所有释放结束的收益， TODO：这个待定
### getDestructionAmount (0xea474720)

```solidity
function getDestructionAmount(
    uint256 amount_
) external view returns (ReleasePool.RetDestruction[] memory amountList_)
```

根据指定收益数量，获取所有天数对应的销毁数量


Parameters:

| Name    | Type    | Description |
| :------ | :------ | :---------- |
| amount_ | uint256 | 收益数量        |


Return values:

| Name        | Type                                | Description               |
| :---------- | :---------------------------------- | :------------------------ |
| amountList_ | struct ReleasePool.RetDestruction[] | 销毁信息的数组，元素为RetDestruction |

### getUserRecords (0x51096b02)

```solidity
function getUserRecords(
    address user_
) external view returns (ReleasePool.Record[] memory rList_)
```

获取用户的收益释放列表


Parameters:

| Name  | Type    | Description |
| :---- | :------ | :---------- |
| user_ | address | 用户地址        |


Return values:

| Name   | Type                        | Description      |
| :----- | :-------------------------- | :--------------- |
| rList_ | struct ReleasePool.Record[] | 收益列表信息，元素为Record |

### setInterestDestructionConfig (0xc2a56914)

```solidity
function setInterestDestructionConfig(
    ReleasePool.DestructionConfig[] calldata configList_
) external onlyOwner
```


### setContract (0x865e6fd3)

```solidity
function setContract(
    ReleasePool.CONTRACTS _contract,
    address _address
) external onlyOwner
```

sets the contract address for LP staking
        @param _contract address
