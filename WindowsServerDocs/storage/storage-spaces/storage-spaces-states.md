---
title: 저장소 공간 다이렉트 상태 및 작동 상태
description: 다른 상태와 저장소 공간 다이렉트 및 저장소 공간 (실제 디스크, 풀 및 가상 디스크 포함)의 작동 상태를 이해 하 고 찾을 방법 및 수행할 관련 작업 항목.
keywords: 저장소 공간을 분리 하 고, 가상 디스크, 실제 디스크 성능 저하
author: jasongerend
ms.author: jgerend
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage-spaces
manager: brianlic
ms.openlocfilehash: 5090a68270438bd9a06c7d50f9d4abca066d31e6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849144"
---
# <a name="troubleshoot-storage-spaces-direct-health-and-operational-states"></a>저장소 공간 다이렉트 상태 및 작동 상태 문제 해결

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server (반기 채널), Windows 10, Windows 8.1

이 항목에서는 상태 및 가상 디스크 (저장소 공간에 볼륨 아래 배치), 저장소 풀의 작동 상태 설명 하 고 드라이브 [저장소 공간 다이렉트](storage-spaces-direct-overview.md) 하 고 [저장소 공간](overview.md)입니다. 이러한 상태를 읽기 전용 구성으로 인해 가상 디스크를 삭제할 수 없는 이유 등 다양 한 문제를 해결 하려고 할 때 유용할 없습니다 수 있습니다. 도 (CannotPoolReason) 풀에 드라이브를 추가할 수 없습니다는 이유를 설명 합니다.

저장소 공간에 세 가지 기본 개체 *실제 디스크* (하드 드라이브에서 Ssd에 등)에 추가 되는 *저장소 풀*를 만들 수 있도록 저장소를 가상화 *가상디스크* 다음과 같이에서 풀에서 공간을 확보 합니다. 풀 메타 데이터는 풀의 각 드라이브에 기록 됩니다. 볼륨 가상 디스크를 기반으로 생성 되 고 파일을 저장 하 하지만 여기에 볼륨에 대 한 이야기를 다룰 필요가 없습니다.

![실제 디스크를 저장소 풀에 추가 되 고 가상 디스크에서 만든 풀 공간](media/storage-spaces-states/storage-spaces-object-model.png)

서버 관리자에서 또는 PowerShell을 사용 하 여 상태 및 작동 상태를 볼 수 있습니다. 다음은 다양 한 (대개 잘못 된) 상태 및 작동 상태는 클러스터 노드의 대부분 누락 된 저장소 공간 다이렉트 클러스터에서의 예 (추가할 열 머리글을 마우스 오른쪽 단추로 클릭 **작동 상태**). 이 클러스터를 만족 하지 않습니다.

![많은 누락 된 실제 디스크 및 비정상 상태의 가상 디스크를 저장소 공간 다이렉트 클러스터에서 누락 된 노드를 두 개 결과 표시 하는 서버 관리자](media/storage-spaces-states/unhealthy-disks-in-server-manager.png)

## <a name="storage-pool-states"></a>저장소 풀 상태

모든 저장소 풀에는 상태- **정상**하십시오 **경고**, 또는 **알 수 없는**/**비정상**도 하나 이상의 작동 상태입니다.

풀 상태를 확인 하려면 다음 PowerShell 명령을 사용 합니다.

```PowerShell
Get-StoragePool -IsPrimordial $False | Select-Object HealthStatus, OperationalStatus, ReadOnlyReason
```

읽기 전용 작업 상태를 사용 하 여 알 수 없는 상태에서 저장소 풀을 보여 주는 출력 예는 다음과 같습니다.

```
FriendlyName                OperationalStatus HealthStatus IsPrimordial IsReadOnly
------------                ----------------- ------------ ------------ ----------
S2D on StorageSpacesDirect1 Read-only         Unknown      False        True
```

다음 섹션에서는 상태 및 작동 상태를 나열합니다.

### <a name="pool-health-state-healthy"></a>풀 상태: 정상

|작동 상태    |설명|
|---------            |---------  |
|확인|저장소 풀에 정상입니다.|

### <a name="pool-health-state-warning"></a>풀 상태: 경고

저장소 풀에는 **경고** 상태 상태, 풀에 액세스할 수는 있지만 하나 이상의 드라이브 되지 않았거나 누락 된 것입니다. 결과적으로, 저장소 풀 복원 력을 저하 있을 수 있습니다.

|작동 상태    |설명|
|---------            |---------  |
|저하됨|저장소 풀에는 실패 했거나 누락 된 드라이브를 있습니다. 이 상태는 풀 메타 데이터를 호스트 하는 드라이브에만 발생 합니다. <br><br>**작업**: 드라이브의 상태를 확인 하 고 추가 실패 하기 전에 실패 한 모든 드라이브를 대체 합니다.|

### <a name="pool-health-state-unknown-or-unhealthy"></a>풀 상태: 알 수 없거나 비정상

저장소 풀에는 **알 수 없는** 또는 **비정상** 상태 상태, 저장소 풀은 읽기 전용 및 풀에 반환 될 때까지 수정할 수 없습니다는 의미는 **경고**나 **확인** 상태입니다.

|작동 상태    |읽기 전용 이유 |설명|
|---------            |---------       |--------   |
|읽기 전용|불완전 한|저장소 풀 끊어지는 경우 발생할 수 있습니다 해당 [쿼럼](understand-quorum.md), 즉,는 대부분의 풀에서 실패 한 드라이브나는 어떤 이유로 오프 라인 상태입니다. 풀의 쿼럼을 잃으면 저장소 공간 자동으로 풀 구성을 설정 읽기 전용으로 충분 한 드라이브를 다시 사용할 수 있게 될 때까지 합니다.<br><br>**작업:** <br>1. 누락 된 모든 드라이브를 다시 연결 하 고 저장소 공간 다이렉트를 사용 하는 경우에 모든 서버를 온라인 상태로 전환 합니다. <br>2. 관리자 권한으로 PowerShell 세션을 열고 다음 입력 하 여 읽기 전용으로 풀을 다시 설정:<br><br> <code>Get-StoragePool <PoolName> -IsPrimordial $False \| Set-StoragePool -IsReadOnly $false</code>|
||정책|관리자를 읽기 전용으로 저장소 풀을 설정 합니다.<br><br>**작업:** 읽기 / 쓰기 액세스 장애 조치 클러스터 관리자에서 클러스터 된 저장소 풀을 설정 하려면로 이동 **풀**풀을 마우스 오른쪽 단추로 클릭 하 고 선택한 **온라인**합니다.<br><br>다른 서버 및 Pc에 대 한 관리자 권한으로 PowerShell 세션을 열고 입력:<br><br><code>Get-StoragePool <PoolName> \| Set-StoragePool -IsReadOnly $false</code><br><br> |
||시작 중|저장소 공간 시작 되었거나 풀에 연결 되어 드라이브 대기 중입니다. 이 일시적인 상태 여야 합니다. 완전히 시작 되 면 풀을 다른 운영 상태로 전환 해야 합니다.<br><br>**작업:** 풀에서 유지 되는 경우는 *시작* 상태, 풀의 모든 드라이브가 제대로 연결 되어 있는지 확인 합니다.|

참고 항목 [읽기 전용 구성을 포함 하는 저장소 풀 수정](https://social.technet.microsoft.com/wiki/contents/articles/14861.modifying-a-storage-pool-that-has-a-read-only-configuration.aspx)합니다.

## <a name="virtual-disk-states"></a>가상 디스크 상태

저장소 공간에 볼륨 공간 풀에서 분리 되는 가상 디스크 (저장소 공간)에 배치 됩니다. 모든 가상 디스크에 상태- **정상**를 **경고**를 **Unhealthy**, 또는 **알 수 없는** 뿐만 아니라 하나 이상의 작동 상태입니다.

에 있는 가상 디스크 상태를 확인 하려면 다음 PowerShell 명령을 사용 합니다.

```PowerShell
Get-VirtualDisk | Select-Object FriendlyName,HealthStatus, OperationalStatus, DetachedReason
```

분리 된 가상 디스크 및 성능 저하/불완전 한 가상 디스크를 보여 주는 출력의 예는 다음과 같습니다.

```
FriendlyName HealthStatus OperationalStatus      DetachedReason
------------ ------------ -----------------      --------------
Volume1      Unknown      Detached               By Policy
Volume2      Warning      {Degraded, Incomplete} None
```

다음 섹션에서는 상태 및 작동 상태를 나열합니다.

### <a name="virtual-disk-health-state-healthy"></a>가상 디스크 상태: 정상

|작동 상태    |설명|
|---------            |---------          |
|확인    |가상 디스크 정상입니다.|
|최적이 아닌    |데이터는 드라이브에 걸쳐 균등 하 게 기록 되지 않습니다. <br><br>**작업**: 실행 하 여 저장소 풀에 대 한 드라이브 사용량을 최적화 합니다 [Optimize-storagepool](https://technet.microsoft.com/itpro/powershell/windows/storage/optimize-storagepool) cmdlet.|

### <a name="virtual-disk-health-state-warning"></a>가상 디스크 상태: 경고

가상 디스크에는 **경고** 상태 상태 이면 하나 이상의 데이터 복사본을 사용할 수 있습니다. 하지만 저장소 공간에는 하나 이상의 데이터 복사본 여전히 읽을 수는 것입니다.

|작동 상태    |설명|
|---------            |---------          |
|서비스에서            |Windows는 추가 하거나 드라이브를 제거한 후 같은 가상 디스크를 복구 합니다. 복구가 완료 되 면 가상 디스크가 정상 상태를 반환 해야 합니다.|
|불완전 한           |하나 이상의 드라이브 되지 않았거나 누락 된 때문에 가상 디스크의 복원 력을 줄어듭니다. 그러나 누락 된 드라이브는 데이터의 최신 복사본을 포함합니다.<br><br> **작업**: <br>1. 누락 된 드라이브에 다시 연결 하 고, 실패 한 모든 드라이브를 바꾸고, 저장소 공간 다이렉트를 사용 하는 경우 오프 라인 상태인 서버 온라인입니다. <br>2. 저장소 공간 다이렉트 사용 하지 않는, 다음 복구 된 가상 디스크를 사용 하 여 [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) cmdlet.<br> 저장소 공간 다이렉트 자동으로 시작 복구를 다시 연결 하거나 드라이브를 대체 한 후 필요한 경우.|
|저하됨             |하나 이상의 드라이브 되지 않았거나 누락 된 이러한 드라이브에서 데이터의 오래 된 복사본이 있으므로 가상 디스크의 복원 력을 줄어듭니다. <br><br>**작업**: <br> 1. 누락 된 드라이브에 다시 연결 하 고, 실패 한 모든 드라이브를 바꾸고, 저장소 공간 다이렉트를 사용 하는 경우 오프 라인 상태인 서버 온라인입니다. <br> 2. 저장소 공간 다이렉트 사용 하지 않는, 다음 복구 된 가상 디스크를 사용 하 여 [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) cmdlet. <br>저장소 공간 다이렉트 자동으로 시작 복구를 다시 연결 하거나 드라이브를 대체 한 후 필요한 경우.|

### <a name="virtual-disk-health-state-unhealthy"></a>가상 디스크 상태: Unhealthy

가상 디스크에는 **비정상** 상태, 일부 또는 모든 가상 디스크의 데이터를 현재 액세스할 수 없는 합니다.

|작동 상태    |설명|
|---------            |--------   |
|중복 되지 않은|가상 디스크 드라이브가 너무 많아서 하지 못하여 데이터가 손실 되었습니다.<br><br>**작업**: 실패 한 드라이브를 바꾼 다음 백업에서 데이터를 복원 합니다.|

### <a name="virtual-disk-health-state-informationunknown"></a>가상 디스크 상태: 정보/알 수 없음

가상 디스크에 있을 수도 있습니다는 **정보** 상태 (처럼 저장소 공간 제어판 항목) 또는 **알 수 없는** 상태 상태와 같이 PowerShell에서 관리자가 가상 디스크를 수행한 경우 오프 라인 또는 가상 디스크에 분리 됩니다.

|작동 상태    |분리 된 이유 |설명|
|---------            |---------       |--------   |
|Detached             |정책에 의해            |Windows 다시 시작 될 때마다 가상 디스크를 수동으로 연결 해야 하는 경우, 관리자가 가상 디스크를 오프 라인으로 수행 하거나 수동 첨부 파일을 요구 하도록 가상 디스크를 설정 합니다.,<br><br>**작업**: 가상 디스크를 다시 온라인 상태로 전환 합니다. 이렇게 하려면 가상 디스크를 클러스터 된 저장소 풀의 경우 장애 조치 클러스터 관리자에서 선택 **스토리지** > **풀** > **가상 디스크** 를 보여 주는 가상 디스크를 선택 합니다 **오프 라인** 상태 및 선택 **온라인**합니다. <br><br>클러스터에 없는 경우 가상 디스크를 다시 온라인 상태로 만드는, 관리자 권한으로 PowerShell 세션을 열고 추가한 후 다음 명령을 사용 하 여:<br><br> <code>Get-VirtualDisk \| Where-Object -Filter { $_.OperationalStatus -eq "Detached" } \| Connect-VirtualDisk</code><br><br>Windows 다시 시작 된 후에 자동으로 모든 클러스터 되지 않은 가상 디스크를 연결, 관리자 권한으로 PowerShell 세션을 열고 명령을 사용 하 여 합니다.<br><br> <code>Get-VirtualDisk \| Set-VirtualDisk -ismanualattach $false</code>|
|            |비정상 대부분 디스크 |이 가상 디스크에서 사용 하는 너무 많은 드라이브 실패, 없는 경우 또는 오래 된 데이터가 있는 합니다.   <br><br>**작업**: <br> 1. 누락 된 모든 드라이브를 다시 연결 하 고 저장소 공간 다이렉트를 사용 하는 경우 오프 라인 상태인 서버 온라인입니다. <br> 2. 모든 드라이브 및 서버가 온라인 상태가 된 후 실패 한 모든 드라이브를 대체 합니다. 참조 [Health Service](../../failover-clustering/health-service-overview.md) 세부 정보에 대 한 합니다. <br>저장소 공간 다이렉트 자동으로 시작 복구를 다시 연결 하거나 드라이브를 대체 한 후 필요한 경우.<br>3. 저장소 공간 다이렉트 사용 하지 않는, 다음 복구 된 가상 디스크를 사용 하 여 [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) cmdlet.  <br><br>더 많은 디스크 데이터의 복사본이 있고 가상 디스크에 중간 오류가 복구 되지 않은 보다 실패 한 경우 가상 디스크에 있는 모든 데이터가 영구적으로 손실 됩니다. 부적절 한 여기서는 가상 디스크를 삭제 하 고 새 가상 디스크를 만들고 백업에서 복원.|
|                     |불완전 한 |드라이브가 부족 가상 디스크를 읽을 수 있습니다.    <br><br>**작업**: <br> 1. 누락 된 모든 드라이브를 다시 연결 하 고 저장소 공간 다이렉트를 사용 하는 경우 오프 라인 상태인 서버 온라인입니다. <br> 2. 모든 드라이브 및 서버가 온라인 상태가 된 후 실패 한 모든 드라이브를 대체 합니다. 참조 [Health Service](../../failover-clustering/health-service-overview.md) 세부 정보에 대 한 합니다. <br>저장소 공간 다이렉트 자동으로 시작 복구를 다시 연결 하거나 드라이브를 대체 한 후 필요한 경우.<br>3. 저장소 공간 다이렉트 사용 하지 않는, 다음 복구 된 가상 디스크를 사용 하 여 [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) cmdlet.<br><br>더 많은 디스크 데이터의 복사본이 있고 가상 디스크에 중간 오류가 복구 되지 않은 보다 실패 한 경우 가상 디스크에 있는 모든 데이터가 영구적으로 손실 됩니다. 부적절 한 여기서는 가상 디스크를 삭제 하 고 새 가상 디스크를 만들고 백업에서 복원.|
| |시간 제한|너무 길어서 가상 디스크를 연결 합니다. <br><br> **작업:** 이 발생 해서는 안 됩니다 종종 시간에서 조건을 통과 하는 경우 참조를 볼 수 있습니다. 사용 하 여 가상 디스크를 연결 해제를 시도할 수 있습니다 합니다 [Disconnect-virtualdisk](https://docs.microsoft.com/powershell/module/storage/disconnect-virtualdisk?view=win10-ps) cmdlet을 사용 하는 [Connect-virtualdisk](https://docs.microsoft.com/powershell/module/storage/connect-virtualdisk?view=win10-ps) cmdlet을 다시 연결 합니다. |

## <a name="drive-physical-disk-states"></a>(실제 디스크) 드라이브 상태

다음 섹션에서는 상태 드라이브에 있을 수 있습니다. 풀의 드라이브도 PowerShell에 표시 됩니다 *실제 디스크* 개체입니다.

### <a name="drive-health-state-healthy"></a>드라이브 상태: 정상

|작동 상태    |설명|
|---------            |---------          |
|확인|드라이브 정상입니다.|
|서비스에서|드라이브는 몇 가지 내부 하우스키핑 작업을 수행 합니다. 작업이 완료 되 면 드라이브를 반환 해야 합니다 *확인* 상태입니다.|

### <a name="drive-health-state-warning"></a>드라이브 상태: 경고

경고 상태 있습니다 드라이브 읽기 및 데이터를 성공적으로 작성 되었지만 문제.

|작동 상태    |설명|
|---------            |---------          |
|통신 끊김된|드라이브가 없습니다. 저장소 공간 다이렉트를 사용 중인 경우 서버가 다운 된 때문일 수 있습니다.<br><br>**작업**: 저장소 공간 다이렉트를 사용 하는 경우에 모든 서버를 다시 온라인 상태로 전환 합니다. 해결 하지 않습니다 하는 경우 드라이브를 다시 연결, 대체 또는 Windows 오류 보고를 사용 하 여 문제 해결 단계를 수행 하 여이 드라이브에 대 한 자세한 진단 정보를 가져오는 시도 > [실제 디스크 시간이 초과 되었습니다.](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-timed-out)합니다.|
|풀에서 제거|저장소 공간은 저장소 풀에서 드라이브를 분리 하는 중입니다. <br><br> 이 임시 상태입니다. 제거가 완료 되 면 드라이브 아직 시스템에 연결 하는 경우 드라이브 다른 운영 상태로 전환 (일반적으로 확인) 원시 풀에 있습니다.|
|유지 관리 모드 시작|저장소 공간은 관리자가 드라이브를 유지 관리 모드로 전환 후 드라이브를 유지 관리 모드로 설정 하는 중입니다. 이 임시 상태-드라이브에 곧 있어야 합니다 *유지 관리 모드로* 상태.|
|유지 관리 모드|중지를 읽고 쓰는 드라이브에서 유지 관리 모드에서 드라이브를 배치 하는 관리자입니다. 드라이브 펌웨어를 업데이트 하기 전에 또는 실패를 테스트 하는 경우 일반적으로 수행 됩니다.<br><br>**작업**: 유지 관리 모드에서 드라이브를 사용 하려면 사용 합니다 [사용 안 함-StorageMaintenanceMode](https://technet.microsoft.com/itpro/powershell/windows/storage/disable-storagemaintenancemode) cmdlet.|
|유지 관리 모드 중지|저장소 공간 드라이브를 다시 온라인 상태로 전환 중임를 관리자로 유지 관리 모드에서 드라이브를 했습니다. 이 임시 상태-드라이브 곧 상태에 있어야 다른-이상적 *정상*합니다.|
|자동 완성 오류|드라이브 실패 가깝다는 것을 보고 합니다.<br><br>**작업**: 드라이브를 대체 합니다.|
|IO 오류|드라이브에 액세스 하는 일시적인 오류가 발생 했습니다.<br><br>**작업**: <br>1. 드라이브를 다시 전환 하지 하는 경우는 **확인** 상태를 사용 하 여 할 수는 [Reset-physicaldisk](https://docs.microsoft.com/powershell/module/storage/reset-physicaldisk) 드라이브를 초기화 하는 cmdlet입니다. <br> 2. 사용 하 여 [Repair-virtualdisk](https://docs.microsoft.com/powershell/module/storage/repair-virtualdisk) 영향을 받는 가상 디스크의 복원 력을 복원 합니다. <br>3. 이 계속 발생 하는 경우에 드라이브를 교체 합니다.|
|일시적인 오류|드라이브에서 일시적 오류가 발생이 했습니다. 이 문제는 일반적으로 드라이브 응답 했지만 것일 수도 있는 보호 파티션에 드라이브에서 부적절 하 게 제거 된 저장소 공간을 의미 합니다. <br><br>**작업**: <br>1. 드라이브를 다시 전환 하지 하는 경우는 **확인** 상태를 사용 하 여 할 수는 [Reset-physicaldisk](https://docs.microsoft.com/powershell/module/storage/reset-physicaldisk) 드라이브를 초기화 하는 cmdlet입니다. <br> 2. 사용 하 여 [Repair-virtualdisk](https://docs.microsoft.com/powershell/module/storage/repair-virtualdisk) 영향을 받는 가상 디스크의 복원 력을 복원 합니다. <br>3. 이 계속 발생 하는 경우 드라이브를 바꾸거나 Windows 오류 보고를 사용 하 여 문제 해결 단계를 수행 하 여이 드라이브에 대 한 자세한 진단 정보를 가져오는 시도 > [실제 디스크를 온라인 상태로 만들지](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-failed-to-come-online)합니다.|
|비정상적인 대기 시간|드라이브는 상태 서비스 저장소 공간 다이렉트에서 측정 된 대로 느리게 수행 합니다.<br><br>**작업**: 이 계속 발생 하는 경우 전체 저장소 공간의 성능을 줄이지 않으므로 하므로 드라이브를 대체 합니다.

### <a name="drive-health-state-unhealthy"></a>드라이브 상태: Unhealthy

비정상 상태의 드라이브에 기록 하거나 현재 액세스할 수 없습니다.

|작동 상태    |설명|
|---------            |---------          |
|사용할 수 없음|이 드라이브는 저장소 공간에서 사용할 수 없습니다. 자세한 내용은 참조 하세요. [저장소 공간 다이렉트 하드웨어 요구 사항](storage-spaces-direct-hardware-requirements.md)하는 경우 저장소 공간 다이렉트를 사용 하지 않는; 참조 [저장소 공간 개요](https://technet.microsoft.com/library/hh831739(v=ws.11).aspx#Requirements)합니다.|
|분할|드라이브를 풀에서 분리 했습니다.<br><br>**작업**: 드라이브에서 모든 데이터를 제거 하 고 빈 드라이브로 풀에 다시 추가 드라이브를 다시 설정 합니다. 그렇게 하려면 실행 관리자 권한으로 PowerShell 세션을 엽니다는 [Reset-physicaldisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk) cmdlet을 실행 한 다음 [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk). <br><br>이 드라이브에 대 한 자세한 진단 정보를 가져오려는 Windows 오류 보고를 사용 하 여 문제 해결 단계에 따라 > [실제 디스크를 온라인 상태로 만들지](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-failed-to-come-online)합니다.|
|오래 된 메타 데이터|저장소 공간 드라이브에 이전 메타 데이터를 찾았습니다.<br><br>**작업**: 이 일시적인 상태 여야 합니다. 드라이브를 확인으로 다시 전환 하지 않습니다, 경우 실행할 수 있습니다 [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) 영향을 받는 가상 디스크에서 복구 작업을 시작 합니다. 이 문제를 해결 하지 않습니다 하는 경우 다시 설정할 수 있습니다 사용 하 여 드라이브를 [Reset-physicaldisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk) cmdlet을 실행 한 다음 확인 하 고 드라이브에서 모든 데이터를 초기화 [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)합니다.|
|인식할 수 없는 메타 데이터|저장소 공간 드라이브에 다른 풀에서 메타 데이터에는 일반적으로 의미 있는 드라이브에서 인식할 수 없는 메타 데이터를 찾았습니다.<br><br>**작업**: 드라이브를 초기화 하 고 현재 풀에 추가할 드라이브를 다시 설정 합니다. 드라이브를 다시 설정 하려면 실행 관리자 권한으로 PowerShell 세션을 엽니다는 [Reset-physicaldisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk) cmdlet을 실행 한 다음 [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)합니다.|
|실패 한 미디어|드라이브 하지 못했으며 저장소 공간에서 더 이상 사용 되지 않습니다.<br><br>**작업**: 드라이브를 대체 합니다. <br><br>이 드라이브에 대 한 자세한 진단 정보를 가져오려는 Windows 오류 보고를 사용 하 여 문제 해결 단계에 따라 > [실제 디스크를 온라인 상태로 만들지](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-failed-to-come-online)합니다.|
|장치 하드웨어 오류|이 드라이브에 하드웨어 오류가 있습니다. <br><br>**작업**: 드라이브를 대체 합니다.|
|펌웨어 업데이트|Windows는 드라이브의 펌웨어를 업데이트 하 고 있습니다. 일반적으로 지속 되는 1 분 미만 동안 풀에서 다른 드라이브에서 모든 백업을 처리할 시간 읽기 및 쓰기 및 임시 상태입니다. 자세한 내용은 참조 하세요. [드라이브 펌웨어 업데이트](../update-firmware.md)합니다.|
|시작 중|드라이브를 작업에 대 한 준비를 하 고 있습니다. 이 드라이브는 다른 운영 상태로 전환 되어야 완료 되 면 임시 상태-이어야 합니다.|

## <a name="reasons-a-drive-cant-be-pooled"></a>드라이브를 풀링할 수 없는 이유

방금 일부 드라이브를 저장소 풀에 포함 되도록 준비 되지 않았습니다. 확인할 수 있습니다 드라이브를 확인 하 여 풀링을 사용할 수 없는 이유는 `CannotPoolReason` 실제 디스크의 속성입니다. CannotPoolReason 속성을 표시 하는 PowerShell 스크립트 예제는 다음과 같습니다.

```PowerShell
Get-PhysicalDisk | Format-Table FriendlyName,MediaType,Size,CanPool,CannotPoolReason
```

출력 예는 다음과 같습니다.

```
FriendlyName          MediaType          Size CanPool CannotPoolReason
------------          ---------          ---- ------- ----------------
ATA MZ7LM120HCFD00D3  SSD        120034123776   False Insufficient Capacity
Msft Virtual Disk     SSD         10737418240    True
Generic Physical Disk SSD        119990648832   False In a Pool
```

다음 표에서 각 이유 때문에 좀 더 자세히를 제공합니다.

|이유|설명|
|---|---|
|풀의|드라이브를 저장소 풀에 이미 속해 있습니다. <br><br>드라이브는 단일 저장소 풀만 한 번에 속할 수 있습니다. 다른 저장소 풀에서이 드라이브를 사용 하려면 먼저 저장소 공간 풀에서 다른 드라이브에는 드라이브에 데이터를 이동 하는 해당 기존 풀에서 드라이브를 제거 합니다. 또는 드라이브가 저장소 공간에 게 알리지 않고 해당 풀에서 연결이 하는 경우에 드라이브를 다시 설정 합니다. <br><br>제거할 안전 하 게 드라이브를 저장소 풀에서 사용 하 여 [Remove-physicaldisk](https://technet.microsoft.com/itpro/powershell/windows/storage/remove-physicaldisk), 또는 서버 관리자 > **File and Storage Services** > **저장소 풀**, > **실제 디스크가**드라이브를 마우스 오른쪽 단추로 클릭 하 고 선택한 **디스크 제거**합니다.<br><br>드라이브를 다시 설정 하려면 사용 하 여 [Reset-physicaldisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk)합니다.|
|비정상입니다.|드라이브 정상 상태가 아니며 교체 해야 할 수 있습니다.|
|이동식 미디어|드라이브를 이동식 드라이브로 분류 됩니다. <br><br>저장소 공간으로 인식 되는 Windows에서 Blu-ray 드라이브와 같은 이동식 미디어를 지원 하지 않습니다. 있지만 여러 고정 드라이브는 이동식 슬롯에 일반적으로 되는 미디어 *분류* 이동식으로 Windows에서 저장소 공간 사용에 적합 하지 합니다.|
|클러스터에서 사용|드라이브는 현재 장애 조치 클러스터에서 사용 됩니다.|
|오프라인|드라이브가 오프 라인입니다. <br><br>읽기/쓰기로 집합과 모든 오프 라인 드라이브가 온라인 상태로 하려면 관리자 권한으로 PowerShell 세션을 열고 다음 스크립트를 사용 하 여:<br><br><code>Get-Disk \| Where-Object -Property OperationalStatus -EQ "Offline" \| Set-Disk -IsOffline $false</code><br><br><code>Get-Disk \| Where-Object -Property IsReadOnly -EQ $true \| Set-Disk -IsReadOnly $false</code>|
|용량이 부족|이 문제는 일반적으로 분할이 드라이브의 여유 공간을 차지 하는 경우 발생 합니다. <br><br>**작업**: 드라이브의 모든 데이터 지우기 드라이브에서 볼륨을 삭제 합니다. 작업을 수행 하는 한 가지 방법은 사용 하는 것은 [Clear-disk](https://docs.microsoft.com/powershell/module/storage/clear-disk?view=win10-ps) PowerShell cmdlet.|
|확인 중|합니다 [Health Service](../../failover-clustering/health-service-overview.md#supported-components-document) 확인 하는 경우 드라이브 또는 드라이브의 펌웨어를 사용이 승인 서버 관리자는 합니다.|
|확인 하지 못했습니다.|합니다 [Health Service](../../failover-clustering/health-service-overview.md#supported-components-document) 경우 드라이브 또는 드라이브의 펌웨어 승인을 사용 하 여 서버 관리자를 확인 하지 못했습니다.|
|펌웨어 규격이 아닙니다.|실제 드라이브의 펌웨어를 사용 하 여 서버 관리자가 지정 하는 승인 된 펌웨어 수정 버전의 목록에 없는 합니다 [Health Service](../../failover-clustering/health-service-overview.md#supported-components-document)합니다. |
|하드웨어 규격이 아닙니다.|드라이브를 사용 하 여 서버 관리자에 의해 지정 된 승인 된 저장소 모델의 목록에 없는 합니다 [Health Service](../../failover-clustering/health-service-overview.md#supported-components-document)합니다.|

## <a name="see-also"></a>참조

- [저장소 공간 다이렉트](storage-spaces-direct-overview.md)
- [저장소 공간 다이렉트 하드웨어 요구 사항](storage-spaces-direct-hardware-requirements.md)
- [클러스터 및 풀 쿼럼을 이해](understand-quorum.md)