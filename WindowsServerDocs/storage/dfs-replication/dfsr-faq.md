---
title: 'DFS 복제: FAQ(질문과 대답)'
ms.date: 06/18/2014
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: ee4dfe223635b176f10691c186144ed5360e3af7
ms.sourcegitcommit: 23a6e83b688119c9357262b6815c9402c2965472
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2019
ms.locfileid: "69560526"
---
# <a name="dfs-replication-frequently-asked-questions-faq"></a>DFS 복제: FAQ(질문과 대답)


업데이트됨: 2019 년 4 월 30 일

적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

이 FAQ에서는 Windows Server 용 dfs (분산 파일 시스템) 복제 (DFS (R) 또는 DFSR이 라고도 함)에 대 한 질문에 답변 합니다.

Dfs 네임 스페이스 [에 대 한 자세한 내용은 dfs 네임 스페이스: 질문과 대답](https://technet.microsoft.com/library/ee404780)

DFS 복제의 새로운 기능에 대 한 자세한 내용은 다음 항목을 참조 하세요.

  - [DFS 네임 스페이스 및 DFS 복제 개요](https://technet.microsoft.com/library/jj127250) (Windows Server 2012)  
      
  - [Windows server 2008에서 Windows server 2008 r 2로의 기능 변경 내용](https://technet.microsoft.com/library/dd391932) [분산 파일 시스템 항목의 새로운](https://technet.microsoft.com/library/ee307957) 기능  
      
  - Windows Server 2003 s p 1 [에서 Windows server 2008로 기능 변경](https://technet.microsoft.com/library/cc753208) 의 [분산 파일 시스템](https://technet.microsoft.com/library/cc753479) 항목  
      

이 항목에 대한 최근 변경 내용 목록은 이 항목의 [변경 내용](#change-history) 섹션을 참조하세요.

      

## <a name="interoperability"></a>상호 운용성

### <a name="can-dfs-replication-communicate-with-frs"></a>FRS와 DFS 복제 통신할 수 있나요?

아니요. DFS 복제는 FRS (파일 복제 서비스)와 통신 하지 않습니다. DFS 복제와 FRS는 동시에 동일한 서버에서 실행 될 수 있지만,이로 인해 데이터가 손실 될 수 있으므로 동일한 폴더 또는 하위 폴더를 복제 하도록 구성 해서는 안 됩니다.

### <a name="can-dfs-replication-replace-frs-for-sysvol-replication"></a>SYSVOL 복제를 위해 FRS를 대체할 DFS 복제 있습니다.

예, DFS 복제 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008을 실행 하는 서버에서 SYSVOL 복제를 위해 FRS를 대체할 수 있습니다. Windows Server 2003 r 2를 실행 하는 서버는 DFS 복제을 사용 하 여 SYSVOL 폴더를 복제할 수 없습니다.

DFS 복제를 사용 하 여 sysvol을 복제 하는 [방법에 대 한 자세한 내용은 sysvol 복제 마이그레이션 가이드를 참조 하세요. FRS를 DFS 복제](https://technet.microsoft.com/library/dd640019)합니다.

### <a name="can-i-upgrade-from-frs-to-dfs-replication-without-losing-configuration-settings"></a>구성 설정을 잃지 않고 FRS에서 DFS 복제로 업그레이드할 수 있나요?

예. FRS에서 DFS 복제로 복제를 마이그레이션하려면 다음 문서를 참조 하세요.

  - SYSVOL 폴더가 [아닌 폴더의 복제를 마이그레이션하려면 DFS 작업 가이드: Frs에서 DFS 복제](http://go.microsoft.com/fwlink/?linkid=192776) 및 [FRS2DFSR – frs에서 DFSR 마이그레이션 유틸리티](http://go.microsoft.com/fwlink/?linkid=195437) (http://go.microsoft.com/fwlink/?LinkID=195437) 로 마이그레이션  
      
  - Sysvol 폴더의 복제를 DFS 복제로 마이그레이션하려면 sysvol 복제 마이그레이션 [가이드를 참조 하세요. FRS를 DFS 복제](https://technet.microsoft.com/library/dd640019)합니다.  
      

### <a name="can-i-use-dfs-replication-in-a-mixed-windowsunix-environment"></a>혼합 된 Windows/UNIX 환경에서 DFS 복제를 사용할 수 있나요?

예. DFS 복제는 Windows Server를 실행 하는 서버 간에만 콘텐츠 복제를 지원 하지만 UNIX 클라이언트는 Windows 서버의 파일 공유에 액세스할 수 있습니다. 이렇게 하려면 DFS 복제 서버에 NFS (네트워크 파일 시스템) 용 서비스를 설치 합니다.

많은 UNIX 클라이언트에 포함 된 SMB/CIFS 클라이언트 기능을 사용 하 여 Windows 파일 공유에 직접 액세스할 수도 있습니다 .이 기능은 종종 제한적 이거나 Windows 환경에 대 한 수정이 필요 합니다 (예:를 사용 하 여 SMB 서명 사용 안 함). 그룹 정책).

DFS 복제는 Windows Server 운영 체제를 실행 하는 서버에서 NFS와 상호 운용할 수 있지만 NFS 탑재 지점을 복제할 수는 없습니다.

### <a name="can-i-use-the-volume-shadow-copy-service-with-dfs-replication"></a>DFS 복제에서 볼륨 섀도 복사본 서비스를 사용할 수 있나요?

예. DFS 복제은 VSS (볼륨 섀도 복사본 서비스) 볼륨에서 지원 되며 이전 버전의 클라이언트를 사용 하 여 이전 스냅숏을 복원할 수 있습니다.

### <a name="can-i-use-windowsbackup-ntbackupexe-to-remotely-back-up-a-replicated-folder"></a>Windows 백업 (Ntbackup.exe)을 사용 하 여 복제 된 폴더를 원격으로 백업할 수 있나요?

아니요, windows server 2003 또는 이전 버전을 실행 하는 컴퓨터에서 windows 백업 (Ntbackup.exe)을 사용 하 여 Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008을 실행 하는 컴퓨터에서 복제 된 폴더의 콘텐츠를 백업 하는 것은 지원 되지 않습니다.

복제 된 폴더에 저장 된 파일을 백업 하려면 Windows Server 백업 또는 Microsoft® System Center Data Protection Manager를 사용 합니다. Windows Server 2008 R2 및 Windows Server 2008의 백업 및 복구 기능에 대 한 자세한 내용은 [백업 및 복구](https://technet.microsoft.com/library/Cc754097)를 참조 하세요. 자세한 내용은 [System Center Data Protection Manager](http://go.microsoft.com/fwlink/?linkid=182261) (http://go.microsoft.com/fwlink/?LinkId=182261) 를 참조 하세요.

### <a name="do-file-system-policies-impact-dfs-replication"></a>파일 시스템 정책에 영향을 DFS 복제?

예. 복제 된 폴더에 대해 파일 시스템 정책을 구성 하지 마십시오. 파일 시스템 정책은 모든 그룹 정책 새로 고침 간격 마다 NTFS 사용 권한을 다시 적용 합니다. 이 경우 파일을 닫을 때까지 열려 있는 파일이 복제 되지 않기 때문에 공유 위반이 발생할 수 있습니다.

### <a name="does-dfs-replication-replicate-mailboxes-hosted-on-microsoft-exchange-server"></a>Microsoft Exchange Server에서 호스트 되는 사서함을 복제할 DFS 복제 있나요?

아니요. Microsoft Exchange Server에서 호스트 되는 사서함을 복제 하는 데 DFS 복제를 사용할 수 없습니다.

### <a name="does-dfs-replication-support-file-screens-created-by-file-server-resource-manager"></a>파일 서버 리소스 관리자에서 만든 파일 차단을 지원 DFS 복제?

예. 그러나 FSRM (파일 서버 리소스 관리자) 파일 차단 설정은 복제의 양쪽 끝에서 일치 해야 합니다. 또한 DFS 복제에는 복제에서 특정 파일 및 파일 형식을 제외 하는 데 사용할 수 있는 파일 및 폴더에 대 한 자체 필터 메커니즘이 있습니다.

다음은 파일 화면 또는 할당량을 구현 하기 위한 모범 사례입니다.

  - 숨겨진 DfsrPrivate 폴더는 할당량 또는 파일 차단이 적용 되지 않아야 합니다.  
      
  - 심사를 사용 하도록 설정 하기 전에는 차단 된 파일이 복제 된 폴더에 없어야 합니다.  
      
  - 할당량을 사용 하도록 설정 하기 전에 폴더는 할당량을 초과할 수 없습니다.  
      
  - 하드 할당량은 주의 해 서 사용 해야 합니다. 복제 그룹의 개별 구성원이 복제 전에 할당량 내에 유지 될 수 있지만 파일이 복제 될 때이를 초과할 수 있습니다. 예를 들어 사용자가 서버 A에 10mb 파일 (하드 제한)을 복사 하 고 다른 사용자가 5mb 파일을 서버 B로 복사 하는 경우, 다음 복제가 발생 하면 두 서버 모두 5 메가바이트의 할당량을 초과 하 게 됩니다. 이로 인해 DFS 복제에서 파일 복제를 지속적으로 다시 시도 하 여 버전 벡터 및 성능 문제를 일으킬 수 있습니다.  
      

### <a name="is-dfs-replication-cluster-aware"></a>DFS 복제 클러스터를 인식 하나요?

예, DFS 복제 windows server 2012 R2, Windows Server 2012 및 Windows Server 2008 r 2의 경우 장애 조치 (failover) 클러스터를 복제 그룹의 구성원으로 추가할 수 있습니다. 자세한 내용은 [복제 그룹에 장애 조치 (Failover) 클러스터 추가](http://go.microsoft.com/fwlink/?linkid=155085) (http://go.microsoft.com/fwlink/?LinkId=155085) 를 참조 하세요. Windows Server 2008 R2 이전의 Windows 버전에 대 한 DFS 복제 서비스는 장애 조치 (failover) 클러스터와 조정 하도록 설계 되지 않았으므로 서비스가 다른 노드로 장애 조치 (failover) 되지 않습니다.


> [!NOTE]
> DFS 복제는 클러스터 공유 볼륨의 파일 복제를 지원 하지 않습니다. 
<br>


### <a name="is-dfs-replication-compatible-with-data-deduplication"></a>데이터 중복 제거와 호환 DFS 복제?

예, DFS 복제 Windows Server에서 데이터 중복 제거를 사용 하는 볼륨의 폴더를 복제할 수 있습니다.

### <a name="is-dfs-replication-compatible-with-ris-and-wds"></a>DFS 복제 RIS 및 WDS와 호환 되나요?

예. DFS 복제 SIS (단일 인스턴스 저장소)를 사용 하도록 설정 된 볼륨을 복제 합니다. SIS는 RIS (원격 설치 서비스), WDS (Windows 배포 서비스) 및 Windows Storage 서버에서 사용 됩니다.

### <a name="is-it-possible-to-use-dfs-replication-with-offline-files"></a>오프라인 파일에서 DFS 복제를 사용할 수 있나요?

한 번에 한 명의 사용자만 파일에 쓰는 경우 시나리오에서 DFS 복제 및 오프라인 파일를 안전 하 게 사용할 수 있습니다. 이는 두 지점 간에 이동 하는 사용자가 분기 또는 오프 라인에서 파일에 액세스할 수 있게 하려는 경우에 유용 합니다. 오프라인 파일 오프 라인에서 사용 하기 위해 파일을 로컬로 캐시 하 고 DFS 복제 각 지점 간에 데이터를 복제 합니다.

DFS 복제는 분산 잠금 메커니즘 또는 파일 체크 아웃 기능을 제공 하지 않으므로 다중 사용자 환경에서 오프라인 파일와 함께 DFS 복제를 사용 하지 마세요. 두 사용자가 서로 다른 서버에서 동일한 파일을 동시에 수정 하는 경우 다음 복제 중에 DFS 복제 이전 파일\\을 복제 된 폴더의 로컬 경로 아래에 있는 DfsrPrivate ConflictandDeleted 폴더로 이동 합니다.

### <a name="what-antivirus-applications-are-compatible-with-dfs-replication"></a>DFS 복제와 호환 되는 바이러스 백신 응용 프로그램은 무엇 인가요?

바이러스 백신 응용 프로그램은 검색 활동이 복제 된 폴더의 파일을 변경 하는 경우 과도 한 복제를 발생 시킬 수 있습니다. 자세한 내용은 [DFS 복제와의 바이러스 백신 응용 프로그램 상호 운용성 테스트](http://go.microsoft.com/fwlink/?linkid=73990) (http://go.microsoft.com/fwlink/?LinkId=73990).

### <a name="what-are-the-benefits-of-using-dfs-replication-instead-of-windows-sharepoint-services"></a>Windows SharePoint Services 대신 DFS 복제를 사용 하면 어떤 이점이 있나요?

Windows® SharePoint® 서비스는 DFS 복제 되지 않는 파일 체크 아웃 기능 형태로 일관성 있는 일관성을 제공 합니다. 여러 사람이 동일한 파일을 편집 하는 것에 관심이 있는 경우 Windows SharePoint Services를 사용 하는 것이 좋습니다. Windows SharePoint Services 2.0 서비스 팩 2는 Windows Server 2003 r 2의 일부로 제공 됩니다. Microsoft 웹 사이트에서 Windows SharePoint Services를 다운로드할 수 있습니다. 최신 버전의 Windows Server에는 포함 되어 있지 않습니다. 그러나 여러 사이트에 걸쳐 데이터를 복제 하는 경우 사용자가 동시에 동일한 파일을 편집 하지 않는 경우에는 DFS 복제에서 더 높은 대역폭과 관리가 간단해 집니다.

## <a name="limitations-and-requirements"></a>제한 사항 및 요구 사항

### <a name="can-dfs-replication-replicate-between-branch-offices-without-a-vpn-connection"></a>VPN 연결을 사용 하지 않고 지점 간에 복제를 DFS 복제 수 있나요?

예-지사를 연결 하는 WAN (광역 네트워크) 링크 (인터넷 아님)가 있다고 가정 합니다. 그러나 외부 방화벽에서 적절 한 포트를 열어야 합니다. DFS 복제는 RPC 끝점 매퍼 (포트 135) 및 임의로 할당 된 삭제 포트 1024을 사용 합니다. **Dfsrdiag** 명령줄 도구를 사용 하 여 임시 포트 대신 고정 포트를 지정할 수 있습니다. RPC 끝점 매퍼를 지정 하는 방법에 대 한 자세한 내용은 Microsoft 기술 자료 [문서 154596](http://go.microsoft.com/fwlink/?linkid=73991) (http://go.microsoft.com/fwlink/?LinkId=73991) 을 참조 하십시오.

### <a name="can-dfs-replication-replicate-files-encrypted-with-the-encrypting-file-system"></a>파일 시스템 암호화로 암호화 된 파일을 복제할 DFS 복제 있습니다.

아니요. DFS 복제는 EFS (파일 시스템 암호화)를 사용 하 여 암호화 된 파일이 나 폴더를 복제 하지 않습니다. 사용자가 이전에 복제 된 파일을 암호화 하는 경우 DFS 복제은 복제 그룹의 다른 모든 구성원에서 해당 파일을 삭제 합니다. 이렇게 하면 사용 가능한 파일 복사본이 서버에서 암호화 된 버전 으로만 사용 됩니다.

### <a name="can-dfs-replication-replicate-outlook-pst-or-microsoft-office-access-database-files"></a>Outlook .pst 또는 Microsoft Office Access 데이터베이스 파일을 DFS 복제 복제할 수 있나요?

Microsoft Outlook 개인 폴더 파일 (.pst) 및 Microsoft Access 파일은 보관 목적으로 저장 되 고 Outlook 또는 Access (.pst 또는 Access to open)와 같은 클라이언트를 사용 하 여 네트워크에서 액세스 되지 않는 경우에만 안전 하 게 복제할 수 있습니다. DFS 복제 파일, 먼저 로컬 저장 장치에 파일을 복사 합니다. 이에 대 한 이유는 다음과 같습니다.

  - 네트워크 연결을 통해 .pst 파일을 열면 .pst 파일의 데이터가 손상 될 수 있습니다. 네트워크를 통해에서 .pst 파일에 안전 하 게 액세스할 수 없는 이유에 대 한 자세한 내용은 Microsoft 기술 자료 [문서 297019](http://go.microsoft.com/fwlink/?linkid=125363) (http://go.microsoft.com/fwlink/?LinkId=125363) 을 참조 하십시오.  
      
  - .pst 및 Access 파일은 Outlook 또는 Office Access와 같은 클라이언트에서 액세스 하는 동안 오랫동안 열려 있는 상태를 유지 하는 경향이 있습니다. 이렇게 하면 DFS 복제 닫힐 때까지 이러한 파일을 복제할 수 없습니다.  
      

### <a name="can-i-use-dfs-replication-in-a-workgroup"></a>작업 그룹에서 DFS 복제를 사용할 수 있나요?

아니요. DFS 복제는 구성에 대 한 Active Directory® 도메인 서비스에 의존 합니다. 도메인 에서만 작동 합니다.

### <a name="can-more-than-one-folder-be-replicated-on-a-single-server"></a>단일 서버에서 두 개 이상의 폴더를 복제할 수 있습니까?

예. DFS 복제는 서버 간에 다양 한 폴더를 복제할 수 있습니다. 복제 된 각 폴더가 고유한 루트 경로를 포함 하 고 중복 되지 않는지 확인 합니다. 예를 들어 d:\\sales 및 d:\\Accounting은 두 개의 복제 된 폴더에 대 한 루트 경로가 될 수\\있지만 d: sales\\및\\d: sales Reports는 두 개의 복제 된 폴더에 대 한 루트 경로가 될 수 없습니다.

### <a name="does-dfs-replication-require-dfs-namespaces"></a>DFS 네임 스페이스 DFS 복제 필요 한가요?

아니요. DFS 복제 및 DFS 네임 스페이스는 개별적으로 또는 함께 사용할 수 있습니다. 또한 DFS 복제를 사용 하 여 독립 실행형 DFS 네임 스페이스를 복제할 수 있으며,이는 FRS에서 가능 하지 않습니다.

### <a name="does-dfs-replication-require-time-synchronization-between-servers"></a>서버 간의 시간 동기화가 필요한 DFS 복제 있나요?

아니요. DFS 복제는 서버 간의 시간 동기화를 명시적으로 요구 하지 않습니다. 그러나 DFS 복제 서버 클록이 긴밀 하 게 일치 해야 합니다. Kerberos 인증이 제대로 작동 하려면 서버 클록이 서로 다른 5 분 내에 설정 되어 있어야 합니다 (기본값). 예를 들어 DFS 복제는 타임 스탬프를 사용 하 여 충돌이 발생 한 경우 어떤 파일이 우선적으로 적용 되는지 확인 합니다. 정확한 시간은 가비지 수집, 일정 및 기타 기능에도 중요 합니다.

### <a name="does-dfs-replication-support-replicating-an-entire-volume"></a>전체 볼륨 복제를 지원할 DFS 복제 있나요?

예. 그러나 Windows Server 2003 서비스 팩 2 또는 핫픽스를 먼저 설치 해야 합니다. 자세한 내용은 Microsoft 기술 자료 [문서 920335](http://go.microsoft.com/fwlink/?linkid=76776) (http://go.microsoft.com/fwlink/?LinkId=76776) 을 참조 하십시오. 또한 전체 볼륨을 복제 하면 다음과 같은 문제가 발생할 수 있습니다.

  - 볼륨에 Windows 페이징 파일이 포함 되어 있으면 복제에 실패 하 고 시스템 이벤트 로그에서 DFSR 이벤트 4312을 기록 합니다.  
      
  - DFS 복제은 대상 서버에서 복제 된 폴더의 시스템 및 숨겨진 특성을 설정 합니다. 이는 기본적으로 Windows에서 시스템 및 숨겨진 특성을 볼륨 루트 폴더에 적용 하기 때문에 발생 합니다. 대상 서버에서 복제 된 폴더의 로컬 경로가 볼륨 루트 이기도 한 경우 폴더 특성을 추가로 변경할 필요가 없습니다.  
      
  - Windows 시스템 폴더가 포함 된 볼륨을 복제 하는 경우 DFS 복제% WINDIR% 폴더를 인식 하 고 복제 하지 않습니다. 그러나 DFS 복제는 Microsoft가 아닌 응용 프로그램에서 사용 하는 폴더를 복제 하므로 응용 프로그램에 DFS 복제과의 상호 운용성 문제가 있는 경우 대상 서버에서 응용 프로그램이 실패할 수 있습니다.  
      

### <a name="does-dfs-replication-support-rpc-over-http"></a>RPC over HTTP를 지원할 DFS 복제 있나요?

아니요.

### <a name="does-dfs-replication-work-across-wireless-networks"></a>무선 네트워크에서 작동 DFS 복제 있나요?

예. DFS 복제는 연결 형식과는 독립적입니다.

### <a name="does-dfs-replication-work-on-refs-or-fat-volumes"></a>ReFS 또는 FAT 볼륨에서 작동 DFS 복제?

아니요. DFS 복제는 NTFS 파일 시스템으로 포맷 된 볼륨만 지원 합니다. ReFS (복원 파일 시스템) 및 FAT 파일 시스템은 지원 되지 않습니다. Ntfs 파일 시스템의 ntfs 변경 저널 및 기타 기능을 사용 하기 때문에 DFS 복제에는 NTFS가 필요 합니다.

### <a name="does-dfs-replication-work-with-sparse-files"></a>스파스 파일에 대 한 작업 DFS 복제?

예. 스파스 파일을 복제할 수 있습니다. **스파스** 특성은 받는 멤버에서 유지 됩니다.

### <a name="do-i-need-to-log-in-as-administrator-to-replicate-files"></a>파일을 복제 하려면 관리자 권한으로 로그인 해야 하나요?

아니요. DFS 복제는 로컬 시스템 계정으로 실행 되는 서비스 이므로 복제할 관리자 권한으로 로그인 할 필요가 없습니다. 그러나 DFS 복제 구성을 변경 하려면 영향을 받는 파일 서버의 도메인 관리자 또는 로컬 관리자 여야 합니다.

자세한 내용은 [DFS 복제를 관리할 수 있는 기능 위임](http://go.microsoft.com/fwlink/?linkid=182294) ()http://go.microsoft.com/fwlink/?LinkId=182294) 의 "DFS 복제 보안 요구 사항 및 위임"을 참조 하십시오.

### <a name="how-can-i-upgrade-or-replace-a-dfs-replication-member"></a>DFS 복제 구성원을 업그레이드 하거나 교체 하려면 어떻게 해야 하나요?

DFS 복제 구성원을 업그레이드 하거나 교체 하려면 디렉터리 서비스 팀 블로그에서 다음 블로그 게시물을 참조 하세요. [DFSR 구성원 하드웨어 또는 OS를 대체](http://blogs.technet.com/b/askds/archive/2010/09/10/series-wrap-up-and-downloads-replacing-dfsr-member-hardware-or-os.aspx)합니다.

### <a name="is-dfs-replication-suitable-for-replicating-roaming-profiles"></a>로밍 프로필을 복제 하는 데 적합 DFS 복제?

예. 로밍 사용자 프로필을 복제 하는 경우 특정 시나리오가 지원 됩니다. 지원 되는 시나리오에 대 한 자세한 내용은 [복제 된 사용자 프로필 데이터에 대 한 Microsoft의 지원 명세서](http://go.microsoft.com/fwlink/?linkid=201282) (http://go.microsoft.com/fwlink/?LinkId=201282) 를 참조 하세요.

### <a name="is-there-a-file-character-limit-or-limit-to-the-folder-depth"></a>파일 문자 제한이 있거나 폴더 깊이에 제한이 있나요?

Windows 및 DFS 복제는 최대 32000 자까지 폴더 경로를 지원 합니다. DFS 복제는 260 자의 폴더 경로로 제한 되지 않습니다.

### <a name="must-members-of-a-replication-group-reside-in-the-same-domain"></a>복제 그룹의 구성원이 동일한 도메인에 상주해 야 합니다.

아니요. 복제 그룹은 단일 포리스트 내의 여러 도메인에 걸쳐 있을 수 있지만 여러 포리스트에 걸쳐 있을 수 있습니다.

### <a name="what-are-the-supported-limits-of-dfs-replication"></a>DFS 복제 지원 되는 제한은 무엇 인가요?

다음 목록에서는 Windows Server 2012 r 2에서 Microsoft가 테스트 한 확장성 지침 집합을 제공 합니다.

  - 서버에 있는 모든 복제 된 파일의 크기: 100 테라바이트  
      
  - 볼륨의 복제 된 파일 수: 7000만.  
      
  - 최대 파일 크기: 250 기가바이트  
      


> [!IMPORTANT]
> 많은 수의 파일을 포함 하는 복제 그룹을 만들 때 데이터베이스 클론을 내보내고 초기 복제 기간을 최소화 하기 위해 사전 시드 기술을 사용 하는 것이 좋습니다. 자세한 내용은 Windows Server 2012 <A href="http://blogs.technet.com/b/filecab/archive/2013/08/21/dfs-replication-initial-sync-in-windows-server-2012-r2-attack-of-the-clones.aspx">r 2에서 DFS 복제 초기 동기화를 참조 하세요. 클론</A>의 공격입니다. 
<br>


다음 목록에서는 Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008에 대해 Microsoft에서 테스트 한 확장성 지침 집합을 제공 합니다.

  - 서버에 있는 모든 복제 된 파일의 크기: 10tb  
      
  - 볼륨의 복제 된 파일 수: 1100만.  
      
  - 최대 파일 크기: 64 기가바이트  
      


> [!NOTE]
> 더 이상 복제 그룹, 복제 된 폴더, 연결 또는 복제 그룹 구성원 수에 대 한 제한이 없습니다. 
<br>


Microsoft에서 Windows Server 2003 r 2 용으로 테스트 한 확장성 지침 목록은 [DFS 복제 확장성 지침](http://go.microsoft.com/fwlink/?linkid=75043) ()http://go.microsoft.com/fwlink/?LinkId=75043) 을 참조 하세요.

### <a name="when-should-i-not-use-dfs-replication"></a>DFS 복제를 사용 하지 않아야 하는 경우

여러 사용자가 서로 다른 서버에서 동일한 파일을 동시에 업데이트 하거나 수정 하는 환경에서는 DFS 복제을 사용 하지 마십시오. 이렇게 하면 DFS 복제 파일의 충돌 하는 복사본을 숨겨진 DfsrPrivate\\ConflictandDeleted 폴더로 이동할 수 있습니다.

여러 사용자가 서로 다른 서버에서 동일한 파일을 동시에 수정 해야 하는 경우에는 Windows SharePoint Services의 파일 체크 아웃 기능을 사용 하 여 한 사용자만 파일에서 작업 하 고 있는지 확인 합니다. Windows SharePoint Services 2.0 서비스 팩 2는 Windows Server 2003 r 2의 일부로 제공 됩니다. Microsoft 웹 사이트에서 Windows SharePoint Services를 다운로드할 수 있습니다. 최신 버전의 Windows Server에는 포함 되어 있지 않습니다.

### <a name="why-is-a-schema-update-required-for-dfs-replication"></a>DFS 복제에 스키마 업데이트가 필요한 이유는 무엇 인가요?

DFS 복제은 Active Directory Domain Services의 도메인 명명 컨텍스트에서 새 개체를 사용 하 여 구성 정보를 저장 합니다. 이러한 개체는 Active Directory Domain Services 스키마를 업데이트할 때 생성 됩니다. 자세한 내용은 DFS 복제 (http://go.microsoft.com/fwlink/?LinkId=182264) ) [의 요구 사항 검토](http://go.microsoft.com/fwlink/?linkid=182264) 를 참조 하세요.

## <a name="monitoring-and-management-tools"></a>모니터링 및 관리 도구

### <a name="can-i-automate-the-health-report-to-receive-warnings"></a>상태 보고서를 자동화 하 여 경고를 받을 수 있나요?

예. 상태 보고서를 자동화 하는 방법에는 다음 세 가지가 있습니다.

  - 예약 된 작업과 함께 Windows Server 2012 R2 또는 DfsrAdmin에 포함 된 DFSR Windows PowerShell 모듈을 사용 하 여 정기적으로 상태 보고서를 생성 합니다. 자세한 내용은 [DFS 복제 상태 보고서 자동화](http://go.microsoft.com/fwlink/?linkid=74010) (http://go.microsoft.com/fwlink/?LinkId=74010) 를 참조 하세요.  
      
  - System Center Operations Manager에 대 한 DFS 복제 관리 팩을 사용 하 여 지정 된 조건에 따라 경고를 만듭니다.  
      
  - DFS 복제 WMI 공급자를 사용 하 여 경고를 스크립팅 합니다.  
      

### <a name="can-i-use-microsoft-system-center-operations-manager-to-monitor-dfs-replication"></a>Microsoft System Center Operations Manager를 사용 하 여 DFS 복제를 모니터링할 수 있나요?

예. 자세한 내용은 Microsoft 다운로드 센터 ()http://go.microsoft.com/fwlink/?LinkId=182265) 에서 [System Center Operations Manager 2007에 대 한 DFS 복제 관리 팩](http://go.microsoft.com/fwlink/?linkid=182265) 을 참조 하세요.

### <a name="does-dfs-replication-support-remote-management"></a>원격 관리를 지원할 DFS 복제 있나요?

예. DFS 복제는 DFS 관리 콘솔과 **복제 그룹 추가** 명령을 사용 하 여 원격 관리를 지원 합니다. 예를 들어 서버 A에서 서버 A와 B를 구성원으로 사용 하 여 포리스트에 정의 된 복제 그룹에 연결할 수 있습니다.

DFS 관리는 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 및 Windows Server 2003 r 2에 포함 되어 있습니다. 다른 버전의 Windows에서 DFS 복제를 관리 하려면 원격 데스크톱 또는 [windows 7 용 원격 서버 관리 도구](https://technet.microsoft.com/library/Ee449475)를 사용 합니다.


> [!IMPORTANT]
> 읽기 전용 복제 폴더 또는 장애 조치 (failover) 클러스터용 구성원을 포함 하는 복제 그룹을 보거나 관리 하려면 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, 원격 서버에 포함 된 DFS 관리 버전을 사용 해야 합니다. <a href="http://go.microsoft.com/fwlink/p/?linkid=238560"> Windows 8 용 서버 관리 도구</a>또는 <a href="https://technet.microsoft.com/library/ee449475">windows 7에 대 한 원격 서버 관리 도구</a>입니다. 
<br>


### <a name="do-ultrasound-and-sonar-work-with-dfs-replication"></a>DFS 복제를 사용 하 여 Ultrasound 및 Sonar.projectname)을 사용 하나요?

아니요. DFS 복제에는 자체 모니터링 및 진단 도구 집합이 있습니다. Ultrasound 및 Sonar.projectname)는 FRS만 모니터링할 수 있습니다.

### <a name="how-can-files-be-recovered-from-the-conflictanddeleted-or-preexisting-folders"></a>ConflictAndDeleted 또는 기존 폴더에서 파일을 복구 하려면 어떻게 해야 하나요?

손실 된 파일을 복구 하려면 파일 히스토리, 파일 탐색기의 **이전 버전 복원** 명령을 사용 하거나 백업에서 파일을 복원 하 여 파일 시스템 폴더 또는 공유 폴더에서 파일을 복원 합니다. ConflictAndDeleted 또는 기존 폴더에서 직접 파일을 복구 하려면 및 `Get-DfsrPreservedFiles` `Restore-DfsrPreservedFiles` windows PowerShell cmdlet (windows Server 2012 r 2의 DFSR 모듈에 포함) 또는 MSDN의 [RestoreDFSR](http://code.msdn.microsoft.com/restoredfsr) 샘플 스크립트를 사용 합니다. 코드 갤러리. 이 스크립트는 재해 복구 전용 이며 보증 없이 있는 그대로 제공 됩니다.

### <a name="is-there-a-way-to-know-the-state-of-replication"></a>복제 상태를 확인 하는 방법이 있나요?

예. 복제를 모니터링 하는 방법에는 여러 가지가 있습니다.

  - DFS 복제에는 사전 모니터링을 제공 하는 System Center Operations Manager에 대 한 관리 팩이 있습니다.  
      
  - DFS 관리에는 복제 백로그, 복제 효율성 및 지정 된 복제 그룹의 파일 및 폴더 수에 대 한 기본 진단 보고서가 있습니다.  
      
  - Windows Server 2012 r 2의 DFSR Windows PowerShell 모듈에는 전파 테스트를 시작 하 고 전파 및 상태 보고서를 작성 하기 위한 cmdlet이 포함 되어 있습니다. 자세한 내용은 [분산 파일 시스템 Replication cmdlet In Windows PowerShell](https://technet.microsoft.com/library/dn296601.aspx)을 참조 하세요.  
      
  - Dfsrdiag는 백로그 수를 생성 하거나 전파 테스트를 트리거할 수 있는 명령줄 도구입니다. 둘 다 복제 상태를 표시 합니다. 전파는 파일이 모든 노드에 복제 되 고 있는지를 표시 합니다. 백로그는 두 대의 컴퓨터가 동기화 되기 전에 복제 해야 하는 파일 수를 표시 합니다. 백로그 수는 복제 그룹 구성원이 처리 하지 않은 업데이트 수입니다. Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 r 2를 실행 하는 컴퓨터에서 Dfsrdiag가 현재 복제 중인 업데이트 DFS 복제 표시할 수도 있습니다.  
      
  - 스크립트는 WMI를 사용 하 여 백로그 정보 (수동 또는 MOM)를 수집할 수 있습니다.  
      

## <a name="performance"></a>성능

### <a name="does-dfs-replication-support-dial-up-connections"></a>전화 접속 연결을 지원 DFS 복제?

DFS 복제는 전화 접속 속도에서 작동 하지만 복제할 변경 내용이 많을 경우 백로그를 가져올 수 있습니다. 기존 파일을 약간만 변경 하는 경우에는 RDC (원격 차등 압축)를 사용 하는 DFS 복제 파일을 직접 복사 하는 것 보다 훨씬 더 높은 성능을 제공 합니다.

### <a name="does-dfs-replication-perform-bandwidth-sensing"></a>대역폭 감지를 수행할 DFS 복제 있나요?

아니요. DFS 복제 대역폭 감지를 수행 하지 않습니다. 연결 단위로 제한 된 대역폭 (대역폭 제한)을 사용 하도록 DFS 복제를 구성할 수 있습니다. 그러나 네트워크 인터페이스가 포화 상태가 되는 경우 DFS 복제는 대역폭 사용률을 더 줄일 수 없으며, DFS 복제 짧은 기간 동안 링크의 포화 상태를 설정할 수 있습니다. RPC 호출을 제한 하 여 대역폭을 제한 때문 DFS 복제에 DFS 복제 대역폭 제한은 완전히 정확 하지 않습니다. 결과적으로, 네트워크 스택 (RPC 포함)의 하위 수준에 있는 다양 한 버퍼가 방해할 수 있으므로 네트워크 트래픽이 급증 하 게 됩니다.

### <a name="does-dfs-replication-throttle-bandwidth-per-schedule-per-server-or-per-connection"></a>일정 당, 서버당 또는 연결당 제한 대역폭을 DFS 복제 합니까?

일정을 지정할 때 대역폭 제한을 구성 하면 해당 복제 그룹에 대 한 모든 연결에서 해당 설정을 대역폭 제한에 사용 합니다. DFS 관리를 사용 하는 연결 수준 설정으로 대역폭 제한을 설정할 수도 있습니다.

### <a name="does-dfs-replication-use-active-directory-domain-services-to-calculate-site-links-and-connection-costs"></a>Active Directory Domain Services를 사용 하 여 사이트 링크와 연결 비용을 계산 DFS 복제?

아니요. DFS 복제는 관리자가 정의한 토폴로지를 사용 합니다 .이 토폴로지는 Active Directory Domain Services 사이트 비용에 독립적입니다.

### <a name="how-can-i-improve-replication-performance"></a>복제 성능을 향상 하려면 어떻게 해야 하나요?

복제 성능 튜닝에 대 한 다양 한 방법에 대해 알아보려면 [디렉터리 서비스 팀 블로그](http://blogs.technet.com/b/askds/)를 참조 하 여 [DFSR에서 복제 성능 조정](http://blogs.technet.com/b/askds/archive/2010/03/31/tuning-replication-performance-in-dfsr-especially-on-win2008-r2.aspx) 을 참조 하세요.

### <a name="how-does-dfs-replication-avoid-saturating-a-connection"></a>에서 연결의 포화를 방지 하는 방법 DFS 복제

DFS 복제에서 연결에 사용할 최대 대역폭을 설정 하 고 서비스는 네트워크 사용 수준을 유지 합니다. 이는 Background Intelligent Transfer Service (비트)와 다르며, 적절 하 게 설정 하는 경우 연결을 포화 하지 않습니다 DFS 복제.

그럼에도 불구 하 고 대역폭 제한은 100% 정확 하지 않으며 짧은 시간 동안 링크의 포화를 DFS 복제 수 있습니다. 이는 DFS 복제 RPC 호출을 제한 하 여 대역폭을 제한 때문입니다. 이 프로세스는 RPC를 비롯 하 여 네트워크 스택의 하위 수준에 있는 다양 한 버퍼를 사용 하기 때문에 네트워크 링크의 포화 시간을 초과할 수 있는 복제 트래픽이 버스트로 이동 하는 경향이 있습니다.

Windows server 2008의 DFS 복제에는 [분산 파일 시스템](https://technet.microsoft.com/library/Cc753479)에 설명 된 대로 몇 가지 성능 향상이 포함 되어 있습니다 .이 항목은 [windows server 2003 s p 1에서 windows server 2008로의 기능 변경 내용](https://technet.microsoft.com/library/cc753208)에 설명 되어 있습니다.

### <a name="how-does-dfs-replication-performance-compare-with-frs"></a>DFS 복제 성능이 FRS와 어떻게 비교 되나요?

특히 큰 파일을 약간만 변경 하 고 RDC를 사용 하도록 설정한 경우 DFS 복제는 FRS 보다 훨씬 빠릅니다. 예를 들어 RDC를 사용 하는 경우 2mb PowerPoint® 프레젠테이션이 약간만 변경 되 면 네트워크를 통해 60 킬로바이트 (KB)의 전송 (97%의 절약 바이트)이 발생할 수 있습니다.

RDC는 64 보다 작은 파일에는 사용 되지 않으며 네트워크 대역폭이 경합이 없는 고속 Lan에서는 유용 하지 않을 수 있습니다. RDC는 DFS 관리를 사용 하 여 연결 별로 사용 하지 않도록 설정할 수 있습니다.

### <a name="how-frequently-does-dfs-replication-replicate-data"></a>얼마나 자주 DFS 복제 데이터를 복제 하나요?

사용자가 설정한 일정에 따라 데이터가 복제 됩니다. 예를 들어 일정을 15 분 간격으로, 일주일에 7 일로 설정할 수 있습니다. 이러한 간격 동안에는 복제를 사용할 수 있습니다. 파일 변경이 검색 된 후에 즉시 복제가 시작 됩니다 (일반적으로 몇 초 내에).

연결 일정이 받는 구성원의 현지 시간으로 설정 되어 있는 동안에는 복제 그룹 일정을 UTC (Universal Time 좌표)로 설정할 수 있습니다. 복제 그룹이 여러 표준 시간대에 걸쳐 있을 때이를 고려해 야 합니다. 현지 시간은 인바운드 연결을 호스트 하는 멤버의 시간을 의미 합니다. 일정을 현지 시간으로 설정 하는 경우 인바운드 연결 및 해당 아웃 바운드 연결의 표시 된 일정은 표준 시간대 차이를 반영 합니다.

### <a name="how-much-of-my-servers-system-resources-will-dfs-replication-consume"></a>서버 시스템 리소스의 DFS 복제 사용 되는 양은 얼마 인가요?

DFS 복제에서 사용 하는 디스크, 메모리 및 CPU 리소스는 파일의 수와 크기, 변경 비율, 복제 그룹 구성원 수 및 복제 된 폴더 수를 비롯 한 여러 요인에 따라 달라 집니다. 또한 일부 리소스는 예측이 어렵습니다. 예를 들어 DFS 복제 데이터베이스에 사용 되는 ESE (Extensible Storage Engine) 기술은 사용 가능한 메모리의 상당 부분을 소비할 수 있으며,이 기술은 필요할 때 해제 됩니다. DFS 복제 이외의 응용 프로그램은 서버 구성에 따라 동일한 서버에서 호스팅될 수 있습니다. 그러나 단일 서버에서 여러 응용 프로그램 또는 서버 역할을 호스팅하는 경우 프로덕션 환경에서 구현 하기 전에이 구성을 테스트 하는 것이 중요 합니다.

### <a name="what-happens-if-a-wan-link-fails-during-replication"></a>복제 하는 동안 WAN 링크에 오류가 발생 하면 어떻게 되나요?

연결이 중단 되 면 일정을 여는 동안 DFS 복제가 복제를 계속 시도 합니다. MOM을 사용 하 여 수집 될 수 있는 DFS 복제 이벤트 로그 (사전에 경고를 통해) 및 DFS 복제 상태 보고서 (관리자가 실행 하는 경우와 같은 대응적)에도 연결 오류가 기록 됩니다.

## <a name="remote-differential-compression-details"></a>원격 차등 압축 정보

### <a name="are-changes-compressed-before-being-replicated"></a>복제 전에 변경 내용을 압축 합니까?

예. 파일의 변경 된 부분은 이미 압축 된 다음을 제외한 모든 파일 형식에 대해 전송 되기 전에 압축 됩니다. wma, .wmv, .zip, .jpg,. mpg,. m,. .m1v,. mp2,. mp3,, .cab, .wav,. snd, au, .asf, .asf, .avi, a-z, release.tar.gz,. tgz 및 frx입니다. 이러한 파일 형식에 대 한 압축 설정은 Windows Server 2003 r 2에서 구성할 수 없습니다.

### <a name="can-an-administrator-turn-off-rdc-or-change-the-threshold"></a>관리자가 RDC를 끄거나 임계값을 변경할 수 있나요?

예. 지정 된 연결의 속성 페이지를 통해 RDC를 해제할 수 있습니다. RDC를 사용 하지 않도록 설정 하면 대역폭 제약 조건이 없거나 64 미만의 파일을 주로 구성 하는 복제 그룹에 대 한 CPU 사용률 및 복제 대기 시간을 줄일 수 있습니다. 연결에서 RDC를 사용 하지 않도록 선택 하는 경우 변경 전후에 복제 효율성을 테스트 하 여 복제 성능이 개선 되었는지 확인 합니다.

**Dfsradmin 연결 집합** 명령, DFS 복제 WMI 공급자 또는 구성 XML 파일을 수동으로 편집 하 여 RDC 크기 임계값을 변경할 수 있습니다.

### <a name="does-rdc-work-on-all-file-types"></a>RDC는 모든 파일 형식에서 작동 하나요?

예. RDC는 파일 데이터 형식과 관계 없이 블록 수준에서 차이를 계산 합니다. 그러나 RDC는 Word 문서, PST 파일, VHD 이미지 등의 특정 파일 형식에서 보다 효율적으로 작동 합니다.

### <a name="how-does-rdc-work-on-a-compressed-file"></a>RDC는 압축 된 파일에서 어떻게 작동 하나요?

DFS 복제는 RDC를 사용 하 여 변경 된 파일의 블록을 계산 하 고 네트워크를 통해 해당 블록만 보냅니다. DFS 복제는 파일의 내용에 대 한 정보를 알 필요가 없으며, 해당 블록만 변경 된 것입니다.

### <a name="is-cross-file-rdc-enabled-when-upgrading-to-windows-server-enterprise-edition-or-datacenter-edition"></a>Windows Server Enterprise Edition 또는 Datacenter Edition으로 업그레이드할 때 파일 간 RDC를 사용할 수 있나요?

Windows Server Standard Edition은 파일 간 RDC를 지원 하지 않습니다. 그러나 파일 간 RDC를 지 원하는 버전으로 업그레이드 하거나 복제 연결의 멤버가 지원 되는 버전을 실행 하는 경우 자동으로 사용 하도록 설정 됩니다. 파일 간 RDC를 지 원하는 버전 목록은 Windows 운영 체제에서 파일 간 RDC를 지 원하는 버전을 참조 하세요.

### <a name="is-rdc-true-block-level-replication"></a>RDC true 블록 수준 복제 여부

아니요. RDC는 파일 전송을 압축 하기 위한 범용 프로토콜입니다. DFS 복제는 디스크 블록 수준이 아닌 파일 수준에서 RDC를 사용 합니다. RDC는 파일을 블록으로 나눕니다. 파일의 각 블록에 대해 더 큰 블록을 나타낼 수 있는 작은 바이트 수 인 서명을 계산 합니다. 서명 집합은 서버에서 클라이언트로 전송 됩니다. 클라이언트는 서버 서명을 자체와 비교 합니다. 클라이언트는 클라이언트에 아직 없는 서명의 데이터만 보내도록 서버에 요청 합니다.

### <a name="what-happens-if-i-rename-a-file"></a>파일의 이름을 바꾸면 어떻게 되나요?

DFS 복제 다음 복제 중에 복제 그룹의 다른 모든 구성원에서 파일의 이름을 바꿉니다. 파일은 고유 ID를 사용 하 여 추적 되므로 파일의 이름을 바꾸고 복제본 내에서 파일을 이동 하는 것은 파일을 복제 하 DFS 복제 기능에 영향을 주지 않습니다.

### <a name="what-is-cross-file-rdc"></a>파일 간 RDC 란?

파일 간 RDC를 사용 하면 동일한 이름의 파일이 클라이언트 끝에 없는 경우에도 DFS 복제 RDC를 사용할 수 있습니다. 파일 간 RDC는 추론을 사용 하 여 복제 해야 하는 파일과 유사한 파일을 결정 하 고 복제 파일과 동일한 유사한 파일의 블록을 사용 하 여 WAN을 통해 전송 되는 데이터의 양을 최소화 합니다. 파일 간 RDC는이 프로세스에서 최대 5 개의 비슷한 파일 블록을 사용할 수 있습니다.

파일 간 RDC를 사용 하려면 복제 연결의 한 구성원에서 파일 간 RDC를 지 원하는 Windows 버전을 실행 해야 합니다. 파일 간 RDC를 지 원하는 버전 목록은 Windows 운영 체제에서 파일 간 RDC를 지 원하는 버전을 참조 하세요.

### <a name="what-is-rdc"></a>RDC 란?

RDC (원격 차등 압축)는 제한 된 대역폭 네트워크를 통해 효율적으로 파일을 업데이트 하는 데 사용할 수 있는 클라이언트-서버 프로토콜입니다. RDC는 파일에서 데이터의 삽입, 제거 및 다시 정렬을 검색 하 여 파일이 업데이트 될 때 변경 내용만 복제할 DFS 복제 수 있도록 합니다. RDC는 기본적으로 64 KB 이상인 파일에만 사용 됩니다. RDC는 복제 된 폴더 또는 복제 된 폴더의 로컬 경로 아래에 있는 DfsrPrivate\\ConflictandDeleted 폴더에서 이름이 같은 이전 버전의 파일을 사용할 수 있습니다.

### <a name="when-is-rdc-used-for-replication"></a>RDC가 복제에 사용 되는 경우

파일이 최소 크기 임계값을 초과 하는 경우 RDC가 사용 됩니다. 이 크기 임계값은 기본적으로 64 KB입니다. 이 임계값을 초과 하는 파일을 복제 한 후에는 파일의 일부를 변경 하거나 RDC를 사용 하지 않는 한, 업데이트 된 버전의 파일은 항상 RDC를 사용 합니다.

### <a name="which-editions-of-the-windows-operating-system-support-cross-file-rdc"></a>파일 간 RDC를 지 원하는 Windows 운영 체제 버전은 무엇입니까?

파일 간 RDC를 사용 하려면 복제 연결의 한 구성원에서 파일 간 RDC를 지 원하는 Windows 운영 체제 버전을 실행 해야 합니다. 다음 표에서는 Windows 운영 체제에서 파일 간 RDC를 지 원하는 버전을 보여 줍니다.

### <a name="cross-file-rdc-availability-in-editions-of-the-windows-operating-system"></a>Windows 운영 체제 버전에서 파일 간 RDC 가용성

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
<td><p>사용자 계정 컨트롤</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2003 R2</p></td>
<td><p>아니요</p></td>
<td><p>사용자 계정 컨트롤</p></td>
<td><p>아니요</p></td>
</tr>
</tbody>
</table>

\*필요에 따라 Windows Server 2012 r 2에서 파일 간 RDC를 사용 하지 않도록 설정할 수 있습니다.

## <a name="replication-details"></a>복제 세부 정보

### <a name="can-i-change-the-path-for-a-replicated-folder-after-it-is-created"></a>복제 된 폴더를 만든 후 해당 폴더에 대 한 경로를 변경할 수 있나요?

아니요. 복제 된 폴더의 경로를 변경 해야 하는 경우 DFS 관리에서 삭제 하 고 새 복제 된 폴더로 다시 추가 해야 합니다. 그런 다음 DFS 복제는 RDC (원격 차등 압축)를 사용 하 여 데이터를 보내고 받는 구성원의 데이터와 동일한 지 여부를 확인 하는 동기화를 수행 합니다. 폴더의 모든 데이터를 다시 복제 하지는 않습니다.

### <a name="can-i-configure-which-file-attributes-are-replicated"></a>복제할 파일 특성을 구성할 수 있나요?

아니요, DFS 복제 복제할 파일 특성을 구성할 수 없습니다.

특성 값 및 해당 설명의 목록은 MSDN의 [파일 특성](http://go.microsoft.com/fwlink/?linkid=182268) (http://go.microsoft.com/fwlink/?LinkId=182268) 을 참조 하세요.

다음 특성 값은 `SetFileAttributes dwFileAttributes` 함수를 사용 하 여 설정 되며 DFS 복제에 의해 복제 됩니다. 이러한 특성 값을 변경 하면 특성 복제가 트리거됩니다. 내용이 변경 되는 경우를 제외 하 고 파일의 내용은 복제 되지 않습니다. 자세한 내용은 MSDN 라이브러리 ()http://go.microsoft.com/fwlink/?LinkId=182269) 의 [setfileattributes 함수](http://go.microsoft.com/fwlink/?linkid=182269) 를 참조 하세요.

  - 파일\_특성\_숨김  
      
  - 파일\_특성\_READONLY  
      
  - 파일\_특성\_시스템  
      
  - 파일\_\_특성이\_콘텐츠인덱싱되지\_않음  
      
  - 오프\_라인\_파일 특성  
      

다음 특성 값은 DFS 복제에 의해 복제 되지만 복제를 트리거하지 않습니다.

  - 파일\_특성\_보관  
      
  - 파일\_특성\_정상  
      

다음 파일 특성 값도 `SetFileAttributes` 함수를 사용 하 여 설정할 수는 없지만 ( `GetFileAttributes` 함수를 사용 하 여 특성 값 보기) 복제를 트리거합니다.

  - 파일\_특성\_재분석지점\_  
      

> [!NOTE]
> 재분석 태그가 IO_REPARSE_TAG_SYMLINK 않는 한 DFS 복제은 재분석 지점 특성 값을 복제 하지 않습니다. IO_REPARSE_TAG_DEDUP, IO_REPARSE_TAG_SIS 또는 IO_REPARSE_TAG_HSM 재분석 태그가 있는 파일은 일반 파일로 복제 됩니다. 그러나 재분석 지점은 로컬 시스템 에서만 작동 하므로 재분석 태그 및 재분석 데이터 버퍼는 다른 서버로 복제 되지 않습니다. 
<br>

  - 압축\_된\_파일 특성  
      
  - 암호화\_된\_파일 특성  
      

> [!NOTE]
> DFS 복제는 EFS (파일 시스템 암호화)를 사용 하 여 암호화 된 파일을 복제 하지 않습니다. DFS 복제는 타사 소프트웨어를 사용 하 여 암호화 된 파일을 복제 하지만 파일에 FILE_ATTRIBUTE_ENCRYPTED 특성 값이 설정 되지 않은 경우에만이 파일을 복제 합니다. 
<br>

  - 파일\_특성\_스파스파일\_  
      
  - 파일\_특성\_디렉터리  
      

DFS 복제 파일\_특성\_임시 값을 복제 하지 않습니다.

### <a name="can-i-control-which-member-is-replicated"></a>복제할 멤버를 제어할 수 있나요?

예. 복제 그룹을 만들 때 토폴로지를 선택할 수 있습니다. 또는 **토폴로지 없음** 을 선택 하 고 복제 그룹을 만든 후에 연결을 수동으로 구성할 수 있습니다.

### <a name="can-i-seed-a-replication-group-member-with-data-prior-to-the-initial-replication"></a>초기 복제 전에 데이터를 사용 하 여 복제 그룹 구성원의 초기값을 지정할 수 있나요?

예. DFS 복제는 초기 복제 전에 복제 그룹 구성원에 파일을 복사 하는 것을 지원 합니다. 이 "사전 준비"는 초기 복제 중에 복제 되는 데이터의 양을 크게 줄일 수 있습니다.

파일이 실제 특성 또는 타임 스탬프에 의해서만 다를 경우 초기 복제는 콘텐츠를 복제할 필요가 없습니다. 실제 특성은 Win32 함수 `SetFileAttributes`에서 설정할 수 있는 특성입니다. 자세한 내용은 MSDN 라이브러리 ()http://go.microsoft.com/fwlink/?LinkId=182269) 의 [setfileattributes 함수](http://go.microsoft.com/fwlink/?linkid=182269) 를 참조 하세요. 두 파일이 압축과 같은 다른 특성에 따라 다르면 파일의 내용이 복제 됩니다.

복제 그룹 구성원을 사전 준비 하려면 대상 서버의 해당 폴더에 파일을 복사 하 고 복제 그룹을 만든 다음 주 구성원을 선택 합니다. 주 구성원의 내용이 "신뢰할 수 있는" 것으로 간주 되기 때문에 복제 하려는 최신 파일이 있는 구성원을 선택 합니다. 즉, 초기 복제 중에 주 구성원의 파일은 항상 복제 그룹의 다른 멤버에 있는 다른 버전의 파일을 덮어씁니다.

DFSR 데이터베이스를 미리 시드해야 하 고 복제 하는 방법에 대 [한 자세한 내용은 Windows Server 2012 r 2에서 DFS 복제 초기 동기화를 참조 하세요. 클론](http://blogs.technet.com/b/filecab/archive/2013/08/21/dfs-replication-initial-sync-in-windows-server-2012-r2-attack-of-the-clones.aspx)의 공격입니다.

초기 복제에 대 한 자세한 내용은 [복제 그룹 만들기](https://technet.microsoft.com/library/cc725893)를 참조 하세요.

### <a name="does-dfs-replication-overcome-common-file-replication-service-issues"></a>일반적인 파일 복제 서비스 문제를 해결할 DFS 복제 있나요?

예. DFS 복제 일반적인 세 가지 FRS 문제를 극복 합니다.

  - 저널 줄 바꿈: 저널에서 복구 하는 DFS 복제 즉시 래핑합니다. 복제를 다시 사용 하기 전에 각 기존 파일 또는 폴더가 journalWrap로 표시 되 고 파일 시스템에 대해 확인 됩니다. 복구 하는 동안에는 어느 방향으로도 복제에이 볼륨을 사용할 수 없습니다.  
      
  - 과도 한 복제: 과도 한 복제를 방지 하기 위해 DFS 복제 크레딧을 시스템을 사용 합니다.  
      
  - 머프 폴더: 머프 폴더 이름을 방지 하기 위해 DFS 복제는 복제 된 폴더의 로컬 경로\\아래에 있는 숨겨진 DfsrPrivate ConflictandDeleted 폴더에 충돌 하는 데이터를 저장 합니다. 예를 들어 FRS를 사용 하 여 복제 된 다른 서버에서 동일한 이름을 사용 하 여 여러 폴더를 동시에 만들면 FRS에서 이전 폴더의 이름을 바꿉니다. DFS 복제 대신 이전 폴더를 로컬 충돌 및 삭제 된 폴더로 이동 합니다.  
      

### <a name="does-dfs-replication-replicate-files-in-chronological-order"></a>파일을 시간 순서 대로 복제 DFS 복제?

아니요. 파일이 순서 대로 복제 될 수 있습니다.

### <a name="does-dfs-replication-replicate-files-that-are-being-used-by-another-application"></a>다른 응용 프로그램에서 사용 중인 파일을 복제할 DFS 복제 있습니까?

응용 프로그램에서 파일을 열고 파일 잠금을 만들면 (열려 있는 동안 다른 응용 프로그램에서 해당 파일을 사용할 수 없도록 함) DFS 복제 파일을 닫을 때까지 파일을 복제 하지 않습니다. 응용 프로그램이 읽기-공유 액세스를 사용 하 여 파일을 여는 경우에도 파일을 복제할 수 있습니다.

### <a name="does-dfs-replication-replicate-ntfs-file-permissions-alternate-data-streams-hard-links-and-reparse-points"></a>NTFS 파일 사용 권한, 대체 데이터 스트림, 하드 링크 및 재분석 지점은 DFS 복제 복제 하나요?

  - DFS 복제 NTFS 파일 사용 권한과 대체 데이터 스트림을 복제 합니다.  
      
  - Microsoft는 복제 된 폴더의 파일에 대 한 NTFS 하드 링크 생성을 지원 하지 않습니다. 이렇게 하면 영향을 받는 파일에서 복제 문제가 발생할 수 있습니다. 하드 링크 파일은 DFS 복제에서 무시 되 고 복제 되지 않습니다. 또한 연결 지점은 복제 되지 않으며 DFS 복제는 발생 하는 각 연결 지점에 대해 이벤트 4406을 기록 합니다.  
      
  - DFS 복제에서 복제 하는 유일한 재분석 지점은 IO\_재분석\_태그\_SYMLINK 태그를 사용 하는 것 이지만 DFS 복제는 SYMLINK의 대상도 복제 되도록 보장 하지 않습니다. 자세한 내용은 [디렉터리 서비스 팀 블로그](http://blogs.technet.com/b/askds/archive/2011/09/30/friday-mail-sack-super-slo-mo-edition.aspx)를 참조 하세요.  
      
  - \_Io 재분석태그중복제거\_,\_io 재분석\_태그\_SIS 또는io\_재분석 태그 HSM 재분석 태그를 사용 하는 파일을 복제 합니다.\_\_\_ 일반 파일로 재분석 지점은 로컬 시스템 에서만 작동 하므로 재분석 태그 및 재분석 데이터 버퍼는 다른 서버로 복제 되지 않습니다. 따라서 Windows Server 2012 또는 SIS (단일 인스턴스 저장소)에서 데이터 중복 제거를 사용 하는 볼륨의 폴더를 복제할 수 있지만, 데이터 중복 제거 정보는 역할 서비스를 사용 하도록 설정 된 각 서버에서 별도로 유지 관리 됩니다. DFS 복제  
      

### <a name="does-dfs-replication-replicate-timestamp-changes-if-no-other-changes-are-made-to-the-file"></a>파일에 대 한 다른 변경 내용이 없는 경우 타임 스탬프 변경을 복제할 DFS 복제 있습니까?

아니요, DFS 복제는 타임 스탬프에 대 한 변경 내용만 변경 되는 파일을 복제 하지 않습니다. 또한 변경 된 타임 스탬프는 다른 파일 변경 내용이 적용 되지 않는 한 복제 그룹의 다른 구성원에 복제 되지 않습니다.

### <a name="does-dfs-replication-replicate-updated-permissions-on-a-file-or-folder"></a>파일이 나 폴더에 대 한 업데이트 된 사용 권한을 DFS 복제 복제 합니까?

예. DFS 복제는 파일 및 폴더에 대 한 사용 권한 변경 내용을 복제 합니다. Access Control 목록 (ACL)과 연결 된 파일의 일부만 복제 되지만 DFS 복제는 여전히 전체 파일을 준비 영역으로 읽어야 합니다.


> [!NOTE]
> 많은 수의 파일에서 Acl을 변경 하면 복제 성능에 영향을 줄 수 있습니다. 그러나 RDC를 사용 하는 경우 전송 되는 데이터의 양은 전체 파일 크기가 아니라 Acl의 크기에 비례 합니다. 준비 폴더에서 파일을 읽어야 하므로 디스크 트래픽 양은 파일 크기에 비례 합니다. 
<br>


### <a name="does-dfs-replication-support-merging-text-files-in-the-event-of-a-conflict"></a>충돌이 발생 한 경우 텍스트 파일 병합을 지원 DFS 복제?

충돌이 발생 한 경우 DFS 복제는 파일을 병합 하지 않습니다. 그러나 충돌이 검색 된 컴퓨터의 hidden DfsrPrivate\\ConflictandDeleted 폴더에 있는 파일의 이전 버전을 유지 하려고 시도 합니다.

### <a name="does-dfs-replication-use-encryption-when-transmitting-data"></a>데이터를 전송할 때 암호화를 사용 DFS 복제?

예. DFS 복제는 암호화로 RPC (원격 프로시저 호출) 연결을 사용 합니다.

### <a name="is-it-possible-to-disable-the-use-of-encrypted-rpc"></a>암호화 된 RPC 사용을 사용 하지 않도록 설정할 수 있나요?

아니요. DFS 복제 서비스는 TCP를 통해 RPC (원격 프로시저 호출)를 사용 하 여 데이터를 복제 합니다. 인터넷을 통해 데이터 전송을 보호 하기 위해 DFS 복제 서비스는 항상 인증 수준 상수인를 `RPC_C_AUTHN_LEVEL_PKT_PRIVACY`사용 하도록 설계 되었습니다. 이렇게 하면 인터넷을 통한 RPC 통신이 항상 암호화 됩니다. 따라서 DFS 복제 서비스에서 암호화 된 RPC 사용을 사용 하지 않도록 설정할 수 없습니다.

자세한 내용은 다음 Microsoft 웹 사이트를 참조 하십시오.

  - [RPC 기술 참조](http://go.microsoft.com/fwlink/?linkid=182278)  
      
  - [원격 차등 압축 정보](http://go.microsoft.com/fwlink/?linkid=182279)  
      
  - [인증 수준 상수](http://go.microsoft.com/fwlink/?linkid=182280)  
      

### <a name="how-are-simultaneous-replications-handled"></a>동시 복제는 어떻게 처리 되나요?

복제 된 폴더당 하나의 업데이트 관리자가 있습니다. 업데이트 관리자는 서로 독립적으로 작동 합니다.

기본적으로 최대 16 개 (Windows Server 2003 R2) 동시 다운로드는 모든 연결 및 복제 그룹 간에 공유 됩니다. 연결 및 복제 그룹 업데이트는 serialize 되지 않으므로 업데이트를 수신 하는 특정 순서는 없습니다. 두 개의 일정이 열리면 업데이트는 일반적으로 두 연결에서 동시에 수신 및 설치 됩니다.

### <a name="how-do-i-force-replication-or-polling"></a>강제로 복제 또는 폴링을 어떻게 할까요??

[복제 일정 편집](https://technet.microsoft.com/library/Cc732278)에 설명 된 대로 DFS 관리를 사용 하 여 즉시 복제를 강제로 수행할 수 있습니다. Windows Server 2012 r 2에 도입 된 `Sync-DfsReplicationGroup` DFSR PowerShell 모듈 또는 **Dfsrdiag syncnow** 명령에 포함 된 cmdlet을 사용 하 여 강제로 복제할 수도 있습니다. `Update-DfsrConfigurationFromAD` Cmdlet 또는 **Dfsrdiag PollAD** 명령을 사용 하 여 강제 폴링을 수행할 수 있습니다.

### <a name="is-it-possible-to-configure-a-quiet-time-between-replications-for-files-that-change-frequently"></a>자주 변경 되는 파일에 대 한 복제 간에 자동 시간을 구성할 수 있나요?

아니요. 일정이 열려 있으면 DFS 복제에서 변경 내용을 통지 하는 대로 복제 합니다. 파일에 대 한 침묵 시간을 구성 하는 방법은 없습니다.

### <a name="is-it-possible-to-configure-one-way-replication-with-dfs-replication"></a>DFS 복제를 사용 하 여 단방향 복제를 구성할 수 있나요?

예. Windows Server 2012 또는 Windows Server 2008 r 2를 사용 하는 경우 단방향 연결을 통해 콘텐츠를 복제 하는 읽기 전용 복제 폴더를 만들 수 있습니다. 자세한 내용은 [특정 멤버에 대해 복제 된 폴더를 읽기](http://go.microsoft.com/fwlink/?linkid=156740) 전용으로 설정 (http://go.microsoft.com/fwlink/?LinkId=156740) 을 참조 하세요.

Windows Server 2008 또는 Windows Server 2003 r 2에서 DFS 복제를 사용 하 여 단방향 복제 연결을 만들 수 없습니다. 이렇게 하면 상태 검사 토폴로지 오류, 준비 문제 및 DFS 복제 데이터베이스 관련 문제를 비롯 한 다양 한 문제가 발생할 수 있습니다.

Windows Server 2008 또는 Windows Server 2003 r 2를 사용 하는 경우 다음 작업을 수행 하 여 단방향 연결을 시뮬레이션할 수 있습니다.

  - 관리자를 학습 하 여 기본 서버로 지정할 서버 에서만 변경을 수행 합니다. 그런 다음 변경 내용을 대상 서버에 복제 합니다.  
      
  - 최종 사용자에 게 쓰기 권한이 없도록 대상 서버에 대 한 공유 권한을 구성 합니다. 분기 서버에서 변경이 허용 되지 않는 경우에는 다시 복제 하 여 단방향 연결을 시뮬레이션 하 고 WAN 사용률을 낮게 유지할 수 없습니다.  
      

### <a name="is-there-a-way-to-force-a-complete-replication-of-all-files-including-unchanged-files"></a>변경 되지 않은 파일을 포함 하 여 모든 파일의 전체 복제를 강제로 수행 하는 방법이 있나요?

아니요. DFS 복제 파일을 동일한 것으로 간주 하는 경우 복제 하지 않습니다. 변경 된 파일이 복제 되지 않은 경우이를 수행 하도록 구성 된 경우 DFS 복제에서 자동으로 복제 합니다. 구성 된 일정을 덮어쓰려면 WMI 메서드 **ForceReplicate ()** 를 사용 합니다. 그러나이는 일정을 재정의 하는 것 이며 변경 되지 않았거나 동일한 파일을 강제로 복제 하지 않습니다.

### <a name="what-happens-if-the-primary-member-suffers-a-database-loss-during-initial-replication"></a>초기 복제 중에 주 구성원의 데이터베이스 손실이 발생 하면 어떻게 되나요?

초기 복제 중에는 받는 멤버가 주 멤버에 서로 다른 버전의 파일을 포함 하는 경우에 발생 하는 충돌 해결에 주 구성원의 파일이 항상 우선 적용 됩니다. 주 구성원 지정은 Active Directory Domain Services에 저장 되 고, 주 구성원은 복제할 준비가 된 후, 복제 그룹의 모든 구성원이 복제 되기 전에 지정이 지워집니다.

초기 복제에 실패 하거나 복제 중에 DFS 복제 서비스가 다시 시작 되 면 주 구성원은 로컬 DFS 복제 데이터베이스에서 주 구성원 지정을 확인 하 고 초기 복제를 다시 시도 합니다. Active Directory Domain Services에서 기본 지정을 지운 후에도 주 구성원의 DFS 복제 데이터베이스가 손실 되는 경우 복제 그룹의 모든 구성원이 초기 복제를 완료 하기 전에 복제 그룹의 모든 구성원이 실패 합니다. 주 구성원으로 지정 된 서버가 없기 때문에 폴더를 복제 합니다. 이 경우 주 멤버 서버에서 **Dfsradmin membership/set/isprimary: true** 명령을 사용 하 여 주 멤버 지정을 수동으로 복원 합니다.

초기 복제에 대 한 자세한 내용은 [복제 그룹 만들기](https://technet.microsoft.com/library/cc725893)를 참조 하세요.


> [!WARNING]
> 기본 멤버 지정은 초기 복제 프로세스 중에만 사용 됩니다. 복제가 완료 된 후 <STRONG>Dfsradmin</STRONG> 명령을 사용 하 여 복제 된 폴더의 주 구성원을 지정 하는 경우 DFS 복제은 Active Directory Domain Services에서 서버를 기본 멤버로 지정 하지 않습니다. 그러나 서버에 DFS 복제 데이터베이스의 손상이 나 데이터 손실이 발생할 경우 서버는 복제의 다른 구성원 으로부터 데이터를 복구 하는 대신 주 구성원으로 초기 복제를 수행 하려고 시도 합니다. 그룹. 기본적으로 서버는 rogue 주 서버가 되므로 충돌이 발생할 수 있습니다. 이러한 이유로 인해 초기 복제에 실패 한 것이 확실 한 경우에만 주 구성원을 수동으로 지정 회복할 수. 
<br>


### <a name="what-happens-if-the-replication-schedule-closes-while-a-file-is-being-replicated"></a>파일이 복제 되는 동안 복제 일정이 닫히면 어떻게 되나요?

연결에서 RDC (원격 차등 압축)를 사용 하도록 설정 하는 경우 일정 종료 (또는 **대역폭 없음**) 직전에 복제를 시작 하는 64 보다 큰 파일의 인바운드 복제는 일정을 열 때 (또는 **대역폭**을 제외 하 고 다른 항목에 대 한 변경 내용입니다. 복제가 중지 되었을 때의 상태에서 복제가 계속 됩니다.

RDC가 꺼져 있으면 DFS 복제에서 파일 전송을 완전히 다시 시작 합니다. 이는 수신 멤버에서 파일을 사용할 수 있을 때 지연 될 수 있습니다.

### <a name="what-happens-when-two-users-simultaneously-update-the-same-file-on-different-servers"></a>두 사용자가 서로 다른 서버에서 동일한 파일을 동시에 업데이트 하면 어떻게 되나요?

DFS 복제에서 충돌을 발견 하면 마지막으로 저장 된 파일 버전을 사용 합니다. 다른 파일을 DfsrPrivate\\ConflictandDeleted 폴더로 이동 합니다 (충돌을 해결 한 컴퓨터에서 복제 된 폴더의 로컬 경로 아래). 충돌 및 삭제 된 폴더 정리는 충돌 및 삭제 된 폴더 정리가 구성 된 크기를 초과 DFS 복제 하거나 디스크 공간이 부족 하 여 발생 하는 경우에 발생할 수 있습니다. 충돌 및 삭제 된 폴더는 복제 되지 않으므로이 충돌 해결 방법은 FRS에서 가능한 머프 디렉터리 문제를 방지 합니다.

충돌이 발생 하면 DFS 복제는 정보 이벤트를 DFS 복제 이벤트 로그에 기록 합니다. 이 이벤트에는 다음과 같은 이유로 사용자 작업이 필요 하지 않습니다.

  - 사용자에 게는 표시 되지 않습니다 (서버 관리자 에게만 표시 됨).  
      
  - DFS 복제은 충돌 및 삭제 된 폴더를 캐시로 처리 합니다. 할당량 임계값에 도달 하면 이러한 파일 중 일부를 정리 합니다. 충돌 하는 파일을 저장 하는 것은 보장 되지 않습니다.  
      
  - 충돌은 충돌 원본과 다른 서버에 있을 수 있습니다.  
      

## <a name="staging"></a>준비

### <a name="does-dfs-replication-continue-staging-files-when-replication-is-disabled-by-a-schedule-or-bandwidth-throttling-quota-or-when-a-connection-is-manually-disabled"></a>일정 또는 대역폭 제한 할당량으로 복제를 사용 하지 않도록 설정 하거나 수동으로 연결을 사용 하지 않도록 설정할 때 준비 파일을 계속 DFS 복제 합니까?

아니요. 대역폭 제한 할당량을 초과 하거나 연결을 사용 하지 않도록 설정 하는 경우 DFS 복제는 예약 된 복제 시간 외의 파일을 계속 준비 하지 않습니다.

### <a name="does-dfs-replication-prevent-other-applications-from-accessing-a-file-during-staging"></a>다른 응용 프로그램에서 준비 중에 파일에 액세스 하지 못하도록 DFS 복제 합니까?

아니요. DFS 복제는 사용자 또는 응용 프로그램이 복제 폴더에서 파일을 열 수 없도록 차단 하는 방식으로 파일을 엽니다. 이 메서드를 "oplocks 잠금" 이라고 합니다.

### <a name="is-it-possible-to-change-the-location-of-the-staging-folder-with-the-dfs-management-tool"></a>DFS 관리 도구를 사용 하 여 준비 폴더의 위치를 변경할 수 있나요?

예. 준비 폴더 위치는 복제 그룹의 각 구성원에 대 한 **속성** 대화 상자의 **고급** 탭에서 구성 됩니다.

### <a name="when-are-files-staged"></a>파일이 준비 된 시기

파일은 다음 표에 나와 있는 것 처럼 수신 멤버가 파일을 요청 하는 경우 (64 KB이 하) 해당 파일을 보내는 멤버에서 준비 됩니다. 연결에서 RDC (원격 차등 압축)를 사용 하지 않도록 설정 하는 경우 파일은 256 KB이 하를 제외 하 고 준비 됩니다. 파일이 64 KB 미만으로 전송 될 때 수신 구성원에도 준비 됩니다 .이 설정은 16kb와 1mb 사이에서 구성할 수 있습니다. 일정이 닫히면 파일이 준비 되지 않습니다.

### <a name="the-minimum-file-sizes-for-staging-files"></a>준비 파일의 최소 파일 크기

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
<td><p>보내기 멤버</p></td>
<td><p>64KB</p></td>
<td><p>256 KB</p></td>
</tr>
<tr class="odd">
<td><p>수신 구성원</p></td>
<td><p>기본적으로 64 KB</p></td>
<td><p>기본적으로 64 KB</p></td>
</tr>
</tbody>
</table>

### <a name="what-happens-if-a-file-is-changed-after-it-is-staged-but-before-it-is-completely-transmitted-to-the-remote-site"></a>파일이 준비 된 후 원격 사이트로 완전히 전송 되기 전에 파일이 변경 되 면 어떻게 되나요?

파일의 일부를 이미 전송 중인 경우 DFS 복제는 전송을 계속 합니다. DFS 복제 파일 전송을 시작 하기 전에 파일이 변경 되 면 파일의 최신 버전이 전송 됩니다.

## <a name="change-history"></a>변경 내역


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Date</th>
<th>설명</th>
<th>Reason</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>2018년 11월 15일</p></td>
<td><p>Windows Server 2019에 대해 업데이트 되었습니다.</p></td>
<td><p>새 운영 체제</p></td>
</tr>
<tr class="even">
<td><p>2013년 10월 9일</p></td>
<td><p>DFS 복제 지원 되는 한도는 업데이트 되었습니까? Windows Server 2012 r 2에 대 한 테스트 결과를 포함 하는 섹션입니다.</p></td>
<td><p>최신 버전의 Windows Server에 대 한 업데이트</p></td>
</tr>
<tr class="odd">
<td><p>2013 년 1 월 30 일</p></td>
<td><p>일정 또는 대역폭 제한 할당량으로 복제를 사용 하지 않도록 설정 하는 경우 또는 연결을 수동으로 사용 하지 않도록 설정한 경우에는 DFS 복제 준비 파일 계속 준비를 추가 했습니다. 엔트리의.</p></td>
<td><p>고객 질문</p></td>
</tr>
<tr class="even">
<td><p>10 월 31 일, 2012</p></td>
<td><p>DFS 복제에 대해 지원 되는 제한은 무엇 인가요? 항목을 입력 하 여 볼륨의 테스트 된 복제 파일 수를 늘립니다.</p></td>
<td><p>고객 의견</p></td>
</tr>
<tr class="odd">
<td><p>2012 년 8 월 15 일</p></td>
<td><p>편집 된 DFS 복제 NTFS 파일 사용 권한, 대체 데이터 스트림, 하드 링크 및 재분석 지점은 복제할 필요가 있나요? 항목을 통해 DFS 복제 하드 링크 및 재분석 위치를 처리 하는 방법을 보다 명확 하 게 설명할 수 있습니다.</p></td>
<td><p>고객 지원 서비스의 피드백</p></td>
</tr>
<tr class="even">
<td><p>June 13, 2012</p></td>
<td><p>편집 된 DFS 복제 ReFS 또는 FAT 볼륨에서 작동 하나요? ReFS에 대 한 설명을 추가할 항목입니다.</p></td>
<td><p>고객 의견</p></td>
</tr>
<tr class="odd">
<td><p>4 월 25 일, 2012</p></td>
<td><p>편집 된 DFS 복제 NTFS 파일 사용 권한, 대체 데이터 스트림, 하드 링크 및 재분석 지점은 복제할 필요가 있나요? DFS 복제 하드 링크를 처리 하는 방법을 설명 하는 항목입니다.</p></td>
<td><p>잠재적 혼동 줄이기</p></td>
</tr>
<tr class="even">
<td><p>2011 년 3 월 30 일</p></td>
<td><p>편집 됨 DFS 복제 Outlook .pst 또는 Microsoft Office Access 데이터베이스 파일을 복제할 수 있나요? 항목을 사용 하 여 .pst 및 Access 파일에 DFS 복제를 사용 하는 경우 발생 하는 잠재적인 영향을 해결 합니다.</p>
<p>복제 성능을 향상 시킬 수 있는 방법이 추가 되었습니까?</p></td>
<td><p>이전 항목에 대 한 고객 질문입니다 .이는 .pst 또는 Access 파일을 복제 하면 DFS 복제 데이터베이스가 손상 될 수 있음을 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p>2011 년 1 월 26 일</p></td>
<td><p>ConflictAndDeleted 또는 기존 폴더에서 파일을 복구 하는 방법을 추가 했습니까?</p></td>
<td><p>고객 의견</p></td>
</tr>
<tr class="even">
<td><p>10 월 20 일, 2010</p></td>
<td><p>DFS 복제 멤버를 어떻게 업그레이드 하거나 바꿀 수 있나요?</p></td>
<td><p>고객 의견</p></td>
</tr>
</tbody>
</table>

