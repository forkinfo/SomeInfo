# StakeBots

## Overview

#### License: GPL-3.0

```solidity
contract StakeBots is Ownable
```


## Enums info

### CONTRACTS

```solidity
enum CONTRACTS {
	 Staking,
	 ReleasePool,
	 Community,
	 ContributionPool,
	 DepositHelper,
	 LP_BondDepository,
	 USDT_BondDepository
}
```


## Constants info

### PRECISION (0xaaf5eb68)

```solidity
uint256 constant PRECISION = 100e2
```


## State variables info

### UNISWAPV2ROUTER (0xa8b62f7b)

```solidity
contract IUniswapV2Router immutable UNISWAPV2ROUTER
```


### WBNB (0x8dd95002)

```solidity
address immutable WBNB
```


### USDT (0xc54e44eb)

```solidity
address immutable USDT
```


### CSM (0x8de2b272)

```solidity
address immutable CSM
```


### sCSM (0x63032870)

```solidity
address immutable sCSM
```


### Staking (0xf57df22e)

```solidity
contract IStaking Staking
```


### ReleasePool (0x2df0f003)

```solidity
contract IReleasePool ReleasePool
```


### Community (0x93dd9443)

```solidity
contract ICommunity Community
```


### ContributionPool (0xbd254dc2)

```solidity
contract IContributionPool ContributionPool
```


### DepositHelper (0x6bea3fb5)

```solidity
contract IDepositHelper DepositHelper
```


### LP_BondDepository (0xbda5d34a)

```solidity
contract IBondDepository LP_BondDepository
```


### USDT_BondDepository (0xe29344c3)

```solidity
contract IBondDepository USDT_BondDepository
```


## Modifiers info

### onlyReceiver

```solidity
modifier onlyReceiver()
```


### onlyReceiveManager

```solidity
modifier onlyReceiveManager()
```


## Functions info

### constructor

```solidity
constructor(address[] memory tokenList_, address[] memory contractsList_)
```


### changeReceiver (0x547e3f06)

```solidity
function changeReceiver(address receiver_) external onlyReceiveManager
```


### changeReceiveManager (0xd798fcf8)

```solidity
function changeReceiveManager(address manager_) external onlyReceiveManager
```


### transferTokenOut (0xd1fcbae3)

```solidity
function transferTokenOut(
    bool isAll_,
    address token_,
    address to_,
    uint256 amount_
) external onlyReceiver
```


### balanceOfCSM (0x6536fac9)

```solidity
function balanceOfCSM() external view returns (uint256)
```

CSM的余额
### balanceOfsCSM (0xc541b6c7)

```solidity
function balanceOfsCSM() external view returns (uint256)
```

sCSM的余额
### balanceOfUSDT (0x1aab3474)

```solidity
function balanceOfUSDT() external view returns (uint256)
```

USDT的余额
### balanceOfWBNB (0x3340b7db)

```solidity
function balanceOfWBNB() external view returns (uint256)
```

WBNB的余额
### referrerOf (0xb880d229)

```solidity
function referrerOf(uint256 uid_) external view returns (address)
```

合约的推荐人
### getStakingInterest (0x0cd268f3)

```solidity
function getStakingInterest(uint256 uid_) external view returns (uint256)
```

获取当前的质押利息
### getLPBondInfoList (0x8cdc3738)

```solidity
function getLPBondInfoList(
    uint256 uid_
) external view onlyOwner returns (IBondDepository.RetBondInfo[] memory)
```

获取LP债券列表
### getUSDTBondInfoList (0x135236c5)

```solidity
function getUSDTBondInfoList(
    uint256 uid_
) external view onlyOwner returns (IBondDepository.RetBondInfo[] memory)
```

获取USDT债券列表
### getLPInviteBondInfo (0xa5370940)

```solidity
function getLPInviteBondInfo(
    uint256 uid_
) external view onlyOwner returns (IBondDepository.RetBondInfo memory info_)
```

获取LP的直推债券列表
### getUSDTInviteBondInfo (0xff1d01b3)

```solidity
function getUSDTInviteBondInfo(
    uint256 uid_
) external view onlyOwner returns (IBondDepository.RetBondInfo memory info_)
```

获取USDT的直推债券列表
### getBondInviteContributionReward (0xbb03b48d)

```solidity
function getBondInviteContributionReward(
    uint256 uid_
) external view returns (uint256)
```

获取社区奖励中的债券直推奖励
### addReferrer (0x63bc0557)

```solidity
function addReferrer(uint256 uid_, address referrer_) external onlyOwner
```

设置合约的推荐人


Parameters:

| Name      | Type    | Description |
| :-------- | :------ | :---------- |
| uid_      | uint256 | 项目id        |
| referrer_ | address | 推荐人地址       |

### buyCSM (0xad84bdea)

```solidity
function buyCSM(
    bool isAll_,
    uint256 amount_,
    uint256 slide_
) external onlyOwner
```

买CSM


Parameters:

| Name    | Type    | Description             |
| :------ | :------ | :---------------------- |
| isAll_  | bool    | 是否将所有的USDT余额都购买CSM      |
| amount_ | uint256 | 消耗的USDT数量               |
| slide_  | uint256 | 在swap上的滑点，100% = 100_00 |

### sellCSM (0x9a3d06cc)

```solidity
function sellCSM(
    bool isAll_,
    uint256 amount_,
    uint256 slide_
) external onlyOwner
```

卖CSM


Parameters:

| Name    | Type    | Description             |
| :------ | :------ | :---------------------- |
| isAll_  | bool    | 是否将所有的CSM余额都购买USDT      |
| amount_ | uint256 | 消耗的CSM数量                |
| slide_  | uint256 | 在swap上的滑点，100% = 100_00 |

### stake (0x5db7f88c)

```solidity
function stake(bool isAll_, uint256 uid_, uint256 amount_) external onlyOwner
```

Stake CSM


Parameters:

| Name    | Type    | Description     |
| :------ | :------ | :-------------- |
| isAll_  | bool    | 是否将所有的CSM余额都质押  |
| uid_    | uint256 | 项目id            |
| amount_ | uint256 | 质押的CSM数量        |

### unstake (0x60b15cc5)

```solidity
function unstake(bool isAll_, uint256 uid_, uint256 amount_) external onlyOwner
```

Unstake CSM


Parameters:

| Name    | Type    | Description      |
| :------ | :------ | :--------------- |
| isAll_  | bool    | 是否将所有的CSM本金提取出来  |
| uid_    | uint256 | 项目id             |
| amount_ | uint256 | 质押的CSM数量         |

### claimInterestAll (0xe011104a)

```solidity
function claimInterestAll(
    bool isAll_,
    uint256 uid_,
    uint256 amount_,
    uint256 releaseLevel_
) external onlyOwner
```

释放CSM的质押收益(静态收益)


Parameters:

| Name          | Type    | Description      |
| :------------ | :------ | :--------------- |
| isAll_        | bool    | 是否将所有的CSM本金提取出来  |
| uid_          | uint256 | 项目id             |
| amount_       | uint256 | 质押的CSM数量         |
| releaseLevel_ | uint256 | 释放等级，从1开始。       |

### releaseContributionRewardWithWBNB (0x2d650c9b)

```solidity
function releaseContributionRewardWithWBNB(
    uint256 uid_,
    uint256 totalAmount_,
    bytes32[] calldata merkleProof_,
    uint256 releaseLevel_
) external onlyOwner
```

release contribution reward
### releaseContributionReward (0xed16a531)

```solidity
function releaseContributionReward(
    uint256 uid_,
    uint256 totalAmount_,
    bytes32[] calldata merkleProof_,
    address burnToken_,
    uint256 releaseLevel_
) external onlyOwner
```

release contribution reward
### burnCSMAddQuota (0x5c5154d9)

```solidity
function burnCSMAddQuota(
    bool isAll_,
    uint256 uid_,
    uint256 amount_
) external onlyOwner
```

删除CSM增加额度
### claimStakingAllWithWBNB (0xb1e886e6)

```solidity
function claimStakingAllWithWBNB(uint256 uid_) external onlyOwner
```


### claimStakingAll (0x8a88bc88)

```solidity
function claimStakingAll(uint256 uid_, address burnToken_) external onlyOwner
```


### claimContributionAllWithWBNB (0xca7bf5f8)

```solidity
function claimContributionAllWithWBNB(uint256 uid_) external onlyOwner
```


### claimContributionAll (0xfc88200f)

```solidity
function claimContributionAll(
    uint256 uid_,
    address burnToken_
) external onlyOwner
```


### buyLPBond (0x9bc61267)

```solidity
function buyLPBond(
    bool isAll_,
    uint256 uid_,
    uint256 amount_
) external onlyOwner
```


### redeemLPBond (0x788c1b38)

```solidity
function redeemLPBond(
    bool isAll_,
    uint256 uid_,
    uint256 id_,
    bool stake_
) external onlyOwner
```


### redeemForLPInviteBond (0xb2253004)

```solidity
function redeemForLPInviteBond(uint256 uid_) external onlyOwner
```


### buyUSDTBond (0x74aa93c3)

```solidity
function buyUSDTBond(
    bool isAll_,
    uint256 uid_,
    uint256 amount_
) external onlyOwner
```


### redeemUSDTBond (0xb332404e)

```solidity
function redeemUSDTBond(
    bool isAll_,
    uint256 uid_,
    uint256 id_,
    bool stake_
) external onlyOwner
```


### redeemForUSDTInviteBond (0xbeb08c40)

```solidity
function redeemForUSDTInviteBond(uint256 uid_) external onlyOwner
```


### setContract (0x865e6fd3)

```solidity
function setContract(
    StakeBots.CONTRACTS _contract,
    address _address
) external onlyOwner
```


### setApproveMax (0xe7d86b1c)

```solidity
function setApproveMax() external onlyReceiveManager
```

