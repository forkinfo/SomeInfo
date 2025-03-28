# ReleasePool

## Overview

#### License: AGPL-3.0-or-later

```solidity
contract ReleasePool is IReleasePool, AccessControlUpgradeable
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
	uint256 rewardType;
	address destructionToken;
	uint256 destructionAmt;
	uint256 interestAmt;
	uint256 claimedAmt;
}
```


### RetDestruction

```solidity
struct RetDestruction {
	uint256 releaseLevel;
	uint256 duration;
	uint256 destructionAmt;
}
```


## Events info

### EventBurnToken

```solidity
event EventBurnToken(address indexed user, uint256 amount)
```


### EventStartStakingRelease

```solidity
event EventStartStakingRelease(address indexed user, uint256 amount, address burnToken, uint64 releaseLevel, uint256 index, ReleasePool.Record record)
```


### EventStartContributionRelease

```solidity
event EventStartContributionRelease(address indexed user, uint256 amount, address burnToken, uint64 releaseLevel, uint256 index, ReleasePool.Record record)
```


### EventLevelupRewardRelease

```solidity
event EventLevelupRewardRelease(address indexed user, uint64 now, uint64 releaseLevel, uint256 destructionAmt, ReleasePool.Record record)
```


### EventClaimStakingInterest

```solidity
event EventClaimStakingInterest(address indexed user, uint256 claimableAmt_, ReleasePool.Record record)
```


### EventClaimStakingInterestAll

```solidity
event EventClaimStakingInterestAll(address indexed user, uint256 claimableAmt, ReleasePool.Record[] record)
```


### EventClaimContributionInterest

```solidity
event EventClaimContributionInterest(address indexed user, uint256 claimableAmt_, ReleasePool.Record record)
```


### EventClaimContributionInterestAll

```solidity
event EventClaimContributionInterestAll(address indexed user, uint256 claimableAmt, ReleasePool.Record[] record)
```


### EventReleaseDestruction

```solidity
event EventReleaseDestruction(address indexed user, uint256 rewardType, address burnToken, uint256 destructionAmt)
```


## Constants info

### BOND_DEPOSITORY (0x361beb07)

```solidity
bytes32 constant BOND_DEPOSITORY = keccak256("BOND_DEPOSITORY")
```


### CONTRIBUTION_POOL (0x819ebe52)

```solidity
bytes32 constant CONTRIBUTION_POOL = keccak256("CONTRIBUTION_POOL")
```


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

用户销毁的CSM数量
### recordLength (0x8fdade05)

```solidity
uint256 recordLength
```


### recordList (0x19da83a8)

```solidity
mapping(uint256 => struct ReleasePool.Record) recordList
```


## Modifiers info

### onlyManager

```solidity
modifier onlyManager()
```


### onlyStaking

```solidity
modifier onlyStaking()
```


### onlyContributionPool

```solidity
modifier onlyContributionPool()
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

### burnToken (0x7b47ec1a)

```solidity
function burnToken(uint256 amount_) external
```

用户销毁CSM，降低ContributionFactor


Parameters:

| Name    | Type    | Description |
| :------ | :------ | :---------- |
| amount_ | uint256 | 销毁数量        |

### startStakingRelease (0xeffe1f8e)

```solidity
function startStakingRelease(
    address user_,
    uint256 amount_,
    address burnToken_,
    uint256 burnAmt_,
    uint256 releaseLv_
) external payable onlyStaking
```

Claim interest with release duration.
### startContributionRelease (0x2e91474b)

```solidity
function startContributionRelease(
    address user_,
    uint256 amount_,
    address burnToken_,
    uint256 burnAmt_,
    uint256 releaseLv_
) external payable onlyContributionPool
```

Claim interest with release duration.
### levelup (0x339559f2)

```solidity
function levelup(
    uint256 rewardType_,
    uint256 index_,
    address burnToken_,
    uint256 burnAmt_,
    uint64 releaseLevel_
) external payable
```

为释放中的收益，提高释放等级。


Parameters:

| Name          | Type    | Description       |
| :------------ | :------ | :---------------- |
| rewardType_   | uint256 | 收益类型              |
| index_        | uint256 | 收益序号              |
| burnAmt_      | uint256 | 释放收益所需要销毁的数量      |
| releaseLevel_ | uint64  | 释放等级。1~5对应150天到7天 |

### claimStaking (0x380b5498)

```solidity
function claimStaking(
    address user_,
    uint256 index_,
    address burnToken_
) external
```

领取Staking释放结束的收益


Parameters:

| Name       | Type    | Description |
| :--------- | :------ | :---------- |
| user_      | address | 用户地址        |
| index_     | uint256 | 收益序号        |
| burnToken_ | address | 销毁的token地址  |

### claimStakingAll (0xdc0b0229)

```solidity
function claimStakingAll(address burnToken_) external
```

领取用户staking的，指定burn token的所有释放结束的收益


Parameters:

| Name       | Type    | Description |
| :--------- | :------ | :---------- |
| burnToken_ | address | 销毁的token地址  |

### claimContribution (0x41b214f3)

```solidity
function claimContribution(
    address user_,
    uint256 index_,
    address burnToken_
) external
```

领取Contribution释放结束的收益


Parameters:

| Name       | Type    | Description |
| :--------- | :------ | :---------- |
| user_      | address | 用户地址        |
| index_     | uint256 | 收益序号        |
| burnToken_ | address | 销毁的token地址  |

### claimContributionAll (0xb5042dea)

```solidity
function claimContributionAll(address burnToken_) external
```

领取用户staking的，指定burn token的所有释放结束的收益


Parameters:

| Name       | Type    | Description |
| :--------- | :------ | :---------- |
| burnToken_ | address | 销毁的token地址  |

### getDestructionAmount (0x417bf725)

```solidity
function getDestructionAmount(
    address burnToken_,
    uint256 amount_
) external view returns (ReleasePool.RetDestruction[] memory amountList_)
```

根据指定收益数量，获取所有天数对应的销毁数量


Parameters:

| Name       | Type    | Description |
| :--------- | :------ | :---------- |
| burnToken_ | address | 指定销毁币种      |
| amount_    | uint256 | 收益数量        |


Return values:

| Name        | Type                                | Description               |
| :---------- | :---------------------------------- | :------------------------ |
| amountList_ | struct ReleasePool.RetDestruction[] | 销毁信息的数组，元素为RetDestruction |

### getUserStakingRecords (0x6e0fac88)

```solidity
function getUserStakingRecords(
    address user_,
    address burnToken_
) external view returns (ReleasePool.Record[] memory rList_)
```

获取用户的staking收益释放列表


Parameters:

| Name       | Type    | Description |
| :--------- | :------ | :---------- |
| user_      | address | 用户地址        |
| burnToken_ | address | 指定销毁币种      |


Return values:

| Name   | Type                        | Description      |
| :----- | :-------------------------- | :--------------- |
| rList_ | struct ReleasePool.Record[] | 收益列表信息，元素为Record |

### getUserConstribtionRecords (0x198be4a3)

```solidity
function getUserConstribtionRecords(
    address user_,
    address burnToken_
) external view returns (ReleasePool.Record[] memory rList_)
```

获取用户的Constribution收益释放列表


Parameters:

| Name       | Type    | Description |
| :--------- | :------ | :---------- |
| user_      | address | 用户地址        |
| burnToken_ | address | 指定销毁币种      |


Return values:

| Name   | Type                        | Description      |
| :----- | :-------------------------- | :--------------- |
| rList_ | struct ReleasePool.Record[] | 收益列表信息，元素为Record |

### setInterestDestructionConfig (0xc2a56914)

```solidity
function setInterestDestructionConfig(
    ReleasePool.DestructionConfig[] calldata configList_
) external onlyManager
```


### setContract (0x865e6fd3)

```solidity
function setContract(
    ReleasePool.CONTRACTS _contract,
    address _address
) external onlyManager
```

sets the contract address for LP staking
        @param _contract address