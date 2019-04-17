---
ms.assetid: 1ea2e1be-874f-4df3-bc9a-eb215002da91
title: "ADFS 지원을 사용자 인증 인증서에 대 한 구성"
description: 
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 01/18/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.service: active-directory
ms.technology: identity-adfs
ms.openlocfilehash: 9941d4dd997e857874aceddc920ec7f9d8944a81
ms.sourcegitcommit: d351cdbb0bf2533d6db35626ebbc4924b3834309
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2018
---
# <a name="configuring-ad-fs-for-user-certificate-authentication"></a>ADFS 사용자 인증 인증서에 대 한 구성

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

ADFS 모드 중 하나를 사용 하 여 사용자 인증서 인증에 설명 된 x509 구성할 수 있습니다 [이 문서의](ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md)합니다. 이 기능을 사용할 수 [Azure Active Directory를](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/) 는 자체 클라이언트 및 디바이스 수 있도록 프로 비전 인증서 ADFS 액세스를 사용자와 인트라넷 또는 익스트라넷에에서 리소스 또는 합니다.

## <a name="prerequisites"></a>필수
- 모든 Adfs와 WAP 서버에서 신뢰 하 여 사용자 인증서 확인
- 신뢰 사용자 인증서 체인의 루트 인증서 Active Directory에 NTAuth 스토어에서가 있는지 확인
- ADFS 대체 인증서 인증 모드에서를 사용 하는 경우 ADFS 및 WAP 서버 SSL "certauth" 접두사 ADFS 호스트 이름을 포함 하는 예를 들어 "certauth.fs.contoso.com" 하 고 인증서 방화벽을 통해이 호스트 트래픽을 허용 있는지 확인
- 엑스트라넷 인증 인증서를 사용 하는 경우 하나 이상의 AIA, 인증서에 지정 된 목록에서 하나 이상의 CDP 또는 OCSP 위치는 인터넷에서 액세스할 수 있는지 확인 하세요.
- ADFS Azure AD 인증서를 인증에 대 한 구성 하는 경우 사용자가 구성 되어 있는지 확인는 [Azure AD 설정](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-certificate-based-authentication-get-started#step-2-configure-the-certificate-authorities) 및 [ADFS 주장 필요한 규칙](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-certificate-based-authentication-ios#requirements) 인증서 발행인이 및 일련 번호
- 또한 Exchange ActiveSync 클라이언트에 대 한 Azure AD 인증서 인증에 대 한 클라이언트 인증서 있어야 사용자 경로 조정 가능 메일 주소 Exchange 온라인 사용자 이름 또는 주체 대체 이름 필드 RFC822 이름 값 합니다. (Azure Active Directory 지도 RFC822 값 프록시 주소 특성 디렉터리에.)

## <a name="configure-ad-fs-for-user-certificate-authentication"></a>ADFS 사용자 인증 인증서에 대 한 구성  
- 인트라넷 또는 광고 FS Management console 또는 PowerShell cmdlet Set-AdfsGlobalAuthenticationPolicy 사용 하 여 adfs에서 익스트라넷 인증 방법을 사용자 인증서 인증 설정
- 신뢰, 중간 인증서를 포함 하 여 전체 체인 모든 ADFS 및 WAP 서버에 설치 되어 있는지 확인 합니다. 로컬 컴퓨터 중간 인증 기관 저장소 모든 Adfs와 WAP 서버에 중간 인증서를 설치 해야 합니다.
- If you wish to use claims based on certificate fields and extensions in addition to EKU (claim type https://schemas.microsoft.com/2012/12/certificatecontext/extension/eku), configure additional claim pass through rules on the Active Directory claims provider trust.  사용 가능한 인증서 클레임의 전체 목록은 아래 참조 하십시오.  
- [선택적] "클라이언트 인증을 위해 신뢰할 수 있는 발급자 관리" 아래의 지침을 사용 하 여 클라이언트 인증서를 허용된 발급 인증 기관에서 구성 [이 문서의](https://technet.microsoft.com/en-us/library/dn786429(v=ws.11).aspx)합니다.

## <a name="configure-seamless-certificate-authentication-for-chrome-browser-on-windows-desktops"></a>Windows 데스크톱에서 크롬 브라우저에 대 한 원활 하 게 인증서 인증을 구성 합니다.
(예: Wi-fi 인증서) 여러 사용자 인증서 클라이언트 인증 목적 충족 하는 컴퓨터에 있는 경우 Windows 데스크톱에서 크롬 브라우저 사용자 오른쪽 인증서를 요청 합니다. 최종 사용자에 게 혼동 될 수 있습니다. 이 환경을 최적화 하려면 Chrome 자동 선택 사용자 환경 개선을 위한 오른쪽 인증서에 대 한 정책을 설정할 수 있습니다. 이 정책 레지스트리 변경이으로 수동으로 설정 하거나 GPO (레지스트리 키 설정)를 통해 자동으로 구성 될 수 있습니다. 이를 사용 하 여 경우도의 고유한 발급자 Adfs에 대해 인증에 대 한 사용자 클라이언트 인증서 필요 합니다. 

Chrome이 구성에 대 한 자세한 내용은이 참조 하 여 [링크](http://www.chromium.org/administrators/policy-list-3#AutoSelectCertificateForUrls)합니다.  


## <a name="troubleshooting"></a>문제 해결
- 인증서 인증 요청 HTTP 204 "https://certauth.fs.contoso.com에서 콘텐츠 더" 응답와 함께 실패를 루트와 중간 캘리포니아 인증서 설치 되어 있는지 확인을 각각, 캐나다 및 중간 캘리포니아 신뢰할 수 있는 루트 인증서 모든 federation 서버에 저장 합니다.
- 알 수 없는 이유로 인증서 인증 요청이 실패를 클라이언트 인증서.cer 파일을 내보내고 명령을 실행합니다 

`certutil -f -urlfetch -verify certificatefilename.cer`

모든 CRL 및 CRL 위치 해결 델타 있는지 확인 합니다.  델타 CRL 위치 발견 되는 참고 자료 crl 내용에 따라 합니다.

## <a name="reference-complete-list-of-user-certificate-claim-types-and-example-values"></a>참조: 유형과 예제 값 사용자 인증서의 전체 목록은 주장

|클레임 유형|예제 가치
|-----|-----
|https://schemas.microsoft.com/2012/12/certificatecontext/field/x509version | 3
|https://schemas.microsoft.com/2012/12/certificatecontext/field/signaturealgorithm | sha256RSA
|https://schemas.microsoft.com/2012/12/certificatecontext/field/issuer | CN DC entca = = 도메인, DC DC contoso = com =
|https://schemas.microsoft.com/2012/12/certificatecontext/field/issuername | CN DC entca = = 도메인, DC DC contoso = com =
|https://schemas.microsoft.com/2012/12/certificatecontext/field/notbefore | 12/05/2016 20:50:18
|https://schemas.microsoft.com/2012/12/certificatecontext/field/notafter | 12/05/2017 20:50:18
|https://schemas.microsoft.com/2012/12/certificatecontext/field/subject | E =user@contoso.com, CN CN 사용자 = = DC 사용자 = 도메인, DC DC contoso = com =
|https://schemas.microsoft.com/2012/12/certificatecontext/field/subjectname | E =user@contoso.com, CN CN 사용자 = = DC 사용자 = 도메인, DC DC contoso = com =
|https://schemas.microsoft.com/2012/12/certificatecontext/field/rawdata | {Base 64 디지털 인증서 데이터 인코딩된}
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/keyusage | DigitalSignature
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/keyusage | KeyEncipherment
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/subjectkeyidentifier | 9D11941EC06FACCCCB1B116B56AA97F3987D620A
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/authoritykeyidentifier | KeyID d 6 13 e3 6b = bc e 5 d 8 15 52 0a fd 36 6a d 5 0b 51 f3 0b 25 7f
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/certificatetemplatename | 사용자
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/san | 다른 이름: 사용자 이름 =user@contoso.com, RFC822 이름을 =user@contoso.com
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/eku | 1.3.6.1.4.1.311.10.3.4


