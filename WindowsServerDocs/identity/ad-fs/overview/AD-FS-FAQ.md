---
ms.assetid: acc9101b-841c-4540-8b3c-62a53869ef7a
title: AD 2016 FS FAQ
description: "AD FS 2016에 대 한 질문과 대답"
author: jenfieldmsft
ms.author: billmath
manager: femila
ms.date: 03/06/2018
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 313447d2c92c15505434ec5c39898ca84aef46db
ms.sourcegitcommit: 556361fe7c73c75d6cdc46a67dc88679fbe89c61
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="ad-fs-frequently-asked-questions-faq"></a>ADFS (FAQ 질문과)

>Windows Server 2016 적용 됩니다.

이 문서 홈 Active Directory Federation Services와 관련 된 질문과 대답입니다.  문서에 질문의 종류에 따라 그룹별로 분할 되었습니다.

## <a name="deployment"></a>배포 

### <a name="how-can-i-upgrademigrate-from-previous-versions-of-ad-fs"></a>어떻게 마이그레이션할 수 있습니까 업그레이드/Adfs의 이전 버전에서 인가요
다음 중 하나를 사용 하 여 ADFS 업그레이드할 수 있습니다.


- Windows Server 2012 r 2 ADFS Windows Server 2016 광고 FS
    - [Adfs의 Windows Server 2016 WID 데이터베이스를 사용 하 여 업그레이드](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)
    - [Adfs의 Windows Server 2016 SQL 데이터베이스를 사용 하 여 업그레이드](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL.md)
- Windows Server 2012 ADFS Windows Server 2012 r 2 ADFS
    - [Windows Server 2012 r 2 ADFS 마이그레이션을](https://technet.microsoft.com/library/dn486815.aspx)
- Windows Server 2012 광고 FS에 ADFS 2.0
    - [Windows Server 2012에서 ADFS 마이그레이션을](https://technet.microsoft.com/library/jj647765.aspx)
- ADFS ADFS 2.0에 1.x 
    - [Adfs의 업그레이드를 ADFS 2.0 1.x](https://technet.microsoft.com/library/ff678035.aspx)

ADFS 2.0 또는 2.1 (Windows Server 2008 R2 또는 Windows Server 2012)에서 업그레이드 하는 데 필요한 경우 기본 스크립트 (C:\Windows\ADFS 위치)를 사용 해야 합니다.

### <a name="why-does-ad-fs-installation-require-a-reboot-of-the-server"></a>ADFS 설치 서버를 다시 부팅을 요구 하는 이유

Windows Server 2016 HTTP/2 지원이 추가 되었습니다 하지만 HTTP/2 클라이언트 인증서를 인증에 사용할 수 없습니다.  클라이언트 인증서의 사용 및 상당수 클라이언트의 시도 지원 하지 많은 ADFS 시나리오를 개선 하기 때문에 요청/1.1, ADFS 농장 구성 구성 다시 사용 하 여/1.1 로컬 서버가 HTTP 설정 합니다.  서버를 다시 부팅을 해야 합니다.  

### <a name="is-using-windows-2016-wap-servers-to-publish-the-ad-fs-farm-to-the-internet-without-upgrading-the-back-end-ad-fs-farm-supported"></a>지원 백 엔드 ADFS 농장 업그레이드 하지 않고 인터넷에 ADFS 농장 게시할 Windows 2016 WAP 서버를 사용 하는?
그러나 예,이 구성이 지원 새 FS 2016 AD 기능이이 구성에서 지원 되는.  이 구성 FS 2016 ad AD FS 2012 r 2의에서 마이그레이션 단계 임시 알 수 있도록 및 오랜 시간 동안 배포할 수 없습니다.

## <a name="design"></a>디자인

### <a name="what-third-party-multi-factor-authentication-providers-are-available-for-ad-fs"></a>제 3 자 무엇입니까 다단계 인증 공급자 adfs 사용할 수 있습니까? 
다음은의 알고 제 3 자 프로바이더의 목록입니다.  사용 가능한에 대해 알 수 없어도 하 고 목록에 대 한 학습으로 업데이트할 것 공급자 항상 있을 수 있습니다.

- [Gemalto Id 및 보안 서비스](http://www.gemalto.com/identity)
- [inWebo 인증 엔터프라이즈 서비스](http://www.inwebo.com/)
- [로그인 피플 MFA API 커넥터](https://www.loginpeople.com)
- [Microsoft의 Active Directory Federation Services RSA SecurID 인증 에이전트](http://www.emc.com/security/rsa-securid/rsa-authentication-agents/microsoft-ad-fs.htm)
- [Adfs SafeNet 인증 서비스 (SAS) 에이전트](http://www.safenet-inc.com/resources/integration-guide/data-protection/Safenet_Authentication_Service/SafeNet_Authentication_Service__AD_FS_Agent_Configuration_Guide/?langtype=1033)
- [Swisscom 모바일 ID 인증 서비스](http://swisscom.ch/mid)
- [ID 보호 서비스 (VIP)를 Symantec 유효성 검사](http://www.symantec.com/vip-authentication-service) 

### <a name="are-third-party-proxies-supported-with-ad-fs"></a>제 3 자 프록시 Adfs로 지원 되나요?
예, 제 3 자 프록시 웹 응용 프로그램 프록시 앞 배치할 수 있지만 모든 제 3 자 프록시 지원 해야는 [MS ADFSPIP 프로토콜](https://msdn.microsoft.com/library/dn392811.aspx) 웹 응용 프로그램 프록시 대신 사용할 수 있습니다.

### <a name="what-third-party-proxies-are-available-for-ad-fs-that-support-ms-adfspip"></a>어떤 제 3 자 프록시 MS ADFSPIP 지원 adfs 사용할 수 있습니까?

다음은의 알고 제 3 자 프로바이더의 목록입니다.  사용 가능한에 대해 알 수 없어도 하 고 목록에 대 한 학습으로 업데이트할 것 공급자 항상 있을 수 있습니다.

- [F5 액세스 정책 관리자](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-third-party-integration-13-1-0/12.html#guid-1ee8fbb3-1b33-4982-8bb3-05ae6868d9ee)

### <a name="where-is-the-capacity-planning-sizing-spreadsheet-for-ad-fs-2016"></a>용량은 어디 AD FS 2016에 대 한 크기 조정 스프레드시트 계획는?
스프레드시트 FS 2016 AD 버전을 다운로드할 수 있습니다 [여기](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx)합니다.
이 Windows Server 2012 r 2에서 adfs도 사용할 수 있습니다.

### <a name="how-can-i-ensure-my-ad-fs-and-wap-servers-support-apples-atp-requirements"></a>확인 하는 방법 내 Adfs와 WAP 서버 지원 Apple의 ATP 요구 사항이 있나요?

Apple에서는 앱 Transport Security (ATS) ADFS 인증 iOS 앱에서 호출 영향을 미칠 수 있는 라고 요구 사항 릴리스 했습니다.  사용자 ADFS 되도록 할 수과 WAP 서버 지원 하 않도록 하 여는 [ATS를 사용 하 여 연결에 대 한 요구](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57)합니다.  
특히, ADFS 및 WAP 서버 TLS 1.2를 지원 하 고 TLS 연결 하기로 암호화 제품군에서 전달 완전을 지원 하는지 확인 해야 합니다.

및 1.0 민 1.1, 1.2 SSL 2.0 3.0 및 TLS 버전을 사용 하지 않도록 설정할 수 있습니다 사용 하 여 [adfs에서 SSL 프로토콜 관리](../operations/Manage-SSL-Protocols-in-AD-FS.md)합니다.

ADFS 및 WAP 되도록 서버 협상할 ATP 지만 TLS 암호 그룹에 있는 모든 암호 그룹 사용 하지 않도록 설정할 수 있는 [ATP 호환 암호 그룹 목록이](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57)합니다.  이 위해 사용 하 여 [Windows TLS PowerShell cmdlet](https://technet.microsoft.com/itpro/powershell/windows/tls/index)합니다. 


## <a name="operations"></a>작업

### <a name="how-do-i-replace-the-ssl-certificate-for-ad-fs"></a>Adfs SSL 인증서를 교체 하려면 어떻게 합니까? 
광고 FS SSL 인증서가 FS 관리 AD 스냅인에서 찾을 수 있는 ADFS 서비스 통신 인증서와 동일 합니다.  AD FS SSL 인증서를 변경 하려면 PowerShell 사용 해야 합니다. 다음 문서에 대 한 지침을 따르세요.

[ADFS 및 WAP 2016 SSL 인증서 관리](../operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)

### <a name="how-can-i-enable-or-disable-tlsssl-settings-for-ad-fs"></a>활성화 또는 비활성화할 adfs TLS/SSL 설정을 수 어떻게 하나요
사용 하지 않도록 설정 하거나 SSL 프로토콜을 사용 하 고 암호화 된 도구 모음이, 하려면 다음을 사용 합니다.

[Adfs의 SSL 프로토콜 관리](../operations/Manage-SSL-Protocols-in-AD-FS.md)

### <a name="does-the-proxy-ssl-certificate-have-to-be-the-same-as-the-ad-fs-ssl-certificate"></a>프록시 SSL 인증서 AD FS SSL 인증서 같을 수 있습니까?  
프록시 SSL 인증서 및 AD FS SSL 인증서 다음 지침을 사용 하 여 다음과 같습니다.


- 프록시 하는 데 사용 되는 경우 Windows 통합 인증을 프록시 SSL 인증서를 사용 하는 프록시 ADFS 요청 동일 해야 (같은 키를 사용 하 여) federation 서버 SSL 인증서로
- 프록시 SSL 인증서 (같은 키를 사용 하 여)와 동일 federation 서버 SSL 인증서 해야 ADFS 속성 "ExtendedProtectionTokenCheck" (기본 adfs에서 설정)를 사용 하도록 설정 하는 경우
- 그렇지 않은 경우 프록시 SSL 인증서 수 AD FS SSL 인증서에서 다른 키 없지만 만족 해야 동일한 [요구 사항](../overview/AD-FS-2016-Requirements.md)

### <a name="how-can-i-configure-promptlogin-behavior-for-ad-fs"></a>프롬프트 구성 어떻게 = Adfs에 대해 로그인 동작 있나요?
로그인, = 프롬프트를 구성 하는 방법에 대 한 정보를 참조 [Active Directory Federation Services 프롬프트 로그인 매개 지원 =](../operations/AD-FS-Prompt-Login.md)합니다.

### <a name="how-can-i-configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>ADFS 통합 인증 (WIA Windows)를 사용 하는 브라우저 구성 하려면 어떻게 해야 하나요

브라우저를 구성 하는 방법에 대 한 내용은 [브라우저 Adfs와 통합 된 인증 (WIA Windows)를 사용 하도록 구성](../operations/Configure-AD-FS-Browser-WIA.md)합니다.


### <a name="how-long-are-ad-fs-tokens-valid"></a>ADFS 토큰 유효한는 얼마나 되나요?

이 질문 '얼마나 오래 수행 사용자가 단일 로그인 (sso)를 않고도 가져올 새 자격 증명을 입력 하며 컨트롤 하는 방법 프로그램 관리자는?'을 의미 하는 자주  이 동작을 및 구성 설정을 제어 하는 문서에서 설명한 [여기](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/operations/ad-fs-2016-single-sign-on-settings)합니다.

다양 한 쿠키 및 토큰 기본 수명 (뿐만 아니라 수명을 제어 하는 매개) 다음과 같습니다.

**등록 된 디바이스**

- 쿠키 PRT 및 SSO: 90 일 최대, PSSOLifeTimeMins 주기가 적용 됩니다. (제공된 장치를 사용 14 일 마다 이상 DeviceUsageWindow 하 여 제어)

- 토큰 새로 고침: 일관 되 게 동작을 제공 하려면 위의 유형에 따라 계산

- access_token: 1 시간 기본적으로 당사자에 따라

- id_token: 액세스 토큰 동일

**취소 등록 된 디바이스**

- 쿠키 SSO: 기본적으로 8 시간 SSOLifetimeMins 주기가 적용 됩니다.  계속 로그인 (KMSI)를 사용 하도록 설정 하는 경우 기본은 24 시간 및 KMSILifetimeMins 되었습니다.


- 토큰 새로 고침: 기본적으로 8 시간 합니다. KMSI 사용 하 여 24 시간

- access_token: 1 시간 기본적으로 당사자에 따라

- id_token: 액세스 토큰 동일

### <a name="does-ad-fs-support-http-strict-transport-security-hsts"></a>Adfs는 HTTP Strict Transport Security (HSTS)를 지원 되나요?  

HTTP Strict Transport Security (HSTS)은 웹 보안 정책 메커니즘 프로토콜 다운 그레이드 공격 및 쿠키 가로채기 HTTP 및 HTTPS 끝점 있는 서비스에 대 한을 완화 하는 데 도움이 됩니다. 웹 서버를를 웹 브라우저 (또는 다른 유효한 사용자 에이전트) 해야만 상호 작용 HTTPS를 사용 하 여 HTTP 프로토콜을 통해 절대 선언 수 있습니다.

인증 교통 웹에 대 한 모든 ADFS 끝점 HTTPS를 통해 단독으로 열립니다.  효과적으로 ADFS HTTP Strict Transport Security 정책 장치를 제공 하는 위험을 완화 결과적으로, (으로 설계가 없는 다운 그레이드 HTTP HTTP 수신기가 이후). 또한 ADFS 쿠키를 플래그 보안을 사용 하 여 모든 쿠키를 표시 하 여 다른 HTTP 프로토콜 끝점 서버에 전송 되지 않습니다.

따라서 ADFS 서버의 HSTS 구현 필요 하지 않은 다운 그레이드 절대 수 있습니다.  준수 목적을 위해 ADFS 서버가 HTTP 절대 사용할 수 있는 모든 쿠키 안전 하 게 표시 하기 때문에이 요구 사항을 충족입니다.

### <a name="x-ms-forwarded-client-ip-does-not-contain-the-ip-of-the-client-but-contains-ip-of-the-firewall-in-front-of-the-proxy-where-can-i-get-the-right-ip-of-the-client"></a>X ms-전달-클라이언트-ip 클라이언트 IP 포함 되어 있지 않습니다 있지만 프록시 앞 방화벽 IP 있습니다. 클라이언트의 오른쪽 IP 가져오기
하지 WAP 하기 전에 SSL 종료를 수행 하는 것이 좋습니다. SSL 해지는 WAP 앞 완료 되는 경우를 대비 X-ms-전달-클라이언트-ip WAP 앞 네트워크 디바이스의 IP 포함 됩니다. 다음은 다양 한 IP 한 간략 한 설명을 관련 된 청구 Adfs에서 지원 되는입니다.
 - Ms 클라이언트 ip x: 네트워크 STS에 연결 하는 디바이스의 IP 합니다.  항상 익스트라넷 요청 대해서는 WAP IP 포함합니다.
 - X ms-전달-클라이언트-ip: 다중 값된 클레임 Exchange Online 이용는 WAP에 연결 하는 디바이스의 IP 주소 ADFS를 전달 값 포함 됩니다.
 - Userip: 익스트라넷 요청에 대 한이 클레임은 포함 x ms-전달-클라이언트-ip 값 합니다.  인트라넷 요청에 대 한이 클레임 같은 ms 클라이언트 ip x 값을 포함 됩니다.

### <a name="i-am-trying-to-get-additional-claims-on-the-user-info-endpoint-but-its-only-returning-subject-how-can-i-get-additional-claims"></a>사용자 정보 끝점 추가 클레임 다운로드 하려고 했지만 주제를 반환 하는 합니다. 자세한 청구를 다운로드 하려면 어떻게 해야 하나요?
항상 ADFS 사용자 정보 끝점 OpenID 표준을에 지정 된 대로 제목 클레임을 반환합니다. ADFS 추가 클레임 사용자 정보 끝점 통해 요청을 제공 하지 않습니다. 자세한 청구 ID 토큰에 필요한 경우를 참조 [Adfs의 사용자 지정 ID 토큰](../development/custom-id-tokens-in-ad-fs.md)합니다.

### <a name="why-do-i-see-alot-of-1021-errors-on-my-ad-fs-servers"></a>Why do I see alot of 1021 errors on my AD FS servers?
This event is logged usually for an invalid resource access on AD FS for resource 00000003-0000-0000-c000-000000000000. This error is caused by an erroneous behavior of the client where it tries to get an access token for the Azure AD Graph service. Since the resource is not present on AD FS, this results in event ID 1021 on the AD FS servers. It’s safe to ignore any warnings or errors for resource 00000003-0000-0000-c000-000000000000 on AD FS. 

### <a name="why-am-i-seeing-a-warning-for-failure-to-add-the-ad-fs-service-account-to-the-enterprise-key-admins-group"></a>Why am I seeing a warning for failure to add the AD FS service account to the Enterprise Key Admins group?
This group is only created when a Windows 2016 Domain Controller with the FSMO PDC role exists in the Domain. To resolve the error, you can create the Group manually and follow the below to give the required permission after adding the service account as member of the group.
1.  Open **Active Directory Users and Computers**. 
2.  **Right-click** your domain name from the navigation pane and **click** Properties.
3.  **Click** Security (if the Security tab is missing, turn on Advanced Features from the View menu).
4.  **Click** Advanced. **Click** Add. **Click** Select a principal.
5.  The Select User, Computer, Service Account, or Group dialog box appears.  In the Enter the object name to select text box, type Key Admin Group.  확인을 클릭 합니다.
6.  In the Applies to list box, select **Descendant User objects**.
7.  Using the scroll bar, scroll to the bottom of the page and **click** Clear all.
8.  In the **Properties** section, select **Read msDS-KeyCredentialLink** and **Write msDS-KeyCrendentialLink**.

### <a name="why-does-modern-authentication-from-android-devices-fail-if-the-server-does-not-send-all-the-intermediate-certificates-in-the-chain-with-the-ssl-cert"></a>Why does modern authentication from Android devices fail if the server does not send all the intermediate certificates in the chain with the SSL cert?

Federated users may experience authentication to Azure AD for apps that use the Android ADAL library failing. The app will get an **AuthenticationException** when it tries to show the login page. In chrome the AD FS login page might be called out as unsafe.

Android - across all versions and all devices - does not support downloading additional certificates from the **authorityInformationAccess** field of the certificate. This is true of the Chrome browser as well. Any Server Authentication certificate that’s missing intermediate certificates will result in this error if the entire certificate chain is not passed from AD FS. 

A proper solution to this problem is to configure the AD FS and WAP servers to send the necessary intermediate certificates along with the SSL certificate. 

When exporting the SSL certificate, from one machine, to be imported to the computer’s personal store, of the AD FS and WAP server(s), make sure to export the Private key and select **Personal Information Exchange - PKCS #12**. 

It is important that the check box to **Include all certificates in the certificate path if possible** is checked, as well as **Export all extended properties**. 

Run certlm.msc on the Windows servers and import the *.PFX into the Computer’s Personal Certificate store. This will cause the server to pass the entire certificate chain to the ADAL library. 

>[!NOTE]
> The certificate store of Network Load Balancers should also be updated to include the entire certificate chain if present

### <a name="does-ad-fs-support-head-requests"></a>Does AD FS support HEAD requests?
AD FS does not support HEAD requests.  Applications should not be using HEAD requests against AD FS endpoints.  This may cause HTTP error responses that are unexpected and/or delayed.  Additionally, you may see unexpected error events in the AD FS event log.

### <a name="why-am-i-not-seeing-a-refresh-token-when-i-am-logging-in-with-a-remote-idp"></a>하지 표시 되는 이유를 새로 고침 토큰 I @ 원격 IdP 로그인 할 때 있나요?
새로 고침 토큰 되지 IdP에서 발급 한 토큰에 1 시간 미만의 validty 경우 발생 합니다. 새로 고침 토큰 실행 되도록 토큰 1 시간 이상 하 고 IdP에서 발급 한의 유효성을 늘립니다.
