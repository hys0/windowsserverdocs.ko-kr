---
title: 장애 조치 (failover) 클러스터에서 클러스터 공유 볼륨 사용
description: 장애 조치 (failover) 클러스터에서 클러스터 공유 볼륨을 사용 하는 방법
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: da0f541c34c7f8687822bec365364fdd406fa3c3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369739"
---
# <a name="use-cluster-shared-volumes-in-a-failover-cluster"></a>장애 조치 (failover) 클러스터에서 클러스터 공유 볼륨 사용

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2

CSV(클러스터 공유 볼륨)는 장애 조치 클러스터의 여러 노드에서 NTFS 볼륨으로 프로비전된 동일한 LUN(디스크)에 동시에 읽기/쓰기 액세스할 수 있도록 지원합니다. Windows Server 2012 r 2에서는 디스크를 NTFS 또는 ReFS (Resilient File System)로 프로 비전 할 수 있습니다. CSV를 사용하면 드라이브 소유권을 변경하거나 볼륨을 분리하고 다시 탑재할 필요 없이 클러스터된 역할을 노드 간에 신속하게 장애 조치(failover)할 수 있습니다. 또한 장애 조치(failover) 클러스터에서 잠재적으로 많은 LUN을 간소화할 수 있습니다.

CSV는 NTFS (또는 Windows Server 2012 r 2의 경우 ReFS) 위에 계층화 된 범용 클러스터 된 파일 시스템을 제공 합니다. CSV 응용 프로그램은 다음과 같습니다.

- 클러스터된 Hyper-V 가상 컴퓨터의 클러스터된 VHD(가상 하드 디스크) 파일
- 스케일 아웃 파일 서버 클러스터된 역할의 응용 프로그램 데이터를 저장하는 스케일 아웃 파일 공유. 이 역할의 응용 프로그램 데이터에 대한 예로는 Hyper-V 가상 컴퓨터 파일 및 Microsoft SQL Server 데이터를 들 수 있습니다. ReFS는 스케일 아웃 파일 서버에서 지원되지 않습니다. 스케일 아웃 파일 서버에 대 한 자세한 내용은 [응용 프로그램 데이터에 대 한 스케일 아웃 파일 서버](sofs-overview.md)를 참조 하세요.

> [!NOTE]
> Csv SQL Server 2012 및 이전 버전 SQL Server에서 Microsoft SQL Server 클러스터 된 워크 로드를 지원 하지 않습니다.

Windows Server 2012에서는 CSV 기능이 크게 향상 되었습니다. 예를 들어 Active Directory 도메인 서비스에 대한 종속성이 제거되었습니다. **chkdsk**의 기능 향상, 바이러스 백신 및 백업 응용 프로그램과의 상호 운용성, BitLocker로 암호화된 볼륨 및 저장소 공간과 같은 일반적인 저장소 기능과의 통합 등에 대한 지원이 추가되었습니다. Windows Server 2012에 도입 된 CSV 기능에 대 한 개요는 [Windows server 2012에서 장애 조치 (Failover) 클러스터링의 새로운 기능 \[redirected @ no__t-2](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265972(v%3dws.11)>)를 참조 하세요.

Windows Server 2012 r 2에서는 분산 CSV 소유권과 같은 추가 기능을 제공 하 고, 서버 서비스의 가용성을 통해 복원 력을 높이고, CSV 캐시에 할당할 수 있는 실제 메모리의 양에 대 한 유연성을 향상 시킵니다. 진단 가능성 및 ReFS 및 중복 제거에 대 한 지원을 포함 하는 향상 된 상호 운용성. 자세한 내용은 [장애 조치 (Failover) 클러스터링의 새로운 기능](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265972(v%3dws.11)>)을 참조 하세요.

> [!NOTE]
> VDI(가상 데스크톱 인프라) 시나리오에 CSV의 데이터 중복 제거를 사용하는 방법에 대한 자세한 내용은 블로그 게시물 [Windows Server 2012 R2에서 VDI 저장소에 대한 데이터 중복 제거 배포](https://blogs.technet.com/b/filecab/archive/2013/07/31/deploying-data-deduplication-for-vdi-storage-in-windows-server-2012-r2.aspx) (영문) 및 [Windows Server 2012 R2에서 새워크로드로 데이터 중복 제거 확장](https://blogs.technet.com/b/filecab/archive/2013/07/31/extending-data-deduplication-to-new-workloads-in-windows-server-2012-r2.aspx)(영문)을 참조하세요.

## <a name="review-requirements-and-considerations-for-using-csv-in-a-failover-cluster"></a>장애 조치(failover) 클러스터에서 CSV를 사용하기 위한 요구 사항 및 고려 사항 검토

장애 조치(failover) 클러스터에서 CSV를 사용하기 전에 이 섹션의 네트워크, 저장소 및 기타 요구 사항과 고려 사항을 검토합니다.

### <a name="network-configuration-considerations"></a>네트워크 구성 고려 사항

CSV를 지원하는 네트워크를 구성할 때 고려할 사항은 다음과 같습니다.

- **여러 네트워크와 여러 네트워크 어댑터**. 네트워크 오류가 발생한 경우 내결함성을 지원하려면 여러 클러스터 네트워크에서 CSV 트래픽을 처리하거나 팀으로 구성된 네트워크 어댑터를 구성하는 것이 좋습니다.
    
    클러스터 노드가 클러스터에서 사용할 수 없는 네트워크에 연결된 경우 이러한 노드를 비활성화해야 합니다. 예를 들어 이러한 네트워크에서 CSV 트래픽을 방지하기 위해 클러스터에서 iSCSI 네트워크를 사용하지 않도록 설정하는 것이 좋습니다. 네트워크를 사용 하지 않도록 설정 하려면 장애 조치(Failover) 클러스터 관리자에서 **네트워크를 선택 하**고, 네트워크를 선택 하 고, **속성** 작업을 선택한 후 **이 네트워크에서 클러스터 네트워크 통신 허용 안 함**을 선택 합니다. 또는 [Get clusternetwork](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusternetwork?view=win10-ps) Windows PowerShell cmdlet을 사용 하 여 네트워크의 **역할** 속성을 구성할 수 있습니다.
- **네트워크 어댑터 속성**. 클러스터 통신을 수행하는 모든 어댑터에 대한 속성에서 다음 설정이 사용하도록 설정되어 있는지 확인합니다.

  - **Microsoft Networks용 클라이언트** and **Microsoft 네트워크용 파일 및 프린터 공유**. 이러한 설정은 노드 간에 CSV 트래픽을 전달하는 데 기본적으로 사용되는 SMB(서버 메시지 블록) 3.0을 지원합니다. SMB를 사용하려면 서버 서비스와 워크스테이션 서비스가 실행되고 있으며 각 클러스터 노드에서 자동으로 시작하도록 구성되어 있는지도 확인해야 합니다.

    >[!NOTE]
    >Windows Server 2012 r 2에는 장애 조치 (failover) 클러스터 노드당 여러 개의 서버 서비스 인스턴스가 있습니다. 일반 파일 공유에 액세스한 SMB 클라이언트에서 들어오는 트래픽을 처리하는 기본 인스턴스와 노드 간 CSV 트래픽만 처리하는 두 번째 CSV 인스턴스가 있습니다. 또한 노드의 서버 서비스가 비정상 상태가 되면 CSV 소유권이 자동으로 다른 노드로 전환됩니다.

    SMB 3.0에는 CSV 트래픽을 클러스터의 여러 네트워크에서 스트리밍할 수 있으며 RDMA(원격 직접 메모리 액세스)가 지원되는 네트워크 어댑터를 활용할 수 있는 SMB 다중 채널 및 SMB 다이렉트 기능이 포함되어 있습니다. 기본적으로 SMB 다중 채널은 CSV 트래픽에 사용됩니다. 자세한 내용은 [서버 메시지 블록 개요](../storage/file-server/file-server-smb-overview.md)를 참조하세요.
  - **Microsoft 장애 조치(failover) 클러스터 가상 어댑터 성능 필터**. 이 설정은 CSV에 연결해야 하는 경우(예: 연결 실패로 인해 CSV 디스크에 직접 연결할 수 없는 경우) I/O 리디렉션을 수행하는 노드의 기능을 향상시킵니다. 자세한 내용은이 항목의 뒷부분에 나오는 [CSV 통신의 i/o 동기화 및 i/o 리디렉션 정보](#about-io-synchronization-and-io-redirection-in-csv-communication) 를 참조 하십시오.
- **클러스터 네트워크 우선 순위**. 일반적으로 클러스터에서 구성한 네트워크 기본 설정을 변경하지 않는 것이 좋습니다.
- **IP 서브넷 구성**. CSV를 사용하는 네트워크의 노드에는 특정 서브넷 구성이 필요하지 않습니다. CSV는 다중 서브넷 클러스터를 지원할 수 있습니다.
- **정책 기반 QoS(서비스 품질)** . CSV를 사용하는 경우 각 노드의 네트워크 트래픽에 대한 QoS 우선 순위 정책 및 최소 대역폭 정책을 구성하는 것이 좋습니다. 자세한 내용은 [QoS (서비스 품질)](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831679(v%3dws.11)>)를 참조 하세요.
- **저장소 네트워크**. 저장소 네트워크 권장 사항은 저장소 공급업체에서 제공하는 지침을 검토합니다. CSV 저장소에 대 한 추가 고려 사항은이 항목의 뒷부분에 있는 [저장소 및 디스크 구성 요구 사항](#storage-and-disk-configuration-requirements) 을 참조 하세요.

장애 조치(Failover) 클러스터의 하드웨어, 네트워크 및 저장소 요구 사항에 대한 개요는 [Failover Clustering Hardware Requirements and Storage Options](clustering-requirements.md)을 참조하세요.

#### <a name="about-io-synchronization-and-io-redirection-in-csv-communication"></a>CSV 통신의 I/O 동기화 및 리디렉션된 I/O 모드 정보

- I/o **동기화**: CSV를 사용 하면 여러 노드에서 동일한 공유 저장소에 대 한 동시 읽기/쓰기 액세스를 사용할 수 있습니다. 노드에서 CSV 볼륨에 대해 디스크 I/O(입/출력)를 수행하는 경우 이 노드는 SAN(저장소 영역 네트워크) 등을 통해 저장소와 직접 통신합니다. 그러나 항상 단일 노드(코디네이터 노드라고 함)에서 LUN과 연결된 실제 디스크 리소스를 "소유"합니다. CSV 볼륨의 코디네이터 노드는 장애 조치(failover) 클러스터 관리자에서 **디스크** 아래에 **소유자 노드**로 표시됩니다. 또한이 파일은 [Get ClusterSharedVolume](https://docs.microsoft.com/powershell/module/failoverclusters/get-clustersharedvolume?view=win10-ps) Windows PowerShell cmdlet의 출력에도 표시 됩니다.

  >[!NOTE]
  >Windows Server 2012 r 2에서는 CSV 소유권이 각 노드에서 소유한 CSV 볼륨 수에 따라 장애 조치 (failover) 클러스터 노드 전체에 고르게 분산 됩니다. 또한 CSV 장애 조치(failover)와 같은 조건이 있거나, 노드가 클러스터에 다시 가입하거나, 클러스터에 새 노드를 추가하거나, 클러스터 노드를 다시 시작하거나, 종료 후 장애 조치(failover) 클러스터를 시작하는 경우 소유권의 균형이 자동으로 조정됩니다.

  CSV 볼륨의 파일 시스템에서 사소한 특정 변경 사항이 발생한 경우 단일 코디네이터 노드뿐만 아니라 LUN에 액세스하는 각 실제 노드에서 이 메타데이터를 동기화해야 합니다. 예를 들어 CSV 볼륨의 가상 컴퓨터가 시작, 생성 또는 삭제되거나 가상 컴퓨터가 마이그레이션된 경우 해당 가상 컴퓨터에 액세스하는 각 실제 노드에서 이 정보를 동기화해야 합니다. 이러한 메타데이터 업데이트 작업은 SMB 3.0을 통해 클러스터 네트워크에서 병렬로 발생합니다. 이러한 작업은 모든 실제 노드가 공유 저장소와 통신하지 않아도 실행됩니다.

- I/o **리디렉션**: 저장소 연결 실패 및 특정 저장소 작업이 지정된 노드에서 해당 저장소와 직접 통신하는 것을 차단할 수 있습니다. 노드에서는 저장소와 통신하지 않는 동안 기능을 유지 관리하기 위해 디스크가 현재 탑재된 코디네이터 노드 또는 클러스터 네트워크를 통해 디스크 I/O를 리디렉션합니다. 현재 코디네이터 노드에서 저장소 연결 오류가 발생한 경우 새 노드가 코디네이터 노드로 설정되는 동안 일시적으로 모든 디스크 I/O 작업이 대기합니다.

서버는 상황에 따라 다음 I/O 리디렉션 모드 중 하나를 사용합니다.

- **파일 시스템 리디렉션** 리디렉션이 볼륨 단위로 발생합니다(예: CSV 볼륨이 리디렉션된 I/O 모드에 수동으로 배치되었을 때 백업 응용 프로그램에서 CSV 스냅숏을 만드는 경우).
- **블록 리디렉션** 리디렉션이 파일 블록 수준에서 발생합니다(예: 볼륨의 저장소 연결이 끊어진 경우). 블록 리디렉션은 파일 시스템 리디렉션보다 훨씬 빠릅니다.

Windows Server 2012 r 2에서는 노드 단위로 CSV 볼륨의 상태를 볼 수 있습니다. 예를 들어 I/O가 직접인지, 리디렉션되었는지 또는 CSV 볼륨을 사용할 수 없는지 여부 등을 확인할 수 있습니다. CSV 볼륨이 리디렉션된 I/O 모드에 있으면 이유를 확인할 수도 있습니다. Windows PowerShell cmdlet **Get-ClusterSharedVolumeState** 를 사용하여 이 정보를 볼 수 있습니다.

> [!NOTE]
> * Windows Server 2012에서 CSV 디자인의 향상 된 기능으로 인해 CSV는 Windows Server 2008 r 2에서 발생 한 것 보다 직접 i/o 모드에서 더 많은 작업을 수행 합니다.
> * SMB 다중 채널 및 SMB 다이렉트와 같은 SMB 3.0 기능과 CSV의 통합으로 인해 리디렉션된 I/O 트래픽을 여러 클러스터 네트워크에서 스트리밍할 수 있습니다.
> * I/O 리디렉션 중 코디네이터 노드로 네트워크 트래픽의 잠재적 증가를 허용하도록 클러스터 네트워크를 계획해야 합니다.

### <a name="storage-and-disk-configuration-requirements"></a>저장소 및 디스크 구성 요구 사항

CSV를 사용하려면 저장소 및 디스크가 다음 요구 사항을 충족해야 합니다.

- **파일 시스템 형식**. Windows Server 2012 r 2에서 CSV 볼륨의 디스크 또는 저장소 공간은 NTFS 또는 ReFS로 분할 된 기본 디스크 여야 합니다. Windows Server 2012에서 CSV 볼륨의 디스크 또는 저장소 공간은 NTFS로 분할 된 기본 디스크 여야 합니다.

  CSV의 추가 요구 사항은 다음과 같습니다.
    
  - Windows Server 2012 r 2에서는 FAT 또는 FAT32로 포맷 된 디스크를 CSV에 사용할 수 없습니다.
  - Windows Server 2012에서는 FAT, FAT32 또는 ReFS로 포맷 된 디스크를 CSV에 사용할 수 없습니다.
  - CSV에 저장소 공간을 사용하려는 경우 간단한 공간 또는 미러 공간을 구성할 수 있습니다. Windows Server 2012 r 2에서는 패리티 공간을 구성할 수도 있습니다. Windows Server 2012에서는 CSV가 패리티 공간을 지원 하지 않습니다.
  - CSV를 쿼럼 감시 디스크로 사용할 수 없습니다. 클러스터 쿼럼에 대 한 자세한 내용은 [스토리지 공간 다이렉트 쿼럼 이해](../storage/storage-spaces/understand-quorum.md)를 참조 하세요.
  - 디스크를 CSV로 추가하면 CSVFS 형식(CSV 파일 시스템용)으로 지정됩니다. 따라서 클러스터 및 기타 소프트웨어를 다른 NTFS 또는 ReFS 저장소의 CSV 저장소와 구분할 수 있습니다. 일반적으로 CSVFS는 NTFS 또는 ReFS와 동일한 기능을 지원합니다. 그러나 특정 기능은 지원되지 않습니다. 예를 들어 Windows Server 2012 r 2에서는 CSV에서 압축을 사용 하도록 설정할 수 없습니다. Windows Server 2012에서는 CSV에서 데이터 중복 제거 또는 압축을 사용 하도록 설정할 수 없습니다.
- **클러스터의 리소스 종류**. CSV 볼륨에는 실제 디스크 리소스 종류를 사용해야 합니다. 기본적으로 클러스터 저장소에 추가된 디스크 또는 저장소 공간은 이 방식으로 자동으로 구성됩니다.
- **클러스터 저장소에서 CSV 디스크 또는 다른 디스크 선택**. 클러스터된 가상 컴퓨터에 대해 하나 이상의 디스크를 선택할 때는 각 디스크의 사용 방법을 고려해야 합니다. 디스크가 VHD 파일 또는 구성 파일과 같은 Hyper-V에서 생성된 파일을 저장하는 데 사용되는 경우 CSV 디스크 또는 클러스터 저장소의 다른 사용 가능한 디스크에서 선택할 수 있습니다. 디스크가 가상 컴퓨터에 직접 연결되는 실제 디스크(통과 디스크라고도 함)인 경우에는 CSV 디스크를 선택할 수 없으며, 클러스터 저장소의 다른 사용 가능한 디스크에서 선택해야 합니다.
- **디스크를 식별하는 경로 이름**. CSV의 디스크는 경로 이름으로 식별됩니다. 각 경로는 노드의 시스템 드라이브에서 **\\ClusterStorage** 폴더 아래에 번호가 매겨진 볼륨으로 표시 됩니다. 이 경로는 클러스터의 모든 노드에서 동일하게 표시됩니다. 필요한 경우 볼륨의 이름을 바꿀 수 있습니다.

CSV에 대한 저장소 요구 사항은 저장소 공급업체에서 제공하는 지침을 검토합니다. CSV에 대한 추가 저장소 계획 고려 사항은 이 항목의 뒷부분에 있는 [장애 조치(failover) 클러스터에서 CSV 사용 계획](#plan-to-use-csv-in-a-failover-cluster)을 참조하세요.

### <a name="node-requirements"></a>노드 요구 사항

CSV를 사용하려면 노드가 다음 요구 사항을 충족해야 합니다.

- **시스템 디스크의 드라이브 문자**. 모든 노드에서 시스템 디스크의 드라이브 문자는 동일해야 합니다.
- **인증 프로토콜**. 모든 노드에서 NTLM 프로토콜을 사용하도록 설정해야 합니다. 이 기능은 기본적으로 사용됩니다.

## <a name="plan-to-use-csv-in-a-failover-cluster"></a>장애 조치(failover) 클러스터에서 CSV 사용 계획

이 섹션에서는 Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 장애 조치 (failover) 클러스터에서 CSV를 사용 하기 위한 계획 고려 사항과 권장 사항을 설명 합니다.

> [!IMPORTANT]
> CSV의 특정 저장 장치를 구성하는 방법에 대한 권장 사항은 저장소 공급 업체에 문의하세요. 저장소 공급업체의 권장 사항이 이 항목의 정보와 다른 경우에는 저장소 공급업체의 권장 사항을 사용합니다.

### <a name="arrangement-of-luns-volumes-and-vhd-files"></a>LUN, 볼륨 및 VHD 파일 배열

CSV를 사용하여 클러스터된 가상 컴퓨터에 가장 효율적으로 저장소를 제공하려면 실제 서버를 구성할 때 LUN(디스크)을 배열하는 방법을 검토하는 것이 좋습니다. 해당 가상 컴퓨터를 구성할 때 유사한 방식으로 VHD 파일을 배열해 보세요.

실제 서버의 디스크 및 파일을 정리할 때 고려할 사항은 다음과 같습니다.

- 하나의 실제 디스크에 시스템 파일(페이지 파일 포함) 배치
- 다른 실제 디스크에 데이터 파일 배치

동등한 클러스터된 가상 컴퓨터의 경우 유사한 방식으로 볼륨 및 파일을 정리해야 합니다.

- 하나의 CSV 내 VHD 파일에 시스템 파일(페이지 파일 포함) 배치
- 다른 CSV 내 VHD 파일에 데이터 파일 배치

다른 가상 컴퓨터를 추가할 경우 가능하면 해당 가상 컴퓨터의 VHD와 동일한 배열을 유지해야 합니다.

### <a name="number-and-size-of-luns-and-volumes"></a>LUN 수 및 볼륨 크기

CSV를 사용하는 장애 조치(failover) 클러스터에 대한 저장소 구성을 계획할 때는 다음 권장 사항을 따릅니다.

- 구성할 LUN 수를 결정하려면 저장소 공급업체에 문의합니다. 예를 들어 저장소 공급업체는 하나의 파티션으로 각 LUN을 구성하고 하나의 CSV 볼륨을 배치하도록 권장할 수 있습니다.
- 단일 CSV 볼륨에서 지원할 수 있는 가상 컴퓨터의 수에 대한 제한은 없습니다. 그러나 클러스터에 두려는 가상 컴퓨터 수와 각 가상 컴퓨터에 대한 워크로드(초당 I/O 작업)를 고려해야 합니다. 다음 예를 참조하세요.

  - 어떤 조직에서 VDI(가상 데스크톱 인프라)를 지원할 가상 컴퓨터를 배포하려고 합니다(비교적 작업량이 적음). 클러스터에서는 고성능 저장소를 사용합니다. 클러스터 관리자는 저장소 공급업체에 문의한 후 CSV 볼륨당 비교적 많은 수의 가상 컴퓨터를 배치하기로 결정합니다.
  - 또 다른 조직에서는 자주 사용되는 데이터베이스 응용 프로그램을 지원할 많은 가상 컴퓨터를 배포하려고 합니다(비교적 작업량이 많음). 클러스터에서는 성능이 낮은 저장소를 사용합니다. 클러스터 관리자는 저장소 공급업체에 문의한 후 CSV 볼륨당 비교적 적은 수의 가상 컴퓨터를 배치하기로 결정합니다.
- 특정 가상 컴퓨터에 대한 저장소 구성을 계획할 때는 해당 가상 컴퓨터에서 지원할 서비스, 응용 프로그램 또는 역할에 대한 디스크 요구 사항을 고려합니다. 이러한 요구 사항을 이해하면 성능을 저하시킬 수 있는 디스크 경합을 방지할 수 있습니다. 가상 컴퓨터에 대한 저장소 구성은 동일한 서비스, 응용 프로그램 또는 역할을 실행하는 실제 서버에 사용할 수 있는 저장소 구성과 유사해야 합니다. 자세한 내용은이 항목의 앞부분에 나오는 [lun, 볼륨 및 VHD 파일 배열](#arrangement-of-luns-volumes-and-vhd-files) 을 참조 하십시오.

    저장소에 독립된 실제 하드 디스크를 많이 배치하여 디스크 경합을 완화할 수도 있습니다. 그에 따라 저장소 하드웨어를 선택하고 공급업체와 상의하여 저장소의 성능을 최적화합니다.
- 클러스터 워크로드를 및 I/O 작업의 필요성에 따라 각 LUN에 액세스할 비율의 가상 컴퓨터만 구성하고, 나머지 가상 컴퓨터는 연결하지 않으며 대신 컴퓨팅 작업에만 전용되도록 구성할 수 있습니다.

## <a name="add-a-disk-to-csv-on-a-failover-cluster"></a>장애 조치(failover) 클러스터에 CSV로 디스크 추가

CSV 기능은 장애 조치(failover) 클러스터링에서 기본적으로 사용됩니다. CSV에 디스크를 추가하려면 클러스터의 **사용 가능한 저장소** 그룹(이미 추가되지 않은 경우)에 디스크를 추가한 다음 클러스터의 CSV에 디스크를 추가합니다. 장애 조치(Failover) 클러스터 관리자 또는 장애 조치 (Failover) 클러스터 Windows PowerShell cmdlet을 사용 하 여 이러한 절차를 수행할 수 있습니다.

### <a name="add-a-disk-to-available-storage"></a>사용 가능한 저장소에 디스크 추가

1. 장애 조치(failover) 클러스터 관리자의 콘솔 트리에서 클러스터 이름을 확장한 다음 **저장소**를 확장합니다.
2. **디스크**를 마우스 오른쪽 단추로 클릭 한 다음 **디스크 추가**를 선택 합니다. 장애 조치(failover) 클러스터에서 사용하기 위해 추가할 수 있는 디스크 목록이 표시됩니다.
3. 추가 하려는 디스크를 하나 이상 선택한 다음 **확인**을 선택 합니다.

    이제 디스크가 **사용 가능한 저장소** 그룹에 할당됩니다.

#### <a name="windows-powershell-equivalent-commands-add-a-disk-to-available-storage"></a>Windows PowerShell 해당 명령 (사용 가능한 저장소에 디스크 추가)

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

다음 예제에서는 클러스터에 추가할 준비가 된 디스크를 식별하여 **사용 가능한 저장소** 그룹에 추가합니다.

```PowerShell
Get-ClusterAvailableDisk | Add-ClusterDisk
```

### <a name="add-a-disk-in-available-storage-to-csv"></a>사용 가능한 저장소의 디스크를 CSV에 추가

1. 장애 조치(Failover) 클러스터 관리자의 콘솔 트리에서 클러스터 이름을 확장 하 고 **저장소**를 확장 한 다음 **디스크**를 선택 합니다.
2. **사용 가능한 저장소**에 할당 된 디스크를 하나 이상 선택 하 고 선택 항목을 마우스 오른쪽 단추로 클릭 한 다음 **클러스터 공유 볼륨에 추가를**선택 합니다.

    이제 디스크가 클러스터의 **클러스터 공유 볼륨** 그룹에 할당됩니다. 이러한 디스크는 %SystemDisk %ClusterStorage 폴더 아래에 번호가 매겨진 볼륨(탑재 지점)으로 각 클러스터 노드에 노출됩니다. 볼륨은 CSVFS 파일 시스템에 표시됩니다.

>[!NOTE]
>%SystemDisk %ClusterStorage 폴더에서 CSV 볼륨의 이름을 바꿀 수 있습니다.

#### <a name="windows-powershell-equivalent-commands-add-a-disk-to-csv"></a>Windows PowerShell 해당 명령 (CSV에 디스크 추가)

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

다음 예제에서는 *사용 가능한 저장소*의 **Cluster Disk 1**을 로컬 클러스터의 CSV에 추가합니다.

```PowerShell
Add-ClusterSharedVolume –Name "Cluster Disk 1"
```

## <a name="enable-the-csv-cache-for-read-intensive-workloads-optional"></a>읽기 중심 워크로드에 CSV 캐시 사용(선택 사항)

CSV 캐시는 시스템 메모리(RAM)를 쓰기 캐시로 할당하여 버퍼링되지 않은 읽기 전용 I/O 작업의 블록 수준에서 캐시를 제공합니다. 버퍼링되지 않은 I/O 작업은 캐시 관리자에서 캐시되지 않습니다. 따라서 VHD에 액세스할 때 버퍼링되지 않은 I/O 작업을 수행하는 Hyper-V와 같은 응용 프로그램의 성능이 향상됩니다. CSV 캐시는 쓰기 요청을 캐시하지 않고도 읽기 요청의 성능을 높일 수 있습니다. CSV 캐시 사용은 스케일 아웃 파일 서버 시나리오에도 유용합니다.

>[!NOTE]
>클러스터된 모든 Hyper-V 및 스케일 아웃 파일 서버 배포에 CSV 캐시를 사용하는 것이 좋습니다.

기본적으로 Windows Server 2012에서는 CSV 캐시를 사용할 수 없습니다. Windows Server 2012 R2 이상에서는 CSV 캐시가 기본적으로 사용 하도록 설정 되어 있습니다. 그러나 여전히 예약할 블록 캐시의 크기를 할당해야 합니다.

다음 표에서는 CSV 캐시를 제어하는 두 가지 구성 설정을 설명합니다.

| Windows Server 2012 R2 이상 |  Windows Server 2012                 | 설명 |
| -------------------------------- | ------------------------------------ | ----------- |
| BlockCacheSize                   | SharedVolumeBlockCacheSizeInMB       | 클러스터의 각 노드에서 CSV 캐시용으로 예약할 메모리의 크기(MB)를 정의할 수 있는 클러스터의 공용 속성입니다. 예를 들어 값이 512로 정의된 경우 512MB의 시스템 메모리가 각 노드에 예약됩니다. 많은 클러스터에서 권장 되는 값은 512입니다. 기본 설정은 0 (사용 안 함)입니다. |
| EnableBlockCache                 | CsvEnableBlockCache                  | 클러스터 실제 디스크 리소스의 프라이빗 속성입니다. 이 속성을 통해 CSV에 추가된 개별 디스크에서 CSV 캐시를 사용하도록 설정할 수 있습니다. Windows Server 2012에서 기본 설정은 0 (사용 안 함)입니다. 디스크에서 CSV 캐시를 사용하려면 값을 1로 구성합니다. 기본적으로 Windows Server 2012 r 2에서는이 설정이 사용 됩니다. |

**클러스터 CSV 볼륨 캐시**아래에 카운터를 추가하여 성능 모니터에서 CSV 캐시를 모니터링할 수 있습니다.

#### <a name="configure-the-csv-cache"></a>CSV 캐시 구성

1. 관리자 권한으로 Windows PowerShell을 시작 합니다.
2. 각 노드에서 예약할 *512* MB의 캐시를 정의하려면 다음을 입력합니다.

    - Windows Server 2012 R2 이상:

        ```PowerShell
        (Get-Cluster).BlockCacheSize = 512  
        ```

    - Windows Server 2012의 경우:

        ```PowerShell
        (Get-Cluster).SharedVolumeBlockCacheSizeInMB = 512  
        ```
3. Windows Server 2012에서는 *클러스터 디스크 1*이라는 CSV에서 csv 캐시를 사용 하도록 설정 하려면 다음을 입력 합니다.

    ```PowerShell
    Get-ClusterSharedVolume "Cluster Disk 1" | Set-ClusterParameter CsvEnableBlockCache 1
    ```

>[!NOTE]
> * Windows Server 2012에서는 CSV 캐시에 총 실제 RAM의 20%만 할당할 수 있습니다. Windows Server 2012 R2 이상에서는 최대 80%까지 할당할 수 있습니다. 스케일 아웃 파일 서버에는 일반적으로 메모리 제한이 없으므로 CSV 캐시에 추가 메모리를 사용하여 성능을 크게 향상시킬 수 있습니다.
> * 리소스 경합을 방지 하려면 CSV 캐시에 할당 된 메모리를 수정한 후 클러스터의 각 노드를 다시 시작 해야 합니다. Windows Server 2012 R2 이상에서는 더 이상 다시 시작이 필요 하지 않습니다.
> * 개별 디스크에서 CSV 캐시를 사용하거나 사용하지 않도록 설정한 후 이 설정을 적용하려면 실제 디스크 리소스를 오프라인 상태로 전환했다가 다시 온라인 상태로 전환해야 합니다. 기본적으로 Windows Server 2012 R2 이상에서는 CSV 캐시가 사용 됩니다. 
> * 성능 카운터 정보를 포함하는 CSV 캐시에 대한 자세한 내용은 블로그 게시물 [CSV 캐시를 사용하도록 설정하는 방법](https://blogs.msdn.microsoft.com/clustering/2013/07/19/how-to-enable-csv-cache/)(영문)을 참조하세요.

## <a name="backing-up-csvs"></a>Csv 백업

장애 조치 (failover) 클러스터의 Csv에 저장 된 정보를 백업 하는 방법에는 여러 가지가 있습니다. Microsoft 백업 응용 프로그램 또는 타사 응용 프로그램을 사용할 수 있습니다. 일반적으로 CSV는 NTFS 또는 ReFS로 포맷된 클러스터된 저장소에 대한 요구 사항 외에 특별한 백업 요구 사항이 없습니다. 또한 CSV 백업은 다른 CSV 저장소 작업을 방해하지 않습니다.

백업 응용 프로그램 및 CSV에 대한 백업 일정을 선택할 때 다음과 같은 요소를 고려해야 합니다.

- CSV 볼륨의 볼륨 수준 백업은 해당 CSV 볼륨에 연결하는 모든 노드에서 실행할 수 있습니다.
- 백업 응용 프로그램에서는 소프트웨어 스냅샷 또는 하드웨어 스냅샷을 사용할 수 있습니다. 백업 응용 프로그램의 지원 여부에 따라 백업에서 응용 프로그램 일치 및 크래시 일치 VSS(볼륨 섀도 복사본 서비스) 스냅샷을 사용할 수 있습니다.
- 여러 가상 컴퓨터를 실행 중인 CSV를 백업하려면 일반적으로 관리 운영 체제 기반 백업 방법을 선택해야 합니다. 백업 응용 프로그램에서 지원하는 경우 여러 가상 컴퓨터를 동시에 백업할 수 있습니다.
- CSV는 Windows Server 2012 R2 백업, Windows Server 2012 백업 또는 Windows Server 2008 R2 백업을 실행 하는 백업 요청자를 지원 합니다. 그러나 Windows Server 백업에서는 일반적으로 많은 클러스터를 사용하는 조직에 적합하지 않을 수 있는 기본 백업 솔루션만 제공합니다. Windows Server Backup은 CSV에서 응용 프로그램 일치 Virtual Machine 백업을 지원하지 않습니다. 크래시 일치 볼륨 수준 백업만 지원합니다. 크래시 일치 백업을 복원하면 백업이 실행된 시점과 정확히 동일한 시점에 가상 컴퓨터의 작동이 중단된 경우 가상 컴퓨터가 당시와 동일한 상태에 있게 됩니다. CSV 볼륨에서 가상 컴퓨터의 백업에는 성공하지만 이는 지원되지 않음을 나타내는 오류 이벤트가 로깅됩니다.
- 장애 조치(failover) 클러스터를 백업할 때 관리 자격 증명이 필요할 수 있습니다.

> [!IMPORTANT]
>백업 응용 프로그램에서 백업 및 복원하는 데이터, 지원하는 CSV 기능 및 각 클러스터 노드의 응용 프로그램에 대한 리소스 요구 사항을 신중하게 검토해야 합니다.

> [!WARNING]
> 백업 데이터를 CSV 볼륨에 복원해야 하는 경우 클러스터 노드에서 응용 프로그램 일치 데이터를 유지 관리하고 복원하는 백업 응용 프로그램의 기능 및 제한 사항을 알아야 합니다. 예를 들어 일부 응용 프로그램에서는 CSV가 CSV 볼륨이 백업된 노드와 다른 노드에 복원된 경우 복원이 실행된 노드에서 응용 프로그램 상태에 대한 중요한 데이터를 실수로 덮어쓸 수도 있습니다.

## <a name="more-information"></a>자세한 정보

- [장애 조치(failover) 클러스터링](failover-clustering.md)
- [클러스터 된 저장소 공간 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11)>)