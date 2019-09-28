---
ms.assetid: 60fca6b2-f1c0-451f-858f-2f6ab350d220
title: 데이터 중복 제거 상호 운용성
ms.technology: storage-deduplication
ms.prod: windows-server
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 09/16/2016
ms.openlocfilehash: fb3c9842f1d698151bffebbe5f77618c8b19b366
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403201"
---
# <a name="data-deduplication-interoperability"></a>데이터 중복 제거 상호 운용성

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2019

## <a name="supported"></a>지원됨

### <a name="refs"></a>ReFS
데이터 중복 제거는 Windows Server 2019에서 지원 됩니다. 

### <a name="failover-clustering"></a>장애 조치(failover) 클러스터링

[장애 조치(failover) 클러스터링](../..//failover-clustering/failover-clustering-overview.md)은 클러스터의 모든 노드에 [데이터 중복 제거 기능이 설치](install-enable.md#install-dedup)되어 있는 경우 완전히 지원됩니다. 기타 중요한 참고 사항:

* [수동으로 시작한 데이터 중복 제거 작업](run.md#running-dedup-jobs-manually)은 클러스터 공유 볼륨의 소유자 노드에서 실행해야 합니다.
* 예약된 데이터 중복 제거 작업은 예약된 클러스터 작업에 저장되므로 중복 제거된 볼륨이 다른 노드에서 사용되는 경우 예약된 작업은 다음 예약 간격에서 적용됩니다.
* 데이터 중복 제거는 [클러스터 OS 롤링 업그레이드](../..//failover-clustering/cluster-operating-system-rolling-upgrade.md) 기능과 완전히 상호 운용됩니다.
* 데이터 중복 제거는 [저장소 공간 다이렉트](../storage-spaces/storage-spaces-direct-overview.md) NTFS로 포맷 된 볼륨(미러 또는 패리티)에서 완전히 지원됩니다. 여러 계층이 있는 볼륨에서는 중복 제거가 지원되지 않습니다. 자세한 내용은 [ReFS에서 데이터 중복 제거](#unsupported)를 참조하세요.

### <a name="storage-replica"></a>저장소 복제본
[저장소 복제본](../storage-replica/storage-replica-overview.md)은 완전히 지원됩니다. 데이터 중복 제거는 보조 복사본에서 실행되지 않도록 구성되어야 합니다.

### <a name="branchcache"></a>BranchCache
서버 및 클라이언트에서 [BranchCache](../../networking/branchcache/branchcache.md)를 사용하도록 설정하면 네트워크를 통한 데이터 액세스를 최적화할 수 있습니다. BranchCache 사용 시스템이 데이터 중복 제거를 실행하는 원격 파일 서버와 WAN을 통해 통신할 때 중복 제거된 모든 파일은 이미 인덱싱 및 해시된 상태입니다. 따라서 지점의 데이터 요청이 빠르게 계산됩니다. 이러한 과정은 BranchCache 사용 서버를 미리 인덱싱하거나 미리 해싱하는 것과 비슷합니다.

### <a name="dfs-replication"></a>DFS 복제
데이터 중복 제거는 DFS(분산 파일 시스템) 복제에서 제대로 작동합니다. 파일을 최적화하거나 최적화 해제하는 경우 파일이 변경되지 않으므로 복제가 트리거되지 않습니다. DFS 복제는 네트워크 절약을 위해 청크 저장소의 청크가 아니라 RDC(원격 차등 압축)를 사용합니다. 또한 복제본이 데이터 중복 제거를 사용하는 경우 중복 제거를 사용하여 복제본의 파일을 최적화할 수 있습니다.

### <a name="quotas"></a>할당량
데이터 중복 제거는 중복 제거가 사용되는 볼륨 루트 폴더에 하드 할당량을 만들도록 지원하지 않습니다. 하드 할당량이 볼륨 루트에 있는 경우 볼륨의 실제 여유 공간과 볼륨의 할당량 제한 공간이 같지 않습니다. 이로 인해 중복 제거 최적화 작업이 실패할 수 있습니다. 하지만 중복 제거가 사용되는 볼륨 루트에 소프트 할당량을 만들 수는 있습니다. 

중복 제거된 볼륨에서 할당량을 사용하는 경우 할당량은 파일의 실제 크기가 아니라 파일의 논리적 크기를 사용합니다. 중복 제거에 의해 파일이 처리될 때 할당량 사용 현황(할당량 임계값을 포함하여)은 변경되지 않습니다. 볼륨 루트 소프트 할당량 및 하위 폴더의 할당량을 비롯한 다른 모든 할당량 기능은 중복 제거가 사용될 때 정상적으로 작동합니다.

### <a name="windows-server-backup"></a>Windows Server 백업
Windows Server 백업에서는 최적화된 볼륨을 있는 그대로(즉, 중복 제거된 데이터를 제거하지 않고) 백업할 수 있습니다. 다음 단계에서는 볼륨을 백업하는 방법과 볼륨 또는 볼륨에서 선택한 파일을 복원하는 방법을 보여 줍니다.
1. Windows Server 백업을 설치합니다.  
    ```PowerShell
    Install-WindowsFeature -Name Windows-Server-Backup
    ```

2. 다음 명령을 실행하여 상황에 맞는 올바른 볼륨 이름으로 대체하여 E: 볼륨을 다른 볼륨에 백업합니다.  
    ```PowerShell
    wbadmin start backup –include:E: -backuptarget:F: -quiet
    ```
3. 방금 만든 백업의 버전 ID를 가져옵니다.

    ```PowerShell
    wbadmin get versions
    ```

    이 출력 버전 ID는 날짜 및 시간 문자열이 됩니다. 예를 들면 다음과 같습니다. 08/18/2016-06:22.

4. 전체 볼륨을 복원합니다.
    ```PowerShell
    wbadmin start recovery –version:02/16/2012-06:22 -itemtype:Volume  -items:E: -recoveryTarget:E:
    ```

    **--또는--**  

    특정 폴더를 복원합니다(이 경우 E:\Docs 폴더).
    ```PowerShell
    wbadmin start recovery –version:02/16/2012-06:22 -itemtype:File  -items:E:\Docs  -recursive
    ```

## <a name="unsupported"></a>지원되지 않음

### <a name="windows-10-client-os"></a>Windows 10 (클라이언트 OS)
Windows 10에서는 데이터 중복 제거가 지원되지 않습니다. Windows Server 2016에서 해당 이진 파일을 분리하여 Windows 10에 설치하는 방법을 설명하는 몇몇 블로그 포스트가 Windows 커뮤니티에서 널리 읽히고 있으나 이러한 시나리오는 데이터 중복 제거 개발 과정에서 검증된 적이 없습니다. [Windows 10 vNext에 이 항목이 포함되도록 Windows Server Storage UserVoice에서 투표하실 수 있습니다](https://windowsserver.uservoice.com/forums/295056-storage/suggestions/9011008-add-deduplication-support-to-client-os).

### <a name="windows-search"></a>Windows 검색
Windows Search는 데이터 중복 제거를 지원하지 않습니다. 데이터 중복 제거는 Windows Search에서 인덱싱할 수 없는 재분석 지점을 사용하므로 Windows Search에서는 중복 제거된 파일을 모두 건너뛰고 인덱스에서 제외시킵니다. 결과적으로, 중복 제거된 볼륨에 대한 검색 결과는 불완전할 수 있습니다. [Windows Server vNext에 이 항목이 포함되도록 Windows Server Storage UserVoice에서 투표하실 수 있습니다](https://windowsserver.uservoice.com/forums/295056-storage/suggestions/17888647-make-windows-search-service-work-with-data-dedupli).

### <a name="robocopy"></a>Robocopy
데이터 중복 제거와 함께 Robocopy를 실행하는 것은 권장되지 않습니다. 특정 Robocopy 명령이 청크 저장소를 손상시킬 수 있기 때문입니다. 청크 저장소는 볼륨에 대한 시스템 볼륨 정보 폴더에 저장됩니다. 이 폴더가 삭제되면 데이터 청크가 대상 볼륨에 복사되지 않기 때문에 원본 볼륨에서 복사된 최적화된 파일(재분석 지점)이 손상됩니다.
