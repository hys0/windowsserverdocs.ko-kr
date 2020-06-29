---
title: 유지 관리를 위해 스토리지 공간 다이렉트 서버를 오프 라인 상태로 만들기
ms.prod: windows-server
ms.author: eldenc
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 10/08/2018
ms.assetid: 73dd8f9c-dcdb-4b25-8540-1d8707e9a148
ms.localizationpriority: medium
ms.openlocfilehash: a317f358c37f607475890efe773b57ee8efaeb14
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473480"
---
# <a name="taking-a-storage-spaces-direct-server-offline-for-maintenance"></a>유지 관리를 위해 스토리지 공간 다이렉트 서버를 오프 라인 상태로 만들기

> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 [스토리지 공간 다이렉트](storage-spaces-direct-overview.md)를 사용 하 여 서버를 다시 시작 하거나 종료 하는 방법에 대 한 지침을 제공 합니다

스토리지 공간 다이렉트를 사용 하는 경우 서버를 오프 라인으로 전환 하는 것은 클러스터의 모든 서버에서 공유 되는 저장소의 오프 라인 부분을 수행 하는 것을 의미 합니다. 이렇게 하려면 오프 라인으로 전환 하려는 서버를 일시 중지 (일시 중단) 하 고, 역할을 클러스터의 다른 서버로 이동 하 고, 유지 관리를 수행 하는 동안 데이터를 안전 하 게 유지 하 고 액세스할 수 있도록 클러스터의 다른 서버에서 모든 데이터를 사용할 수 있는지 확인 해야 합니다.

다음 절차를 사용 하 여 서버를 오프 라인으로 전환 하기 전에 스토리지 공간 다이렉트 클러스터에서 서버를 적절히 일시 중지 합니다.

   > [!IMPORTANT]
   > 스토리지 공간 다이렉트 클러스터에 업데이트를 설치 하려면이 항목의 절차를 자동으로 수행 하는 CAU (클러스터 인식 업데이트)를 사용 합니다. 이렇게 하면 업데이트를 설치할 때가 필요 하지 않습니다. 자세한 내용은 [CAU (클러스터 인식 업데이트)](https://technet.microsoft.com/library/hh831694.aspx)를 참조 하십시오.

## <a name="verifying-its-safe-to-take-the-server-offline"></a>서버를 오프 라인 상태로 전환 하는 것이 안전한 지 확인

유지 관리를 위해 서버를 오프 라인으로 전환 하기 전에 모든 볼륨이 정상 상태 인지 확인 합니다.

이렇게 하려면 관리자 권한으로 PowerShell 세션을 열고 다음 명령을 실행 하 여 볼륨 상태를 확인 합니다.

```PowerShell
Get-VirtualDisk
```

출력의 예는 다음과 같습니다.
```
FriendlyName ResiliencySettingName OperationalStatus HealthStatus IsManualAttach Size
------------ --------------------- ----------------- ------------ -------------- ----
MyVolume1    Mirror                OK                Healthy      True           1 TB
MyVolume2    Mirror                OK                Healthy      True           1 TB
MyVolume3    Mirror                OK                Healthy      True           1 TB
```

모든 볼륨 (가상 디스크)의 **HealthStatus** 속성이 **정상**상태 인지 확인 합니다.

장애 조치(Failover) 클러스터 관리자에서이 작업을 수행 하려면 **저장소**  >  **디스크**로 이동 합니다.

모든 볼륨 (가상 디스크)의 **상태** 열에 **온라인**이 표시 되는지 확인 합니다.

## <a name="pausing-and-draining-the-server"></a>서버 일시 중지 및 드레이닝

서버를 다시 시작 하거나 종료 하기 전에 가상 컴퓨터에서 실행 되는 가상 컴퓨터와 같은 모든 역할을 일시 중지 하 고 드레이닝 (이동) 합니다. 이를 스토리지 공간 다이렉트 통해 해당 서버에서 실행 중인 모든 응용 프로그램에 대해 종료가 투명 하 게 수행 되도록 데이터를 정상적으로 플러시 및 커밋할 수 있습니다.

   > [!IMPORTANT]
   > 클러스터 된 서버를 다시 시작 하거나 종료 하기 전에 항상 일시 중지 하 고 드레이닝 하세요.

PowerShell에서 관리자 권한으로 다음 cmdlet을 실행 하 여 일시 중지 하 고 드레이닝 합니다.

```PowerShell
Suspend-ClusterNode -Drain
```

장애 조치(Failover) 클러스터 관리자에서이 작업을 수행 **하려면 노드로 이동**하 여 노드를 마우스 오른쪽 단추로 클릭 한 다음 드레이닝 역할 **일시 중지**를 선택  >  **Drain Roles**합니다.

![일시 중지-드레이닝](media/maintain-servers/pause-drain.png)

모든 가상 머신은 클러스터의 다른 서버로 실시간 마이그레이션을 시작 합니다. 몇 분 정도 걸릴 수 있습니다.

   > [!NOTE]
   > 클러스터 노드를 일시 중지 하 고 드레이닝 하면 Windows에서 자동 안전 검사를 수행 하 여 계속 진행 하는 것이 안전한 지 확인 합니다. 비정상 상태인 볼륨이 있으면 중지 되 고 진행 하는 것이 안전 하지 않음을 알리는 경고 메시지가 표시 됩니다.

![안전-확인](media/maintain-servers/safety-check.png)

## <a name="shutting-down-the-server"></a>서버를 종료 하는 중

서버에서 드레이닝이 완료 되 면 장애 조치(Failover) 클러스터 관리자 및 PowerShell에서 **일시 중지** 됨으로 표시 됩니다.

![일시 중지됨](media/maintain-servers/paused.png)

이제 정상적으로 (예: 컴퓨터 다시 시작 또는 중지-컴퓨터 PowerShell cmdlet 사용)와 마찬가지로 안전 하 게 다시 시작 하거나 종료할 수 있습니다.

```PowerShell
Get-VirtualDisk

FriendlyName ResiliencySettingName OperationalStatus HealthStatus IsManualAttach Size
------------ --------------------- ----------------- ------------ -------------- ----
MyVolume1    Mirror                Incomplete        Warning      True           1 TB
MyVolume2    Mirror                Incomplete        Warning      True           1 TB
MyVolume3    Mirror                Incomplete        Warning      True           1 TB
```

노드가 종료 되거나 노드에서 클러스터 서비스를 시작/중지 하 고 문제가 발생 하지 않아야 하는 경우 불완전 하거나 저하 된 작업 상태가 정상입니다. 모든 볼륨이 온라인 상태를 유지 하 고 액세스할 수 있습니다.

## <a name="resuming-the-server"></a>서버 다시 시작

서버에서 작업 호스팅을 다시 시작할 준비가 되 면 다시 시작 합니다.

PowerShell에서 관리자 권한으로 다음 cmdlet을 실행 하 여를 다시 시작 합니다.

```PowerShell
Resume-ClusterNode
```

이 서버에서 이전에 실행 했던 역할을 다시 이동 하려면 선택적 **-장애 복구 (Failback** ) 플래그를 사용 합니다.

```PowerShell
Resume-ClusterNode –Failback Immediate
```

장애 조치(Failover) 클러스터 관리자에서이 작업을 수행 **하려면 노드로 이동**하 여 노드를 마우스 오른쪽 단추로 클릭 한 다음 **Resume**  >  **역할 장애 복구 다시**시작을 선택 합니다.

![다시 시작-장애 복구](media/maintain-servers/resume-failback.png)

## <a name="waiting-for-storage-to-resync"></a>저장소를 다시 동기화 하기를 기다리는 중

서버가 다시 시작 되 면 사용할 수 없는 상태에서 발생 한 모든 새 쓰기를 다시 동기화 해야 합니다. 이는 자동으로 수행 됩니다. 지능형 변경 내용 추적을 사용 하 여 *모든* 데이터를 검색 하거나 동기화 할 필요는 없습니다. 변경 내용만 이 프로세스는 프로덕션 워크 로드에 대 한 영향을 완화 하기 위해 제한 됩니다. 서버가 일시 중지 된 시간 및 작성 된 새 데이터 크기에 따라 완료 하는 데 몇 분 정도 걸릴 수 있습니다.

클러스터의 다른 서버를 오프 라인으로 전환 하기 전에 다시 동기화가 완료 될 때까지 기다려야 합니다.

PowerShell에서 관리자 권한으로 다음 cmdlet을 실행 하 여 진행률을 모니터링 합니다.

```PowerShell
Get-StorageJob
```
다음은 다시 동기화 (복구) 작업을 보여 주는 몇 가지 예제 출력입니다.
```
Name   IsBackgroundTask ElapsedTime JobState  PercentComplete BytesProcessed BytesTotal
----   ---------------- ----------- --------  --------------- -------------- ----------
Repair True             00:06:23    Running   65              11477975040    17448304640
Repair True             00:06:40    Running   66              15987900416    23890755584
Repair True             00:06:52    Running   68              20104802841    22104819713
```

**BytesTotal** 은 다시 동기화 해야 하는 저장소의 양을 보여 줍니다. **완료율** 은 진행률을 표시 합니다.

   > [!WARNING]
   > 이러한 복구 작업이 완료 될 때까지 다른 서버를 오프 라인 상태로 전환 하는 것은 안전 하지 않습니다.

이 시간 동안에는 볼륨이 정상 인 **경고**로 계속 표시 됩니다.

예를 들어 cmdlet을 사용 하는 경우 `Get-VirtualDisk` 다음 출력이 표시 될 수 있습니다.
```
FriendlyName ResiliencySettingName OperationalStatus HealthStatus IsManualAttach Size
------------ --------------------- ----------------- ------------ -------------- ----
MyVolume1    Mirror                InService         Warning      True           1 TB
MyVolume2    Mirror                InService         Warning      True           1 TB
MyVolume3    Mirror                InService         Warning      True           1 TB
```

작업이 완료 되 면 cmdlet을 사용 하 여 볼륨이 다시 **정상** 상태로 표시 되는지 확인 합니다 `Get-VirtualDisk` . 다음은 몇 가지 예제 출력입니다.

```
FriendlyName ResiliencySettingName OperationalStatus HealthStatus IsManualAttach Size
------------ --------------------- ----------------- ------------ -------------- ----
MyVolume1    Mirror                OK                Healthy      True           1 TB
MyVolume2    Mirror                OK                Healthy      True           1 TB
MyVolume3    Mirror                OK                Healthy      True           1 TB
```

이제 클러스터의 다른 서버를 일시 중지 하 고 다시 시작 하는 것이 안전 합니다.

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


## <a name="additional-references"></a>추가 참조

- [스토리지 공간 다이렉트 개요](storage-spaces-direct-overview.md)
- [CAU (클러스터 인식 업데이트)](https://technet.microsoft.com/library/hh831694.aspx)
