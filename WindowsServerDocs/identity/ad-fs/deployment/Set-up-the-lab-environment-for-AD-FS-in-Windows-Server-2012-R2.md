---
ms.assetid: 6b38480e-5b1c-49f0-9d46-8cf22f70f0d2
title: Windows Server 2012 R2의 AD FS에 대한 랩 환경 설정
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 52199ab8ca6f82443e78e72c6980746fa561363a
ms.sourcegitcommit: 06ae7c34c648538e15c4d9fe330668e7df32fbba
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78371675"
---
# <a name="set-up-the-lab-environment-for-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 R2의 AD FS에 대한 랩 환경 설정


이 항목에서는 다음 연습 가이드의 연습을 완료하는 데 사용할 수 있는 테스트 환경을 구성하는 단계에 대해 간략히 설명합니다.

-   [연습: iOS 장치를 사용 하 여 Workplace Join](../../ad-fs/operations/Walkthrough--Workplace-Join-with-an-iOS-Device.md)

-   [연습: Windows 장치를 사용 하 여 Workplace Join](../../ad-fs/operations/Walkthrough--Workplace-Join-with-a-Windows-Device.md)


-   [연습 가이드: 조건부 Access Control를 사용 하 여 위험 관리](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)

-   [연습 가이드: 중요 한 응용 프로그램에 대 한 추가 Multi-Factor Authentication로 위험 관리](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

> [!NOTE]
> 웹 서버와 페더레이션 서버를 동일한 컴퓨터에 설치하지 않는 것이 좋습니다.

이 테스트 환경을 설정하려면 다음 단계를 완료합니다.

1.  [1 단계: 도메인 컨트롤러 (DC1) 구성](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_1)

2.  [2 단계: Device Registration Service를 사용 하 여 페더레이션 서버 (ADFS1) 구성](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)

3.  [3 단계: 웹 서버 (WebServ1) 및 샘플 클레임 기반 응용 프로그램 구성](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_5)

4.  [4 단계: 클라이언트 컴퓨터 (Client1) 구성](../../ad-fs/deployment/../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_10)

## <a name="BKMK_1"></a>1 단계: 도메인 컨트롤러 (DC1) 구성
이 테스트 환경의 목적을 위해 루트 Active Directory 도메인 **contoso.com** 를 호출 하 고 <strong>pass@word1</strong> 을 관리자 암호로 지정할 수 있습니다.

-   AD DS 역할 서비스를 설치 하 고 Active Directory Domain Services (AD DS)를 설치 하 여 Windows Server 2012 r 2에서 컴퓨터를 도메인 컨트롤러로 만듭니다. 이 작업을 수행 하면 도메인 컨트롤러 만들기의 일부로 AD DS 스키마가 업그레이드 됩니다. 자세한 내용 및 단계별 지침은[https://technet.microsoft.com/library/hh472162.aspx](https://technet.microsoft.com/library/hh472162.aspx)를 참조 하세요.

### <a name="BKMK_2"></a>테스트 Active Directory 계정 만들기
도메인 컨트롤러가 작동하면 이 도메인에서 테스트 그룹 및 테스트 사용자 계정을 만들고 해당 사용자 계정을 그룹 계정에 추가할 수 있습니다. 이러한 계정을 사용하여 이 항목의 앞부분에 언급된 연습 가이드의 연습을 완료합니다.

다음 계정을 만듭니다.

- 사용자: 다음 자격 증명을 사용 하는 **Robert Hatley** : 사용자 이름: **roberth** 및 암호: <strong>P@ssword</strong>

- 그룹: **Finance**

AD (Active Directory)에서 사용자 및 그룹 계정을 만드는 방법에 대 한 자세한 내용은 [https://technet.microsoft.com/library/cc783323%28v.aspx](https://technet.microsoft.com/library/cc783323%28v=ws.10%29.aspx)을 참조 하세요.

**Robert Hatley** 계정을 **Finance** 그룹에 추가합니다. Active Directory에서 그룹에 사용자를 추가 하는 방법에 대 한 자세한 내용은 [https://technet.microsoft.com/library/cc737130%28v=ws.10%29.aspx](https://technet.microsoft.com/library/cc737130%28v=ws.10%29.aspx)을 참조 하세요.

### <a name="create-a-gmsa-account"></a>GMSA 계정 만들기
GMSA (그룹 관리 서비스 계정) 계정은 Active Directory Federation Services (AD FS) 설치 및 구성 중에 필요 합니다.

##### <a name="to-create-a-gmsa-account"></a>GMSA 계정을 만들려면

1.  Windows PowerShell 명령 창을 열고 다음을 입력합니다.

    ```
    Add-KdsRootKey -EffectiveTime (Get-Date).AddHours(-10)
    New-ADServiceAccount FsGmsa -DNSHostName adfs1.contoso.com -ServicePrincipalNames http/adfs1.contoso.com

    ```

## <a name="BKMK_4"></a>2 단계: Device Registration Service를 사용 하 여 페더레이션 서버 (ADFS1) 구성
다른 가상 컴퓨터를 설정 하려면 Windows Server 2012 r 2를 설치 하 고이를 도메인 **contoso.com**에 연결 합니다. 도메인에 가입한 후 컴퓨터를 설정 하 고 AD FS 역할 설치 및 구성을 계속 진행 합니다.

비디오는 [Active Directory Federation Services How-To Video Series: Installing an AD FS Server Farm(Active Directory Federation Services 방법 비디오 시리즈: AD FS 서버 팜 설치)](https://technet.microsoft.com/video/dn469436)을 참조하세요.

### <a name="install-a-server-ssl-certificate"></a>서버 SSL 인증서 설치
ADFS1 서버의 로컬 컴퓨터 저장소에 서버 SSL(Secure Socket Layer) 인증서를 설치해야 합니다. 인증서에는 다음 특성이 있어야 합니다.

-   주체 이름(CN): adfs1.contoso.com

-   주체 대체 이름(DNS): adfs1.contoso.com

-   주체 대체 이름(DNS): enterpriseregistration.contoso.com

SSL 인증서를 설정하는 방법에 대한 자세한 내용은 [엔터프라이즈 CA를 사용하여 도메인의 웹 사이트에서 SSL/TLS 구성](https://social.technet.microsoft.com/wiki/contents/articles/12485.configure-ssltls-on-a-web-site-in-the-domain-with-an-enterprise-ca.aspx)(영문)을 참조하세요.

[Active Directory Federation Services How-To Video Series: Updating Certificates(Active Directory Federation Services 방법 비디오 시리즈: 인증서 업데이트)](https://technet.microsoft.com/video/adfs-updating-certificates).

### <a name="install-the-ad-fs-server-role"></a>AD FS 서버 역할 설치

##### <a name="to-install-the-federation-service-role-service"></a>페더레이션 서비스 역할 서비스를 설치하려면

1. 도메인 관리자 계정 administrator@contoso.com를 사용 하 여 서버에 로그온 합니다.

2. 서버 관리자를 시작합니다. 서버 관리자를 시작하려면 Windows **시작** 화면에서 **서버 관리자**를 클릭하거나 Windows 바탕 화면의 Windows 작업 표시줄에서 **서버 관리자**를 클릭합니다. **대시보드** 페이지의 **시작** 타일에 있는 **빠른 시작** 탭에서 **역할 및 기능 추가**를 클릭합니다. **관리** 메뉴에서 **역할 및 기능 추가**를 클릭해도 됩니다.

3. **시작하기 전에** 페이지에서 **다음**을 클릭합니다.

4. **설치 유형 선택** 페이지에서 **역할 기반 또는 기능 기반 설치**를 클릭한 다음 **다음**을 클릭합니다.

5. **대상 서버 선택** 페이지에서 **서버 풀에서 서버 선택**을 클릭하고 대상 컴퓨터가 선택되어 있는지 확인한 후 **다음**을 클릭합니다.

6. **서버 역할 선택** 페이지에서 **Active Directory Federation Services**를 클릭하고 **다음**을 클릭합니다.

7. **기능 선택** 페이지에서 **다음**을 클릭합니다.

8. **AD FS(Active Directory Federation Services)** 페이지에서 **다음**을 클릭합니다.

9. **설치 선택 확인** 페이지의 정보를 확인하고 **필요한 경우 자동으로 대상 서버 다시 시작** 확인란을 선택한 후에 **설치**를 클릭합니다.

10. **설치 진행률** 페이지에서 모든 항목이 올바르게 설치되었는지 확인하고 **닫기**를 클릭합니다.

### <a name="configure-the-federation-server"></a>페더레이션 서버 구성
다음 단계에서는 페더레이션 서버를 구성합니다.

##### <a name="to-configure-the-federation-server"></a>페더레이션 서버를 구성하려면

1.  서버 관리자 **대시보드** 페이지에서 **알림** 플래그를 클릭한 다음 **이 서버에 페더레이션 서비스를 구성하세요.** 을 클릭합니다.

    **Active Directory Federation Service 구성 마법사**가 열립니다.

2.  **시작** 페이지에서 **페더레이션 서버 팜에 첫 번째 페더레이션 서버를 만듭니다.** 를 선택하고 **다음**을 클릭합니다.

3.  **AD DS에 연결** 페이지에서 이 컴퓨터가 가입된 **contoso.com** Active Directory 도메인에 대한 도메인 관리자 권한이 있는 계정을 지정하고 **다음**을 클릭합니다.

4.  **서비스 속성 지정** 페이지에서 다음을 수행한 후 **다음**을 클릭합니다.

    -   이전에 얻은 SSL 인증서를 가져옵니다. 이 인증서는 필수 서비스 인증 인증서입니다. SSL 인증서의 위치를 찾아봅니다.

    -   페더레이션 서비스의 이름을 제공하기 위해 **adfs1.contoso.com**을 입력합니다. 이 값은 AD CS(Active Directory 인증서 서비스)에 SSL 인증서를 등록할 때 지정한 것과 동일한 값입니다.

    -   페더레이션 서비스의 표시 이름을 제공하기 위해 **Contoso Corporation**을 입력합니다.

5.  **서비스 계정 지정** 페이지에서 **기존 도메인 사용자 계정 또는 그룹 관리 서비스 계정 사용**을 선택하고 도메인 컨트롤러를 만들 때 만든 GMSA 계정 **fsgmsa**를 지정합니다.

6.  **구성 데이터베이스 지정** 페이지에서 **Windows 내부 데이터베이스를 사용하여 이 서버에 데이터베이스를 만듭니다.** 를 선택하고 **다음**을 클릭합니다.

7.  **검토 옵션** 페이지에서 구성 선택 사항을 확인하고 **다음**을 클릭합니다.

8.  **필수 조건 확인** 페이지에서 모든 필수 구성 요소 검사가 성공적으로 완료되었는지 확인하고 **구성**을 클릭합니다.

9. **결과** 페이지에서 결과를 검토하고 구성이 성공적으로 완료되었는지 확인한 다음 **페더레이션 서비스 배포를 완료하는 데 필요한 다음 단계**를 클릭합니다.

### <a name="configure-device-registration-service"></a>Device Registration Service 구성
다음 단계에서는 ADFS1 서버에서 Device Registration Service를 구성합니다. 비디오는 [Active Directory Federation Services How-To Video Series: Enabling the Device Registration Service(Active Directory Federation Services 방법 비디오 시리즈: Device Registration Service 사용)](https://technet.microsoft.com/video/adfs-how-to-enabling-the-device-registration-service)를 참조하세요.

##### <a name="to-configure-device-registration-service-for-windows-server-2012-rtm"></a>Windows Server 2012 RTM에 대한 Device Registration Service를 구성하려면

1.  > [!IMPORTANT]
    > **다음 단계는 Windows Server 2012 R2 RTM 빌드에 적용 됩니다.**

    Windows PowerShell 명령 창을 열고 다음을 입력합니다.

    ```
    Initialize-ADDeviceRegistration
    ```

    서비스 계정을 묻는 메시지가 표시되면 **contoso\fsgmsa$** 를 입력합니다.

    이제 Windows PowerShell cmdlet을 실행 합니다.

    ```
    Enable-AdfsDeviceRegistration
    ```

2.  ADFS1 서버의 **AD FS 관리** 콘솔에서 **인증 정책**으로 이동합니다. **전역 기본 인증 편집**을 선택합니다. **장치 인증 사용** 옆의 확인란을 선택하고 **확인**을 클릭합니다.

### <a name="add-host-a-and-alias-cname-resource-records-to-dns"></a>DNS에 호스트(A) 및 별칭(CNAME) 리소스 레코드 추가
DC1에서 다음 DNS(Domain Name System) 레코드가 Device Registration Service에 대해 만들어졌는지 확인해야 합니다.

|항목|형식|Address|
|---------|--------|-----------|
|adfs1|호스트(A)|AD FS 서버의 IP 주소|
|enterpriseregistration|별칭(CNAME)|adfs1.contoso.com|

다음 절차를 사용하여 페더레이션 서버 및 Device Registration Service용 회사 DNS 이름 서버에 호스트(A) 리소스 레코드를 추가할 수 있습니다.

이 절차를 완료하려면 최소한 Administrators 또는 이와 동등한 그룹 구성원 자격이 필요합니다. 하이퍼링크 "<https://go.microsoft.com/fwlink/?LinkId=83477>" 로컬 및 도메인 기본 그룹 (<https://go.microsoft.com/fwlink/p/?LinkId=83477>)에서 적절 한 계정 및 그룹 구성원 자격 사용에 대 한 세부 정보를 검토 합니다.

##### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>페더레이션 서버에 대한 DNS에 호스트(A) 및 별칭(CNAME) 리소스 레코드를 추가하려면

1.  DC1의 서버 관리자 **도구** 메뉴에서 **DNS**를 클릭하여 DNS 스냅인을 엽니다.

2.  콘솔 트리에서 DC1과 **정방향 조회 영역**을 확장하고 **contoso.com**을 마우스 오른쪽 단추로 클릭한 후 **새 호스트(A 또는 AAAA)** 를 클릭합니다.

3.  **이름**에 AD FS 팜에 사용할 이름을 입력합니다. 이 연습에서는 **adfs1**을 입력합니다.

4.  **IP 주소**에 ADFS1 서버의 IP 주소를 입력합니다. **호스트 추가**를 클릭합니다.

5.  **contoso.com**을 마우스 오른쪽 단추로 클릭하고 **새 별칭(CNAME)** 을 클릭합니다.

6.  **새 리소스 레코드** 대화 상자의 **별칭 이름** 상자에 **enterpriseregistration**을 입력합니다.

7.  대상 호스트 상자의 FQDN(정규화된 도메인 이름)에 **adfs1.contoso.com**을 입력하고 **확인**을 클릭합니다.

    > [!IMPORTANT]
    > 실제 배포에서는 회사에 여러 UPN(사용자 계정 이름) 접미사가 있는 경우 DNS의 각 UPN 접미사마다 하나씩 여러 CNAME 레코드를 만들어야 합니다.

## <a name="BKMK_5"></a>3 단계: 웹 서버 (WebServ1) 및 샘플 클레임 기반 응용 프로그램 구성
Windows Server 2012 R2 운영 체제를 설치 하 고 도메인 **contoso.com**에 연결 하 여 가상 컴퓨터 (WebServ1)를 설정 합니다. 도메인에 가입한 후에는 웹 서버 역할 설치 및 구성을 계속 진행할 수 있습니다.

이 항목의 앞부분에 언급된 연습을 완료하려면 페더레이션 서버(ADFS1)로 보호된 예제 애플리케이션이 있어야 합니다.

샘플 클레임 기반 응용 프로그램을 포함 하는 Windows Identity Foundation SDK ([https://www.microsoft.com/download/details.aspx?id=4451](https://www.microsoft.com/download/details.aspx?id=4451)를 다운로드할 수 있습니다.

이 예제 클레임 기반 애플리케이션으로 웹 서버를 설정하려면 다음 단계를 완료해야 합니다.

> [!NOTE]
> 이러한 단계는 Windows Server 2012 R2 운영 체제를 실행 하는 웹 서버에서 테스트 되었습니다.

1.  [웹 서버 역할 및 Windows Identity Foundation 설치](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_15)

2.  [Windows Identity Foundation SDK 설치](../../ad-fs/deployment/../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_13)

3.  [IIS에서 간단한 클레임 응용 프로그램 구성](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_9)

4.  [페더레이션 서버에서 신뢰 당사자 트러스트 만들기](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_11)

### <a name="BKMK_15"></a>웹 서버 역할 및 Windows Identity Foundation 설치

1. > [!NOTE]
   > Windows Server 2012 R2 설치 미디어에 대 한 액세스 권한이 있어야 합니다.

   <strong>administrator@contoso.com</strong> 및 암호 <strong>pass@word1</strong>를 사용 하 여 WebServ1에 로그온 합니다.

2. 서버 관리자 **대시보드** 페이지의 **시작** 타일에 있는 **빠른 시작** 탭에서 **역할 및 기능 추가**를 클릭합니다. **관리** 메뉴에서 **역할 및 기능 추가**를 클릭해도 됩니다.

3. **시작하기 전에** 페이지에서 **다음**을 클릭합니다.

4. **설치 유형 선택** 페이지에서 **역할 기반 또는 기능 기반 설치**를 클릭한 다음 **다음**을 클릭합니다.

5. **대상 서버 선택** 페이지에서 **서버 풀에서 서버 선택**을 클릭하고 대상 컴퓨터가 선택되어 있는지 확인한 후 **다음**을 클릭합니다.

6. **서버 역할 선택** 페이지에서 **웹 서버(IIS)** 옆의 확인란을 선택하고 **기능 추가**를 클릭한 후 **다음**을 클릭합니다.

7. **기능 선택** 페이지에서 **Windows Identity Foundation 3.5**를 선택하고 **다음**을 클릭합니다.

8. **웹 서버 역할(IIS)** 페이지에서 **다음**을 클릭합니다.

9. **역할 서비스 선택** 페이지에서 **응용 프로그램 개발**을 선택하고 확장합니다. **ASP.NET 3.5**를 선택하고 **기능 추가**를 클릭한 후 **다음**을 클릭합니다.

10. **설치 선택 확인** 페이지에서 **대체 원본 경로 지정**을 클릭합니다. Windows Server 2012 R2 설치 미디어에 있는 Sxs 디렉터리의 경로를 입력 합니다. 예를 들어 D:\Sources\Sxs를 입력합니다. **확인**을 클릭한 다음 **설치**를 클릭합니다.

### <a name="BKMK_13"></a>Windows Identity Foundation SDK 설치

1.  Windowsidentityfoundation-sdk-3.5.msi 3.5 .msi를 실행 하 여 Windows Identity Foundation SDK 3.5 (https://www.microsoft.com/download/details.aspx?id=4451)를 설치 합니다. 모든 기본 옵션을 선택합니다.

### <a name="BKMK_9"></a>IIS에서 간단한 클레임 앱 구성

1.  컴퓨터 인증서 저장소에 유효한 SSL 인증서를 설치합니다. 인증서에는 웹 서버의 이름 **webserv1.contoso.com**이 포함되어야 합니다.

2.  C:\Program Files (x86)\Windows Identity Foundation SDK\v3.5\Samples\Quick Start\Web Application\PassiveRedirectBasedClaimsAwareWebApp의 내용을 C:\Inetpub\Claimapp에 복사합니다.

3.  클레임 필터링이 발생하지 않도록 **Default.aspx.cs** 파일을 편집합니다. 이 단계는 예제 애플리케이션이 페더레이션 서버에서 발급한 모든 클레임을 표시하도록 하기 위해 수행됩니다. 다음을 수행합니다.

    1.  텍스트 편집기에서 **Default.aspx.cs**를 엽니다.

    2.  파일에서 `ExpectedClaims`의 두 번째 인스턴스를 검색합니다.

    3.  전체 `IF` 문과 해당 중괄호를 주석 처리합니다. 줄의 시작 부분에 "//" (따옴표 제외)를 입력 하 여 주석을 표시 합니다.

    4.  `FOREACH` 문이 다음 코드 예제와 유사하게 표시됩니다.

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

    5.  **Default.aspx.cs**를 저장하고 닫습니다.

    6.  텍스트 편집기에서 **web.config**를 엽니다.

    7.  전체 `<microsoft.identityModel>` 섹션을 제거합니다. `including <microsoft.identityModel>` 에서 `</microsoft.identityModel>`(포함)까지 모든 항목을 제거합니다.

    8.  **web.config**를 저장하고 닫습니다.

4.  **IIS 관리자 구성**

    1.  **IIS(인터넷 정보 서비스) 관리자**를 엽니다.

    2.  **응용 프로그램 풀**로 이동하여 **DefaultAppPool**을 마우스 오른쪽 단추로 클릭하고 **고급 설정**을 선택합니다. **사용자 프로필 로드**를 **True**로 설정하고 **확인**을 클릭합니다.

    3.  **DefaultAppPool**을 마우스 오른쪽 단추로 클릭하고 **기본 설정**을 선택합니다. **.NET CLR 버전**을 **.NET CLR Version v2.0.50727**로 변경합니다.

    4.  **기본 웹 사이트**를 마우스 오른쪽 단추로 클릭하여 **바인딩 편집**을 선택합니다.

    5.  설치한 SSL 인증서를 사용하는 포트 **443**에  **HTTPS** 바인딩을 추가합니다.

    6.  **기본 웹 사이트**를 마우스 오른쪽 단추로 클릭하여 **응용 프로그램 추가**를 선택합니다.

    7.  별칭을 **claimapp**으로 설정하고 실제 경로를 **c:\inetpub\claimapp**으로 설정합니다.

5.  **claimapp**을 페더레이션 서버와 함께 작동하도록 구성하려면 다음을 수행합니다.

    1.  **C:\Program Files (x86)\Windows Identity Foundation SDK\v3.5**에 있는 FedUtil.exe를 실행합니다.

    2.  응용 프로그램 구성 위치를 **c:\inetput\claimapp\web.config로 설정** 로 설정 하 고 응용 프로그램 URI를 사이트의 URL ( **https://webserv1.contoso.com/claimapp/** )로 설정 합니다. **다음**을 클릭합니다.

    3.  **기존 STS 사용** 을 선택 하 고 AD FS 서버의 메타 데이터 URL **https://adfs1.contoso.com/federationmetadata/2007-06/federationmetadata.xml** 를 찾습니다. **다음**을 클릭합니다.

    4.  **인증서 체인 유효성 검사 사용 안 함**을 선택하고 **다음**을 클릭합니다.

    5.  **암호화 없음**을 선택하고 **다음**을 클릭합니다. **제공된 클레임** 페이지에서 **다음**을 클릭합니다.

    6.  **매일 WS-Federation 메타데이터 업데이트를 수행하도록 작업 예약** 옆의 확인란을 선택합니다. **마침**을 클릭합니다.

    7.  이제 예제 애플리케이션이 구성되었습니다. **https://webserv1.contoso.com/claimapp** 응용 프로그램 URL을 테스트 하면 페더레이션 서버로 리디렉션됩니다. 신뢰 당사자 트러스트를 구성하지 않았으므로 페더레이션 서버에 오류 메시지가 표시됩니다. 즉, AD FS 하 여이 테스트 응용 프로그램을 보호 하지 않았습니다.

이제 AD FS를 사용 하 여 웹 서버에서 실행 되는 샘플 응용 프로그램의 보안을 유지 해야 합니다. 이렇게 하려면 페더레이션 서버(ADFS1)에서 신뢰 당사자 트러스트를 추가하면 됩니다. 비디오는 [Active Directory Federation Services How-To Video Series: Add a Relying Party Trust(Active Directory Federation Services 방법 비디오 시리즈: 신뢰 당사자 트러스트 추가)](https://technet.microsoft.com/video/adfs-how-to-add-a-relying-party-trust)를 참조하세요.

### <a name="BKMK_11"></a>페더레이션 서버에서 신뢰 당사자 트러스트 만들기

1.  페더레이션 서버(ADFS1)의 **AD FS 관리 콘솔**에서 **신뢰 당사자 트러스트**로 이동하여 **신뢰 당사자 트러스트 추가**를 클릭합니다.

2.  **데이터 원본 선택** 페이지에서 **온라인 또는 로컬 네트워크에 게시된 신뢰 당사자에 대한 데이터 가져오기**를 선택하고 **claimapp**에 대한 메타데이터 URL을 입력한 후 **다음**을 클릭합니다. FedUtil.exe를 실행하면 메타데이터 .xml 파일이 생성됩니다. **https://webserv1.contoso.com/claimapp/federationmetadata/2007-06/federationmetadata.xml** 에 있습니다.

3.  **표시 이름 지정** 페이지에서 신뢰 당사자 트러스트에 대한 **표시 이름** **claimapp**을 지정하고 **다음**을 클릭합니다.

4.  **지금 다단계 인증을 구성하시겠습니까?** 페이지에서 **이 신뢰 당사자 트러스트에 대한 다단계 인증 설정을 지금 지정 안 함**을 선택하고 **다음**을 클릭합니다.

5.  **발급 권한 부여 규칙 선택** 페이지에서 **모든 사용자가 이 신뢰 당사자에 액세스하도록 허용**을 선택하고 **다음**을 클릭합니다.

6.  **트러스트 추가 준비** 페이지에서 **다음**을 클릭합니다.

7.  **클레임 규칙 편집** 대화 상자에서 **규칙 추가**를 클릭합니다.

8.  **규칙 유형 선택** 페이지에서 **사용자 지정 규칙을 사용하여 클레임 보내기**를 선택하고 **다음**을 클릭합니다.

9. **클레임 규칙 구성** 페이지의 **클레임 규칙 이름** 상자에 **All Claims**를 입력합니다. **사용자 지정 규칙** 상자에 다음 클레임 규칙을 입력합니다.

    ```
    c:[ ]
    => issue(claim = c);

    ```

10. **마침**을 클릭한 다음 **확인**을 클릭합니다.

## <a name="BKMK_10"></a>4 단계: 클라이언트 컴퓨터 (Client1) 구성
다른 가상 컴퓨터를 설정 하 고 Windows 8.1를 설치 합니다. 이 가상 컴퓨터는 다른 컴퓨터와 동일한 가상 네트워크에 있어야 합니다. 이 컴퓨터는 Contoso 도메인에 가입되지 않아야 합니다.

클라이언트는 [Step 2: Configure the federation server (ADFS1) with Device Registration Service](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)에서 설정한 페더레이션 서버(ADFS1)에 사용된 SSL 인증서를 신뢰해야 합니다. 또한 인증서에 대한 인증서 해지 정보의 유효성을 검사할 수 있어야 합니다.

Microsoft 계정을 설정하고 이를 사용하여 Client1에 로그온해야 합니다.

## <a name="see-also"></a>관련 항목


- [Active Directory Federation Services 방법 비디오 시리즈: AD FS 서버 팜 설치](https://technet.microsoft.com/video/dn469436)
- [Active Directory Federation Services 방법 비디오 시리즈: 인증서 업데이트](https://technet.microsoft.com/video/adfs-updating-certificates)
- [Active Directory Federation Services 방법 비디오 시리즈: 신뢰 당사자 트러스트 추가](https://technet.microsoft.com/video/adfs-how-to-add-a-relying-party-trust)
- [Active Directory Federation Services 방법 비디오 시리즈: Device Registration Service 사용](https://technet.microsoft.com/video/adfs-how-to-enabling-the-device-registration-service)
- [Active Directory Federation Services 방법 비디오 시리즈: 웹 응용 프로그램 프록시 설치](https://technet.microsoft.com/video/dn469438)



