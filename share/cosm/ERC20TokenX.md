# ERC20TokenX

## Overview

#### License: AGPL-3.0-or-later

```solidity
contract ERC20TokenX is ERC20Token
```


## Events info

### FeeRatioChanged

```solidity
event FeeRatioChanged(uint8 ratioType, uint256 ratio)
```


### FeeTaken

```solidity
event FeeTaken(address indexed payer, address indexed receiver, bool isBuy, uint256 left, uint256 fee)
```


## Constants info

### PRECISION (0xaaf5eb68)

```solidity
uint256 constant PRECISION = 100e3
```


### INTERN_SYSTEM (0x1f9bbe20)

```solidity
bytes32 constant INTERN_SYSTEM = keccak256("INTERN_SYSTEM")
```


### COOLING_PROTECTOR (0x6d851e71)

```solidity
bytes32 constant COOLING_PROTECTOR = keccak256("COOLING_PROTECTOR")
```


## State variables info

### mainPair (0x85af30c5)

```solidity
address mainPair
```


### feeReceiver (0xb3f00674)

```solidity
address feeReceiver
```


### sellFeeRatio (0x9a44bc63)

```solidity
uint256 sellFeeRatio = 5e3
```


### buyFeeRatio (0xbffad1ad)

```solidity
uint256 buyFeeRatio
```


### coolingPeriod (0x9328beee)

```solidity
uint256 coolingPeriod
```


### coolingPeriodEndBlock (0x37391a60)

```solidity
uint256 coolingPeriodEndBlock
```


## Modifiers info

### onlyDefaultAdmin

```solidity
modifier onlyDefaultAdmin()
```


## Functions info

### constructor

```solidity
constructor(
    address _feeReceiver,
    uint256 _buyFeeRatio,
    string memory name_,
    string memory symbol_,
    address[] memory _coolingProtectors,
    uint256 _coolingPeriod
) ERC20Token(name_, symbol_)
```


### setMainPair (0xf30e85bc)

```solidity
function setMainPair(address pair) external onlyDefaultAdmin
```


### setRatio (0x799c711a)

```solidity
function setRatio(uint8 ratioType, uint256 ratio) external onlyDefaultAdmin
```

