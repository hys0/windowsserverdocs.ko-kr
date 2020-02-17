---
title: 'DFS 복제: FAQ(질문과 대답)'
ms.date: 06/18/2014
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: e92ada07140b88ef4178a5aecdb263b825380c2d
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950280"
---
# <a name="dfs-replication-frequently-asked-questions-faq"></a>DFS 복제: FAQ(질문과 대답)


업데이트됨: 2019년 4월 30일

적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

이 FAQ에서는 Windows Server용 DFS(분산 파일 시스템) 복제(DFS-R 또는 DFSR이라고도 함)에 대한 질문에 답변합니다.

DFS 네임스페이스에 대한 자세한 내용은 [DFS 네임스페이스: 질문과 대답](https://technet.microsoft.com/library/ee404780)을 참조하세요.

DFS 복제의 새로운 기능에 대한 자세한 내용은 다음 항목을 참조하세요.

  - [DFS 네임스페이스 및 DFS 복제 개요](https://technet.microsoft.com/library/jj127250)(Windows Server 2012)  
      
  - [Windows Server 2008에서 Windows Server 2008 R2로 기능 변경](https://technet.microsoft.com/library/dd391932)의 [분산 파일 시스템 항목의 새로운 기능](https://technet.microsoft.com/library/ee307957) 항목  
      
  - [Windows Server 2003 SP1에서 Windows Server 2008로 기능 변경](https://technet.microsoft.com/library/cc753208)의 [분산 파일 시스템](https://technet.microsoft.com/library/cc753479) 항목  
      

이 항목에 대한 최근 변경 내용 목록은 이 항목의 [변경 내용](#change-history) 섹션을 참조하세요.

      

## <a name="interoperability"></a>상호 운용성

### <a name="can-dfs-replication-communicate-with-frs"></a>DFS 복제에서 FRS와 통신할 수 있나요?

아니요. DFS 복제는 FRS(파일 복제 서비스)와 통신하지 않습니다. DFS 복제와 FRS는 동일한 서버에서 동시에 실행될 수 있지만, 이 경우 데이터가 손실될 수 있으므로 동일한 폴더 또는 하위 폴더를 복제하도록 구성하면 안 됩니다.

### <a name="can-dfs-replication-replace-frs-for-sysvol-replication"></a>DFS 복제는 SYSVOL 복제를 위해 FRS를 대체할 수 있나요?

예, DFS 복제는 SYSVOL 복제를 위해 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008을 실행하는 서버에서 FRS를 대체할 수 있습니다. Windows Server 2003 R2를 실행하는 서버는 DFS 복제를 사용하여 SYSVOL 폴더를 복제할 수 없습니다.

DFS 복제를 사용하여 SYSVOL을 복제하는 방법에 대한 자세한 내용은 [SYSVOL 복제 마이그레이션 가이드: FRS에서 DFS 복제로](https://technet.microsoft.com/library/dd640019)를 참조하세요.

### <a name="can-i-upgrade-from-frs-to-dfs-replication-without-losing-configuration-settings"></a>구성 설정을 손실하지 않고 FRS에서 DFS 복제로 업그레이드할 수 있나요?

예. 복제를 FRS에서 DFS 복제로 마이그레이션하려면 다음 문서를 참조하세요.

  - SYSVOL 폴더 이외의 폴더 복제를 마이그레이션하려면 [DFS 작업 가이드: FRS에서 DFS 복제로 마이그레이션](https://go.microsoft.com/fwlink/?linkid=192776) 및 [FRS2DFSR – FRS에서 DFSR로 마이그레이션 유틸리티](https://go.microsoft.com/fwlink/?linkid=195437)(https://go.microsoft.com/fwlink/?LinkID=195437) 를 참조하세요.  
      
  - SYSVOL 폴더 복제를 DFS 복제로 마이그레이션하려면 [SYSVOL 복제 마이그레이션 가이드: FRS에서 DFS 복제로](https://technet.microsoft.com/library/dd640019)를 참조하세요.  
      

### <a name="can-i-use-dfs-replication-in-a-mixed-windowsunix-environment"></a>Windows/UNIX 혼합 환경에서 DFS 복제를 사용할 수 있나요?

예. DFS 복제는 Windows Server를 실행하는 서버 간의 콘텐츠만 복제하도록 지원하지만, UNIX 클라이언트는 Windows Server의 파일 공유에 액세스할 수 있습니다. 이렇게 하려면 DFS 복제 서버에 NFS(네트워크 파일 시스템)용 서비스를 설치합니다.

또한 많은 UNIX 클라이언트에 포함된 SMB/CIFS 클라이언트 기능을 사용하여 Windows 파일 공유에 직접 액세스할 수도 있습니다. 그러나 이 기능은 제한적이거나 Windows 환경을 수정해야 하는 경우가 많습니다(예: 그룹 정책을 사용하여 SMB 서명을 사용하지 않도록 설정).

DFS 복제는 Windows Server 운영 체제를 실행하는 서버에서 NFS와 상호 운용되지만, NFS 탑재 지점은 복제할 수 없습니다.

### <a name="can-i-use-the-volume-shadow-copy-service-with-dfs-replication"></a>DFS 복제에서 볼륨 섀도 복사본 서비스를 사용할 수 있나요?

예. DFS 복제는 VSS(볼륨 섀도 복사본 서비스) 볼륨에서 지원되며, 이전 버전의 클라이언트를 사용하여 이전 스냅샷을 성공적으로 복원할 수 있습니다.

### <a name="can-i-use-windowsbackup-ntbackupexe-to-remotely-back-up-a-replicated-folder"></a>Windows 백업(Ntbackup.exe)을 사용하여 복제된 폴더를 원격으로 백업할 수 있나요?

아니요, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008을 실행하는 컴퓨터에서 복제된 폴더의 콘텐츠는 Windows Server 2003 이하를 실행하는 컴퓨터에서 Windows 백업(Ntbackup.exe)을 사용하여 백업할 수 없습니다.

저장된 파일을 복제된 폴더에 백업하려면 Windows Server 백업 또는 Microsoft® System Center Data Protection Manager를 사용합니다. Windows Server 2008 R2 및 Windows Server 2008의 백업 및 복구 기능에 대한 자세한 내용은 [백업 및 복구](https://technet.microsoft.com/library/Cc754097)를 참조하세요. 자세한 내용은 [System Center Data Protection Manager](https://go.microsoft.com/fwlink/?linkid=182261)(https://go.microsoft.com/fwlink/?LinkId=182261) 를 참조하세요.

### <a name="do-file-system-policies-impact-dfs-replication"></a>파일 시스템 정책이 DFS 복제에 영향을 주나요?

예. 복제된 폴더에 대한 파일 시스템 정책을 구성하지 않습니다. 파일 시스템 정책은 그룹 정책 새로 고침 간격마다 NTFS 권한을 다시 적용합니다. 이 경우 파일을 닫을 때까지 열려 있는 파일이 복제되지 않으므로 공유 위반이 발생할 수 있습니다.

### <a name="does-dfs-replication-replicate-mailboxes-hosted-on-microsoft-exchange-server"></a>DFS 복제는 Microsoft Exchange Server에서 호스팅되는 사서함을 복제하나요?

아니요. DFS 복제는 Microsoft Exchange Server에서 호스팅되는 사서함을 복제하는 데 사용할 수 없습니다.

### <a name="does-dfs-replication-support-file-screens-created-by-file-server-resource-manager"></a>DFS 복제는 파일 서버 리소스 관리자에서 만든 파일 차단을 지원하나요?

예. 그러나 FSRM(파일 서버 리소스 관리자) 파일 차단 설정은 복제의 양쪽 끝에서 일치해야 합니다. 또한 DFS 복제에는 복제에서 특정 파일 및 파일 형식을 제외하는 데 사용할 수 있는 파일 및 폴더에 대한 자체의 필터 메커니즘이 있습니다.

파일 차단 또는 할당량을 구현하기 위한 모범 사례는 다음과 같습니다.

  - 숨겨진 DfsrPrivate 폴더에는 할당량 또는 파일 차단이 적용되지 않아야 합니다.  
      
  - 차단을 사용하도록 설정하기 전에 차단된 파일이 복제된 폴더에 없어야 합니다.  
      
  - 할당량을 사용하도록 설정하기 전에 폴더는 할당량을 초과할 수 없습니다.  
      
  - 하드 할당량은 신중하게 사용해야 합니다. 복제 그룹의 개별 멤버는 복제하기 전에 할당량 내에서 유지될 수 있지만, 파일이 복제될 때는 이를 초과할 수 있습니다. 예를 들어 사용자가 10MB(메가바이트) 파일을 서버 A에 복사하고 다른 사용자가 5MB 파일을 서버 B에 복사하는 경우 다음에 복제를 수행할 때 두 서버에서 모두 할당량을 5MB 초과하게 됩니다. 이로 인해 DFS 복제에서 파일 복제를 지속적으로 다시 시도하여 버전 벡터 결함 및 성능 문제가 발생할 수 있습니다.  
      

### <a name="is-dfs-replication-cluster-aware"></a>DFS 복제 클러스터가 인식되나요?

예, Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 R2의 DFS 복제에는 장애 조치 클러스터를 복제 그룹의 멤버로 추가하는 기능이 포함되어 있습니다. 자세한 내용은 [복제 그룹에 장애 조치 클러스터 추가](https://go.microsoft.com/fwlink/?linkid=155085)(https://go.microsoft.com/fwlink/?LinkId=155085) 를 참조하세요. Windows Server 2008 R2 이전 버전의 Windows에서 DFS 복제 서비스는 장애 조치 클러스터와 조정하도록 설계되지 않았으며 서비스가 다른 노드로 장애 조치되지 않습니다.


> [!NOTE]
> DFS 복제는 클러스터 공유 볼륨에서 파일 복제를 지원하지 않습니다. 
<br>


### <a name="is-dfs-replication-compatible-with-data-deduplication"></a>DFS 복제는 데이터 중복 제거와 호환되나요?

예, DFS 복제는 Windows Server에서 데이터 중복 제거를 사용하는 볼륨의 폴더를 복제할 수 있습니다.

### <a name="is-dfs-replication-compatible-with-ris-and-wds"></a>DFS 복제는 RIS 및 WDS와 호환되나요?

예. DFS 복제는 SIS(단일 인스턴스 스토리지)를 사용하도록 설정된 볼륨을 복제합니다. SIS는 RIS(원격 설치 서비스), WDS(Windows 배포 서비스) 및 Windows Storage Server에서 사용됩니다.

### <a name="is-it-possible-to-use-dfs-replication-with-offline-files"></a>오프라인 파일에서 DFS 복제를 사용할 수 있나요?

한 번에 한 명의 사용자만 파일에 쓰는 시나리오에서 DFS 복제 및 오프라인 파일을 모두 안전하게 사용할 수 있습니다. 이 기능은 두 지점 간에 이동하고 지점 또는 오프라인에서 파일에 액세스할 수 있게 하려는 사용자에게 유용합니다. 오프라인 파일은 오프라인 사용을 위해 파일을 로컬로 캐시하고, DFS 복제는 각 지점 간에 데이터를 복제합니다.

DFS 복제는 분산 잠금 메커니즘 또는 파일 체크 아웃 기능을 제공하지 않으므로 다중 사용자 환경에서 오프라인 파일을 통해 DFS 복제를 사용하지 않습니다. 두 사용자가 서로 다른 서버에서 동일한 파일을 동시에 수정하는 경우 DFS 복제는 다음 복제 중에 이전 파일을 DfsrPrivate\\ConflictandDeleted 폴더(복제된 폴더의 로컬 경로 아래에 있음)로 이동합니다.

### <a name="what-antivirus-applications-are-compatible-with-dfs-replication"></a>DFS 복제와 호환되는 바이러스 백신 애플리케이션은 무엇인가요?

바이러스 백신 애플리케이션의 검색 활동으로 인해 복제된 폴더의 파일이 변경되면 과도한 복제가 발생할 수 있습니다. 자세한 내용은 [바이러스 백신 애플리케이션 및 DFS 복제 간의 상호 운용성 테스트](https://go.microsoft.com/fwlink/?linkid=73990)(https://go.microsoft.com/fwlink/?LinkId=73990) 를 참조하세요.

### <a name="what-are-the-benefits-of-using-dfs-replication-instead-of-windows-sharepoint-services"></a>Windows SharePoint Services 대신 DFS 복제를 사용하면 어떤 이점이 있나요?

Windows® SharePoint® Services는 DFS 복제에서 제공하지 않는 파일 체크 아웃 기능의 형태로 긴밀한 일관성을 제공합니다. 여러 사용자가 동일한 파일을 편집하는 데 관심이 있는 경우 Windows SharePoint Services를 사용하는 것이 좋습니다. Windows SharePoint Services 2.0 서비스 팩 2는 Windows Server 2003 R2의 일부로 제공됩니다. Windows SharePoint Services는 Microsoft 웹 사이트에서 다운로드할 수 있으며, 최신 버전의 Windows Server에는 포함되어 있지 않습니다. 그러나 여러 사이트에 걸쳐 데이터를 복제하고 사용자가 동일한 파일을 동시에 편집하지 않는 경우 DFS 복제는 더 높은 대역폭과 더 간단한 관리를 제공합니다.

## <a name="limitations-and-requirements"></a>제한 사항 및 요구 사항

### <a name="can-dfs-replication-replicate-between-branch-offices-without-a-vpn-connection"></a>DFS 복제에서 VPN 연결을 사용하지 않고 지점 간에 복제할 수 있나요?

예, 지점을 연결하는 개인 WAN(광역 네트워크) 링크가 있다고 가정합니다. 그러나 외부 방화벽에서 적절한 포트를 열어야 합니다. DFS 복제는 RPC 엔드포인트 매퍼(포트135)와 사용 후 삭제 포트(1025 이상)를 사용합니다. **Dfsrdiag** 명령줄 도구를 사용하여 사용 후 삭제 포트 대신 정적 포트를 지정할 수 있습니다. RPC 엔드포인트 매퍼를 지정하는 방법에 대한 자세한 내용은 Microsoft 기술 자료 [문서 154596](https://go.microsoft.com/fwlink/?linkid=73991)(https://go.microsoft.com/fwlink/?LinkId=73991) 을 참조하세요.

### <a name="can-dfs-replication-replicate-files-encrypted-with-the-encrypting-file-system"></a>DFS 복제에서 파일 시스템 암호화를 사용하여 암호화된 파일을 복제할 수 있나요?

아니요. DFS 복제는 EFS(파일 시스템 암호화)를 사용하여 암호화된 파일 또는 폴더를 복제하지 않습니다. 사용자가 이전에 복제된 파일을 암호화하는 경우 DFS 복제는 복제 그룹의 다른 모든 멤버로부터 해당 파일을 삭제합니다. 이렇게 하면 사용 가능한 파일 복사본만 서버에서 암호화된 버전이 됩니다.

### <a name="can-dfs-replication-replicate-outlook-pst-or-microsoft-office-access-database-files"></a>DFS 복제에서 Outlook .pst 또는 Microsoft Office Access 데이터베이스 파일을 복제할 수 있나요?

Microsoft Outlook 개인 폴더 파일(.pst) 및 Microsoft Access 파일을 보관 목적으로 저장하고 Outlook 또는 Access와 같은 클라이언트를 사용하여 네트워크를 통해 액세스할 수 없는 경우에만 DFS 복제에서 이러한 파일을 안전하게 복제할 수 있습니다(.pst 또는 Access 파일을 열기 위해 먼저 파일을 로컬 스토리지 디바이스에 복사). 그 이유는 다음과 같습니다.

  - 네트워크 연결을 통해 .pst 파일을 열면 .pst 파일의 데이터가 손상될 수 있습니다. 네트워크를 통해 .pst 파일에 안전하게 액세스할 수 없는 이유에 대한 자세한 내용은 Microsoft 기술 자료 [문서 297019](https://go.microsoft.com/fwlink/?linkid=125363)(https://go.microsoft.com/fwlink/?LinkId=125363) 를 참조하세요.  
      
  - .pst 및 Access 파일은 Outlook 또는 Office Access와 같은 클라이언트에서 액세스하는 동안 오랫동안 열려 있는 상태를 유지하는 경향이 있습니다. 이렇게 하면 파일이 닫힐 때까지 DFS 복제에서 이러한 파일을 복제할 수 없습니다.  
      

### <a name="can-i-use-dfs-replication-in-a-workgroup"></a>DFS 복제는 작업 그룹에서 사용할 수 있나요?

아니요. DFS 복제는 구성을 위해 Active Directory® Domain Services를 사용합니다. 이는 도메인에서만 작동합니다.

### <a name="can-more-than-one-folder-be-replicated-on-a-single-server"></a>단일 서버에서 둘 이상의 폴더를 복제할 수 있나요?

예. DFS 복제는 서버 간에 수많은 폴더를 복제할 수 있습니다. 복제된 각 폴더에는 고유한 루트 경로가 있고 겹치지 않아야 합니다. 예를 들어 D:\\Sales 및 D:\\Accounting은 두 복제된 폴더의 루트 경로가 될 수 있지만, D:\\Sales 및 D:\\Sales\\Reports는 두 복제된 폴더의 루트 경로가 될 수 없습니다.

### <a name="does-dfs-replication-require-dfs-namespaces"></a>DFS 복제에 DFS 네임스페이스가 필요한가요?

아니요. DFS 복제 및 DFS 네임스페이스는 개별적으로 또는 함께 사용할 수 있습니다. 또한 DFS 복제를 사용하여 독립 실행형 DFS 네임스페이스를 복제할 수 있지만, FRS에서는 이를 복제할 수 없습니다.

### <a name="does-dfs-replication-require-time-synchronization-between-servers"></a>DFS 복제에 서버 간 시간 동기화가 필요한가요?

아니요. DFS 복제에는 서버 간 시간 동기화가 명시적으로 필요하지 않습니다. 그러나 DFS 복제를 사용하려면 서버 시계가 긴밀하게 일치해야 합니다. Kerberos 인증이 제대로 작동하려면 서버 시계가 서로 5분 이내로(기본값) 설정되어 있어야 합니다. 예를 들어 DFS 복제는 타임스탬프를 사용하여 충돌 시 우선으로 적용할 파일을 결정합니다. 정확한 시간은 가비지 수집, 일정 및 기타 기능에도 중요합니다.

### <a name="does-dfs-replication-support-replicating-an-entire-volume"></a>DFS 복제에서 전체 볼륨 복제를 지원하나요?

예. 그러나 먼저 Windows Server 2003 서비스 팩 2 또는 핫픽스를 설치해야 합니다. 자세한 내용은 Microsoft 기술 자료 [문서 920335](https://go.microsoft.com/fwlink/?linkid=76776)(https://go.microsoft.com/fwlink/?LinkId=76776) 를 참조하세요. 또한 전체 볼륨을 복제하면 다음과 같은 문제가 발생할 수 있습니다.

  - Windows 페이징 파일이 볼륨에 포함되어 있으면 복제가 실패하고 시스템 이벤트 로그에 4312 DFSR 이벤트가 기록됩니다.  
      
  - DFS 복제에서 System 및 Hidden 특성을 대상 서버의 복제된 폴더에 설정합니다. 이는 Windows가 기본적으로 볼륨 루트 폴더에 System 및 Hidden 특성을 적용하기 때문에 발생합니다. 대상 서버에서 복제된 폴더의 로컬 경로도 볼륨 루트인 경우 폴더 특성을 추가로 변경하지 않습니다.  
      
  - Windows 시스템 폴더가 포함된 볼륨을 복제하는 경우 DFS 복제는 %WINDIR% 폴더를 인식하여 복제하지 않습니다. 그러나 DFS 복제는 타사 애플리케이션에서 사용하는 폴더를 복제하므로 애플리케이션에 DFS 복제와의 상호 운용성 문제가 있으면 대상 서버에서 애플리케이션이 실패할 수 있습니다.  
      

### <a name="does-dfs-replication-support-rpc-over-http"></a>DFS 복제에서 RPC over HTTP를 지원하나요?

아니요.

### <a name="does-dfs-replication-work-across-wireless-networks"></a>DFS 복제가 무선 네트워크에서 작동하나요?

예. DFS 복제는 연결 형식과 관련이 없습니다.

### <a name="does-dfs-replication-work-on-refs-or-fat-volumes"></a>DFS 복제가 ReFS 또는 FAT 볼륨에서 작동하나요?

아니요. DFS 복제는 NTFS 파일 시스템으로 포맷된 볼륨만 지원합니다. ReFS(복원 파일 시스템) 및 FAT 파일 시스템은 지원되지 않습니다. DFS 복제에서 NTFS 파일 시스템의 NTFS 변경 저널 및 기타 기능을 사용하므로 NTFS가 필요합니다.

### <a name="does-dfs-replication-work-with-sparse-files"></a>DFS 복제가 스파스 파일과 함께 작동하나요?

예. 스파스 파일을 복제할 수 있습니다. **Sparse** 특성은 받는 멤버에서 유지됩니다.

### <a name="do-i-need-to-log-in-as-administrator-to-replicate-files"></a>파일을 복제하려면 관리자 권한으로 로그인해야 하나요?

아니요. DFS 복제는 로컬 시스템 계정으로 실행되는 서비스이므로 복제하기 위해 관리자 권한으로 로그인할 필요가 없습니다. 그러나 DFS 복제 구성을 변경하려면 영향을 받는 파일 서버의 도메인 관리자 또는 로컬 관리자여야 합니다.

자세한 내용은 [DFS 복제 관리 기능 위임](https://go.microsoft.com/fwlink/?linkid=182294)(https://go.microsoft.com/fwlink/?LinkId=182294) 의 "DFS 복제 보안 요구 사항 및 위임"을 참조하세요.

### <a name="how-can-i-upgrade-or-replace-a-dfs-replication-member"></a>DFS 복제 멤버를 업그레이드하거나 바꾸려면 어떻게 해야 하나요?

DFS 복제 멤버를 업그레이드하거나 바꾸려면 ‘디렉터리 서비스 팀에 문의’ 블로그인 [DFSR 멤버 하드웨어 또는 OS 교체](https://blogs.technet.com/b/askds/archive/2010/09/10/series-wrap-up-and-downloads-replacing-dfsr-member-hardware-or-os.aspx) 블로그 게시물을 참조하세요.

### <a name="is-dfs-replication-suitable-for-replicating-roaming-profiles"></a>DFS 복제가 로밍 프로필을 복제하는 데 적합한가요?

예. 로밍 사용자 프로필을 복제하는 경우 특정 시나리오가 지원됩니다. 지원되는 시나리오에 대한 자세한 내용은 [복제된 사용자 프로필 데이터와 관련된 Microsoft 지원 정책](https://go.microsoft.com/fwlink/?linkid=201282)(https://go.microsoft.com/fwlink/?LinkId=201282) 을 참조하세요.

### <a name="is-there-a-file-character-limit-or-limit-to-the-folder-depth"></a>파일 문자 제한 또는 폴더 깊이 제한이 있나요?

Windows 및 DFS 복제는 최대 32,000자의 폴더 경로를 지원합니다. DFS 복제는 260자의 폴더 경로로 제한되지 않습니다.

### <a name="must-members-of-a-replication-group-reside-in-the-same-domain"></a>복제 그룹의 멤버가 동일한 도메인에 상주해야 하나요?

아니요. 복제 그룹은 단일 포리스트 내의 여러 도메인에 걸쳐 있을 수 있지만, 다른 포리스트에는 걸쳐 있을 수 없습니다.

### <a name="what-are-the-supported-limits-of-dfs-replication"></a>지원되는 DFS 복제에 대한 제한 사항은 무엇인가요?

다음 목록에는 Microsoft에서 테스트하여 Windows Server 2012 R2, Windows Server 2016 및 Windows Server 2019에 적용되는 확장성 지침이 나와 있습니다.

  - 서버에서 복제된 모든 파일의 크기: 100TB  
      
  - 볼륨에서 복제된 파일의 수: 7,000만 개  
      
  - 최대 파일 크기: 250GB  
      


> [!IMPORTANT]
> 많거나 큰 파일이 포함된 복제 그룹을 만드는 경우 데이터베이스 복제본을 내보내고 미리 시드 기술을 사용하여 초기 복제 기간을 최소화하는 것이 좋습니다. 자세한 내용은 [Windows Server 2012 R2의 DFS 복제 초기 동기화: 복제본의 공격](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/DFS-Replication-Initial-Sync-in-Windows-Server-2012-R2-Attack-of/ba-p/424877)을 참조하세요. 
<br>


다음 목록에는 Microsoft에서 테스트하여 Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008에 적용되는 확장성 지침이 나와 있습니다.

  - 서버에서 복제된 모든 파일의 크기: 10TB  
      
  - 볼륨에서 복제된 파일의 수: 1,100만 개  
      
  - 최대 파일 크기: 64GB  
      


> [!NOTE]
> 복제 그룹, 복제된 폴더, 연결 또는 복제 그룹 멤버의 수는 더 이상 제한되지 않습니다. 
<br>


Microsoft에서 Windows Server 2003 R2용으로 테스트한 확장성 지침 목록은 [DFS 복제 확장성 지침](https://go.microsoft.com/fwlink/?linkid=75043)(https://go.microsoft.com/fwlink/?LinkId=75043) 을 참조하세요.

### <a name="when-should-i-not-use-dfs-replication"></a>DFS 복제를 사용하지 않아야 하는 경우는 어떻게 되나요?

여러 사용자가 서로 다른 서버에서 동일한 파일을 동시에 업데이트하거나 수정하는 환경에서는 DFS 복제를 사용하지 않습니다. 이렇게 하면 DFS 복제에서 충돌하는 파일의 복사본을 숨겨진 DfsrPrivate\\ConflictandDeleted 폴더로 이동시킬 수 있습니다.

여러 사용자가 서로 다른 서버에서 동일한 파일을 동시에 수정해야 하는 경우 Windows SharePoint Services의 파일 체크 아웃 기능을 사용하여 한 명의 사용자만 파일에서 작업하도록 합니다. Windows SharePoint Services 2.0 서비스 팩 2는 Windows Server 2003 R2의 일부로 제공됩니다. Windows SharePoint Services는 Microsoft 웹 사이트에서 다운로드할 수 있으며, 최신 버전의 Windows Server에는 포함되어 있지 않습니다.

### <a name="why-is-a-schema-update-required-for-dfs-replication"></a>DFS 복제에 스키마 업데이트가 필요한 이유는 무엇인가요?

DFS 복제는 Active Directory Domain Services의 도메인 명명 컨텍스트에서 새 개체를 사용하여 구성 정보를 저장합니다. 이러한 개체는 Active Directory Domain Services 스키마를 업데이트할 때 만들어집니다. 자세한 내용은 [DFS 복제 요구 사항 검토](https://go.microsoft.com/fwlink/?linkid=182264)(https://go.microsoft.com/fwlink/?LinkId=182264) 를 참조하세요.

## <a name="monitoring-and-management-tools"></a>모니터링 및 관리 도구

### <a name="can-i-automate-the-health-report-to-receive-warnings"></a>경고를 받도록 상태 보고서를 자동화할 수 있나요?

예. 상태 보고서를 자동화하는 세 가지 방법은 다음과 같습니다.

  - Windows Server 2012 R2 또는 DfsrAdmin.exe에 포함된 DFSR Windows PowerShell 모듈을 예약된 작업과 함께 사용하여 상태 보고서를 정기적으로 생성합니다. 자세한 내용은 [DFS 복제 상태 보고서 자동화](https://go.microsoft.com/fwlink/?linkid=74010)(https://go.microsoft.com/fwlink/?LinkId=74010) 를 참조하세요.  
      
  - System Center Operations Manager용 DFS 복제 관리 팩을 사용하여 지정된 조건에 따라 경고를 만듭니다.  
      
  - DFS 복제 WMI 공급자를 사용하여 경고를 스크립팅합니다.  
      

### <a name="can-i-use-microsoft-system-center-operations-manager-to-monitor-dfs-replication"></a>Microsoft System Center Operations Manager를 사용하여 DFS 복제를 모니터링할 수 있나요?

예. 자세한 내용은 Microsoft 다운로드 센터에서 [System Center Operations Manager 2007용 DFS 복제 관리 팩](https://go.microsoft.com/fwlink/?linkid=182265)(https://go.microsoft.com/fwlink/?LinkId=182265) 을 참조하세요.

### <a name="does-dfs-replication-support-remote-management"></a>DFS 복제에서 원격 관리를 지원하나요?

예. DFS 복제는 DFS 관리 콘솔 및 **복제 그룹 추가** 명령을 사용하여 원격 관리를 지원합니다. 예를 들어 서버 A에서 서버 A 및 B를 멤버로 사용하여 포리스트에 정의된 복제 그룹에 연결할 수 있습니다.

DFS 관리는 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 및 Windows Server 2003 R2에 포함되어 있습니다. 다른 버전의 Windows에서 DFS 복제를 관리하려면 원격 데스크톱 또는 [Windows 7용 원격 서버 관리 도구](https://technet.microsoft.com/library/Ee449475)를 사용합니다.


> [!IMPORTANT]
> 장애 조치 클러스터인 읽기 전용 복제 폴더 또는 멤버가 포함된 복제 그룹을 보거나 관리하려면 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, <a href="https://go.microsoft.com/fwlink/p/?linkid=238560">Windows 8용 원격 서버 관리 도구</a> 또는 <a href="https://technet.microsoft.com/library/ee449475">Windows 7용 원격 서버 관리 도구</a>에 포함된 DFS 관리 버전을 사용해야 합니다. 
<br>


### <a name="do-ultrasound-and-sonar-work-with-dfs-replication"></a>Ultrasound 및 Sonar는 DFS 복제에서 작동하나요?

아니요. DFS 복제에는 자체 모니터링 및 진단 도구 세트가 있습니다. Ultrasound 및 Sonar는 FRS만 모니터링할 수 있습니다.

### <a name="how-can-files-be-recovered-from-the-conflictanddeleted-or-preexisting-folders"></a>ConflictAndDeleted 또는 PreExisting 폴더에서 파일을 복구하려면 어떻게 해야 하나요?

손실된 파일을 복구하려면 파일 기록, 파일 탐색기의 **이전 버전 복원** 명령을 사용하거나 백업에서 파일을 복원하여 파일 시스템 폴더 또는 공유 폴더에서 파일을 복원합니다. ConflictAndDeleted 또는 PreExisting 폴더에서 파일을 직접 복구하려면 `Get-DfsrPreservedFiles` 및 `Restore-DfsrPreservedFiles` Windows PowerShell cmdlet(Windows Server 2012 R2의 DFSR 모듈에 포함되어 있음) 또는 MSDN 코드 갤러리의 [RestoreDFSR](https://code.msdn.microsoft.com/restoredfsr) 샘플 스크립트를 사용합니다. 이 스크립트는 재해 복구 전용이며, 보증 없이 있는 그대로 제공됩니다.

### <a name="is-there-a-way-to-know-the-state-of-replication"></a>복제 상태를 확인할 수 있는 방법이 있나요?

예. 복제를 모니터링하는 방법에는 여러 가지가 있습니다.

  - DFS 복제에는 사전 모니터링을 제공하는 System Center Operations Manager용 관리 팩이 있습니다.  
      
  - DFS 관리에는 복제 백로그, 복제 효율성 및 지정된 복제 그룹의 파일 및 폴더 수에 대한 기본 제공 진단 보고서가 있습니다.  
      
  - Windows Server 2012 R2의 DFSR Windows PowerShell 모듈에는 전파 테스트를 시작하고 전파 및 상태 보고서를 쓰는 cmdlet이 포함되어 있습니다. 자세한 내용은 [Windows PowerShell의 분산 파일 시스템 복제 cmdlet](https://technet.microsoft.com/library/dn296601.aspx)을 참조하세요.  
      
  - Dfsrdiag.exe는 백로그 수를 생성하거나 전파 테스트를 트리거할 수 있는 명령줄 도구입니다. 둘 다 복제 상태를 표시합니다. 전파는 모든 노드에 파일이 복제되고 있는지 여부를 표시합니다. 백로그는 두 컴퓨터를 동기화하기 전에 복제해야 하는 파일의 수를 표시합니다. 백로그 수는 복제 그룹 멤버가 처리하지 않은 업데이트 수입니다. Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2를 실행하는 컴퓨터에서 Dfsrdiag.exe는 DFS 복제를 통해 현재 복제 중인 업데이트를 표시할 수도 있습니다.  
      
  - 스크립트는 WMI를 사용하여 수동으로 또는 MOM을 통해 백로그 정보를 수집할 수 있습니다.  
      

## <a name="performance"></a>성능

### <a name="does-dfs-replication-support-dial-up-connections"></a>DFS 복제에서 전화 접속 연결을 지원하나요?

DFS 복제는 전화 접속 속도로 작동하지만, 복제할 변경 내용이 많은 경우 백로그될 수 있습니다. 기존 파일을 약간만 변경하는 경우 RDC(원격 차등 압축)를 사용하는 DFS 복제에서 파일을 직접 복사하는 것보다 훨씬 더 높은 성능을 제공합니다.

### <a name="does-dfs-replication-perform-bandwidth-sensing"></a>DFS 복제에서 대역폭 감지를 수행하나요?

아니요. DFS 복제는 대역폭 감지를 수행하지 않습니다. 연결별로 제한된 양의 대역폭을 사용하도록 DFS 복제를 구성할 수 있습니다(대역폭 제한). 그러나 네트워크 인터페이스가 포화 상태인 경우 DFS 복제는 대역폭 사용률을 더 낮추지 않으며, 링크를 단기간 동안 포화시킬 수 있습니다. DFS 복제에서 RPC 호출을 제한하여 대역폭을 제한하므로 DFS 복제를 통한 대역폭 제한이 완전히 정확하지는 않습니다. 결과적으로 낮은 수준의 네트워크 스택(RPC 포함)에 있는 다양한 버퍼가 방해하여 네트워크 트래픽이 급증할 수 있습니다.

### <a name="does-dfs-replication-throttle-bandwidth-per-schedule-per-server-or-per-connection"></a>DFS 복제에서 일정, 서버 또는 연결별로 대역폭을 제한하나요?

일정을 지정할 때 대역폭 제한을 구성하면 해당 복제 그룹에 대한 모든 연결에서 해당 대역폭 제한 설정을 사용합니다. 대역폭 제한은 DFS 관리를 사용하여 연결 수준 설정으로 지정할 수도 있습니다.

### <a name="does-dfs-replication-use-active-directory-domain-services-to-calculate-site-links-and-connection-costs"></a>DFS 복제에서 Active Directory Domain Services를 사용하여 사이트 링크 및 연결 비용을 계산하나요?

아니요. DFS 복제는 Active Directory Domain Services 사이트 비용과 관련이 없는 관리자가 정의한 토폴로지를 사용합니다.

### <a name="how-can-i-improve-replication-performance"></a>복제 성능을 향상시키려면 어떻게 해야 하나요?

복제 성능을 튜닝하는 다양한 방법에 대한 자세한 내용은 [디렉터리 서비스 팀에 문의 블로그](https://blogs.technet.com/b/askds/)의 [DFSR의 복제 성능 튜닝](https://blogs.technet.com/b/askds/archive/2010/03/31/tuning-replication-performance-in-dfsr-especially-on-win2008-r2.aspx)을 참조하세요.

### <a name="how-does-dfs-replication-avoid-saturating-a-connection"></a>DFS 복제에서 연결이 포화되지 않도록 방지하는 방법은 무엇인가요?

DFS 복제에서 연결에 사용하려는 최대 대역폭을 설정하고, 서비스에서 해당 수준의 네트워크 사용을 유지합니다. 이는 BITS(Background Intelligent Transfer Service)와 다르며, DFS 복제에서 연결을 적절하게 설정하는 경우 연결이 포화되지 않습니다.

그럼에도 불구하고 대역폭 제한은 100% 정확하지 않으며, DFS 복제에서 링크를 짧은 시간 동안 포화시킬 수 있습니다. 이는 DFS 복제에서 RPC 호출을 제한하여 대역폭을 제한하기 때문입니다. 이 프로세스는 RPC를 포함하여 더 낮은 수준의 네트워크 스택에 있는 다양한 버퍼를 사용하므로 복제 트래픽이 버스트 단위로 이동하는 경향이 있으며, 이로 인해 네트워크 링크가 포화될 수 있습니다.

Windows Server 2008의 DFS 복제에는 [Windows Server 2003 SP1에서 Windows Server 2008로 기능 변경](https://technet.microsoft.com/library/cc753208)의 [분산 파일 시스템](https://technet.microsoft.com/library/Cc753479) 항목에서 설명한 대로 몇 가지 향상된 성능이 포함되어 있습니다.

### <a name="how-does-dfs-replication-performance-compare-with-frs"></a>DFS 복제 성능은 FRS와 어떻게 비교되나요?

DFS 복제는 FRS보다 훨씬 빠릅니다(특히 큰 파일을 약간만 변경하고 RDC를 사용하도록 설정한 경우). 예를 들어 RDC를 사용하는 경우 2MB PowerPoint® 프레젠테이션을 약간만 변경하면 네트워크를 통해 60KB만 전송되므로 전송되는 바이트 수가 97% 절약될 수 있습니다.

RDC는 64KB 미만의 파일에는 사용되지 않으며, 네트워크 대역폭 경합이 없는 고속 LAN에서 유용하지 않을 수 있습니다. RDC는 DFS 관리를 사용하여 연결별로 사용하지 않도록 설정할 수 있습니다.

### <a name="how-frequently-does-dfs-replication-replicate-data"></a>DFS 복제에서 데이터를 복제하는 빈도는 어떻게 되나요?

데이터는 설정한 일정에 따라 복제됩니다. 예를 들어 일정을 일주일에 7일, 15분 간격으로 설정할 수 있습니다. 이러한 간격 동안 복제가 활성화됩니다. 파일 변경이 검색되는 즉시(일반적으로 몇 초 이내) 복제가 시작됩니다.

연결 일정이 받는 멤버의 현지 시간으로 설정되어 있는 동안 복제 그룹 일정은 UTC(Universal Time Coordinate)로 설정할 수 있습니다. 복제 그룹이 여러 표준 시간대에 걸쳐 있는 경우에는 이를 고려해야 합니다. 현지 시간은 멤버가 인바운드 연결을 호스팅하는 시간을 의미합니다. 일정이 현지 시간으로 설정된 경우 인바운드 연결 및 해당 아웃바운드 연결에 대해 표시되는 일정은 표준 시간대 차이를 반영합니다.

### <a name="how-much-of-my-servers-system-resources-will-dfs-replication-consume"></a>DFS 복제에서 사용하는 서버의 시스템 리소스 양은 얼마인가요?

DFS 복제에서 사용하는 디스크, 메모리 및 CPU 리소스는 파일 수와 크기, 변경 비율, 복제 그룹 멤버 수, 복제된 폴더 수를 포함한 여러 요소에 따라 달라집니다. 또한 일부 리소스는 예측하기 어렵습니다. 예를 들어 DFS 복제 데이터베이스에 사용되는 ESE(Extensible Storage Engine) 기술은 사용 가능한 메모리 중 상당 부분을 소비할 수 있으며, 필요에 따라 해제됩니다. DFS 복제 이외의 애플리케이션은 서버 구성에 따라 동일한 서버에서 호스팅할 수 있습니다. 그러나 단일 서버에서 여러 애플리케이션 또는 서버 역할을 호스팅하는 경우 프로덕션 환경에서 구현하기 전에 이 구성을 테스트해야 합니다.

### <a name="what-happens-if-a-wan-link-fails-during-replication"></a>복제 중에 WAN 링크가 실패하면 어떻게 되나요?

연결이 끊어지면 일정이 열려 있는 동안 DFS 복제에서 복제를 계속 시도합니다. 또한 MOM(사전에 경고를 통해) 및 DFS 복제 상태 보고서(예: 관리자가 실행하는 경우와 같이 사후에)를 사용하여 수집할 수 있는 DFS 복제 이벤트 로그에 연결 오류가 표시될 수도 있습니다.

## <a name="remote-differential-compression-details"></a>원격 차등 압축 세부 정보

### <a name="are-changes-compressed-before-being-replicated"></a>변경 내용을 복제하기 전에 압축하나요?

예. 파일의 변경된 부분은 이미 압축되어 있는 wma, .wmv, .zip, .jpg, .mpg, .mpeg, .m1v, .mp2, .mp3, .mpa, .cab, .wav, .snd, .au, .asf, .wm, .avi, .z, .gz, .tgz 및 .frx를 제외한 모든 파일 형식에 대해 전송되기 전에 압축됩니다. Windows Server 2003 R2에서는 이러한 파일 형식에 대한 압축 설정을 구성할 수 없습니다.

### <a name="can-an-administrator-turn-off-rdc-or-change-the-threshold"></a>관리자가 RDC를 해제하거나 임계값을 변경할 수 있나요?

예. 지정된 연결의 속성 페이지를 통해 RDC를 해제할 수 있습니다. RDC를 사용하지 않도록 설정하면 대역폭 제약이 없는 고속 LAN(Local Area Network) 링크 또는 주로 64KB 미만의 파일로 구성된 복제 그룹에 대한 CPU 사용률 및 복제 대기 시간을 줄일 수 있습니다. 연결에서 RDC를 사용하지 않도록 선택하는 경우 변경 전후에 복제 효율성을 테스트하여 복제 성능이 향상되었는지 확인합니다.

**Dfsradmin Connection Set** 명령, DFS 복제 WMI 공급자를 사용하거나 구성 XML 파일을 수동으로 편집하여 RDC 크기 임계값을 변경할 수 있습니다.

### <a name="does-rdc-work-on-all-file-types"></a>RDC가 모든 파일 형식에서 작동하나요?

예. RDC는 파일 데이터 형식에 관계없이 블록 수준의 차이를 계산합니다. 그러나 RDC는 Word 문서, PST 파일 및 VHD 이미지와 같은 특정 파일 형식에서 더 효율적으로 작동합니다.

### <a name="how-does-rdc-work-on-a-compressed-file"></a>RDC는 압축 파일에서 어떻게 작동하나요?

DFS 복제는 변경된 파일의 블록을 계산하여 네트워크를 통해 해당 블록만 보내는 RDC를 사용합니다. DFS 복제는 파일 내용에 대해 알 필요가 없으며, 변경된 블록만 알 수 있습니다.

### <a name="is-cross-file-rdc-enabled-when-upgrading-to-windows-server-enterprise-edition-or-datacenter-edition"></a>Windows Server Enterprise Edition 또는 Datacenter Edition으로 업그레이드할 때 파일 간 RDC를 사용할 수 있나요?

Windows Server Standard Edition은 파일 간 RDC를 지원하지 않습니다. 그러나 파일 간 RDC를 지원하는 버전으로 업그레이드하거나 복제 연결의 멤버가 지원되는 버전을 실행하는 경우 자동으로 사용하도록 설정됩니다. 파일 간 RDC를 지원하는 버전 목록은 "파일 간 RDC를 지원하는 Windows 운영 체제 버전은 무엇인가요?"를 참조하세요.

### <a name="is-rdc-true-block-level-replication"></a>RDC는 진정한 블록 수준 복제인가요?

아니요. RDC는 파일 전송 압축을 위한 범용 프로토콜입니다. DFS 복제는 디스크 블록 수준이 아니라 파일 블록 수준에서 RDC를 사용합니다. RDC는 파일을 블록으로 분할합니다. 파일의 각 블록에 대해 더 큰 블록을 나타낼 수 있는 작은 바이트 수인 서명을 계산합니다. 서명 세트는 서버에서 클라이언트로 전송됩니다. 클라이언트는 서버 서명을 자체 서명과 비교합니다. 그런 다음, 클라이언트에서 아직 클라이언트에 없는 서명에 대한 데이터만 보내도록 서버에 요청합니다.

### <a name="what-happens-if-i-rename-a-file"></a>파일 이름을 바꾸면 어떻게 되나요?

DFS 복제는 다음 복제 중에 복제 그룹의 다른 모든 멤버에 대한 파일의 이름을 바꿉니다. 파일은 고유 ID를 사용하여 추적되므로 파일 이름을 바꾸고 복제본 내에서 파일을 이동하더라도 파일을 복제하는 DFS 복제의 기능에는 영향을 주지 않습니다.

### <a name="what-is-cross-file-rdc"></a>파일 간 RDC란 무엇인가요?

파일 간 RDC를 사용하면 클라이언트 쪽에 동일한 이름의 파일이 없는 경우에도 DFS 복제에서 RDC를 사용할 수 있습니다. 파일 간 RDC는 추론을 사용하여 복제해야 하는 파일과 비슷한 파일을 결정하고, 복제 파일과 동일한 파일과 비슷한 블록을 사용하여 WAN을 통해 전송되는 데이터 양을 최소화합니다. 파일 간 RDC는 이 프로세스에서 최대 5개의 비슷한 파일 블록을 사용할 수 있습니다.

파일 간 RDC를 사용하려면 복제 연결의 멤버 중 한 명이 파일 간 RDC를 지원하는 Windows 버전을 실행해야 합니다. 파일 간 RDC를 지원하는 버전 목록은 "파일 간 RDC를 지원하는 Windows 운영 체제 버전은 무엇인가요?"를 참조하세요.

### <a name="what-is-rdc"></a>RDC는 무엇인가요?

RDC(원격 차등 압축)는 제한된 대역폭 네트워크를 통해 파일을 효율적으로 업데이트하는 데 사용할 수 있는 클라이언트-서버 프로토콜입니다. RDC는 파일 데이터의 삽입, 제거 및 다시 정렬을 검색하여 파일이 업데이트될 때 DFS 복제에서 변경 내용만 복제할 수 있도록 합니다. RDC는 기본적으로 64KB 이상인 파일에만 사용됩니다. RDC는 복제된 폴더 또는 DfsrPrivate\\ConflictandDeleted 폴더(복제된 폴더의 로컬 경로 아래에 있음)에서 이름이 동일한 이전 버전의 파일을 사용할 수 있습니다.

### <a name="when-is-rdc-used-for-replication"></a>RDC가 복제에 사용되는 경우는 언제인가요?

파일이 최소 크기 임계값을 초과하면 RDC가 사용됩니다. 이 크기 임계값은 기본적으로 64KB입니다. 이 임계값을 초과하는 파일이 복제되면 파일의 많은 부분이 변경되거나 RDC를 사용하지 않도록 설정되지 않는 한 업데이트된 버전의 파일에서 항상 RDC를 사용합니다.

### <a name="which-editions-of-the-windows-operating-system-support-cross-file-rdc"></a>파일 간 RDC를 지원하는 Windows 운영 체제 버전은 무엇인가요?

파일 간 RDC를 사용하려면 복제 연결의 멤버 중 한 명이 파일 간 RDC를 지원하는 Windows 운영 체제 버전을 실행해야 합니다. 다음 표에는 파일 간 RDC를 지원하는 Windows 운영 체제 버전이 나와 있습니다.

### <a name="cross-file-rdc-availability-in-editions-of-the-windows-operating-system"></a>Windows 운영 체제 버전의 파일 간 RDC 가용성

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>운영 체제 버전</th>
<th>Standard Edition</th>
<th>Enterprise Edition</th>
<th>Datacenter Edition</th>
</tr>
</thead>
<tbody>
<tr class="even">
<td><p>Windows Server 2012 R2</p></td>
<td><p>예<em></p></td>
<td><p>사용할 수 없음</p></td>
<td><p>예</em></p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012</p></td>
<td><p>예</p></td>
<td><p>사용할 수 없음</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 R2</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2003 R2</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
</tbody>
</table>

\* 필요에 따라 Windows Server 2012 R2에서 파일 간 RDC를 사용하지 않도록 설정할 수 있습니다.

## <a name="replication-details"></a>복제 세부 정보

### <a name="can-i-change-the-path-for-a-replicated-folder-after-it-is-created"></a>복제된 폴더를 만든 후 경로를 변경할 수 있나요?

아니요. 복제된 폴더의 경로를 변경해야 하는 경우 DFS 관리에서 해당 경로를 삭제하고 새 복제된 폴더로 다시 추가해야 합니다. 그런 다음, DFS 복제는 RDC(원격 차등 압축)를 사용하여 보내는 멤버 및 받는 멤버의 데이터가 동일한지 여부를 확인하는 동기화를 수행합니다. 폴더의 모든 데이터를 다시 복제하지는 않습니다.

### <a name="can-i-configure-which-file-attributes-are-replicated"></a>복제할 파일 특성을 구성할 수 있나요?

아니요, DFS 복제에서 복제하는 파일 특성은 구성할 수 없습니다.

특성 값 및 해당 설명에 대한 목록은 MSDN의 [파일 특성](https://go.microsoft.com/fwlink/?linkid=182268)(https://go.microsoft.com/fwlink/?LinkId=182268) 을 참조하세요.

다음 특성 값은 `SetFileAttributes dwFileAttributes` 함수를 사용하여 설정되며 DFS 복제에서 복제됩니다. 이러한 특성 값을 변경하면 특성의 복제가 트리거됩니다. 파일의 내용이 변경되지 않으면 복제되지도 않습니다. 자세한 내용은 MSDN 라이브러리의 [SetFileAttributes 함수](https://go.microsoft.com/fwlink/?linkid=182269)(https://go.microsoft.com/fwlink/?LinkId=182269) 를 참조하세요.

  - FILE\_ATTRIBUTE\_HIDDEN  
      
  - FILE\_ATTRIBUTE\_READONLY  
      
  - FILE\_ATTRIBUTE\_SYSTEM  
      
  - FILE\_ATTRIBUTE\_NOT\_CONTENT\_INDEXED  
      
  - FILE\_ATTRIBUTE\_OFFLINE  
      

다음 특성 값은 DFS 복제에서 복제되지만 복제를 트리거하지는 않습니다.

  - FILE\_ATTRIBUTE\_ARCHIVE  
      
  - FILE\_ATTRIBUTE\_NORMAL  
      

또한 다음 파일 특성 값은 `SetFileAttributes` 함수를 사용하여 설정할 수 없지만 복제를 트리거합니다(특성 값을 확인하려면 `GetFileAttributes` 함수 사용).

  - FILE\_ATTRIBUTE\_REPARSE\_POINT  
      

> [!NOTE]
> 재분석 태그가 IO_REPARSE_TAG_SYMLINK가 아니면 DFS 복제에서 재분석 지점 특성 값을 복제하지 않습니다. IO_REPARSE_TAG_DEDUP, IO_REPARSE_TAG_SIS 또는 IO_REPARSE_TAG_HSM 재분석 태그가 있는 파일은 일반 파일로 복제됩니다. 그러나 재분석 지점은 로컬 시스템에서만 작동하므로 재분석 태그 및 재분석 데이터 버퍼는 다른 서버로 복제되지 않습니다. 
<br>

  - FILE\_ATTRIBUTE\_COMPRESSED  
      
  - FILE\_ATTRIBUTE\_ENCRYPTED  
      

> [!NOTE]
> DFS 복제는 EFS(파일 시스템 암호화)를 사용하여 암호화된 파일을 복제하지 않습니다. DFS 복제에서 타사 소프트웨어를 사용하여 암호화된 파일을 복제하지만, 파일에서 FILE_ATTRIBUTE_ENCRYPTED 특성 값을 설정하지 않은 경우에만 복제합니다. 
<br>

  - FILE\_ATTRIBUTE\_SPARSE\_FILE  
      
  - FILE\_ATTRIBUTE\_DIRECTORY  
      

DFS 복제는 FILE\_ATTRIBUTE\_TEMPORARY 값을 복제하지 않습니다.

### <a name="can-i-control-which-member-is-replicated"></a>복제된 멤버를 제어할 수 있나요?

예. 복제 그룹을 만들 때 토폴로지를 선택할 수 있습니다. 또는 복제 그룹을 만든 후에 **토폴로지 없음**을 선택하고 연결을 수동으로 구성할 수 있습니다.

### <a name="can-i-seed-a-replication-group-member-with-data-prior-to-the-initial-replication"></a>초기 복제 전에 데이터를 사용하여 복제 그룹 멤버를 시드할 수 있나요?

예. DFS 복제는 초기 복제 전에 파일을 복제 그룹 멤버에 복사하도록 지원합니다. 이 "사전 준비"를 통해 초기 복제 중에 복제되는 데이터의 양을 크게 줄일 수 있습니다.

파일의 실제 특성 또는 타임스탬프만 다를 경우 초기 복제에서 파일의 내용을 복제할 필요가 없습니다. 실제 특성은 Win32 함수 `SetFileAttributes`에서 설정할 수 있는 특성입니다. 자세한 내용은 MSDN 라이브러리의 [SetFileAttributes 함수](https://go.microsoft.com/fwlink/?linkid=182269)(https://go.microsoft.com/fwlink/?LinkId=182269) 를 참조하세요. 두 파일의 다른 특성(예: 압축)이 다를 경우 파일의 내용이 복제됩니다.

복제 그룹 멤버를 사전 준비하려면 파일을 대상 서버의 해당 폴더에 복사하고, 복제 그룹을 만든 다음, 주 멤버를 선택합니다. 주 멤버의 콘텐츠가 "신뢰할 수 있는" 것으로 간주되므로 복제하려는 최신 파일이 있는 멤버를 선택합니다. 즉, 초기 복제 중에 주 멤버의 파일이 항상 복제 그룹의 다른 멤버에 있는 다른 버전의 파일을 덮어씁니다.

DFSR 데이터베이스를 미리 시드하고 복제하는 방법에 대한 자세한 내용은 [Windows Server 2012 R2의 DFS 복제 초기 동기화: 복제본의 공격](https://blogs.technet.com/b/filecab/archive/2013/08/21/dfs-replication-initial-sync-in-windows-server-2012-r2-attack-of-the-clones.aspx)을 참조하세요.

초기 복제에 대한 자세한 내용은 [복제 그룹 만들기](https://technet.microsoft.com/library/cc725893)를 참조하세요.

### <a name="does-dfs-replication-overcome-common-file-replication-service-issues"></a>DFS 복제에서 일반적인 파일 복제 서비스 문제를 해결하나요?

예. DFS 복제에서 해결하는 세 가지 일반적인 FRS 문제는 다음과 같습니다.

  - 저널 랩: DFS 복제는 저널 랩에서 즉시 복구합니다. 기존의 각 파일 또는 폴더가 journalWrap으로 표시되고, 복제가 다시 활성화되기 전에 파일 시스템에 대해 확인됩니다. 복구 중에는 이 볼륨을 어느 방향으로도 복제에 사용할 수 없습니다.  
      
  - 과도한 복제: 과도한 복제를 방지하기 위해 DFS 복제는 크레딧 시스템을 사용합니다.  
      
  - 동일화된 폴더: 동일화된 폴더 이름을 방지하기 위해 DFS 복제는 충돌하는 데이터를 숨겨진 DfsrPrivate\\ConflictandDeleted 폴더(복제된 폴더의 로컬 경로 아래에 있음)에 저장합니다. 예를 들어 FRS를 사용하여 동일한 이름의 여러 폴더를 복제된 다른 서버에 동시에 만들면 FRS에서 이전 폴더의 이름을 바꿉니다. 대신 DFS 복제는 이전 폴더를 로컬 Conflict 및 Deleted 폴더로 이동시킵니다.  
      

### <a name="does-dfs-replication-replicate-files-in-chronological-order"></a>DFS 복제에서 파일을 시간 순서대로 복제하나요?

아니요. 파일이 시간 순서대로 복제되지 않을 수 있습니다.

### <a name="does-dfs-replication-replicate-files-that-are-being-used-by-another-application"></a>DFS 복제는 다른 애플리케이션에서 사용 중인 파일을 복제하나요?

애플리케이션에서 파일을 열고 열려 있는 동안 다른 애플리케이션에서 사용하지 못하도록 파일 잠금을 해당 파일에 만드는 경우 파일이 닫힐 때까지 DFS 복제에서 복제하지 않습니다. 애플리케이션에서 읽기 공유 액세스 권한으로 파일을 여는 경우에도 파일을 복제할 수 있습니다.

### <a name="does-dfs-replication-replicate-ntfs-file-permissions-alternate-data-streams-hard-links-and-reparse-points"></a>DFS 복제에서 NTFS 파일 권한, 대체 데이터 스트림, 하드 링크 및 재분석 지점을 복제하나요?

  - DFS 복제는 NTFS 파일 권한과 대체 데이터 스트림을 복제합니다.  
      
  - Microsoft는 복제된 폴더의 파일에 대한 NTFS 하드 링크 만들기를 지원하지 않습니다. 이러한 하드 링크를 만드는 경우 영향을 받는 파일에 대한 복제 문제가 발생할 수 있습니다. 하드 링크 파일은 DFS 복제에서 무시되며 복제되지 않습니다. 접합 지점도 복제되지 않으며, DFS 복제에서 발생하는 각 접합 지점에 대해 4406 이벤트를 기록합니다.  
      
  - DFS 복제에서 복제하는 유일한 재분석 지점은 IO\_REPARSE\_TAG\_SYMLINK 태그를 사용하는 지점입니다. 그러나 DFS 복제는 symlink의 대상도 복제되도록 보장하지 않습니다. 자세한 내용은 [디렉터리 서비스 팀에 문의 블로그](https://blogs.technet.com/b/askds/archive/2011/09/30/friday-mail-sack-super-slo-mo-edition.aspx)를 참조하세요.  
      
  - IO\_REPARSE\_TAG\_DEDUP, IO\_REPARSE\_TAG\_SIS 또는 IO\_REPARSE\_TAG\_HSM 재분석 태그가 있는 파일은 일반 파일로 복제됩니다. 재분석 지점은 로컬 시스템에서만 작동하므로 재분석 태그 및 재분석 데이터 버퍼는 다른 서버로 복제되지 않습니다. 따라서 DFS 복제는 Windows Server 2012의 데이터 중복 제거 또는 SIS(단일 인스턴스 스토리지)를 사용하는 볼륨에 있는 폴더를 복제할 수 있지만, 데이터 중복 제거 정보는 역할 서비스를 사용하도록 설정된 각 서버에서 별도로 유지 관리됩니다.  
      

### <a name="does-dfs-replication-replicate-timestamp-changes-if-no-other-changes-are-made-to-the-file"></a>파일에 다른 변경 내용이 없는 경우 DFS 복제에서 타임스탬프 변경 내용을 복제하나요?

아니요, DFS 복제는 타임스탬프만 변경된 파일을 복제하지 않습니다. 또한 파일에 다른 변경 내용이 없으면 변경된 타임스탬프는 복제 그룹의 다른 멤버에게 복제되지 않습니다.

### <a name="does-dfs-replication-replicate-updated-permissions-on-a-file-or-folder"></a>DFS 복제는 파일 또는 폴더에 대한 업데이트된 권한을 복제하나요?

예. DFS 복제는 파일 및 폴더에 대한 권한 변경 내용을 복제합니다. DFS 복제에서 여전히 전체 파일을 준비 영역으로 읽어야 하지만, ACL(액세스 제어 목록)과 연결된 파일의 일부만 복제됩니다.


> [!NOTE]
> 많은 파일에서 ACL을 변경하면 복제 성능에 영향을 줄 수 있습니다. 그러나 RDC를 사용하는 경우 전송되는 데이터의 양은 전체 파일의 크기가 아니라 ACL의 크기에 비례합니다. 준비 폴더에서 파일을 읽어야 하므로 디스크 트래픽 양은 여전히 파일 크기에 비례합니다. 
<br>


### <a name="does-dfs-replication-support-merging-text-files-in-the-event-of-a-conflict"></a>충돌이 발생하는 경우 DFS 복제에서 텍스트 파일 병합을 지원하나요?

충돌이 발생하는 경우 DFS 복제는 파일을 병합하지 않습니다. 그러나 충돌이 검색된 컴퓨터의 숨겨진 DfsrPrivate\\ConflictandDeleted 폴더에서 이전 버전의 파일을 유지하려고 합니다.

### <a name="does-dfs-replication-use-encryption-when-transmitting-data"></a>데이터를 전송할 때 DFS 복제에서 암호화를 사용하나요?

예. DFS 복제는 암호화를 사용하는 RPC(원격 프로시저 호출) 연결을 사용합니다.

### <a name="is-it-possible-to-disable-the-use-of-encrypted-rpc"></a>암호화된 RPC를 사용하지 않도록 설정할 수 있나요?

아니요. DFS 복제 서비스는 TCP를 통한 RPC(원격 프로시저 호출)를 사용하여 데이터를 복제합니다. 인터넷을 통한 데이터 전송을 보호하기 위해 DFS 복제 서비스는 항상 `RPC_C_AUTHN_LEVEL_PKT_PRIVACY` 인증 수준 상수를 사용하도록 설계되었습니다. 이렇게 하면 인터넷을 통한 RPC 통신이 항상 암호화됩니다. 따라서 DFS 복제 서비스에서 암호화된 RPC를 사용하지 않도록 설정할 수는 없습니다.

자세한 내용은 다음 Microsoft 웹 사이트를 방문하세요.

  - [RPC 기술 참조](https://go.microsoft.com/fwlink/?linkid=182278)  
      
  - [원격 차등 압축 정보](https://go.microsoft.com/fwlink/?linkid=182279)  
      
  - [인증 수준 상수](https://go.microsoft.com/fwlink/?linkid=182280)  
      

### <a name="how-are-simultaneous-replications-handled"></a>동시 복제는 어떻게 처리되나요?

복제된 폴더당 하나의 업데이트 관리자가 있습니다. 업데이트 관리자는 서로 독립적으로 작동합니다.

기본적으로 최대 16개(Windows Server 2003 R2의 경우 4개)의 동시 다운로드가 모든 연결 및 복제 그룹 간에 공유됩니다. 연결 및 복제 그룹 업데이트는 직렬화되지 않으므로 업데이트를 받는 특정 순서가 없습니다. 두 일정이 열려 있으면 일반적으로 두 연결에서 동시에 업데이트를 받고 설치합니다.

### <a name="how-do-i-force-replication-or-polling"></a>복제 또는 폴링을 강제로 적용하려면 어떻게 해야 하나요?

[복제 일정 편집](https://technet.microsoft.com/library/Cc732278)에서 설명한 대로 DFS 관리를 사용하여 복제를 강제로 즉시 적용할 수 있습니다. 또한 Windows Server 2012 R2에 도입된 DFSR PowerShell 모듈에 포함된 `Sync-DfsReplicationGroup` cmdlet 또는 **Dfsrdiag SyncNow** 명령을 사용하여 복제를 강제로 적용할 수도 있습니다. 폴링은 `Update-DfsrConfigurationFromAD` cmdlet 또는 **Dfsrdiag PollAD** 명령을 사용하여 강제로 적용할 수 있습니다.

### <a name="is-it-possible-to-configure-a-quiet-time-between-replications-for-files-that-change-frequently"></a>자주 변경되는 파일의 복제 간에 침묵 시간을 구성할 수 있나요?

아니요. 일정이 열려 있으면 DFS 복제에서 변경 내용 알림을 받는 대로 복제합니다. 파일에 대한 침묵 시간을 구성하는 방법이 없습니다.

### <a name="is-it-possible-to-configure-one-way-replication-with-dfs-replication"></a>DFS 복제를 사용하여 단방향 복제를 구성할 수 있나요?

예. Windows Server 2012 또는 Windows Server 2008 R2를 사용하는 경우 단방향 연결을 통해 콘텐츠를 복제하는 읽기 전용 복제 폴더를 만들 수 있습니다. 자세한 내용은 [특정 멤버에서 복제된 폴더를 읽기 전용으로 설정](https://go.microsoft.com/fwlink/?linkid=156740)(https://go.microsoft.com/fwlink/?LinkId=156740) 을 참조하세요.

Windows Server 2008 또는 Windows Server 2003 R2에서는 DFS 복제를 사용하여 단방향 복제 연결을 만들 수 없습니다. 이 연결을 만드는 경우 상태 검사 토폴로지 오류, 준비 문제, DFS 복제 데이터베이스 관련 문제를 포함하여 다양한 문제가 발생할 수 있습니다.

Windows Server 2008 또는 Windows Server 2003 R2를 사용하는 경우 다음 작업을 수행하여 단방향 연결을 시뮬레이션할 수 있습니다.

  - 주 서버로 지정하려는 서버에서만 변경하도록 관리자를 교육합니다. 그런 다음, 변경 내용을 대상 서버에 복제합니다.  
      
  - 최종 사용자에게 쓰기 권한이 없도록 대상 서버에 대한 공유 권한을 구성합니다. 지점 서버에서 변경이 허용되지 않으면 다시 복제할 항목이 없으므로 단방향 연결을 시뮬레이션하고 WAN 사용률을 낮게 유지할 수 있습니다.  
      

### <a name="is-there-a-way-to-force-a-complete-replication-of-all-files-including-unchanged-files"></a>변경되지 않은 파일을 포함하여 모든 파일의 전체 복제를 강제로 적용하는 방법이 있나요?

아니요. 파일이 동일하다고 간주되면 DFS 복제에서 해당 파일을 복제하지 않습니다. 변경된 파일이 복제되지 않았지만 DFS 복제가 변경된 파일을 복제하도록 구성된 경우 DFS 복제에서 해당 파일을 자동으로 복제합니다. 구성된 일정을 덮어쓰려면 **ForceReplicate()** WMI 메서드를 사용합니다. 그러나 이는 일정 재정의일 뿐이며, 변경되지 않았거나 동일한 파일을 강제로 복제하지는 않습니다.

### <a name="what-happens-if-the-primary-member-suffers-a-database-loss-during-initial-replication"></a>초기 복제 중에 주 멤버의 데이터베이스에 손실이 발생하는 경우 어떻게 되나요?

초기 복제 중에는 받는 멤버에게 주 멤버의 다른 버전의 파일이 있는 경우 발생하는 충돌 해결에서 주 멤버의 파일이 항상 우선적으로 적용됩니다. 주 멤버 지정은 Active Directory Domain Services에 저장되며, 주 멤버가 복제할 준비가 되었지만 복제 그룹의 모든 멤버가 복제하기 전에 해당 지정이 지워집니다.

초기 복제에 실패하거나 복제 중에 DFS 복제 서비스가 다시 시작되면, 주 멤버가 로컬 DFS 복제 데이터베이스에서 주 멤버 지정을 확인하여 초기 복제를 다시 시도합니다. Active Directory Domain Services에서 주 지정 이름을 지운 후에 주 멤버의 DFS 복제 데이터베이스가 손실되지만, 복제 그룹의 모든 멤버가 초기 복제를 완료하기 전에 주 멤버로 지정된 서버가 없으므로 복제 그룹의 모든 멤버가 폴더를 복제하지 못합니다. 이 경우 주 멤버 서버에서 **Dfsradmin membership /set /isprimary:true** 명령을 사용하여 주 멤버 지정을 수동으로 복원합니다.

초기 복제에 대한 자세한 내용은 [복제 그룹 만들기](https://technet.microsoft.com/library/cc725893)를 참조하세요.


> [!WARNING]
> 주 멤버 지정은 초기 복제 프로세스 중에만 사용됩니다. 복제가 완료된 후 <STRONG>Dfsradmin</STRONG> 명령을 사용하여 복제된 폴더의 주 멤버를 지정하는 경우 DFS 복제는 서버를 Active Directory Domain Services의 주 멤버로 지정하지 않습니다. 그러나 그 결과로 서버의 DFS 복제 데이터베이스에 복구할 수 없는 손상 또는 데이터 손실이 발생하면 서버에서 복제 그룹의 다른 멤버로부터 데이터를 복구하는 대신 주 멤버 권한으로 초기 복제를 수행하려고 합니다. 기본적으로 서버는 Rogue 주 서버가 되어 충돌이 발생할 수 있습니다. 이러한 이유로 초기 복제에 확실하게 실패한 경우에만 주 멤버를 수동으로 지정합니다. 
<br>


### <a name="what-happens-if-the-replication-schedule-closes-while-a-file-is-being-replicated"></a>파일을 복제하는 동안 복제 일정이 닫히면 어떻게 되나요?

연결에서 RDC (원격 차등 압축)를 사용하도록 설정된 경우 일정이 열리면(또는 **대역폭 없음** 이외의 다른 항목으로 변경되면) 일정이 닫히기 직전에(또는 **대역폭 없음**으로 변경되기 직전에) 복제를 시작한 64KB보다 큰 파일의 인바운드 복제가 계속됩니다. 복제가 중지되었을 때의 상태에서 복제가 계속됩니다.

RDC가 해제되면 DFS 복제에서 파일 전송을 완전히 다시 시작합니다. 받는 멤버에서 파일을 사용할 수 있는 경우 이 전송은 지연될 수 있습니다.

### <a name="what-happens-when-two-users-simultaneously-update-the-same-file-on-different-servers"></a>두 사용자가 서로 다른 서버에서 동일한 파일을 동시에 업데이트하는 경우 어떻게 되나요?

DFS 복제에서 충돌이 검색되면 마지막으로 저장된 파일의 버전을 사용합니다. 다른 파일은 DfsrPrivate\\ConflictandDeleted 폴더(충돌이 해결된 컴퓨터에 있는 복제된 폴더의 로컬 경로 아래)로 이동합니다. Conflict 및 Deleted 폴더가 구성된 크기를 초과하거나 DFS 복제에서 디스크 공간 부족 오류가 발생하는 경우 Conflict 및 Deleted 폴더는 정리될 때까지 그대로 유지됩니다. Conflict 및 Deleted 폴더는 복제되지 않으며, 이 충돌 해결 방법은 FRS에서 가능했던 동일화된 디렉터리 문제를 방지합니다.

충돌이 발생하면 DFS 복제에서 정보 이벤트를 DFS 복제 이벤트 로그에 기록합니다. 이 이벤트에는 다음과 같은 이유로 사용자 작업이 필요하지 않습니다.

  - 사용자에게 표시되지 않습니다(서버 관리자에게만 표시됨).  
      
  - DFS 복제는 Conflict 및 Deleted 폴더를 캐시로 처리합니다. 할당량 임계값에 도달하면 이러한 파일 중 일부가 정리됩니다. 충돌하는 파일이 저장되도록 보장하지 않습니다.  
      
  - 충돌이 충돌 원본과 다른 서버에 있을 수 있습니다.  
      

## <a name="staging"></a>준비

### <a name="does-dfs-replication-continue-staging-files-when-replication-is-disabled-by-a-schedule-or-bandwidth-throttling-quota-or-when-a-connection-is-manually-disabled"></a>일정 또는 대역폭 제한 할당량에 따라 복제를 사용하지 않도록 설정되었거나 연결을 사용하지 않도록 수동으로 설정된 경우에도 DFS 복제에서 파일을 계속 준비하나요?

아니요. 대역폭 제한 할당량을 초과했거나 연결을 사용하지 않도록 설정한 경우 DFS 복제는 예약된 복제 시간 이외의 파일을 계속 준비하지 않습니다.

### <a name="does-dfs-replication-prevent-other-applications-from-accessing-a-file-during-staging"></a>DFS 복제는 준비하는 동안 다른 애플리케이션에서 파일에 액세스하지 못하도록 방지하나요?

아니요. DFS 복제는 복제 폴더의 파일을 열지 못하도록 사용자 또는 애플리케이션을 차단하는 방식으로 파일을 엽니다. 이 방법을 "편의적 잠금"이라고 합니다.

### <a name="is-it-possible-to-change-the-location-of-the-staging-folder-with-the-dfs-management-tool"></a>DFS 관리 도구를 사용하여 준비 폴더의 위치를 변경할 수 있나요?

예. 준비 폴더 위치는 복제 그룹의 각 멤버에 대한 **속성** 대화 상자의 **고급** 탭에서 구성됩니다.

### <a name="when-are-files-staged"></a>파일이 준비되는 경우는 언제인가요?

다음 표와 같이 받는 멤버에서 파일을 요청하면(파일이 64KB 이하인 경우) 보내는 멤버에서 파일이 준비됩니다. 연결에서 RDC(원격 차등 압축)를 사용하지 않도록 설정된 경우 256KB 이하인 파일을 제외한 파일이 준비됩니다. 이 설정은 16KB와 1MB 사이에서 구성할 수 있지만 크기가 64KB 미만인 파일이 전송되므로 받는 멤버에서도 파일이 준비됩니다. 일정이 닫히면 파일이 준비되지 않습니다.

### <a name="the-minimum-file-sizes-for-staging-files"></a>파일 준비에 적용되는 최소 파일 크기

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th> </th>
<th>RDC 사용</th>
<th>RDC 사용 안 함</th>
</tr>
</thead>
<tbody>
<tr class="even">
<td><p>보내는 멤버</p></td>
<td><p>64KB</p></td>
<td><p>256KB</p></td>
</tr>
<tr class="odd">
<td><p>받는 멤버</p></td>
<td><p>기본적으로 64KB</p></td>
<td><p>기본적으로 64KB</p></td>
</tr>
</tbody>
</table>

### <a name="what-happens-if-a-file-is-changed-after-it-is-staged-but-before-it-is-completely-transmitted-to-the-remote-site"></a>파일을 준비한 후에 원격 사이트로 완전히 전송하기 전에 파일이 변경되면 어떻게 되나요?

파일의 일부가 이미 전송되고 있으면 DFS 복제에서 전송을 계속합니다. DFS 복제에서 파일 전송을 시작하기 전에 파일이 변경되면 최신 버전의 파일이 전송됩니다.

## <a name="change-history"></a>변경 내용


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>날짜</th>
<th>설명</th>
<th>이유</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>2018년 11월 15일</p></td>
<td><p>Windows Server 2019용으로 업데이트되었습니다.</p></td>
<td><p>새 운영 체제</p></td>
</tr>
<tr class="even">
<td><p>2013년 10월 9일</p></td>
<td><p>Windows Server 2012 R2에 대한 테스트 결과를 포함하도록 "지원되는 DFS 복제에 대한 제한 사항은 무엇인가요?" 섹션이 업데이트되었습니다.</p></td>
<td><p>최신 버전의 Windows Server에 대한 업데이트</p></td>
</tr>
<tr class="odd">
<td><p>2013년 1월 30일</p></td>
<td><p>"일정 또는 대역폭 제한 할당량에 따라 복제를 사용하지 않도록 설정되었거나 연결을 사용하지 않도록 수동으로 설정된 경우에도 DFS 복제에서 파일을 계속 준비하나요?" 항목이 추가되었습니다.</p></td>
<td><p>고객 질문</p></td>
</tr>
<tr class="even">
<td><p>2012년 10월 31일</p></td>
<td><p>볼륨에서 테스트되는 복제된 파일의 수를 늘리도록 "지원되는 DFS 복제에 대한 제한 사항은 무엇인가요?" 항목이 편집되었습니다.</p></td>
<td><p>고객 의견</p></td>
</tr>
<tr class="odd">
<td><p>2012년 8월 15일</p></td>
<td><p>DFS 복제에서 하드 링크 및 재분석 지점을 처리하는 방법을 명확히 설명하도록 "DFS 복제에서 NTFS 파일 권한, 대체 데이터 스트림, 하드 링크 및 재분석 지점을 복제하나요?" 항목이 편집되었습니다.</p></td>
<td><p>고객 지원 서비스의 피드백</p></td>
</tr>
<tr class="even">
<td><p>2012년 6월 13일</p></td>
<td><p>ReFS에 대한 토론을 추가하도록 "DFS 복제가 ReFS 또는 FAT 볼륨에서 작동하나요?" 항목이 편집되었습니다.</p></td>
<td><p>고객 의견</p></td>
</tr>
<tr class="odd">
<td><p>2012년 4월 25일</p></td>
<td><p>DFS 복제에서 하드 링크를 처리하는 방법을 명확히 설명하도록 "DFS 복제에서 NTFS 파일 권한, 대체 데이터 스트림, 하드 링크 및 재분석 지점을 복제하나요?" 항목이 편집되었습니다.</p></td>
<td><p>잠재적 혼동 감소</p></td>
</tr>
<tr class="even">
<td><p>2011년 3월 30일</p></td>
<td><p>.pst 및 Access 파일과 함께 DFS 복제를 사용할 경우 발생할 수 있는 영향을 수정하도록 "DFS 복제에서 Outlook .pst 또는 Microsoft Office Access 데이터베이스 파일을 복제할 수 있나요?" 항목이 편집되었습니다.</p>
<p>"복제 성능을 향상시키려면 어떻게 해야 하나요?" 항목이 추가되었습니다.</p></td>
<td><p>.pst 또는 Access 파일을 복제하면 DFS 복제 데이터베이스가 손상될 수 있다고 잘못 나타내는 이전 항목에 대한 고객 질문</p></td>
</tr>
<tr class="odd">
<td><p>2011년 1월 26일</p></td>
<td><p>"ConflictAndDeleted 또는 PreExisting 폴더에서 파일을 복구하려면 어떻게 해야 하나요?" 항목이 추가되었습니다.</p></td>
<td><p>고객 의견</p></td>
</tr>
<tr class="even">
<td><p>2010년 10월 20일</p></td>
<td><p>"DFS 복제 멤버를 업그레이드하거나 바꾸려면 어떻게 해야 하나요?" 항목이 추가되었습니다.</p></td>
<td><p>고객 의견</p></td>
</tr>
</tbody>
</table>

