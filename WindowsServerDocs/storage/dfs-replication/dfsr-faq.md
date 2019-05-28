---
Title: 'DFS 복제: FAQ(질문과 대답)'
ms.date: 06/18/2014
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 3782667e54f5e6b52c07645704b95fc9e7409a27
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476067"
---
# <a name="dfs-replication-frequently-asked-questions-faq"></a>DFS 복제: FAQ(질문과 대답)


업데이트됨: 2019 년 4 월 30 일

적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

이 FAQ는 Windows Server에 대 한 분산 파일 시스템 (DFS) 복제 (Dfs-r 또는 DFSR 라고도 함)에 대 한 질문을 답변합니다.

DFS 네임 스페이스에 대 한 자세한 내용은 [DFS 네임 스페이스: 질문과 대답](https://technet.microsoft.com/en-us/library/ee404780)합니다.

DFS 복제의 새로운에 대 한 내용은 다음 항목을 참조 합니다.

  - [DFS 네임 스페이스 및 DFS 복제 개요](http://technet.microsoft.com/en-us/library/jj127250) (Windows Server 2012)에서  
      
  - [분산 파일 시스템의 새로운 기능](https://technet.microsoft.com/en-us/library/ee307957) 항목에서 [Windows Server 2008에서 Windows Server 2008 R2로의 기능 변경](https://technet.microsoft.com/en-us/library/dd391932)  
      
  - [분산 파일 시스템](https://technet.microsoft.com/en-us/library/cc753479) 항목에서 [Windows Server 2003 sp1에서 Windows Server 2008로의 기능 변경](https://technet.microsoft.com/en-us/library/cc753208)  
      

이 항목에 대한 최근 변경 내용 목록은 이 항목의 [변경 내용](#change-history) 섹션을 참조하세요.

      

## <a name="interoperability"></a>상호 운용성

### <a name="can-dfs-replication-communicate-with-frs"></a>DFS 복제 FRS를 사용 하 여 통신할 수 있나요?

아니요. DFS 복제에 사용 하 여 복제 서비스 FRS (파일) 통신 하지 않습니다. DFS 복제 및 FRS 동일한 서버에 동시에 실행할 수 있지만 데이터가 손실이 발생할 수 있으므로 동일한 폴더나 하위 폴더를 복제 하도록 구성할 수 없습니다 해야 합니다.

### <a name="can-dfs-replication-replace-frs-for-sysvol-replication"></a>DFS 복제 SYSVOL 복제에 대 한 FRS를 바꿀 수 있습니까

예, DFS 복제 SYSVOL 복제에서 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008을 실행 하는 서버에 대 한 FRS를 바꿀 수 있습니다. Windows Server 2003 R2를 실행 하는 서버에서 DFS 복제 SYSVOL 폴더를 사용 하 여 지원 하지 않습니다.

DFS 복제를 사용 하 여 SYSVOL을 복제 하는 방법에 대 한 자세한 내용은 참조는 [SYSVOL 복제 마이그레이션 가이드: FRS에서 DFS 복제로](https://technet.microsoft.com/en-us/library/dd640019)합니다.

### <a name="can-i-upgrade-from-frs-to-dfs-replication-without-losing-configuration-settings"></a>로 업그레이드할 수 FRS에서 DFS 복제 구성 파일을 손실 하지 않고?

예 복제를 FRS에서 DFS 복제로 마이그레이션하려면 다음 문서를 참조 합니다.

  - SYSVOL 폴더 이외의 폴더의 복제를 마이그레이션하려면 [DFS Operations Guide: FRS에서 DFS 복제로 마이그레이션](http://go.microsoft.com/fwlink/?linkid=192776) 하 고 [FRS2DFSR – DFSR 마이그레이션 유틸리티에 FRS](http://go.microsoft.com/fwlink/?linkid=195437) (http://go.microsoft.com/fwlink/?LinkID=195437)합니다.  
      
  - DFS 복제 SYSVOL 폴더의 복제를 마이그레이션하려면, [SYSVOL 복제 마이그레이션 가이드: FRS에서 DFS 복제로](https://technet.microsoft.com/en-us/library/dd640019)합니다.  
      

### <a name="can-i-use-dfs-replication-in-a-mixed-windowsunix-environment"></a>혼합된 된 Windows/UNIX 환경에서 DFS 복제를 사용할 수 있나요?

예 DFS 복제만 지원 하지만 Windows Server를 실행 하는 서버 간에 콘텐츠를 복제, UNIX 클라이언트는 Windows 서버에서 파일 공유를 액세스할 수 있습니다. 이렇게 하려면 DFS 복제 서버에서 네트워크 파일 시스템 (NFS)에 대 한 서비스를 설치 합니다.

이 기능은 제한 된 경우가 또는 Windows 환경 (예: SMB 서명을 사용 하 여 비활성화를 수정 해야 하지만 Windows 파일 공유를 직접 액세스할 수 있도록 많은 UNIX 클라이언트에 포함 된 SMB/CIFS 클라이언트 기능을 사용할 수도 있습니다. 그룹 정책)입니다.

Windows Server 운영 체제를 실행 하는 서버에서 DFS 복제 NFS와 상호 운용 되 있지만 NFS 탑재 지점의 복제할 수 없습니다.

### <a name="can-i-use-the-volume-shadow-copy-service-with-dfs-replication"></a>DFS 복제를 사용 하 여 볼륨 섀도 복사본 서비스를 사용할 수 있습니까?

예 볼륨 섀도 복사본 서비스 (VSS) 볼륨에서 DFS 복제는 지원 및 이전 버전 클라이언트를 사용 하 여 이전 스냅숏을 성공적으로 복원할 수 있습니다.

### <a name="can-i-use-windowsbackup-ntbackupexe-to-remotely-back-up-a-replicated-folder"></a>원격으로 복제 된 폴더를 백업 하려면 Windows 백업 (Ntbackup.exe)를 사용할 수 있나요?

아니요, Windows Server 2003을 실행 하는 컴퓨터에서 또는 Windows Server 2012를 실행 하는 컴퓨터의 복제 된 폴더의 콘텐츠를 백업 하는 이전 버전에서 Windows 백업 (Ntbackup.exe)를 사용 하 여, Windows Server 2008 R2 또는 Windows Server 2008 지원 되지 않습니다.

복제 된 폴더에 저장 된 파일을 백업 하려면 Windows Server Backup 또는 Microsoft® System Center Data Protection Manager를 사용 합니다. Windows Server 2008 R2 및 Windows Server 2008의 백업 및 복구 기능에 대 한 자세한 내용은 [백업 및 복구](https://technet.microsoft.com/en-us/library/Cc754097)합니다. 자세한 내용은 [System Center Data Protection Manager](http://go.microsoft.com/fwlink/?linkid=182261) (http://go.microsoft.com/fwlink/?LinkId=182261)합니다.

### <a name="do-file-system-policies-impact-dfs-replication"></a>파일 시스템 정책을 DFS 복제에 영향을 않습니다?

예 복제 된 폴더에 파일 시스템 정책을 구성 하지 마세요. 파일 시스템 정책에는 그룹 정책 새로 고침 간격 마다 NTFS 사용 권한을 다시 적용합니다. 이 파일을 닫을 때까지 열린 파일 복제 하지 않기 때문에 공유 위반 될 수 있습니다.

### <a name="does-dfs-replication-replicate-mailboxes-hosted-on-microsoft-exchange-server"></a>DFS 복제는 Microsoft Exchange Server에 호스트 된 사서함을 복제할?

아니요. Microsoft Exchange Server에 호스트 된 사서함을 복제 하려면 DFS 복제를 사용할 수 없습니다.

### <a name="does-dfs-replication-support-file-screens-created-by-file-server-resource-manager"></a>파일 서버 리소스 관리자에서 만든 파일 차단을 DFS 복제를 지원 하나요?

예 그러나 파일 서버 리소스 관리자 (FSRM) 파일 설정을 차단 복제의 양쪽 끝에서 일치 해야 합니다. 또한 DFS 복제에 파일 및 폴더 복제에서 특정 파일 및 파일 형식을 제외 하는 데 사용할 수 있는 자체 필터 메커니즘이 있습니다.

다음은 파일 화면 또는 할당량을 구현 하기 위한 모범 사례입니다.

  - 숨겨진된 DfsrPrivate 폴더 할당량 또는 파일 차단 될 수 없습니다.  
      
  - 차단을 사용 하기 전에 모든 복제 된 폴더에는 스크린 된 파일이 존재 하지 해야 합니다.  
      
  - 할당량은 사용 하기 전에 없습니다 폴더 할당량을 초과할 수 있습니다.  
      
  - 하드 할당량을 사용 하 여 주의 해야 합니다. 복제 하기 전에 할당량 내로 유지 되지만 파일 복제 되는 경우이 초과 하는 복제 그룹의 개별 멤버에 대 한 것 같습니다. 예를 들어, 사용자 (다음에 있는 하드 한도) 서버는 10 개의 mb (메가바이트) 파일을 복사 하 고 다음 복제 발생 하면 다른 사용자 B 서버로 5MB 파일을 복사 하는 경우 두 서버는 5mb 하 여 할당량을 초과할 것입니다. 이 인해 DFS 복제가 계속 복제 버전 벡터와 잠재적인 성능 문제에 결함이 발생 하 여 파일을 다시 시도 수 있습니다.  
      

### <a name="is-dfs-replication-cluster-aware"></a>DFS 복제 클러스터 인식 기능

예, DFS 복제 Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 R2의 장애 조치 클러스터를 복제 그룹의 구성원으로 추가 하는 기능을 포함 합니다. 자세한 내용은 [복제 그룹에 장애 조치 클러스터를 추가](http://go.microsoft.com/fwlink/?linkid=155085) (http://go.microsoft.com/fwlink/?LinkId=155085)합니다. Windows Server 2008 R2 이전 Windows 버전에서 DFS 복제 서비스를 장애 조치 클러스터와 조정 하기 위해 디자인 되지 않았으며 서비스는 다른 노드로 장애 조치 되지 않습니다.


> [!NOTE]
> DFS 복제는 클러스터 공유 볼륨에 복제 파일을 지원 하지 않습니다. 
<br>


### <a name="is-dfs-replication-compatible-with-data-deduplication"></a>DFS 복제는 데이터 중복 제거를 사용 하 여 호환 되나요?

예, DFS 복제는 Windows Server에서 데이터 중복 제거를 사용 하는 볼륨에 폴더를 복제할 수 있습니다.

### <a name="is-dfs-replication-compatible-with-ris-and-wds"></a>DFS 복제는 RIS, WDS를 사용 하 여 호환 되나요?

예 DFS 복제는 단일 인스턴스 저장소 (SIS)를 사용 하는 볼륨을 복제 합니다. SIS는 원격 설치 서비스 (RIS), Windows 배포 서비스 (WDS) 및 Windows Storage Server에서 사용 됩니다.

### <a name="is-it-possible-to-use-dfs-replication-with-offline-files"></a>오프 라인 파일을 사용 하 여 DFS 복제를 사용할 수는?

안전 하 게 사용할 수 DFS 복제 및 오프 라인 파일 함께 시나리오에서 파일에 기록 하는 한 번에 한 명의 사용자만 있으면 됩니다. 이 두 지점 간의 여행 있으며 하거나 두 분기에서 파일에 액세스할 수 있으려면 사용자에 게 유용 오프 라인입니다. 오프 라인 사용에 대 한 로컬 파일을 캐시 하는 오프 라인 파일 및 DFS 복제는 각 지사 간에 데이터를 복제 합니다.

사용 하지 마십시오 DFS 복제 오프 라인 파일을 사용 하 여 다중 사용자 환경에서 DFS 복제에서 파일 체크 아웃 기능이 나 분산된 잠금 메커니즘을 제공 하지 않으므로. DFS 복제는 DfsrPrivate 이전 파일 이동 두 명의 사용자가 서로 다른 서버에 동시에 동일한 파일을 수정 하는 경우\\다음 복제 시 ConflictandDeleted 폴더 (복제 된 폴더의 로컬 경로 아래에 있음).

### <a name="what-antivirus-applications-are-compatible-with-dfs-replication"></a>바이러스 백신 응용 프로그램 DFS 복제와 호환 됩니까?

복제 된 폴더에서 파일을 변경 하는 해당 검색 작업 하는 경우 바이러스 백신 응용 프로그램에서 과도 하 게 복제를 발생할 수 있습니다. 자세한 내용은 [테스트 바이러스 백신 응용 프로그램의 상호 운용성 DFS 복제](http://go.microsoft.com/fwlink/?linkid=73990) (http://go.microsoft.com/fwlink/?LinkId=73990)합니다.

### <a name="what-are-the-benefits-of-using-dfs-replication-instead-of-windows-sharepoint-services"></a>DFS 복제를 사용 하 여 Windows SharePoint Services 대신의 이점은 무엇 인가요?

Windows® SharePoint® Services DFS 복제 하지 않는 파일 체크 아웃 기능의 형태로 긴밀 하 게 일관성을 제공 합니다. 동일한 파일을 편집 하는 여러 사람들에 대 한 염려 하는 경우에 Windows SharePoint Services를 사용 하는 것이 좋습니다. Windows SharePoint Services 2.0 서비스 팩 2를 사용 하 여이 제품은 Windows Server 2003 R2의 일환으로 합니다. Windows SharePoint Services는 Microsoft 웹 사이트에서 다운로드할 수 있습니다. 최신 버전의 Windows Server는 포함 되지 않습니다. 그러나 여러 사이트에 걸쳐 데이터를 복제 하는 경우 사용자가 동시에 동일한 파일을 편집 하지 DFS 복제는 큰 대역폭 및 간편해 진 관리를 제공 합니다.

## <a name="limitations-and-requirements"></a>제한 사항 및 요구 사항

### <a name="can-dfs-replication-replicate-between-branch-offices-without-a-vpn-connection"></a>DFS 복제 VPN 연결 없이 지사 간에 복제할 수 있습니까?

예-지점 연결 개인 와이드 WAN (광역 네트워크) 링크 (인터넷이 아닌) 것을 가정 하 고 있습니다. 그러나 외부 방화벽에 적절 한 포트를 열어야 합니다. DFS 복제는 RPC 끝점 매퍼 (포트 135) 및 1024 이상 임의로 할당 된 사용 후 삭제 포트를 사용합니다. 사용할 수는 **Dfsrdiag** 명령줄 도구 사용 후 삭제 포트 대신 고정 포트를 지정 합니다. RPC 끝점 매퍼를 지정 하는 방법에 대 한 자세한 내용은 참조 하세요. [154596 문서](http://go.microsoft.com/fwlink/?linkid=73991) Microsoft 기술 자료 (http://go.microsoft.com/fwlink/?LinkId=73991)합니다.

### <a name="can-dfs-replication-replicate-files-encrypted-with-the-encrypting-file-system"></a>DFS 복제 파일 시스템 암호화를 사용 하 여 암호화 된 파일을 복제할 수 있습니까?

아니요. DFS 복제는 파일 또는 파일 시스템 EFS (암호화)를 사용 하 여 암호화 된 폴더를 복제 하지 않습니다. 사용자가 이전에 복제 하는 파일을 암호화 하는 경우 DFS 복제는 복제 그룹의 다른 모든 멤버에서 파일을 삭제 합니다. 이렇게 하면 파일 복사본에만 사용할 수는 서버에서 암호화 된 버전입니다.

### <a name="can-dfs-replication-replicate-outlook-pst-or-microsoft-office-access-database-files"></a>Outlook.pst 또는 Microsoft Office Access 데이터베이스 파일에 DFS 복제 복제할 수 있습니까?

DFS 복제 안전 하 게 복제할 수 Microsoft Outlook 개인 폴더 파일 (.pst) 및 Microsoft Access 파일 보관을 위해 저장 되 고 (.pst 열거나 액세스를 Outlook 또는 액세스와 같은 클라이언트를 사용 하 여 네트워크를 통해 액세스 하지 않는 경우에 파일을 먼저 파일을 복사 합니다는 로컬 저장소 장치). 그 이유는 다음과 같습니다.

  - 네트워크 연결을 통해.pst 파일을 열고.pst 파일의 데이터가 손상 될 수 있습니다. 이유.pst 파일 안전 하 게에서 액세스할 수 없는 네트워크에 대 한 자세한 내용은 참조 하세요. [297019 문서](http://go.microsoft.com/fwlink/?linkid=125363) Microsoft 기술 자료 (http://go.microsoft.com/fwlink/?LinkId=125363)합니다.  
      
  - .pst 파일에 액세스 하 고 Outlook 이나 Office Access와 같은 클라이언트에서 액세스 하는 동안 장시간 동안 열린 채로 유지 하는 경향이 있습니다. 이 종료 시까지 이러한 파일을 복제에서 DFS 복제를 방지 합니다.  
      

### <a name="can-i-use-dfs-replication-in-a-workgroup"></a>작업 그룹에서 DFS 복제를 사용할 수 있나요?

아니요. DFS 복제 구성에 대 한 Active Directory® Domain Services에 의존 합니다. 도메인에만 작동 합니다.

### <a name="can-more-than-one-folder-be-replicated-on-a-single-server"></a>단일 서버에 둘 이상의 폴더 복제할 수 있습니까?

예 DFS 복제 서버 간에 다양 한 폴더를 복제할 수 있습니다. 각 복제 된 폴더에는 고유한 확인 루트 경로 이러한 겹치지 않도록 합니다. 예를 들어, d:\\판매 및 d:\\계정에는 두 개의 복제 된 폴더만 아니라 d:에 대 한 루트 경로 수\\판매 및 d:\\Sales\\보고서에는 두 개의 복제 된 폴더에 대 한 루트 경로 여야 합니다.

### <a name="does-dfs-replication-require-dfs-namespaces"></a>DFS 복제 DFS 네임 스페이스를 필요 합니까?

아니요. DFS 복제 및 DFS 네임 스페이스는 개별적으로 또는 함께 사용할 수 있습니다. 또한는 FRS.를 사용 하 여 수 없었습니다. 독립 실행형 DFS 네임 스페이스를 복제 하려면 DFS 복제를 사용할 수 있습니다.

### <a name="does-dfs-replication-require-time-synchronization-between-servers"></a>DFS 복제 서버 간의 시간 동기화 필요 합니까?

아니요. DFS 복제 서버 간의 시간 동기화를 명시적으로 필요 하지 않습니다. 그러나 DFS 복제는 서버 클럭을 밀접 하 게 일치 하는지 필요 합니다. 서버 클럭은 Kerberos 인증이 제대로 작동 하려면 기본적으로 서로 5 분 내에서 설정 되어야 합니다. 예를 들어 DFS 복제는 파일이 충돌 시 우선 순위를 확인 하려면 타임 스탬프를 사용 합니다. 정확한 시간에 가비지 컬렉션, 일정 및 기타 기능에 대 한 중요 한도.

### <a name="does-dfs-replication-support-replicating-an-entire-volume"></a>DFS 복제는 전체 볼륨을 복제를 지원 하나요?

예 그러나 Windows Server 2003 서비스 팩 2 나 핫픽스 먼저 설치 해야 있습니다. 자세한 내용은 [920335 문서](http://go.microsoft.com/fwlink/?linkid=76776) Microsoft 기술 자료 (http://go.microsoft.com/fwlink/?LinkId=76776)합니다. 또한 전체 볼륨을 복제 하면 다음과 같은 문제가 발생할 수 있습니다.

  - 볼륨을 Windows 페이징 파일에 있으면 복제는 실패 하 고 DFSR 이벤트 4312 시스템 이벤트 로그에 기록 합니다.  
      
  - DFS 복제는 대상 서버에서 복제 된 폴더에 시스템과 Hidden 특성을 설정합니다. Windows 볼륨 루트 폴더에 기본적으로 시스템 및 Hidden 특성을 적용 하기 때문에 발생 합니다. 으로 경우에 대상 서버에서 복제 된 폴더의 로컬 경로 볼륨 루트 폴더 특성에 더 이상 변경 내용이 있습니다.  
      
  - Windows 시스템 폴더에 포함 된 볼륨을 복제할 때 DFS 복제는 % WINDIR % 폴더를 인식 하 고 복제 하지 않습니다. 그러나 DFS 복제는 응용 프로그램에는 DFS 복제를 사용 하 여 상호 운용성 문제가 있는 경우 실패 하는 응용 프로그램 대상 서버에서 발생할 수 있습니다는 타사 응용 프로그램을 사용 하는 폴더를 복제지 않습니다.  
      

### <a name="does-dfs-replication-support-rpc-over-http"></a>DFS 복제 HTTP를 통한 RPC를 지원 하나요?

아니요.

### <a name="does-dfs-replication-work-across-wireless-networks"></a>DFS 복제 무선 네트워크를 통해 작동 하나요?

예 DFS 복제는 연결 형식과 독립적입니다.

### <a name="does-dfs-replication-work-on-refs-or-fat-volumes"></a>DFS 복제 ReFS 또는 FAT 볼륨에서 작동 합니까?

아니요. DFS 복제 되지 않습니다 NTFS 파일 시스템으로 포맷 된 볼륨만 지원 ReFS (복원 파일 시스템) 및 FAT 파일 시스템 지원 되지 않습니다. DFS 복제에서 NTFS 변경 저널을 사용 하 여 서 다른 기능의 NTFS 파일 시스템 NTFS 필요 합니다.

### <a name="does-dfs-replication-work-with-sparse-files"></a>스파스 파일을 사용 하 여 DFS 복제가 작동 합니까?

예 스파스 파일을 복제할 수 있습니다. 합니다 **Sparse** 받는 구성원의 특성이 유지 됩니다.

### <a name="do-i-need-to-log-in-as-administrator-to-replicate-files"></a>파일을 복제 하려면 관리자 권한으로 로그인 해야 합니까?

아니요. DFS 복제는 복제 하려면 관리자 권한으로 로그인 해야 하므로 로컬 시스템 계정으로 실행 되는 서비스입니다. 그러나 DFS 복제 구성을 변경 하려면 도메인 관리자 또는 영향을 받는 파일 서버의 로컬 관리자 여야 합니다.

"자세한 내용은 DFS 복제 보안 요구 사항 및" 참조 위임에는 [DFS 복제를 관리 하는 기능을 위임](http://go.microsoft.com/fwlink/?linkid=182294) (http://go.microsoft.com/fwlink/?LinkId=182294)합니다.

### <a name="how-can-i-upgrade-or-replace-a-dfs-replication-member"></a>업그레이드 하거나 DFS 복제 구성원을 바꿀 수 있습니다 어떻게 하나요?

업그레이드 또는 DFS 복제 멤버이 블로그 Ask에서 디렉터리 서비스 팀 블로그 게시물을 참조 하세요. [DFSR 구성원 하드웨어 또는 OS 교체](http://blogs.technet.com/b/askds/archive/2010/09/10/series-wrap-up-and-downloads-replacing-dfsr-member-hardware-or-os.aspx)합니다.

### <a name="is-dfs-replication-suitable-for-replicating-roaming-profiles"></a>DFS 복제는 로밍 프로필을 복제 하기 위한 적합 한가?

예 로밍 사용자 프로필을 복제 하는 경우 특정 시나리오가 지원 됩니다. 지원 되는 시나리오에 대 한 정보를 참조 하세요 [Microsoft의 지원 문에 관련 복제 된 사용자 프로필 데이터](http://go.microsoft.com/fwlink/?linkid=201282) (http://go.microsoft.com/fwlink/?LinkId=201282)합니다.

### <a name="is-there-a-file-character-limit-or-limit-to-the-folder-depth"></a>파일 문자 제한 또는 폴더 크기에 제한이 있나요?

Windows 및 DFS 복제는 최대 32 천 문자를 사용 하 여 폴더 경로 지원합니다. DFS 복제 폴더 경로가 260 자 제한 됩니다.

### <a name="must-members-of-a-replication-group-reside-in-the-same-domain"></a>복제 그룹의 구성원이 동일한 도메인에 있어야 하나요?

아니요. 복제 그룹에는 단일 포리스트 안에서 도메인 간 하지만 서로 다른 여러 포리스트의 전체가 아닌 걸쳐 있을 수 있습니다.

### <a name="what-are-the-supported-limits-of-dfs-replication"></a>DFS 복제의 지원 되는 제한은 무엇 인가요?

다음 목록에는 일련을의 Microsoft Windows Server 2012 r2에서 입증 된 확장성 지침을 제공 합니다.

  - 서버에서 모든 복제 된 파일의 크기: 100tb입니다.  
      
  - 볼륨에 복제 된 파일 수: 70 백만 합니다.  
      
  - 최대 파일 크기: 250 기가바이트입니다.  
      


> [!IMPORTANT]
> 많은 수 또는 파일의 크기를 사용 하 여 복제 그룹을 만들 때 데이터베이스 복제를 내보내고 미리 시드 기술을 사용 하 여 초기 복제의 기간을 최소화 하는 것이 좋습니다. 자세한 내용은 참조 하세요. <A href="http://blogs.technet.com/b/filecab/archive/2013/08/21/dfs-replication-initial-sync-in-windows-server-2012-r2-attack-of-the-clones.aspx">DFS 복제 Windows Server 2012 R2에서 초기 동기화 합니다. 클론의 습격</A>합니다. 
<br>


다음 목록에는 일련을의 Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008에는 Microsoft에서 입증 된 확장성 지침을 제공 합니다.

  - 서버에서 모든 복제 된 파일의 크기: 10 테라바이트 합니다.  
      
  - 볼륨에 복제 된 파일 수: 11 백만 합니다.  
      
  - 최대 파일 크기: 64gb입니다.  
      


> [!NOTE]
> 복제 그룹, 복제 된 폴더, 연결 또는 복제 그룹 구성원의 수에 제한이 더 이상 됩니다. 
<br>


Microsoft Windows Server 2003 R2 용으로 입증 된 확장성 지침의 목록을 참조 하세요 [DFS 복제 확장성 지침](http://go.microsoft.com/fwlink/?linkid=75043) (http://go.microsoft.com/fwlink/?LinkId=75043)합니다.

### <a name="when-should-i-not-use-dfs-replication"></a>하지 DFS 복제를 사용 해야는 경우

여러 사용자를 업데이트 하거나 다른 서버에서 동시에 동일한 파일을 수정 위치 환경에서 DFS 복제를 사용 하지 마세요. 이렇게 하면 DFS 복제 충돌 하는 파일의 복사본을 숨겨진된 DfsrPrivate 이동할\\ConflictandDeleted 폴더입니다.

여러 사용자를 서로 다른 서버에 동시에 동일한 파일을 수정 해야 하는 경우 Windows SharePoint Services의 파일 체크 아웃 기능을 사용 하 여 사용자 한 명만 파일에서 작동 되도록 합니다. Windows SharePoint Services 2.0 서비스 팩 2를 사용 하 여이 제품은 Windows Server 2003 R2의 일환으로 합니다. Windows SharePoint Services는 Microsoft 웹 사이트에서 다운로드할 수 있습니다. 최신 버전의 Windows Server는 포함 되지 않습니다.

### <a name="why-is-a-schema-update-required-for-dfs-replication"></a>DFS 복제에 필요한 스키마 업데이트를 이유는 무엇입니까?

DFS 복제 Active Directory Domain Services 도메인 명명 컨텍스트에서 새 개체를 사용 하 여 구성 정보를 저장 합니다. 이러한 개체는 Active Directory Domain Services 스키마를 업데이트할 때 생성 됩니다. 자세한 내용은 [DFS 복제에 대 한 요구 사항 검토](http://go.microsoft.com/fwlink/?linkid=182264) (http://go.microsoft.com/fwlink/?LinkId=182264)합니다.

## <a name="monitoring-and-management-tools"></a>모니터링 및 관리 도구

### <a name="can-i-automate-the-health-report-to-receive-warnings"></a>경고를 받으려면 상태 보고서를 자동화할 수 있나요?

예 상태 보고서를 자동화 하는 방법은 세 가지가 있습니다.

  - 정기적으로 상태 보고서를 생성 하려면 예약 된 작업과 함께에서 Windows Server 2012 R2 또는 DfsrAdmin.exe에 포함 된 DFSR Windows PowerShell 모듈을 사용 합니다. 자세한 내용은 [DFS 복제 상태 보고서를 자동화](http://go.microsoft.com/fwlink/?linkid=74010) (http://go.microsoft.com/fwlink/?LinkId=74010)합니다.  
      
  - 지정 된 조건을 기반으로 하는 경고를 만들려면 System Center Operations Manager에 대 한 DFS 복제 관리 팩을 사용 합니다.  
      
  - 경고를 스크립팅하려면 DFS 복제 WMI 공급자를 사용 합니다.  
      

### <a name="can-i-use-microsoft-system-center-operations-manager-to-monitor-dfs-replication"></a>DFS 복제를 모니터링 하려면 Microsoft System Center Operations Manager를 사용할 수 있나요?

예 자세한 내용은 참조는 [System Center Operations Manager 2007에 대 한 DFS 복제 관리 팩](http://go.microsoft.com/fwlink/?linkid=182265) Microsoft 다운로드 센터에서 (http://go.microsoft.com/fwlink/?LinkId=182265)합니다.

### <a name="does-dfs-replication-support-remote-management"></a>DFS 복제 원격 관리를 지원 하나요?

예 DFS 복제에서 DFS 관리 콘솔을 사용 하 여 원격 관리를 지원 하며 **복제 그룹 추가** 명령입니다. 예를 들어 서버 A에서 포리스트의 구성원으로 서버 A와 B를 사용 하 여 정의 된 복제 그룹에 연결할 수 있습니다.

DFS 관리는 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 및 Windows Server 2003 R2에 포함 합니다. 다른 버전의 Windows에서 DFS 복제를 관리 하려면 원격 데스크톱을 사용 하 여 또는 [원격 서버 관리 도구에 대 한 Windows 7](https://technet.microsoft.com/en-us/library/Ee449475)합니다.


> [!IMPORTANT]
> 을 확인 하거나 읽기 전용 복제 폴더 또는 장애 조치 클러스터는 멤버를 포함 하는 복제 그룹을 관리 하려면 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, 합니다 에포함되어있는DFS관리버전을사용해야<a href="http://go.microsoft.com/fwlink/p/?linkid=238560">Windows 8 용 원격 서버 관리 도구</a>, 또는 <a href="https://technet.microsoft.com/en-us/library/ee449475">Windows 7 용 원격 서버 관리 도구</a>합니다. 
<br>


### <a name="do-ultrasound-and-sonar-work-with-dfs-replication"></a>Ultrasound 및 Sonar 작동 하나요 DFS 복제를 사용 하 여?

아니요. DFS 복제에 자체 모니터링 및 진단 도구 집합이 있습니다. Ultrasound 및 Sonar FRS. 모니터링 수만 있습니다.

### <a name="how-can-files-be-recovered-from-the-conflictanddeleted-or-preexisting-folders"></a>ConflictAndDeleted 또는 PreExisting 폴더에서 파일을 어떻게 복구할 수 있습니다?

손실 된 파일 복구, 파일 시스템 폴더 또는 파일 히스토리를 사용 하 여 공유 폴더에서 파일을 복원 합니다 **이전 버전 복원** 파일 탐색기 또는 파일 백업에서 복원 하 여 명령입니다. ConflictAndDeleted 또는 PreExisting 폴더에서 직접 파일을 복구 하려면 사용 합니다 `Get-DfsrPreservedFiles` 하 고 `Restore-DfsrPreservedFiles` (Windows Server 2012 R2에서 DFSR 모듈과 함께 포함), Windows PowerShell cmdlet 또는 [RestoreDFSR](http://code.msdn.microsoft.com/restoredfsr) MSDN 코드 갤러리에서 샘플 스크립트입니다. 이 스크립트는 재해 복구용 으로만 이며 제공 AS-보증 없이 합니다.

### <a name="is-there-a-way-to-know-the-state-of-replication"></a>복제 상태를 파악 방법이 있습니까?

예 복제를 모니터링 하는 방법의 여러 가지

  - DFS 복제에 사전 예방적으로 모니터링 하는 System Center Operations Manager 관리 팩  
      
  - DFS 관리는 복제 백로그, 복제 효율성 및 지정 된 복제 그룹의 파일 및 폴더 수에 대 한 기본 진단 보고서를 갖습니다.  
      
  - Windows Server 2012 R2에서 DFSR Windows PowerShell 모듈을 전파 테스트를 시작 하 고 전파 및 상태 보고서를 작성 하기 위한 cmdlet을 포함 합니다. 자세한 내용은 [Windows PowerShell의 파일 시스템 복제 Cmdlet Distributed](http://technet.microsoft.com/library/dn296601.aspx)합니다.  
      
  - Dfsrdiag.exe는 백로그 개수나 트리거 전파 테스트를 생성할 수 있는 명령줄 도구 이며 모두 복제의 상태를 표시 합니다. 전파 파일 모든 노드에 복제 되는 경우 보여 줍니다. 백로그 파일 개수는 여전히 두 대의 컴퓨터를 동기화 하기 전에 복제 해야 보여 줍니다. 백로그 수가 복제 그룹 구성원을 처리 되지 않은 업데이트입니다. Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2를 실행 하는 컴퓨터에서 Dfsrdiag.exe DFS 복제는 현재 복제 하는 업데이트를 표시할 수도 있습니다.  
      
  - 스크립트 WMI를 사용 하 여 백로그 정보를 수집할 수 있습니다-수동으로 또는 MOM 통해.  
      

## <a name="performance"></a>성능

### <a name="does-dfs-replication-support-dial-up-connections"></a>DFS 복제 전화 접속 연결을 지원 하나요?

DFS 복제는 전화 접속 속도로 작동 하지만 많은 수의 변경 내용 복제할 경우 백로그 가져올 수 있습니다. 기존 파일을 작은 변경 된 경우 DFS 복제 사용 하 여 압축 RDC (원격 차등) 파일을 직접 복사 하는 보다 훨씬 높은 성능을 제공 합니다.

### <a name="does-dfs-replication-perform-bandwidth-sensing"></a>DFS 복제 대역폭 감지를 수행 하나요?

아니요. DFS 복제 대역폭 감지를 수행 하지 않습니다. 제한 된 대역폭 (대역폭) 각 연결 단위로 사용 하도록 DFS 복제를 구성할 수 있습니다. 그러나 DFS 복제 추가로 줄어들지 않습니다 대역폭 사용률 네트워크 인터페이스 포화 되 고 짧은 기간에 대 한 DFS 복제 링크 포화 될 수 있습니다. DFS 복제는 RPC 호출을 제한 하 여 대역폭을 제한 하기 때문에 DFS 복제를 사용 하 여 제한 된 대역폭을 완전히 정확 하지 않습니다. 결과적으로, 다양 한 버퍼 (RPC) 네트워크 스택의 하위 수준에 영향을 줄 수, 네트워크 트래픽 폭주를 유발 합니다.

### <a name="does-dfs-replication-throttle-bandwidth-per-schedule-per-server-or-per-connection"></a>에서는 DFS 복제는 일정에 따라, 서버당 또는 연결당 대역폭을 제한할?

일정을 지정할 때 대역폭 제한을 구성 하는 경우 해당 복제 그룹에 대 한 모든 연결 대역폭 제한에 대 한 해당 설정이 사용 됩니다. 대역폭 제한이 설정할 수 있습니다도 DFS 관리를 사용 하 여 연결 수준 설정으로.

### <a name="does-dfs-replication-use-active-directory-domain-services-to-calculate-site-links-and-connection-costs"></a>DFS 복제 사이트 링크 및 연결 비용을 계산 하려면 Active Directory Domain Services를 사용 합니까?

아니요. DFS 복제는 Active Directory Domain Services 사이트 비용에 독립적인 관리자가 정의 된 토폴로지를 사용 합니다.

### <a name="how-can-i-improve-replication-performance"></a>복제 성능을 향상 어떻게 해야 하나요?

복제 성능 튜닝의 다른 메서드를 알아보려면 [DFSR에서 복제 성능 튜닝](http://blogs.technet.com/b/askds/archive/2010/03/31/tuning-replication-performance-in-dfsr-especially-on-win2008-r2.aspx) 에 [디렉터리 서비스 팀 블로그에 요청](http://blogs.technet.com/b/askds/)합니다.

### <a name="how-does-dfs-replication-avoid-saturating-a-connection"></a>에서는 DFS 복제를 피하는 방법은 연결 포화?

DFS 복제 연결에서 사용 하려는 최대 대역폭을 설정 하 고 서비스 네트워크 사용량 수준의 유지 합니다. BITS Background Intelligent Transfer Service (), 다른 이며 적절 하 게 설정 하는 경우 DFS 복제 연결을 포화 되지 않습니다.

그럼에도 불구 하 고 대역폭 제한 100% 정확한 아니며 짧은 기간에 대 한 DFS 복제 링크 포화 될 수 있습니다. DFS 복제는 RPC 호출을 제한 하 여 대역폭을 제한 때문입니다. 이 프로세스는 RPC를 포함 하 여 네트워크 스택의 더 낮은 수준에서 다양 한 버퍼에 의존 하므로 복제 트래픽이 네트워크 링크를 포화 때때로 수 있는 버스트에서 이동 하는 경향이 있습니다.

Windows Server 2008의 DFS 복제에서 설명한 대로 몇 가지 성능 개선 사항을 포함 [분산 파일 시스템](https://technet.microsoft.com/en-us/library/Cc753479)를 토픽에 [Windows Server 2003 sp1에서 Windows Server로의 기능 변경 2008](https://technet.microsoft.com/en-us/library/cc753208)합니다.

### <a name="how-does-dfs-replication-performance-compare-with-frs"></a>DFS 복제 성능 FRS를 사용 하 여 어떻게 비교 되나요?

DFS 복제는 특히 큰 파일에 작은 변경 내용이 고 RDC를 사용 하는 경우 FRS를 보다 훨씬 더 빠릅니다. 예를 들어, RDC를 사용 하 여 2 MB PowerPoint® 프레젠테이션을 약간 변경 될 수 있습니다만 60 (kb) 네트워크를 통해 전송 되 고, 전송 된 바이트는 97%를 절감 합니다.

RDC에서 사용 되지 않는 파일 64KB 보다 작은 및 없습니다 유용할 수 있습니다 고속 Lan에서 네트워크 대역폭은 하지 경합이 있는 합니다. DFS 관리를 사용 하 여 각 연결 단위로 RDC는 비활성화할 수 있습니다.

### <a name="how-frequently-does-dfs-replication-replicate-data"></a>DFS 복제 데이터를 복제 하는 빈도

설정한 일정에 따라 데이터가 복제 됩니다. 예를 들어, 연중 무휴로 15 분 간격을 일정을 설정할 수 있습니다. 이러한 간격 동안 복제가 설정 되어 있습니다. 복제에는 (일반적으로 몇 초 안에) 파일 변경이 감지 된 후에 곧 시작 됩니다.

복제 그룹 일정의 연결 일정 받는 구성원의 현지 시간으로 설정 되어 있지만를 조정 (협정 세계시) 설정할 수 있습니다. 여러 표준 시간대의 복제 그룹에 걸쳐 있는 경우이를 고려 합니다. 현지 시간 인바운드 연결을 호스트 하는 멤버의 시간을 의미 합니다. 일정은 현지 시간으로 설정 된 경우 인바운드 연결과 해당 아웃 바운드 연결의 표시 된 일정 시간대 차이 반영 합니다.

### <a name="how-much-of-my-servers-system-resources-will-dfs-replication-consume"></a>My server의 시스템 리소스의 양을 DFS 복제 사용?

디스크, 메모리 및 DFS 복제에서 사용 된 CPU 리소스 비율 변경, 복제 그룹 구성원의 수 및 복제 된 폴더 수 파일의 크기와 수를 비롯 한 인수의 수에 따라 달라 집니다. 또한 일부 리소스 예측 하기 어려운 합니다. 예를 들어 DFS 복제 데이터베이스에 사용 되는 저장소 엔진 ESE (Extensible) 기술에는 주문형 해제 하는 사용 가능한 메모리의 비율을 사용할 수 있습니다. 서버 구성에 따라 동일한 서버에서 DFS 복제 이외의 응용 프로그램을 호스트할 수 있습니다. 그러나 여러 응용 프로그램 또는 단일 서버의 서버 역할을 호스팅 때 프로덕션 환경에서 구현 하기 전에이 구성을 테스트 하는 것이 중요 합니다.

### <a name="what-happens-if-a-wan-link-fails-during-replication"></a>WAN 링크를 복제 하는 동안 오류가 발생 하는 경우 어떻게 되나요?

연결이 다운 되 면 DFS 복제는 계속 시도 일정 열려 있는 동안 복제 합니다. 연결 오류를 사전에 (경고)를 통해 MOM 및 DFS 복제 상태 보고서 (사후,와 같은 경우 관리자로 실행)를 사용 하 여 수집 수는 DFS 복제 이벤트 로그에 명시 된 수도 있습니다.

## <a name="remote-differential-compression-details"></a>원격 차등 압축 세부 정보

### <a name="are-changes-compressed-before-being-replicated"></a>변경 내용은 복제 하기 전에 압축은?

예 모든 파일 (이미 압축 된)는 다음을 제외 하 고 형식에 대 한 전송 되기 전에 압축 된 파일의 변경 된 부분이:.wma,.wmv,.zip,.jpg,.mpg,.mpeg. m1v,.mp2. mp3,.mpa,.cab,.wav,.snd,.au,.asf,.wm,.avi,.z,.gz,.tgz, 및.frx 합니다. 이러한 파일 형식에 대 한 압축 설정은 Windows Server 2003 R2에서 구성할 수 없는 합니다.

### <a name="can-an-administrator-turn-off-rdc-or-change-the-threshold"></a>관리자로는 RDC를 해제 하거나 수 임계값을 변경?

예 지정된 된 연결의 속성 페이지를 통해 RDC를 해제할 수 있습니다. RDC를 사용 하지 않도록 설정 하면 CPU 사용률 및 복제 대기 시간에 대역폭 제약 조건이 없는 고속 로컬 영역 네트워크 (LAN) 링크 또는 64KB 보다 작은 파일 주로 구성 된 복제 그룹에 대 한 줄일 수 있습니다. 복제 성능 개선 확인 하려면 변경 이전과 이후의 연결 RDC를 사용 하지 않도록 설정 하려는 경우은 복제 효율성을 테스트 합니다.

RDC 크기 임계값을 사용 하 여 변경할 수 있습니다 합니다 **Dfsradmin 연결이 설정** 명령, DFS 복제 WMI 공급자 또는 구성 XML을 수동으로 편집 하 여 파일입니다.

### <a name="does-rdc-work-on-all-file-types"></a>RDC 모든 파일 형식에서 작동 합니까?

예 RDC는 파일 데이터 형식에 관계 없이 블록 수준에서 차이 계산 합니다. 그러나 RDC Word 문서, PST 파일을 VHD 이미지 등 특정 파일 형식에서 보다 효율적으로 작동합니다.

### <a name="how-does-rdc-work-on-a-compressed-file"></a>RDC는 압축 된 파일에서 어떻게 작동 합니까?

DFS 복제는 RDC를 변경 하 고 해당 블록에만 네트워크를 통해 전송 하는 파일에 블록을 계산 합니다. DFS 복제 파일의 내용에 대해 알 필요가 없습니다-는 블록만 변경 되었습니다.

### <a name="is-cross-file-rdc-enabled-when-upgrading-to-windows-server-enterprise-edition-or-datacenter-edition"></a>Windows Server Enterprise Edition 또는 Datacenter Edition으로 업그레이드할 때 사용 하도록 설정 하는 RDC 파일은?

Windows Server의 Standard 버전을 지원 하지 않는 파일 간 RDC 합니다. 그러나 지원 파일 간 RDC를는 버전으로 업그레이드할 때 또는 복제 연결의 멤버는 지원 되는 버전을 실행 중인 경우 활성화 자동으로 됩니다. 목록을 버전 지원 파일 간 RDC는 에디션의 Windows 운영 체제 지원 파일 간 RDC를 참조 하세요?

### <a name="is-rdc-true-block-level-replication"></a>RDC true 블록 수준 복제 기능

아니요. RDC는 파일 전송 압축에 대 한 범용 프로토콜. DFS 복제 디스크 블록 수준이 아닌 파일 수준에서 블록에 RDC를 사용합니다. RDC는 파일을 블록으로 나눕니다. 파일의 각 블록에 적은 수의 큰 블록을 나타낼 수 있는 바이트는 서명을 계산 합니다. 서명 집합을 서버에서 클라이언트로 전송 됩니다. 클라이언트는 자체 서버 서명을 비교합니다. 클라이언트를 서버에 클라이언트에서 없는 서명에 대 한 데이터만 전송 요청 합니다.

### <a name="what-happens-if-i-rename-a-file"></a>이름을 바꾸려면 파일 하는 경우 어떻게 되나요?

DFS 복제에는 다음 복제 시 복제 그룹의 다른 모든 멤버에 파일을 이름을 바꿉니다. 파일은 추적 된 고유 ID를 사용 하 여, 하므로 파일 이름 바꾸기 및 이동 하는 복제본 내에서 파일에 파일을 복제 하려면 DFS 복제 기능에 영향을 주지 않습니다.

### <a name="what-is-cross-file-rdc"></a>항목은 파일 간 RDC?

파일 간 RDC 클라이언트 쪽에서 동일한 이름의 파일이 존재 하지 않습니다 하는 경우에 RDC를 사용 하도록 DFS 복제를 허용 합니다. 파일 간 RDC 경험적 접근을 사용 하 여 복제 해야 하는 파일에 유사한 파일을 확인 하 고 WAN을 통해 사용 하 여 블록 복제 파일 데이터의 양을 최소화 하기 위해 동일한 유사한 파일을 전송 합니다. 파일 간 RDC는이 프로세스의 최대 5 개의 유사한 파일의 블록을 사용할 수 있습니다.

사용할 파일 간 RDC, 복제 연결의 멤버로 실행 해야 Windows 버전에서는 파일 간 RDC 합니다. 목록을 버전 지원 파일 간 RDC는 에디션의 Windows 운영 체제 지원 파일 간 RDC를 참조 하세요?

### <a name="what-is-rdc"></a>RDC는 무엇입니까?

RDC (원격 차등 압축)는 효율적으로 제한 된 대역폭 네트워크를 통해 파일을 업데이트 하는 데 사용할 수 있는 클라이언트-서버 프로토콜. Rdc 삽입, 제거 및 재배열을 데이터 파일에서 파일을 업데이트할 때 변경 내용만 복제 하려면 DFS 복제를 사용 하도록 설정 합니다. RDC는 기본적으로 64 KB 수 있는 파일에 대해서만 사용 하거나 더 큰 됩니다. RDC는 DfsrPrivate 또는 복제 된 폴더에서 이름이 같은 파일의 이전 버전을 사용할 수\\ConflictandDeleted 폴더 (복제 된 폴더의 로컬 경로 아래에 있음).

### <a name="when-is-rdc-used-for-replication"></a>복제에 대 한 RDC는 사용 하는 경우

파일을 최소 크기 임계값을 초과 하는 경우에 RDC가 사용 됩니다. 이 크기 임계값은 기본적으로 64KB입니다. 해당 임계값을 초과 하면 파일에 복제 한 후 파일의 많은 부분을 변경 하거나 RDC를 사용 하지 않도록 설정 하지 않는 한 파일의 업데이트 된 버전이 항상 RDC를 사용 합니다.

### <a name="which-editions-of-the-windows-operating-system-support-cross-file-rdc"></a>버전 Windows 운영 체제 지원에 파일 간 RDC?

사용할 파일 간 RDC, 복제 연결의 멤버로 실행 해야 합니다는 에디션의 Windows 운영 체제에서는 파일 간 RDC 합니다. 파일 간 RDC를 다음 표에서 Windows 운영 체제의 버전을 지원 합니다.

### <a name="cross-file-rdc-availability-in-editions-of-the-windows-operating-system"></a>파일 버전의 Windows 운영 체제에서 RDC 가용성

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
<td><p>예*</p></td>
<td><p>제공되지 않음</p></td>
<td><p>예*</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012</p></td>
<td><p>예</p></td>
<td><p>제공되지 않음</p></td>
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
<td><p>아니오</p></td>
<td><p>사용자 계정 컨트롤</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2003 R2</p></td>
<td><p>아니오</p></td>
<td><p>사용자 계정 컨트롤</p></td>
<td><p>아니요</p></td>
</tr>
</tbody>
</table>

\* 선택적으로 해제할 수 있습니다 파일 간 RDC Windows Server 2012 r2.

## <a name="replication-details"></a>복제 세부 정보

### <a name="can-i-change-the-path-for-a-replicated-folder-after-it-is-created"></a>변경 복제 된 폴더의 경로를 만든 후

아니요. 복제 된 폴더의 경로 변경 해야 할 경우 DFS 관리에서 삭제 하 고 새 복제 폴더를 다시 추가 해야 합니다. 다음 DFS 복제는 압축 RDC (원격 차등)를 사용 하 여 데이터를 보내는 구성원과 받는 구성원으로 같은지 여부를 결정 하는 동기화를 수행 합니다. 다시 폴더의 모든 데이터를 복제 하지 않습니다.

### <a name="can-i-configure-which-file-attributes-are-replicated"></a>파일 특성은 복제를 구성할 수 있나요?

아니요, DFS 복제는 파일 특성을 구성할 수 없습니다.

특성 값 및 해당 설명의 목록을 참조 하세요 [파일 특성](http://go.microsoft.com/fwlink/?linkid=182268) MSDN의 (http://go.microsoft.com/fwlink/?LinkId=182268)합니다.

다음 특성 값을 사용 하 여 설정 됩니다는 `SetFileAttributes dwFileAttributes` 함수 및 이러한 DFS 복제에서 복제 됩니다. 이러한 특성 값이 변경 된 특성의 복제를 트리거합니다. 내용을 변경도 하지 않는 한 파일의 내용은 복제 되지 않습니다. 자세한 내용은 [SetFileAttributes 함수](http://go.microsoft.com/fwlink/?linkid=182269) MSDN 라이브러리에서 (http://go.microsoft.com/fwlink/?LinkId=182269)합니다.

  - FILE\_ATTRIBUTE\_HIDDEN  
      
  - 파일\_특성\_읽기 전용  
      
  - 파일\_특성\_시스템  
      
  - 파일\_특성\_없습니다\_콘텐츠\_인덱스  
      
  - 파일\_특성\_오프 라인  
      

DFS 복제에서 다음 특성 값을 복제할지 하지만 복제 트리거하지 않습니다.

  - 파일\_특성\_보관  
      
  - 파일\_특성\_보통  
      

다음 파일 특성 값을 트리거할 수도 복제를 사용 하 여 설정할 수 없습니다 있지만 합니다 `SetFileAttributes` 함수 (사용 하 여는 `GetFileAttributes` 특성 값을 볼 수는 함수).

  - 파일\_특성\_재분석\_지점  
      

> [!NOTE]
> DFS 복제는 재분석 태그 IO_REPARSE_TAG_SYMLINK 아닌 재분석 지점 특성 값을 복제 하지 않습니다. 일반 파일 처럼 IO_REPARSE_TAG_DEDUP, IO_REPARSE_TAG_SIS 또는 IO_REPARSE_TAG_HSM 재분석 태그를 사용 하 여 파일 복제 됩니다. 그러나 재분석 태그 및 재분석 데이터 버퍼를 재분석 지점을 로컬 시스템에만 작동 하기 때문에 다른 서버에 복제 되지 않습니다. 
<br>

  - FILE\_ATTRIBUTE\_COMPRESSED  
      
  - FILE\_ATTRIBUTE\_ENCRYPTED  
      

> [!NOTE]
> DFS 복제는 파일 시스템 EFS (암호화)를 사용 하 여 암호화 된 파일을 복제 하지 않습니다. DFS 복제에는 타사 소프트웨어를 사용 하 여 암호화 된 파일에 FILE_ATTRIBUTE_ENCRYPTED 특성 값을 설정 하지 않는 경우에 됩니다 하는 파일 복제지 않습니다. 
<br>

  - 파일\_특성\_SPARSE\_파일  
      
  - 파일\_특성\_디렉터리  
      

DFS 복제 파일을 복제 하지 않습니다\_특성\_임시 값입니다.

### <a name="can-i-control-which-member-is-replicated"></a>멤버는 복제를 제어할 수 있나요?

예 복제 그룹을 만들 때 토폴로지를 선택할 수 있습니다. 선택할 수 있습니다 **토폴로지가 없습니다** 복제 그룹을 만든 후에 수동으로 연결을 구성 합니다.

### <a name="can-i-seed-a-replication-group-member-with-data-prior-to-the-initial-replication"></a>초기 복제 하기 전에 데이터를 사용 하 여 복제 그룹 구성원을 시드할 수 있습니까?

예 DFS 복제는 초기 복제 하기 전에 복제 그룹 멤버에 대 한 파일 복사를 지원합니다. 이 "사전 준비" 초기 복제 시 복제 된 데이터의 양이 대폭 감소 수 있습니다.

초기 복제 파일 실제 특성 또는 타임 스탬프에 의해서만 달라 지는 경우 콘텐츠를 복제할 필요가 없습니다. 실제 특성은 Win32 함수에서 설정할 수 있는 특성 `SetFileAttributes`합니다. 자세한 내용은 [SetFileAttributes 함수](http://go.microsoft.com/fwlink/?linkid=182269) MSDN 라이브러리에서 (http://go.microsoft.com/fwlink/?LinkId=182269)합니다. 두 개의 파일 압축 등의 다른 특성을 다른 파일의 내용은 복제 됩니다.

복제 그룹 구성원을 사전 준비할 대상 서버에서 해당 폴더로 파일을 복사 하 고 복제 그룹을 만들 다음 기본 멤버를 선택 합니다. 주 구성원의 콘텐츠는 "신뢰할 수 있습니다." 것으로 간주 하기 때문에 복제 하려는 가장 최신 파일이 있는 멤버를 선택 합니다. 이 초기 복제 하는 동안 주 구성원의 파일이 항상 덮어씁니다 복제 그룹의 다른 멤버에 있는 파일의 다른 버전을 의미 합니다.

사전 시드 및 DFSR 데이터베이스를 복제 하는 방법에 대 한 내용은 [DFS 복제 Windows Server 2012 R2에서 초기 동기화 합니다. 클론의 습격](http://blogs.technet.com/b/filecab/archive/2013/08/21/dfs-replication-initial-sync-in-windows-server-2012-r2-attack-of-the-clones.aspx)합니다.

초기 복제에 대 한 자세한 내용은 참조 하세요. [복제 그룹을 만들](https://technet.microsoft.com/en-us/library/cc725893)합니다.

### <a name="does-dfs-replication-overcome-common-file-replication-service-issues"></a>DFS 복제에 일반적인 파일 복제 서비스 문제 해결할 수는?

예 DFS 복제는 세 가지 일반적인 FRS 문제 극복 합니다.

  - 업무 일지를 래핑합니다. DFS 복제는 저널 래핑하고 즉석에서 복구합니다. 각 기존 파일 또는 폴더 journalWrap로 표시 되며 복제를 다시 사용 하기 전에 파일 시스템에 대해 확인 합니다. 이 볼륨을 복구 하는 동안 어느 방향으로든에서 복제에 대 한 제공 되지 않습니다.  
      
  - 과도 하 게 복제 합니다. 과도 한 복제를 방지 하려면 DFS 복제는 크레딧의 시스템을 사용 합니다.  
      
  - 모핑 된 폴더: 모핑 된 폴더 이름을 방지 하려면 DFS 복제는 숨겨진된 DfsrPrivate에 충돌 하는 데이터를 저장\\ConflictandDeleted 폴더 (복제 된 폴더의 로컬 경로 아래에 있음). 예를 들어, FRS를 사용 하 여 복제 하는 서로 다른 서버에 동일한 이름의 여러 폴더를 동시에 만드는 이전 폴더 이름을 바꾸려면 FRS 하면 됩니다. DFS 복제는 대신 로컬 충돌 및 삭제 된 폴더에 이전 폴더를 이동합니다.  
      

### <a name="does-dfs-replication-replicate-files-in-chronological-order"></a>DFS 복제는 시간 순서 대로 파일을 복제?

아니요. 파일의 순서가 복제 될 수 있습니다.

### <a name="does-dfs-replication-replicate-files-that-are-being-used-by-another-application"></a>DFS 복제는 다른 응용 프로그램에서 사용 중인 파일을 복제할?

응용 프로그램 파일을 엽니다 (열려 있는 동안 다른 응용 프로그램에서 사용 되지 않도록 방지)를 파일 잠금을 만듭니다를 닫을 때까지 DFS 복제 파일을 복제 하지 않습니다. 응용 프로그램이 읽기 공유 액세스를 사용 하 여 파일을 열면 파일을 여전히 복제할 수 있습니다.

### <a name="does-dfs-replication-replicate-ntfs-file-permissions-alternate-data-streams-hard-links-and-reparse-points"></a>에서는 DFS 복제 NTFS 파일 권한이, 대체 데이터 스트림, 하드 링크를 복제 하 고 재분석 지점을?

  - DFS 복제는 NTFS 파일 권한이 및 대체 데이터 스트림을 복제합니다.  
      
  - Microsoft 복제 된 폴더에 NTFS 하드 링크를 만들 파일에서 지원 하지 않습니다 – 발생할 수 있으므로 복제 문제로 영향을 받는 파일과 함께 합니다. 하드 링크 파일 DFS 복제에서 무시 되 고 복제 되지 않습니다. 연결 지점을 복제 되지 않습니다 하 고 DFS 복제 4406 발견할 각 연결 지점에 대 한 이벤트를 기록 합니다.  
      
  - DFS 복제에서 복제만 재분석 지점을 IO를 사용 하는\_재분석\_태그\_SYMLINK 태그; 그러나 DFS 복제는 보장 하지는 symlink의 대상도 복제 됩니다. 자세한 내용은 참조는 [디렉터리 서비스 팀 블로그에 요청](http://blogs.technet.com/b/askds/archive/2011/09/30/friday-mail-sack-super-slo-mo-edition.aspx)합니다.  
      
  - IO 사용 하 여 파일\_재분석\_태그\_중복 제거, IO\_재분석\_태그\_SIS, 또는 IO\_재분석\_태그\_HSM 재분석 태그 복제 일반 파일로. 재분석 태그 및 재분석 데이터 버퍼를 복제 되지 않습니다 다른 서버로 재분석 지점을 로컬 시스템에만 작동 하기 때문입니다. 따라서 DFS 복제는 Windows Server 2012 또는 단일 인스턴스 저장소 (SIS)의 데이터 중복 제거를 사용 하는 볼륨에 폴더를 복제할 수, 단, 데이터 중복 제거 정보는 역할 서비스를 사용 하는 각 서버에서 별도로 유지 됩니다.  
      

### <a name="does-dfs-replication-replicate-timestamp-changes-if-no-other-changes-are-made-to-the-file"></a>DFS 복제 경우 다른 변경 내용이 없는 파일에 타임 스탬프 변경 내용 복제는?

아니요, DFS 복제는 유일한 변경 내용은 변경 되는 타임 스탬프 파일을 복제 하지 않습니다. 또한 파일에 다른 변경을 수행 하는 경우가 아니면 변경 된 타임 스탬프 복제 그룹의 다른 구성원에 복제 되지 않습니다.

### <a name="does-dfs-replication-replicate-updated-permissions-on-a-file-or-folder"></a>파일 또는 폴더에서 DFS 복제 복제 업데이트 권한 하나요?

예 DFS 복제는 파일 및 폴더에 대 한 권한을 변경 합니다. DFS 복제 준비 영역으로 전체 파일을 계속 읽을 해야 하지만 액세스 제어 목록 (ACL)를 사용 하 여 연결 된 파일 부분에만 복제 됩니다.


> [!NOTE]
> 많은 수의 파일에 대 한 Acl 변경 복제 성능에 영향을 미칠 수 있습니다. 그러나 RDC를 사용 하면 전송 되는 데이터 양이 Acl, 전체 파일의 크기가 아니라의 크기에 비례 합니다. 디스크 트래픽의 양에 여전히 파일의 크기에 비례하여 이므로 준비 폴더에서 파일을 읽어야 합니다. 
<br>


### <a name="does-dfs-replication-support-merging-text-files-in-the-event-of-a-conflict"></a>DFS 복제 충돌이 발생 한 경우 병합 텍스트 파일을 지원 하나요?

DFS 복제는 충돌 하는 경우 파일을 병합 하지 않습니다. 그러나 숨겨진된 DfsrPrivate 파일의 이전 버전을 유지 하려고지 않습니다\\충돌을 감지 하는 컴퓨터의 ConflictandDeleted 폴더입니다.

### <a name="does-dfs-replication-use-encryption-when-transmitting-data"></a>DFS 복제 데이터를 전송할 때 암호화 사용 합니까?

예 DFS 복제는 암호화를 사용 하 여 원격 프로시저 호출 (RPC) 연결을 사용합니다.

### <a name="is-it-possible-to-disable-the-use-of-encrypted-rpc"></a>암호화 된 RPC의 사용을 비활성화할 수는?

아니요. DFS 복제 서비스가 TCP를 통한 원격 프로시저 호출 (RPC)를 사용 하 여 데이터를 복제. 인터넷을 통해 전송 데이터를 보호 하려면 DFS 복제 서비스를 항상 인증 수준 상수를 사용 하도록 설계 된 `RPC_C_AUTHN_LEVEL_PKT_PRIVACY`합니다. 이렇게 하면 인터넷을 통해 RPC 통신이 항상 암호화 됩니다. 따라서 DFS 복제 서비스에서 암호화 된 RPC의 사용을 비활성화할 수 없는 합니다.

자세한 내용은 다음 Microsoft 웹 사이트를 참조 하세요.

  - [RPC 기술 참조](http://go.microsoft.com/fwlink/?linkid=182278)  
      
  - [원격 차등 압축에 대 한](http://go.microsoft.com/fwlink/?linkid=182279)  
      
  - [인증 수준 상수](http://go.microsoft.com/fwlink/?linkid=182280)  
      

### <a name="how-are-simultaneous-replications-handled"></a>동시 복제는 어떻게 처리 되나요?

복제 된 폴더당 하나의 업데이트 관리자가 있습니다. 관리자 작업 서로 독립적으로 업데이트 합니다.

기본적으로 최대 16 개 (4의 Windows Server 2003 R2) 동시 다운로드 수가 모든 연결 및 복제 그룹 간에 공유 됩니다. 연결 및 복제 그룹 업데이트 serialize 되지 않습니다 이므로 순서에 관계 없이 업데이트 수신 됩니다. 두 일정을 열 경우 업데이트 일반적으로 받아서 두 연결 모두에서 동시에 설치 합니다.

### <a name="how-do-i-force-replication-or-polling"></a>복제 또는 폴링을 강제로 수행 하는 방법

할 수 있습니다 복제 즉시 DFS 관리를 사용 하 여에 설명 된 대로 [복제 일정 편집](https://technet.microsoft.com/en-us/library/Cc732278)합니다. 복제를 사용 하 여 강제로 수도 있습니다는 `Sync-DfsReplicationGroup` Windows Server 2012 r2에 도입 된 DFSR PowerShell 모듈에 포함 된 cmdlet 또는 **Dfsrdiag SyncNow** 명령입니다. 사용 하 여 폴링을 할 수 있습니다 합니다 `Update-DfsrConfigurationFromAD` cmdlet 또는 **Dfsrdiag PollAD** 명령입니다.

### <a name="is-it-possible-to-configure-a-quiet-time-between-replications-for-files-that-change-frequently"></a>자주 변경 되는 파일에 대 한 복제 간의 시간 간격을 자동 구성할 수는?

아니요. 일정이 열려 있으면 사용자가 알림을 받으면으로 DFS 복제는 변경 내용을 복제 합니다. 파일에 대 한 유휴 시간 구성 방법이 없습니다.

### <a name="is-it-possible-to-configure-one-way-replication-with-dfs-replication"></a>DFS 복제를 사용 하 여 단방향 복제를 구성할 수는?

예 Windows Server 2012 또는 Windows Server 2008 R2를 사용 하는 경우에 단방향 연결을 통해 콘텐츠를 복제 하는 읽기 전용 복제 폴더를 만들 수 있습니다. 자세한 내용은 [복제 된 폴더가 읽기 전용 특정 멤버에 게](http://go.microsoft.com/fwlink/?linkid=156740) (http://go.microsoft.com/fwlink/?LinkId=156740)합니다.

Windows Server 2008 또는 Windows Server 2003 R2에서 DFS 복제를 사용 하 여 단방향 복제 연결을 만들기 지원 하지 않습니다. 이렇게 하면 문제 및 DFS 복제 데이터베이스를 사용 하 여 문제를 준비 상태 확인 토폴로지 오류를 포함 한 다양 한 문제가 발생할 수 있습니다.

Windows Server 2008 또는 Windows Server 2003 R2를 사용 하는 경우 다음 작업을 수행 하 여 단방향 연결을 시뮬레이션할 수 있습니다.

  - 관리자는 주 서버로 지정 하려면 서버에만 변경할 수 있도록 교육 합니다. 다음 대상 서버로 변경 내용을 복제 합니다.  
      
  - 최종 사용자에 대 한 쓰기 권한이 없는 있도록 대상 서버의 공유 사용 권한을 구성 합니다. 변경 하지 않고 허용 되 면 분기 서버에서 다시 복제할 대상이 됩니다 단방향 연결을 시뮬레이션 하 고 WAN 사용률을 낮게 유지 합니다.  
      

### <a name="is-there-a-way-to-force-a-complete-replication-of-all-files-including-unchanged-files"></a>변경 되지 않은 파일을 비롯 한 모든 파일의 전체 복제를 강제로 방법이 있습니까?

아니요. DFS 복제가 파일을 동일한 경우 해당 복제 하지 않습니다. 변경 된 파일, 복제 되지 않은 경우 DFS 복제는 자동으로 수행 하도록 구성 하는 경우으로 복제 됩니다. WMI 메서드를 사용 하 여 구성된 된 일정을 덮어쓰려면 **ForceReplicate()** 합니다. 그러나 이것이 일정을 재정의 하 고 변경 되거나 동일한 파일의 복제를 강제 하지 않습니다.

### <a name="what-happens-if-the-primary-member-suffers-a-database-loss-during-initial-replication"></a>주 구성원에 초기 복제 하는 동안 데이터베이스가 손실 문제가 발생 하는 경우 어떻게 되나요?

초기 복제 하는 동안 주 구성원의 파일 받는 구성원에 주 구성원에 있는 파일의 버전이 다른 경우 발생 하는 충돌 해결 우선 항상 적용 됩니다. 기본 멤버를 지정 하는 Active Directory Domain Services에 저장 됩니다 하 고 지정 되었으나 복제의 모든 멤버 그룹 복제 주 구성원에 복제 하려면 준비 된 후의 선택을 취소 합니다.

초기 복제 실패 또는 복제 하는 동안 DFS 복제 서비스를 다시 시작 하는 경우 주 구성원 로컬 DFS 복제 데이터베이스에 주 구성원 지정을 확인 하 고 초기 복제를 다시 시도 합니다. 주 구성원의 DFS 복제 데이터베이스는 기본으로 지정 하는 Active Directory Domain Services를 지운 후 손실 되지만 복제 그룹의 모든 멤버에는 초기 복제를 완료 하기 전에 복제 그룹의 모든 멤버 하지 못했습니다. 서버가 없는 기본 멤버로 지정 하기 때문에 폴더를 복제 합니다. 이 경우 사용 합니다 **Dfsradmin 멤버 자격 /isprimary:true 설정** 주 구성원 지정을 수동으로 복원 하려면 주 구성원 서버에서 명령입니다.

초기 복제에 대 한 자세한 내용은 참조 하십시오 [복제 그룹을 만들](https://technet.microsoft.com/en-us/library/cc725893)합니다.


> [!WARNING]
> 기본 멤버를 지정 하는 초기 복제 프로세스 중에 사용 됩니다. 사용 하는 경우는 <STRONG>Dfsradmin</STRONG> 복제 후 복제 된 폴더에 대 한 기본 멤버 완료 되 면 DFS 복제 Active Directory Domain Services의 기본 구성원으로 서버를 지정 하지 않습니다 지정 하는 명령입니다. 그러나 되돌릴 손상이 나 데이터 손실에도 서버에서 DFS 복제 데이터베이스 이후에 저하 하는 경우 서버 시도 복제의 다른 멤버에서 해당 데이터를 복구 하는 대신 기본 멤버는 초기 복제를 수행 하려면 그룹입니다. 기본적으로, 서버 충돌이 발생할 수 있으므로 rogue 주 서버에서 됩니다. 따라서 초기 복제에 영구적으로 실패 한 것이 확실 한 경우 기본 멤버를 수동으로 지정 합니다. 
<br>


### <a name="what-happens-if-the-replication-schedule-closes-while-a-file-is-being-replicated"></a>복제 일정을 닫으면 파일 복제 되는 동안 어떻게 되나요?

RDC (원격 차등 압축) 연결에 사용 되는 경우 인바운드 일정 닫기 직전 복제를 시작 하는 64KB 보다 큰 파일의 복제 (또는 변경 **없습니다 대역폭**) 계속 될 때를 예약 열립니다 (이외의 값으로 변경 하거나 **없습니다 대역폭**). 복제 중지 될 때의 상태로에서 복제가 계속 됩니다.

RDC 꺼져 있으면 DFS 복제에 완전히 파일 전송을 다시 시작 합니다. 이 파일을 받는 구성원에서 사용할 수 있는 때 지연 될 수 있습니다.

### <a name="what-happens-when-two-users-simultaneously-update-the-same-file-on-different-servers"></a>두 명의 사용자가 동시에 서로 다른 서버에 동일한 파일을 업데이트 하는 경우 어떻게 되나요?

DFS 복제에서 충돌을 감지 하는 경우 마지막으로 저장 된 파일의 버전을 사용 합니다. 다른 파일에는 DfsrPrivate 이동\\ConflictandDeleted 폴더 (아래에 충돌을 해결 하는 컴퓨터의 복제 된 폴더의 로컬 경로). 구성 된 크기를 초과 하는 충돌 및 삭제 된 폴더 또는 DFS 복제에서 디스크 공간 오류 부족 때 발생 하는 충돌 및 삭제 된 폴더 정리 될 때까지 남아 있습니다. 충돌 및 삭제 된 폴더를 복제 되지 않습니다 및 FRS.에서 가능 했던 모핑 된 디렉터리의 문제를 방지 하는이 메서드의 충돌 해결

충돌이 발생할 경우 DFS 복제에서 DFS 복제 이벤트 로그에 정보 이벤트를 기록 합니다. 이 이벤트는 다음과 같은 이유로 사용자 조치가 필요 없는 않습니다.

  - (서버 관리자 에게만 표시 됩니다) 사용자에 게 표시 되지 않습니다.  
      
  - DFS 복제 캐시로 충돌 및 삭제 된 폴더를 처리합니다. 할당량 임계값에 도달 하면 해당 파일의 일부 정리 합니다. 충돌 하는 파일이 저장 될 하지 않을 수도가 있습니다.  
      
  - 충돌은 충돌의 원점부터 다른 서버에 있을 수 있습니다.  
      

## <a name="staging"></a>준비

### <a name="does-dfs-replication-continue-staging-files-when-replication-is-disabled-by-a-schedule-or-bandwidth-throttling-quota-or-when-a-connection-is-manually-disabled"></a>DFS 복제 준비 파일 연결을 수동으로 사용 하지 않는 경우 또는 복제 일정 또는 대역폭 할당량 제한에 의해 비활성화 되 면 계속지 않습니다?

아니요. DFS 복제 대역폭 제한 할당량을 초과 하는 경우 또는 연결 해제 하면 예약 된 복제 시간 외부 단계 파일에 계속 되지 않습니다.

### <a name="does-dfs-replication-prevent-other-applications-from-accessing-a-file-during-staging"></a>DFS 복제에 다른 응용 프로그램 파일을 준비 하는 동안 액세스 하지 못하도록 방지 않습니다?

아니요. DFS 복제는 사용자 또는 응용 프로그램 복제 폴더에 파일을 열 수 없도록 차단 되지 않는 방식으로 파일을 엽니다. 이 방법은 "편의적 잠금." 라고 합니다.

### <a name="is-it-possible-to-change-the-location-of-the-staging-folder-with-the-dfs-management-tool"></a>DFS 관리 도구를 사용 하 여 준비 폴더의 위치를 변경할 수는?

예 준비 폴더 위치에 구성 되어 합니다 **고급** 탭의 **속성** 복제 그룹의 각 멤버에 대 한 대화 상자.

### <a name="when-are-files-staged"></a>파일을 준비 하는 경우

파일에서 받는 구성원의 파일을 요청 하는 경우 보내는 구성원에서 준비 된 (파일이 64KB 경우가 아니면 작거나)는 다음 표에 나와 있는 것 처럼 합니다. 256kb까지 가능 하지 않은 파일 준비 된 압축 RDC (원격 차등) 연결에서 비활성화 된 경우 또는 작게 합니다. 파일 전송 될 때 크기가 64KB 보다 작은 경우 16 KB 1 MB 간에이 설정을 구성할 수 있지만 받는 구성원의 준비도 됩니다. 일정 닫혀 있는 경우 파일 준비 되지 않습니다.

### <a name="the-minimum-file-sizes-for-staging-files"></a>파일을 준비 하는 것에 대 한 최소 파일 크기

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th> </th>
<th>RDC를 사용 하도록 설정</th>
<th>RDC를 사용 하지 않도록 설정</th>
</tr>
</thead>
<tbody>
<tr class="even">
<td><p>보내는 구성원</p></td>
<td><p>64KB</p></td>
<td><p>256KB.</p></td>
</tr>
<tr class="odd">
<td><p>받는 구성원</p></td>
<td><p>기본적으로 64 KB</p></td>
<td><p>기본적으로 64 KB</p></td>
</tr>
</tbody>
</table>

### <a name="what-happens-if-a-file-is-changed-after-it-is-staged-but-before-it-is-completely-transmitted-to-the-remote-site"></a>파일이 준비 되어 있지만 완전히 원격 사이트에 전송 되기 전에 변경 된 경우 어떻게 되나요?

파일의 일부가 이미 전송 되는 경우 DFS 복제 계속 전송이 됩니다. 파일에는 DFS 복제 시작 파일을 전송 하기 전에 변경 되 면 최신 버전의 파일 전송 됩니다.

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
<td><p>Windows Server 2019 업데이트 되었습니다.</p></td>
<td><p>새 운영 체제입니다.</p></td>
</tr>
<tr class="even">
<td><p>2013년 10월 9일</p></td>
<td><p>업데이트 DFS 복제의 지원 되는 제한은 무엇 인가요? Windows Server 2012 R2에 대 한 테스트의 결과 사용 하 여 섹션입니다.</p></td>
<td><p>최신 버전의 Windows Server에 대 한 업데이트</p></td>
</tr>
<tr class="odd">
<td><p>2013 년 1 월 30</p></td>
<td><p>DFS 복제는 추가 연결을 수동으로 사용 하지 않는 경우 또는 복제 일정 또는 대역폭 할당량 제한에 의해 비활성화 되 면 파일을 스테이징 계속? 항목입니다.</p></td>
<td><p>고객 질문</p></td>
</tr>
<tr class="even">
<td><p>2012 년 10 월 31 일</p></td>
<td><p>편집할 DFS 복제의 지원 되는 제한은 무엇 인가요? 볼륨에 복제 된 파일의 테스트 수를 늘리려면 항목입니다.</p></td>
<td><p>고객 의견</p></td>
</tr>
<tr class="odd">
<td><p>2012 년 8 월 15 일</p></td>
<td><p>DFS 복제는 복제 NTFS 권한, 대체 데이터 스트림, 하드 링크 파일 및 재분석 지점 편집? DFS 복제에서 하드 링크를 처리 하는 방법을 명확 하 고 재분석 시키는 진입점입니다.</p></td>
<td><p>고객 지원 서비스에서 피드백</p></td>
</tr>
<tr class="even">
<td><p>2012 년 6 월 13 일</p></td>
<td><p>ReFS 또는 FAT 볼륨에서 DFS 복제는 작업을 편집할? ReFS의 토론에 추가할 항목입니다.</p></td>
<td><p>고객 의견</p></td>
</tr>
<tr class="odd">
<td><p>2012 년 4 월 25 일</p></td>
<td><p>DFS 복제는 복제 NTFS 권한, 대체 데이터 스트림, 하드 링크 파일 및 재분석 지점 편집? DFS 복제에서 하드 링크를 처리 하는 방법을 명확 하 게 항목입니다.</p></td>
<td><p>잠재적인 혼동을 줄이기 위해</p></td>
</tr>
<tr class="even">
<td><p>2011 년 3 월 30 일</p></td>
<td><p>DFS 복제 수 복제 Outlook.pst 또는 Microsoft Office Access 데이터베이스 파일을 편집? DFS 복제를 사용 하 여.pst 파일에 액세스와 잠재적인 영향을 해결 하려면 항목입니다.</p>
<p>복제 성능 향상 수는 어떻게 추가?</p></td>
<td><p>이전 항목을 올바르게 표시 되지 않습니다.pst 또는 Access 파일 복제 DFS 복제 데이터베이스 손상 될 수 있습니다 하는 방법에 대 한 고객 질문입니다.</p></td>
</tr>
<tr class="odd">
<td><p>2011 년 1 월 26 일</p></td>
<td><p>어떻게 파일에서에서 복구할 수는 ConflictAndDeleted 추가 또는 기존 폴더?</p></td>
<td><p>고객 의견</p></td>
</tr>
<tr class="even">
<td><p>2010 년 10 월 20 일</p></td>
<td><p>어떻게 업그레이드 하거나 수 DFS 복제 멤버 추가?</p></td>
<td><p>고객 의견</p></td>
</tr>
</tbody>
</table>

