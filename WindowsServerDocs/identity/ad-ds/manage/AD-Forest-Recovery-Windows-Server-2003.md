---
title: AD 포리스트 복구-Windows Server 2003 복구
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: e2af1bfc295469d43e59593d69d4ba88f476e427
ms.sourcegitcommit: 21165734a0f37c4cd702c275e85c9e7c42d6b3cb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2019
ms.locfileid: "65034145"
---
# <a name="ad-forest-recovery---windows-server-2003-recovery"></a>AD 포리스트 복구-Windows Server 2003 복구

>적용 대상: Windows Server 2003

이 항목에서는 Windows Server 2003을 실행 하는 도메인 컨트롤러 (Dc)에 대 한 포리스트 복구 절차를 포함 합니다. 포리스트 복구를 위한 일반적인 프로세스는 Windows Server 2003 Dc와 다르지 않지만 다른 tools 인해 특정 프로시저 다를 수 있습니다. 예를 들어, 백업 및 Windows Server Backup 또는 Wbadmin.exe 이상인 Windows Server 2008을 실행 하는 Dc에 사용 되는 반면 Windows Server 2003 Dc를 실행 하는 Dc를 복원 하려면 Ntdsutil.exe는 사용할 수 있습니다.  
  
- [시스템 상태 데이터 백업](#backing-up-the-system-state-data)  
- [신뢰할 수 없는 복원을 수행합니다.](#performing-a-nonauthoritative-restore)  
- [DNS 서버 서비스 설치 및 구성](#install-and-configure-the-dns-server-service)

## <a name="backing-up-the-system-state-data"></a>시스템 상태 데이터 백업
Windows Server 2003을 실행 하는 DC의 현재 백업 작업을 위해 선택한 다른 데이터와 함께 시스템 상태 데이터를 백업 하려면 다음 절차를 따르십시오. Windows Server 2003 시스템 상태 데이터를 백업 하는 데 사용할 수 있는 Ntbackup 도구를 포함 합니다.  
  
멤버 자격이 **관리자** 또는 **Backup Operators**, 또는 이와 동등한 파일 및 폴더를 백업 하는 데 필요한 최소값입니다.   
  
시스템 상태 데이터를 테이프에 백업 되는 백업 프로그램 사용할 수 있는 사용 되지 않는 미디어 없음 임을 나타냅니다를 이동식 저장소를 사용 하는 것이 해야 합니다. 이 테이프는 풀에 추가 무료 미디어 백업을 사용할 수 있도록 합니다.  
  
만 로컬 컴퓨터에서 시스템 상태 데이터를 백업할 수 있습니다. 원격 컴퓨터 백업할 수 없습니다.  
  
### <a name="to-back-up-the-system-state-data-on-a-domain-controller-that-runs-windows-server-2003"></a>Windows Server 2003을 실행 하는 도메인 컨트롤러에서 시스템 상태 데이터를 백업 하려면  
  
1. 클릭 **시작**, 가리킨 **모든 프로그램**를 가리킵니다 **Accessories**, 가리킵니다 **시스템 도구**를 클릭 하 고 **백업** .  
2. 에 **시작** 페이지에서 클릭 **고급 모드**합니다.  
3. 에 **백업** 탭, 드라이브, 폴더 또는 백업 하려는 파일에 대 한 확인란을 선택 합니다.  
4. 선택 된 **시스템 상태** 확인란 합니다.  
5. 클릭 **백업을 시작**합니다.  
  
## <a name="performing-a-nonauthoritative-restore"></a>신뢰할 수 없는 복원을 수행합니다.  

Windows Server 2003을 실행 하는 DC의 신뢰할 수 없는 복원을 수행 하려면 다음 절차를 따르십시오. Windows Server 2003의 Active directory를 신뢰할 수 없는 복원을 수행 하 여 자동으로 SYSVOL의 신뢰할 수 없는 복원을 수행 합니다. 추가 단계가 필요 하지 않습니다.  
  
> [!NOTE]
> 또한 Windows Server 2003 운영 체제를 다시 설치 수 또는 컴퓨터를 도메인에 가입 되지 않을 수 있습니다 및 운영 체제의 설치 중 컴퓨터에 모든 이름을 지정할 수 있습니다. Active Directory를 설치 하지 마세요. 운영 체제를 다시 설치한 후 4 단계로 직접 이동 합니다.  
  
Windows Server 2003 도메인 컨트롤러 시스템 상태 데이터를 복원한에 복구 하기 전에 Dc에서 실행 중이 던 모든 소프트웨어 응용 프로그램 다시 설치 해야 합니다. AD DS 도메인의 첫 번째 DC도 복원 레지스트리 이기 때문에 두 시스템 상태 데이터의 일부가 됩니다. 모든 정보를 레지스트리에 저장 해야 하는 경우 및이 Dc에서 실행 중인 응용 프로그램을 설치한 경우이 점에 염두 해야 합니다.  
  
소프트웨어를 다시 설치 하는 데 필요한 시간을 절약 하려면 Dc에 설치 해야 하는 응용 프로그램 가상 DC 복제와 호환 되는 경우를 결정 합니다. 복제 된 가상 Dc에 설치 하는 데 필요한 노력과 시간을 줄이기 위해 복제 하기 전에 원본 DC에서 이러한 응용 프로그램을 설치할 수 있습니다.  
  
### <a name="to-perform-a-nonauthoritative-restore"></a>신뢰할 수 없는 복원을 수행 하려면
  
1. DC를 시작한 후 f8 키를 눌러에서 디렉터리 서비스 복원 모드 (DSRM) 컴퓨터를 다시 시작 합니다.  
2. 선택 **디렉터리 서비스 복원 모드 (Windows 도메인 컨트롤러에만 해당)** 합니다.  
3. 복원 모드로 시작 하려면 원하는 운영 체제를 선택 합니다.  
4. (수만 사용 하 여 로컬 컴퓨터 계정, 도메인 로그온 옵션 없음 사용할 수 있습니다)에 관리자로 로그온 합니다.  
5. 명령 프롬프트에서 입력 **ntbackup**, 한 다음 ENTER를 누릅니다.  
6. 에 **시작** 페이지에서 **고급 모드**를 선택한 후는 **복원 및 미디어 관리** 탭. (선택 하지 마세요 **복원 마법사**.)  
7. 적절 한 백업 파일에서 복원 하 고 확인을 선택 합니다 **시스템 디스크** 하 고 **시스템 상태** 확인란을 선택 합니다.  
8. **복원 시작**을 클릭합니다.  
9. 복원 작업이 완료 되 면 컴퓨터를 다시 시작 합니다.  
  
Windows Server 2003을 실행 하는 DC에서 SYSVOL의 신뢰할 수 있는 (기본 라고도) 복원을 수행 하려면 다음 절차를 따르십시오. 도메인에서 복원 되는 첫 번째 Windows Server 2003 DC에만이 절차를 수행 합니다.  
  
### <a name="to-perform-an-authoritative-restore-of-sysvol"></a>SYSVOL의 정식 복원을 수행 하려면  
  
1. 이전 절차의 1 ~ 8 단계를 수행 합니다.  
2. 에 **복원 확인** 대화 상자, 클릭 **고급**합니다.  
3. SYSVOL의 신뢰할 수 있는 복원 하는 경우를 수행 하려면 확인란을 선택 **복원 데이터 집합에 복제 하는 경우 모든 복제본에 대 한 기본 데이터와 복원 된 데이터 표시**합니다.  

   > [!NOTE]
   > 백업에는 기본 데이터 설정에 해당 하는 복원 된 데이터를 표시 합니다 **BurFlags** D4 다음 레지스트리 하위 키 아래에 있는 항목:  
   >   
   > **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NtFrs\Parameters\Cumulative Replica Sets\\** *GUID*  

4. 복원 작업이 완료 되 면 컴퓨터를 다시 시작 합니다.  
  
## <a name="install-and-configure-the-dns-server-service"></a>DNS 서버 서비스 설치 및 구성

백업에서 복원 하는 DC에서 Windows Server 2003을 실행 중인 경우에 DC를 네트워크에 연결 하지 않고 DNS 서버를 설치할 수 있습니다.  
  
### <a name="to-install-and-configure-the-dns-server-service"></a>DNS 서버 서비스 설치 및 구성 하려면  
  
1. Windows 구성 요소 마법사를 엽니다. 마법사를 열려면:  

   - **시작**, **제어판**, **프로그램 추가/제거**를 차례로 클릭합니다.  
   - 클릭 **Windows 구성 요소 추가/제거**합니다.  

2. **구성 요소**를 선택 합니다 **네트워킹 서비스** 확인란을 선택한 다음 클릭 **세부 정보**합니다.  
3. **네트워킹 서비스의 하위 구성 요소**를 선택 합니다 **도메인 이름 시스템 (DNS)** 확인란을 클릭 **확인**를 클릭 하 고 **다음**합니다.  
4. 메시지가 나타나면 **파일을 복사할**에 배포 파일의 전체 경로 입력 하 고 클릭 **확인**합니다.  

   설치 후 DNS 서버를 구성 하려면 다음 단계를 완료 합니다.  

5. 클릭 **시작**, 가리킨 **모든 프로그램**를 가리킨 **관리 도구**를 클릭 하 고 **DNS**.  
6. 중요 한 고장 하기 전에 DNS 서버에서 호스팅되는 동일한 DNS 도메인 이름에 대 한 DNS 영역을 만듭니다. 자세한 내용은 정방향 조회 영역을 추가 참조 ([https://go.microsoft.com/fwlink/?LinkId=74574](https://go.microsoft.com/fwlink/?LinkId=74574)).  
7. 중요 한 고장 전에 존재 했던 대로 DNS 데이터를 구성 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  

   - AD DS에 저장 될 DNS 영역을 구성 합니다. 자세한 내용은 참조 영역 종류 변경 ([https://go.microsoft.com/fwlink/?LinkId=74579](https://go.microsoft.com/fwlink/?LinkId=74579)).  
   - 보안 동적 업데이트를 허용 하도록 도메인 컨트롤러 로케이터 (DC 로케이터) 리소스 레코드에 대 한 권한이 있는 DNS 영역을 구성 합니다. 자세한 내용은 허용 보안 동적 업데이트만 참조 하세요. ([https://go.microsoft.com/fwlink/?LinkId=74580](https://go.microsoft.com/fwlink/?LinkId=74580)).  

8. 부모 DNS 영역에 위임 리소스 레코드 (이름 서버 (NS) 및 붙이기 호스트 (A) 리소스 레코드)이 DNS 서버에서 호스트 되는 자식 영역에 대 한이 포함 되어 있는지 확인 합니다. 자세한 내용은 영역 위임을 만들기를 참조 ([https://go.microsoft.com/fwlink/?LinkId=74562](https://go.microsoft.com/fwlink/?LinkId=74562)).  
9. DNS를 구성 하면 명령 프롬프트에서 다음 명령을 입력 하 고 enter 키를 눌러:  

   **net stop netlogon**

10. 다음 명령을 입력한 후 Enter 키를 누릅니다.  

   **net 시작 netlogon**

   > [!NOTE]
   > Net Logon은이 DC에 대 한 DNS에서 DC 로케이터 리소스 레코드를 등록 합니다. 자식 도메인의 서버에서 DNS 서버 서비스를 설치 하는 경우이 DC 즉시 해당 레코드를 등록할 수 없습니다. 즉, 복구 프로세스 및 해당 주 DNS 서버는 포리스트 루트 DNS 서버가 현재 격리 됩니다. DC 서비스 조회 오류를 방지 하려면 재해가 발생 하기 전에 있었던 것과 동일한 IP 주소를 사용 하 여이 컴퓨터를 구성 합니다.

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 - 필수 조건](AD-Forest-Recovery-Prerequisties.md)  
- [사용자 지정 포리스트 복구 계획을 고안 AD 포리스트 복구-](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD 포리스트 복구 문제를 식별 합니다.](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD 포리스트 Recovery-복구 하는 방법 결정](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD 포리스트 복구-초기 복구를 수행 합니다.](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)  
- [AD 포리스트 복구-질문과 대답](AD-Forest-Recovery-FAQ.md)  
- [AD 포리스트 복구-Multidomain 포리스트에 단일 도메인 복구](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [AD 포리스트 복구-Windows Server 2003 도메인 컨트롤러를 사용 하 여 포리스트 복구](AD-Forest-Recovery-Windows-Server-2003.md) 
