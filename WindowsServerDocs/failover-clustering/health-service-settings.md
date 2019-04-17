---
title: "건강 서비스 설정"
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: 
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: 569cf7ba30fd3f993394efd3735a56d116c067e0
ms.sourcegitcommit: 30fcae929ce7b611f5d3a5f8fee64b0299272110
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2017
---
# <a name="health-service-settings"></a>건강 서비스 설정
> Windows Server 2016 적용 됩니다.

상태 서비스는 Storage Spaces Direct 실행 클러스터에 대 한 작동 경험과 일상적인 모니터링 개선 하는 Windows Server 2016의 새로운 기능입니다.

매개 상태 서비스의 동작을 결정 하는 다양 한 설정으로 표시 됩니다. 켜기/끄기 특정 동작을 조정 오류나 작업의 수준에이 등을 수정할 수 있습니다.

다음 PowerShell cmdlet를 설정 하거나 설정 수정할 사용 합니다.

### <a name="usage"></a>사용

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name <SettingName> -Value <Value>  
```

#### <a name="example"></a>예제

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.Volume.CapacityThreshold.Warning" -Value 70
```

### <a name="common-settings"></a>일반 설정

일부 일반적으로 수정된 설정이 기본값으로 함께 아래 나열 됩니다.

#### <a name="volume-capacity-threshold"></a>볼륨 용량 임계값

```
"System.Storage.Volume.CapacityThreshold.Enabled"  = True
"System.Storage.Volume.CapacityThreshold.Warning"  = 80
"System.Storage.Volume.CapacityThreshold.Critical" = 90
```

#### <a name="pool-reserve-capacity-threshold"></a>풀 용량 임계값 예약

```
"System.Storage.StoragePool.CheckPoolReserveCapacity.Enabled" = True
```

#### <a name="physical-disk-lifecycle"></a>하 여 실제 디스크 수명 주기

```
"System.Storage.PhysicalDisk.AutoPool.Enabled"                             = True
"System.Storage.PhysicalDisk.AutoRetire.OnLostCommunication.Enabled"       = True
"System.Storage.PhysicalDisk.AutoRetire.OnUnresponsive.Enabled"            = True
"System.Storage.PhysicalDisk.AutoRetire.DelayMs"                           = 900000 (i.e. 15 minutes)
"System.Storage.PhysicalDisk.Unresponsive.Reset.CountResetIntervalSeconds" = 360 (i.e. 60 minutes)
"System.Storage.PhysicalDisk.Unresponsive.Reset.CountAllowed"              = 3
```

#### <a name="supported-components-document"></a>지원 되는 구성 요소 문서

이전 섹션을 참조 합니다.

#### <a name="firmware-rollout"></a>펌웨어 롤아웃

```
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.SingleDrive.Enabled"       = True
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.Enabled"           = True
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.LongDelaySeconds"  = 604800 (i.e. 7 days)
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.ShortDelaySeconds" = 86400 (i.e. 1 day)
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.LongDelayCount"    = 1
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.FailureTolerance"  = 3
```

#### <a name="platform--quiescence"></a>플랫폼 / Quiescence

```
"Platform.Quiescence.MinDelaySeconds" = 120 (i.e. 2 minutes)
"Platform.Quiescence.MaxDelaySeconds" = 420 (i.e. 7 minutes)
```

#### <a name="metrics"></a>메트릭

```
"System.Reports.ReportingPeriodSeconds" = 1
```

#### <a name="debugging"></a>디버깅

```
"System.LogLevel" = 4
```

## <a name="see-also"></a>참조 하십시오

- [Windows Server 2016에에서 상태 서비스](health-service-overview.md)
- [Windows Server 2016에에서 저장소 공간 다이렉트](../storage/storage-spaces/storage-spaces-direct-overview.md)
