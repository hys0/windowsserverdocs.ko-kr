---
ms.assetid: 5f733510-c96e-4d3a-85d2-4407de95926e
title: AD FS 사전 인증을 사용하는 응용 프로그램 게시
description: ''
author: kgremban
manager: femila
ms.date: 07/13/2016
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: web-app-proxy
ms.openlocfilehash: c7dab1dbf97d2dcbda1fe0375e61300f2a1cc373
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862244"
---
# <a name="publishing-applications-using-ad-fs-preauthentication"></a>AD FS 사전 인증을 사용하는 응용 프로그램 게시

>적용 대상: Windows Server 2016

**이 콘텐츠는 웹 응용 프로그램 프록시의 온-프레미스 버전에 적합 합니다. 클라우드를 통해 온-프레미스 응용 프로그램에 대 한 보안 액세스를 사용 합니다 [Azure AD 응용 프로그램 프록시 콘텐츠](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/)합니다.**  
  
이 항목에서는 Active Directory Federation Services (AD FS) 사전 인증을 사용 하 여 웹 응용 프로그램 프록시를 통해 응용 프로그램을 게시 하는 방법을 설명 합니다.  
  
AD FS 사전 인증을 사용 하 여 게시할 수 있는 응용 프로그램의 모든 형식에 대 한 AD FS 신뢰 당사자 트러스트를 페더레이션 서비스를 추가 해야 합니다.  
  
일반적인 AD FS 사전 인증 흐름과 다음과 같습니다.  
  
> [!NOTE]  
> 이 인증 흐름 Microsoft Store 앱을 사용 하는 클라이언트에 대 한 적용 되지 않습니다.  
  
1.  클라이언트 장치는 특정 리소스 URL에 게시 된 웹 응용 프로그램에 액세스 하려고 합니다. 예를 들어 https://app1.contoso.com/합니다.  
  
    리소스 URL은 웹 응용 프로그램 프록시 들어오는 HTTPS 요청을 수신 하는 공용 주소입니다.  
  
    HTTP-HTTPS 리디렉션 사용 하는 경우 들어오는 HTTP 요청에 대 한 웹 응용 프로그램 프록시 수신 됩니다.  
  
2.  웹 응용 프로그램 프록시 리소스 URL 및 appRealm (신뢰 당사자 식별자)를 포함 하는 URL로 인코딩된 매개 변수를 사용 하 여 AD FS 서버에 HTTPS 요청을 리디렉션합니다.  
  
    AD FS 서버에서 필요한 인증 방법을 사용 하 여 사용자 인증 예를 들어, 사용자 이름 및 암호, 일회성 암호 및 등을 사용 하 여 2 단계 인증 합니다.  
  
3.  사용자가 인증 되 면 AD FS 서버 토큰을 발급 보안 토큰 ' edge', 다음 정보 및 웹 응용 프로그램 프록시 서버에 HTTPS 요청 리디렉션을 포함 하 합니다.  
  
    -   사용자가 액세스하려고 한 리소스 식별자  
  
    -   사용자 계정 이름 (UPN)로 사용자의 id입니다.  
  
    -   액세스 권한 부여 승인 만료(즉, 사용자에게는 제한된 기간 동안 액세스 권한이 부여되며, 이 기간이 경과한 후에는 다시 인증해야 함)  
  
    -   에지 토큰의 정보 서명  
  
4.  웹 응용 프로그램 프록시의 유효성을 검사 및 다음과 같은 토큰을 사용 하 여에 지 토큰을 사용 하 여 AD FS 서버에서 리디렉션된 HTTPS 요청을 받으면:  
  
    -   웹 응용 프로그램 프록시 구성에서 구성 된 페더레이션 서비스에서에 지 토큰 서명이 인지 확인 합니다.  
  
    -   토큰이 올바른 응용 프로그램에 대해 발급되었는지 확인  
  
    -   토큰이 만료되지 않았는지 확인  
  
    -   필요한 경우(예: 백 엔드 서버가 Windows 통합 인증을 사용하도록 구성된 경우 Kerberos 티켓을 받기 위해) 사용자 ID 사용  
  
5.  에 지 토큰이 유효한 경우 웹 응용 프로그램 프록시는 HTTP 또는 HTTPS를 사용 하 여 게시 된 웹 응용 프로그램에 HTTPS 요청을 전달 합니다.  
  
6.  이제 클라이언트에서 게시된 웹 응용 프로그램에 액세스할 수 있습니다. 그러나 게시된 응용 프로그램이 사용자의 추가 인증을 요구하도록 구성되어 있을 수도 있습니다. 예를 들어 게시된 웹 응용 프로그램이 SharePoint 사이트이고 추가 인증을 요구하지 않는 경우 사용자는 브라우저에서 SharePoint 사이트를 볼 수 있습니다.  
  
7.  웹 응용 프로그램 프록시는 클라이언트 장치에 쿠키를 저장 합니다. 쿠키는이 세션이 이미 사전 인증 하 고는 추가 사전 인증이 필요 하지 데 웹 응용 프로그램 프록시에 의해 사용 됩니다.  
  
> [!IMPORTANT]  
> 외부 URL 및 백 엔드 서버 URL을 구성할 때 IP 주소가 아니라 FQDN(정규화된 도메인 이름)을 포함해야 합니다.  
  
> [!NOTE]  
> 이 항목에는 설명한 절차의 일부를 자동화하는 데 사용할 수 있는 샘플 Windows PowerShell cmdlet이 포함되어 있습니다. 자세한 내용은 참조 [Cmdlet를 사용 하 여](https://go.microsoft.com/fwlink/p/?linkid=230693)합니다.  
  
## <a name="BKMK_1.1"></a>웹 브라우저 클라이언트용 클레임 기반 응용 프로그램 게시  
인증에 클레임을 사용하는 응용 프로그램을 게시하려면 응용 프로그램의 신뢰 당사자 트러스트를 페더레이션 서비스에 추가해야 합니다.  
  
클레임 기반 응용 프로그램을 게시하고 브라우저에서 응용 프로그램에 액세스할 때의 일반적인 인증 흐름은 다음과 같습니다.  
  
1.  클라이언트 웹 브라우저를 사용 하 여 클레임 기반 응용 프로그램에 액세스 하려고 합니다. 예를 들어 https://appserver.contoso.com/claimapp/합니다.  
  
2.  웹 브라우저를 AD FS 서버에 요청을 리디렉션하는 웹 응용 프로그램 프록시 서버에 HTTPS 요청을 보냅니다.  
  
3.  AD FS 서버는 사용자 및 장치를 인증 하 고 웹 응용 프로그램 프록시를 다시 요청을 리디렉션합니다. 이제 요청에 에지 토큰이 포함되어 있습니다. AD FS 서버를 이미 AD FS 서버에 대 한 인증을 수행 하기 때문에 요청에 단일 로그온 (SSO) 쿠키를 추가 합니다.  
  
4.  웹 응용 프로그램 프록시는 토큰의 유효성을 검사 하 고, 고유한 쿠키를 추가, 백 엔드 서버로 요청을 전달 합니다.  
  
5.  백 엔드 서버 응용 프로그램 보안 토큰을 가져오는 AD FS 서버에 요청을 리디렉션합니다.  
  
6.  AD FS 서버에서 백 엔드 서버로 요청을 리디렉션할 수 있습니다. 이제 요청에 응용 프로그램 토큰 및 SSO 쿠키가 포함되어 있습니다. 사용자에게 응용 프로그램에 대한 액세스 권한이 부여되며, 사용자는 사용자 이름이나 암호를 입력할 필요가 없습니다.  
  
이 절차에서는 웹 브라우저 클라이언트에서 액세스할 수 있는 SharePoint 사이트와 같은 클레임 기반 응용 프로그램을 게시하는 방법에 대해 설명합니다. 시작하기 전에 다음 작업을 완료했는지 확인합니다.  
  
-   AD FS 관리 콘솔에서 응용 프로그램에 대 한 신뢰 당사자 트러스트를 생성 합니다.  
  
-   웹 응용 프로그램 프록시 서버에서 인증서를 게시 하려는 응용 프로그램에 적합 한지 확인 합니다.  
  

  
#### <a name="to-publish-a-claims-based-application"></a>클레임 기반 응용 프로그램을 게시하려면  
  
1.  원격 액세스 관리 콘솔에서 웹 응용 프로그램 프록시 서버의는 **탐색** 창 클릭 **웹 응용 프로그램 프록시**를 선택한 다음를 **작업** 창 클릭 **게시**합니다.  
  
2.  **새 응용 프로그램 게시 마법사**의 **시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  에 **사전 인증을** 페이지에서 클릭 **Active Directory Federation Services (AD FS)** 를 클릭 하 고 **다음**합니다.  
  
4.  **지원되는 클라이언트** 페이지에서 **웹 및 MSOFBA**를 선택하고 **다음**을 클릭합니다.  
  
5.  **신뢰 당사자** 페이지의 신뢰 당사자 목록에서 게시할 응용 프로그램의 신뢰 당사자를 선택하고 **다음**을 클릭합니다.  
  
6.  **게시 설정** 페이지에서 다음 작업을 수행한 후 **다음**을 클릭합니다.  
  
    -   **이름** 상자에 응용 프로그램의 이름을 입력합니다.  
  
        이 이름은 원격 액세스 관리 콘솔의 게시된 응용 프로그램 목록에만 사용됩니다.  
  
    -   **External URL(외부 URL)** 상자에 이 응용 프로그램의 외부 URL(예: https://sp.contoso.com/app1/)을 입력합니다.  
  
    -   **외부 인증서** 목록에서 주체에 외부 URL이 포함된 인증서를 선택합니다.  
  
    -   **백 엔드 서버 URL** 상자에 백 엔드 서버의 URL을 입력합니다. 외부 URL을 입력 하 고 백 엔드 서버 URL이 다른 경우에 변경 해야 하는 경우이 값은 자동으로 입력는 note 예를 들어 https://sp/app1/합니다.  
  
        > [!NOTE]  
        > 웹 응용 프로그램 프록시 Url의 호스트 이름을 변환할 수 있지만 경로 이름을 변환할 수 없습니다. 따라서 서로 다른 호스트 이름을 입력할 수 있지만 경로 이름은 같아야 합니다. 예를 들어 외부 URL을 입력할 수 있습니다 https://apps.contoso.com/app1/ 백 엔드 서버 URL 및 https://app-server/app1/합니다. 그러나 외부 URL을 입력할 수 없습니다 https://apps.contoso.com/app1/ 백 엔드 서버 URL 및 https://apps.contoso.com/internal-app1/합니다.  
  
7.  **확인** 페이지에서 설정을 검토하고 **게시**를 클릭합니다. PowerShell 명령을 복사하여 게시된 추가 응용 프로그램을 설정할 수 있습니다.  
  
8.  **결과** 페이지에서 응용 프로그램이 게시되었는지 확인하고 **닫기**를 클릭합니다.  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
Add-WebApplicationProxyApplication  
    -BackendServerURL 'https://sp.contoso.com/app1/'  
    -ExternalCertificateThumbprint '1a2b3c4d5e6f1a2b3c4d5e6f1a2b3c4d5e6f1a2b'  
    -ExternalURL 'https://sp.contoso.com/app1/'  
    -Name 'SP'  
    -ExternalPreAuthentication ADFS  
    -ADFSRelyingPartyName 'SP_Relying_Party'  
```  
  
## <a name="BKMK_1.2"></a>웹 브라우저 클라이언트용 Windows 통합 인증 기반 응용 프로그램 게시  
웹 응용 프로그램 프록시를 사용 하 여 통합 Windows 인증을 사용 하는 응용 프로그램을 게시할 수 있습니다. 즉, 웹 응용 프로그램 프록시는 필요에 따라 사전 인증을 수행 하 고 통합 Windows 인증을 사용 하는 게시 된 응용 프로그램에 SSO를 수행할 수 있습니다. Windows 통합 인증을 사용하는 응용 프로그램을 게시하려면 응용 프로그램의 비 클레임 인식 신뢰 당사자 트러스트를 페더레이션 서비스에 추가해야 합니다.  
  
웹 응용 프로그램 프록시에서에서 single sign-on (SSO) 수행 하 고 Kerberos를 사용 하 여 자격 증명 위임을 수행 하도록 허용 하려면 제한 된 위임을 웹 응용 프로그램 프록시 서버를 도메인에 가입 되어야 합니다. 참조 [Active Directory 계획](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD)합니다.  
  
통합 Windows 인증을 사용 하는 응용 프로그램에 액세스할 수 있도록 웹 응용 프로그램 프록시 서버 사용자가 게시 된 응용 프로그램에 대 한 위임을 제공할 수 있어야 합니다. 이 작업은 도메인 컨트롤러에서 모든 응용 프로그램에 대해 수행할 수 있습니다. 또한 이렇게 하려면 백 엔드 서버에서 Windows Server 2012 R2 또는 Windows Server 2012에서 실행 중인 경우. 자세한 내용은 [Kerberos 인증의 새로운 기능](https://technet.microsoft.com/library/hh831747.aspx)을 참조하세요.  
  
통합 Windows 인증을 사용 하 여 응용 프로그램을 게시 하려면 웹 응용 프로그램 프록시를 구성 하는 방법의 연습을 참조 하세요 [통합 Windows 인증을 사용 하도록 사이트 구성](https://technet.microsoft.com/library/dn280943.aspx#BKMK_3)합니다.  
  
백 엔드 서버로 통합 Windows 인증을 사용 하면 웹 응용 프로그램 프록시 및 게시 된 응용 프로그램 간의 인증은 클레임 기반이 아니며, 대신 Kerberos 제한 위임을 응용 프로그램에 최종 사용자 인증 사용 합니다. 일반적인 흐름은 다음과 같습니다.  
  
1.  클라이언트 웹 브라우저를 사용 하 여 클레임 기반이 아닌 응용 프로그램에 액세스 하려고 합니다. 예를 들어 https://appserver.contoso.com/nonclaimapp/합니다.  
  
2.  웹 브라우저를 AD FS 서버에 요청을 리디렉션하는 웹 응용 프로그램 프록시 서버에 HTTPS 요청을 보냅니다.  
  
3.  AD FS 서버는 사용자를 인증 하 고 웹 응용 프로그램 프록시를 다시 요청을 리디렉션합니다. 이제 요청에 에지 토큰이 포함되어 있습니다.  
  
4.  웹 응용 프로그램 프록시는 토큰의 유효성을 검사 합니다.  
  
5.  토큰이 유효한 경우 웹 응용 프로그램 프록시는 사용자를 대신해 서 Kerberos 티켓을 도메인 컨트롤러에서 가져옵니다.  
  
6.  웹 응용 프로그램 프록시는 간편 하 고 Protected GSS-API Negotiation 메커니즘 (SPNEGO) 토큰의 일부로 Kerberos 티켓 요청에 추가 하 고 백 엔드 서버로 요청을 전달 합니다. 요청에 Kerberos 티켓이 포함되어 있으므로 추가 인증 없이 사용자에게 응용 프로그램에 대한 액세스 권한이 부여됩니다.  
  
이 절차에서는 웹 브라우저 클라이언트에서 액세스할 수 있는 Outlook Web App과 같은 Windows 통합 인증을 사용하는 응용 프로그램을 게시하는 방법에 대해 설명합니다. 시작하기 전에 다음 작업을 완료했는지 확인합니다.  
  
-   AD FS 관리 콘솔에서 응용 프로그램에 대 한 비 클레임 인식 신뢰 당사자 트러스트를 생성 합니다.  
  
-   -PrincipalsAllowedToDelegateToAccount 매개 변수와 함께 Set-ADUser cmdlet을 사용하거나 도메인 컨트롤러에서 Kerberos 제한 위임을 지원하도록 백 엔드 서버 구성. 백 엔드 서버에서 Windows Server 2012 R2 또는 Windows Server 2012에서을 실행 하는 경우 또한 명령을 실행할 수 있습니다이 PowerShell 백 엔드 서버에서 참고 합니다.  
  
-   백 엔드 서버의 서비스 사용자 이름에 위임에 대 한 웹 응용 프로그램 프록시 서버 구성 되어 있는지 확인 했습니다.  
  
-   웹 응용 프로그램 프록시 서버에서 인증서를 게시 하려는 응용 프로그램에 적합 한지 확인 합니다.  
  
 
  
#### <a name="to-publish-a-non-claims-based-application"></a>클레임 기반이 아닌 응용 프로그램을 게시하려면  
  
1.  원격 액세스 관리 콘솔에서 웹 응용 프로그램 프록시 서버의는 **탐색** 창 클릭 **웹 응용 프로그램 프록시**를 선택한 다음를 **작업** 창 클릭 **게시**합니다.  
  
2.  **새 응용 프로그램 게시 마법사**의 **시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  에 **사전 인증을** 페이지에서 클릭 **Active Directory Federation Services (AD FS)** 를 클릭 하 고 **다음**합니다.  
  
4.  **지원되는 클라이언트** 페이지에서 **웹 및 MSOFBA**를 선택하고 **다음**을 클릭합니다.  
  
5.  **신뢰 당사자** 페이지의 신뢰 당사자 목록에서 게시할 응용 프로그램의 신뢰 당사자를 선택하고 **다음**을 클릭합니다.  
  
6.  **게시 설정** 페이지에서 다음 작업을 수행한 후 **다음**을 클릭합니다.  
  
    -   **이름** 상자에 응용 프로그램의 이름을 입력합니다.  
  
        이 이름은 원격 액세스 관리 콘솔의 게시된 응용 프로그램 목록에만 사용됩니다.  
  
    -   **External URL(외부 URL)** 상자에 이 응용 프로그램의 외부 URL(예: https://owa.contoso.com/)을 입력합니다.  
  
    -   **외부 인증서** 목록에서 주체에 외부 URL이 포함된 인증서를 선택합니다.  
  
    -   **백 엔드 서버 URL** 상자에 백 엔드 서버의 URL을 입력합니다. 외부 URL을 입력 하 고 백 엔드 서버 URL이 다른 경우에 변경 해야 하는 경우이 값은 자동으로 입력는 note 예를 들어 https://owa/합니다.  
  
        > [!NOTE]  
        > 웹 응용 프로그램 프록시 Url의 호스트 이름을 변환할 수 있지만 경로 이름을 변환할 수 없습니다. 따라서 서로 다른 호스트 이름을 입력할 수 있지만 경로 이름은 같아야 합니다. 예를 들어 외부 URL을 입력할 수 있습니다 https://apps.contoso.com/app1/ 백 엔드 서버 URL 및 https://app-server/app1/합니다. 그러나 외부 URL을 입력할 수 없습니다 https://apps.contoso.com/app1/ 백 엔드 서버 URL 및 https://apps.contoso.com/internal-app1/합니다.  
  
    -   **백 엔드 서버 SPN** 상자에 백 엔드 서버의 서비스 사용자 이름(예: HTTP/owa.contoso.com)을 입력합니다.  
  
7.  **확인** 페이지에서 설정을 검토하고 **게시**를 클릭합니다. PowerShell 명령을 복사하여 게시된 추가 응용 프로그램을 설정할 수 있습니다.  
  
8.  **결과** 페이지에서 응용 프로그램이 게시되었는지 확인하고 **닫기**를 클릭합니다.  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
Add-WebApplicationProxyApplication  
    -BackendServerAuthenticationSpn 'HTTP/owa.contoso.com'  
    -BackendServerURL 'https://owa.contoso.com/'  
    -ExternalCertificateThumbprint '1a2b3c4d5e6f1a2b3c4d5e6f1a2b3c4d5e6f1a2b'  
    -ExternalURL 'https://owa.contoso.com/'  
    -Name 'OWA'  
    -ExternalPreAuthentication ADFS  
    -ADFSRelyingPartyName 'Non-Claims_Relying_Party'  
```  
  
## <a name="BKMK_1.3"></a>MS OFBA를 사용 하는 응용 프로그램 게시  
웹 응용 프로그램 프록시 액세스 지원 Microsoft Word와 같은 Microsoft Office 클라이언트에서 해당 문서 및 데이터 액세스 백 엔드 서버에서 합니다. 이러한 응용 프로그램과 표준 브라우저 간의 유일한 차이점은 STS로 리디렉션에 지정 된 대로 특수 한 MS OFBA 헤더 하지만 일반 HTTP 리디렉션을 통해 수행 되도록 합니다. [ https://msdn.microsoft.com/library/dd773463(v=office.12).aspx ](https://msdn.microsoft.com/library/dd773463(v=office.12).aspx)합니다. 백 엔드 응용 프로그램은 클레임 또는 IWA일 수 있습니다.   
MS OFBA를 사용 하는 클라이언트 응용 프로그램을 게시 하려면 신뢰 당사자 트러스트를 페더레이션 서비스 응용 프로그램을 추가 해야 합니다. 응용 프로그램에 따라 클레임 기반 인증 또는 Windows 통합 인증을 사용할 수 있습니다. 따라서 응용 프로그램에 따라 관련 신뢰 당사자 트러스트를 추가해야 합니다.  
  
웹 응용 프로그램 프록시에서에서 single sign-on (SSO) 수행 하 고 Kerberos를 사용 하 여 자격 증명 위임을 수행 하도록 허용 하려면 제한 된 위임을 웹 응용 프로그램 프록시 서버를 도메인에 가입 되어야 합니다. 참조 [Active Directory 계획](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD)합니다.  
  
응용 프로그램에서 클레임 기반 인증을 사용하는 경우에는 추가 계획 단계가 없습니다. 통합 Windows 인증을 사용 하는 응용 프로그램, 참조 [웹 브라우저 클라이언트용 Windows 통합 인증 기반 응용 프로그램을 게시](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md#BKMK_1.2)합니다.  
  
클레임 기반 인증을 사용 하 여 MS OFBA 프로토콜을 사용 하는 클라이언트에 대 한 인증 흐름에 대 한 설명은 다음과 같습니다. 이 시나리오의 인증에서는 URL 또는 본문에 응용 프로그램 토큰을 사용할 수 있습니다.  
  
1.  Office 프로그램에서 작업 중인 사용자가 **최근 문서** 목록에서 SharePoint 사이트에 있는 파일을 엽니다.  
  
2.  Office 프로그램에서 사용자가 자격 증명을 입력해야 하는 브라우저 컨트롤이 포함된 창을 표시합니다.  
  
    > [!NOTE]  
    > 클라이언트가 이미 인증된 경우 이 창이 표시되지 않을 수도 있습니다.  
  
3.  웹 응용 프로그램 프록시는 인증을 수행 하는 AD FS 서버에 요청을 리디렉션합니다.  
  
4.  AD FS 서버는 웹 응용 프로그램 프록시를 다시 요청을 리디렉션합니다. 이제 요청에 에지 토큰이 포함되어 있습니다.  
  
5.  AD FS 서버를 이미 AD FS 서버에 대 한 인증을 수행 하기 때문에 요청에 단일 로그온 (SSO) 쿠키를 추가 합니다.  
  
6.  웹 응용 프로그램 프록시는 토큰의 유효성을 검사 하 고 백 엔드 서버로 요청을 전달 합니다.  
  
7.  백 엔드 서버 응용 프로그램 보안 토큰을 가져오는 AD FS 서버에 요청을 리디렉션합니다.  
  
8.  요청이 백 엔드 서버로 리디렉션됩니다. 이제 요청에 응용 프로그램 토큰 및 SSO 쿠키가 포함되어 있습니다. 사용자에게 SharePoint 사이트에 대한 액세스 권한이 부여되며, 사용자는 사용자 이름이나 암호를 입력하지 않고 파일을 볼 수 있습니다.  
  
MS OFBA를 사용 하는 응용 프로그램을 게시 하는 단계는 클레임 기반 응용 프로그램 또는 비 클레임 기반 응용 프로그램에 대 한 단계와 동일 합니다. 클레임 기반 응용 프로그램에 대 한 참조 [웹 브라우저 클라이언트용 클레임 기반 응용 프로그램을 게시할](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md#BKMK_1.1), 비 클레임 기반 응용 프로그램을 참조 하세요. [Windows 통합 인증 기반 응용 프로그램을 게시 웹 브라우저 클라이언트](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md#BKMK_1.2)합니다. 웹 응용 프로그램 프록시는 자동으로 클라이언트를 검색 하 고 필요에 따라 사용자를 인증 합니다.  
  
## <a name="publish-an-application-that-uses-http-basic"></a>HTTP Basic을 사용 하는 응용 프로그램 게시  

HTTP Basic은 다양 한 프로토콜 Exchange 사서함이 있는 스마트폰을 포함 하는 다양 한 클라이언트 연결을 사용 하는 권한 부여 프로토콜입니다. HTTP Basic에 대 한 자세한 내용은 참조 하세요. [RFC 2617](https://www.ietf.org/rfc/rfc2617.txt)합니다. 웹 응용 프로그램 프록시 리디렉션;를 사용 하 여 AD FS를 사용 하 여 일반적으로 상호 작용 대부분의 다양 한 클라이언트 쿠키 또는 상태 관리를 지원 하지 않습니다. 웹 응용 프로그램 프록시에 HTTP 앱이 비 클레임을 받을 수 있도록이 방식으로 신뢰 당사자 트러스트를 페더레이션 서비스 응용 프로그램에 대 한 합니다. 참조 [Active Directory 계획](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD)합니다.  
  
HTTP Basic을 사용 하는 클라이언트에 대 한 인증 흐름에는이 다이어그램 아래에 설명 되어 있습니다.  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/WebApplicationProxy_httpBasicflow.png)  
  
1.  사용자가 게시 된 웹 응용 프로그램 전화 클라이언트에 액세스 하려고 합니다.  
  
2.  앱 웹 응용 프로그램 프록시에 의해 게시 된 URL에 HTTPS 요청을 보냅니다.  
  
3.  요청에 자격 증명이 없으면 웹 응용 프로그램 프록시 인증 AD FS 서버의 URL이 포함 된 앱에 HTTP 401 응답을 반환 합니다.  
  
4.  사용자 앱에 HTTPS 요청 다시 기본 및 사용자 이름 및 Base 64로 설정 하는 권한 부여를 사용 하 여 암호화 된 암호는 www의 사용자가 보내는-요청 헤더를 인증 합니다.  
  
5.  장치는 AD FS로 리디렉션될 수 없습니다, 때문에 웹 응용 프로그램 프록시 인증 요청을 보냅니다 자격 증명을 사용 하 여 AD FS에 사용자 이름 및 암호를 포함 하는 합니다. 장치를 대신 하 여 토큰을 가져옵니다.  
  
6.  AD FS로 전송 된 요청 수를 최소화 하기 위해 웹 응용 프로그램 프록시는 토큰이 잘못으로 캐시 된 토큰을 사용 하 여 후속 클라이언트 요청을 확인 합니다. 웹 응용 프로그램 프록시는 주기적으로 캐시를 정리 합니다. 성능 카운터를 사용 하 여 캐시의 크기를 볼 수 있습니다.  
  
7.  토큰이 유효한 경우 웹 응용 프로그램 프록시는 백 엔드 서버로 요청을 전달 하 고 사용자에는 게시 된 웹 응용 프로그램에 대 한 액세스 권한이 부여 됩니다.  
  
다음 절차에는 HTTP 기본 응용 프로그램을 게시 하는 방법을 설명 합니다.  
  
#### <a name="to-publish-an-http-basic-application"></a>HTTP 기본 응용 프로그램 게시  
  
1.  원격 액세스 관리 콘솔에서 웹 응용 프로그램 프록시 서버의는 **탐색** 창 클릭 **웹 응용 프로그램 프록시**를 선택한 다음를 **작업** 창 클릭 **게시**합니다.  
  
2.  **새 응용 프로그램 게시 마법사**의 **시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  에 **사전 인증을** 페이지에서 클릭 **Active Directory Federation Services (AD FS)** 를 클릭 하 고 **다음**합니다.  
  
4.  에 **지원 되는 클라이언트** 페이지에서 **HTTP Basic** 클릭 하 고 **다음**합니다.  
  
    작업 공간 연결 장치 에서만에서 Exchange에 액세스할 수 있도록 하려는 경우 선택 합니다 **가입 장치를 작업 공간에 대해서만 액세스 사용** 상자입니다. 자세한 내용은 참조 [SSO 및 원활한 두 번째 단계 인증에서 회사 응용 프로그램에 대 한 모든 장치에서 작업 공간 가입](https://technet.microsoft.com/library/dn280945.aspx)합니다.  
  
5.  **신뢰 당사자** 페이지의 신뢰 당사자 목록에서 게시할 응용 프로그램의 신뢰 당사자를 선택하고 **다음**을 클릭합니다. 이 목록에만 포함 하는 온-클레임 신뢰 당사자입니다.  
  
6.  **게시 설정** 페이지에서 다음 작업을 수행한 후 **다음**을 클릭합니다.  
  
    -   **이름** 상자에 응용 프로그램의 이름을 입력합니다.  
  
        이 이름은 원격 액세스 관리 콘솔의 게시된 응용 프로그램 목록에만 사용됩니다.  
  
    -   에 **외부 URL** 상자에서이 응용 프로그램에 대 한 외부 URL을 입력 합니다. 예를 들어 mail.contoso.com  
  
    -   **외부 인증서** 목록에서 주체에 외부 URL이 포함된 인증서를 선택합니다.  
  
    -   **백 엔드 서버 URL** 상자에 백 엔드 서버의 URL을 입력합니다. 외부 URL을 입력 하 고 백 엔드 서버 URL이 다른 경우에 변경 해야 하는 경우이 값은 자동으로 입력는 note 예를 들어 mail.contoso.com 합니다.  
  
7.  **확인** 페이지에서 설정을 검토하고 **게시**를 클릭합니다. PowerShell 명령을 복사하여 게시된 추가 응용 프로그램을 설정할 수 있습니다.  
  
8.  **결과** 페이지에서 응용 프로그램이 게시되었는지 확인하고 **닫기**를 클릭합니다.  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
이 Windows PowerShell 스크립트 작업 공간 연결 장치 뿐 아니라, 모든 장치에 대 한 사전 인증을 활성화합니다.  
  
```  
Add-WebApplicationProxyApplication  
     -BackendServerUrl 'https://mail.contoso.com'   
     -ExternalCertificateThumbprint '697F4FF0B9947BB8203A96ED05A3021830638E50'   
     -ExternalUrl 'https://mail.contoso.com'   
     -Name 'Exchange'   
     -ExternalPreAuthentication ADFSforRichClients  
     -ADFSRelyingPartyName 'EAS_Relying_Party'  
```  
  
Workplace 조인 장치에만 다음 사전 인증 합니다.  
  
```  
Add-WebApplicationProxyApplication  
     -BackendServerUrl 'https://mail.contoso.com'   
     -ExternalCertificateThumbprint '697F4FF0B9947BB8203A96ED05A3021830638E50'   
     -EnableHTTPRedirect:$true   
     -ExternalUrl 'https://mail.contoso.com'   
     -Name 'Exchange'   
     -ExternalPreAuthentication ADFSforRichClients  
     -ADFSRelyingPartyName 'EAS_Relying_Party'  
```  
  
## <a name="BKMK_1.4"></a>Microsoft Store 앱과 같은 OAuth2를 사용 하는 응용 프로그램 게시  
Microsoft Store 앱에 대 한 응용 프로그램을 게시 하려면 신뢰 당사자 트러스트를 페더레이션 서비스 응용 프로그램을 추가 해야 합니다.  
  
웹 응용 프로그램 프록시에서에서 single sign-on (SSO) 수행 하 고 Kerberos를 사용 하 여 자격 증명 위임을 수행 하도록 허용 하려면 제한 된 위임을 웹 응용 프로그램 프록시 서버를 도메인에 가입 되어야 합니다. 참조 [Active Directory 계획](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD)합니다.  
  
> [!NOTE]  
> 웹 응용 프로그램 프록시는 OAuth 2.0 프로토콜을 사용 하는 Microsoft Store 앱에 대해서만 게시를 지원 합니다.  
  
AD FS 관리 콘솔에서 OAuth 끝점 프록시가 사용 되는지 확인 해야 합니다. OAuth 끝점에서 프록시를 사용하는지 확인하려면 AD FS 관리 콘솔을 열고 **서비스**를 확장한 다음 **끝점**을 클릭합니다. **끝점** 목록에서 OAuth 끝점을 찾아서 **프록시 사용** 열의 값이 **예**인지 확인합니다.  
  
Microsoft Store 앱을 사용 하는 클라이언트에 대 한 인증 흐름에 대 한 설명은 다음과 같습니다.  
  
> [!NOTE]  
> 웹 응용 프로그램 프록시 인증에 대 한 AD FS 서버로 리디렉션합니다. Microsoft Store 앱을 사용 하는 경우 Microsoft Store 앱에 리디렉션을 지원 하지 않으므로, Set-webapplicationproxyconfiguration cmdlet과 OAuthAuthenticationURL 매개 변수를 사용 하 여 AD FS 서버의 URL을 설정 하는 데 필요한 것입니다.  
>   
> 만 Windows PowerShell을 사용 하 여 Microsoft Store 앱을 게시할 수 있습니다.  
  
1.  클라이언트는 Microsoft Store 앱을 사용 하 여 게시 된 웹 응용 프로그램에 액세스 하려고 합니다.  
  
2.  앱 웹 응용 프로그램 프록시에 의해 게시 된 URL에 HTTPS 요청을 보냅니다.  
  
3.  웹 응용 프로그램 프록시 인증 AD FS 서버의 URL이 포함 된 앱에 HTTP 401 응답을 반환 합니다. 이 프로세스를 '검색' 이라고 합니다.  
  
    > [!NOTE]  
    > 앱 인증 AD FS 서버의 URL을 알고 있고 이미 OAuth 토큰 및에 지 토큰이 포함 된 콤보 토큰을이 인증 흐름에서 2와 3 단계는 건너뜁니다.  
  
4.  앱은 AD FS 서버에 HTTPS 요청을 보냅니다.  
  
5.  앱 웹 인증 브로커를 사용 하 여는 사용자가 AD FS 서버에 인증할 때 자격 증명을 입력 하는 대화 상자를 생성 합니다. 웹 인증 브로커에 대한 자세한 내용은 [웹 인증 브로커](https://msdn.microsoft.com/library/windows/apps/hh750287.aspx)를 참조하세요.  
  
6.  인증이 성공 하면 AD FS 서버 앱에 토큰을 보내고 OAuth 토큰 및에 지 토큰이 포함 된 콤보 토큰을 만듭니다.  
  
7.  앱에 웹 응용 프로그램 프록시에 의해 게시 된 URL로 콤보 토큰이 포함 된 HTTPS 요청을 보냅니다.  
  
8.  웹 응용 프로그램 프록시는 콤보 토큰을 두 부분으로 분할 하 고 여에 지 토큰의 유효성을 검사 합니다.  
  
9. 에 지 토큰이 유효한 경우 웹 응용 프로그램 프록시는 OAuth 토큰만 포함 된 백 엔드 서버로 요청을 전달 합니다. 사용자에게 게시된 웹 응용 프로그램에 대한 액세스 권한이 부여됩니다.  
  
이 절차에서는 OAuth2용 응용 프로그램을 게시하는 방법에 대해 설명합니다. 만 Windows PowerShell을 사용 하 여 이러한 유형의 응용 프로그램을 게시할 수 있습니다. 시작하기 전에 다음 작업을 완료했는지 확인합니다.  
  
-   AD FS 관리 콘솔에서 응용 프로그램에 대 한 신뢰 당사자 트러스트를 생성 합니다.  
  
-   OAuth 끝점에서 AD FS 관리 콘솔을 사용 하도록 설정 하는 프록시 이며 URL 경로 기록해 있게 확인 하십시오.  
  
-   웹 응용 프로그램 프록시 서버에서 인증서를 게시 하려는 응용 프로그램에 적합 한지 확인 합니다.  
  
#### <a name="to-publish-an-oauth2-app"></a>OAuth2 앱을 게시 하려면  
  
1.  원격 액세스 관리 콘솔에서 웹 응용 프로그램 프록시 서버의는 **탐색** 창 클릭 **웹 응용 프로그램 프록시**를 선택한 다음를 **작업** 창 클릭 **게시**합니다.  
  
2.  **새 응용 프로그램 게시 마법사**의 **시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  에 **사전 인증을** 페이지에서 클릭 **Active Directory Federation Services (AD FS)** 를 클릭 하 고 **다음**합니다.  
  
4.  에 **지원 되는 클라이언트** 페이지에서 **OAuth2** 을 클릭 한 다음 **다음**합니다.  
  
5.  **신뢰 당사자** 페이지의 신뢰 당사자 목록에서 게시할 응용 프로그램의 신뢰 당사자를 선택하고 **다음**을 클릭합니다.  
  
6.  **게시 설정** 페이지에서 다음 작업을 수행한 후 **다음**을 클릭합니다.  
  
    -   **이름** 상자에 응용 프로그램의 이름을 입력합니다.  
  
        이 이름은 원격 액세스 관리 콘솔의 게시된 응용 프로그램 목록에만 사용됩니다.  
  
    -   **External URL(외부 URL)** 상자에 이 응용 프로그램의 외부 URL(예: https://server1.contoso.com/app1/)을 입력합니다.  
  
    -   **외부 인증서** 목록에서 주체에 외부 URL이 포함된 인증서를 선택합니다.  
  
        URL에 HTTPS를 입력 하는 것을 잊은 경우에에 사용자가 앱에 액세스할 수 있는지를 확인 하 고, 하려면 선택 합니다 **HTTP-HTTPS 리디렉션을 사용 하도록 설정** 상자입니다.  
  
    -   **백 엔드 서버 URL** 상자에 백 엔드 서버의 URL을 입력합니다. 외부 URL을 입력 하 고 백 엔드 서버 URL이 다른 경우에 변경 해야 하는 경우이 값은 자동으로 입력는 note 예를 들어 https://sp/app1/합니다.  
  
        > [!NOTE]  
        > 웹 응용 프로그램 프록시 Url의 호스트 이름을 변환할 수 있지만 경로 이름을 변환할 수 없습니다. 따라서 서로 다른 호스트 이름을 입력할 수 있지만 경로 이름은 같아야 합니다. 예를 들어 외부 URL을 입력할 수 있습니다 https://apps.contoso.com/app1/ 백 엔드 서버 URL 및 https://app-server/app1/합니다. 그러나 외부 URL을 입력할 수 없습니다 https://apps.contoso.com/app1/ 백 엔드 서버 URL 및 https://apps.contoso.com/internal-app1/합니다.  
  
7.  **확인** 페이지에서 설정을 검토하고 **게시**를 클릭합니다. PowerShell 명령을 복사하여 게시된 추가 응용 프로그램을 설정할 수 있습니다.  
  
8.  **결과** 페이지에서 응용 프로그램이 게시되었는지 확인하고 **닫기**를 클릭합니다.  
  
서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
주소가 fs.contoso.com이 고 /adfs oauth2 / URL 경로 페더레이션 서버에 대 한 OAuth 인증 URL을 설정 합니다.  
  
```  
Set-WebApplicationProxyConfiguration -OAuthAuthenticationURL 'https://fs.contoso.com/adfs/oauth2/'  
```  
  
응용 프로그램을 게시하려면  
  
```  
Add-WebApplicationProxyApplication  
    -BackendServerURL 'https://storeapp.contoso.com/'  
    -ExternalCertificateThumbprint '1a2b3c4d5e6f1a2b3c4d5e6f1a2b3c4d5e6f1a2b'  
    -ExternalURL 'https://storeapp.contoso.com/'  
    -Name 'Microsoft Store app Server'  
    -ExternalPreAuthentication ADFS  
    -ADFSRelyingPartyName 'Store_app_Relying_Party'  
    -UseOAuthAuthentication  
```  
  
## <a name="BKMK_Links"></a>참고 항목  
  
-   [웹 응용 프로그램 프록시 문제 해결](https://technet.microsoft.com/library/dn770156.aspx)  
  
-   [웹 응용 프로그램 프록시를 통한 응용 프로그램 게시](https://technet.microsoft.com/library/dn383659.aspx)  
  
-   [웹 응용 프로그램 프록시를 사용 하 여 응용 프로그램 게시 계획](https://technet.microsoft.com/library/dn383650.aspx)  
  
-   [웹 응용 프로그램 프록시 연습 가이드](https://technet.microsoft.com/library/dn280944.aspx)  
  
-   [Windows PowerShell의 웹 응용 프로그램 프록시 Cmdlet](https://technet.microsoft.com/library/dn283404.aspx)  
  
-   [Add-WebApplicationProxyApplication](https://technet.microsoft.com/library/dn283409.aspx)  
  
-   [Set-WebApplicationProxyConfiguration](https://technet.microsoft.com/library/dn283406.aspx)  
  


