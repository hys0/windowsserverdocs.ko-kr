---
title: 장애 조치 클러스터의 클러스터 공유 볼륨을 사용 하 여
description: 장애 조치 클러스터의 클러스터 공유 볼륨을 사용 하는 방법입니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f5bd0ad05bdc2573a5ea0abbe165de2d3e7f5c8f
ms.sourcegitcommit: 375e94dc70c76e7aa5679c32f0f4dbc26cf7dd83
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2018
ms.locfileid: "2233519"
---
# <a name="use-cluster-shared-volumes-in-a-failover-cluster"></a>장애 조치 클러스터의 클러스터 공유 볼륨을 사용 하 여

>적용 대상: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

클러스터 공유 볼륨 (CSV) NTFS 볼륨으로 프로 비전 된 동일한 LUN (디스크)에 대 한 읽기 / 쓰기 액세스를 동시에 장애 조치 클러스터의 여러 노드를 사용 하도록 설정 합니다. (Windows Server 2012 r 2에서는 디스크 수를 구축할 수 NTFS 또는 복원 파일 시스템 (ReFS)로.) CSV와 클러스터 된 역할 수 장애 조치 신속 하 게 한 노드에서 다른 노드에 필요한 드라이브 소유권을 변경 하거나 분리 및 볼륨을 다시 탑재 하지 않고 합니다. CSV에는 장애 조치 클러스터의 Lun의 잠재적으로 많은 수의 관리를 단순화 데 도움이 됩니다.

CSV는 NTFS (또는 Windows Server 2012 r 2의 ReFS) 위에 계층화 하는 일반적인 용도의 클러스터 된 파일 시스템을 제공 합니다. CSV 응용 프로그램은 다음과 같습니다.

- 클러스터링 클러스터 된 Hyper-v 가상 컴퓨터에 대 한 가상 하드 디스크 (VHD) 파일
- 확장 파일 공유 확장 파일 서버 클러스터 된 역할에 대 한 응용 프로그램 데이터를 저장 합니다. 이 역할에 대 한 응용 프로그램 데이터의 예로 Hyper-v 가상 컴퓨터 파일 및 Microsoft SQL Server 데이터를 들 수 있습니다. (주의 ReFS 확장 파일 서버에 대 한 지원 되지 않습니다.) 파일 서버를 확장 하는 방법에 대 한 자세한 내용은 [응용 프로그램 데이터에 대 한 확장 파일 서버](sofs-overview.md)를 참조 하십시오.

>[!NOTE]
>CSV는 SQL Server 2012 및 이전 버전의 SQL Server에서 Microsoft SQL Server 클러스터 된 작업량을 지원 하지 않습니다.

Windows Server 2012에서 CSV 기능이 크게 향상 되었습니다. 예, Active Directory 도메인 서비스에 대 한 종속성이 제거 되었습니다. **Chkdsk**에서 기능 향상을 위한, 바이러스 백신 및 백업 응용 프로그램 상호 운용성을 위해 및 볼륨 BitLocker 암호화 및 저장소 공간 등의 일반 저장소 기능와의 통합에 대 한 지원이 추가 되었습니다. Windows Server 2012에 도입 된 CSV 기능의 개요를 참조 하십시오. [Windows Server 2012 \[redirected\에서 장애 조치 클러스터링의 새로운 기능을]](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265972(v%3dws.11)>)합니다.

Windows Server 2012 R2 분산된 CSV 소유권을 더 잘 CSV 캐시에 할당할 수 있는 실제 메모리 크기 보다 유연 하 게 서버 서비스의 가용성을 통해 향상 된 복구 등의 추가 기능을 소개 diagnosibility, 및 ReFS 및 중복 제거에 대 한 지원을 포함 하는 상호 운용성을 향상된 합니다. 자세한 내용은 [장애 조치 클러스터링의 새로운 기능](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265972(v%3dws.11)>)을 참조 하십시오.

>[!NOTE]
>가상 인프라 VDI (데스크톱) 시나리오에 대 한 CSV에서 데이터 중복 제거를 사용 하는 방법에 대 한 정보를 참조 [Windows Server 2012 r 2에서 VDI 저장소에 대 한 배포 데이터 중복 제거](https://blogs.technet.com/b/filecab/archive/2013/07/31/deploying-data-deduplication-for-vdi-storage-in-windows-server-2012-r2.aspx) 및 [확장 데이터 중복 제거는 블로그 게시물에 새 작업을 Windows Server 2012 R2](https://blogs.technet.com/b/filecab/archive/2013/07/31/extending-data-deduplication-to-new-workloads-in-windows-server-2012-r2.aspx)합니다.

## <a name="review-requirements-and-considerations-for-using-csv-in-a-failover-cluster"></a>요구 사항 및 장애 조치 클러스터에 CSV 사용 시 고려 사항 검토

장애 조치 클러스터에 CSV를 사용 하기 전에 네트워크, 저장소 및 기타 요구 사항 및이 섹션의 고려 사항 검토 합니다.

### <a name="network-configuration-considerations"></a>네트워크 구성 고려 사항

CSV을 지 원하는 네트워크를 구성 하는 경우 다음을 고려 하십시오.

- **여러 네트워크 및 다중 네트워크 어댑터**입니다. 네트워크에 오류가 발생할 때 내결함성의 사용 하도록 설정 하려면 여러 클러스터 네트워크 CSV 트래픽을 전달 하거나 네트워크 어댑터 협력 하 여 구성 하는 것이 좋습니다.
    
    클러스터 노드는 클러스터에 의해를 사용 하지 않아야 하는 네트워크로 연결 되 고 해제 해야 합니다. 예, 이러한 네트워크에서 CSV 트래픽을 방지 하기 위해 클러스터 사용에 대 한 iSCSI 네트워크를 사용 하지 않도록 설정 하는 것이 좋습니다. 장애 조치 클러스터 관리자에서 네트워크를 사용 하지 않으려면 **네트워크**를 선택, 네트워크를 선택, **속성** 작업을 선택한 후 선택 **이 네트워크에서 클러스터 네트워크 통신을 허용 하지 않습니다**. 또는 [Get ClusterNetwork](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusternetwork?view=win10-ps) Windows PowerShell cmdlet을 사용 하 여 네트워크의 **역할** 속성을 구성할 수 있습니다.
- **네트워크 어댑터 속성**입니다. 클러스터 통신을 수행 하는 모든 어댑터에 대 한 속성에서 다음 설정을 사용 하도록 설정 된 있는지를 확인 합니다.

  - **Microsoft Networks 용 클라이언트** 와 **파일 및 프린터 Microsoft Networks 용 공유**합니다. 이러한 설정은 SMB 서버 메시지 블록 () 3.0, 노드 간에 CSV 트래픽을 하기 위해 기본적으로 사용 되는 지원 합니다. SMB를 사용 하도록 설정 하는 서버 서비스와 워크스테이션 서비스가 실행 되 고 각 클러스터 노드에 자동으로 시작 하도록 구성 되었는지 확인 합니다.

    >[!NOTE]
    >Windows Server 2012 r 2의 장애 조치 클러스터 노드 당 여러 서버 서비스 인스턴스가 있습니다. 일반 파일 공유에 액세스 하는 SMB 클라이언트에서 들어오는 트래픽을 처리 하는 기본 인스턴스 간 노드 CSV 트래픽만 처리 하는 두번째 CSV 인스턴스. 또한 비정상 노드에서 서버 서비스 상태가 되 면, CSV 소유권 자동으로 사이 전환 다른 노드에 있습니다.

    SMB 3.0 하 고 원격 직접 메모리 액세스 (RDMA)를 지 원하는 네트워크 어댑터를 활용 하는 클러스터의 여러 네트워크를 통해 CSV 트래픽을 스트림에 SMB 다중 채널 및 SMB 직접 기능이 포함 됩니다. 기본적으로 SMB 다중 채널 CSV 트래픽에 사용 됩니다. 자세한 내용은 [서버 메시지 블록 개요](../storage/file-server/file-server-smb-overview.md)를 참조 하십시오.
  - **Microsoft 장애 조치 클러스터 가상 어댑터 성능 필터**입니다. 이 설정은 연결 오류 CSV 디스크에 직접 연결에서 노드를 방지 하는 경우 예, CSV, 도달 하기 위해 필요한 경우 I/O 리디렉션을 수행 하려면 노드 능력을 향상 시킵니다. 자세한 내용은이 항목 뒷부분에 나오는 [I/O에 대 한 동기화 및 CSV 통신의 I/O 리디렉션을](#about-i/o-synchronization-and-i/o-redirection-in-csv-communication) 참조 합니다.
- **클러스터 네트워크 우선순위를 지정**합니다. 일반적으로 클러스터 구성 하는 기본를 사용 하는 네트워크에 대 한 설정을 변경 하지 않는 것이 좋습니다.
- **IP 서브넷 구성**합니다. 네트워크에서 CSV를 사용 하는 노드에 대 한 필요한 특정 서브넷 구성은 하지 않습니다. CSV multisubnet 클러스터를 지원할 수 있습니다.
- **정책 기반 QoS (서비스) 품질**입니다. CSV를 사용 하면 QoS 우선순위 정책 및 각 노드에 대 한 네트워크 트래픽에 대 한 최소 대역폭 정책을 구성 하는 것이 좋습니다. 자세한 내용은 [의 QoS (서비스 품질)를](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831679(v%3dws.11)>)참조 하십시오.
- **저장소 네트워크**선택 합니다. 저장소 네트워크 권장 사항에 대 한 저장소 공급 업체에서 제공 되는 지침을 검토 합니다. CSV에 대 한 저장소에 대 한 추가 고려에 대 한이 항목 뒷부분에 나오는 [저장소 및 디스크 구성 요구 사항](#storage-and-disk-configuration-requirements) 를 참조 하십시오.

하드웨어, 네트워크 및 장애 조치 클러스터에 대 한 저장소 요구 사항 개요, [장애 조치 클러스터링 하드웨어 요구 사항 및 저장소 옵션을](clustering-requirements.md)참조 하십시오.

#### <a name="about-io-synchronization-and-io-redirection-in-csv-communication"></a>CSV 통신의 I/O 리디렉션 및 I/O 동기화 하는 방법에 대 한

- **I/O 동기화**: CSV 여러 노드가 동일한 공유 저장소에 대 한 동시 읽기 / 쓰기 액세스를 사용 하도록 설정 합니다. 노드에서 CSV 볼륨에 디스크 입/출력 (I/O)를 수행 하면 노드 통해 통신 하는 저장소를 사용 하 여 직접 등 저장 영역 네트워크 (SAN). 그러나 언제 든 지 단일 노드 (코디네이터 노드라고도 함) "소유 하 고" LUN와 연결 된 실제 디스크 리소스입니다. CSV 볼륨에 대 한 코디네이터 노드 **디스크**에서 **소유자 노드** 장애 조치 클러스터 관리자에 표시 됩니다. [Get ClusterSharedVolume](https://docs.microsoft.com/powershell/module/failoverclusters/get-clustersharedvolume?view=win10-ps) Windows PowerShell cmdlet의 출력에도 나타납니다.

  >[!NOTE]
  >Windows Server 2012 r 2에서는 CSV 소유권은 균등 하 게 각 노드를 소유 하는 CSV 볼륨의 수에 따라 장애 조치 클러스터 노드 간에 합니다. 또한 소유권은 자동으로 균형이 다시 조정 CSV 장애 조치 등 조건이, 노드 클러스터에 다시 가입, 클러스터에 새 노드를 추가, 클러스터 노드를 다시 시작 하거나 종료 한 후에 장애 조치 클러스터를 시작 합니다.

  CSV 볼륨에 파일 시스템에서 특정 작은 변경 되 면이 메타 데이터의 각 단일 코디네이터 노드에서 뿐아니라 LUN에 액세스 하는 실제 노드에 동기화 되어야 합니다. 예 CSV 볼륨에 가상 컴퓨터를 시작, 만든 하거나, 삭제할 때 또는 가상 컴퓨터를 마이그레이션할 때이 정보는 각 가상 컴퓨터에 액세스 하는 실제 노드의 동기화 해야 합니다. 이러한 메타 데이터 업데이트 작업이 발생할 병렬로 클러스터 네트워크를 통한 SMB 3.0을 사용 하 여. 이러한 작업에 공유 저장소와 통신 하는 모든 실제 노드를 사용할 필요가 없습니다.

- **I/O 리디렉션**: 저장소 연결 오류 및 특정 저장소 작업 저장소와 직접 통신에서 지정 된 노드를 방지할 수 있습니다. 노드를 유지 하기 위해 함수는 노드는 저장소와 통신 하지 않는 하는 동안 디스크를 탑재 현재 코디네이터 노드 클러스터 네트워크를 통해 디스크를 입/출력 리디렉션합니다. 현재 코디네이터 노드 오류가 발생 한 저장소 연결, 코디네이터 노드로 새 노드를 설정 하는 동안에 일시적으로 모든 디스크 I/O 작업은 대기 됩니다.

서버 상황에 따라 다음과 같은 I/O 리디렉션 모드 중 하나를 사용 합니다.

- **파일 시스템 리디렉션** 리디렉션 / 볼륨은 — 등 때 CSV 스냅숏을 때 수행 되는 백업 응용 프로그램에서 CSV 볼륨 리디렉션된 I/O 모드에 수동으로 배치 됩니다.
- **블록 리디렉션** 리디렉션 파일 블록 수준에서은 — 저장소 연결에는 볼륨 손실 됩니다 예입니다. 블록 리디렉션 파일 시스템 리디렉션 보다 훨씬 빠릅니다.

Windows Server 2012 r 2에서는 당 노드 별로 CSV 볼륨의 상태를 볼 수 있습니다. 예, 직접 또는 리디렉션된, I/O 인지 또는 CSV 볼륨은 사용할 수 있는지 여부를 볼 수 있습니다. CSV 볼륨 I/O 리디렉션된 모드인 경우에 이유를 볼 수 있습니다. **Get ClusterSharedVolumeState** Windows PowerShell cmdlet를 사용 하 여이 정보를 볼 수 있습니다.

>[!NOTE]
> * Windows Server 2012에서 CSV 디자인의 향상 된 기능으로 인해 CSV 보다 작업을 수행할 직접 I/O 모드에서 Windows Server 2008 r 2에서 오류가 발생 했습니다 보다 합니다.
> * 예: SMB 다중 채널 및 SMB 직접 SMB 3.0 기능으로 CSV의 통합을로 인해 리디렉션된 I/O 트래픽이 여러 클러스터 네트워크를 통해 스트리밍할 수 있습니다.
> * I/O 리디렉션 하는 동안 네트워크 트래픽이 코디네이터 노드로 잠재적인 증가 대 한 허용 하도록 클러스터 네트워크를 계획 해야 합니다.

### <a name="storage-and-disk-configuration-requirements"></a>저장소 및 디스크 구성 요구 사항

저장소 및 디스크 CSV을 사용 하려면 다음 요구 사항을 충족 해야 합니다.

- **파일 시스템 형식**입니다. Windows Server 2012 r 2에서는 CSV 볼륨에 대 한 디스크 또는 저장소 공간 NTFS 또는 ReFS 분할 된 기본 디스크 이어야 합니다. Windows Server 2012에서 CSV 볼륨에 대 한 디스크 또는 저장소 공간 NTFS로 분할 된 기본 디스크 이어야 합니다.

  CSV에는 다음과 같은 추가 요구 사항에 있습니다.
    
  - Windows Server 2012 r 2에서는 FAT 또는 FAT32 서식이 지정 된 CSV에 대 한 디스크를 사용할 수 없습니다.
  - Windows Server 2012 FAT, FAT32 또는 ReFS 서식 있는 CSV에 대 한 디스크를 사용할 수 없습니다.
  - CSV에 대 한 저장 공간을 사용 하려는 경우에 간단한 공간 또는 미러 공간을 구성할 수 있습니다. Windows Server 2012 r 2에서는 패리티 공간을 구성할 수도 있습니다. (Windows Server 2012에서 CSV 지원 하지 않습니다 패리티 공백을.)
  - CSV 쿼럼 미러링 모니터 서버 디스크로 사용할 수 없습니다. 클러스터 쿼럼에 대 한 자세한 내용은 [저장소 공간 직접에서 이해 쿼럼](../storage/storage-spaces/understand-quorum.md)를 참조 하십시오.
  - CSV로 디스크를 추가한 후 CSVFS 형식에서 (CSV 파일 시스템)에 대 한 지정 됩니다. 이렇게 하면 클러스터 및 기타 소프트웨어에서 다른 NTFS CSV 저장소 또는 ReFS 저장소를 구분할 수 있습니다. 일반적으로 CSVFS NTFS 또는 ReFS와 동일한 기능을 지원합니다. 그러나 일부 기능은 지원 되지 않습니다. 예, Windows Server 2012 r 2에서는 CSV에 압축을 사용할 수 없습니다. Windows Server 2012 데이터 중복 제거 또는 CSV에 압축을 활성화할 수 없습니다.
- **클러스터의 자원 종류**입니다. CSV 볼륨에 대 한 실제 디스크 리소스 종류를 사용 해야 합니다. 기본적으로 클러스터 저장소에 추가 되는 디스크 또는 저장소 공간 이와 같은 방식으로 자동으로 구성 됩니다.
- **선택의 CSV 디스크 또는 클러스터 저장소의 다른 디스크**합니다. 클러스터 된 가상 컴퓨터에 대 한 하나 이상의 디스크를 선택 하는 경우에 각 디스크를 사용할 방법 하는 것이 좋습니다. 디스크를 사용 하 여 구성 파일, VHD 파일 등 Hyper-v, 하 여 만든 파일을 저장 하는 경우에 CSV 디스크 또는 클러스터 저장소의 사용 가능한 디스크에서 선택할 수 있습니다. 디스크를 직접 되는 실제 디스크 수 없는 경우 CSV 디스크를 선택할 수는 없습니다 (통과 디스크 라고도 함)이 가상 컴퓨터에 연결 된 및 클러스터 저장소의 사용 가능한 디스크를 선택 해야 합니다.
- **디스크를 식별 하는 것에 대 한 경로 이름**입니다. CSV에서 디스크 경로 이름으로 식별 됩니다. 각 경로 **\\ClusterStorage** 폴더에서 번호가 매겨진된 볼륨으로 노드의 시스템 드라이브에 있는 것으로 표시 됩니다. 이 경로 클러스터의 모든 노드에서 볼 때 동일 합니다. 필요한 경우 볼륨의 이름을 바꿀 수 있습니다.

CSV에 대 한 저장소 요구 사항에 대 한 저장소 공급 업체에서 제공 되는 지침을 검토 합니다. CSV에 대 한 계획 고려 사항 추가 저장소에 대 한이 항목 뒷부분의 [장애 조치 클러스터에 CSV를 사용 하 여 계획](#plan-to-use-csv-in-a-failover-cluster) 을 참조 하십시오.

### <a name="node-requirements"></a>노드 요구 사항

CSV를 사용 하 여 노드 다음 요구 사항을 충족 해야 합니다.

- **드라이브 시스템 디스크의 문자**입니다. 모든 노드에서 시스템 디스크에 대 한 드라이브 문자는 동일 해야 합니다.
- **인증 프로토콜**입니다. NTLM 프로토콜 모든 노드에 대해 활성화 되어야 합니다. 기본적으로 사용 하도록 설정 됩니다.

## <a name="plan-to-use-csv-in-a-failover-cluster"></a>장애 조치 클러스터에 CSV를 사용 하 여 계획

이 섹션에는 계획 고려 사항 및 Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 장애 조치 클러스터에 CSV를 사용 하기 위한 권장 사항을 나열 합니다.

>[!IMPORTANT]
>CSV에 대 한의 특정 저장 장치를 구성 하는 방법에 대 한 권장 사항에 대 한 저장소 공급 업체에 문의 함 저장소 공급 업체에서 권장 사항은이 항목의 정보를 다를 경우에 저장소 공급 업체에서 권장 사항을 사용 합니다.

### <a name="arrangement-of-luns-volumes-and-vhd-files"></a>Lun, 볼륨 및 VHD 파일의 정렬

클러스터 된 가상 컴퓨터에 대 한 저장소를 제공 하는 CSV를 최대한 활용 하려면 실제 서버를 구성할 때 Lun (디스크)을 정리 하듯이 방법을 검토 하는 것이 좋습니다. 해당 가상 컴퓨터를 구성 하는 경우 유사한 방식으로 VHD 파일을 정렬 하려고 합니다.

실제 서버를를 정리 하는 것은 디스크 및 파일 다음과 같은 것이 좋습니다.

- 시스템 파일을 하나의 실제 디스크에 있는 페이지 파일을 포함 하 여
- 다른 실제 디스크에 데이터 파일

해당 하는 클러스터 된 가상 컴퓨터에 대 한 볼륨 및 파일 유사한 방식으로 구성 해야 합니다.

- 시스템 파일을 하나의 CSV에서 VHD 파일에서 페이지 파일을 포함 하 여
- 다른 CSV에서 VHD 파일에서 데이터 파일

가능한 경우 다른 가상 컴퓨터를 추가 하는 경우에 해당 가상 컴퓨터에서 Vhd에 대 한 동일한 정렬을 유지 해야 합니다.

### <a name="number-and-size-of-luns-and-volumes"></a>Lun 및 볼륨의 수 및 크기

CSV를 사용 하는 장애 조치 클러스터에 대 한 저장소 구성과 계획할 때 다음 권장 사항을 고려 합니다.

- 구성, 저장소 공급 업체에 문의에 얼마나 많은 Lun을 결정 합니다. 예, 저장소 공급 업체에 문의 파티션 하나를 사용 하 여 각 LUN을 구성 하 고 하나의 CSV 볼륨에 배치 하는 것이 좋습니다 될 수 있습니다.
- 단일 CSV 볼륨에 지원할 수 있는 가상 컴퓨터의 수에 대 한 제한은 없습니다. 그러나 클러스터 및 각 가상 컴퓨터에 대 한 작업량 (초당 I/O 작업 수)에서 계획 하는 가상 컴퓨터 수를 고려해 야 합니다. 다음 예를 참조하세요.

  - 하나의 조직 하 고 비교적 간단 작업량에 해당 하는 가상 데스크톱 인프라 (VDI)를 지원 되는 가상 컴퓨터를 배포 합니다. 클러스터는 고성능 저장소를 사용 합니다. 클러스터 관리자가 저장소 공급 업체와을 조사한 후 하기로 결정 비교적 많은 CSV 볼륨당 가상 컴퓨터를 배치 합니다.
  - 다른 조직 많은 수의 가상 컴퓨터를 지 원하는 두꺼운 작업은 많이 사용 되는 데이터베이스 응용 프로그램을 구축 하 고 있습니다. 클러스터 아래 수행 저장소를 사용 합니다. 클러스터 관리자가 저장소 공급 업체와을 조사한 후 하기로 결정 비교적 적은 수의 CSV 볼륨당 가상 컴퓨터를 배치 합니다.
- 특정 가상 컴퓨터에 대 한 저장소 구성을 계획할 때는 서비스, 응용 프로그램 또는 가상 컴퓨터에서 지 원하는 역할의 디스크 요구 사항을 고려해 야 합니다. 이러한 요구 사항을 이해 하면 성능이 저하 될 수 있는 디스크 경합을 방지 합니다. 가상 컴퓨터에 대 한 저장소 구성과를 밀접 하 게 동일한 서비스, 응용 프로그램 또는 역할을 실행 하는 실제 서버에 대해 사용할 수 있는 저장소 구성과 비슷합니다. 자세한 내용은이 항목의 앞부분에서 [정렬의 Lun, 볼륨 및 VHD 파일을](#arrangement-of-luns,-volumes,-and-vhd-files) 참조 합니다.

    또한 독립 실제 하드 디스크의 많은 수의 저장소 하 여 디스크 경합을 줄일 수 있습니다. 저장소 하드웨어를 적절 하 게 선택 하 고 사용자 저장소의 성능을 최적화 하기 위해 공급 업체 문의 하십시오.
- 클러스터 작업 및 I/O 작업에 대 한 자신의 요구에 따라 다른 가상 컴퓨터 연결 하지 않은 전용 작업을 계산 하는 대신 하는 동안 각 LUN에 액세스 하려면 가상 컴퓨터의 백분율로 구성 고려할 수 있습니다.

## <a name="add-a-disk-to-csv-on-a-failover-cluster"></a>장애 조치 클러스터에서 디스크를 CSV로 추가

CSV 기능 장애 조치 클러스터링에 기본적으로 활성화 됩니다. 디스크를 CSV로를 추가 하려면 디스크 (것 추가 되지 않은 경우 이미) 클러스터의 **사용 가능한 저장소** 그룹에 추가 하 고 클러스터에서 CSV로 디스크를 추가 해야 합니다. 이러한 절차를 수행 하려면 장애 조치 클러스터 관리자 또는 장애 조치 클러스터 Windows PowerShell cmdlet을 사용할 수 있습니다.

### <a name="add-a-disk-to-available-storage"></a>디스크 사용 가능한 저장소를 추가

1. 장애 조치 클러스터 관리자에서 콘솔 트리에 클러스터의 이름을 확장 하 고 **저장소**를 확장 합니다.
2. **디스크**마우스 오른쪽 단추로 클릭 하 고 **추가 디스크**를 선택 합니다. 장애 조치 클러스터에 사용 하기 위해 추가할 수 있는 디스크를 보여주는 프로그램 목록이 나타납니다.
3. 디스크 또는 디스크를 추가 하려면 선택한 다음 **확인**을 선택 합니다.

    디스크는 이제 **사용 가능한 저장소** 그룹에 할당 됩니다.

#### <a name="windows-powershell-equivalent-commands-add-a-disk-to-available-storage"></a>Windows PowerShell에 해당 명령 (디스크 사용 가능한 저장소를 추가 하는)

다음 Windows PowerShell cmdlet 또는 cmdlet 위 절차와 동일한 기능을 수행 합니다. 수 나타나는 여러 줄 여기에서 바꿈 서식 제약 조건으로 인해 하는 경우에 각 cmdlet과 관련 한 줄에 입력 합니다.

클러스터에 추가 될 수 있는 디스크를 식별 하 고 **사용 가능한 저장소** 그룹에 추가 하는 해당 하는 다음 예제입니다.

```PowerShell
Get-ClusterAvailableDisk | Add-ClusterDisk
```

### <a name="add-a-disk-in-available-storage-to-csv"></a>사용 가능한 저장소에서 디스크를 CSV로 추가

1. 장애 조치 클러스터 관리자에서 콘솔 트리에서 클러스터의 이름을 확장 하 고, **저장소**를 확장 하 고, **디스크**를 선택 합니다.
2. 하나를 선택 하거나 더 많은 디스크 **사용 가능한 저장소**할당 된 다음은 선택 영역을 마우스 오른쪽 단추로 클릭 하 고 **클러스터 공유 볼륨에 추가**선택 합니다.

    이제 디스크는 클러스터의 **클러스터 공유 볼륨** 그룹에 할당 됩니다. 디스크 % SystemDisk %ClusterStorage 폴더에서 번호가 매겨진된 볼륨 (탑재 지점)으로 각 클러스터 노드에 노출 됩니다. 볼륨은 CSVFS 파일 시스템에 표시 됩니다.

>[!NOTE]
>CSV 볼륨 % SystemDisk %ClusterStorage 폴더의 이름을 바꿀 수 있습니다.

#### <a name="windows-powershell-equivalent-commands-add-a-disk-to-csv"></a>Windows PowerShell에 해당 명령 (디스크를 CSV로 추가)

다음 Windows PowerShell cmdlet 또는 cmdlet 위 절차와 동일한 기능을 수행 합니다. 수 나타나는 여러 줄 여기에서 바꿈 서식 제약 조건으로 인해 하는 경우에 각 cmdlet과 관련 한 줄에 입력 합니다.

다음 예제에서는 *클러스터 디스크 1* **사용 가능한 저장소** 에서 CSV 로컬 클러스터에 추가합니다.

```PowerShell
Add-ClusterSharedVolume –Name "Cluster Disk 1"
```

## <a name="enable-the-csv-cache-for-read-intensive-workloads-optional"></a>(선택 사항) 읽기를 많이 사용 작업에 대 한 CSV 캐시를 사용 하도록 설정

CSV 캐시 쓰기 통해 캐시로 시스템 메모리 (RAM)를 할당 하 여 읽기 전용 버퍼링 되지 않은 I/O 작업의 블록 수준에서 캐싱을 제공 합니다. (버퍼링 되지 않은 I/O 작업 캐시 관리자에 의해 캐시 되지 않습니다.) Hyper-v, VHD에 액세스할 때 버퍼링 되지 않은 I/O 작업을 수행 하는 등의 응용 프로그램에 대 한 성능을 향상 시킬 수이. CSV 캐시 쓰기 요청 캐싱을 사용 하지 않고 읽기 요청의 성능을 높일 수 있습니다. CSV 캐시를 사용 하면 해당 확장 파일 서버 시나리오에도 유용 합니다.

>[!NOTE]
>클러스터 된 모든 Hyper-v 및 확장 파일 서버 배포에 대 한 CSV 캐시를 사용 하도록 설정 하는 것이 좋습니다.

Windows Server 2012에는 기본적으로 CSV 캐시를 사용할 수 없습니다. Windows Server 2012 r 2에서는 CSV 캐시는 기본적으로 활성화 됩니다. 그러나를 예약 하기 위해 블록 캐시의 크기 여전히 할당 해야 합니다.

다음 표에서 CSV 캐시를 제어 하는 두 구성 설정을 설명 합니다.

<table>
<thead>
<tr class="header">
<th>Windows Server 2012 r 2의 속성 이름</th>
<th>Windows Server 2012의에서 속성 이름</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>BlockCacheSize</strong></td>
<td><strong>SharedVolumeBlockCacheSizeInMB</strong></td>
<td>각 클러스터 노드에 대해 CSV 캐시에 대 한 예약 하기 위해 메모리 양을 메가바이트 단위로 정의할 수 있도록 하는 클러스터 공통 속성입니다. 예, 512의 값을 정의 하는 경우 512MB 시스템 메모리의 각 노드에 예약 됩니다. (많은 클러스터에서 512MB 권장된 값입니다.) 기본 설정은 0 (사용 안함) 해야 합니다.</td>
</tr>
<tr class="even">
<td><strong>EnableBlockCache</strong></td>
<td><strong>CsvEnableBlockCache</strong></td>
<td>실제 디스크 리소스는 클러스터의 개인 속성입니다. CSV에 추가 되는 개별 디스크에 CSV 캐시를 사용 하도록 설정 하면 수 있습니다. Windows Server 2012의 기본 설정은 0 (사용 안함) 해야 합니다. 디스크에 CSV 캐시를 사용 하도록 설정 하려면 1의 값을 구성 합니다. 기본적으로 Windows Server 2012 r 2에서는이 설정을 사용 합니다.</td>
</tr>
</tbody>
</table>

**클러스터 CSV 볼륨 캐시**에서 카운터를 추가 하 여 성능 모니터에서 CSV 캐시를 모니터링할 수 있습니다.

#### <a name="configure-the-csv-cache"></a>CSV 캐시를 구성 합니다.

1. 관리자 권한으로 Windows PowerShell을 시작 합니다.
2. *512* MB 각 노드에 대해 예약 된 수의 캐시를 정의 하려면 다음을 입력 합니다.

    - Windows Server 2012 r 2:

        ```PowerShell
        (Get-Cluster).BlockCacheSize = 512  
        ```

    - Windows server 2012의 경우

        ```PowerShell
        (Get-Cluster).SharedVolumeBlockCacheSizeInMB = 512  
        ```
3. Windows Server 2012 *클러스터 디스크 1*이라는 CSV에서 CSV 캐시를 사용 하도록 설정 하려면 다음을 입력 합니다.

    ```PowerShell
    Get-ClusterSharedVolume "Cluster Disk 1" | Set-ClusterParameter CsvEnableBlockCache 1
    ```

>[!NOTE]
> * Windows Server 2012에서 CSV 캐시에 총 실제 RAM의 20%만 할당할 수 있습니다. Windows Server 2012 r 2의 80%까지를 할당할 수 있습니다. 파일 서버를 확장 하지 않으므로 일반적으로 제한 하는 메모리, CSV 캐시에 대 한 추가 메모리를 사용 하 여 큰 성능 향상을 수행할 수 있습니다.
> * 리소스 경합을 방지 하려면 다시 시작 해야 각 노드 클러스터의 후 CSV 캐시에 할당 되는 메모리를 수정 합니다. Windows Server 2012 r 2의 컴퓨터를 다시 시작 필요 하지 않습니다.
> * 사용 하도록 설정 하거나 설정을 적용 하려면 적용을 개별 디스크에 CSV 캐시를 사용 하지 않도록 한 후에 실제 디스크 리소스를 오프 라인으로 수행 하 고 다시 온라인 해야 합니다. (기본적으로 Windows Server 2012 r 2에서는 CSV 캐시가 사용 되 고 있습니다.) 
> * CSV 캐시 성능 카운터에 대 한 정보를 포함 하는 방법에 대 한 자세한 내용은 블로그 게시물 [CSV 캐시를 사용 하도록 설정 하는 방법](https://blogs.msdn.microsoft.com/clustering/2013/07/19/how-to-enable-csv-cache/)을 참조 하십시오.

## <a name="back-up-csv"></a>CSV 백업

장애 조치 클러스터에 CSV에 저장 된 정보를 백업 하는 방법은 여러 가지가 있습니다. Microsoft 백업 응용 프로그램 또는 비 Microsoft 응용 프로그램을 사용할 수 있습니다. 일반적으로 CSV NTFS 또는 ReFS로 서식이 지정 된 클러스터 된 저장소에 대 한 것 이외의 특별 한 백업 요구를 발생 하지 않습니다. 또한 CSV 백업을 다른 CSV 저장소 작업을 방해 하지 않는 합니다.

백업 응용 프로그램 및 CSV에 대 한 백업 일정을 선택 하면 다음과 같은 요인을 고려해 야 합니다.

- CSV 볼륨에 연결 하는 모든 노드에서 CSV 볼륨의 볼륨 수준 백업을 실행할 수 있습니다.
- 백업 응용 프로그램 소프트웨어 스냅숏 또는 하드웨어 스냅숏을 사용할 수 있습니다. 지원 하도록 백업 응용 프로그램의 기능을 따라 백업을 응용 프로그램 일관적이 고 일관성 있는 충돌에 해당 하는 볼륨 섀도 복사본 서비스 (VSS)의 스냅숏을 사용할 수 있습니다.
- 여러 실행 중인 가상 컴퓨터에 있는 CSV를 백업 하는 경우 해야 일반적으로 하는 관리 운영 체제 기반 백업 방법을 선택 합니다. 백업 응용 프로그램에서 지 원하는 경우 여러 가상 컴퓨터를 백업할 수 있습니다 동시에 있습니다.
- CSV는 Windows Server 2012 R2 백업, Windows Server 2012 백업 또는 Windows Server 2008 R2 백업을 실행 하는 백업 요청자를 지원 합니다. 그러나 Windows Server 백업 일반적으로 기본 백업 있는 솔루션을 제공 조직 더 큰 클러스터에 대 한 적합 한 수 있습니다. Windows Server 백업은 CSV에서 응용 프로그램으로 일관 된 가상 컴퓨터 백업을 지원 하지 않습니다. 크래시 일관성 있는 볼륨 수준 백업만을 지원합니다. (크래시 일관 된 백업, 복원 하는 경우 가상 컴퓨터 됩니다 가상 컴퓨터 명의 백업을 수행한 정확 하 게 지금은 작동 중단 하는 경우 전과 동일한 상태로.) CSV 볼륨에 가상 컴퓨터의 백업을 테스트가 성공 하지만 지원 되지 않습니다이 나타내는 오류 이벤트가 기록 됩니다.
- 장애 조치 클러스터를 백업 하는 경우 관리 자격 증명을 필요할 수 있습니다.

>[!IMPORTANT]
>노드를 클러스터 하는 각 응용 프로그램에 대 한 리소스 요구 사항 및 신중 하 게 데이터를 검토 하려면 백업 응용 프로그램 백업 및 복원를 지 원하는 CSV 기능을 확인 해야 합니다.

>[!WARNING]
>CSV 볼륨에 백업 데이터를 복원 해야하는 경우에 기능 및 유지 관리 하 고 클러스터 노드 간에 일관 된 응용 프로그램 데이터를 복원 하려면 백업 응용 프로그램의 제한 사항에 유의 합니다. 등 일부 응용 프로그램에서 CSV 여기서 CSV 볼륨 백업한, 노드에서 다른 노드에서 복원 되 면 있습니다 덮어쓸 수 있습니다 실수로 여기서 복원을 수행 중이면 노드에서 응용 프로그램 상태에 대 한 중요 한 데이터.

## <a name="more-information"></a>자세한 정보

- [장애 조치(failover) 클러스터링](failover-clustering.md)
- [클러스터 된 저장소 공간을 배포 합니다.](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11)>)