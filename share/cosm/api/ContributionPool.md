# ContributionPool

## Overview

#### License: AGPL-3.0-or-later

```solidity
contract ContributionPool is AccessControlUpgradeable
```


## Structs info

### RootParams

```solidity
struct RootParams {
	uint256 rewardType;
	bytes32 merkleRoot;
	uint256 totalReward;
}
```


## Events info

### EventUpdateMerkleRoot

```solidity
event EventUpdateMerkleRoot(uint256 uid, uint256 epochIndex, uint256 maxReward, bytes32 merkleRoot, uint256 newTotalReward, uint256 newRewardOffset, uint256 prevRewardOffset)
```

事件-默克尔根的更新


Parameters:

| Name             | Type    | Description                |
| :--------------- | :------ | :------------------------- |
| epochIndex       | uint256 | epoch序号                    |
| maxReward        | uint256 | 本次更新，理论上的总奖励上限             |
| merkleRoot       | bytes32 | 新的默克尔根                     |
| newTotalReward   | uint256 | root manager本次更新的奖励总额      |
| newRewardOffset  | uint256 | 本次更新过后，总奖励的累积历史偏差          |
| prevRewardOffset | uint256 | 本次更新过后，上一轮epoch的总奖励的累积历史偏差 |

### EventClaimContributionReward

```solidity
event EventClaimContributionReward(uint256 uid, address account, uint256 userMerkleTotalReward, uint256 claimReward, uint256 merkleClaimReward, uint256 bondInviteReward)
```

事件-用户领取社群贡献奖励并线性释放


Parameters:

| Name                  | Type    | Description            |
| :-------------------- | :------ | :--------------------- |
| account               | address | 奖励领取用户                 |
| userMerkleTotalReward | uint256 | 用户新的总奖励(merkle树中存储的值)  |
| claimReward           | uint256 | 本次释放的总奖励               |
| merkleClaimReward     | uint256 | 本次通过merkle释放的奖励数量      |
| bondInviteReward      | uint256 | 本次释放的债券推荐奖励            |

### EventTriggerBondInviteReward

```solidity
event EventTriggerBondInviteReward(uint256 uid, address recipient, uint256 triggerTime, uint256 amount)
```

用户新增债券推荐奖励


Parameters:

| Name        | Type    | Description |
| :---------- | :------ | :---------- |
| recipient   | address | 用户地址        |
| triggerTime | uint256 | 新增时间        |
| amount      | uint256 | 新增数量        |

## Constants info

### ROOT_MANAGER (0x5f61e3ec)

```solidity
bytes32 constant ROOT_MANAGER = keccak256("ROOT_MANAGER")
```


### BOND_DEPOSITORY (0x361beb07)

```solidity
bytes32 constant BOND_DEPOSITORY = keccak256("BOND_DEPOSITORY")
```


## State variables info

### RELEASE_POOL (0x0119d777)

```solidity
contract IReleasePool immutable RELEASE_POOL
```


### CSM (0x8de2b272)

```solidity
address immutable CSM
```


### merkleTotalClaimed (0x82328939)

```solidity
mapping(uint256 => uint256) merkleTotalClaimed
```


### lastRewardOffset (0x7f968dd8)

```solidity
mapping(uint256 => uint256) lastRewardOffset
```


### bondInviteTotalReward (0x3ea3a5a4)

```solidity
mapping(uint256 => uint256) bondInviteTotalReward
```


### bondInviteClaimableReward (0x4737d7eb)

```solidity
mapping(uint256 => mapping(address => uint256)) bondInviteClaimableReward
```

uid=>user=>未开始释放的债券推荐奖励
### merkleRoot (0x3c70b357)

```solidity
mapping(uint256 => bytes32) merkleRoot
```


### merkleClaimedAmounts (0x43029480)

```solidity
mapping(uint256 => mapping(address => uint256)) merkleClaimedAmounts
```

uid=>用户地址=>社群奖励中已领取奖励数量
### maxEpoch (0x51a1e2ac)

```solidity
mapping(uint256 => uint256) maxEpoch
```


### prevEpochRewardOffset (0xfdbc8a8a)

```solidity
mapping(uint256 => uint256) prevEpochRewardOffset
```


## Modifiers info

### onlyRootManager

```solidity
modifier onlyRootManager()
```


### onlyBondDepository

```solidity
modifier onlyBondDepository()
```


## Functions info

### constructor

```solidity
constructor(address _CSM, address _releasePool)
```


### initialize (0x8129fc1c)

```solidity
function initialize() public initializer
```


### cumulativeReward (0x68002a04)

```solidity
function cumulativeReward(uint256 uid_) public view returns (uint256)
```


### rebaseMaxContributionReward (0x2611bf85)

```solidity
function rebaseMaxContributionReward(
    uint256 uid_
) public view returns (uint256)
```

当前最新的社区奖励的最大值

需要减去Bond invite奖励


Parameters:

| Name | Type    | Description |
| :--- | :------ | :---------- |
| uid_ | uint256 | 项目id        |


Return values:

| Name | Type    | Description |
| :--- | :------ | :---------- |
| [0]  | uint256 | 奖励最大值       |

### rebaseMaxContributionRewardFromPrev (0x25c6cb14)

```solidity
function rebaseMaxContributionRewardFromPrev(
    uint256 uid_
) public view returns (uint256)
```

上轮epoch结束后的社区奖励的最大值

需要减去Bond invite奖励


Parameters:

| Name | Type    | Description |
| :--- | :------ | :---------- |
| uid_ | uint256 | 项目id        |


Return values:

| Name | Type    | Description |
| :--- | :------ | :---------- |
| [0]  | uint256 | 奖励最大值       |

### receiveBondInvite (0xc9c44e63)

```solidity
function receiveBondInvite(
    uint256 uid_,
    address recipient_,
    uint256 amount_
) external onlyBondDepository
```


### claim (0x67cb559c)

```solidity
function claim(
    uint256 uid_,
    uint256 totalAmount_,
    bytes32[] calldata merkleProof_,
    address burnToken_,
    uint256 burnAmt_,
    uint256 releaseLevel_
) external
```

领取社群奖励，包括债券的invite


Parameters:

| Name          | Type      | Description |
| :------------ | :-------- | :---------- |
| uid_          | uint256   | 项目id        |
| totalAmount_  | uint256   | 总奖励金额       |
| merkleProof_  | bytes32[] | 默克尔证明       |
| burnToken_    | address   | 销毁Token     |
| burnAmt_      | uint256   | 销毁数量        |
| releaseLevel_ | uint256   | 释放等级        |

### updateMerkleRoot (0x85f15c13)

```solidity
function updateMerkleRoot(
    uint256 uid_,
    bytes32 merkleRoot_,
    uint256 newTotalReward_,
    uint256 epochIndex_
) external onlyRootManager
```

更新默克尔根


Parameters:

| Name            | Type    | Description |
| :-------------- | :------ | :---------- |
| uid_            | uint256 | 项目id        |
| merkleRoot_     | bytes32 | 默克尔根        |
| newTotalReward_ | uint256 | 本次更新的总奖励    |
| epochIndex_     | uint256 | epochNumber |
