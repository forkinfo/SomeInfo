# DashboardInfo

## Overview

#### License: GPL-3.0

```solidity
contract DashboardInfo is OwnableUpgradeable
```


## Enums info

### CONTRACTS

```solidity
enum CONTRACTS {
	 USDT,
	 CSM,
	 SCSM,
	 LP_CSM_USDT,
	 STAKING,
	 RELEASEPOOL,
	 TREASURY,
	 DISTRIBUTOR,
	 BONDCALCULATOR
}
```


## Constants info

### PRECISION (0xaaf5eb68)

```solidity
uint256 constant PRECISION = 1e4
```


### RATE_PRECISION (0x2b3ba681)

```solidity
uint256 constant RATE_PRECISION = 1e6
```


## State variables info

### USDT (0xc54e44eb)

```solidity
address USDT
```


### CSM (0x8de2b272)

```solidity
address CSM
```


### sCSM (0x63032870)

```solidity
address sCSM
```


### LP_CSM_USDT (0xdf5f7551)

```solidity
address LP_CSM_USDT
```


### staking (0x4cf088d9)

```solidity
address staking
```


### releasePool (0x23f7f407)

```solidity
address releasePool
```


### treasury (0x61d027b3)

```solidity
address treasury
```


### distributor (0xbfe10928)

```solidity
address distributor
```


### bondCalculator (0xc5332b7c)

```solidity
address bondCalculator
```


## Functions info

### initialize (0xf5e95acb)

```solidity
function initialize(
    address _USDT,
    address _CSM,
    address _sCSM,
    address _LP_CSM_USDT,
    address _staking,
    address _releasePool,
    address _treasury,
    address _distributor,
    address _bondCalculator
) public initializer
```


### overview (0x3a2056f1)

```solidity
function overview()
    external
    view
    returns (
        uint256 amountCSM,
        uint256 priceCSM,
        uint256 circulatingCSM,
        uint256 stakedCSM,
        uint256 bondUSDT,
        uint256 bondLPWorth
    )
```

Dashboard基本信息.


Return values:

| Name           | Type    | Description                       |
| :------------- | :------ | :-------------------------------- |
| amountCSM      | uint256 | Total Minting Amount(NVB), 精度9.   |
| priceCSM       | uint256 | NVB Price, 精度4.                   |
| circulatingCSM | uint256 | Circulating supply xxx CSM, 精度9.  |
| stakedCSM      | uint256 | Staked xxx CSM, 精度9.              |
| bondUSDT       | uint256 | Bond USDT$xxxx, 精度4.              |
| bondLPWorth    | uint256 | Bond LP$xxxx, 精度4.                |

### getChartsInfo (0xb17f20ea)

```solidity
function getChartsInfo(
    uint256 uid_
)
    external
    view
    returns (
        uint256 circulatingWorthCSM,
        uint256 treasuryRFV,
        uint256 treasuryLPRatio,
        uint256 stakedCSMRatio,
        uint256 runwayDay,
        uint256 treasuryAssetTotal,
        uint256 totalCSMBurning
    )
```

获取图标信息


Parameters:

| Name | Type    | Description |
| :--- | :------ | :---------- |
| uid_ | uint256 | 项目id        |


Return values:

| Name                | Type    | Description                                  |
| :------------------ | :------ | :------------------------------------------- |
| circulatingWorthCSM | uint256 | Total value of sCSM circulating supply, 精度4  |
| treasuryRFV         | uint256 | Risk Free Value of Treasury Assets, 精度4      |
| treasuryLPRatio     | uint256 | Protocol Owned Liquidity CSM-USDT, 精度4       |
| stakedCSMRatio      | uint256 | CSM Staked, 精度4                              |
| runwayDay           | uint256 | Runway Available, 精度4                        |
| treasuryAssetTotal  | uint256 | Market Value of Treasury Assets, 精度4         |
| totalCSMBurning     | uint256 | Total CSM Burning, 精度9                       |

### setContract (0x865e6fd3)

```solidity
function setContract(
    DashboardInfo.CONTRACTS _contract,
    address _address
) external onlyOwner
```


### getCirculatingWorthCSM (0x51363dfe)

```solidity
function getCirculatingWorthCSM()
    external
    view
    returns (uint256 circulatingWorthCSM)
```


### getTreasuryRFV (0x9f61a73a)

```solidity
function getTreasuryRFV() external view returns (uint256 treasuryRFV)
```


### getTreasuryLPRatio (0xeeeee4d4)

```solidity
function getTreasuryLPRatio() external view returns (uint256)
```


### getStakedCSMRatio (0xba410e67)

```solidity
function getStakedCSMRatio() external view returns (uint256)
```


### getRunway (0x5b6f9455)

```solidity
function getRunway() external view returns (uint256)
```


### getTotalCSMBurning (0xc38fb9ed)

```solidity
function getTotalCSMBurning(uint256 uid_) external view returns (uint256)
```


### getTreasuryAssetTotal (0x4ed3648a)

```solidity
function getTreasuryAssetTotal()
    external
    view
    returns (uint256 treasuryAssetTotal)
```

