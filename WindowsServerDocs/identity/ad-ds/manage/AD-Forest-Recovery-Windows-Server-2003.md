---
title: AD 포리스트 복구-Windows Server 2003 복구
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: 43a2034cb707d4333abdce5f5b2b09d6c4b5a33a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390064"
---
# <a name="ad-forest-recovery---windows-server-2003-recovery"></a>AD 포리스트 복구-Windows Server 2003 복구

>적용 대상: Windows Server 2003

이 항목에는 Windows Server 2003를 실행 하는 Dc (도메인 컨트롤러)의 포리스트 복구 절차가 포함 되어 있습니다. 포리스트 복구에 대 한 일반적인 프로세스는 Windows Server 2003 Dc와 다르지만 다른 도구로 인해 특정 절차가 달라질 수 있습니다. 예를 들어 Ntdsutil.exe를 사용 하 여 Windows Server 2003 Dc를 실행 하는 Dc를 백업 및 복원할 수 있습니다. 반면에 Windows Server 2008 이상을 실행 하는 Dc에는 Windows Server 백업 또는 stsadm.exe가 사용 됩니다.  
  
- [시스템 상태 데이터 백업](#backing-up-the-system-state-data)  
- [비정식 복원 수행](#performing-a-nonauthoritative-restore)  
- [DNS 서버 서비스 설치 및 구성](#install-and-configure-the-dns-server-service)

## <a name="backing-up-the-system-state-data"></a>시스템 상태 데이터 백업
다음 절차를 사용 하 여 Windows Server 2003를 실행 하는 DC의 현재 백업 작업을 위해 선택한 다른 데이터와 함께 시스템 상태 데이터를 백업 합니다. Windows Server 2003에는 시스템 상태 데이터를 백업 하는 데 사용할 수 있는 Ntbackup 도구가 포함 되어 있습니다.  
  
파일과 폴더를 백업 하려면 최소한 **Administrators** 또는 **Backup Operators**또는 이와 동등한 멤버 자격이 필요 합니다.   
  
시스템 상태 데이터를 테이프에 백업 하는 경우 백업 프로그램에서 사용 가능한 미디어를 사용 하지 않는 것으로 표시 되 면 이동식 저장소를 사용 해야 할 수 있습니다. 그러면 백업에서 사용할 수 있도록 사용 가능한 미디어 풀에 테이프가 추가 됩니다.  
  
로컬 컴퓨터의 시스템 상태 데이터만 백업할 수 있습니다. 원격 컴퓨터에서 백업할 수 없습니다.  
  
### <a name="to-back-up-the-system-state-data-on-a-domain-controller-that-runs-windows-server-2003"></a>Windows Server 2003를 실행 하는 도메인 컨트롤러에서 시스템 상태 데이터를 백업 하려면  
  
1. **시작**을 클릭 하 고 **모든 프로그램**, **보조 프로그램**, **시스템 도구**를 차례로 가리킨 다음 **백업**을 클릭 합니다.  
2. **시작** 페이지에서 **고급 모드**를 클릭 합니다.  
3. **백업** 탭에서 백업 하려는 드라이브, 폴더 또는 파일의 확인란을 선택 합니다.  
4. **시스템 상태** 확인란을 선택 합니다.  
5. **백업 시작**을 클릭 합니다.  
  
## <a name="performing-a-nonauthoritative-restore"></a>비정식 복원 수행  

다음 절차를 사용 하 여 Windows Server 2003를 실행 하는 DC를 신뢰할 수 없는 복원 작업을 수행할 수 있습니다. Windows Server 2003의 Active Directory에 대 한 신뢰할 수 없는 복원을 수행 하 여 SYSVOL의 비정식 복원을 자동으로 수행 합니다. 추가 단계가 필요 하지 않습니다.  
  
> [!NOTE]
> Windows Server 2003 운영 체제도 다시 설치 하는 경우 컴퓨터를 도메인에 가입 시킬 수도 있고 그렇지 않을 수도 있으며, 운영 체제를 설치 하는 동안 컴퓨터에 이름을 지정할 수도 있습니다. Active Directory를 설치 하지 마십시오. 운영 체제를 다시 설치한 후 4 단계로 직접 이동 합니다.  
  
시스템 상태 데이터만 복원한 Windows Server 2003 도메인 컨트롤러에서 복구 하기 전에 Dc에서 실행 중인 모든 소프트웨어 응용 프로그램을 다시 설치 해야 합니다. 도메인의 첫 번째 DC에서 AD DS 복원 하는 것은 모두 시스템 상태 데이터의 일부 이기 때문에 레지스트리도 복원 합니다. 이러한 Dc에서 실행 중인 응용 프로그램이 있고 레지스트리에 저장 된 정보가 있는 경우이 점을 염두에 두어야 합니다.  
  
소프트웨어를 다시 설치 하는 데 필요한 시간을 절약 하려면 Dc에 설치 해야 하는 응용 프로그램이 가상 DC 복제와 호환 되는지 확인 합니다. 복제 된 가상 Dc에 이러한 응용 프로그램을 설치 하는 데 필요한 시간과 노력을 절약 하기 위해 복제 전에 원본 DC에 이러한 응용 프로그램을 설치할 수 있습니다.  
  
### <a name="to-perform-a-nonauthoritative-restore"></a>비정식 복원 수행
  
1. DC를 시작한 후 F8 키를 눌러 DSRM (디렉터리 서비스 복원 모드)에서 컴퓨터를 다시 시작 합니다.  
2. **디렉터리 서비스 복원 모드 (Windows 도메인 컨트롤러만)** 를 선택 합니다.  
3. 복원 모드에서 시작 하려는 운영 체제를 선택 합니다.  
4. 관리자로 로그온 합니다. 로컬 컴퓨터 계정만 사용할 수 있으며 도메인 로그온 옵션은 사용할 수 없습니다.  
5. 명령 프롬프트에서 **ntbackup**을 입력 한 다음 enter 키를 누릅니다.  
6. **시작** 페이지에서 **고급 모드**를 클릭 한 다음 **미디어 복원 및 관리** 탭을 선택 합니다. **복원 마법사**를 선택 하지 마십시오.  
7. 복원할 적절 한 백업 파일을 선택 하 고 **시스템 디스크** 및 **시스템 상태** 확인란이 선택 되었는지 확인 합니다.  
8. **복원 시작**을 클릭합니다.  
9. 복원 작업이 완료 되 면 컴퓨터를 다시 시작 합니다.  
  
다음 절차를 사용 하 여 Windows Server 2003를 실행 하는 DC에서 SYSVOL의 신뢰할 수 있는 (기본이 라고도 함) 복원을 수행할 수 있습니다. 도메인에 복원 된 첫 번째 Windows Server 2003 DC 에서만이 절차를 수행 합니다.  
  
### <a name="to-perform-an-authoritative-restore-of-sysvol"></a>SYSVOL의 신뢰할 수 있는 복원을 수행 하려면  
  
1. 이전 절차의 1 ~ 8 단계를 수행 합니다.  
2. **복원 확인** 대화 상자에서 **고급**을 클릭 합니다.  
3. SYSVOL의 정식 복원을 수행 하려면 **복제 된 데이터 집합을 복원할 때 확인란을 선택 하 고 복원 된 데이터를 모든 복제본의 주 데이터로 표시**합니다.  

   > [!NOTE]
   > 복원 된 데이터를 백업의 주 데이터로 표시 하는 것은 다음 레지스트리 하위 키 아래에서 **BurFlags** 항목을 D4로 설정 하는 것과 같습니다.  
   >   
   > **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NtFrs\Parameters\Cumulative 복제본 집합 @ no__t-1** *GUID*  

4. 복원 작업이 완료 되 면 컴퓨터를 다시 시작 합니다.  
  
## <a name="install-and-configure-the-dns-server-service"></a>DNS 서버 서비스 설치 및 구성

백업에서 복원한 DC가 Windows Server 2003를 실행 하는 경우 DC를 네트워크에 연결 하지 않고 DNS 서버를 설치할 수 있습니다.  
  
### <a name="to-install-and-configure-the-dns-server-service"></a>DNS 서버 서비스를 설치 및 구성 하려면  
  
1. Windows 구성 요소 마법사를 엽니다. 마법사를 열려면 다음을 수행 합니다.  

   - **시작**, **제어판**, **프로그램 추가/제거**를 차례로 클릭합니다.  
   - **Windows 구성 요소 추가/제거**를 클릭 합니다.  

2. **구성 요소**에서 **네트워킹 서비스** 확인란을 선택한 다음 **세부 정보**를 클릭 합니다.  
3. **네트워킹 서비스의 하위 구성 요소**에서 **DNS (Domain Name System)** 확인란을 선택 하 고 **확인**을 클릭 한 후 **다음**을 클릭 합니다.  
4. 메시지가 표시 되 면 **파일 복사**에서 배포 파일의 전체 경로를 입력 한 다음 **확인**을 클릭 합니다.  

   설치 후 다음 단계를 수행 하 여 DNS 서버를 구성 합니다.  

5. **시작**을 클릭 하 고 **모든 프로그램**, **관리 도구**를 차례로 가리킨 다음 **DNS**를 클릭 합니다.  
6. 중요 한 오작동 전에 DNS 서버에 호스트 된 동일한 DNS 도메인 이름에 대 한 DNS 영역을 만듭니다. 자세한 내용은 전방 조회 영역 추가 ([https://go.microsoft.com/fwlink/?LinkId=74574](https://go.microsoft.com/fwlink/?LinkId=74574))를 참조 하세요.  
7. 중요 한 오작동 이전의 DNS 데이터를 구성 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  

   - AD DS에 저장할 DNS 영역을 구성 합니다. 자세한 내용은 영역 유형 변경 ([https://go.microsoft.com/fwlink/?LinkId=74579](https://go.microsoft.com/fwlink/?LinkId=74579))을 참조 하세요.  
   - 도메인 컨트롤러 로케이터 (DC 로케이터) 리소스 레코드에 대 한 권한이 있는 DNS 영역을 구성 하 여 보안 동적 업데이트를 허용 합니다. 자세한 내용은 보안 동적 업데이트만 허용 ([https://go.microsoft.com/fwlink/?LinkId=74580](https://go.microsoft.com/fwlink/?LinkId=74580))을 참조 하세요.  

8. 부모 DNS 영역에이 DNS 서버에서 호스트 되는 자식 영역에 대 한 위임 리소스 레코드 (이름 서버 (NS) 및 glue host (A) 리소스 레코드)가 포함 되어 있는지 확인 합니다. 자세한 내용은 영역 위임 만들기 ([https://go.microsoft.com/fwlink/?LinkId=74562](https://go.microsoft.com/fwlink/?LinkId=74562))를 참조 하세요.  
9. DNS를 구성한 후 명령 프롬프트에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  

   **net stop netlogon**

10. 다음 명령을 입력한 후 Enter 키를 누릅니다.  

    **net start netlogon**

    > [!NOTE]
    > Net Logon은 dc 로케이터 리소스 레코드를이 DC에 대 한 DNS에 등록 합니다. 자식 도메인의 서버에 DNS 서버 서비스를 설치 하는 경우이 DC는 해당 레코드를 즉시 등록할 수 없습니다. 이는 현재 복구 프로세스의 일부로 격리 되어 있으며 해당 주 DNS 서버가 포리스트 루트 DNS 서버 이기 때문입니다. DC 서비스 조회 실패를 방지 하기 위해 재해 전과 동일한 IP 주소를 사용 하 여이 컴퓨터를 구성 합니다.

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 - 필수 조건](AD-Forest-Recovery-Prerequisties.md)  
- [AD 포리스트 복구-사용자 지정 포리스트 복구 계획 고안](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD 포리스트 복구-문제 식별](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD 포리스트 복구-복구 방법을 결정 합니다.](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD 포리스트 복구-초기 복구 수행](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)  
- [AD 포리스트 복구-질문과 대답](AD-Forest-Recovery-FAQ.md)  
- [AD 포리스트 복구-다중 도메인 포리스트 내에서 단일 도메인 복구](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [AD 포리스트 복구-Windows Server 2003 도메인 컨트롤러를 사용 하 여 포리스트 복구](AD-Forest-Recovery-Windows-Server-2003.md) 
