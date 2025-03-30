# DashboardInfo

## Overview

#### License: GPL-3.0

```solidity
contract DashboardInfo is OwnableUpgradeable
```


## Functions info

### initialize (0x8129fc1c)

```solidity
function initialize() public initializer
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

### getChartsInfo (0x9b72aea1)

```solidity
function getChartsInfo()
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
