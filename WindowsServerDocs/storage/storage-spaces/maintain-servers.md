---
title: 유지 관리를 위해 저장소 공간 다이렉트 서버를 오프라인으로 전환
ms.prod: windows-server
ms.author: eldenc
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 10/08/2018
ms.assetid: 73dd8f9c-dcdb-4b25-8540-1d8707e9a148
ms.localizationpriority: medium
ms.openlocfilehash: 2ccf8d809354f96277701cd365966ba5e914f64b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857536"
---
# <a name="taking-a-storage-spaces-direct-server-offline-for-maintenance"></a>유지 관리를 위해 저장소 공간 다이렉트 서버를 오프라인으로 전환

> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 [저장소 공간 다이렉트](storage-spaces-direct-overview.md)를 사용하여 서버를 올바르게 다시 시작 또는 종료하기 위한 지침을 제공합니다.

저장소 공간 다이렉트를 사용하는 경우 서버를 오프라인으로 전환(중지)한다는 것은 클러스터의 모든 서버가 공유하는 저장소 부분까지 오프라인으로 전환한다는 것입니다. 이렇게 하려면 오프라인으로 전환할 서버를 일시 중지(일시 중단)하고, 역할을 클러스터의 다른 서버로 이동하고, 클러스터의 다른 서버에서 모든 데이터를 사용할 수 있는지 확인해야 합니다. 그래야만 데이터가 안전하게 보존되고 유지 관리 작업이 수행되는 동안 데이터에 액세스할 수 있습니다.

다음 절차에 따라 저장소 공간 다이렉트 클러스터의 서버를 올바르게 일시 중지한 후 서버를 오프라인으로 전환하세요. 

   > [!IMPORTANT]
   > 저장소 공간 다이렉트 클러스터에 업데이트를 설치하려면 CAU(클러스터 인식 업데이트)를 사용하세요. 이 항목의 절차를 자동으로 수행하기 때문에 사용자는 업데이트를 설치할 때 아무 것도 할 필요가 없습니다. 자세한 내용은 [CAU(클러스터 인식 업데이트)](https://technet.microsoft.com/library/hh831694.aspx)를 참조하세요.

## <a name="verifying-its-safe-to-take-the-server-offline"></a>서버를 오프라인으로 전환해도 안전한지 확인

유지 관리를 위해 서버를 오프라인으로 전환하기 전에 모든 볼륨이 정상인지 확인해야 합니다.

확인하려면 관리자 권한으로 PowerShell 세션을 열고 다음 명령을 실행하여 볼륨 상태를 봅니다.

```PowerShell
Get-VirtualDisk 
```

그러면 다음과 같은 출력이 표시됩니다.
```
FriendlyName ResiliencySettingName OperationalStatus HealthStatus IsManualAttach Size
------------ --------------------- ----------------- ------------ -------------- ----
MyVolume1    Mirror                OK                Healthy      True           1 TB
MyVolume2    Mirror                OK                Healthy      True           1 TB
MyVolume3    Mirror                OK                Healthy      True           1 TB
```

모든 볼륨(가상 디스크)의 **HealthStatus** 속성이 **정상**인지 확인합니다.

장애 조치(failover) 클러스터 관리자에서 상태를 확인하려면 **저장소** > **디스크**로 이동합니다.

모든 볼륨(가상 디스크)의 **상태** 열이 **온라인**으로 표시되는지 확인합니다.

## <a name="pausing-and-draining-the-server"></a>서버 일시 중지 및 드레이닝

서버를 다시 시작하거나 종료하기 전에 서버에서 실행되는 모든 역할(예: 가상 컴퓨터)을 일시 중지하고 드레이닝(이동)합니다. 이렇게 하면 저장소 공간 다이렉트가 데이터를 정상적으로 플러시 및 커밋하여 해당 서버에서 실행되는 모든 응용 프로그램에 영향을 주지 않고 종료할 수 있습니다.

   > [!IMPORTANT]
   > 반드시 클러스터 서버를 일시 중지하고 드레이닝한 후 서버를 다시 시작하거나 종료하세요.

PowerShell에서 다음 cmdlet을 관리자 권한으로 실행하여 서버를 일시 중지하고 드레이닝합니다.

```PowerShell
Suspend-ClusterNode -Drain
```

장애 조치(Failover) 클러스터 관리자에서 이렇게 하려면 **노드**로 이동하여 노드를 마우스 오른쪽 단추로 클릭한 후 **일시 중지** > **역할 드레이닝**을 선택합니다.

![일시 중지-드레이닝](media/maintain-servers/pause-drain.png)

모든 가상 컴퓨터가 클러스터의 다른 서버로 실시간 마이그레이션을 시작합니다. 이 작업은 몇 분 정도 걸릴 수 있습니다.

   > [!NOTE]
   > 클러스터 노드를 일시 중지하고 적절하게 드레이닝하면 Windows가 자동으로 안전 검사를 수행하여 계속 진행해도 안전한지 확인합니다. 비정상적인 볼륨이 있으면 작업을 중지하고 사용자에게 계속 진행하기에 안전하지 않다고 경고합니다.

![안전 검사](media/maintain-servers/safety-check.png)

## <a name="shutting-down-the-server"></a>서버 종료

서버가 드레이닝을 완료하면 장애 조치(Failover) 클러스터 관리자 및 PowerShell에 **일시 중지됨**으로 표시됩니다.

![일시 중지됨](media/maintain-servers/paused.png)

이제 평소처럼(예를 들어 Restart-Computer 또는 Stop-Computer PowerShell cmdlet을 사용하여) 서버를 안전하게 다시 시작하거나 종료할 수 있습니다.

```PowerShell
Get-VirtualDisk 

FriendlyName ResiliencySettingName OperationalStatus HealthStatus IsManualAttach Size
------------ --------------------- ----------------- ------------ -------------- ----
MyVolume1    Mirror                Incomplete        Warning      True           1 TB
MyVolume2    Mirror                Incomplete        Warning      True           1 TB
MyVolume3    Mirror                Incomplete        Warning      True           1 TB
```

노드가 종료 되거나 노드에서 클러스터 서비스를 시작/중지 하 고 문제가 발생 하지 않아야 하는 경우 불완전 하거나 저하 된 작업 상태가 정상입니다. 모든 볼륨이 온라인 상태로 유지되며 액세스 가능합니다.

## <a name="resuming-the-server"></a>서버 다시 시작

서버가 워크로드를 호스트할 준비가 완료되면 서버를 다시 시작합니다.

PowerShell에서 다음 cmdlet을 관리자 권한으로 실행하여 서버를 다시 시작합니다.

```PowerShell
Resume-ClusterNode
```

이전에 이 서버에서 실행되던 역할을 되돌리려면 **-Failback** 플래그(선택 사항)를 사용합니다.

```PowerShell
Resume-ClusterNode –Failback Immediate
```

장애 조치(Failover) 클러스터 관리자에서 이렇게 하려면 **노드**로 이동하여 노드를 마우스 오른쪽 단추로 클릭한 후 **다시 시작** > **역할 장애 복구(failback)** 를 선택합니다.

![다시 시작-장애 복구(Failback)](media/maintain-servers/resume-failback.png)

## <a name="waiting-for-storage-to-resync"></a>저장소가 동기화될 때까지 대기

서버가 다시 시작 되 면 사용할 수 없는 상태에서 발생 한 모든 새 쓰기를 다시 동기화 해야 합니다. 이 작업은 자동으로 수행됩니다. 지능형 변경 추적을 사용하면 *모든* 데이터를 스캔하거나 동기화할 필요 없이 변경 내용만 처리하면 됩니다. 프로덕션 워크로드에 미치는 영향을 줄이기 위해 이 프로세스가 제한됩니다. 서버가 일시 중지된 시간과 새로 쓰여진 데이터의 양에 따라 작업이 완료될 때까지 다소 시간이 걸릴 수 있습니다.

재동기화가 완료될 때까지 기다렸다가 클러스터의 다른 서버를 오프라인으로 전환해야 합니다.

PowerShell에서 다음 cmdlet을 관리자 권한으로 실행하여 진행 상황을 모니터링합니다.

```PowerShell
Get-StorageJob
```
다음은 재동기화(복구) 작업을 보여 주는 몇 가지 출력 예제입니다.
```
Name   IsBackgroundTask ElapsedTime JobState  PercentComplete BytesProcessed BytesTotal
----   ---------------- ----------- --------  --------------- -------------- ----------
Repair True             00:06:23    Running   65              11477975040    17448304640
Repair True             00:06:40    Running   66              15987900416    23890755584
Repair True             00:06:52    Running   68              20104802841    22104819713
```

**BytesTotal**은 동기화해야 하는 저장소 공간을 보여 줍니다. **PercentComplete**는 진행 상황을 표시합니다.

   > [!WARNING]
   > 이러한 복구 작업이 완료되기 전에 다른 서버를 오프라인으로 전환하는 것은 안전하지 않습니다.

이 시간 동안 볼륨은 계속 **경고**로 표시되며 이는 정상적인 동작입니다. 

예를 들어 `Get-VirtualDisk`cmdlet을 사용하면 다음과 같은 출력이 표시될 수 있습니다.
```
FriendlyName ResiliencySettingName OperationalStatus HealthStatus IsManualAttach Size
------------ --------------------- ----------------- ------------ -------------- ----
MyVolume1    Mirror                InService         Warning      True           1 TB
MyVolume2    Mirror                InService         Warning      True           1 TB
MyVolume3    Mirror                InService         Warning      True           1 TB
```

작업이 완료되면 **cmdlet을 사용하여 볼륨이 다시**정상`Get-VirtualDisk`으로 표시되는지 확인합니다. 다음은 몇 가지 출력 예제입니다.

```
FriendlyName ResiliencySettingName OperationalStatus HealthStatus IsManualAttach Size
------------ --------------------- ----------------- ------------ -------------- ----
MyVolume1    Mirror                OK                Healthy      True           1 TB
MyVolume2    Mirror                OK                Healthy      True           1 TB
MyVolume3    Mirror                OK                Healthy      True           1 TB
```

이제 클러스터의 다른 서버를 일시 중지하고 다시 시작해도 안전합니다.

## <a name="how-to-update-storage-spaces-direct-nodes-offline"></a>오프 라인으로 스토리지 공간 다이렉트 노드를 업데이트 하는 방법
다음 단계를 사용 하 여 스토리지 공간 다이렉트 시스템의 경로를 신속 하 게 파악할 수 있습니다. 유지 관리 기간을 예약 하 고 시스템에서 패치를 적용 하는 작업을 수행 합니다. 신속 하 게 적용 해야 하는 중요 한 보안 업데이트가 있거나 유지 관리 기간에 패치를 완료 해야 하는 경우이 방법이 필요할 수 있습니다. 이 프로세스는 스토리지 공간 다이렉트 클러스터를 가져와서 패치 한 후 다시 설치 합니다. 절충은 호스트 된 리소스에 대 한 가동 중지 시간입니다.

1. 유지 관리 기간을 계획 합니다.
2. 가상 디스크를 오프 라인으로 전환 합니다.
3. 클러스터를 중지 하 여 저장소 풀을 오프 라인 상태로 전환 합니다. 클러스터 **중지** cmdlet을 실행 하거나 장애 조치(Failover) 클러스터 관리자를 사용 하 여 클러스터를 중지 합니다.
4. 각 노드의 services.msc에서 클러스터 서비스를 **사용 안 함으로** 설정 합니다. 이렇게 하면 패치가 적용 되는 동안 클러스터 서비스를 시작할 수 없습니다.
5. 모든 노드에 Windows Server 누적 업데이트 및 필요한 모든 서비스 스택 업데이트를 적용 합니다. 모든 노드를 동시에 업데이트할 수 있으며 클러스터가 다운 된 후에는 기다릴 필요가 없습니다.  
6. 노드를 다시 시작 하 고 모든 것이 양호한 지 확인 합니다.
7. 각 노드에서 클러스터 서비스를 다시 **자동** 으로 설정 합니다.
8. 클러스터를 시작 합니다. **시작-클러스터** cmdlet을 실행 하거나 장애 조치(Failover) 클러스터 관리자를 사용 합니다. 

   몇 분 정도 제공 합니다.  저장소 풀이 정상 상태 인지 확인 합니다.
9. 가상 디스크를 다시 온라인 상태로 전환 합니다.
10. **VirtualDisk** **cmdlet을 실행** 하 여 가상 디스크의 상태를 모니터링 합니다.


## <a name="see-also"></a>참고 항목

- [스토리지 공간 다이렉트 개요](storage-spaces-direct-overview.md)
- [CAU (클러스터 인식 업데이트)](https://technet.microsoft.com/library/hh831694.aspx)
