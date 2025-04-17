# Treasury

## Overview

#### License: AGPL-3.0-or-later

```solidity
contract Treasury is OwnableUpgradeable
```


## Enums info

### MANAGING

```solidity
enum MANAGING {
	 RESERVEDEPOSITOR,
	 RESERVESPENDER,
	 RESERVETOKEN,
	 RESERVEMANAGER,
	 LIQUIDITYDEPOSITOR,
	 LIQUIDITYTOKEN,
	 LIQUIDITYMANAGER,
	 DEBTOR,
	 REWARDMANAGER,
	 SCSM
}
```


## Events info

### Deposit

```solidity
event Deposit(address indexed token, uint256 amount, uint256 value)
```


### Withdrawal

```solidity
event Withdrawal(address indexed token, uint256 amount, uint256 value)
```


### CreateDebt

```solidity
event CreateDebt(address indexed debtor, address indexed token, uint256 amount, uint256 value)
```


### RepayDebt

```solidity
event RepayDebt(address indexed debtor, address indexed token, uint256 amount, uint256 value)
```


### ReservesManaged

```solidity
event ReservesManaged(address indexed token, uint256 amount)
```


### ReservesUpdated

```solidity
event ReservesUpdated(uint256 indexed totalReserves)
```


### ReservesAudited

```solidity
event ReservesAudited(uint256 indexed totalReserves)
```


### RewardsMinted

```solidity
event RewardsMinted(address indexed caller, address indexed recipient, uint256 amount)
```


### ChangeQueued

```solidity
event ChangeQueued(Treasury.MANAGING indexed managing, address queued)
```


### ChangeActivated

```solidity
event ChangeActivated(Treasury.MANAGING indexed managing, address activated, bool result)
```


## State variables info

### CSM (0x8de2b272)

```solidity
address immutable CSM
```


### blocksNeededForQueue (0xd07f390f)

```solidity
uint256 immutable blocksNeededForQueue
```


### reserveTokens (0xd031370b)

```solidity
address[] reserveTokens
```


### isReserveToken (0x68c31dd5)

```solidity
mapping(address => bool) isReserveToken
```


### reserveTokenQueue (0x788c6c01)

```solidity
mapping(address => uint256) reserveTokenQueue
```


### reserveDepositors (0x6b5e40a7)

```solidity
address[] reserveDepositors
```


### isReserveDepositor (0x124154ca)

```solidity
mapping(address => bool) isReserveDepositor
```


### reserveDepositorQueue (0x932cc8c3)

```solidity
mapping(address => uint256) reserveDepositorQueue
```


### reserveSpenders (0x437f7912)

```solidity
address[] reserveSpenders
```


### isReserveSpender (0x87d67dff)

```solidity
mapping(address => bool) isReserveSpender
```


### reserveSpenderQueue (0xc24ad43e)

```solidity
mapping(address => uint256) reserveSpenderQueue
```


### liquidityTokens (0xfd1ec010)

```solidity
address[] liquidityTokens
```


### isLiquidityToken (0xa569e571)

```solidity
mapping(address => bool) isLiquidityToken
```


### LiquidityTokenQueue (0x8f59c727)

```solidity
mapping(address => uint256) LiquidityTokenQueue
```


### liquidityDepositors (0x8f6a7b57)

```solidity
address[] liquidityDepositors
```


### isLiquidityDepositor (0xa1210a2d)

```solidity
mapping(address => bool) isLiquidityDepositor
```


### LiquidityDepositorQueue (0xfff9ee87)

```solidity
mapping(address => uint256) LiquidityDepositorQueue
```


### bondCalculator (0x1af4da70)

```solidity
mapping(address => address) bondCalculator
```


### reserveManagers (0x0619aff1)

```solidity
address[] reserveManagers
```


### isReserveManager (0xebd83cd8)

```solidity
mapping(address => bool) isReserveManager
```


### ReserveManagerQueue (0xb1bd38b0)

```solidity
mapping(address => uint256) ReserveManagerQueue
```


### liquidityManagers (0x70a0502a)

```solidity
address[] liquidityManagers
```


### isLiquidityManager (0xdf89b344)

```solidity
mapping(address => bool) isLiquidityManager
```


### LiquidityManagerQueue (0xab319c9a)

```solidity
mapping(address => uint256) LiquidityManagerQueue
```


### debtors (0x869871bf)

```solidity
address[] debtors
```


### isDebtor (0xee4e19a1)

```solidity
mapping(address => bool) isDebtor
```


### debtorQueue (0xcd85641a)

```solidity
mapping(address => uint256) debtorQueue
```


### debtorBalance (0x094a8651)

```solidity
mapping(address => uint256) debtorBalance
```


### rewardManagers (0xb5b1d560)

```solidity
address[] rewardManagers
```


### isRewardManager (0x4e83423c)

```solidity
mapping(address => bool) isRewardManager
```


### rewardManagerQueue (0xfb939588)

```solidity
mapping(address => uint256) rewardManagerQueue
```


### sCSM (0x63032870)

```solidity
address sCSM
```


### sCSMQueue (0x6f297ab0)

```solidity
uint256 sCSMQueue
```


### totalReserves (0x8f840ddd)

```solidity
uint256 totalReserves
```


### totalDebt (0xfc7b9c18)

```solidity
uint256 totalDebt
```


## Functions info

### constructor

```solidity
constructor(address _CSM, uint256 _blocksNeededForQueue)
```


### initialize (0xc0c53b8b)

```solidity
function initialize(
    address _USDT,
    address _USDTCSM,
    address _calu
) public initializer
```


### deposit (0xbc157ac1)

```solidity
function deposit(
    uint256 _amount,
    address _token,
    uint256 _profit
) external returns (uint256 send_)
```

allow approved address to deposit an asset for CSM
        @param _amount uint
        @param _token address
        @param _profit uint
        @return send_ uint
### withdraw (0x00f714ce)

```solidity
function withdraw(uint256 _amount, address _token) external
```

allow approved address to burn CSM for reserves
        @param _amount uint
        @param _token address
### incurDebt (0x12422d23)

```solidity
function incurDebt(uint256 _amount, address _token) external
```

allow approved address to borrow reserves
        @param _amount uint
        @param _token address
### repayDebtWithReserve (0xd796ffb8)

```solidity
function repayDebtWithReserve(uint256 _amount, address _token) external
```

allow approved address to repay borrowed reserves with reserves
        @param _amount uint
        @param _token address
### repayDebtWithCSM (0x5aff82c6)

```solidity
function repayDebtWithCSM(uint256 _amount) external
```

allow approved address to repay borrowed reserves with CSM
        @param _amount uint
### manage (0x0b0eee30)

```solidity
function manage(address _token, uint256 _amount) external
```

allow approved address to withdraw assets
        @param _token address
        @param _amount uint
### mintRewards (0x6a20de92)

```solidity
function mintRewards(address _recipient, uint256 _amount) external
```

send epoch reward to staking contract
### excessReserves (0x0c3513a8)

```solidity
function excessReserves() public view returns (uint256)
```

returns excess reserves not backing tokens
        @return uint
### auditReserves (0x2b7ce500)

```solidity
function auditReserves() external onlyOwner
```

takes inventory of all tracked assets
        @notice always consolidate to recognized reserves before audit
### valueOf (0x1eec5a9a)

```solidity
function valueOf(
    address _token,
    uint256 _amount
) public view returns (uint256 value_)
```

returns CSM valuation of asset
        @param _token address
        @param _amount uint
        @return value_ uint
### queue (0xe83afee3)

```solidity
function queue(
    Treasury.MANAGING _managing,
    address _address
) external onlyOwner returns (bool)
```

queue address to change boolean in mapping
        @param _managing MANAGING
        @param _address address
        @return bool
### toggle (0xfbfd393b)

```solidity
function toggle(
    Treasury.MANAGING _managing,
    address _address,
    address _calculator
) external onlyOwner returns (bool)
```

verify queue then set boolean in mapping
        @param _managing MANAGING
        @param _address address
        @param _calculator address
        @return bool