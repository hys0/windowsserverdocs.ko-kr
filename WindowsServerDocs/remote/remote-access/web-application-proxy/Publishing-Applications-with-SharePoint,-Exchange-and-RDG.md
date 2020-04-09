---
ms.assetid: 61ed00fd-51c7-4728-91fa-8501de9d8f28
title: SharePoint, Exchange 및 RDG로 응용 프로그램 게시
author: billmath
manager: mtillman
ms.author: billmath
ms.date: 04/30/2018
ms.topic: article
ms.prod: windows-server
ms.technology: web-app-proxy
ms.openlocfilehash: 18851463b82afc1dc34615e6faaa14622c80224a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818686"
---
# <a name="publishing-applications-with-sharepoint-exchange-and-rdg"></a>SharePoint, Exchange 및 RDG로 응용 프로그램 게시

> 적용 대상: Windows Server 2016

**이 콘텐츠는 웹 응용 프로그램 프록시의 온-프레미스 버전과 관련이 있습니다. 클라우드를 통해 온-프레미스 응용 프로그램에 안전 하 게 액세스할 수 있도록 하려면 [Azure AD 응용 프로그램 프록시 콘텐츠](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/)를 참조 하세요.**

이 항목에서는 웹 응용 프로그램 프록시를 통해 SharePoint Server, Exchange Server 또는 RDP (원격 데스크톱 게이트웨이)를 게시 하는 데 필요한 작업에 대해 설명 합니다.

> [!NOTE]
> 이 정보는 있는 그대로 제공 됩니다.  원격 데스크톱 서비스에서는 Azure 앱 프록시를 사용 하 여 [온-프레미스 응용 프로그램에 보안 원격 액세스를 제공](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)하는 것을 권장 합니다.

## <a name="publish-sharepoint-server"></a><a name="BKMK_6.1"></a>SharePoint 서버 게시
SharePoint 사이트가 클레임 기반 인증 또는 Windows 통합 인증을 사용 하도록 구성 된 경우에는 웹 응용 프로그램 프록시를 통해 SharePoint 사이트를 게시할 수 있습니다. 사전 인증에 Active Directory Federation Services (AD FS)를 사용 하려는 경우 마법사 중 하나를 사용 하 여 신뢰 당사자를 구성 해야 합니다.

-   SharePoint 사이트에서 클레임 기반 인증을 사용하는 경우에는 신뢰 당사자 트러스트 추가 마법사를 사용하여 애플리케이션에 대한 신뢰 당사자 트러스트를 구성해야 합니다.

-   SharePoint 사이트에서 Windows 통합 인증을 사용하는 경우에는 비 클레임 기반 신뢰 당사자 트러스트 추가 마법사를 사용하여 애플리케이션에 대한 신뢰 당사자 트러스트를 구성해야 합니다. KDC를 구성한 경우 클레임 기반 웹 애플리케이션과 IWA를 사용할 수 있습니다.

    사용자가 Windows 통합 인증을 사용 하 여 인증할 수 있도록 하려면 웹 응용 프로그램 프록시 서버가 도메인에 가입 되어 있어야 합니다.

    Kerberos 제한 위임을 지원하도록 애플리케이션을 구성해야 합니다. 이 작업은 도메인 컨트롤러에서 모든 애플리케이션에 대해 수행할 수 있습니다. 또한 Windows Server 2012 R2 또는 Windows Server 2012에서 실행 중인 경우 백 엔드 서버에서 직접 응용 프로그램을 구성할 수 있습니다. 자세한 내용은 [Kerberos 인증의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831747(v=ws.11))을 참조하세요. 또한 웹 응용 프로그램 프록시 서버가 백 엔드 서버의 서비스 사용자 이름에 위임 되도록 구성 되었는지 확인 해야 합니다. Windows 통합 인증을 사용 하 여 응용 프로그램을 게시 하도록 웹 응용 프로그램 프록시를 구성 하는 방법에 대 한 연습은 [Windows 통합 인증을 사용 하도록 사이트 구성](https://docs.microsoft.com/previous-versions/orphan-topics/ws.11/dn308246(v=ws.11))을 참조 하세요.

SharePoint 사이트가 AAM(대체 액세스 매핑) 또는 호스트 이름이 지정된 사이트 컬렉션 중 하나를 사용하여 구성된 경우 다른 외부 및 백 엔드 서버 URL을 사용하여 애플리케이션을 게시할 수 있습니다. 그러나 AAM 또는 호스트 이름이 지정된 사이트 컬렉션을 사용하여 SharePoint 사이트를 구성하지 않은 경우 동일한 외부 및 백 엔드 서버 URL을 사용해야 합니다.

## <a name="publish-exchange-server"></a><a name="BKMK_6.2"></a>Exchange Server 게시
다음 표에서는 웹 응용 프로그램 프록시를 통해 게시할 수 있는 Exchange 서비스와 이러한 서비스에 대해 지원 되는 사전 인증에 대해 설명 합니다.


|    Exchange 서비스    |                                                                            사전 인증                                                                            |                                                                                                                                       참고                                                                                                                                        |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Outlook Web App     | -비 클레임 기반 인증을 사용 하 AD FS<br />-통과<br />-온-프레미스 Exchange 2013 서비스 팩 1 (SP1)에 대 한 클레임 기반 인증을 사용 하는 AD FS |                                                                  자세한 내용은 [Outlook Web App 및 EAC에서 AD FS 클레임 기반 인증 사용](https://go.microsoft.com/fwlink/?LinkId=393723)을 참조하세요.                                                                  |
| Exchange 제어판 |                                                                               통과                                                                               |                                                                                                                                                                                                                                                                                    |
|    외부에서 Outlook 사용    |                                                                               통과                                                                               | 올바로 작동하려면 외부에서 Outlook 사용에 대한 다음 3개의 URL을 게시해야 합니다.<p>-자동 검색 URL입니다.<br />-Exchange Server의 외부 호스트 이름 즉, 클라이언트에 연결 하도록 구성 된 URL입니다.<br />-Exchange Server의 내부 FQDN |
|  Exchange ActiveSync   |                                                     통과<br/> HTTP 기본 권한 부여 프로토콜을 사용 하 AD FS                                                      |                                                                                                                                                                                                                                                                                    |

Windows 통합 인증을 사용하여 Outlook Web App을 게시하는 경우에는 비 클레임 기반 신뢰 당사자 트러스트 추가 마법사를 사용하여 애플리케이션에 대한 신뢰 당사자 트러스트를 구성해야 합니다.

사용자가 Kerberos 제한 위임을 사용 하 여 인증할 수 있도록 하려면 웹 응용 프로그램 프록시 서버가 도메인에 가입 되어 있어야 합니다.

Kerberos 인증을 지원 하도록 응용 프로그램을 구성 해야 합니다. 또한 웹 서비스가 실행 되는 계정에 SPN (서비스 사용자 이름)을 등록 해야 합니다. 도메인 컨트롤러 또는 백 엔드 서버에서이 작업을 수행할 수 있습니다. 부하가 분산 된 Exchange 환경에서는 대체 서비스 계정을 사용 해야 합니다. [부하 분산 클라이언트 액세스 서버에 대 한 Kerberos 인증 구성](https://docs.microsoft.com/exchange/configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help) 을 참조 하세요.

또한 Windows Server 2012 R2 또는 Windows Server 2012에서 실행 중인 경우 백 엔드 서버에서 직접 응용 프로그램을 구성할 수 있습니다. 자세한 내용은 [Kerberos 인증의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831747(v=ws.11))을 참조하세요. 또한 웹 응용 프로그램 프록시 서버가 백 엔드 서버의 서비스 사용자 이름에 위임 되도록 구성 되었는지 확인 해야 합니다.

## <a name="publishing-remote-desktop-gateway-through-web-application-proxy"></a>웹 응용 프로그램 프록시를 통해 원격 데스크톱 게이트웨이 게시
원격 액세스 게이트웨이에 대 한 액세스를 제한 하 고 원격 액세스에 대 한 사전 인증을 추가 하려는 경우 웹 응용 프로그램 프록시를 통해 롤아웃할 수 있습니다. 이 방법은 MFA를 포함 하 여 RDG에 대 한 풍부한 사전 인증이 있는지 확인 하는 매우 좋은 방법입니다. 사전 인증 없이 게시는 옵션 이기도 하며 시스템에 대 한 단일 진입점을 제공 합니다.

#### <a name="how-to-publish-an-application-in-rdg-using-web-application-proxy-pass-through-authentication"></a>웹 응용 프로그램 프록시 통과 인증을 사용 하 여 RDG에 응용 프로그램을 게시 하는 방법

1. RD 웹 액세스 (/rdweb) 및 RD 게이트웨이 (rpc) 역할이 동일한 서버나 다른 서버에 있는지 여부에 따라 설치는 달라 집니다.

2. RD 웹 액세스 및 RD 게이트웨이 역할이 동일한 RDG 서버에서 호스트 되는 경우, https://rdg.contoso.com/와 같은 웹 응용 프로그램 프록시에 루트 FQDN을 게시 하면 됩니다.

   두 가상 디렉터리를 개별적으로 게시할 수도 있습니다 (예:<https://rdg.contoso.com/rdweb/> 및 https://rdg.contoso.com/rpc/).

3. RD 웹 액세스 및 RD 게이트웨이 별도의 RDG 서버에서 호스트 되는 경우 두 가상 디렉터리를 개별적으로 게시 해야 합니다. 동일한 또는 다른 외부 FQDN (예: https://rdweb.contoso.com/rdweb/ 및 https://gateway.contoso.com/rpc/를 사용할 수 있습니다.

4. 외부 및 내부 FQDN이 다르면 RDWeb 게시 규칙에서 요청 헤더 변환을 사용 하지 않도록 설정 하면 안 됩니다. 웹 응용 프로그램 프록시 서버에서 다음 PowerShell 스크립트를 실행 하 여이 작업을 수행할 수 있지만 기본적으로 사용 하도록 설정 해야 합니다.

   ```PowerShell
   Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableTranslateUrlInRequestHeaders:$false
   ```

   > [!NOTE]
   > RemoteApp, 데스크톱 연결 또는 iOS 원격 데스크톱 연결과 같은 리치 클라이언트를 지원 해야 하는 경우에는 사전 인증을 지원 하지 않으므로 통과 인증을 사용 하 여 RDG를 게시 해야 합니다.

#### <a name="how-to-publish-an-application-in-rdg-using-web-application-proxy-with-pre-authentication"></a>사전 인증을 사용 하는 웹 응용 프로그램 프록시를 사용 하 여 RDG에 응용 프로그램을 게시 하는 방법

1.  RDG를 사용 하는 웹 응용 프로그램 프록시 사전 인증은 원격 데스크톱 연결 클라이언트 (mstsc)로 전달 되는 Internet Explorer에서 얻은 사전 인증 쿠키를 전달 하 여 작동 합니다. 이는 원격 데스크톱 연결 클라이언트 (mstsc)에서 사용 됩니다. 이는 원격 데스크톱 연결 클라이언트에서 인증 증명으로 사용 됩니다.

    다음 절차에서는 클라이언트에 전송 되는 원격 응용 프로그램 RDP 파일에 필요한 사용자 지정 RDP 속성을 포함 하도록 컬렉션 서버에 지시 합니다. 클라이언트에 사전 인증이 필요 하 고 사전 인증 서버 주소에 대 한 쿠키를 원격 데스크톱 연결 client (mstsc)에 전달 하도록 클라이언트에 지시 합니다. 웹 응용 프로그램 프록시 응용 프로그램에서 HttpOnly 기능을 사용 하지 않도록 설정 하는 것과 함께 원격 데스크톱 연결 클라이언트 (mstsc)는 브라우저를 통해 가져온 웹 응용 프로그램 프록시 쿠키를 활용할 수 있습니다.

    RD 웹 액세스 서버에 대 한 인증은 RD 웹 액세스 양식 로그온을 계속 사용 합니다. RD 웹 액세스 logon 양식이 클라이언트 쪽 자격 증명 저장소를 만들 때 가장 적은 수의 사용자 인증 프롬프트를 제공 합니다 .이 자격 증명 저장소는 이후의 원격 앱 시작을 위해 원격 데스크톱 연결 클라이언트 (mstsc)에서 사용할 수 있습니다.

2.  먼저 클레임 인식 앱을 게시 하는 것 처럼 AD FS에서 수동 신뢰 당사자 트러스트를 만듭니다. 즉, 게시 된 서버에 대 한 Kerberos 제한 위임 없이 사전 인증을 받을 수 있도록 사전 인증을 적용할 더미 신뢰 당사자 트러스트를 만들어야 합니다. 사용자가 인증 되 면 다른 모든 항목이 전달 됩니다.

    > [!WARNING]
    > 위임을 사용 하는 것이 더 낫지만, 클라이언트에서 RD 게이트웨이 인증 자체를 처리할 것으로 예상 하기 때문에/sourcesso 요구 사항을 완전 하 게 해결 하지 않으며/rpc 디렉터리에 위임할 때 문제가 있습니다.

3.  수동 신뢰 당사자 트러스트를 만들려면 AD FS 관리 콘솔의 단계를 수행 합니다.

    1.  신뢰 당사자 **트러스트 추가** 마법사 사용

    2.  **신뢰 당사자에 대 한 데이터를 수동으로 입력을**선택 합니다.

    3.  모든 기본 설정을 적용 합니다.

    4.  신뢰 당사자 트러스트 식별자에 대해 RDG 액세스에 사용할 외부 FQDN (예: https://rdg.contoso.com/을 입력 합니다.

        웹 응용 프로그램 프록시에서 앱을 게시할 때 사용 하는 신뢰 당사자 트러스트입니다.

4.  웹 응용 프로그램 프록시에 사이트의 루트 (예: https://rdg.contoso.com/)를 게시 합니다. AD FS에 대 한 사전 인증을 설정 하 고 위에서 만든 신뢰 당사자 트러스트를 사용 합니다. 이렇게 하면/rdweb 및/trpc가 동일한 웹 응용 프로그램 프록시 인증 쿠키를 사용할 수 있습니다.

    /Rdweb 및/rpc를 별도의 응용 프로그램으로 게시 하 고 다른 게시 된 서버를 사용할 수도 있습니다. 신뢰 당사자 트러스트에 대해 웹 응용 프로그램 프록시 토큰이 발급 되므로 동일한 신뢰 당사자 트러스트를 사용 하 여 둘 다 게시 해야 하며, 따라서 동일한 신뢰 당사자 트러스트를 사용 하 여 게시 된 응용 프로그램 전체에서 유효 합니다.

5.  외부 및 내부 FQDN이 다르면 RDWeb 게시 규칙에서 요청 헤더 변환을 사용 하지 않도록 설정 하면 안 됩니다. 웹 응용 프로그램 프록시 서버에서 다음 PowerShell 스크립트를 실행 하 여이 작업을 수행할 수 있지만 기본적으로 사용 하도록 설정 해야 합니다.

    ```PowerShell
    Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableTranslateUrlInRequestHeaders:$false
    ```

6.  RDG 게시 된 응용 프로그램의 웹 응용 프로그램 프록시에서 HttpOnly 쿠키 속성을 사용 하지 않도록 설정 합니다. RDG ActiveX 컨트롤에 웹 응용 프로그램 프록시 인증 쿠키에 대 한 액세스를 허용 하려면 웹 응용 프로그램 프록시 쿠키에서 HttpOnly 속성을 사용 하지 않도록 설정 해야 합니다.

    이렇게 하려면 [WINDOWS RT 8.1, Windows 8.1 및 Windows Server 2012 R2 (KB3000850)에 대 한 11 월 2014 업데이트 롤업을](https://support.microsoft.com/kb/3000850)설치 해야 합니다.

    핫픽스를 설치한 후에는 관련 응용 프로그램 이름을 지정 하 여 웹 응용 프로그램 프록시 서버에서 다음 PowerShell 스크립트를 실행 합니다.

    ```PowerShell
    Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableHttpOnlyCookieProtection:$true
    ```

    HttpOnly를 사용 하지 않도록 설정 하면 RDG ActiveX 컨트롤에서 웹 응용 프로그램 프록시 인증 쿠키에 액세스할 수 있습니다.

7.  원격 데스크톱 연결 클라이언트 (mstsc)가 rdp 파일에서 사전 인증을 요구 하는 것을 알 수 있도록 컬렉션 서버에서 관련 RDG 컬렉션을 구성 합니다.

    -   Windows Server 2012 및 Windows Server 2012 r 2에서는 RDG 컬렉션 서버에서 다음 PowerShell cmdlet을 실행 하 여이 작업을 수행할 수 있습니다.

        ```PowerShell
        Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s: <https://externalfqdn/rdweb/>`nrequire pre-authentication:i:1"
        ```

        사용자 고유의 값으로 바꿀 때 < 및 대괄호 > 제거 해야 합니다. 예를 들면 다음과 같습니다.

        ```PowerShell
        Set-RDSessionCollectionConfiguration -CollectionName "MyAppCollection" -CustomRdpProperty "pre-authentication server address:s: https://rdg.contoso.com/rdweb/`nrequire pre-authentication:i:1"
        ```

    -   Windows Server 2008 R2:

        1.  관리자 권한이 있는 계정으로 터미널 서버에 로그온 합니다.

        2.  **시작** >**관리 도구** > **터미널 서비스** > **TS RemoteApp 관리자로 이동 합니다.**

        3.  TS RemoteApp Manager의 **개요** 창에서 RDP 설정 옆의 **변경**을 클릭 합니다.

        4.  **사용자 지정 rdp** 설정 탭의 사용자 지정 rdp 설정 상자에 다음 rdp 설정을 입력 합니다.

            `pre-authentication server address: s: https://externalfqdn/rdweb/`

            `require pre-authentication:i:1`

        5.  완료 되 면 **적용**을 클릭 합니다.

            이렇게 하면 클라이언트에 전송 되는 RDP 파일에 사용자 지정 RDP 속성을 포함 하도록 컬렉션 서버에 지시 합니다. 클라이언트에 사전 인증이 필요 하 고 사전 인증 서버 주소에 대 한 쿠키를 원격 데스크톱 연결 클라이언트 (mstsc)에 전달 하도록 클라이언트에 지시 합니다. 이를 통해 웹 응용 프로그램 프록시 응용 프로그램에서 HttpOnly를 사용 하지 않도록 설정 하면 원격 데스크톱 연결 클라이언트 (mstsc)가 브라우저를 통해 가져온 웹 응용 프로그램 프록시 인증 쿠키를 활용할 수 있습니다.

            RDP에 대 한 자세한 내용은 [TS 게이트웨이 OTP 시나리오 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731249(v=ws.10))을 참조 하세요.

## <a name="see-also"></a><a name="BKMK_Links"></a>참고 항목

- [웹 응용 프로그램 프록시를 사용 하 여 응용 프로그램 게시 계획](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383650(v=ws.11))

- [웹 애플리케이션 프록시 문제 해결](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn770156(v=ws.11))

- [웹 응용 프로그램 프록시 연습 가이드](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280944(v=ws.11))
