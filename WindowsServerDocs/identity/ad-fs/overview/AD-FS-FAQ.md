---
ms.assetid: acc9101b-841c-4540-8b3c-62a53869ef7a
title: AD FS 2016 FAQ
description: AD FS 2016에 대 한 질문과 대답
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 04/17/2019
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f3f84a5c18589d38606825ee064cfb729003a05d
ms.sourcegitcommit: a3958dba4c2318eaf2e89c7532e36c78b1a76644
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719688"
---
# <a name="ad-fs-frequently-asked-questions-faq"></a>AD FS에는 질문과 대답 (FAQ)


다음 문서는 Active Directory Federation Services와 관련 하 여 자주 묻는 질문에 대 한 홈입니다.  문서 질문의 유형에 따라 그룹으로 분할 되었습니다.

## <a name="deployment"></a>배포

### <a name="how-can-i-upgrademigrate-from-previous-versions-of-ad-fs"></a>어떻게 마이그레이션할 수 있습니까 업그레이드/AD FS의 이전 버전에서
다음 중 하나를 사용 하 여 AD FS를 업그레이드할 수 있습니다.


- Windows Server 2016 AD FS Windows Server 2012 R2 AD FS
    - [WID 데이터베이스를 사용하여 Windows Server 2016에서 AD FS로 업그레이드](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)
    - [SQL 데이터베이스를 사용하여 Windows Server 2016에서 AD FS로 업그레이드](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL.md)
- Windows Server 2012 R2 AD FS Windows Server 2012 AD FS
    - [Windows Server 2012 R2에서 AD FS로 마이그레이션](https://technet.microsoft.com/library/dn486815.aspx)
- Windows Server 2012 AD FS AD FS 2.0
    - [Windows Server 2012에서 AD FS로 마이그레이션](https://technet.microsoft.com/library/jj647765.aspx)
- AD FS 1.x to AD FS 2.0
    - [AD FS에서 업그레이드 AD fs 2.0 1.x](https://technet.microsoft.com/library/ff678035.aspx)

AD FS 2.0 또는 2.1 (Windows Server 2008 R2 또는 Windows Server 2012)에서 업그레이드 하는 경우 (C:\Windows\ADFS에 있음) 상자에서 스크립트를 사용 해야 합니다.

### <a name="why-does-ad-fs-installation-require-a-reboot-of-the-server"></a>AD FS 설치 서버를 다시 부팅을 왜 필요 합니까?

Windows Server 2016에서 http/2 지원이 추가 되었습니다 하지만 HTTP/2 클라이언트 인증서 인증에 사용할 수 없습니다.  여러 AD FS 시나리오 만들지 클라이언트 인증서 인증을 사용 및 많은 수의 클라이언트 다시 시도 지원 하지 않으므로 요청 HTTP/1.1, AD FS 팜 구성 구성 다시 사용 하 여 HTTP/1.1 로컬 서버의 HTTP 설정 합니다.  이 서버를 재부팅을 해야합니다.  

### <a name="is-using-windows-2016-wap-servers-to-publish-the-ad-fs-farm-to-the-internet-without-upgrading-the-back-end-ad-fs-farm-supported"></a>지원 되는 백 엔드 AD FS 팜을 업그레이드 하지 않고 인터넷에 AD FS 팜에 게시 하는 데 Windows 2016 WAP 서버를 사용 하는?
예,이 구성은 지원, 되지만 새 AD FS 2016 기능이 없습니다는이 구성에서 지원 됩니다.  이 AD FS 2012 r 2에서에서 AD FS 2016에는 마이그레이션 단계에 있는 임시 알 수 있도록 구성과 오랜 시간 동안 배포 해서는 안 됩니다.

### <a name="is-it-possible-to-deploy-ad-fs-for-office-365-without-publishing-a-proxy-to-office-365"></a>Office 365에 프록시를 게시 하지 않고 Office 365에 대 한 AD FS를 배포할 수는?
예,이 지원 됩니다. 그러나 부작용으로

1. 수동으로 토큰 서명 인증서를 Azure AD 페더레이션 메타 데이터에 액세스할 수 없기 때문에 업데이트를 관리 해야 합니다. 수동으로 토큰 서명 인증서를 업데이트 하는 방법은 읽기 [Office 365 및 Azure Active Directory에 대 한 페더레이션 인증서 갱신](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-o365-certs)
2. 레거시 인증 흐름 (예:: ExO 프록시 인증 흐름)을 활용할 수 없습니다.

### <a name="what-are-load-balancing-requirements-for-ad-fs-and-wap-servers"></a>AD FS 및 WAP 서버에 대 한 부하 분산 요구 사항은 무엇입니까?

AD FS는 상태 비저장 시스템. 따라서 부하 분산은 로그인에 대 한 매우 간단 합니다. 부하 분산 시스템에 대 한 주요 권장 사항은 다음과 같습니다.


- IP 선호도 사용 하 여 부하 분산 장치를 구성 되어야 합니다. 특정 Exchange Online 시나리오에서는 서버의 하위 집합에 과도 한 부하를 배치할 수이 있습니다.
- 하지 부하 분산 장치는 HTTPS 연결을 종료 하 고 ADFS 서버에 새 연결을 다시 시작 해야 합니다.
- 부하 분산 장치는 연결 IP 주소가 ADFS에 전송 될 때 HTTP 패킷의 원본 IP로 변환 해야 확인 해야 합니다. 부하 분산 장치는 HTTP 패킷의 원본 IP를 보낼 수 없습니다, 하는 경우에 부하 분산 장치 해야 추가 (또는 기존 경우 추가) IP 주소 x-전달 기능에 대 한 헤더를 합니다. 이것이 필요한 특정 IP의 올바른 처리 관련 기능 (IP 차단, 엑스트라넷 잠금,...) 및 잘못 구성 된 경우 보안이 약화 될 수 있습니다.
- 부하 분산 장치는 SNI를 지원 해야 합니다. 하지 않는 이벤트, 비 SNI 수 있는 클라이언트를 처리 하는 HTTPS 바인딩을 만드는 AD FS가 구성 되었는지 확인 합니다.
- 부하 분산 장치를 감지 하 AD FS 또는 WAP 서버 시작 되어 실행 되 고 200 확인을 받지 못할 경우를 제외 하는 경우 AD FS HTTP 상태 프로브 끝점을 사용 해야 합니다.

### <a name="what-multi-forest-configurations-are-supported-by-ad-fs"></a>다중 포리스트 구성 AD FS에서 지원 되나요?

AD FS 여러 다중 포리스트 구성을 지원 하며 여러 신뢰할 수 있는 영역 간 사용자 인증을 기본 AD DS 신뢰 네트워크입니다. 좋습니다 양방향 포리스트 트러스트를 이것은 신뢰 하위 시스템 문제 없이 올바르게 작동 하는지 확인 하려면 더 간편한 설치. 또한

- 파트너 id를 포함 하는 DMZ 포리스트 같은 단방향 포리스트 트러스트의 경우 corp 포리스트의에서 ADFS 배포 및 LDAP를 통해 연결 하는 다른 로컬 클레임 공급자 트러스트로 DMZ 포리스트를 처리 하는 것이 좋습니다. 이 경우 Windows 통합 인증 DMZ 포리스트 사용자에 대해 작동 하지 않습니다 및 LDAP에 대 한 지원 되는 유일한 메커니즘 이므로 암호 인증을 수행 해야 합니다. 이 옵션을 선택할 수 없습니다. 이벤트를 다른 ADFS DMZ 포리스트에 corp 포리스트의 ADFS에서 클레임 공급자 트러스트를 추가 해야 합니다. 사용자 영역 검색 홈 수행 해야 합니다. 하지만 Windows 통합 인증 및 암호 인증을 모두 작동 합니다. Corp 포리스트의 ADFS DMZ 포리스트에서 사용자에 대 한 추가 사용자 정보를 가져올 수 없으므로 DMZ 포리스트에 ADFS에서 발급 규칙에 적절 한 변경 내용의 확인 하세요.
- 도메인 수준 트러스트 지을 사용할 수 있지만 좋습니다 포리스트 수준 신뢰 모델로 전환 합니다. 또한 UPN 라우팅 및 이름의 NETBIOS 이름 확인 해야 한다는 정확 하 게 작동 되도록 해야 합니다.



## <a name="design"></a>디자인

### <a name="what-third-party-multi-factor-authentication-providers-are-available-for-ad-fs"></a>AD FS에 대 한 사용할 수 있는 어떤 제 3 자 다단계 인증 공급자?
다음은 알고 타사 공급자의 목록입니다.  에 대 한 파악 하지 못해도 자세히 알아보면 목록 업데이트는 사용할 수 있는 공급자는 항상 있을 수 있습니다.

- [Gemalto Id 및 보안 서비스](http://www.gemalto.com/identity)
- [inWebo Enterprise Authentication 서비스](http://www.inwebo.com/)
- [Login People MFA API 커넥터](https://www.loginpeople.com)
- [Microsoft Active Directory Federation Services 용 RSA SecurID Authentication Agent](http://www.emc.com/security/rsa-securid/rsa-authentication-agents/microsoft-ad-fs.htm)
- [AD FS에 대 한 SafeNet Authentication Service (SAS) 에이전트](http://www.safenet-inc.com/resources/integration-guide/data-protection/Safenet_Authentication_Service/SafeNet_Authentication_Service__AD_FS_Agent_Configuration_Guide/?langtype=1033)
- [Swisscom 모바일 ID 인증 서비스](http://swisscom.ch/mid)
- [Symantec 유효성 검사 and ID Protection Service (VIP)](http://www.symantec.com/vip-authentication-service)

### <a name="are-third-party-proxies-supported-with-ad-fs"></a>AD FS를 사용 하 여 제 3 자 프록시 지원 되나요?
예, 제 3 자 프록시 웹 응용 프로그램 프록시를 앞에 배치할 수 있지만 모든 제 3 자 프록시를 지원 해야 합니다는 [MS ADFSPIP 프로토콜](https://msdn.microsoft.com/library/dn392811.aspx) 웹 응용 프로그램 프록시를 대신 사용할 수 있습니다.

### <a name="what-third-party-proxies-are-available-for-ad-fs-that-support-ms-adfspip"></a>어떤 제 3 자 프록시 MS ADFSPIP 지 AD FS에 대해 사용할 수 있습니까?

다음은 알고 타사 공급자의 목록입니다.  에 대 한 파악 하지 못해도 자세히 알아보면 목록 업데이트는 사용할 수 있는 공급자는 항상 있을 수 있습니다.

- [F5 Access Policy Manager](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-third-party-integration-13-1-0/12.html#guid-1ee8fbb3-1b33-4982-8bb3-05ae6868d9ee)

### <a name="where-is-the-capacity-planning-sizing-spreadsheet-for-ad-fs-2016"></a>여기서는 용량 계획 규모 산정 스프레드시트 AD FS 2016에 대 한?
스프레드시트의 AD FS 2016 버전을 다운로드할 수 있습니다 [여기](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx)합니다.
이 Windows Server 2012 R2에서 AD FS에 대 한 사용 될 수도 있습니다.

### <a name="how-can-i-ensure-my-ad-fs-and-wap-servers-support-apples-atp-requirements"></a>되도록 하려면 어떻게 해야 내 AD FS 및 WAP 서버 지원 Apple ATP 요구 사항?

Apple에 앱 전송 보안 ATS () 호출에서 AD FS에 인증 하는 iOS 앱에 영향을 줄 수 있는 호출 하는 요구 사항 집합을 출시 했습니다.  AD FS를 확인할 수 있습니다 및 WAP 서버 지 확인 하 여 준수 합니다 [ATS를 사용 하 여 연결에 대 한 요구 사항](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57)합니다.  
특히 AD FS 및 WAP 서버는 TLS 1.2를 지원 하 고 TLS 연결을 협상 된 암호화 suite에서 전달 완전 보안을 지원 하는지 확인 해야 합니다.

및 SSL 2.0, 3.0 및 TLS 버전 1.0, 1.1 및 1.2를 사용 하지 않도록 설정할 수 있습니다 사용 하 여 [AD FS에서 SSL 프로토콜 관리](../operations/Manage-SSL-Protocols-in-AD-FS.md)합니다.

에 AD FS 및 WAP 되도록 ATP 지만 TLS 암호 도구 모음을 협상 하는 서버에 없는 모든 암호 그룹이 사용 하지 않도록 설정 합니다 [ATP 준수 암호화 그룹 목록은](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57)합니다.  이 작업을 수행 하려면 사용 합니다 [Windows TLS PowerShell cmdlet](https://technet.microsoft.com/itpro/powershell/windows/tls/index)합니다.

## <a name="developer"></a>Developer

### <a name="when-generating-an-idtoken-with-adfs-for-a-user-authenticated-against-ad-how-is-the-sub-claim-generated-in-the-idtoken"></a>AD에 대해 인증 된 사용자에 대 한 ADFS 사용 하 여 id_token을 생성 하는 경우 생성 되는 방식을 "sub" 클레임 id_token에서?
"Sub" 클레임의 값은 클라이언트 ID의 해시 + 앵커 클레임 값입니다.

### <a name="what-is-the-lifetime-of-the-refresh-tokenaccess-token-when-the-user-logs-in-via-a-remote-claims-provider-trust-over-ws-fedsaml-p"></a>사용자가 로그인 할 때 원격 클레임 공급자 트러스트를 통한 WS-Fed/Saml-p를 통해 새로 고침 토큰/액세스 토큰의 수명을 란?
새로 고침 토큰의 수명을 ADFS 원격 클레임 공급자 트러스트에서 가져온 토큰의 수명이 됩니다. 액세스 토큰의 수명을 액세스 토큰이 발급 되는 신뢰 당사자의 토큰 수명이 됩니다.

### <a name="i-need-to-return-profile-and-email-scopes-as-well-in-addition-to-the-openid-scope-can-i-obtain-additional-information-using-scopes-how-to-do-it-in-ad-fs"></a>OpenId 범위가 외에 프로필 및 전자 메일 범위를 반환 해야 합니다. 범위를 사용 하 여 추가 정보를 얻을 수 있습니까? AD FS에서 작업을 수행 하는 방법
자체 id_token에 있는 관련 정보를 추가 하려면 사용자 지정 된 id_token을 사용할 수 있습니다. 자세한 내용은 문서 참조 [id_token에 내보내지는 클레임을 사용자 지정](../development/Custom-Id-Tokens-in-AD-FS.md)합니다.

### <a name="how-to-issue-json-blobs-inside-jwt-tokens"></a>JWT 토큰 내에서 json blob을 실행 하는 방법
특수 값 형식 ("<http://www.w3.org/2001/XMLSchema#json>") 및 AD FS 2016에서에서 추가 된이 character(\x22)를 이스케이프 합니다. 발급 규칙 및 액세스 토큰의 최종 출력에 대 한 아래 샘플 하세요.

샘플 발급 규칙:

    => issue(Type = "array_in_json", ValueType = "http://www.w3.org/2001/XMLSchema#json", Value = "{\x22Items\x22:[{\x22Name\x22:\x22Apple\x22,\x22Price\x22:12.3},{\x22Name\x22:\x22Grape\x22,\x22Price\x22:3.21}],\x22Date\x22:\x2221/11/2010\x22}");

액세스 토큰에서 발급 된 클레임:

    "array_in_json":{"Items":[{"Name":"Apple","Price":12.3},{"Name":"Grape","Price":3.21}],"Date":"21/11/2010"}

### <a name="can-i-pass-resource-value-as-part-of-the-scope-value-like-how-requests-are-done-against-azure-ad"></a>Azure AD에 대해 요청은 완료 하는 방법 같은 범위 값의 일부로 리소스 값을 전달할 수 있나요?
서버 2019에 AD FS를 사용 하 여 이제 범위 매개 변수에 포함 된 리소스 값을 전달할 수 있습니다. 범위 매개 변수에 있는 각 항목은 리소스/범위 구조를 공백으로 구분 된 목록으로 이제 구성할 수 있습니다. 예를 들면 다음과 같습니다.  
**< 잘못 샘플 요청 만들기 >**

### <a name="does-ad-fs-support-pkce-extension"></a>AD FS PKCE 확장을 지원 하나요?
AD FS 서버 2019에는 지원 Proof Key 코드 Exchange (PKCE)에 대 한 OAuth 인증 코드 부여 흐름에 대 한

### <a name="what-permitted-scopes-are-supported-by-ad-fs"></a>AD FS는 허용 된 범위를 지원 하나요?
- aza-사용 하는 경우 [Broker 클라이언트에 대 한 OAuth 2.0 프로토콜 확장](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-oapxbc/2f7d8875-0383-4058-956d-2fb216b44706) 서버 범위 매개 변수 "aza" 범위에 있으면 새 기본 새로 고침 토큰을 발급 하 고 설정 뿐만 아니라 응답 refresh_token 필드에 설정 없으면 새 기본 새로 고침 토큰의 수명과 refresh_token_expires_in 필드 적용 됩니다.
- openid-응용 프로그램의 OpenID Connect 인증 프로토콜을 사용 하 여 요청을 허용 합니다.
- logon_cert-logon_cert 범위를 통해 응용 프로그램을 대화형으로 인증 된 사용자를 로그온에 사용할 수 있는 로그온 인증서를 요청 합니다. AD FS 서버는 응답의 access_token 매개 변수를 생략 하 고 대신 base64로 인코딩된 CMS 인증서 체인 또는 CMC 전체 PKI 응답을 제공 합니다. 자세한 내용은 사용 가능한 [여기](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-oapx/32ce8878-7d33-4c02-818b-6c9164cc731e)합니다. 
- user_impersonation-user_impersonation 범위가 성공적으로 AD FS에서-대신-의 액세스 토큰을 요청 하는 데 필요한입니다. 이 범위를 사용 하는 방법에 대 한 세부 정보 참조 [On-Behalf-Of (OBO) OAuth를 사용 하 여 ad FS 2016을 사용 하 여 다중 계층 응용 프로그램 빌드](../../ad-fs/development/ad-fs-on-behalf-of-authentication-in-windows-server.md)합니다.
- vpn_cert-vpn_cert 범위 EAP-TLS 인증을 사용 하 여 VPN 연결을 사용할 수 있는 VPN 인증서를 요청 하는 응용 프로그램을 허용 합니다. 이 더 이상 지원 되지 않습니다.
- 전자 메일-응용 프로그램이 로그인된 한 사용자에 대 한 전자 메일 클레임을 요청할 수 있게 합니다. 이 더 이상 지원 되지 않습니다. 
- 프로 파일링-응용 프로그램 프로필 요청을 사용 하면 로그인 한 사용자에 대 한 클레임 관련 합니다. 이 더 이상 지원 되지 않습니다. 


## <a name="operations"></a>작업

### <a name="how-do-i-replace-the-ssl-certificate-for-ad-fs"></a>AD FS에 대 한 SSL 인증서를 교체 하려면 어떻게 합니까?
AD FS SSL 인증서는 AD FS 관리 스냅인에 AD FS 서비스 통신 인증서로 같지는 않습니다.  AD FS SSL 인증서를 변경 하려면 PowerShell을 사용 해야 합니다. 아래 문서에서 제공 된 지침을 따르세요.

[AD FS 및 WAP 2016의 SSL 인증서 관리](../operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)

### <a name="how-can-i-enable-or-disable-tlsssl-settings-for-ad-fs"></a>어떻게 사용 하도록 설정 하거나 수 AD FS에 대 한 TLS/SSL 설정 사용 안 함
사용 하지 않도록 설정 또는 SSL 프로토콜을 사용 하도록 설정 하 고 암호 그룹에 다음을 사용 합니다.

[AD FS에서 SSL 프로토콜 관리](../operations/Manage-SSL-Protocols-in-AD-FS.md)

### <a name="does-the-proxy-ssl-certificate-have-to-be-the-same-as-the-ad-fs-ssl-certificate"></a>프록시 SSL 인증서는 AD FS SSL 인증서와 동일 해야 합니까?  
프록시 SSL 인증서 및 AD FS SSL 인증서와 관련 하 여 다음 지침을 따르세요.


- 프록시를 사용 하는 경우 Windows 통합 인증을 프록시 SSL 인증서를 사용 하는 AD FS 프록시 요청 동일 해야 (동일한 키를 사용 하 여) 페더레이션 서버 SSL 인증서로
- "ExtendedProtectionTokenCheck"는 AD FS 속성 설정 (기본 AD FS에서 설정), 프록시 SSL 인증서 동일 해야 (동일한 키를 사용 하 여) 페더레이션 서버 SSL 인증서로
- 프록시 SSL 인증서는 AD FS SSL 인증서에서 다른 키를 가질 수 있습니다 없지만 동일한 만족 해야이 고, 그렇지 [요구 사항](../overview/AD-FS-2016-Requirements.md)

### <a name="how-can-i-configure-promptlogin-behavior-for-ad-fs"></a>프롬프트를 구성할 수는 어떻게 AD FS에 대 한 로그인 동작 =?
= 로그인 프롬프트를 구성 하는 방법에 대 한 정보에 대 한 참조 [Active Directory Federation Services 프롬프트 로그인 매개 변수 지원 =](../operations/AD-FS-Prompt-Login.md)합니다.

### <a name="how-can-i-change-the-ad-fs-service-account"></a>AD FS 서비스 계정을 어떻게 변경할 수 있나요?
AD FS 서비스 계정을 변경 하려면 AD FS 도구 상자를 사용 하 여 지침을 따릅니다 [서비스 계정 Powershell 모듈](https://github.com/Microsoft/adfsToolbox/tree/master/serviceAccountModule)합니다.

### <a name="how-can-i-configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>AD FS를 사용 하 여 Windows 통합 인증 WIA ()를 사용 하는 브라우저 구성 어떻게 해야 합니까?

브라우저를 구성 하는 방법에 대 한 내용은 [AD FS를 사용 하 여 Windows 통합 인증 WIA ()를 사용 하는 브라우저 구성](../operations/Configure-AD-FS-Browser-WIA.md)합니다.

### <a name="can-i-turn-off-browserssoenabled"></a>BrowserSsoEnabled을 해제할 수 있습니까?
ADFS;를 사용 하 여 비즈니스 인증서 등록 용 ADFS 또는 Windows Hello에서 장치 기반 액세스 제어 정책이 없는 경우 BrowserSsoEnabled를 해제할 수 있습니다. BrowserSsoEnabled ADFS를 PRT (기본 새로 고침 토큰)는 장치 정보를 포함 하는 클라이언트에서 수집할 수 있습니다. ADFS 인증 장치 없이 Windows 10 장치에서 작동 하지 않습니다.

### <a name="how-long-are-ad-fs-tokens-valid"></a>유효한 AD FS 토큰 얼마나 걸리나요?

대개이 질문 의미 ''기간 사용자 가져오나 single sign-on (SSO) 새 자격 증명을 입력 하지 않고도 및 컨트롤 하는 방법으로 관리자는?  이 동작을 제어 하는 구성 설정 및 문서에 나와 [AD FS Single Sign On 설정](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-2016-single-sign-on-settings)합니다.

다양 한 쿠키와 토큰의 기본 수명은 (뿐만 아니라 수명을 제어 하는 매개 변수) 아래 나열 됩니다.

**등록 된 장치**

- PRT 및 SSO 쿠키: 최대 90 일 동안 PSSOLifeTimeMins를 받습니다. (제공 된 장치는 14 일 이상 마다 DeviceUsageWindow로 제어 되는)

- 새로 고침 토큰: 일관 된 동작을 제공 하도록 위의 기준으로 계산

- access_token: 신뢰 당사자를 기반으로 기본적으로 1 시간

- id_token: 액세스 토큰으로 동일한

**장치 등록된 취소**

- SSO 쿠키: 기본적으로 8 시간 SSOLifetimeMins를 받습니다.  기본값은 24 시간 동안 유지 (KMSI)에서 로그인을 사용 하면 되며 KMSILifetimeMins 통해 구성할 수 있습니다.


- 새로 고침 토큰: 기본적으로 8 시간입니다. KMSI 설정 24 시간 동안

- access_token: 신뢰 당사자를 기반으로 기본적으로 1 시간

- id_token: 액세스 토큰으로 동일한

### <a name="does-ad-fs-support-http-strict-transport-security-hsts"></a>AD FS HTTP 엄격한 전송 보안 (HSTS)을 지원 하나요?  

HTTP 엄격한 전송 보안 (HSTS)에는 데 도움이 되는 프로토콜 다운 그레이드 공격 및 HTTP와 HTTPS 끝점이 있는 서비스에 대 한 쿠키 하이재킹 완화 웹 보안 정책 메커니즘입니다. 웹 서버를 웹 브라우저 (또는 다른 유효한 사용자 에이전트) 상호 작용 해야 하지 HTTP 프로토콜을 통해 및 HTTPS를 사용 하 여 선언할 수 있습니다.

웹 인증 트래픽에 대 한 모든 AD FS 끝점은 HTTPS를 통해서만 열립니다.  결과적으로, AD FS HTTP 엄격한 전송 보안 정책 메커니즘을 제공 하는 위협을 효과적으로 완화 (설계에 없는 다운 그레이드 HTTP http에서 수신기를 찾지 되므로). 또한 AD FS 보안 플래그를 사용 하 여 모든 쿠키를 표시 하 여 HTTP 프로토콜 끝점을 사용 하 여 다른 서버로 전송 되는 쿠키를 방지 합니다.

따라서 HSTS를 구현 하는 AD FS 서버에서 필요 하지 않은 다운 그레이드 하지 않습니다 수 있습니다.  규정 준수를 위해 AD FS 서버 HTTP를 사용 하지는 모든 쿠키 보안 표시 된 것 이므로 이러한 요구 사항을 충족 합니다.

### <a name="x-ms-forwarded-client-ip-does-not-contain-the-ip-of-the-client-but-contains-ip-of-the-firewall-in-front-of-the-proxy-where-can-i-get-the-right-ip-of-the-client"></a>X-ms-전달-클라이언트-ip는 클라이언트의 IP 포함 하지 않지만 프록시 앞에 방화벽의 IP를 포함 합니다. 클라이언트의 올바른 IP 가져오기
WAP 하기 전에 SSL 종료를 수행 하는 권장 되지 않습니다. SSL 종료를 WAP 앞에 수행 되는 경우 X-ms-전달-클라이언트-ip는 WAP 앞에 네트워크 장치의 IP를 포함 합니다. 다음은 다양 한 IP에 대 한 간단한 설명은 관련 AD FS에서 지원 되는 클레임입니다.
 - x-ms-client-ip : STS에 연결 된 장치의 IP 네트워크입니다.  요청을 엑스트라넷의 경우 항상 IP WAP 포함합니다.
 - x-ms-forwarded-client-ip : Exchange Online 및 WAP에 연결 하는 장치의 IP 주소에서 ADFS에 전달 된 값을 포함 하는 다중 값된 클레임입니다.
 - Userip: 엑스트라넷의 요청에 대 한이 클레임 x-ms-전달-클라이언트-ip의 값이 포함 됩니다.  인트라넷 요청에 대 한이 클레임 x-ms-클라이언트-ip와 동일한 값을 포함 됩니다.

### <a name="i-am-trying-to-get-additional-claims-on-the-user-info-endpoint-but-its-only-returning-subject-how-can-i-get-additional-claims"></a>사용자 정보 끝점 있지만 반환 하는 추가 클레임을 제목 가져오기 하려고 합니다. 추가 클레임을 어떻게 얻을 수 있나요?
ADFS userinfo 끝점에는 항상 OpenID 표준에 지정 된 주체 클레임을 반환합니다. AD FS UserInfo 끝점을 통해 요청 하는 추가 클레임을 제공 하지 않습니다. ID 토큰에서 추가 클레임을 할 경우 가리킵니다 [AD FS에서 사용자 지정 ID 토큰](../development/custom-id-tokens-in-ad-fs.md)합니다.

### <a name="why-do-i-see-a-lot-of-1021-errors-on-my-ad-fs-servers"></a>내 AD FS 서버에서 많은 1021 오류가 나타나는 이유는 무엇입니까?
이 이벤트는 00000003-0000-0000-c000-000000000000 리소스에 대 한 AD FS에서 잘못 된 리소스 액세스에 대 한 일반적으로 기록 됩니다. 이 오류는 Azure AD Graph 서비스에 대 한 액세스 토큰을 가져오려고 시도 클라이언트는 잘못 된 동작에 의해 발생 합니다. 리소스, AD FS에 있는 아니므로이 인해 AD FS 서버에서 이벤트 ID 1021 합니다. 모든 경고 또는 AD FS에서 00000003-0000-0000-c000-000000000000 리소스에 대 한 오류를 무시 해도 됩니다.

### <a name="why-am-i-seeing-a-warning-for-failure-to-add-the-ad-fs-service-account-to-the-enterprise-key-admins-group"></a>엔터프라이즈 키 관리 그룹에 AD FS 서비스 계정을 추가 하는 오류에 대 한 경고 왜 표시 되나요?
Windows 2016 도메인 컨트롤러에 PDC FSMO 역할을 사용 하 여 도메인에 있는 경우에이 그룹이 생성 됩니다. 오류를 해결 하려면 그룹을 수동으로 만들어야 하 수에 따라는 서비스 계정 그룹의 구성원으로 추가한 후 필요한 권한을 부여 하려면 아래.
1.  **Active Directory 사용자 및 컴퓨터**를 엽니다.
2.  **마우스 오른쪽 단추로 클릭** 탐색 창에서 도메인 이름이 고 **클릭** 속성입니다.
3.  **클릭** Security (보안 탭이 없는 경우 고급 기능 켜기 보기 메뉴에서).
4.  **클릭** 고급입니다. **클릭** 추가 합니다. **클릭** 보안 주체를 선택 합니다.
5.  사용자, 컴퓨터, 서비스 계정 또는 그룹 선택 대화 상자가 나타납니다.  선택 텍스트 상자에 입력 개체 이름, 키 관리 그룹을 입력 합니다.  확인을 클릭합니다.
6.  선택 목록 상자, 적용 대상에서 **하위 사용자 개체**합니다.
7.  페이지의 아래쪽으로 스크롤하여 스크롤 막대를 사용 하 고 **클릭** 모든 선택을 취소 합니다.
8.  에 **속성** 섹션에서 **Msds-keycredentiallink 읽기** 하 고 **Msds-keycredentiallink 작성**합니다.

### <a name="why-does-modern-authentication-from-android-devices-fail-if-the-server-does-not-send-all-the-intermediate-certificates-in-the-chain-with-the-ssl-cert"></a>서버 SSL 인증서를 사용 하 여 체인의 모든 중간 인증서를 보내지 않는 경우 Android 장치에서 최신 인증 실패 이유는 인가요?

페더레이션된 사용자가 Android ADAL 라이브러리 실패를 사용 하는 앱에 대 한 Azure AD 인증을 발생할 수 있습니다. 앱이 표시 됩니다는 **AuthenticationException** 로그인 페이지를 표시 하려고 할 때입니다. Chrome AD FS 로그인 페이지 수 명시 되어 안전 하지 않은 것입니다.

Android-모든 버전 및 모든 장치에서 지원 하지 않습니다 추가 인증서를 다운로드 합니다 **authorityInformationAccess** 인증서의 필드입니다. Chrome 브라우저도 마찬가지입니다. 중간 인증서가 없는 모든 서버 인증 인증서는 AD FS에서 전체 인증서 체인을 전달 하지 않으면이 오류가 발생 합니다.

이 문제를 적절 한 솔루션을 SSL 인증서와 함께 필요한 중간 인증서를 보내도록 AD FS 및 WAP 서버를 구성 하는 것입니다.

경우에 개인 키 및 선택 키를 내보내려면 있는지 확인 컴퓨터의 개인 저장소, AD FS 및 WAP 서버를 가져오기 위해 하나의 컴퓨터에서 SSL 인증서 내보내기 **개인 정보 교환-PKCS #12**합니다.

확인란에 반드시 **가능 하면 인증 경로에 모든 인증서 포함** 확인란이 뿐만 **확장 된 속성 모두 내보내기**합니다.  

Windows 서버의 certlm.msc를 실행 하 고 가져오기는 *입니다. 컴퓨터의 개인 인증서 저장소에 PFX를 제공 합니다. 그러면 ADAL 라이브러리에 전체 인증서 체인을 전달 하는 서버.

>[!NOTE]
> 인증서 저장소의 네트워크 부하 분산 장치 있으면 전체 인증서 체인을 포함 하도록 업데이트 해야

### <a name="does-ad-fs-support-head-requests"></a>AD FS HEAD 요청을 지원 하나요?
AD FS는 HEAD 요청을 지원 하지 않습니다.  응용 프로그램 HEAD 요청 AD FS 끝점에 대해 사용 하지 말아야 합니다.  예기치 않은 및/또는 지연 된 HTTP 오류 응답 않을 수 있습니다.  또한 AD FS 이벤트 로그에 오류 이벤트가 나타날 수 있습니다.

### <a name="why-am-i-not-seeing-a-refresh-token-when-i-am-logging-in-with-a-remote-idp"></a>하지 표시 되는 이유는 새로 고침 토큰 I am 원격 IdP 로그인 할 때?
새로 고침 토큰은 IdP에서 발급 한 토큰에 1 시간 미만의 validty 하는 경우에 발급 되지 않습니다. 새로 고침 토큰을 발급을 위해 1 시간 이상 IdP에서 발급 한 토큰의 유효성을 늘립니다.

### <a name="do-we-have-any-way-to-change-rp-token-encryption-algorithm"></a>RP 토큰 암호화 알고리즘을 변경 하는 방식으로 가요?
기본적으로 RP 토큰 암호화는 AES256을 설정 하 고 다른 값으로 변경할 수 없습니다.

### <a name="on-a-mixed-mode-farm-i-get-error-when-trying-to-set-the-new-ssl-certificate-using-set-adfssslcertificate--thumbprint-how-can-i-update-the-ssl-certificate-in-a-mixed-mode-ad-fs-farm"></a>혼합 모드 팜에서 오류가 Set-adfssslcertificate를 사용 하 여 새 SSL 인증서를 설정 하려고 할 때-지문입니다. 혼합 모드로 AD FS 팜의 SSL 인증서를 업데이트 하려면 어떻게 해야 합니까?
WAP 서버의 집합 WebApplicationProxySslCertificate를 여전히 사용할 수 있습니다. ADFS 서버에서 netsh를 사용 해야 합니다. 아래 제공 된 단계를 수행 합니다.

1. 유지 관리를 위해 ADFS 2016 서버의 하위 집합 선택 (예: 부하 분산 장치에서 제거)
2. # 1에서 선택한 서버에서 MMC 통해 새 인증서를 가져와야 합니다.
3. 기존 인증서를 삭제 합니다.

    a. netsh http delete sslcert hostnameport=fs.contoso.com:443 b입니다. netsh http delete sslcert hostnameport = localhost:443 c입니다. netsh http delete sslcert hostnameport=fs.contoso.com:49443

4.  새 인증서 추가

    a. netsh http 추가 sslcert hostnameport=fs.contoso.com:443 certhash CERTTHUMBPRINT appid = {5d89a20c-beab-4389-9447-324788eb944a} certstorename = MY sslctlstorename = AdfsTrustedDevices =

    b. netsh http 추가 sslcert hostnameport localhost:443 certhash = CERTTHUMBPRINT appid = {5d89a20c-beab-4389-9447-324788eb944a} certstorename = MY sslctlstorename = AdfsTrustedDevices =

    c. netsh http 추가 sslcert hostnameport=fs.contoso.com:49443 certhash CERTTHUMBPRINT appid = {5d89a20c-beab-4389-9447-324788eb944a} certstorename = MY sslctlstorename = AdfsTrustedDevices =

5. 선택한 서버에 ADFS 서비스를 다시 시작
6. 유지 관리에 대 한 WAP 서버의 하위 집합 제거
7. 선택한 WAP 서버에서 MMC 통해 새 인증서를 가져와야 합니다.
8. Cmdlet을 사용 하 여 WAP 새 인증서 설정

    a. 집합 WebApplicationProxySslCertificate-지문 "CERTTHUMBPRINT"

9. 선택한 WAP 서버의 서비스를 다시 시작
10. 프로덕션 환경에 다시 선택한 AD FS 및 WAP 서버를 설치 합니다.

나머지 AD FS 및 WAP 서버 것과 비슷한 방식에 업데이트를 수행 합니다.

### <a name="is-adfs-supported-when-web-application-proxy-wap-servers-are-behind-azure-web-application-firewallwaf"></a>ADFS가 웹 응용 프로그램 프록시 (WAP) 서버는 Azure 웹 응용 프로그램 Firewall(WAF) 뒤 때 지원 되나요?
ADFS 및 웹 응용 프로그램 서버 끝점에서 SSL 종료를 수행 하지 않는 모든 방화벽을 지원 합니다. 또한 ADFS/WAP 서버 기본적으로 교차 사이트 스크립팅, ADFS 프록시가 등 일반적인 웹 공격을 방지 하 고 정의 된 모든 요구 사항을 충족 하는 메커니즘을 [MS ADFSPIP 프로토콜](https://msdn.microsoft.com/library/dn392811.aspx)합니다.

### <a name="i-am-seeing-an-event-441-a-token-with-a-bad-token-binding-key-was-found-what-should-i-do-to-resolve-this"></a>표시는 "441 이벤트: 잘못 된 토큰 바인딩 키를 사용 하 여 토큰을 찾았습니다. " 이 해결 하려면 어떻게 해야 합니까?
Ad FS 2016에서 여러 알려진된 문제가 발생 프록시 및 페더레이션 시나리오와 함께 결과 오류가 및 토큰 바인딩 자동으로 활성화 됩니다. 이 해결 하려면 다음 Powershell 명령을 실행 하 고 토큰 바인딩 지원을 제거 합니다.

`Set-AdfsProperties -IgnoreTokenBinding $true`
