---
ms.assetid: 6b38480e-5b1c-49f0-9d46-8cf22f70f0d2
title: "Windows Server 2012 r 2에서 adfs 랩 환경을 설정합니다"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 049a1a1b0a419b0194edfe56b356a9f1e8b4b058
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="set-up-the-lab-environment-for-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 r 2에서 adfs 랩 환경을 설정합니다

>Windows Server 2012 r 2에 적용 됩니다.

이 항목을 간략하게 설명 단계를 완료 연습 다음 연습 가이드에 사용할 수 있는 테스트 환경을 구성할 수 있습니다.

-   [연습: Workplace Join는 iOS 디바이스와](../../ad-fs/operations/Walkthrough--Workplace-Join-with-an-iOS-Device.md)

-   [연습: Workplace Join 사용 하 여 Windows 장치](../../ad-fs/operations/Walkthrough--Workplace-Join-with-a-Windows-Device.md)


-   [연습 가이드: 관련 된 위험 조건부 액세스 제어도 관리](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)

-   [연습 가이드: 추가 다단계 인증 민감한 응용 프로그램에 대 한 위험을 관리](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

> [!NOTE]
> 웹 서버와 federation 서버 동일한 컴퓨터에 설치 하지 않는 것이 좋습니다.

이 테스트 환경으로 설정 하려면 다음 단계를 완료 합니다.

1.  [1 단계: 구성 도메인 컨트롤러 (d c 1)](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_1)

2.  [2 단계: 장치 등록 서비스와 federation 서버 (ADFS1) 구성](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)

3.  [3 단계: 구성 웹 서버 (WebServ1)와 샘플 클레임 기반 응용 프로그램](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_5)

4.  [4 단계: 구성 클라이언트 컴퓨터 (Client1)](../../ad-fs/deployment/../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_10)

## <a name="BKMK_1"></a>1 단계: 구성 도메인 컨트롤러 (d c 1)
이 테스트 환경을 위해 루트 Active Directory 도메인 호출할 수 **contoso.com** 지정 **pass@word1**관리자 암호를 합니다.

-   AD DS 역할 서비스를 설치 하 고 Active Directory Domain Services (AD DS) 컴퓨터가 도메인 컨트롤러에에서으로 Windows Server 2012 r 2를 설치 합니다. 이 작업을이 수행 도메인 컨트롤러 만들기의 일부로 서 사용자 AD DS 스키마를 업그레이드합니다. For more information and step-by-step instructions, see[https://technet.microsoft.com/ library/hh472162.aspx](https://technet.microsoft.com/library/hh472162.aspx).

### <a name="BKMK_2"></a>테스트 Active Directory 계정 만들기
도메인 컨트롤러가 기능을이 도메인에 있는 테스트 그룹과 테스트 사용자 계정 만들기 하 고 사용자 계정을 그룹 계정에 추가 수 있습니다. 이러한 계정을 사용 하 여 이전이 항목에서에서 참조 되는 연습 가이드의 연습을 완료 하려면.

다음과 같은 계정을 만듭니다.

-   사용자: **로버트 Hatley** 다음과 같은 자격 증명으로: 사용자 이름: **RobertH** 및 비밀 번호:**P@ssword**

-   그룹: **금융**

사용자 및 그룹 계정을 Active Directory (AD)를 만드는 방법에 대 한 정보를 참조 하세요. [https://technet.microsoft.com/library/cc783323%28v.aspx](https://technet.microsoft.com/library/cc783323%28v=ws.10%29.aspx)합니다.

추가 **로버트 Hatley** 계정에 **금융** 그룹입니다. For information on how to add a user to a group in Active Directory, see [https://technet.microsoft.com/library/cc737130%28v=ws.10%29.aspx](https://technet.microsoft.com/library/cc737130%28v=ws.10%29.aspx).

### <a name="create-a-gmsa-account"></a>GMSA 계정 만들기
AD FS(Active Directory Federation Services) 설치 및 구성 그룹 관리 서비스 계정 (GMSA) 계정이 필요 합니다.

##### <a name="to-create-a-gmsa-account"></a>GMSA 계정 만들기

1.  명령 창 Windows PowerShell 및 종류를 엽니다.

    ```
    Add-KdsRootKey -EffectiveTime (Get-Date).AddHours(-10)
    New-ADServiceAccount FsGmsa -DNSHostName adfs1.contoso.com -ServicePrincipalNames http/adfs1.contoso.com

    ```

## <a name="BKMK_4"></a>2 단계: 장치 등록 서비스를 사용 하 여 federation 서버 (ADFS1) 구성
To set up another virtual machine, install  Windows Server 2012 R2  and connect it to the domain **contoso.com**. Set up the computer after you have joined it to the domain, and then proceed to install and configure the AD FS role.

For a video, see [Active Directory Federation Services How-To Video Series: Installing an AD FS Server Farm](https://technet.microsoft.com/video/dn469436).

### <a name="install-a-server-ssl-certificate"></a>서버 SSL 인증서를 설치
로컬 컴퓨터 스토어에서 ADFS1 서버의 서버 Layer SSL (Secure Socket) 인증서를 설치 해야 합니다. 인증서에는 다음과 같은 특성 있어야 합니다.

-   adfs1.contoso.com 주체 이름 (CN):

-   adfs1.contoso.com 주제 대체 (DNS) 이름:

-   enterpriseregistration.contoso.com 주제 대체 (DNS) 이름:

For more information about setting up SSL certificates, see [Configure SSL/TLS on a Web site in the domain with an Enterprise CA](https://social.technet.microsoft.com/wiki/contents/articles/12485.configure-ssltls-on-a-web-site-in-the-domain-with-an-enterprise-ca.aspx).

[Active Directory Federation Services How-To Video Series: Updating Certificates](https://technet.microsoft.com/video/adfs-updating-certificates).

### <a name="install-the-ad-fs-server-role"></a>ADFS 서버 역할을 설치

##### <a name="to-install-the-federation-service-role-service"></a>Federation 서비스 역할 서비스를 설치 하려면

1.  도메인 관리자 계정을 사용 하 여 서버에 로그온 administrator@contoso.com합니다.

2.  서버 관리자를 시작 합니다. 서버 관리자를 시작 하려면 **서버 관리자** Windows에서 **시작** 화면, 키를 누르거나 **서버 관리자** Windows 데스크톱에서 Windows 작업 표시줄에서 합니다. 에 **빠른 시작** 탭에서 **시작** 타일에 **대시보드** 페이지, 클릭 **역할 및 기능을 추가**합니다. 클릭 수 있습니다 **역할 추가 및 기능** 에 **관리** 메뉴 합니다.

3.  에 **시작 하기 전에** 페이지, 클릭 **다음**합니다.

4.  에 **설치 유형을 선택** 페이지, 클릭 **역할 또는 기능 기반 설치**을 차례로 클릭 하 고 **다음**합니다.

5.  에 **선택 대상 서버** 페이지, 클릭 **서버 풀에서 서버를 선택**, 대상 컴퓨터를 선택한 다음 클릭 확인 **다음**합니다.

6.  에 **서버 역할 선택** 페이지, 클릭 **Active Directory Federation Services**, 클릭 한 다음 **다음**합니다.

7.  에 **기능 선택** 페이지, 클릭 **다음**합니다.

8.  에 **Active Directory Federation 서비스 (ADFS)** 페이지, 클릭 **다음**합니다.

9. 정보를 확인 한 후는 **설치 선택을 확인** 페이지를 선택 하 고는 **필요한 경우 자동으로 목적지 서버를 다시 시작** 확인란을 선택한 다음 클릭 **설치**합니다.

10. 에 **설치 진행률** 페이지 모든 올바르게 설치 되었는지 확인 한 다음 클릭 **닫기**합니다.

### <a name="configure-the-federation-server"></a>Federation 서버 구성
다음 단계 federation 서버 구성 하는 것입니다.

##### <a name="to-configure-the-federation-server"></a>Federation 서버 구성 하려면

1.  서버 관리자에서 **대시보드** 페이지, 클릭는 **알림**, 플래그 지정 및 클릭 한 다음 **서버의 federation 서비스 구성**합니다.

    **Active Directory Federation 서비스 구성 마법사** 열립니다.

2.  에 **시작** 페이지를 선택 하 고 **federation 서버 농장의 첫 번째 federation 서버를 만들**을 차례로 클릭 하 고 **다음**합니다.

3.  에 **AD DS에 연결** 페이지에서 계정에 대 한 도메인 관리자 권한으로 지정는 **contoso.com** 클릭 하 고이 컴퓨터에 가입 된 도메인 Active Directory **다음**합니다.

4.  에 **서비스 속성 지정** 페이지에서 다음을 수행 하 고 클릭 한 다음 **다음 **:

    -   이전 가져온 SSL 인증서를 가져옵니다. 이 인증서가 필요한 서비스 인증 인증서 합니다. SSL 인증서의 위치를 찾습니다.

    -   To provide a name for your federation service, type **adfs1.contoso.com**. This value is the same value that you provided when you enrolled an SSL certificate in Active Directory Certificate Services (AD CS).

    -   를 제공 하기 위해 federation 서비스의 표시 이름을 입력 **Contoso Corporation**합니다.

5.  에 **서비스 계정 지정** 페이지를 선택 하 고 **기존 도메인 사용자 계정을 사용 하거나, 그룹 관리 서비스 계정**, 한 다음 지정 GMSA 계정 **fsgmsa** 도메인 컨트롤러를 만들 때 만들었다고 합니다.

6.  에 **구성 데이터베이스 지정** 페이지를 선택 하 고 **Windows 내부 데이터베이스를 사용 하 여이 서버의 데이터베이스를 만듭니다**, 클릭 한 다음 **다음**합니다.

7.  에 **리뷰 옵션** 페이지 구성 선택을 확인 하 고 클릭 한 다음 **다음**합니다.

8.  에 **전 필수 조건 검사** 페이지에서 확인 모든 필수 검사 성공적으로 완료 한 다음 클릭 **구성**합니다.

9. 에 **결과** 페이지 검토 하 고 결과 구성 성공적으로 완료 있는지 여부를 확인 하 고 클릭 한 다음 **다음 단계를 완료 federation 서비스 배포 하는 데 필요한**합니다.

### <a name="configure-device-registration-service"></a>디바이스 등록 서비스 구성
다음 단계 ADFS1 서버에 등록 서비스 디바이스를 구성 하는 것입니다. For a video, see [Active Directory Federation Services How-To Video Series: Enabling the Device Registration Service](https://technet.microsoft.com/video/adfs-how-to-enabling-the-device-registration-service).

##### <a name="to-configure-device-registration-service-for-windows-server-2012-rtm"></a>디바이스 등록 서비스에 대 한 Windows Server 2012 RTM 구성 하려면

1.  > [!IMPORTANT]
    > **Windows Server 2012 r 2 RTM 빌드에는 다음과 같은 단계 적용 됩니다.**

    명령 창 Windows PowerShell 및 종류를 엽니다.

    ```
    Initialize-ADDeviceRegistration
    ```

    서비스 계정에 대 한 메시지가 표시 되 면 입력 **contoso\fsgmsa$**합니다.

    이제 Windows PowerShell cmdlet을 실행 합니다.

    ```
    Enable-AdfsDeviceRegistration
    ```

2.  ADFS1 서버에서에 **AD FS 관리** 콘솔,으로 이동 **인증 정책**합니다. 선택 **전 세계 주요 인증 편집**합니다. 옆에 있는 확인란을 선택 **디바이스 인증 사용**을 차례로 클릭 하 고 **확인**합니다.

### <a name="add-host-a-and-alias-cname-resource-records-to-dns"></a>DNS (A 호스트) 및 리소스 별칭 (CNAME) 레코드가 추가
D c 1에서 다음과 같은 시스템 DNS (도메인 이름) 레코드가 디바이스 등록 서비스에 대 한 생성 해야 합니다.

|항목|입력|주소|
|---------|--------|-----------|
|adfs1|호스트 (A)|ADFS server의 IP 주소|
|enterpriseregistration|별칭 (CNAME)|adfs1.contoso.com|

다음 절차 호스트 (는) 리소스 레코드 회사 DNS 이름 서버 federation 서버와 디바이스 등록 서비스에 대 한 추가를 사용할 수 있습니다.

해당 하는 또는 관리자가 그룹 구성원이이 절차를 수행 하는 최소 요구 사항을입니다. Review details about using the appropriate accounts and group memberships in the  HYPERLINK "https://go.microsoft.com/fwlink/?LinkId=83477" Local and Domain Default Groups (https://go.microsoft.com/fwlink/p/?LinkId=83477).

##### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>해당 federation 서버에 대 한 호스트 (는) 및 (CNAME) 별칭 리소스 레코드 DNS에 추가 하려면

1.  서버 관리자에서 d c 1에서에 **도구** 메뉴를 클릭 **DNS** DNS 스냅인 열려면 합니다.

2.  콘솔 트리에서 d c 1, **앞 조회 영역이**를 마우스 오른쪽 단추로 클릭 **contoso.com**을 차례로 클릭 하 고 **새 호스트 A 등의 AAAA**합니다.

3.  **이름,** ADFS 농장을 사용 하 여 원하는 이름을 입력 합니다. 입력이 연습 **adfs1**합니다.

4.  **IP 주소**, ADFS1 서버의 IP 주소를 입력 합니다. 클릭 **호스트 추가**합니다.

5.  마우스 오른쪽 단추로 클릭 **contoso.com**을 차례로 클릭 하 고 **새 별칭 (CNAME)**합니다.

6.  에 **새 리소스 레코드** 대화 상자, 입력 **enterpriseregistration** 에 **별칭 이름** 상자 합니다.

7.  된 적격 도메인 이름 (FQDN) 대상 호스트 상자의 입력 **adfs1.contoso.com**을 차례로 클릭 하 고 **확인**합니다.

    > [!IMPORTANT]
    > 실제 배포 회사에 여러 사용자 UPN 계정 이름 () 접미사 경우 dns에서 이러한 UPN 접미사 각각에 대 한 여러 CNAME 레코드를 만들어 해야 합니다.

## <a name="BKMK_5"></a>3 단계: 구성 웹 서버 (WebServ1)와 샘플 클레임 기반 응용 프로그램
Set up a virtual machine (WebServ1) by installing the  Windows Server 2012 R2  operating system and connect it to the domain **contoso.com**. After it is joined to the domain, you can proceed to install and configure the Web Server role.

앞에서 설명한 참조 된 연습을 완료 하려면 해당 federation 서버 (ADFS1)으로 보호 된 샘플 응용 프로그램이 있어야 합니다.

You can download Windows Identity Foundation SDK ([https://www.microsoft.com/download/details.aspx?id=4451](https://www.microsoft.com/download/details.aspx?id=4451), which includes a sample claims-based application.

이 샘플 클레임 기반 응용 프로그램 사용 하는 웹 서버를 설정 하려면 다음 단계를 완료 해야 합니다.

> [!NOTE]
> 이러한 단계는 Windows Server 2012 r 2 운영 체제를 실행 하는 웹 서버에 거친 합니다.

1.  [웹 서버 역할와 Windows 신원 파운데이션 설치](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_15)

2.  [Windows 신원을 파운데이션 SDK 설치](../../ad-fs/deployment/../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_13)

3.  [IIS에서 간단한 클레임 앱을 구성 합니다.](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_9)

4.  [해당 federation 서버에 신뢰 파티 신뢰 만들기](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_11)

### <a name="BKMK_15"></a>웹 서버 역할와 Windows 신원을 파운데이션 설치

1.  > [!NOTE]
    > Windows Server 2012 r 2 설치 미디어에 액세스할 수 있어야 합니다.

    사용 하 여 WebServ1 로그온 **administrator@contoso.com**및 암호 **pass@word1**합니다.

2.  서버 관리자에서에 **빠른 시작** 탭에서 **시작** 타일에 **대시보드** 페이지, 클릭 **역할 및 기능을 추가**합니다. 클릭 수 있습니다 **역할 추가 및 기능** 에 **관리** 메뉴 합니다.

3.  에 **시작 하기 전에** 페이지, 클릭 **다음**합니다.

4.  에 **설치 유형을 선택** 페이지, 클릭 **역할 또는 기능 기반 설치**을 차례로 클릭 하 고 **다음**합니다.

5.  에 **선택 대상 서버** 페이지, 클릭 **서버 풀에서 서버를 선택**, 대상 컴퓨터를 선택한 다음 클릭 확인 **다음**합니다.

6.  에 **서버 역할을 선택할** 페이지에서 옆에 있는 확인란을 선택 **웹 IIS ()**, 클릭 **기능 추가**, 클릭 한 다음 **다음**합니다.

7.  에 **기능을 선택** 페이지에서 선택 **Windows 신원을 Foundation 3.5**을 차례로 클릭 하 고 **다음**합니다.

8.  에 **웹 역할 IIS ()** 페이지, 클릭 **다음**합니다.

9. 에 **역할 서비스 선택** 페이지를 선택 하 고, 확장 **응용 프로그램을 개발**합니다. 선택 **ASP.NET 3.5**, 클릭 **기능 추가**을 차례로 클릭 하 고 **다음**합니다.

10. 에 **설치 선택을 확인** 페이지, 클릭 **다른 소스 경로 지정할**합니다. Windows Server 2012 r 2 설치 미디어에 있는 Sxs 디렉터리에 경로 입력 합니다. 예를 들어 D:\Sources\Sxs 합니다. 클릭 **확인**을 차례로 클릭 하 고 **설치**합니다.

### <a name="BKMK_13"></a>Windows 신원을 파운데이션 SDK 설치

1.  Run WindowsIdentityFoundation-SDK-3.5.msi to install Windows Identity Foundation SDK 3.5 (https://www.microsoft.com/download/details.aspx?id=4451). 기본 옵션을 모두 선택 합니다.

### <a name="BKMK_9"></a>IIS에서 간단한 클레임 앱을 구성 합니다.

1.  컴퓨터 인증서 저장소에서 유효한 SSL 인증서를 설치 합니다. 인증서 웹 서버의 이름을 들어 **webserv1.contoso.com**합니다.

2.  C:\Program Files (x86) \Windows Identity Foundation SDK\v3.5\Samples\Quick Start\Web Application\PassiveRedirectBasedClaimsAwareWebApp의 내용을 C:\Inetpub\Claimapp에 복사 합니다.

3.  편집는 **Default.aspx.cs** 파일 수행 필터링 청구 되지 않습니다. 이 단계 수행 되어 샘플 응용 프로그램은 federation 서버에서 발급 한 모든 클레임 표시 되는지 확인 합니다. 다음을 수행 합니다.

    1.  열린 **Default.aspx.cs** 텍스트 편집기에 있습니다.

    2.  두 번째에 대 한 파일을 검색 `ExpectedClaims`합니다.

    3.  전체 아웃 메모 `IF`정책 및 해당 괄호 합니다. 입력 하 여 의견을 나타냅니다 "/ /" (따옴표 제외)를 줄의 시작 부분에 있습니다.

    4.  사용자 `FOREACH`문을 코드는 다음과 비슷합니다 이제 해야 합니다.

        ```
        Foreach (claim claim in claimsIdentity.Claims)
        {
           //Before showing the claims validate that this is an expected claim
           //If it is not in the expected claims list then don't show it
           //if (ExpectedClaims.Contains( claim.ClaimType ) )
           // {
              writeClaim( claim, table );
           //}
        }

        ```

    5.  저장 하 고 닫기 **Default.aspx.cs**합니다.

    6.  열린 **web.config** 텍스트 편집기에 있습니다.

    7.  전체를 제거 `<microsoft.identityModel>`섹션. 시작의 모든 항목 제거 `including <microsoft.identityModel>`최대 및 포함 `</microsoft.identityModel>`합니다.

    8.  저장 하 고 닫기 **web.config**합니다.

4.  **구성 IIS 관리자**

    1.  열린 **인터넷 정보 서비스 (IIS) 관리자**합니다.

    2.  로 이동 **응용 프로그램 풀**를 마우스 오른쪽 단추로 클릭 **DefaultAppPool** 선택 **고급 설정**합니다. 설정 **로드 사용자 프로필** 에 **진정한**을 차례로 클릭 하 고 **확인**합니다.

    3.  마우스 오른쪽 단추로 클릭 **DefaultAppPool** 선택 **기본 설정을**합니다. 변경은 **.NET CLR 버전** 에 **.NET CLR 버전 v2.0.50727**합니다.

    4.  마우스 오른쪽 단추로 클릭 **기본 웹 사이트** 선택 **바인딩 편집**합니다.

    5.  추가 된 **HTTPS** 포트 구속력 **443** 사용자가 설치한 SSL 인증서를 사용 합니다.

    6.  마우스 오른쪽 단추로 클릭 **기본 웹 사이트** 선택 **응용 프로그램 추가**합니다.

    7.  별칭으로 설정 **claimapp** 및의 실제 경로를 **c:\inetpub\claimapp**합니다.

5.  구성 하려면 **claimapp** 해당 federation 서버를 사용 하려면 다음을 수행 합니다.

    1.  FedUtil.exe에 있는 실행 **C:\Program Files (x86) \Windows Identity Foundation SDK\v3.5**합니다.

    2.  응용 프로그램 구성 위치 설정 **C:\inetput\claimapp\web.config** 사이트의 URL을 URI 응용 프로그램을 설정 하 고 **https://webserv1.contoso.com /claimapp/**합니다. 클릭 **다음**합니다.

    3.  선택 **사용 하 여 기존 STS** ADFS 서버의 메타 데이터 URL로 이동 하 고 **https://adfs1.contoso.com/federationmetadata/2007-06/federationmetadata.xml**합니다. 클릭 **다음**합니다.

    4.  선택 **인증서 체인 유효성 검사를 사용 하지 않도록 설정**을 차례로 클릭 하 고 **다음**합니다.

    5.  선택 **암호화**을 차례로 클릭 하 고 **다음**합니다. 에 **클레임 제공** 페이지, 클릭 **다음**합니다.

    6.  옆에 있는 확인란을 선택 **매일 업데이트 합니다. WS Federation 메타 데이터를 수행 하는 작업을 예약**합니다. 클릭 **완료**합니다.

    7.  이제 샘플 신청서 구성 됩니다. URL 응용 프로그램을 테스트 하는 경우 **https://webserv1.contoso.com/claimapp**, 해당 federation 서버에 사용자를 이동 해야 합니다. Federation 서버 신뢰 파티 신뢰 구성 되지 않으므로 오류 페이지가 표시 됩니다. 즉, ADFS 하 여 테스트 응용 프로그램을 보호 하지 했습니다.

이제 ADFS 사용 하 여 웹 서버에서 실행 되 고 샘플 응용 프로그램을 보호 해야 합니다. 이렇게 하려면 해당 federation 서버 (ADFS1)에 신뢰 파티 신뢰를 추가 합니다. For a video, see [Active Directory Federation Services How-To Video Series: Add a Relying Party Trust](https://technet.microsoft.com/video/adfs-how-to-add-a-relying-party-trust).

### <a name="BKMK_11"></a>해당 federation 서버에 신뢰 파티 신뢰 만들기

1.  서버의 하면 federation (ADFS1)에 **광고 FS Management console**로 이동 **파티 신뢰를 사용 하지 않고**, 차례로 클릭 하 고 **의존 파티 신뢰 추가**합니다.

2.  에 **데이터 소스를 선택** 페이지 선택, **당사자에 대 한 데이터 가져오기 게시 로컬 네트워크 또는 온라인**, 메타 데이터 URL을 입력 **claimapp**, 클릭 한 다음 **다음**합니다. FedUtil.exe 실행 메타 데이터.xml 파일을 만들었습니다. 위치는 **https://webserv1.contoso.com/claimapp/federationmetadata/2007-06/federationmetadata.xml**합니다.

3.  에 **표시 이름 지정** 페이지에서 지정는 **표시 이름** 에 대 한 여러분의 신뢰 파티 신뢰 **claimapp**을 차례로 클릭 하 고 **다음**합니다.

4.  에 **다중 요소 인증 이제 구성? **페이지를 선택 하 고 **이 이번에이 신뢰 파티 보안에 대 한 다단계 인증 설정을 지정 하려면 하지 않을**을 차례로 클릭 하 고 **다음**합니다.

5.  에 **발급 승인 규칙 선택** 페이지를 선택 하 고 **모든 사용자가이 당사자에 액세스 하도록 허용**, 클릭 한 다음 **다음**합니다.

6.  에 **신뢰 추가 준비가** 페이지, 클릭 **다음**합니다.

7.  에 **편집 클레임 규칙** 대화 상자를 클릭 **규칙 추가**합니다.

8.  에 **규칙 유형을 선택** 페이지를 선택 하 고 **클레임 사용자 지정 규칙을 사용 하 여 보낼**를 차례로 클릭 하 고 **다음**합니다.

9. 에 **구성 클레임 규칙** 페이지에 **클레임 규칙 이름** 상자에 입력 **모든 클레임**합니다. 에 **사용자 지정 규칙** 상자에 다음 청구 규칙을 입력 합니다.

    ```
    c:[ ]
    => issue(claim = c);

    ```

10. 클릭 **완료**을 차례로 클릭 하 고 **확인**합니다.

## <a name="BKMK_10"></a>4 단계: 구성 클라이언트 컴퓨터 (Client1)
다른 가상 컴퓨터를 설정 하 고.1 Windows 8을 설치 합니다. 이 가상 컴퓨터의 다른 컴퓨터와 동일한 가상 네트워크에 있어야 합니다. 이 컴퓨터에서 Contoso 도메인에 가입 하지 해야 합니다.

설정에서 federation 서버 (ADFS1)에 대 한 사용 되는 SSL 인증서 신뢰 해야 [2 단계: 장치 등록 서비스와 federation 서버 (ADFS1) 구성](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)합니다. 인증서에 대 한 인증서 해지 정보 확인에 수 있어야 합니다.

또한 해야를 설정 하 고 Client1에 로그온 할 때 Microsoft 계정을 사용 합니다.

## <a name="see-also"></a>참조 하십시오


- [Active Directory Federation Services 설치 AD FS 서버 팜 비디오 시리즈 방법:](https://technet.microsoft.com/video/dn469436)
- [Active Directory Federation Services 인증서를 업데이트 하는 비디오 시리즈 방법:](https://technet.microsoft.com/video/adfs-updating-certificates)
- [Active Directory Federation Services 추가 신뢰 파티 신뢰 비디오 시리즈 방법:](https://technet.microsoft.com/video/adfs-how-to-add-a-relying-party-trust)
- [Active Directory Federation Services 디바이스 등록 서비스를 사용 하는 비디오 시리즈 방법:](https://technet.microsoft.com/video/adfs-how-to-enabling-the-device-registration-service)
- [Active Directory Federation Services 설치 웹 응용 프로그램 프록시 비디오 시리즈 방법:](https://technet.microsoft.com/video/dn469438)



