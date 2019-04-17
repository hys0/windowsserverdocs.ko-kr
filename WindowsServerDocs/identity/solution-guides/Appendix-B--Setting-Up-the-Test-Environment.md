---
ms.assetid: 82918181-525d-4e93-af96-957dac6aedb6
title: "부록 B 설정 테스트 환경"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: deb08b0663e5f349df7cce51ddabd4aae7f624c5
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="appendix-b-setting-up-the-test-environment"></a>부록 b: 설정 테스트 환경

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 실습 동적 액세스 제어 테스트를 구축 하는 단계에 설명 합니다. 지침은 다양 한 구성 요소가 있는 종속성 있기 때문에 순서 대로 따라야 할 것입니다.  
  
## <a name="prerequisites"></a>필수  
**하드웨어 및 소프트웨어 요구 사항**  
  
테스트 랩 설정에 대 한 요구 사항:  
  
-   Windows Server 2008 R2 s p 1과 Hyper-v를 사용 하 여 실행 호스트 서버  
  
-   Windows Server 2012 ISO의 복사본을  
  
-   Windows 8 ISO의 복사본을  
  
-   Microsoft Office 2010  
  
-   Microsoft Exchange Server 2003 이상 실행 하는 서버  
  
다음 동적 액세스 제어 시나리오를 테스트 가상 컴퓨터 빌드 해야 합니다.  
  
-   D c 1 (도메인 컨트롤러)  
  
-   D c 2 (도메인 컨트롤러)  
  
-   파일 1 (파일 서버 및 Active Directory 권한 관리 서비스)  
  
-   S r v 1 (POP3 및 SMTP 서버)  
  
-   CLIENT1 (Microsoft outlook 클라이언트 컴퓨터)  
  
가상 컴퓨터에 대 한 암호는 다음과 같은 해야 합니다.  
  
-   BUILTIN\Administrator:pass@word1  
  
-   Contoso\Administrator:pass@word1  
  
-   다른 계정 다음과 같습니다.pass@word1  
  
## <a name="build-the-test-lab-virtual-machines"></a>테스트 랩 가상 컴퓨터 빌드  
  
### <a name="install-the-hyper-v-role"></a>Hyper-v 역할 설치  
Hyper-v 역할 컴퓨터에 설치 하는 Windows Server 2008 R2 s p 1을 사용 하 여 실행 해야 합니다.  
  
##### <a name="to-install-the-hyper-v-role"></a>Hyper-v 역할을 설치 하려면  
  
1.  클릭 **시작**, 다음 서버 관리를 클릭 하 고 있습니다.  
  
2.  서버 관리자 주 창의 역할 요약 영역의 클릭 **역할 추가**합니다.  
  
3.  에 **서버 역할 선택** 페이지, 클릭 **Hyper-v**합니다.  
  
4.  에 **가상 네트워크 만들기** 페이지에서 해당 네트워크 연결이 가상 컴퓨터를 사용할 수 있도록 하나 이상의 네트워크 어댑터를 클릭 합니다.  
  
5.  에 **설치 선택 확인** 페이지, 클릭 **설치**합니다.  
  
6.  설치를 완료 하려면 컴퓨터를 다시 시작 해야 합니다. 클릭 **닫기** 마법사를 완료 한 클릭 한 다음 **예** 컴퓨터를 다시 시작 합니다.  
  
7.  컴퓨터를 다시 시작한 후 역할을 설치 하는 데 사용한 동일한 계정으로 로그인 합니다. 구성 마법사 다시 시작 설치를 완료 한 후 클릭 **닫기** 마법사를 완료 합니다.  
  
### <a name="create-an-internal-virtual-network"></a>내부 가상 네트워크 만들기  
이제 내부 ID_AD_Network 이라는 가상 네트워크를 만듭니다.  
  
##### <a name="to-create-a-virtual-network"></a>가상 네트워크를 만들려면  
  
1.  Hyper-v 관리자를 엽니다.  
  
2.  **작업** 메뉴를 클릭 **가상 네트워크 관리자**합니다.  
  
3.  아래에서 **만들기 가상 네트워크**선택 하 고, 여 **내부**합니다.  
  
4.  클릭 **추가**합니다. **새 가상 네트워크** 페이지가 나타납니다.  
  
5.  입력 **ID_AD_Network** 의 새 네트워크 이름으로 합니다. 다른 속성 검토 하 고 필요한 경우 수정 합니다.  
  
6.  클릭 **확인** 가상 네트워크와 만들거나 가상 네트워크 관리자 닫거나 클릭 **적용** 가상 네트워크 만들고 가상 네트워크 관리자를 사용 하 여 계속 합니다.  
  
### <a name="BKMK_Build"></a>빌드 도메인 컨트롤러  
빌드 가상 컴퓨터 도메인 컨트롤러 d c (1)을 사용할 수 있습니다. Windows Server 2012 ISO를 사용 하 여 가상 컴퓨터에 설치 하 고 이름을 d c 1.  
  
##### <a name="to-install-active-directory-domain-services"></a>Active Directory 도메인 서비스를 설치 하려면  
  
1.  가상 컴퓨터의 ID_AD_Network에 연결 합니다. 에 로그인 하 여 d c 1 관리자 권한으로 암호로 ** pass@word1 **합니다.  
  
2.  서버 관리자 클릭 **관리**을 차례로 클릭 하 고 **역할 추가 및 기능**합니다.  
  
3.  에 **시작 하기 전에** 페이지, 클릭 **다음**합니다.  
  
4.  에 **설치 유형을 선택** 페이지, 클릭 **역할 또는 기능 기반 설치**을 차례로 클릭 하 고 **다음**합니다.  
  
5.  에 **선택 대상 서버** 페이지, 클릭 **다음**합니다.  
  
6.  에 **서버 역할 선택** 페이지, 클릭 **Active Directory 도메인 서비스**합니다. 에 **역할 추가 및 기능 마법사** 대화 상자를 클릭 **기능 추가**, 클릭 한 다음 **다음**합니다.  
  
7.  에 **기능 선택** 페이지, 클릭 **다음**합니다.  
  
8.  에 **Active Directory 도메인 서비스** 페이지에서 정보를 검토 한 다음 클릭 **다음**합니다.  
  
9. 에 **설치 선택을 확인** 페이지, 클릭 **설치**합니다. 결과 페이지에서 기능 설치 진행률 표시줄 역할 설치 되어 있는지를 나타냅니다.  
  
10. 에 **결과** 페이지에서 있는지 설치 되었는지 확인 한 클릭 **닫기**합니다. 서버 관리자에서 옆에 느낌표가 화면 오른쪽 위 모서리에 있는 경고 아이콘을 클릭 **관리**합니다. 작업 목록을 클릭는 **도메인 컨트롤러이 서버 홍보** 링크입니다.  
  
11. 에 **배포 구성** 페이지, 클릭 **새 숲 추가**, 루트 도메인의 이름을 입력 **contoso.com**을 차례로 클릭 하 고 **다음**합니다.  
  
12. 에 **도메인 컨트롤러 옵션** 페이지, Windows Server 2012와 도메인 및 숲 기능 수준을 선택, DSRM 암호 지정 ** pass@word1 **을 차례로 클릭 하 고 **다음**합니다.  
  
13. 에 **DNS 옵션** 페이지, 클릭 **다음**합니다.  
  
14. 에 **추가 옵션** 페이지, 클릭 **다음**합니다.  
  
15. 에 **경로** 페이지, Active Directory 데이터베이스, 로그 파일과 SYSVOL 폴더의 위치를 입력 (또는 기본 위치에 동의)을 차례로 클릭 하 고 **다음**합니다.  
  
16. 에 **리뷰 옵션** 페이지 선택 사항을 확인 하 고 클릭 한 다음 **다음**합니다.  
  
17. 에 **필수 확인** 페이지에서 확인 필수 유효성 검사를 완료 한 후 클릭 **설치**합니다.  
  
18. 에 **결과** 페이지 서버 성공적으로 도메인 컨트롤러도 구성 되어 있는지 확인 한 다음 클릭 **닫기**합니다.  
  
19. 서버 AD DS 설치를 완료 하려면 다시 시작 합니다. (기본적으로이 자동으로 정품 인증 됩니다.)  
  
Active Directory 관리 센터를 사용 하 여 다음 사용자에 게 만듭니다.  
  
##### <a name="create-users-and-groups-on-dc1"></a>D c 1에 사용자 및 그룹 만들기  
  
1.  관리자 권한으로 contoso.com에 로그인 합니다. 관리 센터 Active Directory를 실행 합니다.  
  
2.  다음과 같은 보안 그룹 만듭니다.  
  
    |그룹 이름|메일 주소|  
    |--------------|-----------------|  
    |FinanceAdmin|financeadmin@contoso.com|  
    |FinanceException|financeexception@contoso.com|  
  
3.  다음과 같은 구성 단위를 만듭니다.  
  
    |OU 이름|컴퓨터|  
    |-----------|-------------|  
    |FileServerOU|파일 1|  
  
4.  다음 사용자 지정 된 특성으로 만듭니다.  
  
    |사용자|사용자 이름|메일 주소|성|그룹|국가/지역|  
    |--------|------------|-----------------|--------------|---------|-------------------|  
    |Myriam Delesalle|MDelesalle|MDelesalle@contoso.com|금융||미국|  
    |남궁익선|MReid|MReid@contoso.com|금융|FinanceAdmin|미국|  
    |Esther Valle|EValle|EValle@contoso.com|작업|FinanceException|미국|  
    |Maira Wenzel|MWenzel|MWenzel@contoso.com|시간||미국|  
    |Jeff 낮은|JLow|JLow@contoso.com|시간||미국|  
    |RMS 서버|rms|rms@contoso.com||||  
  
    For more information about creating security groups, see [Create a New Group](https://technet.microsoft.com/library/dd861305.aspx) on the Windows Server website.  
  
##### <a name="to-create-a-group-policy-object"></a>그룹 정책 개체를 만들려면  
  
1.  커서를 화면 오른쪽 위 모서리에서 및 검색 아이콘을 클릭 합니다. 검색 상자에 입력 **그룹 정책 관리**를 클릭 하 고 **그룹 정책 관리**합니다.  
  
2.  확장 **숲: contoso.com**, 다음를 확장 하 고 **도메인**로 이동 **contoso.com**, 확장 **(contoso.com)**를 선택한 다음 **FileServerOU**합니다. 마우스 오른쪽 단추로 클릭 **GPO이이 도메인에 있는 만들고 여기에 연결**
  
3.  와 같은 gpo 설명 이름을 입력 **FlexibleAccessGPO**을 차례로 클릭 하 고 **확인**합니다.  
  
##### <a name="to-enable-dynamic-access-control-for-contosocom"></a>Contoso.com에 대 한 동적 액세스 제어를 사용 하도록 설정 하려면  
  
1.  그룹 정책 관리 콘솔 열을 클릭 **contoso.com**, 다음 두 번 클릭 하 고 **도메인 컨트롤러**합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **기본 도메인 컨트롤러 정책**를 선택 하 고 **편집**합니다.  
  
3.  그룹 정책 편집기 관리 창에서 두 번 클릭 **컴퓨터 구성**를 두 번 클릭 **정책**, 두 번 클릭 **관리 템플릿**, 두 번 클릭 **시스템**, 다음 두 번 클릭 하 고 **KDC**합니다.  
  
4.  두 번 클릭 **KDC 클레임, 복합 인증 및 Kerberos armoring에 대 한 지원은** 옆에 있는 옵션을 선택 하 고 **사용**합니다. 중앙 액세스 정책을 사용 하 여이 설정을 사용 해야 합니다.  
  
5.  관리자 명령 프롬프트를 열고 다음 명령을 실행 합니다.  
  
    ```  
    gpupdate /force  
    ```  
  
### <a name="BKMK_FS1"></a>빌드 파일 서버 및 광고 RMS 서버 (파일 1)  
  
1.  Windows Server 2012 ISO에서 가상 컴퓨터 파일 1 이름의 빌드입니다.  
  
2.  가상 컴퓨터의 ID_AD_Network에 연결 합니다.  
  
3.  가상 컴퓨터 contoso.com 도메인에 가입 하 고 다음으로 암호를 사용 하 여 contoso\administrator 파일 1에 로그인 ** pass@word1 **합니다.  
  
#### <a name="install-file-services-resource-manager"></a>파일 서비스 리소스 관리자 설치  
  
###### <a name="to-install-the-file-services-role-and-the-file-server-resource-manager"></a>파일을 설치 하 고 파일 서버 리소스 관리자 역할 서비스  
  
1.  서버 관리자 클릭 **역할 추가 및 기능**합니다.  
  
2.  에 **시작 하기 전에** 페이지, 클릭 **다음**합니다.  
  
3.  에 **설치 유형을 선택** 페이지, 클릭 **다음**합니다.  
  
4.  에 **선택 대상 서버** 페이지, 클릭 **다음**합니다.  
  
5.  에 **서버 역할 선택** 페이지에서 확장 **파일 및 저장소 서비스**, 옆의 확인란을 선택 **파일과 iSCSI 서비스**를 확장 하 고 선택 **파일 서버 리소스 관리자**합니다.  
  
    역할 추가 및 기능 마법사에서 클릭 **기능 추가**을 차례로 클릭 하 고 **다음**합니다.  
  
6.  에 **기능 선택** 페이지, 클릭 **다음**합니다.  
  
7.  에 **설치 선택을 확인** 페이지, 클릭 **설치**합니다.  
  
8.  에 **설치 진행률** 페이지, 클릭 **닫기**합니다.  
  
#### <a name="install-the-microsoft-office-filter-packs-on-the-file-server"></a>파일 서버에 Microsoft Office 필터 팩 설치  
넓은 배열 기본적으로 제공 하는 것 보다 Office 파일에 대 한 IFilters 수 있도록 Windows Server 2012에서 Microsoft Office 필터 팩을 설치 해야 합니다.  Windows Server 2012 기본적으로 설치, Microsoft Office 파일에 대 한 모든 Ifilter 없는 및 파일 분류 인프라 Ifilter 콘텐츠 분석을 사용 하 여 합니다.  
  
To download and install the IFilters, see [Microsoft Office 2010 Filter Packs](https://go.microsoft.com/fwlink/?LinkID=234122).  
  
#### <a name="configure-email-notifications-on-file1"></a>메일 알림 파일 1에서 구성  
할당량과 파일 화면을 만들 때 할당량 한도 도달 하거나 차단 된 된 파일을 저장 했습니다 후 사용자에 게 메일 알림 보내기 옵션이 있습니다. 정기적으로 관리자에 게 알리려면 특정 할당량 및 파일 이벤트 차단 하려는 경우 기본 받는 구성할 수 있습니다. 이러한 알림을 보내도록 SMTP 서버 메일 메시지를 전달 하기 위해 사용 하도록 지정 해야 합니다.  
  
###### <a name="to-configure-email-options-in-file-server-resource-manager"></a>메일 옵션 파일 서버 리소스 관리자 구성 하려면  
  
1.  파일 서버 리소스 관리자를 엽니다. 파일 서버 리소스 관리자를 열을 클릭 **시작**, 입력 **파일 서버 리소스 관리자**을 차례로 클릭 하 고 **파일 서버 리소스 관리자**합니다.  
  
2.  파일 서버 리소스 관리자 인터페이스에서 마우스 오른쪽 단추로 클릭 **파일 서버 리소스 관리자**을 차례로 클릭 하 고 **옵션 구성**합니다. **파일 서버 리소스 관리자 옵션** 대화 상자를 엽니다.  
  
3.  에 **메일 알림** 탭 SMTP 서버 이름 또는 IP 주소에서 호스트 이름이 나 SMTP 서버를 전달할의 IP 주소를 입력 메일 알림 합니다.  
  
4.  If you want to routinely notify certain administrators of quota or file screening events, under **Default administrator recipients**, type each email address such as fileadmin@contoso.com. Use the format account@domain, and use semicolons to separate multiple accounts.  
  
#### <a name="create-groups-on-file1"></a>파일 1에 그룹 만들기  
  
###### <a name="to-create-security-groups-on-file1"></a>그룹을 만들려면 보안 파일 1에서  
  
1.  파일 1으로 contoso\administrator 암호로 로그인: ** pass@word1 **합니다.  
  
2.  NT AUTHORITY\Authenticated 사용자가 추가 **WinRMRemoteWMIUsers__** 그룹입니다.  
  
#### <a name="create-files-and-folders-on-file1"></a>파일 및 폴더의 파일 1 만들기  
  
1.  파일 1에서 새 NTFS 볼륨 만들고 다음 폴더를 만듭니다: D:\Finance 문서 합니다.  
  
2.  지정 된 정보 사용 다음 파일을 만듭니다.  
  
    -   **재무 Memo.docx**: 일부 재무 문서에서 텍스트 관련 된 추가 합니다. 예를 들어 ' 비즈니스 규칙 금융 문서에 액세스할 수 있는 사람에 대 한 변경 했습니다. 금융 문서 이제만 액세스 FinanceExpert 그룹의 회원 합니다. 다른 부서 또는 그룹에 대 한 액세스 권한이.' 이 변경에 맞게 운영 환경을 구현 하기 전에 영향을 평가 해야 합니다. 이 문서에 모든 페이지에 바닥글과 CONTOSO 기밀 있는지 확인 합니다.  
  
    -   **Hire.docx 승인을 대 한 요청**: 지원자 정보를 수집 하는이 문서의 양식 만듭니다. 문서에서 다음 필드 있어야: **지원자 이름, 1, 직위, 제안 Salary, 시작 날짜, 관리자 이름, 성**합니다. 하기 위한 양식의 있는 문서에서 섹션을 추가 **관리자 서명이 승인 Salary 하며의 제공**, 및 **제공 상태**합니다.   
        사용 하도록 설정 문서 권한 관리를 확인 합니다.  
  
    -   **단어 Document1.docx**:이 문서에 테스트 콘텐츠를 추가 합니다.  
  
    -   **단어 Document2.docx**: 추가이 문서의 콘텐츠를 테스트 합니다.  
  
    -   **Workbook1.xlsx**  
  
    -   **Workbook2.xlsx**  
  
    -   일반 표현 라는 데스크톱에서 폴더를 만듭니다. 라는 폴더에서 텍스트 문서를 작성 **RegEx SSN**합니다. 해당 파일에 다음과 같은 내용을 입력 하 고 저장 하 고 파일을 닫습니다.   
        ^(?! 000)([0-7]\d{2}|7([0-7]\d|7[012])) ([-]?) (?! 00) \d\d\3 (건가요? \d {4} $ 0000)  
  
3.  금융 문서로 D:\Finance 문서 폴더를 공유 하 고 모든 사용자의 읽기 및 공유에 대 한 액세스를 쓸 수 있도록 합니다.  
  
> [!NOTE]  
> 중앙 액세스 정책은 시스템에서 기본적으로 활성화 되지 또는 부팅 볼륨 c: 합니다.  
  
#### <a name="BKMK_CS1"></a>설치 Active Directory 권한 관리 서비스  
Active Directory 권한 관리 서비스 (AD RMS) 서버 관리자를 통해 모든 필요한 기능을 추가 합니다. 기본값을 모두 선택 합니다.  
  
###### <a name="to-install-active-directory-rights-management-services"></a>Active Directory 권한 관리 서비스를 설치 하려면  
  
1.  파일은 1에 CONTOSO\Administrator 도메인 관리자 그룹의 회원으로 로그인 합니다.  
  
    > [!IMPORTANT]  
    > AD RMS 서버 역할 설치 프로그램을 설치 하려면 (이 경우 CONTOSO\Administrator)에서 계정 둘 다의 로컬 관리자가 그룹 AD RMS 설치할 서버 컴퓨터에서 등록 뿐 아니라 Active Directory에 Enterprise 관리자 그룹의 회원 부여 해야 합니다.  
  
2.  서버 관리자 클릭 **역할 추가 및 기능**합니다. 역할 추가 및 기능 마법사 나타납니다.  
  
3.  에 **시작 하기 전에** 화면에서 클릭 **다음**합니다.  
  
4.  에 **설치 유형을 선택** 화면을 클릭 **역할/기능을 기반으로 설치**을 차례로 클릭 하 고 **다음**합니다.  
  
5.  에 **서버 대상 선택** 화면에서 클릭 **다음**합니다.  
  
6.  에 **서버 역할 선택** 화면에서 옆에 있는 상자를 선택한 후 **Active Directory 권한 관리 서비스**, 클릭 한 다음 **다음**합니다.  
  
7.  에 **Active Directory 권한 관리 서비스에 필요한 기능을 추가? ** 대화 상자를 클릭 **기능 추가**합니다.  
  
8.  에 **서버 역할 선택** 화면에서 클릭 **다음**합니다.  
  
9. 에 **설치 선택 기능** 화면에서 클릭 **다음**합니다.  
  
10. 에 **Active Directory 권한 관리 서비스** 화면에서 다음을 클릭 합니다.  
  
11. 에 **역할 서비스 선택** 화면에서 클릭 **다음**합니다.  
  
12. 에 **웹 역할 IIS ()** 화면에서 클릭 **다음**합니다.  
  
13. 에 **역할 서비스 선택** 화면에서 클릭 **다음**합니다.  
  
14. 에 **설치 선택 확인** 화면에서 클릭 **설치**합니다.  
  
15. 에 설치가 완료 된 후는 **설치 진행률** 화면에서 클릭 **수행 추가 구성**합니다. 광고 RMS 구성 마법사가 나타납니다.  
  
16. 에 **AD RMS** 화면에서 클릭 **다음**합니다.  
  
17. 에 **광고 RMS 클러스터** 화면에서 **새 AD RMS 루트 클러스터 만들** 차례로 클릭 하 고 **다음**합니다.  
  
18. 에 **구성 데이터베이스** 화면을 클릭 **이 서버에 사용 하 여 Windows 내부 데이터베이스**을 차례로 클릭 하 고 **다음**합니다.  
  
    > [!NOTE]  
    > Windows 내부 데이터베이스를 사용 하는 것이 좋습니다 테스트 환경을 AD RMS 클러스터에 둘 이상의 서버를 지원 하지 않습니다. 프로덕션 배포 하는 별도 데이터베이스 서버를 사용 해야 합니다.  
  
19. 에 **서비스 계정** 화면에 **도메인 사용자 계정**, 클릭 **지정** 다음 사용자 이름을 지정 하 고 (**contoso\rms**), 및 암호 (**pass@word1**)를 클릭 하 고 **확인**, 클릭 한 다음 **다음**합니다.  
  
20. 에 **암호화 모드** 화면에서 클릭 **암호화 모드 2**합니다.  
  
21. 에 **클러스터 키 저장소** 화면에서 클릭 **다음**합니다.  
  
22. **클러스터 키 암호** 화면에 **암호** 및 **암호 확인** 상자, 입력 ** pass@word1 **을 차례로 클릭 하 고 **다음**합니다.  
  
23. 에 **클러스터 웹 사이트** 화면에서 되어 있는지 확인 **웹 사이트 기본** 을 선택한 다음 클릭 **다음**합니다.  
  
24. 에 **클러스터 주소** 화면에서는 **암호화 된 연결을 사용 하 여** 옵션에 **정식 도메인 이름** 상자에 입력 **FILE1.contoso.com**을 차례로 클릭 하 고 **다음**합니다.  
  
25. 에 **전체 인증서 이름** 화면에서 기본 이름을 (**파일 1**)의 텍스트 상자와 클릭 **다음**합니다.  
  
26. 에 **SCP 등록** 화면에서 **SCP 등록 이제**을 차례로 클릭 하 고 **다음**합니다.  
  
27. 에 **확인** 화면에서 클릭 **설치**합니다.  
  
28. 에 **결과** 화면을 클릭 **닫기**을 차례로 클릭 하 고 **닫기** 에 **설치 진행률** 화면 합니다. 완료 되 면 로그 오프 한 제공 암호를 사용 하 여 contoso\rms로 로그온 (**pass@word1**).  
  
29. AD RMS 콘솔을 실행 하 고 이동 **권한 정책 템플릿**합니다.  
  
    관리자를 열려면 AD RMS 콘솔에서 서버를 클릭 **로컬 서버** 콘솔 트리에서 클릭 **도구**을 차례로 클릭 하 고 **Active Directory 권한 관리 서비스**합니다.  
  
30. 클릭는 **배포 권한 정책 만들기** 템플릿 오른쪽 패널에 위치를 클릭 **추가**, 다음 정보를 선택 하 고 다음과 같습니다.  
  
    -   언어: 미국 영어  
  
    -   : 이름 Contoso 금융 관리자만  
  
    -   설명: Contoso 금융 관리자만  
  
    클릭 **추가**을 차례로 클릭 하 고 **다음**합니다.  
  
31. 사용자와 권한 섹션 아래를 클릭 **사용자 및 사용 권한**, 클릭 **추가**, 입력 ** financeadmin@contoso.com **를 클릭 하 고 **확인**합니다.  
  
32. 선택 **모든 권한**, 두고 **만료 없이 오른쪽으로 소유자가 (작성자) 모든 권한을 부여** 선택 합니다.  
  
33. 하지만 변경 없이 나머지 탭을 클릭 한 다음 클릭 **완료**합니다. CONTOSO\Administrator로 로그인 합니다.  
  
34. C:\inetpub\wwwroot\\_wmcs\certification, 폴더 선택 ServerCertification.asmx 파일을 찾아 읽고 파일에 사용 권한을 쓸를 인증 된 사용자를 추가 합니다.  
  
35. Windows PowerShell 열고 실행 `Get-FsrmRmsTemplate`합니다. 이 명령 사용 하 여이 절차의 이전 단계에서 만든 RMS 템플릿 볼 수 있는지 확인 합니다.  
  
> [!IMPORTANT]  
> 사용자는 파일 서버를 테스트할 수 있도록 즉시 변경 하려는 경우 다음을 수행 해야 할 수 있습니다.  
>   
> 1.  파일 1, 파일 서버에 관리자 명령 프롬프트를 열고 다음 명령을 실행 합니다.  
>   
>     -   gpupdate /force 합니다.  
>     -   NLTEST /SC_RESET:contoso.com  
> 2.  도메인 컨트롤러 d c (1)의 복제 Active Directory 합니다.  
>   
>     For more information about steps to force the replication of Active Directory, see [Active Directory Replication](https://technet.microsoft.com/library/cc794809(WS.10).aspx)  
  
필요에 따라 추가 역할 및 기능 마법사 서버 관리자를 사용 하는 대신 설치 하 고 다음 절차에 표시 된 AD RMS 서버 역할 구성 Windows PowerShell를 사용할 수 있습니다.  
  
###### <a name="to-install-and-configure-an-ad-rms-cluster-in-windows-server-2012-using-windows-powershell"></a>설치 및 사용 하 여 Windows PowerShell Windows Server 2012에서 AD RMS 클러스터 구성 하려면  
  
1.  암호를 사용 하 여 CONTOSO\Administrator로에 로그온: ** pass@word1 **합니다.  
  
    > [!IMPORTANT]  
    > AD RMS 서버 역할 설치 프로그램을 설치 하려면 (이 경우 CONTOSO\Administrator)에서 계정 둘 다의 로컬 관리자가 그룹 AD RMS 설치할 서버 컴퓨터에서 등록 뿐 아니라 Active Directory에 Enterprise 관리자 그룹의 회원 부여 해야 합니다.  
  
2.  서버 바탕 화면 작업 표시줄에서 선택 Windows PowerShell 아이콘을 마우스 오른쪽 단추로 **관리자 권한으로 실행** 를 Windows PowerShell 프롬프트 관리자 권한으로 엽니다.  
  
3.  서버 관리자 cmdlet AD RMS 서버 역할을 설치 하려면을 사용 하려면 다음과 같이 입력  
  
    ```  
    Add-WindowsFeature ADRMS '"IncludeAllSubFeature '"IncludeManagementTools  
    ```  
  
4.  설치 하는 광고 RMS 서버를 표현 Windows PowerShell 드라이브를 만듭니다.  
  
    예를 들어, 설치 하 고 AD RMS 루트 클러스터의 첫 번째 서버 구성 RC 라는 Windows PowerShell 드라이브를 만들기를 입력 합니다.  
  
    ```  
    Import-Module ADRMS  
    New-PSDrive -PSProvider ADRMSInstall -Name RC -Root RootCluster  
    ```  
  
5.  드라이브 이름에서 필요한 구성 설정 나타내는 개체에 속성을 설정 합니다.  
  
    예를 들어 설정 하려면 AD RMS 서비스 계정, Windows PowerShell 명령 프롬프트에 입력 합니다.  
  
    ```  
    $svcacct = Get-Credential  
    ```  
  
    Windows 보안 대화 상자가 나타나면 AD RMS 서비스 계정 도메인 사용자 이름 CONTOSO\RMS 및 할당된 암호를 입력 합니다.  
  
    다음, 광고 RMS 서비스 계정을 AD RMS 클러스터 설정을 할당 하려면 입력 다음 합니다.  
  
    ```  
    Set-ItemProperty -Path RC:\ -Name ServiceAccount -Value $svcacct  
    ```  
  
    다음을 AD RMS 서버 Windows 내부 데이터베이스를 Windows PowerShell 명령 프롬프트 사용 하도록 설정 하려면 다음을 입력 합니다.  
  
    ```  
    Set-ItemProperty -Path RC:\ClusterDatabase -Name UseWindowsInternalDatabase -Value $true  
    ```  
  
    다음을 안전 하 게 저장 클러스터 키 암호 변수를 Windows PowerShell 명령 프롬프트에 입력 합니다.  
  
    ```  
    $password = Read-Host -AsSecureString -Prompt "Password:"  
    ```  
  
    클러스터 주요 암호를 입력 한 다음 ENTER 키를 누릅니다.  
  
    다음, 암호를 Windows PowerShell 명령 프롬프트 AD RMS 설치를 지정 하려면 다음을 입력 합니다.  
  
    ```  
    Set-ItemProperty -Path RC:\ClusterKey -Name CentrallyManagedPassword -Value $password  
    ```  
  
    다음을 AD RMS 클러스터 주소를 Windows PowerShell 명령 프롬프트를 설정 하려면 다음을 입력 합니다.  
  
    ```  
    Set-ItemProperty -Path RC:\ -Name ClusterURL -Value "http://file1.contoso.com:80"  
    ```  
  
    다음를 Windows PowerShell 명령 프롬프트 AD RMS 설치를 위한 SLC 이름을 지정 하려면 다음을 입력 합니다.  
  
    ```  
    Set-ItemProperty -Path RC:\ -Name SLCName -Value "FILE1"  
    ```  
  
    다음으로 설정 하려면 AD RMS 클러스터 서비스 연결 지점 (SCP) Windows PowerShell 명령 프롬프트에 입력 합니다.  
  
    ```  
    Set-ItemProperty -Path RC:\ -Name RegisterSCP -Value $true  
    ```  
  
6.  실행는 **설치-ADRMS** cmdlet 합니다. AD RMS 서버 역할을 설치 및 구성 서버, 외에이 cmdlet도 필요한 경우 AD RMS에서 요구 하는 다른 기능을 설치 합니다.  
  
    예를 들어 RC 라는 Windows PowerShell 드라이브를 변경 하 고 설치 하 고 구성 AD RMS를 입력 합니다.  
  
    ```  
    Set-Location RC:\  
    Install-ADRMS -Path.  
    ```  
  
    타이핑 "Y" cmdlet 확인 하 라는 메시지가 나타나면 설치를 시작 하려고 합니다.  
  
7.  로 로그 아웃 CONTOSO\Administrator 및 로그 제공된 된 암호를 사용 하 여 CONTOSO\RMS ("pass@word1").  
  
    > [!IMPORTANT]  
    > AD RMS 서버 관리 하기 위해 계정에 로그인 하 고 사용 (이 경우 CONTOSO\RMS)에서 서버 관리 하는 모두 로컬 관리자가 그룹의 Active Directory에 Enterprise 관리자 그룹의 회원 뿐만 아니라 AD RMS 서버 컴퓨터에서 등록 부여 해야 합니다.  
  
8.  서버 바탕 화면 작업 표시줄에서 선택 Windows PowerShell 아이콘을 마우스 오른쪽 단추로 **관리자 권한으로 실행** 를 Windows PowerShell 프롬프트 관리자 권한으로 엽니다.  
  
9. 구성 하 고 AD RMS 서버를 표현 Windows PowerShell 드라이브를 만듭니다.  
  
    예를 들어, AD RMS 루트 클러스터 구성 하려면 RC 라는 Windows PowerShell 드라이브를 만든 입력 합니다.  
  
    ```  
    Import-Module ADRMSAdmin `  
    New-PSDrive -PSProvider ADRMSAdmin -Name RC -Root http://localhost -Force -Scope Global  
    ```  
  
10. 새 권한 템플릿을 Contoso 금융 관리자에 대 한 만들고 AD RMS 설치를 Windows PowerShell 명령 프롬프트에서 모든 권한이 있는 사용자 권한을 부여 하려면 다음과 같이 입력  
  
    ```  
    New-Item -Path RC:\RightsPolicyTemplate '"LocaleName en-us -DisplayName "Contoso Finance Admin Only" -Description "Contoso Finance Admin Only" -UserGroup financeadmin@contoso.com  -Right ('FullControl')  
    ```  
  
11. 확인 Contoso 금융 관리자 Windows PowerShell 명령 프롬프트에 대 한 새 권한 템플릿을 볼 수 있습니다.  
  
    ```  
    Get-FsrmRmsTemplate  
    ```  
  
    이전 단계에서 만든 RMS 템플릿을 확인이 cmdlet 출력 검토 표시 됩니다.  
  
### <a name="build-the-mail-server-srv1"></a>빌드 메일 서버 (s r v 1)  
S r v 1 SMTP/POP3 메일 서버를입니다. 액세스 거부 assistance 시나리오의 일환으로 메일 알림을 보낼 수 있도록 설정 해야 합니다.  
  
이 컴퓨터에서 Microsoft Exchange Server 구성 합니다. For more information, see [How to Install Exchange Server](https://go.microsoft.com/fwlink/?prd=12364).  
  
### <a name="build-the-client-virtual-machine-client1"></a>빌드 클라이언트 가상 컴퓨터 (CLIENT1)  
  
##### <a name="to-build-the-client-virtual-machine"></a>클라이언트 가상 컴퓨터 빌드  
  
1.  CLIENT1는 ID_AD_Network에 연결 합니다.  
  
2.  Microsoft Office 2010을 설치 합니다.  
  
3.  Contoso\Administrator,으로 로그인 한 다음 정보를 사용 하 여 Microsoft Outlook 구성 합니다.  
  
    -   사용자 이름: 파일 관리자  
  
    -   메일 주소:fileadmin@contoso.com  
  
    -   계정 유형이: POP3  
  
    -   수신 메일 서버: s r v 1 고정 IP 주소  
  
    -   보내는 메일 서버: s r v 1 고정 IP 주소  
  
    -   사용자 이름:fileadmin@contoso.com  
  
    -   암호를 기억: 선택  
  
4.  Outlook contoso\administrator 바탕 화면 바로 가기 만들기.  
  
5.  Outlook을 열고 모든 처음으로 시작할 메시지 해결 합니다.  
  
6.  생성 된 모든 테스트 메시지를 삭제 합니다.  
  
7.  \\\FILE1\Finance 문서를 가리키는 클라이언트 가상 컴퓨터의 모든 사용자에 대 한 바탕 화면에 새로운 바로 가기 만들기.  
  
8.  필요에 따라 다시 부팅 합니다.  
  
##### <a name="enable-access-denied-assistance-on-the-client-virtual-machine"></a>클라이언트 가상 컴퓨터에 액세스 거부 지원 사용  
  
1.  레지스트리 편집기를 열고 이동 **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Explorer**합니다.  
  
    -   설정 **EnableShellExecuteFileStreamCheck** 에 **1**합니다.  
  
    -   값: DWORD  
  
## <a name="BKMK_CF"></a>클레임 숲 시나리오에서 배포 하기 위한 랩 설정  
  
### <a name="BKMK_2.1"></a>2에 대 한 가상 컴퓨터 빌드  
  
-   Windows Server 2012 ISO에서 가상 컴퓨터 빌드입니다.  
  
-   가상 컴퓨터 이름을 d c 2 만듭니다.  
  
-   가상 컴퓨터의 ID_AD_Network에 연결 합니다.  
  
> [!IMPORTANT]  
> 가상 컴퓨터 도메인에 가입 하 고 클레임 유형 숲을 통한 배포 가상 컴퓨터를 Fqdn 관련 된 도메인의 해결할 수 있다는 필요 합니다. 이를 위해 가상 컴퓨터에는 DNS 설정을 수동으로 구성 해야 할 수 있습니다. For more information, see [Configuring a virtual network](https://technet.microsoft.com/library/cc732470%28v=ws.10%29.aspx).  
>   
> 모든 가상 컴퓨터 이미지 (클라이언트 및 서버)에서 고정 IP IPv4 버전 4 ()를 사용 하 여 다시 구성 해야 주소 및 시스템 DNS (도메인 이름) 클라이언트 설정 합니다. For more information, see [Configure a DNS Client for Static IP Address](https://go.microsoft.com/fwlink/?LinkId=150952).  
  
### <a name="BKMK_2.2"></a>라고에서는 adatum.com 새 숲 설정  
  
##### <a name="to-install-active-directory-domain-services"></a>Active Directory 도메인 서비스를 설치 하려면  
  
1.  가상 컴퓨터의 ID_AD_Network에 연결 합니다. 에 로그인 하 여 d c 2 관리자 권한으로 암호로 ** Pass@word1 **합니다.  
  
2.  서버 관리자 클릭 **관리**을 차례로 클릭 하 고 **역할 추가 및 기능**합니다.  
  
3.  에 **시작 하기 전에** 페이지, 클릭 **다음**합니다.  
  
4.  에 **설치 유형을 선택** 페이지, 클릭 **역할 또는 기능 기반 설치**을 차례로 클릭 하 고 **다음**합니다.  
  
5.  에 **선택 대상 서버** 페이지, 클릭 **서버 풀에서 서버를 선택**, Active Directory 도메인 (AD DS 서비스)를 설치를 클릭 한 다음 원하는 서버의 이름을 클릭 **다음**합니다.  
  
6.  에 **서버 역할 선택** 페이지, 클릭 **Active Directory 도메인 서비스**합니다. 에 **역할 추가 및 기능 마법사** 대화 상자를 클릭 **기능 추가**, 클릭 한 다음 **다음**합니다.  
  
7.  에 **기능 선택** 페이지, 클릭 **다음**합니다.  
  
8.  에 **AD DS** 페이지에서 정보를 검토 한 다음 클릭 **다음**합니다.  
  
9. 에 **확인** 페이지, 클릭 **설치**합니다. 결과 페이지에서 기능 설치 진행률 표시줄 역할 설치 되어 있는지를 나타냅니다.  
  
10. 에 **결과** 페이지에서 있는지 설치 되었는지 확인 한 다음 옆에 있는 느낌표가 화면 오른쪽 위 모서리에 있는 경고 아이콘을 클릭 **관리**합니다. 작업 목록을 클릭는 **도메인 컨트롤러이 서버 홍보** 링크입니다.  
  
    > [!IMPORTANT]  
    > 이 시점 설치 마법사를 닫을 대신 경우 클릭 **도메인 컨트롤러이 서버 홍보**를 클릭 하 여 광고 DS 설치를 계속할 수 있습니다 **작업** 서버 관리자에서 합니다.  
  
11. 에 **배포 구성** 페이지, 클릭 **새 숲 추가**, 루트 도메인의 이름을 입력 **에서는 adatum.com**을 차례로 클릭 하 고 **다음**합니다.  
  
12. 에 **도메인 컨트롤러 옵션** 페이지, Windows Server 2012와 도메인 및 숲 기능 수준을 선택, DSRM 암호 지정 ** pass@word1 **을 차례로 클릭 하 고 **다음**합니다.  
  
13. 에 **DNS 옵션** 페이지, 클릭 **다음**합니다.  
  
14. 에 **추가 옵션** 페이지, 클릭 **다음**합니다.  
  
15. 에 **경로** 페이지, Active Directory 데이터베이스, 로그 파일과 SYSVOL 폴더의 위치를 입력 (또는 기본 위치에 동의)을 차례로 클릭 하 고 **다음**합니다.  
  
16. 에 **리뷰 옵션** 페이지 선택 사항을 확인 하 고 클릭 한 다음 **다음**합니다.  
  
17. 에 **필수 확인** 페이지에서 확인 필수 유효성 검사를 완료 한 후 클릭 **설치**합니다.  
  
18. 에 **결과** 페이지 서버 성공적으로 도메인 컨트롤러도 구성 되어 있는지 확인 한 다음 클릭 **닫기**합니다.  
  
19. 서버 AD DS 설치를 완료 하려면 다시 시작 합니다. (기본적으로이 자동으로 정품 인증 됩니다.)  
  
> [!IMPORTANT]  
> 두는 숲을 설정 하면 네트워크 제대로 구성 되어 있는지 확인 하려면 다음을 수행 해야 합니다.  
>   
> -   에서는 adatum.com adatum\administrator로 로그인 합니다. 명령 프롬프트 창 열기 입력 **nslookup contoso.com**, ENTER 키를 누릅니다.  
> -   Contoso.com contoso\administrator로 로그인 합니다. 명령 프롬프트 창 열기 입력 **nslookup에서는 adatum.com**, ENTER 키를 누릅니다.  
>   
> 오류 없이이 명령을 실행 숲은 서로 통신할 수 있습니다. For more information on nslookup errors, see the troubleshooting section in the topic [Using NSlookup.exe](https://support.microsoft.com/kb/200525)  
  
### <a name="BKMK_2.22"></a>Contoso.com에서는 adatum.com 신뢰 숲 언어로 설정  
In this step, you create a trust relationship between the Adatum Corporation site and the Contoso, Ltd. site.  
  
##### <a name="to-set-contoso-as-a-trusting-forest-to-adatum"></a>Contoso Adatum 신뢰 숲으로 설정 하려면  
  
1.  D c 2 관리자 권한으로 로그인 합니다. 에 **시작** 화면 domain.msc 입력 합니다.  
  
2.  콘솔 트리에서에서는 adatum.com를 마우스 오른쪽 단추로 클릭 하 고 속성을 클릭 합니다.  
  
3.  에 **신뢰** 탭을 클릭 **새 신뢰**을 차례로 클릭 하 고 **다음**합니다.  
  
4.  에 **신뢰 이름** 페이지에서 입력 **contoso.com**를에 시스템 DNS (도메인 이름) 이름 필드를 클릭 한 다음 **다음**합니다.  
  
5.  에 **신뢰 유형** 페이지, 클릭 **숲 신뢰**, 클릭 한 다음 **다음**합니다.  
  
6.  에 **신뢰 방향** 페이지, 클릭 **양방향**합니다.  
  
7.  에 **신뢰 측면** 페이지, 클릭 **이 도메인 및 지정된 된 도메인**을 차례로 클릭 하 고 **다음**합니다.  
  
8.  마법사의 지침에 따라 계속 합니다.  
  
### <a name="BKMK_2.4"></a>사용자가 추가 Adatum 숲 속의 만들기  
Jeff 낮은 사용자 암호 만들기 ** pass@word1 **, 값을 사용 하 여 회사 특성을 지정할 및 **Adatum**합니다.  
  
##### <a name="to-create-a-user-with-the-company-attribute"></a>회사 특성으로 사용자를  
  
1.  관리자 명령 프롬프트를 Windows powershell에서 연 다음 코드:  
  
    ```  
    New-ADUser `  
    -SamAccountName jlow `  
    -Name "Jeff Low" `  
    -UserPrincipalName jlow@adatum.com `  
    -AccountPassword (ConvertTo-SecureString `  
    -AsPlainText "pass@word1" -Force) `  
    -Enabled $true `  
    -PasswordNeverExpires $true `  
    -Path 'CN=Users,DC=adatum,DC=com' `  
    -Company Adatum`  
  
    ```  
  
### <a name="BKMK_2.5"></a>회사 클레임 종류 adataum.com에 만들기  
  
##### <a name="to-create-a-claim-type-by-using-windows-powershell"></a>클레임 유형을 Windows PowerShell를 사용 하 여 만들기  
  
1.  관리자 권한으로에서는 adatum.com에 로그인 합니다.  
  
2.  관리자 명령 프롬프트를 Windows powershell에서 열고 다음 코드를 입력 합니다.  
  
    ```  
    New-ADClaimType `  
    -AppliesToClasses:@('user') `  
    -Description:"Company" `  
    -DisplayName:"Company" `  
    -ID:"ad://ext/Company:ContosoAdatum" `  
    -IsSingleValued:$true `  
    -Server:"adatum.com" `  
    -SourceAttribute:Company `  
    -SuggestedValues:@((New-Object Microsoft.ActiveDirectory.Management.ADSuggestedValueEntry("Contoso", "Contoso", "")), (New-Object Microsoft.ActiveDirectory.Management.ADSuggestedValueEntry("Adatum", "Adatum", ""))) `  
  
    ```  
  
### <a name="BKMK_2.55"></a>회사 리소스 속성 contoso.com 사용 하도록 설정  
  
##### <a name="to-enable-the-company-resource-property-on-contosocom"></a>회사 리소스 속성 contoso.com 사용 하도록 설정 하려면  
  
1.  Contoso.com 관리자 권한으로 로그인 합니다.  
  
2.  서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **Active Directory 관리 센터**합니다.  
  
3.  Active Directory 관리 센터의 왼쪽된 창에서 클릭 **트리 보기**합니다. 왼쪽된 창에서 클릭 **동적 액세스 제어**, 다음 두 번 클릭 하 고 **리소스 속성**합니다.  
  
4.  선택 **회사** 에서 **리소스 속성** 목록을 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다. **제안 값** 섹션에서 클릭 **추가** 추천된 값을 추가 하려면: Contoso 및 Adatum, 클릭 한 다음 **확인** 두 번 합니다.  
  
5.  선택 **회사** 에서 **리소스 속성** 목록을 마우스 오른쪽 단추로 클릭 하 고 선택 **활성화**합니다.  
  
### <a name="BKMK_2.6"></a>동적 액세스 제어에서는 adatum.com에서  
  
##### <a name="to-enable-dynamic-access-control-for-adatumcom"></a>에서는 adatum.com에 대 한 동적 액세스 제어를 사용 하도록 설정 하려면  
  
1.  관리자 권한으로에서는 adatum.com에 로그인 합니다.  
  
2.  그룹 정책 관리 콘솔 열을 클릭 **에서는 adatum.com**, 다음 두 번 클릭 하 고 **도메인 컨트롤러**합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **기본 도메인 컨트롤러 정책**를 선택 하 고 **편집**합니다.  
  
4.  그룹 정책 편집기 관리 창에서 두 번 클릭 **컴퓨터 구성**를 두 번 클릭 **정책**, 두 번 클릭 **관리 템플릿**, 두 번 클릭 **시스템**, 다음 두 번 클릭 하 고 **KDC**합니다.  
  
5.  두 번 클릭 **KDC 클레임, 복합 인증 및 Kerberos armoring에 대 한 지원은** 옆에 있는 옵션을 선택 하 고 **사용**합니다. 중앙 액세스 정책을 사용 하 여이 설정을 사용 해야 합니다.  
  
6.  관리자 명령 프롬프트를 열고 다음 명령을 실행 합니다.  
  
    ```  
    gpupdate /force  
    ```  
  
### <a name="BKMK_2.8"></a>회사 클레임 유형 contoso.com에 만들기  
  
##### <a name="to-create-a-claim-type-by-using-windows-powershell"></a>클레임 유형을 Windows PowerShell를 사용 하 여 만들기  
  
1.  Contoso.com 관리자 권한으로 로그인 합니다.  
  
2.  열기 관리자 명령 프롬프트에서 Windows PowerShell 다음 다음 코드를 입력 합니다.  
  
    ```  
    New-ADClaimType '"SourceTransformPolicy `  
    '"DisplayName 'Company' `  
    '"ID 'ad://ext/Company:ContosoAdatum' `  
    '"IsSingleValued $true `  
    '"ValueType 'string' `  
  
    ```  
  
### <a name="BKMK_2.9"></a>중앙 액세스 규칙 만들기  
  
##### <a name="to-create-a-central-access-rule"></a>중앙 액세스 규칙을 만들려면  
  
1.  Active Directory 관리 센터의 왼쪽된 창에서 클릭 **트리 보기**합니다. 왼쪽된 창에서 클릭 **동적 액세스 제어**을 차례로 클릭 하 고 **중앙 액세스 규칙**합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **중앙 액세스 규칙**, 클릭 **새로**를 선택한 다음 **중앙 액세스 규칙**합니다.  
  
3.  에 **이름** 필드를 입력 **AdatumEmployeeAccessRule**합니다.  
  
4.  **사용 권한을** 섹션을는 **현재 사용 권한으로 다음 권한을 사용 하 여** 옵션을 클릭 **편집**을 차례로 클릭 하 고 **추가**합니다. 클릭는 **주체 선택** 링크, 입력 **인증 된 사용자**, 클릭 한 다음 **확인**합니다.  
  
5.  **권한에 대 한 권한 항목** 대화 상자를 클릭 **조건을 추가**, 다음과 같은 입력 하 고: [**사용자**] [**회사**] [**같음**] [**값**] [**Adatum**] 합니다. 사용 권한이 있어야 **수정, 읽기 하 고 실행 읽고, 쓰기**합니다.  
  
6.  클릭 **확인**합니다.  
  
7.  클릭 **확인** 세 번 완료 한 Active Directory 관리 센터도 돌아갑니다.  
  
    ![해결 방법 가이드](media/Appendix-B--Setting-Up-the-Test-Environment/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
    다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.  
  
    ```  
    New-ADCentralAccessRule `  
    -CurrentAcl:"O:SYG:SYD:AR(A;;FA;;;OW)(A;;FA;;;BA)(A;;FA;;;SY)(XA;;0x1301bf;;;AU;(@USER.ad://ext/Company:ContosoAdatum == `"Adatum`"))" `  
    -Name:"AdatumEmployeeAccessRule" `  
    -ProposedAcl:$null `  
    -ProtectedFromAccidentalDeletion:$true `  
    -Server:"contoso.com" `  
    ```  
  
### <a name="BKMK_2.10"></a>중앙 액세스 정책 만들기  
  
##### <a name="to-create-a-central-access-policy"></a>중앙 액세스 정책 만들려면  
  
1.  Contoso.com 관리자 권한으로 로그인 합니다.  
  
2.  관리자 명령 프롬프트를 Windows powershell에서 열고 다음 코드 다음 잘라내어 합니다.  
  
    ```  
    New-ADCentralAccessPolicy "Adatum Only Access Policy"   
    Add-ADCentralAccessPolicyMember "Adatum Only Access Policy" `  
    -Member "AdatumEmployeeAccessRule" `  
    ```  
  
### <a name="BKMK_2.11"></a>그룹 정책을 통해 새 정책을 게시 합니다.  
  
##### <a name="to-apply-the-central-access-policy-across-file-servers-through-group-policy"></a>그룹 정책을 통해 파일 서버에 대해 중앙 액세스 정책을 적용 하려면  
  
1.  에 **시작** 화면에서 입력 **관리 도구**의 **검색** 표시줄 클릭 **설정**합니다. 에 **설정** 결과 클릭 **관리 도구**합니다. 그룹 정책 관리 콘솔에서 엽니다는 **관리 도구** 폴더 합니다.  
  
    > [!TIP]  
    > 하는 경우는 **표시 관리 도구** 설정은 사용자가, 관리 도구 폴더 및 해당 내용을에 표시 되지 것입니다는 **설정** 결과 합니다.  
  
2.  Contoso.com 도메인을 마우스 오른쪽 단추로 클릭, **GPO이이 도메인에 있는 만들고 여기에 연결**  
  
3.  와 같은 gpo 설명 이름을 입력 **AdatumAccessGPO**을 차례로 클릭 하 고 **확인**합니다.  
  
##### <a name="to-apply-the-central-access-policy-to-the-file-server-through-group-policy"></a>그룹 정책을 통해 파일 서버에 대 한 중앙 액세스 정책을 적용 하려면  
  
1.  에 **시작** 화면에서 입력 **그룹 정책 관리**에 **검색** 상자 합니다. 열린 **그룹 정책 관리** 관리 도구 폴더에서 합니다.  
  
    > [!TIP]  
    > 하는 경우는 **표시 관리 도구** 설정은 사용자가, 관리 도구 폴더 및 해당 내용을 설정 결과에 표시 되지 것입니다.  
  
2.  로 이동 하 고 다음과 같은 Contoso 선택: 그룹 정책 Management\Forest: contoso.com\Domains\contoso.com 합니다.  
  
3.  마우스 오른쪽 단추로 클릭는 **AdatumAccessGPO** 정책과 선택 **편집**합니다.  
  
4.  그룹 정책 관리 편집기를 클릭 **컴퓨터 구성**, 확장 **정책**, 확장 **Windows 설정**을 차례로 클릭 하 고 **보안 설정**합니다.  
  
5.  확장 **파일 시스템**를 마우스 오른쪽 단추로 클릭 **중앙 액세스 정책**을 차례로 클릭 하 고 **중앙 관리 액세스 정책**합니다.  
  
6.  **중앙 액세스 정책에서 구성** 대화 상자를 클릭 **추가**선택 **Adatum만 액세스 정책**, 클릭 한 다음 **확인**합니다.  
  
7.  그룹 정책 관리 편집기 닫습니다. 이제 중앙 액세스 정책을 그룹 정책에 추가 했습니다.  
  
### <a name="BKMK_2.12"></a>파일 서버에 수익 폴더 만들기  
파일 1에서 새 NTFS 볼륨 만들고 다음 폴더를 만들: D:\Earnings 합니다.  
  
> [!NOTE]  
> 중앙 액세스 정책은 시스템에서 기본적으로 활성화 되지 또는 부팅 볼륨 c: 합니다.  
  
### <a name="BKMK_2.13"></a>분류 설정 하 고 중앙 액세스 정책을 수익 폴더에 적용 합니다.  
  
##### <a name="to-assign-the-central-access-policy-on-the-file-server"></a>파일 서버에 대 한 중앙 액세스 정책을 할당 하려면  
  
1.  Hyper-v 관리자에서 파일 1 서버에 연결 합니다. 에 로그인 하는 서버 Contoso\Administrator, 암호를 사용 하 여 ** pass@word1 **합니다.  
  
2.  관리자 권한 명령 프롬프트 및 유형 엽니다: **gpupdate /force**합니다. 이렇게 하면 그룹 정책 변경 사항을 서버에 적용 됩니다.  
  
3.  글로벌 리소스 속성 Active Directory에서 복구 해야 할 수도 있습니다. Windows PowerShell 열기, 입력 `Update-FSRMClassificationpropertyDefinition`, ENTER 키를 누릅니다. Windows PowerShell 닫습니다.  
  
4.  Windows 탐색기를 열고 D:\EARNINGS로 이동 합니다. 마우스 오른쪽 단추로 클릭는 **수익** 폴더를 클릭 하 고 **속성**합니다.  
  
5.  Click the **Classification** tab. Select **Company**, and then select **Adatum** in the **Value** field.  
  
6.  클릭 **변경**선택 **Adatum만 액세스 정책** 드롭다운 메뉴에서 **적용**합니다.  
  
7.  Click the **Security** tab, click **Advanced**, and then click the **Central Policy** tab. You should see the **AdatumEmployeeAccessRule** listed. 항목을 모두 Active Directory 규칙을 만들 때 설정 사용 권한을 보기 확장할 수 있습니다.  
  
8.  클릭 **확인** Windows 탐색기도 돌아갑니다.  
  


