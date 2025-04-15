# Staking

## Overview

#### License: AGPL-3.0-or-later

```solidity
contract Staking is OwnableUpgradeable
```


## Enums info

### CONTRACTS

```solidity
enum CONTRACTS {
	 DISTRIBUTOR,
	 WARMUP,
	 LOCKER
}
```


## Structs info

### Epoch

```solidity
struct Epoch {
	uint256 length;
	uint256 number;
	uint256 endBlockTime;
	uint256 distribute;
}
```


### Claim

```solidity
struct Claim {
	uint256 deposit;
	uint256 gons;
	uint256 expiry;
	bool lock;
}
```


## Events info

### Staked

```solidity
event Staked(uint256 indexed uid, address indexed staker, uint256 amount)
```


### Unstaked

```solidity
event Unstaked(uint256 indexed uid, address indexed staker, uint256 unstakeAmount)
```


### Principal

```solidity
event Principal(uint256 indexed uid, address indexed staker, uint256 principal)
```


### Forfeited

```solidity
event Forfeited(uint256 indexed uid, address indexed staker, uint256 amount)
```


### EventStartClaimInterest

```solidity
event EventStartClaimInterest(uint256 indexed uid, address indexed staker, uint256 amount)
```


### EventRebase

```solidity
event EventRebase(uint256 curEpochNumber, uint256 profit, uint256 nextProfit, uint256 stakingCSMBalance, uint256 sCSMCirculatingSupply)
```

rebase数据


Parameters:

| Name                  | Type    | Description           |
| :-------------------- | :------ | :-------------------- |
| curEpochNumber        | uint256 | 当前epoch序号             |
| profit                | uint256 | 本次rebase总发放收益         |
| nextProfit            | uint256 | 下次rebase预计发放收益        |
| stakingCSMBalance     | uint256 | 当前Staking中CSM的存量      |
| sCSMCirculatingSupply | uint256 | 当前sCSM的circulation供应量 |

## State variables info

### RELEASE_POOL (0x0119d777)

```solidity
contract IReleasePool immutable RELEASE_POOL
```


### PAIR_CSM_USDT (0x428916ac)

```solidity
address immutable PAIR_CSM_USDT
```


### WBNB (0x8dd95002)

```solidity
address immutable WBNB
```


### CSM (0x8de2b272)

```solidity
address immutable CSM
```


### sCSM (0x63032870)

```solidity
address immutable sCSM
```


### epoch (0x900cf0cf)

```solidity
struct Staking.Epoch epoch
```


### distributor (0xbfe10928)

```solidity
address distributor
```


### locker (0xd7b96d4e)

```solidity
address locker
```


### totalBonus (0xa8dd07dc)

```solidity
uint256 totalBonus
```


### warmupContract (0xed4acaa8)

```solidity
address warmupContract
```


### warmupPeriod (0xdeac361a)

```solidity
uint256 warmupPeriod
```


### warmupInfo (0x11c3bf85)

```solidity
mapping(uint256 => mapping(address => struct Staking.Claim)) warmupInfo
```


### principals (0x767f06f1)

```solidity
mapping(uint256 => mapping(address => uint256)) principals
```


## Functions info

### constructor

```solidity
constructor(
    address _CSM,
    address _sCSM,
    address _WBNB,
    address _releasePool,
    address _pairCSMUSDT
)
```


### initialize (0x80d85911)

```solidity
function initialize(
    uint256 _epochTimeLength,
    uint256 _firstEpochNumber,
    uint256 _firstEpochBlockTime
) public initializer
```


### getStakeInfo (0x5cb7d00b)

```solidity
function getStakeInfo(
    uint256 _uid,
    address _user
)
    external
    view
    returns (uint256 principalAmt, uint256 interest, uint256 sCSMInWarmup)
```

获取质押信息


Parameters:

| Name  | Type    | Description |
| :---- | :------ | :---------- |
| _uid  | uint256 | 项目id        |
| _user | address | 用户地址        |


Return values:

| Name         | Type    | Description    |
| :----------- | :------ | :------------- |
| principalAmt | uint256 | 质押本金           |
| interest     | uint256 | 收益             |
| sCSMInWarmup | uint256 | warmup中的sCSM数量 |

### getStakeAmount (0x238aa19d)

```solidity
function getStakeAmount(
    uint256 _uid,
    address _user
) public view returns (uint256)
```

获取质押数量
### getStakeTokenWorth (0x9248f8d3)

```solidity
function getStakeTokenWorth(
    uint256 _uid,
    address _user
) public view returns (uint256)
```

获取质押CSM的USD价值
### getStakedAmountList (0xc2e5ed92)

```solidity
function getStakedAmountList(
    uint256 uid_,
    address[] calldata accountList_
) external view returns (uint256[] memory amountList_)
```


### stake (0x7628a37d)

```solidity
function stake(
    uint256 _uid,
    uint256 _amount,
    address _recipient
) external returns (bool)
```

质押CSM，进入Warmup


Parameters:

| Name       | Type    | Description       |
| :--------- | :------ | :---------------- |
| _uid       | uint256 | 项目id              |
| _amount    | uint256 | 质押数量              |
| _recipient | address | CSM的owner @return |

### claim (0xddd5e1b2)

```solidity
function claim(uint256 _uid, address _recipient) external
```

从Warmup中领取sCSM


Parameters:

| Name       | Type    | Description |
| :--------- | :------ | :---------- |
| _uid       | uint256 | 项目id        |
| _recipient | address | 接受sCSM的地址   |

### forfeit (0x3ed546ab)

```solidity
function forfeit(uint256 _uid) external
```

强制收回CSM
### unstake (0x5b64f391)

```solidity
function unstake(uint256 _uid, bool _trigger, uint256 _amount) external
```

unstake 本金


Parameters:

| Name     | Type    | Description   |
| :------- | :------ | :------------ |
| _uid     | uint256 | 项目id          |
| _trigger | bool    | 是否尝试触发rebase  |
| _amount  | uint256 | unstake的数量    |

### claimInterest (0x3605134e)

```solidity
function claimInterest(
    uint256 _uid,
    bool _trigger,
    uint256 _amount,
    uint256 _burnAmt,
    uint256 _releaseLevel
) external
```

开始释放Staking收益。


Parameters:

| Name          | Type    | Description       |
| :------------ | :------ | :---------------- |
| _uid          | uint256 | 项目id              |
| _trigger      | bool    | 是否尝试触发rebase      |
| _amount       | uint256 | 释放的收益数量           |
| _burnAmt      | uint256 | 释放收益所需要销毁的数量      |
| _releaseLevel | uint256 | 释放等级。1~5对应150天到7天 |

### toggleDepositLock (0xd8295c3f)

```solidity
function toggleDepositLock(uint256 _uid) external
```

prevent new deposits to address (protection from malicious activity)
### index (0x2986c0e5)

```solidity
function index() public view returns (uint256)
```

returns the sCSM index, which tracks rebase growth


Return values:

| Name | Type    | Description        |
| :--- | :------ | :----------------- |
| [0]  | uint256 | uint256 sCSM的index |

### rebase (0xaf14052c)

```solidity
function rebase() public
```

trigger rebase if epoch over
### contractBalance (0x8b7afe2e)

```solidity
function contractBalance() public view returns (uint256)
```

returns contract CSM holdings, including bonuses provided


Return values:

| Name | Type    | Description |
| :--- | :------ | :---------- |
| [0]  | uint256 | uint 合约余额   |

### giveLockBonus (0x03c23670)

```solidity
function giveLockBonus(uint256 _amount) external
```

provide bonus to locked staking contract


Parameters:

| Name    | Type    | Description |
| :------ | :------ | :---------- |
| _amount | uint256 | uint        |

### returnLockBonus (0xf62ae76a)

```solidity
function returnLockBonus(uint256 _amount) external
```

reclaim bonus from locked staking contract


Parameters:

| Name    | Type    | Description |
| :------ | :------ | :---------- |
| _amount | uint256 | uint        |

### setContract (0x865e6fd3)

```solidity
function setContract(
    Staking.CONTRACTS _contract,
    address _address
) external onlyOwner
```

sets the contract address for LP staking
        @param _contract address
### setWarmup (0xc9f464ff)

```solidity
function setWarmup(uint256 _warmupPeriod) external onlyOwner
```

set warmup period for new stakers


Parameters:

| Name          | Type    | Description |
| :------------ | :------ | :---------- |
| _warmupPeriod | uint256 | uint        |

### updateEpoch (0x15ca0dc0)

```solidity
function updateEpoch(uint256 _epochLength) external onlyOwner
```

