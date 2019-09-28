---
title: 상태 및 작동 상태 스토리지 공간 다이렉트
description: 스토리지 공간 다이렉트 및 저장소 공간의 다양 한 상태 및 작동 상태 (실제 디스크, 풀 및 가상 디스크 포함)와 그에 대 한 작업 상태를 찾고 이해 하는 방법입니다.
keywords: 저장소 공간, 분리 됨, 가상 디스크, 실제 디스크, 성능 저하 됨
author: jasongerend
ms.author: jgerend
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server
ms.technology: storage-spaces
manager: brianlic
ms.openlocfilehash: 4b525555333a8aeee416e9ab55981c17137a52ea
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365991"
---
# <a name="troubleshoot-storage-spaces-direct-health-and-operational-states"></a>상태 및 작동 상태 스토리지 공간 다이렉트 문제 해결

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server (반기 채널), Windows 10, Windows 8.1

이 항목에서는 저장소 풀의 상태 및 작동 상태, 저장소 공간의 볼륨 아래에 있는 가상 디스크, [스토리지 공간 다이렉트](storage-spaces-direct-overview.md) 및 [저장소 공간의](overview.md)드라이브에 대해 설명 합니다. 이러한 상태는 읽기 전용 구성으로 인해 가상 디스크를 삭제할 수 없는 이유와 같은 다양 한 문제를 해결 하려는 경우에 유용 합니다. 풀에 드라이브를 추가할 수 없는 이유 (CannotPoolReason)도 설명 합니다.

저장소 공간에는 저장소 *풀*에 추가 된 *실제 디스크* (하드 드라이브, ssd 등)의 세 가지 주 개체가 있습니다. 저장소를 가상화 하 여 저장소를 가상화 하 고 여기에 표시 된 것 처럼 풀의 여유 공간에서 *가상 디스크* 를 만들 수 있습니다. 풀 메타 데이터는 풀의 각 드라이브에 기록 됩니다. 볼륨은 가상 디스크를 기반으로 생성 되 고 파일을 저장 하지만 볼륨에 대해 설명 하지는 않습니다.

![실제 디스크는 저장소 풀에 추가 된 다음, 풀 공간에서 만든 가상 디스크에 추가 됩니다.](media/storage-spaces-states/storage-spaces-object-model.png)

서버 관리자 또는 PowerShell을 사용 하 여 상태 및 작동 상태를 볼 수 있습니다. 다음은 대부분의 클러스터 노드가 누락 된 스토리지 공간 다이렉트 클러스터에 대 한 다양 한 상태 및 작동 상태의 예입니다 ( **작업 상태**를 추가 하려면 열 머리글을 마우스 오른쪽 단추로 클릭). 이는 만족 스럽게 클러스터가 아닙니다.

![스토리지 공간 다이렉트 클러스터에 누락 된 노드 두 개 (비정상 상태의 실제 디스크 및 가상 디스크가 많은 경우)의 결과를 표시 서버 관리자](media/storage-spaces-states/unhealthy-disks-in-server-manager.png)

## <a name="storage-pool-states"></a>저장소 풀 상태

모든 저장소 풀에는 상태 **정상**, **경고**또는 **알 수 없음**/**비정상**및 하나 이상의 작동 상태가 있습니다.

풀이 있는 상태를 확인 하려면 다음 PowerShell 명령을 사용 합니다.

```PowerShell
Get-StoragePool -IsPrimordial $False | Select-Object HealthStatus, OperationalStatus, ReadOnlyReason
```

다음은 읽기 전용 작동 상태를 사용 하 여 알 수 없는 상태의 저장소 풀을 보여 주는 예제 출력입니다.

```
FriendlyName                OperationalStatus HealthStatus IsPrimordial IsReadOnly
------------                ----------------- ------------ ------------ ----------
S2D on StorageSpacesDirect1 Read-only         Unknown      False        True
```

다음 섹션에서는 상태 및 작동 상태를 나열 합니다.

### <a name="pool-health-state-healthy"></a>풀 상태: 정상

|작동 상태    |설명|
|---------            |---------  |
|확인|저장소 풀이 정상입니다.|

### <a name="pool-health-state-warning"></a>풀 상태: Warning

저장소 풀이 **경고** 상태에 있으면 풀에 액세스할 수 있지만 하나 이상의 드라이브가 실패 했거나 누락 되었음을 나타냅니다. 따라서 저장소 풀의 복원 력이 줄어들 수 있습니다.

|작동 상태    |설명|
|---------            |---------  |
|저하됨|저장소 풀에 오류가 있거나 누락 된 드라이브가 있습니다. 이 상태는 풀 메타 데이터를 호스팅하는 드라이브에만 발생 합니다. <br><br>**작업**: 추가 오류가 발생 하기 전에 드라이브의 상태를 확인 하 고 실패 한 드라이브를 바꿉니다.|

### <a name="pool-health-state-unknown-or-unhealthy"></a>풀 상태: 알 수 없음 또는 비정상

저장소 풀이 **알 수** 없거나 **비정상** 상태 이면 저장소 풀이 읽기 전용 이며 풀이 **경고** 또는 **확인** 상태에 반환 될 때까지 수정할 수 없습니다.

|작동 상태    |읽기 전용 이유 |설명|
|---------            |---------       |--------   |
|읽기 전용|안함|이는 저장소 풀이 [쿼럼을](understand-quorum.md)손실 하는 경우 발생할 수 있습니다. 즉, 풀의 대부분의 드라이브가 어떤 이유로 인해 실패 했거나 오프 라인 상태임을 의미 합니다. 풀이 쿼럼을 손실 하면 충분 한 드라이브를 다시 사용할 수 있을 때까지 저장소 공간이 자동으로 풀 구성을 읽기 전용으로 설정 합니다.<br><br>**조치** <br>1. 누락 된 드라이브를 다시 연결 하 고 스토리지 공간 다이렉트를 사용 하는 경우 모든 서버를 온라인 상태로 전환 합니다. <br>2. 관리자 권한으로 PowerShell 세션을 열고 다음을 입력 하 여 풀을 읽기/쓰기로 다시 설정 합니다.<br><br> <code> @ no__t-1 @no__t -IsPrimordial $False \| Set-StoragePool -IsReadOnly $false @ no__t-4|
||정책|관리자가 저장소 풀을 읽기 전용으로 설정 합니다.<br><br>**조치** 장애 조치(Failover) 클러스터 관리자에서 클러스터 된 저장소 풀을 읽기/쓰기 액세스로 설정 하려면 **풀로 이동**하 고 풀을 마우스 오른쪽 단추로 클릭 한 다음 **온라인 상태로 만들기**를 선택 합니다.<br><br>다른 서버 및 Pc의 경우 관리자 권한으로 PowerShell 세션을 열고 다음을 입력 합니다.<br><br><code> @ no__t-1 @no__t \| Set-StoragePool -IsReadOnly $false @ no__t-4<br><br> |
||시작 중|저장소 공간이 풀에서 연결 될 드라이브를 시작 하거나 대기 하는 중입니다. 이는 임시 상태 여야 합니다. 완전히 시작한 후에는 풀이 다른 작동 상태로 전환 되어야 합니다.<br><br>**조치** 풀이 *시작* 상태를 유지 하는 경우 풀의 모든 드라이브가 제대로 연결 되어 있는지 확인 합니다.|

또한 [읽기 전용 구성이 있는 저장소 풀 수정을](https://social.technet.microsoft.com/wiki/contents/articles/14861.modifying-a-storage-pool-that-has-a-read-only-configuration.aspx)참조 하세요.

## <a name="virtual-disk-states"></a>가상 디스크 상태

저장소 공간에서 볼륨은 풀에서 사용 가능한 공간이 공백을 만들 가상 디스크 (저장소 공간)에 배치 됩니다. 모든 가상 디스크에는 상태 **정상**, **경고**, **비정상**또는 **알 수** 는 물론 하나 이상의 작동 상태도 있습니다.

가상 디스크가 있는 상태를 확인 하려면 다음 PowerShell 명령을 사용 합니다.

```PowerShell
Get-VirtualDisk | Select-Object FriendlyName,HealthStatus, OperationalStatus, DetachedReason
```

다음은 분리 된 가상 디스크 및 성능이 저하 되거나 불완전 한 가상 디스크를 보여 주는 출력의 예입니다.

```
FriendlyName HealthStatus OperationalStatus      DetachedReason
------------ ------------ -----------------      --------------
Volume1      Unknown      Detached               By Policy
Volume2      Warning      {Degraded, Incomplete} None
```

다음 섹션에서는 상태 및 작동 상태를 나열 합니다.

### <a name="virtual-disk-health-state-healthy"></a>가상 디스크 상태: 정상

|작동 상태    |설명|
|---------            |---------          |
|확인    |가상 디스크가 정상입니다.|
|최적이 아닌    |데이터는 드라이브 간에 균등 하 게 기록 되지 않습니다. <br><br>**작업**: 저장소 풀의 드라이브 사용 [을 최적화 합니다](https://technet.microsoft.com/itpro/powershell/windows/storage/optimize-storagepool) .|

### <a name="virtual-disk-health-state-warning"></a>가상 디스크 상태: Warning

가상 디스크가 **경고** 상태에 있는 경우 하나 이상의 데이터 복사본을 사용할 수 없지만 저장소 공간에서 하나 이상의 데이터 복사본을 계속 읽을 수 있습니다.

|작동 상태    |설명|
|---------            |---------          |
|서비스에서            |Windows에서 드라이브를 추가 하거나 제거 하는 등의 방법으로 가상 디스크를 복구 하 고 있습니다. 복구가 완료 되 면 가상 디스크가 정상 상태를 반환 해야 합니다.|
|안함           |하나 이상의 드라이브가 실패 했거나 누락 되어 서 가상 디스크의 복원 력을 줄였습니다. 그러나 누락 된 드라이브는 데이터의 최신 복사본을 포함 합니다.<br><br> **작업**: <br>1. 누락 된 드라이브를 다시 연결 하 고, 오류가 발생 한 드라이브를 바꾸고, 스토리지 공간 다이렉트을 사용 하는 경우 오프 라인 상태인 모든 서버를 온라인 상태로 전환 합니다. <br>2. 스토리지 공간 다이렉트 사용 하 고 있지 않은 경우 다음에 [VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) cmdlet을 사용 하 여 가상 디스크를 복구 합니다.<br> 스토리지 공간 다이렉트는 드라이브를 다시 연결 하거나 교체 하 고 나 서 필요한 경우 자동으로 복구를 시작 합니다.|
|저하됨             |하나 이상의 드라이브가 실패 하거나 누락 되었으므로 가상 디스크의 복원 력이 줄어들고,이 드라이브에 오래 된 데이터 복사본이 있습니다. <br><br>**작업**: <br> 1. 누락 된 드라이브를 다시 연결 하 고, 오류가 발생 한 드라이브를 바꾸고, 스토리지 공간 다이렉트을 사용 하는 경우 오프 라인 상태인 모든 서버를 온라인 상태로 전환 합니다. <br> 2. 스토리지 공간 다이렉트 사용 하 고 있지 않은 경우 다음에 [VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) cmdlet을 사용 하 여 가상 디스크를 복구 합니다. <br>스토리지 공간 다이렉트는 드라이브를 다시 연결 하거나 교체 하 고 나 서 필요한 경우 자동으로 복구를 시작 합니다.|

### <a name="virtual-disk-health-state-unhealthy"></a>가상 디스크 상태: Unhealthy

가상 디스크가 **비정상** 상태에 있는 경우 가상 디스크의 일부 또는 모든 데이터에 현재 액세스할 수 없습니다.

|작동 상태    |설명|
|---------            |--------   |
|중복성 없음|너무 많은 드라이브가 실패 하 여 가상 디스크의 데이터가 손실 되었습니다.<br><br>**작업**: 실패 한 드라이브를 바꾼 다음 백업에서 데이터를 복원 합니다.|

### <a name="virtual-disk-health-state-informationunknown"></a>가상 디스크 상태: 정보/알 수 없음

관리자가 가상 디스크를 오프 라인으로 전환 했거나 가상 디스크를 사용할 수 없는 경우에도 가상 디스크는 **정보** 상태 (저장소 공간 제어판 항목에 표시) 또는 **알 수 없는** 상태 (PowerShell에 표시 됨)에 있을 수 있습니다. 단독.

|작동 상태    |분리 된 이유 |설명|
|---------            |---------       |--------   |
|Detached             |정책에 따라            |관리자가 가상 디스크를 오프 라인으로 설정 했거나 수동 첨부 파일이 필요 하도록 가상 디스크를 설정 합니다 .이 경우 Windows가 다시 시작 될 때마다 가상 디스크를 수동으로 연결 해야 합니다.<br><br>**작업**: 가상 디스크를 다시 온라인 상태로 전환 합니다. 이렇게 하려면 가상 디스크가 클러스터 된 저장소 풀에 있는 경우 장애 조치(Failover) 클러스터 관리자 **저장소** > **풀** > **가상**디스크를 선택 하 고, **오프 라인** 상태를 표시 하는 가상 디스크를 선택 하 고 가져오기를 선택 합니다.  **온라인**. <br><br>클러스터에 있지 않을 때 가상 디스크를 다시 온라인 상태로 만들려면 관리자 권한으로 PowerShell 세션을 열고 다음 명령을 사용 하 여 시도 합니다.<br><br> <code>Get-VirtualDisk \| Where-Object -Filter { $_.OperationalStatus -eq "Detached" } \| Connect-VirtualDisk</code><br><br>Windows가 다시 시작 된 후 클러스터 되지 않은 모든 가상 디스크를 자동으로 연결 하려면 관리자 권한으로 PowerShell 세션을 열고 다음 명령을 사용 합니다.<br><br> <code>Get-VirtualDisk \| Set-VirtualDisk -ismanualattach $false</code>|
|            |과반수 디스크가 비정상 상태임 |이 가상 디스크에서 사용 하는 드라이브가 너무 많거나, 누락 되었거나, 오래 된 데이터가 있습니다.   <br><br>**작업**: <br> 1. 누락 된 드라이브를 다시 연결 하 고 스토리지 공간 다이렉트 사용 하는 경우 오프 라인 상태인 모든 서버를 온라인 상태로 전환 합니다. <br> 2. 모든 드라이브 및 서버가 온라인 상태가 되 면 오류가 발생 한 모든 드라이브를 바꿉니다. 자세한 내용은 [상태 관리 서비스](../../failover-clustering/health-service-overview.md) 를 참조 하세요. <br>스토리지 공간 다이렉트는 드라이브를 다시 연결 하거나 교체 하 고 나 서 필요한 경우 자동으로 복구를 시작 합니다.<br>3. 스토리지 공간 다이렉트 사용 하 고 있지 않은 경우 다음에 [VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) cmdlet을 사용 하 여 가상 디스크를 복구 합니다.  <br><br>데이터의 복사본을 포함 하는 것 보다 많은 디스크가 실패 하 고 가상 디스크가 오류 간에 복구 되지 않은 경우 가상 디스크의 모든 데이터가 영구적으로 손실 됩니다. 이 경우 가상 디스크를 삭제 하 고 새 가상 디스크를 만든 다음 백업에서 복원 합니다.|
|                     |안함 |드라이브가 부족 하 여 가상 디스크를 읽을 수 없습니다.    <br><br>**작업**: <br> 1. 누락 된 드라이브를 다시 연결 하 고 스토리지 공간 다이렉트 사용 하는 경우 오프 라인 상태인 모든 서버를 온라인 상태로 전환 합니다. <br> 2. 모든 드라이브 및 서버가 온라인 상태가 되 면 오류가 발생 한 모든 드라이브를 바꿉니다. 자세한 내용은 [상태 관리 서비스](../../failover-clustering/health-service-overview.md) 를 참조 하세요. <br>스토리지 공간 다이렉트는 드라이브를 다시 연결 하거나 교체 하 고 나 서 필요한 경우 자동으로 복구를 시작 합니다.<br>3. 스토리지 공간 다이렉트 사용 하 고 있지 않은 경우 다음에 [VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) cmdlet을 사용 하 여 가상 디스크를 복구 합니다.<br><br>데이터의 복사본을 포함 하는 것 보다 많은 디스크가 실패 하 고 가상 디스크가 오류 간에 복구 되지 않은 경우 가상 디스크의 모든 데이터가 영구적으로 손실 됩니다. 이 경우 가상 디스크를 삭제 하 고 새 가상 디스크를 만든 다음 백업에서 복원 합니다.|
| |시간 제한|가상 디스크를 연결 하는 데 너무 오래 걸렸습니다. <br><br> **조치** 이는 자주 발생 하지 않으므로 조건이 시간 경과 하는지 확인 하는 것이 좋습니다. 또는 [VirtualDisk](https://docs.microsoft.com/powershell/module/storage/disconnect-virtualdisk?view=win10-ps) cmdlet을 사용 하 여 가상 디스크의 연결을 끊은 다음 [VirtualDisk](https://docs.microsoft.com/powershell/module/storage/connect-virtualdisk?view=win10-ps) cmdlet을 사용 하 여 다시 연결할 수 있습니다. |

## <a name="drive-physical-disk-states"></a>드라이브 (실제 디스크) 상태

다음 섹션에서는 드라이브가 있을 수 있는 상태에 대해 설명 합니다. 풀의 드라이브는 PowerShell에서 *실제 디스크* 개체로 표시 됩니다.

### <a name="drive-health-state-healthy"></a>드라이브 상태: 정상

|작동 상태    |설명|
|---------            |---------          |
|확인|드라이브가 정상입니다.|
|서비스에서|드라이브가 내부 정리 작업을 수행 하 고 있습니다. 작업이 완료 되 면 드라이브가 *OK* 성능 상태로 돌아옵니다.|

### <a name="drive-health-state-warning"></a>드라이브 상태: Warning

경고 상태의 드라이브는 데이터를 성공적으로 읽고 쓸 수 있지만 문제가 있을 수 있습니다.

|작동 상태    |설명|
|---------            |---------          |
|통신 끊김|드라이브가 없습니다. 스토리지 공간 다이렉트 사용 하는 경우 서버가 다운 되었기 때문일 수 있습니다.<br><br>**작업**: 스토리지 공간 다이렉트를 사용 하는 경우 모든 서버를 다시 온라인 상태로 전환 합니다. 이 문제가 해결 되지 않으면 드라이브를 다시 연결 하거나, 드라이브를 교체 하거나, Windows 오류 보고를 사용 하 여 문제 해결의 단계를 수행 하 여이 드라이브에 대 한 자세한 진단 정보를 확인 하십시오. > [실제 디스크 시간이 초과 되었습니다](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-timed-out).|
|풀에서 제거|저장소 공간이 저장소 풀에서 드라이브를 제거 하는 중입니다. <br><br> 이는 임시 상태입니다. 제거가 완료 된 후 드라이브가 시스템에 계속 연결 되어 있으면 드라이브는 원시 풀에서 다른 작동 상태 (일반적으로 정상)로 전환 됩니다.|
|유지 관리 모드 시작|저장소 공간은 관리자가 드라이브를 유지 관리 모드로 전환 하 고 나면 드라이브를 유지 관리 모드로 전환 하는 프로세스에 있습니다. 임시 상태입니다. 드라이브가 곧 *유지 관리 모드* 상태에 있게 됩니다.|
|유지 관리 모드|관리자가 드라이브를 유지 관리 모드로 전환 하 여 드라이브의 읽기 및 쓰기를 중지 합니다. 일반적으로이 작업은 드라이브 펌웨어를 업데이트 하거나 오류를 테스트할 때 수행 됩니다.<br><br>**작업**: 드라이브를 유지 관리 모드에서 [해제 하려면 StorageMaintenanceMode](https://technet.microsoft.com/itpro/powershell/windows/storage/disable-storagemaintenancemode) cmdlet을 사용 합니다.|
|유지 관리 모드 중지|관리자가 드라이브를 유지 관리 모드로 전환 하 고 저장소 공간이 드라이브를 다시 온라인 상태로 전환 하는 중입니다. 임시 상태입니다. 드라이브는 곧 *정상*상태가 되는 것이 좋습니다.|
|예측 오류|드라이브에서 오류가 발생 했음을 보고 했습니다.<br><br>**작업**: 드라이브를 바꿉니다.|
|IO 오류|드라이브에 액세스 하는 동안 일시적인 오류가 발생 했습니다.<br><br>**작업**: <br>1. 드라이브가 다시 **정상** 상태로 전환 되지 않으면 PhysicalDisk cmdlet을 사용 하 여 드라이브를 [초기화할](https://docs.microsoft.com/powershell/module/storage/reset-physicaldisk) 수 있습니다. <br> 2. [VirtualDisk](https://docs.microsoft.com/powershell/module/storage/repair-virtualdisk) 를 사용 하 여 영향을 받는 가상 디스크의 복원 력을 복원 합니다. <br>3. 이 문제가 계속 되 면 드라이브를 교체 합니다.|
|일시적인 오류|드라이브에 일시적인 오류가 있습니다. 이는 일반적으로 드라이브가 응답 하지 않는다는 것을 의미 하지만 저장소 공간 보호 파티션이 드라이브에서 부적절 하 게 제거 되었음을 의미할 수도 있습니다. <br><br>**작업**: <br>1. 드라이브가 다시 **정상** 상태로 전환 되지 않으면 PhysicalDisk cmdlet을 사용 하 여 드라이브를 [초기화할](https://docs.microsoft.com/powershell/module/storage/reset-physicaldisk) 수 있습니다. <br> 2. [VirtualDisk](https://docs.microsoft.com/powershell/module/storage/repair-virtualdisk) 를 사용 하 여 영향을 받는 가상 디스크의 복원 력을 복원 합니다. <br>3. 이 문제가 계속 발생 하는 경우 드라이브를 교체 하거나, Windows 오류 보고를 사용 하 여 문제 해결의 단계를 수행 하 여이 드라이브에 대 한 자세한 진단 정보를 확인해 보십시오. > [실제 디스크를 온라인 상태로 만들지 못했습니다](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-failed-to-come-online).|
|비정상 대기 시간|스토리지 공간 다이렉트에서 상태 관리 서비스 측정 된 대로 드라이브가 느리게 작동 하 고 있습니다.<br><br>**작업**: 이 문제가 계속 되 면 드라이브를 교체 하 여 저장소 공간의 성능을 크게 줄이지 않습니다.

### <a name="drive-health-state-unhealthy"></a>드라이브 상태: Unhealthy

비정상 상태의 드라이브는 현재 쓰거나 액세스할 수 없습니다.

|작동 상태    |설명|
|---------            |---------          |
|사용할 수 없음|이 드라이브는 저장소 공간에서 사용할 수 없습니다. 자세한 내용은 [스토리지 공간 다이렉트 하드웨어 요구 사항](storage-spaces-direct-hardware-requirements.md)을 참조 하세요. 스토리지 공간 다이렉트 사용 하지 않는 경우 [저장소 공간 개요](https://technet.microsoft.com/library/hh831739(v=ws.11).aspx#Requirements)를 참조 하세요.|
|분리할|드라이브가 풀에서 분리 되었습니다.<br><br>**작업**: 드라이브를 다시 설정 하 고, 드라이브에서 모든 데이터를 지우고, 빈 드라이브로 다시 풀에 추가 합니다. 이렇게 하려면 관리자 권한으로 PowerShell 세션을 열고 [PhysicalDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk) cmdlet을 실행 한 다음 [VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)를 실행 합니다. <br><br>이 드라이브에 대 한 자세한 진단 정보를 보려면 Windows 오류 보고 사용 하 여 문제 해결의 단계를 수행 > [실제 디스크를 온라인 상태로 만들지 못했습니다](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-failed-to-come-online).|
|오래 된 메타 데이터|저장소 공간에서 드라이브의 이전 메타 데이터를 찾았습니다.<br><br>**작업**: 이는 임시 상태 여야 합니다. 드라이브가 다시 정상으로 전환 되지 않으면 [VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) 를 실행 하 여 영향을 받는 가상 디스크에서 복구 작업을 시작할 수 있습니다. 이렇게 해도 문제가 해결 되지 않으면 [PhysicalDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk) cmdlet을 사용 하 여 드라이브를 다시 설정 하 고, 드라이브에서 모든 데이터를 초기화 한 후 [VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)를 실행할 수 있습니다.|
|인식할 수 없는 메타 데이터|저장소 공간에서 드라이브의 인식할 수 없는 메타 데이터를 찾았습니다 .이는 일반적으로 드라이브에 다른 풀의 메타 데이터가 있음을 의미 합니다.<br><br>**작업**: 드라이브를 초기화 하 여 현재 풀에 추가 하려면 드라이브를 다시 설정 합니다. 드라이브를 다시 설정 하려면 관리자 권한으로 PowerShell 세션을 열고 [PhysicalDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk) cmdlet을 실행 한 다음 [VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)를 실행 합니다.|
|실패 한 미디어|드라이브가 실패 했으며 저장소 공간에서 더 이상 사용 되지 않습니다.<br><br>**작업**: 드라이브를 바꿉니다. <br><br>이 드라이브에 대 한 자세한 진단 정보를 보려면 Windows 오류 보고 사용 하 여 문제 해결의 단계를 수행 > [실제 디스크를 온라인 상태로 만들지 못했습니다](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-failed-to-come-online).|
|장치 하드웨어 오류|이 드라이브에 하드웨어 오류가 발생 했습니다. <br><br>**작업**: 드라이브를 바꿉니다.|
|펌웨어 업데이트|Windows에서 드라이브의 펌웨어를 업데이트 하 고 있습니다. 이는 일반적으로 1 분 미만 동안 지속 되는 일시적인 상태 이며, 해당 시간 동안 풀의 다른 드라이브가 모든 읽기 및 쓰기를 처리 하는 시간입니다. 자세한 내용은 [드라이브 펌웨어 업데이트](../update-firmware.md)를 참조 하세요.|
|시작 중|드라이브가 작업을 준비 하는 중입니다. 임시 상태 여야 합니다. 완료 되 면 드라이브가 다른 작동 상태로 전환 되어야 합니다.|

## <a name="reasons-a-drive-cant-be-pooled"></a>드라이브를 풀링할 수 없는 이유

일부 드라이브는 저장소 풀에 준비 되지 않았습니다. 실제 디스크의 `CannotPoolReason` 속성을 살펴보면 드라이브가 풀링을 사용할 수 없는 이유를 알 수 있습니다. 다음은 CannotPoolReason 속성을 표시 하는 예제 PowerShell 스크립트입니다.

```PowerShell
Get-PhysicalDisk | Format-Table FriendlyName,MediaType,Size,CanPool,CannotPoolReason
```

다음은 출력의 예입니다.

```
FriendlyName          MediaType          Size CanPool CannotPoolReason
------------          ---------          ---- ------- ----------------
ATA MZ7LM120HCFD00D3  SSD        120034123776   False Insufficient Capacity
Msft Virtual Disk     SSD         10737418240    True
Generic Physical Disk SSD        119990648832   False In a Pool
```

다음 표에서는 각 이유에 대 한 자세한 정보를 제공 합니다.

|Reason|설명|
|---|---|
|풀에서|드라이브가 이미 저장소 풀에 속해 있습니다. <br><br>드라이브는 한 번에 하나의 저장소 풀에만 속할 수 있습니다. 다른 저장소 풀에서이 드라이브를 사용 하려면 먼저 기존 풀에서 드라이브를 제거 합니다. 그러면 저장소 공간에서 풀의 다른 드라이브로 드라이브의 데이터를 이동 합니다. 또는 저장소 공간에 알리지 않고 풀에서 드라이브의 연결을 끊은 경우 드라이브를 다시 설정 합니다. <br><br>저장소 풀에서 드라이브를 안전 하 게 제거 하려면 [PhysicalDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/remove-physicaldisk)를 사용 하거나 서버 관리자 > **파일 및 저장소 서비스**@no__t 2**저장소 풀**, > **실제 디스크**로 이동 하 여 드라이브를 마우스 오른쪽 단추로 클릭 한 다음 제거를 선택 합니다.  **디스크**.<br><br>드라이브를 다시 설정 하려면 [PhysicalDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk)를 사용 합니다.|
|비정상|드라이브가 정상 상태가 아니며 교체 해야 할 수 있습니다.|
|이동식 미디어|드라이브가 이동식 드라이브로 분류 됩니다. <br><br>저장소 공간은 Windows에서 사용할 수 있는 이동식 미디어 (예: 블루레이 드라이브)를 지원 하지 않습니다. 대부분의 고정 드라이브가 이동식 슬롯에 있지만 일반적으로 Windows에 의해 이동식으로 *분류* 된 미디어는 저장소 공간에서 사용 하기에 적합 하지 않습니다.|
|클러스터에서 사용|드라이브가 현재 장애 조치 (Failover) 클러스터에서 사용 되 고 있습니다.|
|오프라인|드라이브가 오프 라인 상태입니다. <br><br>모든 오프 라인 드라이브를 온라인으로 전환 하 고 읽기/쓰기로 설정 하려면 관리자 권한으로 PowerShell 세션을 열고 다음 스크립트를 사용 합니다.<br><br><code>Get-Disk \| Where-Object -Property OperationalStatus -EQ "Offline" \| Set-Disk -IsOffline $false</code><br><br><code>Get-Disk \| Where-Object -Property IsReadOnly -EQ $true \| Set-Disk -IsReadOnly $false</code>|
|용량 부족|이는 드라이브에서 사용 가능한 공간을 차지 하는 파티션이 있는 경우에 일반적으로 발생 합니다. <br><br>**작업**: 드라이브의 모든 데이터를 삭제 하 여 드라이브의 모든 볼륨을 삭제 합니다. 이 작업을 수행 하는 한 가지 방법은 [Clear Disk](https://docs.microsoft.com/powershell/module/storage/clear-disk?view=win10-ps) PowerShell cmdlet을 사용 하는 것입니다.|
|확인 진행 중|[상태 관리 서비스](../../failover-clustering/health-service-overview.md#supported-components-document) 는 서버 관리자가 드라이브의 드라이브 또는 펌웨어를 사용할 수 있도록 승인 되었는지 여부를 확인 합니다.|
|확인 실패|[상태 관리 서비스](../../failover-clustering/health-service-overview.md#supported-components-document) 드라이브의 드라이브 또는 펌웨어가 서버 관리자가 사용할 수 있도록 승인 되었는지 확인할 수 없습니다.|
|펌웨어가 비규격 임|물리적 드라이브의 펌웨어가 [상태 관리 서비스](../../failover-clustering/health-service-overview.md#supported-components-document)를 사용 하 여 서버 관리자가 지정한 승인 된 펌웨어 수정 버전 목록에 없습니다. |
|하드웨어 비준수|[상태 관리 서비스](../../failover-clustering/health-service-overview.md#supported-components-document)를 사용 하 여 서버 관리자가 지정한 승인 된 저장소 모델 목록에 드라이브가 없습니다.|

## <a name="see-also"></a>참조

- [스토리지 공간 다이렉트](storage-spaces-direct-overview.md)
- [하드웨어 요구 사항 스토리지 공간 다이렉트](storage-spaces-direct-hardware-requirements.md)
- [클러스터 및 풀 쿼럼의 이해](understand-quorum.md)