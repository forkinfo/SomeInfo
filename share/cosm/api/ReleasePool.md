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
event EventBurnToken(uint256 indexed uid, address indexed user, uint256 amount, uint256 totalAmount, uint256 burnAmt, uint256 lastAmt)
```


### EventStartStakingRelease

```solidity
event EventStartStakingRelease(uint256 indexed uid, address indexed user, uint256 amount, address burnToken, uint64 releaseLevel, uint256 index, ReleasePool.Record record)
```


### EventStartContributionRelease

```solidity
event EventStartContributionRelease(uint256 indexed uid, address indexed user, uint256 amount, address burnToken, uint64 releaseLevel, uint256 index, ReleasePool.Record record)
```


### EventLevelupRewardRelease

```solidity
event EventLevelupRewardRelease(uint256 indexed uid, address indexed user, uint64 now, uint64 releaseLevel, uint256 destructionAmt, ReleasePool.Record record)
```


### EventClaimStakingInterest

```solidity
event EventClaimStakingInterest(uint256 indexed uid, address indexed user, uint256 claimableAmt_, ReleasePool.Record record)
```


### EventClaimStakingInterestAll

```solidity
event EventClaimStakingInterestAll(uint256 indexed uid, address indexed user, uint256 claimableAmt, ReleasePool.Record[] record)
```


### EventClaimContributionInterest

```solidity
event EventClaimContributionInterest(uint256 indexed uid, address indexed user, uint256 claimableAmt_, ReleasePool.Record record)
```


### EventClaimContributionInterestAll

```solidity
event EventClaimContributionInterestAll(uint256 indexed uid, address indexed user, uint256 claimableAmt, ReleasePool.Record[] record)
```


### EventReleaseDestruction

```solidity
event EventReleaseDestruction(uint256 indexed uid, address indexed user, uint256 rewardType, address burnToken, uint256 destructionAmt)
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
uint256 constant STAKE_BASE_MULTI = 4
```


## State variables info

### MAX_STAKE_BASE (0x254538dc)

```solidity
uint256 immutable MAX_STAKE_BASE
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


### userReleasedContributionReward (0xd1192093)

```solidity
mapping(uint256 => mapping(address => uint256)) userReleasedContributionReward
```


### userBurned (0xf5de9560)

```solidity
mapping(uint256 => mapping(address => uint256)) userBurned
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


### totalBurned (0xd89135cd)

```solidity
uint256 totalBurned
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


### getInfo (0x00d53978)

```solidity
function getInfo(
    uint256 uid_,
    address user_
)
    external
    view
    returns (
        uint256 stakeBase_,
        uint256 contributorFactor_,
        uint256 destructionFactor_
    )
```

获取社区信息


Parameters:

| Name  | Type    | Description |
| :---- | :------ | :---------- |
| uid_  | uint256 | 项目id        |
| user_ | address | 用户地址        |


Return values:

| Name               | Type    | Description |
| :----------------- | :------ | :---------- |
| stakeBase_         | uint256 | 质押基数        |
| contributorFactor_ | uint256 | 能量因子        |
| destructionFactor_ | uint256 | 销毁CSM的数量x4  |

### burnToken (0x8225b247)

```solidity
function burnToken(uint256 uid_, uint256 amount_) external
```

用户销毁CSM，降低ContributionFactor


Parameters:

| Name    | Type    | Description |
| :------ | :------ | :---------- |
| uid_    | uint256 | 项目id        |
| amount_ | uint256 | 销毁数量        |

### startStakingRelease (0x752dddb8)

```solidity
function startStakingRelease(
    uint256 uid_,
    address user_,
    uint256 amount_,
    address burnToken_,
    uint256 burnAmt_,
    uint256 releaseLv_
) external payable onlyStaking
```

Claim interest with release duration.
### startContributionRelease (0xbb369d67)

```solidity
function startContributionRelease(
    uint256 uid_,
    address user_,
    uint256 amount_,
    address burnToken_,
    uint256 burnAmt_,
    uint256 releaseLv_
) external payable onlyContributionPool
```

Claim interest with release duration.
### levelup (0x189ef155)

```solidity
function levelup(
    uint256 uid_,
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
| uid_          | uint256 | 项目id              |
| rewardType_   | uint256 | 收益类型              |
| index_        | uint256 | 收益序号              |
| burnAmt_      | uint256 | 释放收益所需要销毁的数量      |
| releaseLevel_ | uint64  | 释放等级。1~5对应150天到7天 |

### claimStaking (0x543d76cc)

```solidity
function claimStaking(
    uint256 uid_,
    address user_,
    uint256 index_,
    address burnToken_
) external
```

领取Staking释放结束的收益


Parameters:

| Name       | Type    | Description |
| :--------- | :------ | :---------- |
| uid_       | uint256 | 项目id        |
| user_      | address | 用户地址        |
| index_     | uint256 | 收益序号        |
| burnToken_ | address | 销毁的token地址  |

### claimStakingAll (0x8a88bc88)

```solidity
function claimStakingAll(uint256 uid_, address burnToken_) external
```

领取用户staking的，指定burn token的所有释放结束的收益


Parameters:

| Name       | Type    | Description |
| :--------- | :------ | :---------- |
| uid_       | uint256 | 项目id        |
| burnToken_ | address | 销毁的token地址  |

### claimContribution (0x91075d37)

```solidity
function claimContribution(
    uint256 uid_,
    address user_,
    uint256 index_,
    address burnToken_
) external
```

领取Contribution释放结束的收益


Parameters:

| Name       | Type    | Description |
| :--------- | :------ | :---------- |
| uid_       | uint256 | 项目id        |
| user_      | address | 用户地址        |
| index_     | uint256 | 收益序号        |
| burnToken_ | address | 销毁的token地址  |

### claimContributionAll (0xfc88200f)

```solidity
function claimContributionAll(uint256 uid_, address burnToken_) external
```

领取用户staking的，指定burn token的所有释放结束的收益


Parameters:

| Name       | Type    | Description |
| :--------- | :------ | :---------- |
| uid_       | uint256 | 项目id        |
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

### getDestructionAmountByLevel (0x921a36fd)

```solidity
function getDestructionAmountByLevel(
    address burnToken_,
    uint256 amount_,
    uint256 releaseLevel_
) external view returns (uint256)
```

根据指定收益数量和释放等级，获取对应的销毁数量
### getUserStakingRecords (0xaece3585)

```solidity
function getUserStakingRecords(
    uint256 uid_,
    address user_,
    address burnToken_
)
    external
    view
    returns (
        ReleasePool.Record[] memory rList_,
        uint256 totalClaimabledReward_
    )
```

获取用户的staking收益释放列表


Parameters:

| Name       | Type    | Description |
| :--------- | :------ | :---------- |
| uid_       | uint256 | 项目id        |
| user_      | address | 用户地址        |
| burnToken_ | address | 指定销毁币种      |


Return values:

| Name                   | Type                        | Description       |
| :--------------------- | :-------------------------- | :---------------- |
| rList_                 | struct ReleasePool.Record[] | 收益列表信息，元素为Record  |
| totalClaimabledReward_ | uint256                     | 总待领取奖励数量          |

### getUserContributionRecords (0x821c6007)

```solidity
function getUserContributionRecords(
    uint256 uid_,
    address user_,
    address burnToken_
)
    external
    view
    returns (
        ReleasePool.Record[] memory rList_,
        uint256 totalClaimabledReward_
    )
```

获取用户的Contribution收益释放列表


Parameters:

| Name       | Type    | Description |
| :--------- | :------ | :---------- |
| uid_       | uint256 | 项目id        |
| user_      | address | 用户地址        |
| burnToken_ | address | 指定销毁币种      |


Return values:

| Name                   | Type                        | Description       |
| :--------------------- | :-------------------------- | :---------------- |
| rList_                 | struct ReleasePool.Record[] | 收益列表信息，元素为Record  |
| totalClaimabledReward_ | uint256                     | 总待领取奖励数量          |

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