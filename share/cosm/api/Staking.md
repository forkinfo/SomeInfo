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
	uint256 endBlock;
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
event Staked(address indexed staker, uint256 amount)
```


### Unstaked

```solidity
event Unstaked(address indexed staker, bool isPrincipal, uint256 unstakeAmount)
```


### Principal

```solidity
event Principal(address indexed staker, uint256 principal)
```


### Forfeited

```solidity
event Forfeited(address indexed staker, uint256 amount)
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


### warmupInfo (0x6746f4c2)

```solidity
mapping(address => struct Staking.Claim) warmupInfo
```


### principals (0x76fbc359)

```solidity
mapping(address => uint256) principals
```


## Functions info

### constructor

```solidity
constructor(address _CSM, address _sCSM, address _releasePool)
```


### initialize (0x80d85911)

```solidity
function initialize(
    uint256 _epochLength,
    uint256 _firstEpochNumber,
    uint256 _firstEpochBlock
) public initializer
```


### stake (0x7acb7757)

```solidity
function stake(uint256 _amount, address _recipient) external returns (bool)
```

stake CSM to enter warmup
        @param _amount uint
        @return bool
### claim (0x1e83409a)

```solidity
function claim(address _recipient) external
```

retrieve sCSM from warmup
        @param _recipient address
### forfeit (0xf3d86e4a)

```solidity
function forfeit() external
```

forfeit sCSM in warmup and retrieve CSM
### unstakePrincipal (0x25dc76ca)

```solidity
function unstakePrincipal(uint256 _amount, bool _trigger) external
```

redeem sCSM for CSM
        @param _amount uint
        @param _trigger bool
### unstake (0x88cc9bd6)

```solidity
function unstake(
    uint256 _amount,
    bool _trigger,
    bool _isPrincipal,
    uint256 _burnAmt,
    uint256 _releaseLevel
) external
```


### toggleDepositLock (0x8f077b83)

```solidity
function toggleDepositLock() external
```

prevent new deposits to address (protection from malicious activity)
### index (0x2986c0e5)

```solidity
function index() public view returns (uint256)
```

returns the sCSM index, which tracks rebase growth
        @return uint
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
        @return uint
### giveLockBonus (0x03c23670)

```solidity
function giveLockBonus(uint256 _amount) external
```

provide bonus to locked staking contract
        @param _amount uint
### returnLockBonus (0xf62ae76a)

```solidity
function returnLockBonus(uint256 _amount) external
```

reclaim bonus from locked staking contract
        @param _amount uint
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
