---
ms.assetid: 1ea2e1be-874f-4df3-bc9a-eb215002da91
title: 사용자 인증서 인증에 대 한 AD FS 지원 구성
description: ''
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 01/18/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b5f2202313c225d57b29997753b090e10b9c2e6c
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949289"
---
# <a name="configuring-ad-fs-for-user-certificate-authentication"></a>사용자 인증서 인증을 위한 AD FS 구성

사용자 인증서 인증은 주로 두 개의 사용 사례에서 사용 됩니다.
* 사용자가 스마트 카드를 사용 하 여 AD FS 시스템에 로그인 하 고 있습니다.
* 사용자가 모바일 장치에 프로 비전 된 인증서를 사용 하 고 있습니다.


## <a name="prerequisites"></a>전제 조건
1) [이 문서](ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md) 에서 설명 하는 모드 중 하나를 사용 하 여 사용 하도록 설정할 AD FS 사용자 인증서 인증 모드를 결정 합니다.
2) 모든 중간 인증 기관을 포함 하 여 모든 AD FS 및 WAP 서버에서 신뢰할 수 & 사용자 인증서 신뢰 체인이 설치 되어 있는지 확인 합니다. 일반적으로이 작업은 AD FS/WAP 서버에서 GPO를 통해 수행 됩니다.
3)  사용자 인증서의 신뢰 체인에 대 한 루트 인증서가의 NTAuth 저장소에 있는지 확인 하십시오 Active Directory
4) 대체 인증서 인증 모드에서 AD FS 사용 하는 경우 AD FS 및 WAP 서버에 "certauth" 접두사가 붙은 AD FS 호스트 이름 (예: "certauth.fs.contoso.com")이 포함 된 SSL 인증서가 있고이 호스트 이름에 대 한 트래픽이 허용 되는지 확인 합니다. 방화벽을 통해
5) 엑스트라넷에서 인증서 인증을 사용 하는 경우 인증서에 지정 된 목록에 있는 하나 이상의 CDP 또는 OCSP 위치를 인터넷에서 액세스할 수 있어야 합니다.
6) 또한 Azure AD 인증서 인증의 경우, Exchange ActiveSync 클라이언트의 경우 클라이언트 인증서 주체 이름 또는 주체 대체 이름 필드의 RFC822 이름 값에 Exchange online의 사용자 라우팅할 수 있는 전자 메일 주소가 있어야 합니다. Azure Active Directory RFC822 값을 디렉터리의 프록시 주소 특성에 매핑합니다.


## <a name="configure-ad-fs-for-user-certificate-authentication"></a>사용자 인증서 인증을 위한 AD FS 구성  

AD FS 관리 콘솔 또는 PowerShell cmdlet `Set-AdfsGlobalAuthenticationPolicy`를 사용 하 여 AD FS에서 사용자 인증서 인증을 인트라넷 또는 엑스트라넷 인증 방법으로 사용 하도록 설정 합니다.

Azure AD 인증서 인증에 대 한 AD FS를 구성 하는 경우 [AZURE ad 설정](https://docs.microsoft.com/azure/active-directory/active-directory-certificate-based-authentication-get-started#step-2-configure-the-certificate-authorities) 및 인증서 발급자와 일련 번호에 [필요한 AD FS 클레임 규칙](https://docs.microsoft.com/azure/active-directory/active-directory-certificate-based-authentication-ios#requirements) 을 구성 했는지 확인 합니다.

또한 몇 가지 선택적 측면이 있습니다.
- EKU (클레임 유형 https://schemas.microsoft.com/2012/12/certificatecontext/extension/eku) 를 비롯 하 여 인증서 필드 및 확장에 기반 하는 클레임을 사용 하려는 경우 Active Directory 클레임 공급자 트러스트에 대 한 추가 클레임 통과 규칙을 구성 합니다.  사용 가능한 인증서 클레임의 전체 목록은 아래를 참조 하십시오.  
- 인증서의 형식에 따라 액세스를 제한 해야 하는 경우에는 응용 프로그램에 대 한 AD FS 발급 권한 부여 규칙에서 인증서에 대 한 추가 속성을 사용할 수 있습니다. 일반적인 시나리오는 "MDM 공급자가 프로 비전 한 인증서만 허용" 또는 "스마트 카드 인증서만 허용"입니다.
- [이 문서](https://technet.microsoft.com/library/dn786429(v=ws.11).aspx)에서 "클라이언트 인증에 대 한 신뢰할 수 있는 발급자 관리"의 지침에 따라 클라이언트 인증서에 대해 허용 된 발급 인증 기관을 구성 합니다.
- 인증서 인증을 수행할 때 최종 사용자의 요구에 맞게 로그인 페이지를 수정 하는 것을 고려해 볼 수 있습니다. 일반적인 사례는 (a) ' X509 인증서를 사용 하 여 로그인 '을 더 많은 최종 사용자에 게 친숙 하 게 변경 하는 것입니다.

## <a name="configure-seamless-certificate-authentication-for-chrome-browser-on-windows-desktops"></a>Windows 데스크톱에서 Chrome 브라우저에 대 한 원활한 인증서 인증 구성
클라이언트 인증의 용도를 충족 하는 여러 사용자 인증서 (예: Wi-fi 인증서)가 컴퓨터에 있는 경우 Windows 데스크톱의 Chrome 브라우저에서 적절 한 인증서를 선택 하 라는 메시지를 표시 합니다. 이는 최종 사용자에 게 혼란 스 러 울 수 있습니다. 이러한 환경을 최적화 하기 위해 Chrome에 대 한 정책을 설정 하 여 더 나은 사용자 환경을 위해 올바른 인증서를 자동으로 선택할 수 있습니다. 레지스트리 키를 설정 하도록 GPO를 통해 자동으로 레지스트리를 변경 하거나 구성 하 여이 정책을 수동으로 설정할 수 있습니다. 이렇게 하려면 다른 사용 사례에서 고유한 발급자를 갖도록 AD FS에 대 한 인증을 위해 사용자 클라이언트 인증서가 필요 합니다. 

Chrome에 대해이를 구성 하는 방법에 대 한 자세한 내용은이 [링크](http://www.chromium.org/administrators/policy-list-3#AutoSelectCertificateForUrls)를 참조 하세요.  


## <a name="troubleshoot-certificate-authentication"></a>인증서 인증 문제 해결
이 문서에서는 AD FS 사용자에 대 한 인증서 인증을 구성할 때 발생 하는 일반적인 문제를 해결 하는 데 중점을 설명 합니다. 

### <a name="check-if-certificate-trusted-issuers-is-configured-properly-in-all-the-ad-fswap-servers"></a>모든 AD FS/WAP 서버에서 인증서 신뢰 발급자가 올바르게 구성 되어 있는지 확인 합니다.
*일반적인 증상: HTTP 204 "https의 콘텐츠 없음\://certuath.adfs.contoso.com"*

AD FS는 기본 windows 운영 체제를 사용 하 여 사용자 인증서의 소유를 증명 하 고 인증서 신뢰 체인 유효성 검사를 수행 하 여 신뢰할 수 있는 발급자와 일치 하는지 확인 합니다. 신뢰할 수 있는 발급자와 일치 시키려면 모든 루트 및 중간 기관이 로컬 컴퓨터 인증 기관 저장소에서 신뢰할 수 있는 발급자로 구성 되었는지 확인 해야 합니다. 자동으로 유효성을 검사 하려면 [AD FS 진단 분석기 도구](https://adfshelp.microsoft.com/DiagnosticsAnalyzer/Analyze)를 사용 하세요. 이 도구는 모든 서버를 쿼리하고 올바른 인증서가 올바르게 프로 비전 되는지 확인 합니다. 
1)  위의 링크에 제공 된 지침에 따라 도구를 다운로드 하 여 실행 합니다.
2)  결과를 업로드 하 고 오류를 검토 합니다.

### <a name="check-if-certificate-authentication-is-enabled-in-the-ad-fs-authentication-policy"></a>AD FS 인증 정책에서 인증서 인증을 사용 하도록 설정 했는지 확인 합니다.
AD FS는 기본적으로 인증서 인증을 사용 하지 않습니다. 인증서 인증을 사용 하도록 설정 하는 방법은이 문서의 시작 부분을 참조 하세요. 

### <a name="check-if-certificate-authentication-is-enabled-in-the-ad-fs-authentication-policy"></a>AD FS 인증 정책에서 인증서 인증을 사용 하도록 설정 했는지 확인 합니다.
AD FS은 기본적으로 AD FS와 동일한 호스트 이름을 사용 하는 포트 49443에서 사용자 인증서 인증을 수행 합니다 (예: `adfs.contoso.com`). 대체 SSL 바인딩을 사용 하 여 포트 443 (기본 HTTPS 포트)를 사용 하도록 AD FS 구성할 수도 있습니다. 그러나이 구성에 사용 되는 URL은 `certauth.<adfs-farm-name>` (예: `certauth.contoso.com`). 자세한 내용은 [이 링크](ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md) 를 참조 하세요. 네트워크 연결의 가장 일반적인 경우는 방화벽이 잘못 구성 되어 사용자 인증서 인증 트래픽을 차단 하거나 방해 하는 것입니다. 일반적으로이 문제가 발생 하면 빈 화면이 표시 되거나 500 서버 오류가 표시 됩니다. 
1)  AD FS에서 구성한 호스트 이름 및 포트를 확인 합니다.
2)  AD FS 또는 WAP (웹 응용 프로그램 프록시) 앞의 방화벽이 AD FS 팜에 대 한 `hostname:port` 조합을 허용 하도록 구성 되어 있는지 확인 합니다. 이 단계를 수행 하려면 네트워크 엔지니어를 참조 해야 합니다. 

### <a name="check-certificate-revocation-list-connectivity"></a>인증서 해지 목록 연결 확인
CRL (인증서 해지 목록)은 런타임 해지 검사를 수행 하기 위해 사용자 인증서로 인코딩된 끝점입니다. 예를 들어 인증서를 포함 하는 장치를 도난당 한 경우 관리자는 해지 된 인증서 목록에 인증서를 추가할 수 있습니다. 이 인증서를 이전에 수락한 모든 끝점은 이제 인증에 실패 합니다.

모든 AD FS 및 WAP 서버는 제공 된 인증서가 여전히 유효 하 고 해지 되지 않은 경우 유효성을 검사 하기 위해 CRL 끝점에 연결 해야 합니다. CRL 유효성 검사는 HTTPS, HTTP, LDAP 또는 OCSP (온라인 인증서 상태 프로토콜)를 통해 수행할 수 있습니다. AD FS/WAP 서버에서 끝점에 연결할 수 없는 경우 인증에 실패 합니다. 문제를 해결 하려면 아래 단계를 따르세요. 
1) Pki 시스템에서 사용자 인증서를 해지 하는 데 사용 되는 CRL 끝점을 확인 하려면 PKI 엔지니어에 게 문의 하세요. 
2)  각 AD FS/WAP 서버에서 사용 되는 프로토콜 (일반적으로 HTTPS 또는 HTTP)을 통해 CRL 끝점에 연결할 수 있는지 확인 합니다.
3)  고급 유효성 검사의 경우 각 AD FS/WAP 서버에서 [CAPI2 이벤트 로깅을 사용 하도록 설정](https://blogs.msdn.microsoft.com/benjaminperkins/2013/09/30/enable-capi2-event-logging-to-troubleshoot-pki-and-ssl-certificate-issues/) 합니다.
4) CAPI2 작업 로그에서 이벤트 ID 41 (해지 확인)를 확인 합니다.
5) `‘\<Result value="80092013"\>The revocation function was unable to check revocation because the revocation server was offline.\</Result\>'` 확인

***팁***: 특정 서버를 가리키도록 DNS 확인 (WINDOWS에서 호스트 파일)을 구성 하 여 쉽게 문제를 해결 하기 위해 단일 AD FS 또는 WAP 서버를 대상으로 지정할 수 있습니다. 이렇게 하면 서버를 대상으로 하는 추적을 사용 하도록 설정할 수 있습니다. 

### <a name="check-if-this-is-a-server-name-indication-sni-issue"></a>SNI (서버 이름 표시) 문제 인지 확인 합니다.
AD FS에는 클라이언트 장치 (또는 브라우저)와 SNI를 지 원하는 부하 분산 장치가 필요 합니다. 일부 클라이언트 장치 (일반적으로 이전 버전의 Android)는 SNI를 지원 하지 않을 수 있습니다. 또한 부하 분산 장치는 SNI를 지원 하지 않거나 SNI에 대해 구성 되지 않았을 수 있습니다. 이러한 경우 사용자 인증 오류가 표시 될 수 있습니다. 
1)  네트워크 엔지니어와 협력 하 여 AD FS/WAP Load Balancer에서 SNI를 지원 하는지 확인 합니다.
2)  SNI를 지원할 수 없는 경우 다음 단계를 수행 하 여 해결 AD FS 있습니다.
    *   기본 AD FS 서버에서 관리자 권한 명령 프롬프트 창을 엽니다.
    *   ```Netsh http show sslcert``` 입력
    *   페더레이션 서비스의 ' 응용 프로그램 GUID ' 및 ' 인증서 해시 ' 복사
    *   `netsh http add sslcert ipport=0.0.0.0:{your_certauth_port} certhash={your_certhash} appid={your_applicaitonGUID}` 입력

### <a name="check-if-the-client-device-has-been-provisioned-with-the-certificate-correctly"></a>클라이언트 장치가 인증서를 사용 하 여 올바르게 프로 비전 되었는지 확인 합니다.
일부 장치가 제대로 작동 하지만 다른 장치는 제대로 작동 하지 않는 것을 알 수 있습니다. 이 경우 일반적으로 사용자 인증서가 클라이언트 장치에서 올바르게 프로 비전 되지 않기 때문입니다. 아래 단계를 따르세요. 
1)  문제가 Android 장치에만 해당 되는 경우 가장 일반적인 문제는 Android 장치에서 인증서 체인이 완전히 신뢰 되지 않는 것입니다.  MDM 공급 업체에 문의 하 여 인증서가 올바르게 프로 비전 되었으며 전체 체인이 Android 장치에서 완전히 신뢰할 수 있는지 확인 하세요. 
2)  문제가 Windows 장치에만 해당 되는 경우 Windows 인증서 저장소에서 로그인 한 사용자 (시스템/컴퓨터 아님)를 확인 하 여 인증서가 올바르게 프로 비전 되었는지 확인 합니다.
3)  클라이언트 사용자 인증서를 .cer 파일로 내보내고 ' certutil-f-urlfetch-verify certificatefilename .cer ' 명령을 실행 합니다.


### <a name="check-if-the-tls-version-is-compatible-between-ad-fswap-servers-and-the-client-device"></a>AD FS/WAP 서버와 클라이언트 장치 간에 TLS 버전이 호환 되는지 확인 합니다.
드문 경우 지만 클라이언트 장치 (일반적으로 모바일 장치)는 더 높은 버전의 TLS (예 1.3)만 지원 하도록 업데이트 되거나 더 높은 TLS 버전만 사용 하도록 AD FS/WAP 서버를 업데이트 하 고 클라이언트 장치에서이를 지원 하지 않는 문제를 발생 시킬 수 있습니다. 온라인 SSL 도구를 사용 하 여 AD FS/WAP 서버를 확인 하 고 장치와 호환 되는지 확인할 수 있습니다. TLS 버전을 제어 하는 방법에 대 한 자세한 내용은 [이 링크](manage-ssl-protocols-in-ad-fs.md)를 참조 하세요.

### <a name="check-if-azure-ad-promptloginbehavior-is-configured-correctly-on-your-federated-domain-settings"></a>페더레이션된 도메인 설정에서 Azure AD PromptLoginBehavior가 올바르게 구성 되어 있는지 확인 합니다.
많은 Office 365 응용 프로그램은 prompt = Azure AD에 로그인을 보냅니다. 기본적으로 Azure AD는 AD FS에 대 한 새 암호 로그인으로 변환 합니다. 따라서 AD FS에서 인증서 인증을 구성한 경우에도 최종 사용자에 게는 암호 로그인만 표시 됩니다. 
1)  ' Get-msoldomainfederationsettings ' 명령 let을 사용 하 여 페더레이션된 도메인 설정 가져오기
2)  PromptLoginBehavior 매개 변수가 ' Disabled ' 또는 ' NativeSupport ' 중 하나로 설정 되었는지 확인 하세요.

자세한 내용은 [이 링크](ad-fs-prompt-login.md)를 참조 하세요. 

### <a name="additional-troubleshooting"></a>추가적인 문제 해결
드물게 발생 합니다.
1)  CRL 목록이 매우 긴 경우 다운로드를 시도할 때 시간이 초과 될 수 있습니다. 이 경우에는 ' MaxFieldLength ' 및 ' Maxfieldlength '를 https://support.microsoft.com/help/820129/http-sys-registry-settings-for-windows 를 기준으로 업데이트 해야 합니다.




## <a name="reference-complete-list-of-user-certificate-claim-types-and-example-values"></a>참조: 사용자 인증서 클레임 유형 및 예제 값의 전체 목록

|                                         클레임 유형                                         |                              예제 값                               |
|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------|
|         https://schemas.microsoft.com/2012/12/certificatecontext/field/x509version         |                                    3                                     |
|     https://schemas.microsoft.com/2012/12/certificatecontext/field/signaturealgorithm      |                                sha256RSA                                 |
|           https://schemas.microsoft.com/2012/12/certificatecontext/field/issuer            |                 CN = entca, DC = domain, DC = contoso, DC = com                  |
|         https://schemas.microsoft.com/2012/12/certificatecontext/field/issuername          |                 CN = entca, DC = domain, DC = contoso, DC = com                  |
|          https://schemas.microsoft.com/2012/12/certificatecontext/field/notbefore          |                           12/05/2016 20:50:18                            |
|          https://schemas.microsoft.com/2012/12/certificatecontext/field/notafter           |                           12/05/2017 20:50:18                            |
|           https://schemas.microsoft.com/2012/12/certificatecontext/field/subject           |   E =user@contoso.com, CN = user, CN = Users, DC = domain, DC = contoso, DC = com   |
|         https://schemas.microsoft.com/2012/12/certificatecontext/field/subjectname         |   E =user@contoso.com, CN = user, CN = Users, DC = domain, DC = contoso, DC = com   |
|           https://schemas.microsoft.com/2012/12/certificatecontext/field/rawdata           |                {Base64 인코딩된 디지털 인증서 데이터}                 |
|        https://schemas.microsoft.com/2012/12/certificatecontext/extension/keyusage         |                             DigitalSignature                             |
|        https://schemas.microsoft.com/2012/12/certificatecontext/extension/keyusage         |                             KeyEncipherment                              |
|  https://schemas.microsoft.com/2012/12/certificatecontext/extension/subjectkeyidentifier   |                 9D11941EC06FACCCCB1B116B56AA97F3987D620A                 |
| https://schemas.microsoft.com/2012/12/certificatecontext/extension/authoritykeyidentifier  |    KeyID = d6 13 e3 6b bc e5 d8 15 52 ffd 36 6a d5 0b 51 f3 0b 25 7f     |
| https://schemas.microsoft.com/2012/12/certificatecontext/extension/certificatetemplatename |                                   사용자                                   |
|           https://schemas.microsoft.com/2012/12/certificatecontext/extension/san           | 기타 이름: Principal Name =user@contoso.com, RFC822 Name =user@contoso.com |
|           https://schemas.microsoft.com/2012/12/certificatecontext/extension/eku           |                          1.3.6.1.4.1.311.10.3.4                          |

## <a name="related-links"></a>관련 링크
* [AD FS 인증서 인증에 대 한 대체 호스트 이름 바인딩 구성](ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md)
* [Azure AD에서 인증 기관 구성](https://docs.microsoft.com/azure/active-directory/active-directory-certificate-based-authentication-get-started#step-2-configure-the-certificate-authorities)
