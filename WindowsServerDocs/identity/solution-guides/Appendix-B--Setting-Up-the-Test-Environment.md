---
ms.assetid: 82918181-525d-4e93-af96-957dac6aedb6
title: 부록 B 테스트 환경 설정
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3ebe125ce7850797d786e7b564c98889cfb19927
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445864"
---
# <a name="appendix-b-setting-up-the-test-environment"></a>부록 B: 테스트 환경 설정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 동적 액세스 제어를 테스트하는 실습 환경을 구축하는 단계에 대해 설명합니다. 종속된 구성 요소가 많으므로 지침을 순서대로 따라야 합니다.  

## <a name="prerequisites"></a>사전 요구 사항  
**하드웨어 및 소프트웨어 요구 사항**  

테스트 랩 설정 요구 사항:  

-   Windows Server 2008 R2 SP1 및 Hyper-V를 실행하는 호스트 서버  

-   Windows Server 2012 ISO 복사본  

-   Windows 8 ISO 복사본  

-   Microsoft Office 2010  

-   Microsoft Exchange Server 2003 이상을 실행하는 서버  

동적 액세스 제어 시나리오를 테스트하려면 다음 가상 컴퓨터를 빌드해야 합니다.  

-   DC1(도메인 컨트롤러)  

-   DC2(도메인 컨트롤러)  

-   FILE1(파일 서버 및 Active Directory Rights Management Services)  

-   SRV1(POP3 맟 SMTP 서버)  

-   CLIENT1(Microsoft Outlook이 설치된 클라이언트 컴퓨터)  

가상 컴퓨터의 암호는 다음과 같습니다.  

-   BUILTIN\Administrator: pass@word1  

-   Contoso\Administrator: pass@word1  

-   다른 모든 계정: pass@word1  

## <a name="build-the-test-lab-virtual-machines"></a>테스트 랩 가상 컴퓨터 빌드  

### <a name="install-the-hyper-v-role"></a>Hyper-V 역할 설치  
Windows Server 2008 R2 SP1을 실행하는 컴퓨터에 Hyper-V를 설치해야 합니다.  

##### <a name="to-install-the-hyper-v-role"></a>Hyper-V 역할을 설치하려면  

1.  **시작**을 클릭한 다음 서버 관리자를 클릭합니다.  

2.  서버 관리자 주 창의 역할 요약 영역에서 **역할 추가**를 클릭합니다.  

3.  **서버 역할 선택** 페이지에서 **Hyper-V**를 클릭합니다.  

4.  **가상 네트워크 만들기** 페이지에서 가상 컴퓨터에 대한 네트워크 연결을 설정하려면 하나 이상의 네트워크 어댑터를 클릭합니다.  

5.  **설치 선택 확인** 페이지에서 **설치**를 클릭합니다.  

6.  설치를 완료하려면 컴퓨터를 다시 시작해야 합니다. **닫기**를 클릭하여 마법사를 마친 다음 **예**를 클릭하여 컴퓨터를 다시 시작합니다.  

7.  컴퓨터를 다시 시작한 후 역할을 설치하는 데 사용한 것과 동일한 계정을 사용하여 로그인합니다. 구성 마법사 다시 시작에서 설치를 완료하면 **닫기**를 클릭하여 마법사를 마칩니다.  

### <a name="create-an-internal-virtual-network"></a>내부 가상 네트워크 만들기  
이제 ID_AD_Network라는 내부 가상 네트워크를 만듭니다.  

##### <a name="to-create-a-virtual-network"></a>가상 네트워크를 만들려면  

1.  Hyper-V 관리자를 엽니다.  

2.  **작업** 메뉴에서 **Virtual Network 관리자**를 클릭합니다.  

3.  **가상 네트워크 만들기**에서 **내부**를 선택합니다.  

4.  **추가**를 클릭합니다. **새 가상 네트워크** 페이지가 나타납니다.  

5.  새 네트워크 이름으로 **ID_AD_Network** 를 입력합니다. 다른 속성을 검토하고 필요한 경우 수정합니다.  

6.  **확인** 을 클릭하여 가상 네트워크를 만들고 가상 네트워크 관리자를 닫거나, **적용** 을 클릭하여 가상 네트워크를 만들고 가상 네트워크 관리자를 계속 사용합니다.  

### <a name="BKMK_Build"></a>도메인 컨트롤러 빌드  
가상 컴퓨터를 도메인 컨트롤러(DC1)로 사용되도록 빌드합니다. Windows Server 2012 ISO를 사용 하 여 가상 컴퓨터를 설치 하 고 d c 1 라는 이름을 지정 합니다.  

##### <a name="to-install-active-directory-domain-services"></a>Active Directory 도메인 서비스를 설치하려면  

1. 가상 컴퓨터를 ID_AD_Network에 연결합니다. DC1에 관리자로 로그인 암호로 <strong>pass@word1</strong>합니다.  

2. 서버 관리자에서 **관리**, **역할 및 기능 추가**를 차례로 클릭합니다.  

3. **시작하기 전** 페이지에서 **다음**을 클릭합니다.  

4. **설치 유형 선택** 페이지에서 **역할 기반 또는 기능 기반 설치**를 클릭한 후 **다음**을 클릭합니다.  

5. **대상 서버 선택** 페이지에서 **다음**을 클릭합니다.  

6. **서버 역할 선택** 페이지에서 **Active Directory 도메인 서비스**를 클릭합니다. **역할 및 기능 추가 마법사** 대화 상자에서 **기능 추가**, **다음**을 차례로 클릭합니다.  

7. **기능 선택** 페이지에서 **다음**을 클릭합니다.  

8. **Active Directory Domain Services** 페이지에서 정보를 검토한 후 **다음**을 클릭합니다.  

9. **설치 선택 확인** 페이지에서 **설치**를 클릭합니다. 결과 페이지의 기능 설치 진행률에 역할을 설치하는 중임이 나타납니다.  

10. **결과** 페이지에서 설치가 완료되었는지 확인하고 **닫기**를 클릭합니다. 서버 관리자의 화면 오른쪽 위 **관리**옆에 있는 느낌표가 표시된 경고 아이콘을 클릭합니다. 작업 목록에서 **이 서버를 도메인 컨트롤러로 승격** 링크를 클릭합니다.  

11. **배포 구성** 페이지에서 **새 포리스트 추가**를 클릭하고 루트 도메인의 이름 **contoso.com**을 입력한 후 **다음**을 클릭합니다.  

12. 에 **도메인 컨트롤러 옵션** 페이지, 도메인 및 포리스트 기능 수준을 Windows Server 2012로 선택 하 고, DSRM 암호를 지정 <strong>pass@word1</strong>를 클릭 하 고 **다음**.  

13. **DNS 옵션** 페이지에서 **다음**을 클릭합니다.  

14. **추가 옵션** 페이지에서 **다음**을 클릭합니다.  

15. **경로** 페이지에서 Active Directory 데이터베이스, 로그 파일 및 SYSVOL 폴더에 대한 위치를 입력하거나 기본 위치를 적용한 후 **다음**을 클릭합니다.  

16. **검토 옵션** 페이지에서 선택 사항을 확인하고 **다음**을 클릭합니다.  

17. **필수 구성 요소 확인** 페이지에서 필수 구성 요소 확인 작업이 완료되었는지 확인하고 **설치**를 클릭합니다.  

18. **결과** 페이지에서 서버가 도메인 컨트롤러로 제대로 구성되었는지 확인하고 **닫기**를 클릭합니다.  

19. 서버를 다시 시작하여 AD DS 설치를 완료합니다. 기본적으로 이 작업은 자동으로 수행됩니다.  

Active Directory 관리 센터를 사용하여 다음 사용자를 만듭니다.  

##### <a name="create-users-and-groups-on-dc1"></a>DC1에서 사용자 및 그룹 만들기  

1. 관리자로 contoso.com에 로그인합니다. Active Directory 관리 센터를 시작합니다.  

2. 다음 보안 그룹을 만듭니다.  


   |    그룹 이름    |        Email Address         |
   |------------------|------------------------------|
   |   FinanceAdmin   |   financeadmin@contoso.com   |
   | FinanceException | financeexception@contoso.com |


3. 다음 OU(조직 구성 단위)를 만듭니다.  


   |   OU 이름    | 컴퓨터 |
   |--------------|-----------|
   | FileServerOU |   FILE1   |


4. 지정된 특성으로 다음 사용자를 만듭니다.  


   |       사용자       |  Username  |     메일 주소      | 부서 |      그룹       | 국가/지역 |
   |------------------|------------|------------------------|------------|------------------|----------------|
   | Myriam Delesalle | MDelesalle | MDelesalle@contoso.com |  재무   |                  |       US       |
   |    Miles Reid    |   MReid    |   MReid@contoso.com    |  재무   |   FinanceAdmin   |       US       |
   |   Esther Valle   |   EValle   |   EValle@contoso.com   | 작업 | FinanceException |       US       |
   |   Maira Wenzel   |  MWenzel   |  MWenzel@contoso.com   |     HR     |                  |       US       |
   |     Jeff Low     |    JLow    |    JLow@contoso.com    |     HR     |                  |       US       |
   |    RMS 서버    |    rms     |    rms@contoso.com     |            |                  |                |

   보안 그룹을 만드는 방법에 대한 자세한 내용은 Windows Server 웹 사이트에서 [새 그룹 만들기](https://technet.microsoft.com/library/dd861305.aspx) 를 참조하세요.  

##### <a name="to-create-a-group-policy-object"></a>그룹 정책 개체를 만들려면  

1.  화면의 오른쪽 위 모서리를 커서로 가리키고 검색 아이콘을 클릭합니다. 검색 상자에 **그룹 정책 관리**를 입력하고 **그룹 정책 관리**를 클릭합니다.  

2.  **포리스트: contoso.com**, **도메인**을 차례로 확장하고 **contoso.com**으로 이동하여 **(contoso.com)** 을 확장한 다음 **FileServerOU**를 선택합니다. 마우스 오른쪽 단추로 클릭 **이 도메인에서 GPO를 만들고 여기에 연결**

3.  GPO에 대한 설명이 포함된 이름(예: **FlexibleAccessGPO**)을 입력하고 **확인**을 클릭합니다.  

##### <a name="to-enable-dynamic-access-control-for-contosocom"></a>contoso.com에 동적 Access Control을 사용하려면  

1.  그룹 정책 관리 콘솔을 열고 **contoso.com**을 클릭한 다음 **도메인 컨트롤러**를 두 번 클릭합니다.  

2.  **기본 도메인 컨트롤러 정책**을 마우스 오른쪽 단추로 클릭하고 **편집**을 선택합니다.  

3.  그룹 정책 관리 편집기 창에서 **컴퓨터 구성**, **정책**, **관리 템플릿**, **시스템**, **KDC**를 차례로 두 번 클릭합니다.  

4.  **클레임, 복합 인증 및 Kerberos 아머링(armoring)에 대한 KDC 지원** 을 두 번 클릭하고 **사용**옆의 옵션을 선택합니다. 중앙 액세스 정책을 사용하려면 이 설정을 지정해야 합니다.  

5.  관리자 권한으로 명령 프롬프트를 열고 다음 명령을 실행합니다.  

    ```  
    gpupdate /force  
    ```  

### <a name="BKMK_FS1"></a>파일 서버 및 AD RMS 서버 (FILE1) 빌드  

1. Windows Server 2012 ISO에서 FILE1 이름으로 가상 컴퓨터를 빌드하십시오.  

2. 가상 컴퓨터를 ID_AD_Network에 연결합니다.  

3. 가상 컴퓨터를 contoso.com 도메인에 가입 하 고 다음 암호를 사용 하 여 contoso\administrator로 FILE1에 로그인 <strong>pass@word1</strong>합니다.  

#### <a name="install-file-services-resource-manager"></a>파일 서비스 리소스 관리자 설치  

###### <a name="to-install-the-file-services-role-and-the-file-server-resource-manager"></a>파일 서비스 역할 및 파일 서버 리소스 관리자를 설치하려면  

1.  서버 관리자에서 **역할 및 기능 추가**를 클릭합니다.  

2.  **시작하기 전** 페이지에서 **다음**을 클릭합니다.  

3.  **설치 유형 선택** 페이지에서 **다음**을 클릭합니다.  

4.  **대상 서버 선택** 페이지에서 **다음**을 클릭합니다.  

5.  **서버 역할 선택** 페이지에서 **File and Storage Services**를 확장하고 **파일 및 iSCSI 서비스** 옆의 확인란을 선택한 다음 **파일 서버 리소스 관리자**를 선택합니다.  

    역할 및 기능 추가 마법사 대화 상자에서 **기능 추가**, **다음**을 차례로 클릭합니다.  

6.  **기능 선택** 페이지에서 **다음**을 클릭합니다.  

7.  **설치 선택 확인** 페이지에서 **설치**를 클릭합니다.  

8.  **설치 진행률** 페이지에서 **닫기**를 클릭합니다.  

#### <a name="install-the-microsoft-office-filter-packs-on-the-file-server"></a>파일 서버에 Microsoft Office Filter Pack 설치  
Office 파일 기본적으로 제공 하는 것 보다 더 넓은 배열에 대 한 Ifilter를 사용 하도록 설정 하려면 Windows Server 2012에서 Microsoft Office Filter Pack을 설치 해야 합니다.  Windows Server 2012에는 기본적으로 설치, Microsoft Office 파일용 Ifilter가 없으며 및 파일 분류 인프라 Ifilter를 사용 하 여 콘텐츠 분석을 수행할 수 있습니다.  

IFilter를 다운로드하여 설치하려면 [Microsoft Office 2010 필터 팩](https://go.microsoft.com/fwlink/?LinkID=234122)을 참조하세요.  

#### <a name="configure-email-notifications-on-file1"></a>FILE1에서 메일 알림 구성  
할당량 및 파일 차단을 만드는 경우, 할당량 한도에 도달했을 때 또는 사용자가 차단된 파일을 저장하려고 시도한 후 사용자에게 메일 알림을 보낼 수 있는 옵션이 제공됩니다. 특정 관리자에게 할당량 및 파일 차단 이벤트를 정기적으로 알리려는 경우 하나 이상의 기본 받는 사람을 구성할 수 있습니다. 이러한 알림을 보내려면 메일 메시지를 전달하는 데 사용할 SMTP 서버를 지정해야 합니다.  

###### <a name="to-configure-email-options-in-file-server-resource-manager"></a>파일 서버 리소스 관리자에서 메일 옵션을 구성하려면  

1. 파일 서버 리소스 관리자를 엽니다. 파일 서버 리소스 관리자를 열려면 **시작**을 클릭하고 **파일 서버 리소스 관리자**를 입력한 다음 **파일 서버 리소스 관리자**를 클릭합니다.  

2. 파일 서버 리소스 관리자 인터페이스에서 **파일 서버 리소스 관리자**를 마우스 오른쪽 단추로 클릭하고 **옵션 구성**을 클릭합니다. **파일 서버 리소스 관리자 옵션** 대화 상자가 열립니다.  

3. **메일 알림** 탭에서 SMTP 서버 이름 또는 IP 주소 아래에 메일 알림을 전달할 SMTP 서버의 호스트 이름 또는 IP 주소를 입력합니다.  

4. 특정 관리자 할당량에 알리거나 아래에 있는 파일 차단 이벤트를 정기적으로 하려는 경우 **기본 수신 관리자**와 같은 각 전자 메일 주소를 입력 fileadmin@contoso.com합니다. 형식을 사용 하 여 account@domain, 및 세미콜론을 사용 하 여 여러 계정을 구분 합니다.  

#### <a name="create-groups-on-file1"></a>FILE1에서 그룹 만들기  

###### <a name="to-create-security-groups-on-file1"></a>FILE1에서 보안 그룹을 만들려면  

1. 암호를 사용 하 여 contoso\administrator로 FILE1에 로그인: <strong>pass@word1</strong>합니다.  

2. NT AUTHORITY\Authenticated Users를 **WinRMRemoteWMIUsers__** 그룹에 추가합니다.  

#### <a name="create-files-and-folders-on-file1"></a>FILE1에서 파일 및 폴더 만들기  

1.  FILE1에서 새 NTFS 볼륨을 만든 다음 D:\Finance Documents 폴더를 만듭니다.  

2.  지정된 세부 정보로 다음 파일을 만듭니다.  

    -   **Finance Memo.docx**: 문서에 일부 재무 관련 텍스트를 추가합니다. 예를 들어 ' 재무 문서에 액세스할 수 있는 사용자에 대 한 비즈니스 규칙이 변경 되었습니다. 이제 FinanceExpert 그룹의 구성원만 재무 문서에 액세스할 수 있습니다. 다른 부서나 그룹에 대 한 액세스 권한이 있습니다.' 환경에 구현하기 전에 이 변경 내용의 영향을 평가해야 합니다. 이 문서의 모든 페이지에 CONTOSO CONFIDENTIAL이 바닥글로 표시되어 있는지 확인합니다.  

    -   **Request for Approval to Hire.docx**: 이 문서에 지원자 정보를 수집하는 양식을 만듭니다. 문서에 **Applicant Name, Social Security number, Job Title, Proposed Salary, Starting Date, Supervisor name, Department** 필드가 있어야 합니다. 문서에 **Supervisor Signature, Approved Salary, Conformation of Offer** 및 **Status of Offer**에 대한 양식이 있는 섹션을 추가합니다.   
        문서 권한 관리를 설정해야 합니다.  

    -   **Word Document1.docx**: 이 문서에 일부 테스트 콘텐츠를 추가합니다.  

    -   **Word Document2.docx**: 이 문서에 테스트 콘텐츠를 추가 합니다.  

    -   **Workbook1.xlsx**  

    -   **Workbook2.xlsx**  

    -   바탕 화면에 Regular Expressions라는 폴더를 만듭니다. 이 폴더에 **RegEx-SSN**이라는 텍스트 문서를 만듭니다. 파일에 다음 콘텐츠를 입력한 다음 파일을 저장하고 닫습니다.   
        ^(?!000)([0-7]\d{2}|7([0-7]\d|7[012]))([ -]?)(?!00)\d\d\3(?!0000)\d{4}$  

3.  D:\Finance Documents 폴더를 Finance Documents로 공유하고 모든 사람이 공유를 읽고 쓸 수 있도록 허용합니다.  

> [!NOTE]  
> 중앙 액세스 정책은 시스템 또는 부팅 볼륨 C:에는 기본적으로 사용되지 않습니다.  

#### <a name="BKMK_CS1"></a>Active Directory Rights Management Services를 설치 합니다.  
서버 관리자를 통해 AD RMS(Active Directory Rights Management Services)와 모든 필수 기능을 추가합니다. 모든 기본값을 선택합니다.  

###### <a name="to-install-active-directory-rights-management-services"></a>Active Directory Rights Management Services를 설치하려면  

1. CONTOSO\Administrator 또는 Domain Admins 그룹의 구성원으로 FILE1에 로그인합니다.  

   > [!IMPORTANT]  
   > AD RMS 서버 역할을 설치하려면 설치 관리자 계정(이 예제의 경우 CONTOSO\Administrator)에 AD RMS를 설치할 서버 컴퓨터의 로컬 Administrators 그룹과 Active Directory의 Enterprise Admins 그룹 모두에 대한 구성원 자격을 부여해야 합니다.  

2. 서버 관리자에서 **역할 및 기능 추가**를 클릭합니다. 역할 및 기능 추가 마법사가 나타납니다.  

3. **시작하기 전** 화면에서 **다음**을 클릭합니다.  

4. **설치 유형 선택** 화면에서 **역할 기반 또는 기능 기반 설치**를 클릭하고 **다음**을 클릭합니다.  

5. **서버 대상 선택** 화면에서 **다음**을 클릭합니다.  

6. **서버 역할 선택** 화면에서 **Active Directory Rights Management Services**옆의 상자를 선택하고 **다음**을 클릭합니다.  

7. **Active Directory Rights Management Services에 필요한 기능을 추가하시겠습니까?** 대화 상자에서 **기능 추가**를 클릭합니다.  

8. **서버 역할 선택** 화면에서 **다음**을 클릭합니다.  

9. **설치할 기능 선택** 화면에서 **다음**을 클릭합니다.  

10. **Active Directory Rights Management Services** 화면에서 다음을 클릭합니다.  

11. **역할 서비스 선택** 화면에서 **다음**을 클릭합니다.  

12. **웹 서버 역할(IIS)** 화면에서 **다음**을 클릭합니다.  

13. **역할 서비스 선택** 화면에서 **다음**을 클릭합니다.  

14. **설치 선택 확인** 화면에서 **설치**를 클릭합니다.  

15. 설치가 완료되면 **설치 진행률** 화면에서 **추가 구성 수행**을 클릭합니다. AD RMS 구성 마법사가 나타납니다.  

16. **AD RMS** 화면에서 **다음**을 클릭합니다.  

17. **AD RMS 클러스터** 화면에서 **새 AD RMS 루트 클러스터 만들기** 를 선택하고 **다음**을 클릭합니다.  

18. **구성 데이터베이스** 화면에서 **이 서버에서 Windows 내부 데이터베이스 사용**을 클릭한 후 **다음**을 클릭합니다.  

    > [!NOTE]  
    > Windows 내부 데이터베이스는 AD RMS 클러스터에서 둘 이상의 서버를 지원하지 않으므로 테스트 환경에서만 사용하는 것이 좋습니다. 프로덕션 배포에서는 별도의 데이터베이스 서버를 사용해야 합니다.  

19. 에 **서비스 계정** 화면의 **도메인 사용자 계정을**, 클릭 **지정** 사용자 이름을 지정 합니다 (**contoso\rms**), 및 암호 (<strong>pass@word1</strong>)를 클릭 하 고 **확인**를 클릭 하 고 **다음**합니다.  

20. **암호화 모드** 화면에서 **암호화 모드 2**를 클릭합니다.  

21. **클러스터 키 저장소** 화면에서 **다음**을 클릭합니다.  

22. 에 **클러스터 키 암호** 화면의 합니다 **암호** 및 **암호 확인** 상자를 입력 <strong>pass@word1</strong>를 클릭 하 고 **다음**합니다.  

23. **클러스터 웹 사이트** 화면에서 **기본 웹 사이트** 가 선택되어 있는지 확인하고 **다음**을 클릭합니다.  

24. **클러스터 주소** 화면에서 **암호화되지 않은 연결 사용** 옵션을 선택한 다음 **정규화된 도메인 이름** 상자에 **FILE1.contoso.com**을 입력하고 **다음**을 클릭합니다.  

25. **사용 허가자 인증서 이름** 화면에서 텍스트 상자에 있는 기본 이름(**FILE1**)을 적용하고 **다음**을 클릭합니다.  

26. **SCP 등록** 화면에서 **지금 SCP 등록**을 선택하고 **다음**을 클릭합니다.  

27. **확인** 화면에서 **설치**를 클릭합니다.  

28. **결과** 화면에서 **닫기**를 클릭한 다음 **설치 진행률** 화면에서 **닫기**를 클릭합니다. 로그 오프 했다가 제공 된 암호를 사용 하 여 contoso\rms로 로그온 완료 되 면 (<strong>pass@word1</strong>).  

29. AD RMS 콘솔을 시작하고 **권한 정책 템플릿**으로 이동합니다.  

    AD RMS 콘솔을 열려면 서버 관리자의 콘솔 트리에서 **로컬 서버**를 클릭하고 **도구**를 클릭한 다음 **Active Directory Rights Management Services**를 클릭합니다.  

30. 오른쪽 패널에 있는 **분산 권한 정책 템플릿 만들기** 를 클릭한 다음 **추가**를 클릭하고 다음 정보를 선택합니다.  

    -   언어: 영어(미국)  

    -   이름: Contoso Finance Admin Only  

    -   설명: Contoso Finance Admin Only  

    **추가**를 클릭하고 **다음**을 클릭합니다.  

31. 사용자 및 권한 섹션에서 클릭 **사용자 및 사용 권한**, 클릭 **추가**, 형식 <strong>financeadmin@contoso.com</strong>를 클릭 하 고 **확인**합니다.  

32. **모든 권한**을 선택하고 **소유자(만든 이)에게 만료 없이 모든 권한을 부여** 를 선택된 상태로 둡니다.  

33. 나머지 탭을 변경하지 말고 클릭한 다음 **마침**을 클릭합니다. CONTOSO\Administrator로 로그인합니다.  

34. C:\inetpub\wwwroot 폴더로\\_wmcs\certification, ServerCertification.asmx 파일을 선택 하 고 인증 된 사용자에 대 한 읽기 및 쓰기 권한이 파일에 추가 합니다.  

35. Windows PowerShell을 열고 `Get-FsrmRmsTemplate`을 실행합니다. 이 절차의 이전 단계에서 만든 RMS 템플릿을 이 명령으로 볼 수 있는지 확인합니다.  

> [!IMPORTANT]  
> 테스트할 수 있도록 파일 서버에 변경 내용을 즉시 적용하려면 다음을 수행해야 합니다.  
>   
> 1.  파일 서버 FILE1에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행합니다.  
>   
>     -   gpupdate /force.  
>     -   NLTEST /SC_RESET:contoso.com  
> 2.  도메인 컨트롤러(DC1)에서 Active Directory를 복제합니다.  
>   
>     Active Directory 복제 단계에 대 한 자세한 내용은 참조 [Active Directory 복제](https://technet.microsoft.com/library/cc794809(WS.10).aspx)  

원하는 경우, 서버 관리자에서 역할 및 기능 추가 마법사를 사용하는 대신 다음 절차에 표시된 대로 Windows PowerShell을 사용하여 AD RMS 서버 역할을 설치하고 구성할 수 있습니다.  

###### <a name="to-install-and-configure-an-ad-rms-cluster-in-windows-server-2012-using-windows-powershell"></a>Windows PowerShell을 사용하여 Windows Server 2012에서 AD RMS 클러스터를 설치하고 구성하려면  

1. 암호를 사용 하 여 CONTOSO\Administrator로 로그온 합니다. <strong>pass@word1</strong>합니다.  

   > [!IMPORTANT]  
   > AD RMS 서버 역할을 설치하려면 설치 관리자 계정(이 예제의 경우 CONTOSO\Administrator)에 AD RMS를 설치할 서버 컴퓨터의 로컬 Administrators 그룹과 Active Directory의 Enterprise Admins 그룹 모두에 대한 구성원 자격을 부여해야 합니다.  

2. 서버 바탕 화면의 작업 표시줄에서 Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행** 을 선택하여 관리자 권한으로 Windows PowerShell 프롬프트를 엽니다.  

3. 서버 관리자 cmdlet을 사용하여 AD RMS 서버 역할을 설치하려면 다음을 입력합니다.  

   ```  
   Add-WindowsFeature ADRMS '"IncludeAllSubFeature '"IncludeManagementTools  
   ```  

4. 설치할 AD RMS 서버를 나타내는 Windows PowerShell 드라이브를 만듭니다.  

   예를 들어 RC라는 Windows PowerShell 드라이브를 만들어 AD RMS 루트 클러스터에 설치하고 첫 번째 서버로 구성하려면 다음을 입력합니다.  

   ```  
   Import-Module ADRMS  
   New-PSDrive -PSProvider ADRMSInstall -Name RC -Root RootCluster  
   ```  

5. 드라이브 네임스페이스의 개체에 대해 필요한 구성 설정을 나타내는 속성을 설정합니다.  

   예를 들어 AD RMS 서비스 계정을 설정하려면 Windows PowerShell 명령 프롬프트에서 다음을 입력합니다.  

   ```  
   $svcacct = Get-Credential  
   ```  

   Windows 보안 대화 상자가 나타나면 AD RMS 서비스 계정 도메인 사용자 이름 CONTOSO\RMS와 지정된 암호를 입력합니다.  

   그런 다음 AD RMS 서비스 계정을 AD RMS 클러스터 설정에 할당하려면 다음을 입력합니다.  

   ```  
   Set-ItemProperty -Path RC:\ -Name ServiceAccount -Value $svcacct  
   ```  

   그런 다음 Windows 내부 데이터베이스를 사용하도록 AD RMS 서버를 설정하려면 Windows PowerShell 명령 프롬프트에서 다음을 입력합니다.  

   ```  
   Set-ItemProperty -Path RC:\ClusterDatabase -Name UseWindowsInternalDatabase -Value $true  
   ```  

   그런 다음 클러스터 키 암호를 변수에 안전하게 저장하려면 Windows PowerShell 명령 프롬프트에서 다음을 입력합니다.  

   ```  
   $password = Read-Host -AsSecureString -Prompt "Password:"  
   ```  

   클러스터 키 암호를 입력하고 Enter 키를 누릅니다.  

   그런 다음 AD RMS 설치에 암호를 지정하려면 Windows PowerShell 명령 프롬프트에서 다음을 입력합니다.  

   ```  
   Set-ItemProperty -Path RC:\ClusterKey -Name CentrallyManagedPassword -Value $password  
   ```  

   그런 다음 AD RMS 클러스터 주소를 설정하려면 Windows PowerShell 명령 프롬프트에서 다음을 입력합니다.  

   ```  
   Set-ItemProperty -Path RC:\ -Name ClusterURL -Value "http://file1.contoso.com:80"  
   ```  

   그런 다음 AD RMS 설치에 대한 SLC 이름을 지정하려면 Windows PowerShell 명령 프롬프트에서 다음을 입력합니다.  

   ```  
   Set-ItemProperty -Path RC:\ -Name SLCName -Value "FILE1"  
   ```  

   그런 다음 AD RMS 설치에 대한 SCP(서비스 연결 지점)를 설정하려면 Windows PowerShell 명령 프롬프트에서 다음을 입력합니다.  

   ```  
   Set-ItemProperty -Path RC:\ -Name RegisterSCP -Value $true  
   ```  

6. **Install-ADRMS** cmdlet을 실행합니다. AD RMS 서버 역할을 설치하고 서버를 구성하는 것 외에도 이 cmdlet은 필요한 경우 AD RMS에 필요한 다른 기능을 설치합니다.  

   예를 들어 RC라는 Windows PowerShell 드라이브로 변경하여 AD RMS를 설치하고 구성하려면 다음을 입력합니다.  

   ```  
   Set-Location RC:\  
   Install-ADRMS -Path.  
   ```  

   설치를 시작할지 확인하라는 메시지가 표시되면 "Y"를 입력합니다.  

7. 로그 아웃 CONTOSO\Administrator로 로그 제공된 된 암호를 사용 하 여 CONTOSO\RMS로 ("pass@word1").  

   > [!IMPORTANT]  
   > AD RMS 서버를 관리하려면 로그온하여 서버를 관리하는 데 사용할 계정(이 예제의 경우 CONTOSO\RMS)에 AD RMS 서버 컴퓨터의 로컬 Administrators 그룹과 Active Directory의 Enterprise Admins 그룹 모두에 대한 구성원 자격을 부여해야 합니다.  

8. 서버 바탕 화면의 작업 표시줄에서 Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행** 을 선택하여 관리자 권한으로 Windows PowerShell 프롬프트를 엽니다.  

9. 구성할 AD RMS 서버를 나타내는 Windows PowerShell 드라이브를 만듭니다.  

    예를 들어 RC라는 Windows PowerShell 드라이브를 만들어 AD RMS 루트 클러스터를 구성하려면 다음을 입력합니다.  

    ```  
    Import-Module ADRMSAdmin `  
    New-PSDrive -PSProvider ADRMSAdmin -Name RC -Root http://localhost -Force -Scope Global  
    ```  

10. Contoso 재무 관리자에 대한 새 권한 템플릿을 만들고 AD RMS 설치에서 모든 권한이 있는 사용자 권한을 할당하려면 Windows PowerShell 명령 프롬프트에서 다음을 입력합니다.  

    ```  
    New-Item -Path RC:\RightsPolicyTemplate '"LocaleName en-us -DisplayName "Contoso Finance Admin Only" -Description "Contoso Finance Admin Only" -UserGroup financeadmin@contoso.com  -Right ('FullControl')  
    ```  

11. Contoso 재무 관리자에 대한 새 권한 템플릿을 볼 수 있는지 확인하려면 Windows PowerShell 명령 프롬프트에서 다음을 입력합니다.  

    ```  
    Get-FsrmRmsTemplate  
    ```  

    이 cmdlet의 출력을 검토하여 이전 단계에서 만든 RMS 템플릿이 있는지 확인합니다.  

### <a name="build-the-mail-server-srv1"></a>메일 서버(SRV1) 빌드  
SRV1은 SMTP/POP3 메일 서버입니다. 액세스 거부 지원 시나리오의 일부로 전자 메일 알림을 보내려면 메일 서버를 설정해야 합니다.  

이 컴퓨터에서 Microsoft Exchange Server를 구성합니다. 자세한 내용은 [Exchange Server를 설치하는 방법](https://go.microsoft.com/fwlink/?prd=12364)을 참조하세요.  

### <a name="build-the-client-virtual-machine-client1"></a>클라이언트 가상 컴퓨터(CLIENT1) 빌드  

##### <a name="to-build-the-client-virtual-machine"></a>클라이언트 가상 컴퓨터를 빌드하려면  

1. CLIENT1을 ID_AD_Network에 연결합니다.  

2. Microsoft Office 2010을 설치합니다.  

3. Contoso\Administrator로 로그인한 후 다음 정보를 사용하여 Microsoft Outlook를 구성합니다.  

   - 이름: File Administrator  

   - 전자 메일 주소: fileadmin@contoso.com  

   - 계정 유형: POP3  

   - 들어오는 메일 서버: SRV1의 고정 IP 주소  

   - 보내는 메일 서버: SRV1의 고정 IP 주소  

   - 사용자 이름: fileadmin@contoso.com  

   - 암호 저장: 선택  

4. contoso\administrator 바탕 화면에 Outlook 바로 가기를 만듭니다.  

5. Outlook을 열고 모든 처음으로 시작 메시지의 주소입니다.  

6. 생성된 모든 테스트 메시지를 삭제합니다.  

7. 가리키는 클라이언트 가상 컴퓨터의 모든 사용자에 대 한 바탕 화면에서 새 바로 가기를 만들어 \\\FILE1\Finance 문서입니다.  

8. 필요에 따라 다시 부팅합니다.  

##### <a name="enable-access-denied-assistance-on-the-client-virtual-machine"></a>클라이언트 가상 컴퓨터에서 액세스 거부 지원 사용  

1.  레지스트리 편집기를 열고 **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Explorer**로 이동합니다.  

    -   **EnableShellExecuteFileStreamCheck**를 **1**로 설정합니다.  

    -   값: DWORD  

## <a name="BKMK_CF"></a>포리스트 시나리오에서 클레임을 배포 하기 위한 랩 설정  

### <a name="BKMK_2.1"></a>DC2 용 가상 머신 빌드  

-   Windows Server 2012 ISO에서 가상 컴퓨터를 빌드하십시오.  

-   DC2라는 가상 컴퓨터를 만듭니다.  

-   가상 컴퓨터를 ID_AD_Network에 연결합니다.  

> [!IMPORTANT]  
> 가상 컴퓨터를 도메인에 가입시키고 포리스트에서 클레임 유형을 배포하려면 가상 컴퓨터가 관련 도메인의 FQDN을 확인할 수 있어야 합니다. 이렇게 하려면 가상 컴퓨터에서 DNS 설정을 수동으로 구성해야 할 수도 있습니다. 자세한 내용은 [가상 네트워크 구성](https://technet.microsoft.com/library/cc732470%28v=ws.10%29.aspx)을 참조하세요.  
>   
> 고정 IPv4(IP 버전 4) 주소 및 DNS(Domain Name System) 클라이언트 설정을 사용하도록 모든 가상 컴퓨터 이미지(서버 및 클라이언트)를 구성해야 합니다. 자세한 내용은 [고정 IP 주소를 사용하도록 DNS 클라이언트 구성](https://go.microsoft.com/fwlink/?LinkId=150952)을 참조하세요.  

### <a name="BKMK_2.2"></a>Adatum.com 이라는 새 포리스트 설정  

##### <a name="to-install-active-directory-domain-services"></a>Active Directory 도메인 서비스를 설치하려면  

1. 가상 컴퓨터를 ID_AD_Network에 연결합니다. DC2에 관리자로 로그인 암호로 <strong>Pass@word1</strong>합니다.  

2. 서버 관리자에서 **관리**, **역할 및 기능 추가**를 차례로 클릭합니다.  

3. **시작하기 전** 페이지에서 **다음**을 클릭합니다.  

4. **설치 유형 선택** 페이지에서 **역할 기반 또는 기능 기반 설치**를 클릭한 후 **다음**을 클릭합니다.  

5. **대상 서버 선택** 페이지에서 **서버 풀에서 서버 선택**을 클릭하고 AD DS(Active Directory 도메인 서비스)를 설치할 서버의 이름을 클릭한 후 **다음**을 클릭합니다.  

6. **서버 역할 선택** 페이지에서 **Active Directory 도메인 서비스**를 클릭합니다. **역할 및 기능 추가 마법사** 대화 상자에서 **기능 추가**, **다음**을 차례로 클릭합니다.  

7. **기능 선택** 페이지에서 **다음**을 클릭합니다.  

8. **AD DS** 페이지에서 정보를 검토하고 **다음**을 클릭합니다.  

9. **확인** 페이지에서 **설치**를 클릭합니다. 결과 페이지의 기능 설치 진행률에 역할을 설치하는 중임이 나타납니다.  

10. **결과** 페이지에서 설치에 성공했는지 확인하고 화면 오른쪽 위 **관리**옆에 있는 느낌표가 표시된 경고 아이콘을 클릭합니다. 작업 목록에서 **이 서버를 도메인 컨트롤러로 승격** 링크를 클릭합니다.  

    > [!IMPORTANT]  
    > 이 시점에서 **이 서버를 도메인 컨트롤러로 승격** 링크를 클릭하지 않고 설치 마법사를 닫은 경우 서버 관리자에서 **작업**을 클릭하여 AD DS 설치를 계속할 수 있습니다.  

11. **배포 구성** 페이지에서 **새 포리스트 추가**를 클릭하고 루트 도메인의 이름 **adatum.com**을 입력한 후 **다음**을 클릭합니다.  

12. 에 **도메인 컨트롤러 옵션** 페이지, 도메인 및 포리스트 기능 수준을 Windows Server 2012로 선택 하 고, DSRM 암호를 지정 <strong>pass@word1</strong>를 클릭 하 고 **다음**.  

13. **DNS 옵션** 페이지에서 **다음**을 클릭합니다.  

14. **추가 옵션** 페이지에서 **다음**을 클릭합니다.  

15. **경로** 페이지에서 Active Directory 데이터베이스, 로그 파일 및 SYSVOL 폴더에 대한 위치를 입력하거나 기본 위치를 적용한 후 **다음**을 클릭합니다.  

16. **검토 옵션** 페이지에서 선택 사항을 확인하고 **다음**을 클릭합니다.  

17. **필수 구성 요소 확인** 페이지에서 필수 구성 요소 확인 작업이 완료되었는지 확인하고 **설치**를 클릭합니다.  

18. **결과** 페이지에서 서버가 도메인 컨트롤러로 제대로 구성되었는지 확인하고 **닫기**를 클릭합니다.  

19. 서버를 다시 시작하여 AD DS 설치를 완료합니다. 기본적으로 이 작업은 자동으로 수행됩니다.  

> [!IMPORTANT]  
> 네트워크가 올바르게 구성되었는지 확인하려면 두 포리스트를 모두 설정한 후 다음을 수행해야 합니다.  
>   
> -   adatum\administrator로 adatum.com에 로그인합니다. 명령 프롬프트 창을 열고 **nslookup contoso.com**을 입력한 다음 Enter 키를 누릅니다.  
> -   contoso\administrator로 contoso.com에 로그인합니다. 명령 프롬프트 창을 열고 **nslookup adatum.com**을 입력한 다음 Enter 키를 누릅니다.  
>   
> 이러한 명령이 오류 없이 실행되면 포리스트에서 서로 통신할 수 있습니다. nslookup 오류에 대한 자세한 내용은 [NSlookup.exe 사용](https://support.microsoft.com/kb/200525)항목에서 문제 해결 섹션을 참조하세요.  

### <a name="BKMK_2.22"></a>Contoso.com을 adatum.com의 트러스팅 포리스트로 설정  
이 단계에서는 Adatum Corporation 사이트와 Contoso, Ltd. 사이트 간의 트러스트 관계를 만듭니다.  

##### <a name="to-set-contoso-as-a-trusting-forest-to-adatum"></a>Contoso를 Adatum의 트러스팅 포리스트로 설정하려면  

1.  관리자로 DC2에 로그인합니다. **시작** 화면에서 domain.msc를 입력합니다.  

2.  콘솔 트리에서 adatum.com을 마우스 오른쪽 단추로 클릭하고 속성을 클릭합니다.  

3.  **트러스트** 탭에서 **새 트러스트**를 클릭한 후 **다음**을 클릭합니다.  

4.  **트러스트 이름** 페이지에서 DNS(Domain Name System) 이름 필드에 **contoso.com**을 입력하고 **다음**을 클릭합니다.  

5.  **트러스트 종류** 페이지에서 **포리스트 트러스트**를 클릭한 후 **다음**을 클릭합니다.  

6.  **트러스트 방향** 페이지에서 **양방향**을 클릭합니다.  

7.  **트러스트 파트너** 페이지에서 **이 도메인 및 지정한 도메인 모두에 대해 트러스트를 만듭니다.** 를 클릭하고 **다음**을 클릭합니다.  

8.  계속해서 마법사의 지침을 따릅니다.  

### <a name="BKMK_2.4"></a>Adatum 포리스트에서 추가 사용자 만들기  
암호를 사용 하 여 사용자 Jeff Low를 만들고 <strong>pass@word1</strong>를 회사 특성 값으로 할당 하 고 **Adatum**합니다.  

##### <a name="to-create-a-user-with-the-company-attribute"></a>Company 특성을 가진 사용자를 만들려면  

1.  Windows PowerShell에서 관리자 권한 명령 프롬프트를 열고 다음 코드를 붙여 넣습니다.  

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

### <a name="BKMK_2.5"></a>Adataum.com에서 Company 클레임 유형 만들기  

##### <a name="to-create-a-claim-type-by-using-windows-powershell"></a>Windows PowerShell을 사용하여 클레임 유형을 만들려면  

1.  관리자로 adatum.com에 로그인합니다.  

2.  Windows PowerShell에서 관리자 권한 명령 프롬프트를 열고 다음 코드를 입력합니다.  

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

### <a name="BKMK_2.55"></a>Contoso.com에서 회사 리소스 속성을 사용 하도록 설정  

##### <a name="to-enable-the-company-resource-property-on-contosocom"></a>contoso.com에서 회사 리소스 속성을 사용하려면  

1.  관리자로 contoso.com에 로그인합니다.  

2.  서버 관리자에서 **도구**를 클릭한 다음 **Active Directory 관리 센터**를 클릭합니다.  

3.  Active Directory 관리 센터의 왼쪽 창에서 **트리 보기**를 클릭합니다. 왼쪽 창에서 **동적 Access Control**을 클릭한 다음 **리소스 속성**을 클릭합니다.  

4.  **리소스 속성** 목록에서 **회사** 를 선택하고 마우스 오른쪽 단추를 클릭한 다음 **속성**을 선택합니다. **제안 값** 섹션에서 **추가**를 클릭하여 제안 값 Contoso와 Adatum을 추가하고 **확인**을 두 번 클릭합니다.  

5.  **리소스 속성** 목록에서 **회사**를 선택하고 마우스 오른쪽 단추를 클릭한 다음 **사용**을 선택합니다.  

### <a name="BKMK_2.6"></a>Adatum.com에서 동적 Access Control을 사용 하도록 설정  

##### <a name="to-enable-dynamic-access-control-for-adatumcom"></a>adatum.com에 동적 액세스 제어를 사용하려면  

1.  관리자로 adatum.com에 로그인합니다.  

2.  그룹 정책 관리 콘솔을 열고 **adatum.com**을 클릭한 다음 **도메인 컨트롤러**를 두 번 클릭합니다.  

3.  **기본 도메인 컨트롤러 정책**을 마우스 오른쪽 단추로 클릭하고 **편집**을 선택합니다.  

4.  그룹 정책 관리 편집기 창에서 **컴퓨터 구성**, **정책**, **관리 템플릿**, **시스템**, **KDC**를 차례로 두 번 클릭합니다.  

5.  **클레임, 복합 인증 및 Kerberos 아머링(armoring)에 대한 KDC 지원** 을 두 번 클릭하고 **사용**옆의 옵션을 선택합니다. 중앙 액세스 정책을 사용하려면 이 설정을 지정해야 합니다.  

6.  관리자 권한으로 명령 프롬프트를 열고 다음 명령을 실행합니다.  

    ```  
    gpupdate /force  
    ```  

### <a name="BKMK_2.8"></a>Contoso.com에서 Company 클레임 유형 만들기  

##### <a name="to-create-a-claim-type-by-using-windows-powershell"></a>Windows PowerShell을 사용하여 클레임 유형을 만들려면  

1.  관리자로 contoso.com에 로그인합니다.  

2.  Windows PowerShell에서 관리자 권한 명령 프롬프트를 열고 다음 코드를 입력합니다.  

    ```  
    New-ADClaimType '"SourceTransformPolicy `  
    '"DisplayName 'Company' `  
    '"ID 'ad://ext/Company:ContosoAdatum' `  
    '"IsSingleValued $true `  
    '"ValueType 'string' `  

    ```  

### <a name="BKMK_2.9"></a>중앙 액세스 규칙 만들기  

##### <a name="to-create-a-central-access-rule"></a>중앙 액세스 규칙을 만들려면  

1. Active Directory 관리 센터의 왼쪽 창에서 **트리 보기**를 클릭합니다. 왼쪽 창에서 **동적 Access Control**을 클릭한 다음 **중앙 액세스 규칙**을 클릭합니다.  

2. **중앙 액세스 규칙**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **중앙 액세스 규칙**을 클릭합니다.  

3. **이름** 필드에 **AdatumEmployeeAccessRule**을 입력합니다.  

4. **사용 권한을** 섹션에서 **다음 권한을 현재 권한으로 사용** 옵션을 선택하고 **편집**을 클릭한 다음 **추가**를 클릭합니다. **보안 주체 선택** 링크를 클릭하고 **Authenticated Users**를 입력한 다음 **확인**을 클릭합니다.  

5. **Permission Entry for Permissions**(사용 권한의 사용 권한 항목) 대화 상자에서 **조건 추가**를 클릭하고 다음 조건을 입력합니다. [**User**] [**Company**] [**Equals**] [**Value**] [**Adatum**]. 사용 권한은 **수정, 읽기 및 실행, 읽기, 쓰기**여야 합니다.  

6. **확인**을 클릭합니다.  

7. **확인** 을 세 번 클릭하여 작업을 마치고 Active Directory 관리 센터로 돌아갑니다.  

   ![솔루션 가이드](media/Appendix-B--Setting-Up-the-Test-Environment/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em>***  

   다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  

   ```  
   New-ADCentralAccessRule `  
   -CurrentAcl:"O:SYG:SYD:AR(A;;FA;;;OW)(A;;FA;;;BA)(A;;FA;;;SY)(XA;;0x1301bf;;;AU;(@USER.ad://ext/Company:ContosoAdatum == `"Adatum`"))" `  
   -Name:"AdatumEmployeeAccessRule" `  
   -ProposedAcl:$null `  
   -ProtectedFromAccidentalDeletion:$true `  
   -Server:"contoso.com" `  
   ```  

### <a name="BKMK_2.10"></a>중앙 액세스 정책 만들기  

##### <a name="to-create-a-central-access-policy"></a>중앙 액세스 정책을 만들려면  

1.  관리자로 contoso.com에 로그인합니다.  

2.  Windows PowerShell에서 관리자 권한 명령 프롬프트를 열고 다음 코드를 붙여 넣습니다.  

    ```  
    New-ADCentralAccessPolicy "Adatum Only Access Policy"   
    Add-ADCentralAccessPolicyMember "Adatum Only Access Policy" `  
    -Member "AdatumEmployeeAccessRule" `  
    ```  

### <a name="BKMK_2.11"></a>그룹 정책을 통해 새 정책 게시  

##### <a name="to-apply-the-central-access-policy-across-file-servers-through-group-policy"></a>그룹 정책을 통해 파일 서버에서 중앙 액세스 정책을 적용하려면  

1.  **시작** 화면에서 **관리 도구**를 입력한 뒤 **검색** 표시줄에서 **설정**을 클릭합니다. **설정** 결과에서 **관리 도구**를 클릭합니다. **관리 도구** 폴더에서 그룹 정책 관리 콘솔을 엽니다.  

    > [!TIP]  
    > **PC 관리 도구 표시** 설정이 사용되지 않도록 설정된 경우 관리 도구 폴더 및 해당 콘텐츠가 **설정** 결과에 표시되지 않습니다.  

2.  Contoso.com 도메인을 마우스 오른쪽 단추로 클릭 하 여, **이 도메인에서 GPO를 만들고 여기에 연결**  

3.  GPO에 대한 설명이 포함된 이름(예: **AdatumAccessGPO**)을 입력하고 **확인**을 클릭합니다.  

##### <a name="to-apply-the-central-access-policy-to-the-file-server-through-group-policy"></a>그룹 정책을 통해 파일 서버에 중앙 액세스 정책을 적용하려면  

1.  **시작** 화면에서 **검색** 상자에 **그룹 정책 관리**를 입력합니다. 관리 도구 폴더에서 **그룹 정책 관리**를 엽니다.  

    > [!TIP]  
    > **PC 관리 도구 표시** 설정이 사용되지 않도록 설정된 경우 관리 도구 폴더 및 해당 콘텐츠가 설정 결과에 표시되지 않습니다.  

2.  그룹 정책 관리\포리스트: contoso.com\도메인\contoso.com으로 이동하여 Contoso를 선택합니다.  

3.  **AdatumAccessGPO** 정책을 마우스 오른쪽 단추로 클릭하고 **편집**을 선택합니다.  

4.  그룹 정책 관리 편집기에서 **컴퓨터 구성**을 클릭하고 **정책**, **Windows 설정**을 차례로 확장한 다음 **보안 설정**을 클릭합니다.  

5.  **파일 시스템**을 확장하고 **중앙 액세스 정책**을 마우스 오른쪽 단추로 클릭한 다음 **중앙 액세스 정책 관리**를 클릭합니다.  

6.  **중앙 액세스 정책 구성** 대화 상자에서 **추가**를 클릭하고 **Adatum 전용 액세스 정책**을 선택한 다음 **확인**을 클릭합니다.  

7.  그룹 정책 관리 편집기를 닫습니다. 이제 그룹 정책에 중앙 액세스 정책이 추가되었습니다.  

### <a name="BKMK_2.12"></a>파일 서버에서 Earnings 폴더 만들기  
FILE1에서 새 NTFS 볼륨을 만든 다음 D:\Earnings 폴더를 만듭니다.  

> [!NOTE]  
> 중앙 액세스 정책은 시스템 또는 부팅 볼륨 C:에는 기본적으로 사용되지 않습니다.  

### <a name="BKMK_2.13"></a>분류를 설정 하 고 Earnings 폴더에 중앙 액세스 정책 적용  

##### <a name="to-assign-the-central-access-policy-on-the-file-server"></a>파일 서버에서 중앙 액세스 정책을 할당하려면  

1. Hyper-V 관리자에서 FILE1 서버에 연결합니다. 암호를 사용 하 여 contoso\administrator로 로그인을 사용 하 여 서버에 로그인 <strong>pass@word1</strong>합니다.  

2. 관리자 권한 명령 프롬프트를 열고 **gpupdate /force**를 입력합니다. 그러면 그룹 정책 변경 내용이 서버에 적용됩니다.  

3. 또한 Active Directory에서 전역 리소스 속성을 새로 고쳐야 합니다. Windows PowerShell을 열고 `Update-FSRMClassificationpropertyDefinition`을 입력한 다음 Enter 키를 누릅니다. Windows PowerShell을 닫습니다.  

4. Windows 탐색기를 열고 D:\EARNINGS로 이동합니다. **Earnings** 폴더를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  

5. **분류** 탭을 클릭합니다. 회사를 선택한 다음 **값** 필드에서 **Adatum** 을 선택합니다.  

6. **변경**을 클릭하고 드롭다운 메뉴에서 **Adatum 전용 액세스 정책** 을 선택한 다음 **적용**을 클릭합니다.  

7. **보안** 탭, **고급**, **중앙 정책** 탭을 차례로 클릭합니다. **AdatumEmployeeAccessRule** 이 나열됩니다. 항목을 확장하여 Active Directory에서 규칙을 만들 때 설정한 모든 사용 권한을 볼 수 있습니다.  

8. **확인**을 클릭하여 Windows 탐색기로 돌아갑니다.  



