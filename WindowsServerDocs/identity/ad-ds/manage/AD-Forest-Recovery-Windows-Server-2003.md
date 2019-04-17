---
title: "광고 숲 복구-Windows Server 2003 복구"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: daebbc65b9864554fde839c3865f507ab787e6b6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---windows-server-2003-recovery"></a>광고 숲 복구-Windows Server 2003 복구

>적용 대상: Windows Server 2003

이 항목 숲 복구 Dc (도메인 컨트롤러) Windows Server 2003을 실행 하는 절차를 포함 합니다. 일반 숲 복구 과정은 Windows Server 2003 Dc로 더 다양 하지만 다양 한 도구도 인해 특정 절차 다를 수 있습니다. 예를 들어, Ntdsutil.exe 백업 및 Windows Server 백업 또는 Wbadmin.exe는 이상을 사용 하는 Windows Server 2008 실행 Dc 반면 Windows Server 2003 Dc 실행 Dc 복원를 사용할 수 있습니다.  
  
-   [시스템 상태 데이터를 백업](#Backing-up-the-System-State-data)  
  
-   [신뢰할 수 없는 복원을 수행](#Performing-a-nonauthoritative restore)  
  
-   [설치 및 구성 DNS 서버 서비스](#Install-and-configure-the-DNS-Server-service)  
  
  
## <a name="backing-up-the-system-state-data"></a>시스템 상태 데이터를 백업  
 다음 절차를 사용 하 여 Windows Server 2003을 실행 하는 DC의 현재 백업 작업에 대해 선택한 다른 데이터가 함께 시스템 상태 데이터를 백업 합니다. Windows Server 2003 시스템 상태 데이터를 백업 하는 데 사용할 수 있는 Ntbackup 도구가 포함 되어 있습니다.  
  
 회원 **관리자** 또는 **백업 운영자**, 해당 하는 파일 및 폴더를 백업 하는 데 필요한 최소 또는 합니다.   
  
 테이프로 시스템 상태 데이터를 백업 하는 경우, 백업 메시지가 나타나면 사용할 수 있는 미디어가 임을 이동식 저장소를 사용 해야 할 수 있습니다. 해당 백업에서 사용할 수 있도록 가능한 미디어 풀 테이프를 추가 합니다.  
  
 로컬 컴퓨터에서 시스템 상태만 백업할 수 있습니다. 원격 컴퓨터에서 백업할 수 없습니다.  
  
### <a name="to-back-up-the-system-state-data-on-a-domain-controller-that-runs-windows-server-2003"></a>Windows Server 2003을 실행 하는 도메인 컨트롤러에서 시스템 상태 데이터를 백업 하려면  
  
1.  클릭 **시작**, 가리킨 **모든 프로그램**, 가리킨 **액세서리**, 가리킨 **시스템 도구**, 클릭 한 다음 **백업**합니다.  
  
2.  에 **시작** 페이지, 클릭 **고급 모드**합니다.  
  
3.  에 **백업** 탭에서 드라이브, 폴더 또는 파일을 백업 하려면에 대 한 확인란을 선택 합니다.  
  
4.  선택는 **시스템 상태** 확인란을 선택 합니다.  
  
5.  클릭 **백업을 시작**합니다.  
  
  
## <a name="performing-a-nonauthoritative-restore"></a>신뢰할 수 없는 복원을 수행  
 다음 절차를 사용 하 여 권한 없는 Windows Server 2003을 실행 하는 DC 복원을 수행 합니다. Windows Server 2003에 대 한 Active Directory를 신뢰할 수 없는 복원을 수행 하 여 자동으로 SYSVOL 신뢰할 수 없는 복원을 수행 합니다. 없이 추가 단계는 필요 합니다.  
  
> [!NOTE]
>  또한 Windows Server 2003 운영 체제를 다시 설치 하거나 컴퓨터에서 도메인에 가입 하지 않을 수도 있습니다 및 운영 체제의 설치 하는 동안 컴퓨터에 이름을 지정할 수 있습니다. Active Directory를 설치 하지 않습니다. 운영 체제를 다시 설치한 후 직접 4 단계로 이동 합니다.  
  
 Windows Server 2003을 도메인 컨트롤러에서 시스템 상태 데이터 복원한도 복구 하기 전에 Dc에서 실행 중이 던는 소프트웨어 응용 프로그램을 다시 설치 해야 합니다. 복원 하는 도메인의 첫 번째 DC에서 AD DS 모두 시스템 상태 데이터의 일부 이므로 레지스트리도 복원 합니다. 이러한 Dc에서 실행 되는 모든 응용 프로그램을 지 원하는 경우 및 레지스트리에 저장 된 모든 정보를 지 원하는 경우이 지워진다는 사실에 유지 합니다.  
  
 소프트웨어를 다시 설치 하는 데 필요한 시간을 절약 하려면 Dc에 설치 하는 응용 프로그램 가상 DC 복제과 호환 되는지 확인 합니다. 이러한 응용 프로그램의 시간과 노력 복제 가상 Dc에 설치 하는 데 필요한 저장 하기 위해 복제 이전 DC 원본에 설치할 수 있습니다.  
  
#### <a name="to-perform-a-nonauthoritative-restore"></a>신뢰할 수 없는 복원을 수행 하려면  
  
1.  DC을 시작 하면 f8 키를 눌러에 DSRM 디렉터리 서비스 복원 모드 () 컴퓨터를 다시 시작 합니다.  
  
2.  선택 **디렉터리 서비스 복원 모드 (Windows 도메인 컨트롤러에만 해당)**합니다.  
  
3.  복원 모드로 시작할 운영 체제를 선택 합니다.  
  
4.  (수를 사용할 수 없음 도메인 로그온 옵션 로컬 컴퓨터 계정 사용) 관리자 권한으로 로그온 합니다.  
  
5.  명령 프롬프트에 입력 **ntbackup**, ENTER 키를 누릅니다.  
  
6.  에 **시작** 페이지, 클릭 **고급 모드**를 선택한 다음는 **미디어 복원 및 관리** 탭 (선택 하지 않으면 **복원 마법사**합니다.)  
  
7.  적절 한 백업에서 복원 하 않도록 파일은 **시스템 디스크** 및 **시스템 상태** 확인란을 선택 합니다.  
  
8.  클릭 **복원을 시작**합니다.  
  
9. 복원 작업이 완료 되 면 컴퓨터를 다시 시작 합니다.  
  
 다음 절차를 사용 하 여 Windows Server 2003을 실행 하는 dc sysvol 신뢰할 수 있는 (주 라고도 함) 복원을 수행 합니다. 도메인에서 복원 하는 첫 번째 Windows Server 2003 DC에만이 절차를 수행 합니다.  
  
### <a name="to-perform-an-authoritative-restore-of-sysvol"></a>Sysvol 정식 복원을 수행 하려면  
  
1.  이전 단계에서 1에서 8 사이의 단계를 수행 합니다.  
  
2.  에 **복원 확인** 대화 상자를 클릭 **고급**합니다.  
  
3.  Sysvol 신뢰할 수 있는 복원을 수행 하려면 확인란을 선택 **데이터 집합 복제 복원, 경우 모든 복제에 대 한 기본 데이터를 복원 된 데이터를 표시**합니다.  
  
    > [!NOTE]
    >  백업에 기본 데이터는로 설정으로 복원된 된 데이터가 표시는 **BurFlags** 다음 레지스트리 키에서 항목을 d 4:  
    >   
    >  **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NtFrs\Parameters\Cumulative 복제본 Sets\\***GUID*  
  
4.  복원 작업이 완료 되 면 컴퓨터를 다시 시작 합니다.  
  
 
## <a name="install-and-configure-the-dns-server-service"></a>설치 및 구성 DNS 서버 서비스  
 DC 백업에서 복원 하는 Windows Server 2003을 실행 중인 경우 DC 모든 네트워크에 연결 하지 않고 DNS 서버를 설치할 수 있습니다.  
  
### <a name="to-install-and-configure-the-dns-server-service"></a>설치 및 구성 DNS 서버 서비스  
  
1.  Windows 구성 요소 마법사를 엽니다. 마법사를 엽니다.  
  
    -   클릭 **시작**, 클릭 **제어판**을 차례로 클릭 하 고 **프로그램 추가 / 제거**합니다.  
  
    -   클릭 **Windows 구성 요소를 추가/제거**합니다.  
  
2.  **구성 요소**는 **네트워킹 서비스** 확인란을 선택한 다음 클릭 **세부 정보**합니다.  
  
3.  **네트워킹 서비스의 하위**는 **시스템 DNS (도메인 이름)** 확인란을 클릭 **확인**을 차례로 클릭 하 고 **다음**합니다.  
  
4.  라는 메시지가 나타나면에 **파일을 복사할**배포 파일의 전체 경로 입력 하 고 클릭 한 다음 **확인**합니다.  
  
     설치 후 다음 단계를 DNS 서버를 구성할 수 있습니다.  
  
5.  클릭 **시작**, 가리킨 **모든 프로그램**, 가리킨 **관리 도구**을 차례로 클릭 하 고 **DNS**합니다.  
  
6.  중요 한 오작동 전에 DNS 서버에서 된 호스트 하는 동일한 DNS 도메인 이름에 대 한 DNS 영역을 만듭니다. 자세한 내용은 참조 추가 앞 조회 영역이 ([https://go.microsoft.com/fwlink/?LinkId=74574](https://go.microsoft.com/fwlink/?LinkId=74574)).  
  
7.  중요 한 오작동 전의 DNS 데이터 구성 합니다. 예를 들어:  
  
    -   DNS AD DS에 저장 되는 영역을 구성 합니다. 자세한 내용은 참조 변경 영역 종류 ([https://go.microsoft.com/fwlink/?LinkId=74579](https://go.microsoft.com/fwlink/?LinkId=74579)).  
  
    -   DNS 도메인 컨트롤러 locator (DC Locator) 수 있도록 리소스 레코드 동적 보안 업데이트를 신뢰할 수 있는 영역을 구성 합니다. 자세한 내용은 참조 허용만 보안 동적 업데이트 ([https://go.microsoft.com/fwlink/?LinkId=74580](https://go.microsoft.com/fwlink/?LinkId=74580)).  
  
8.  부모 DNS 영역 위임 리소스 레코드 (이름을 서버 (NS) 및 리소스 붙이기 호스트 레코드)이 DNS 서버에서 호스트 하는 자녀 영역에 대 한 포함 되어 있는지 확인 합니다. 자세한 내용은 참조 만들기 영역 위임 ([https://go.microsoft.com/fwlink/?LinkId=74562](https://go.microsoft.com/fwlink/?LinkId=74562)).  
  
9. DNS 구성 하 고 나면 명령 프롬프트에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
     **Net 중지 netlogon**  
  
10. 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
     **Net 시작 netlogon**  
  
    > [!NOTE]
    >  Netlogon이 DC이에 대 한 dns에서 DC Locator 리소스 레코드를 등록 합니다. 자녀가 도메인에 있는 서버에서 DNS 서버 서비스를 설치 하는 경우이 DC 레코드를 등록할 수는 즉시 되지 않습니다. 주 DNS 서버 및 복구 과정의 일부는 숲 루트 DNS 서버 현재 격리 이기 때문입니다. 이 컴퓨터와 장애 DC 서비스 조회 오류 하지 않은 것 같은 IP 주소를 구성 합니다.

## <a name="next-steps"></a>다음 단계
-   [광고 숲 복구 필수](AD-Forest-Recovery-Prerequisties.md)  
-   [사용자 지정 숲 복구 계획 고안-광고 숲 복구](AD-Forest-Recovery-Devising-a-Plan.md)  
- [광고 숲 복구-문제 식별](AD-Forest-Recovery-Identify-the-Problem.md)
-   [광고 숲 복구-복구 하는 방법을 확인](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [광고 숲 복구-초기 복구](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)  
-   [광고 숲 복구-질문과 대답](AD-Forest-Recovery-FAQ.md)  
-   [광고 숲 복구-Multidomain 숲 내 단일 도메인 복구](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [광고 숲 복구-Windows Server 2003 도메인 컨트롤러 관련 숲 복구](AD-Forest-Recovery-Windows-Server-2003.md) 
