---
ms.assetid: 61ed00fd-51c7-4728-91fa-8501de9d8f28
title: SharePoint, Exchange 및 RDG로 응용 프로그램 게시
description: ''
author: billmath
manager: mtillman
ms.author: billmath
ms.date: 04/30/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: web-app-proxy
ms.openlocfilehash: fd706f61216ab8760d94faf98d651d17b24efc91
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447138"
---
# <a name="publishing-applications-with-sharepoint-exchange-and-rdg"></a>SharePoint, Exchange 및 RDG로 응용 프로그램 게시

>적용 대상: Windows Server 2016

**이 콘텐츠는 웹 응용 프로그램 프록시의 온-프레미스 버전에 적합 합니다. 클라우드를 통해 온-프레미스 응용 프로그램에 대 한 보안 액세스를 사용 합니다 [Azure AD 응용 프로그램 프록시 콘텐츠](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/)합니다.**  

이 항목에서는 SharePoint Server, Exchange Server 또는 웹 응용 프로그램 프록시를 통한 원격 데스크톱 게이트웨이 (RDP)를 게시 하는 데 필요한 작업을 설명 합니다.  

>[!NOTE]
>이 정보로 제공 됩니다-됩니다.  원격 데스크톱 서비스를 지원 하며 사용 하는 것이 좋습니다 [안전한 원격 액세스를 제공 하기 위해 Azure App Proxy 온-프레미스 응용 프로그램](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)합니다.

## <a name="BKMK_6.1"></a>Publish SharePoint Server  
SharePoint 사이트가 클레임 기반 인증 또는 Windows 통합 인증을 위한 구성 된 경우 웹 응용 프로그램 프록시를 통해 SharePoint 사이트를 게시할 수 있습니다. Active Directory Federation Services (AD FS) 사전 인증을 사용 하려는 경우에 마법사 중 하나를 사용 하 여 신뢰 당사자를 구성 해야 합니다.  

-   SharePoint 사이트에서 클레임 기반 인증을 사용하는 경우에는 신뢰 당사자 트러스트 추가 마법사를 사용하여 응용 프로그램에 대한 신뢰 당사자 트러스트를 구성해야 합니다.  

-   SharePoint 사이트에서 Windows 통합 인증을 사용하는 경우에는 비 클레임 기반 신뢰 당사자 트러스트 추가 마법사를 사용하여 응용 프로그램에 대한 신뢰 당사자 트러스트를 구성해야 합니다. KDC를 구성한 경우 클레임 기반 웹 응용 프로그램과 IWA를 사용할 수 있습니다.  

    사용자가 Windows 통합 인증을 사용 하 여 인증할 수 있도록 웹 응용 프로그램 프록시 서버를 도메인에 가입 해야 합니다.  

    Kerberos 제한 위임을 지원하도록 응용 프로그램을 구성해야 합니다. 이 작업은 도메인 컨트롤러에서 모든 응용 프로그램에 대해 수행할 수 있습니다. 또한 Windows Server 2012 R2 또는 Windows Server 2012에서 실행 중인 경우 백 엔드 서버에서 직접 응용 프로그램을 구성할 수 있습니다. 자세한 내용은 [Kerberos 인증의 새로운 기능](https://technet.microsoft.com/library/hh831747.aspx)을 참조하세요. 또한 백 엔드 서버의 서비스 사용자 이름에 위임에 대 한 웹 응용 프로그램 프록시 서버 구성 되어 있는지 확인 해야 합니다. 통합 Windows 인증을 사용 하 여 응용 프로그램을 게시 하려면 웹 응용 프로그램 프록시를 구성 하는 방법의 연습을 참조 하세요 [통합 Windows 인증을 사용 하도록 사이트 구성](assetId:///b0788958-627f-450f-877c-209b1bd0db52)합니다.  

SharePoint 사이트가 AAM(대체 액세스 매핑) 또는 호스트 이름이 지정된 사이트 컬렉션 중 하나를 사용하여 구성된 경우 다른 외부 및 백 엔드 서버 URL을 사용하여 응용 프로그램을 게시할 수 있습니다. 그러나 AAM 또는 호스트 이름이 지정된 사이트 컬렉션을 사용하여 SharePoint 사이트를 구성하지 않은 경우 동일한 외부 및 백 엔드 서버 URL을 사용해야 합니다.  

## <a name="BKMK_6.2"></a>Publish Exchange Server  
다음 표에서 웹 응용 프로그램 프록시 및 이러한 서비스에 대 한 지원 되는 사전 인증을 통해 게시할 수 있는 Exchange 서비스를 설명 합니다.  


|    Exchange 서비스    |                                                                            사전 인증                                                                            |                                                                                                                                       참고                                                                                                                                        |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Outlook Web App     | 비 클레임 기반 인증을 사용 하 여 AD FS<br />-통과<br />AD FS 클레임 기반 인증을 사용 하 여 온-프레미스 Exchange 2013 서비스 팩 1 (SP1)에 대 한 |                                                                  자세한 내용은 다음을 참조하세요. [Outlook Web App 및 EAC에서 AD FS 클레임 기반 인증 사용](https://go.microsoft.com/fwlink/?LinkId=393723)                                                                  |
| Exchange 제어판 |                                                                               통과                                                                               |                                                                                                                                                                                                                                                                                    |
|    외부에서 Outlook 사용    |                                                                               통과                                                                               | 올바로 작동하려면 외부에서 Outlook 사용에 대한 다음 3개의 URL을 게시해야 합니다.<br /><br />-자동 검색 URL입니다.<br />-Exchange 서버의 외부 호스트 이름 즉, 클라이언트에 연결 하기 위해 구성 된 URL입니다.<br />Exchange 서버의 내부 FQDN-합니다. |
|  Exchange ActiveSync   |                                                     통과<br/> HTTP 기본 인증 프로토콜을 사용 하 여 AD FS                                                      |                                                                                                                                                                                                                                                                                    |

Windows 통합 인증을 사용하여 Outlook Web App을 게시하는 경우에는 비 클레임 기반 신뢰 당사자 트러스트 추가 마법사를 사용하여 응용 프로그램에 대한 신뢰 당사자 트러스트를 구성해야 합니다.  

사용자가 Kerberos를 사용 하 여 인증할 수 있도록 웹 응용 프로그램 프록시 서버를 도메인에 가입 되어 있어야 하는 위임을 제한 합니다.  

Kerberos 인증을 지원 하도록 응용 프로그램을 구성 해야 합니다. 또한 등록 해야 서비스 사용자 이름 (SPN) 웹 서비스를 실행 하는 계정에 있습니다. 백 엔드 서버 또는 도메인 컨트롤러에서이 수행할 수 있습니다. 이 대체 서비스 계정을 사용 해야 하는 분산 된 Exchange 환경 참조 부하에서 [부하 분산 된 클라이언트 액세스 서버에 대 한 구성 Kerberos 인증](https://technet.microsoft.com/library/ff808312(v=exchg.150).aspx)  

또한 Windows Server 2012 R2 또는 Windows Server 2012에서 실행 중인 경우 백 엔드 서버에서 직접 응용 프로그램을 구성할 수 있습니다. 자세한 내용은 [Kerberos 인증의 새로운 기능](https://technet.microsoft.com/library/hh831747.aspx)을 참조하세요. 또한 백 엔드 서버의 서비스 사용자 이름에 위임에 대 한 웹 응용 프로그램 프록시 서버 구성 되어 있는지 확인 해야 합니다.  

## <a name="publishing-remote-desktop-gateway-through-web-application-proxy"></a>웹 응용 프로그램 프록시를 통한 원격 데스크톱 게이트웨이 게시합니다.  
원격 액세스 게이트웨이에 대 한 액세스를 제한 하 고 원격 액세스를 위한 사전 인증을 추가 하려는 경우 웹 응용 프로그램 프록시를 통한 롤백할 수 있습니다. 이것이 MFA를 포함 하는 RDG에 대 한 다양 한 사전 인증 했는지 확인 하는 좋은 방법입니다. 사전 인증 없이 게시 옵션 이기도 하 고 단일 시스템에 대 한 입력을 제공 합니다.  

#### <a name="how-to-publish-an-application-in-rdg-using-web-application-proxy-pass-through-authentication"></a>RDG 웹 응용 프로그램 프록시 통과 인증을 사용 하 여에서 응용 프로그램을 게시 하는 방법  

1. 설치 여부에 따라 달라 지므로 RD 웹 액세스 (/ rdweb)가 있고 동일한 서버나 다른 서버에서 RD 게이트웨이 (rpc) 역할을 합니다.  

2. 경우 RD 웹 액세스 및 RD 게이트웨이 역할을 동일한 RDG 서버에서 호스트를 게시할 수 있습니다 단순히 FQDN 루트 웹 응용 프로그램 프록시에서 같은 https://rdg.contoso.com/합니다.  

   게시할 수도 있습니다 두 가상 디렉터리를 개별적으로 예를 들어<https://rdg.contoso.com/rdweb/> 고 https://rdg.contoso.com/rpc/입니다.  

3. RD 웹 액세스 및 RD 게이트웨이 별도 RDG 서버에서 호스팅되는, 경우에 두 개의 가상 디렉터리를 개별적으로 게시 해야 합니다. 예를 들어 동일한 또는 다른 외부 FQDN의 사용할 수 있습니다 https://rdweb.contoso.com/rdweb/ 고 https://gateway.contoso.com/rpc/입니다.  

4. 외부 및 내부 FQDN 다르면 RDWeb 게시 규칙에 요청 헤더 변환을 사용 해야 합니다. 웹 응용 프로그램 프록시 서버에서 다음 PowerShell 스크립트를 실행 하 여 수행할 수 있습니다이 있지만 기본적으로 사용 합니다.

   ```  
   Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableTranslateUrlInRequestHeaders:$false  
   ```  

   > [!NOTE]  
   > RemoteApp 및 데스크톱 연결 또는 원격 데스크톱 연결을 iOS와 같은 다양 한 클라이언트를 지원 해야 할 경우 이러한 인증을 지원 하지 사전 RDG 통과 인증을 사용 하 여 게시 해야 합니다.  

#### <a name="how-to-publish-an-application-in-rdg-using-web-application-proxy-with-pre-authentication"></a>RDG 웹 응용 프로그램 프록시를 사용 하 여 사전 인증에서 응용 프로그램을 게시 하는 방법  

1.  RDG 웹 응용 프로그램 프록시 사전 인증 하면 원격 데스크톱 연결 클라이언트 (mstsc.exe)에 전달 되는 Internet Explorer에서 얻은 사전 인증 쿠키를 전달 하 여 작동 합니다. 그런 다음 원격 데스크톱 연결 클라이언트 (mstsc.exe)에서 사용 됩니다. 그런 다음 인증 증거로 원격 데스크톱 연결 클라이언트에서 사용 됩니다.  

    다음 절차에는 클라이언트로 전송 되는 원격 앱 RDP 파일에 필요한 사용자 지정 RDP 속성을 포함 하는 컬렉션 서버를 지시 합니다. 이러한 파일을 클라이언트는 사전 인증 필요 하 고 사전 인증에 대 한 쿠키를 전달 하려면 서버 원격 데스크톱 연결 클라이언트 (mstsc.exe)를 해결 합니다. 웹 응용 프로그램 프록시 응용 프로그램은 HttpOnly 기능을 사용 하지 않도록 설정 하는와 함께,이 통해 브라우저를 통해 가져온 웹 응용 프로그램 프록시 쿠키를 활용 하려면 원격 데스크톱 연결 클라이언트 (mstsc.exe).  

    RD 웹 액세스 서버에 인증 하는 RD 웹 액세스 양식 로그온 사용 하 여 계속 합니다. 최소 제공 사용자 인증 수가 대로 RD 웹 액세스 로그온 폼에 사용할 수 있는 다음 원격 데스크톱 연결 클라이언트 (mstsc.exe)에서 모든 후속 원격 앱 시작에 대 한 클라이언트 쪽 자격 증명 저장소를 만듭니다. 라는 메시지가 표시 됩니다.  

2.  먼저 클레임 인식 앱을 게시 된 것 처럼 수동으로 신뢰 당사자 트러스트 AD FS에서 만듭니다. 이 신뢰 당사자 트러스트에 포함 된 사전 인증을 적용 하려면 게시 된 서버를 Kerberos 제한 된 위임 없이 사전 인증을 받을 수 있도록 dummy를 만들 필요가 있는 것을 의미 합니다. 사용자가 인증 되 면 나머지 전달 됩니다.  

    > [!WARNING]  
    > 위임을 사용 하는 것이 좋습니다 있지만 mstsc SSO 요구 사항을 완전히 해결 되지 않으면을 클라이언트 자체 RD 게이트웨이 인증을 처리 하는 것으로 예상 하므로 /rpc 디렉터리에 위임 하는 경우 문제가 있는 것 처럼 보일 수 있습니다.  

3.  수동으로 신뢰 당사자 트러스트를 만들려면 AD FS 관리 콘솔에서 단계를 수행 합니다.  

    1.  사용 된 **신뢰 당사자 트러스트 추가** 마법사  

    2.  선택 **신뢰 당사자에 대 한 데이터를 수동으로 입력**합니다.  

    3.  모든 기본 설정을 적용 합니다.  

    4.  신뢰 당사자 트러스트 식별자에 대 한 예를 들어 RDG 액세스에 사용할 외부 FQDN을 입력 https://rdg.contoso.com/합니다.  

        웹 응용 프로그램 프록시에서 앱을 게시할 때 사용할 신뢰 당사자 트러스트입니다.  

4.  사이트의 루트를 게시 (예를 들어 https://rdg.contoso.com/ ) 웹 응용 프로그램 프록시에서입니다. AD fs 사전 인증을 설정 하 고 위에서 만든 신뢰 당사자 트러스트를 사용 합니다. 이렇게 하면 /rdweb와 동일한 웹 응용 프로그램 프록시 인증 쿠키를 사용 하는 /rpc 사용 됩니다.  

    /Rdweb 및 /rpc 별도 응용 프로그램으로 게시 하 고 다른 게시 된 서버를 사용 하 여도 가능 합니다. 웹 응용 프로그램 프록시 토큰을 신뢰 당사자 트러스트에 대해 실행 되 고 유효 하므로 동일한 신뢰 당사자 트러스트 된 게시 된 응용 프로그램에서 동일한 신뢰 당사자 트러스트를 사용 하는 모두 게시할 수 있도록 하기만 하면 됩니다.  

5.  외부 및 내부 FQDN 다르면 RDWeb 게시 규칙에 요청 헤더 변환을 사용 해야 합니다. 이 웹 응용 프로그램 프록시 서버에서 다음 PowerShell 스크립트를 실행 하 여 수행할 수 있습니다 하지만 기본적으로 활성화 되어야 합니다.

    ```  
    Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableTranslateUrlInRequestHeaders:$false 
    ```  

6.  게시 된 응용 프로그램을 웹 응용 프로그램 프록시는 RDG에 HttpOnly 쿠키 속성을 사용 하지 않도록 설정 합니다. 웹 응용 프로그램 프록시 인증 쿠키에 RDG ActiveX 컨트롤 액세스를 허용 하려면 웹 응용 프로그램 프록시 쿠키는 HttpOnly 속성을 사용 하지 않도록 설정 해야 합니다.  

    이렇게 하려면 다음을 설치할 [웹 응용 프로그램 프록시 핫픽스](https://support.microsoft.com/en-gb/kb/3000850) 또는 [ https://support.microsoft.com/en-gb/kb/3000850 ](https://support.microsoft.com/en-gb/kb/3000850)합니다.  

    핫픽스를 설치한 후 관련 응용 프로그램 이름을 지정 하는 웹 응용 프로그램 프록시 서버에서 다음 PowerShell 스크립트를 실행 합니다.  

    ```  
    Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableHttpOnlyCookieProtection:$true  
    ```  

    웹 응용 프로그램 프록시 인증 쿠키에 RDG ActiveX 컨트롤 액세스를 허용 HttpOnly를 사용 하지 않도록 설정 합니다.  

7.  원격 데스크톱 연결 클라이언트 (mstsc.exe) rdp 파일에는 사전 인증이 필요한 알 수 있도록 컬렉션 서버의 관련 RDG 컬렉션을 구성 합니다.  

    -   Windows Server 2012 및 Windows Server 2012 R2에서 RDG 수집 서버에서 다음 PowerShell cmdlet을 실행 하 여 수행할 수 있습니다.  

        ```
        Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s: <https://externalfqdn/rdweb/>`nrequire pre-authentication:i:1"
        ```

        제거 해야 합니다 < 및 > 대괄호 예를 들어 사용자 고유의 값으로 대체 하면:

        ```
        Set-RDSessionCollectionConfiguration -CollectionName "MyAppCollection" -CustomRdpProperty "pre-authentication server address:s: https://rdg.contoso.com/rdweb/`nrequire pre-authentication:i:1"
        ```

    -   Windows Server 2008 r2:  

        1.  관리자 권한이 있는 계정 사용 하 여 터미널 서버에 로그온 합니다.  

        2.  로 이동 **시작** >**관리 도구** > **터미널 서비스** > **TS RemoteApp 관리자입니다.**  

        3.  에 **개요** TS RemoteApp 관리자의 RDP 설정 옆에 있는 창 클릭 **변경**합니다.  

        4.  에 **사용자 지정 RDP 설정** 탭에서 다음 RDP 설정을 사용자 지정 RDP 설정 상자에 입력 합니다.  

            `pre-authentication server address: s: https://externalfqdn/rdweb/`  

            `require pre-authentication:i:1`  

        5.  완료 되 면 **적용**합니다.  

            이렇게 하면 클라이언트로 전송 되는 RDP 파일에 사용자 지정 RDP 속성을 포함 하는 컬렉션 서버. 이러한 클라이언트는 사전 인증 필수 항목이 며 서버 주소 사전 인증에 대 한 쿠키를 전달 하는 원격 데스크톱 연결 클라이언트 (mstsc.exe)를 알립니다. 따라서, 웹 응용 프로그램 프록시 응용 프로그램은 HttpOnly를 사용 하지 않도록 설정 하는 작업을 함께에서 원격 데스크톱 연결 클라이언트를 수 (mstsc.exe) 브라우저를 통해 가져온 웹 응용 프로그램 프록시 인증 쿠키를 활용 하 합니다.  

            RDP에 대 한 자세한 내용은 참조 하세요. [TS 게이트웨이 OTP 시나리오 구성](https://technet.microsoft.com/library/cc731249(v=ws.10).aspx)합니다.  

## <a name="BKMK_Links"></a>참고 항목  

-   [웹 응용 프로그램 프록시를 사용 하 여 응용 프로그램 게시 계획](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383650(v=ws.11))  

-   [웹 애플리케이션 프록시 문제 해결](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn770156(v=ws.11))  

-   [웹 응용 프로그램 프록시 연습 가이드](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280944(v=ws.11))  
