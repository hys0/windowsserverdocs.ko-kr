---
ms.assetid: 1ea2e1be-874f-4df3-bc9a-eb215002da91
title: 사용자 인증서 인증을 위해 AD FS 지원 구성
description: ''
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 01/18/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2d819ea036029fbe7cfde9ad5a445db6b2b42c96
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189702"
---
# <a name="configuring-ad-fs-for-user-certificate-authentication"></a>사용자 인증서 인증을 위해 AD FS를 구성합니다.


에 설명 된 사용자 인증서 인증 모드 중 하나를 사용 하 여 x509 AD FS를 구성할 수 있습니다 [이 문서에서는](ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md)합니다. 이 기능을 사용할 수 있습니다 [Azure Active Directory를 사용 하 여](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/) 자체적으로 클라이언트 및 장치를 사용 하도록 설정 하려면 프로 비전 된 사용자 인증서 액세스 AD FS 사용 하 여 인트라넷 또는 엑스트라넷에서 리소스 또는 합니다.

## <a name="prerequisites"></a>사전 요구 사항
- 모든 AD FS 및 WAP 서버에서 사용자 인증서는 신뢰할 수 있는지 확인
- Active Directory NTAuth 저장소에 있는 사용자 인증서에 대 한 신뢰 체인의 루트 인증서 인지 확인
- 대체 인증서 인증 모드에서 AD FS를 사용 하는 경우 AD FS 및 WAP 서버 "certauth", 예를 들어 "certauth.fs.contoso.com"가를 접두사로 AD FS 호스트 이름을 포함 하는 SSL 인증서를 갖도록 하 고이 호스트 이름에는 트래픽이 허용 됩니다. 방화벽을 통해
- 엑스트라넷에서 인증서 인증을 사용 하는 경우 하나 이상의 AIA 및 CDP 또는 OCSP를 하나 이상 위치 인증서에 지정 된 목록에서 인터넷에서 액세스할 수 있는지 확인 합니다.
- Azure AD 인증서 인증을 위해 AD FS를 구성 하는 경우 구성 했는지 확인 합니다 [Azure AD 설정을](https://docs.microsoft.com/azure/active-directory/active-directory-certificate-based-authentication-get-started#step-2-configure-the-certificate-authorities) 하며 [AD FS 클레임 규칙 필요한](https://docs.microsoft.com/azure/active-directory/active-directory-certificate-based-authentication-ios#requirements) 인증서 발급자와 일련 번호에 대 한
- 또한 Exchange ActiveSync 클라이언트에 대 한 Azure AD 인증서 인증을 위해 클라이언트 인증서 사용자의 라우팅할 수 있는 전자 메일 주소를 Exchange online 있어야 주체 이름 또는 주체 대체 이름 필드의 RFC822 이름 값에 합니다. (Azure Active Directory 매핑됩니다 RFC822 값을 디렉터리에 프록시 주소 특성.)

## <a name="configure-ad-fs-for-user-certificate-authentication"></a>사용자 인증서 인증을 위한 AD FS 구성  
- 인트라넷 또는 엑스트라넷 인증 방법을 AD FS 관리 콘솔 또는 PowerShell cmdlet 집합 AdfsGlobalAuthenticationPolicy를 사용 하 여 AD FS에서 사용자 인증서 인증을 사용 하도록 설정
- 모든 중간 인증서를 포함 하 여 신뢰의 전체 체인을 모든 AD FS 및 WAP 서버에 설치 되어 있는지 확인 합니다. 중간 인증서는 모든 AD FS 및 WAP 서버의 로컬 컴퓨터 중간 인증 기관 저장소에 설치 되어야 합니다.
- 인증서 필드 및 EKU 외에도 확장을 기반으로 클레임을 사용 하려는 경우 (클레임 유형 https://schemas.microsoft.com/2012/12/certificatecontext/extension/eku), Active Directory 클레임 공급자 트러스트 추가 클레임 통과 규칙을 구성 합니다.  사용 가능한 인증서 클레임의 전체 목록은 아래를 참조 하세요.  
- [선택 사항] "클라이언트 인증을 위해 신뢰할 수 있는 발급자 관리" 아래에 있는 지침을 사용 하 여 클라이언트 인증서에 대 한 허용 된 발급 인증 기관에서 구성할 [이 문서에서는](https://technet.microsoft.com/library/dn786429(v=ws.11).aspx)합니다.

## <a name="configure-seamless-certificate-authentication-for-chrome-browser-on-windows-desktops"></a>Windows 데스크톱에서 Chrome 브라우저에 대 한 원활한 인증서 인증을 구성 합니다.
여러 사용자 인증서 (예: Wi-fi 인증서)가 클라이언트 인증의 목적을 충족 하는 컴퓨터의 Windows 바탕 화면에서 Chrome 브라우저 사용자가 적합 한 인증서를 선택할 요청 합니다. 최종 사용자에 게 혼동을 줄 수 있습니다. 이러한 경험을 최적화 하려면 자동 선택 사용자 경험 개선을 위해 적합 한 인증서를 Chrome에 대 한 정책을 설정할 수 있습니다. 이 정책은 레지스트리 변경 하 여 수동으로 설정 또는 GPO (레지스트리 키 설정)를 통해 자동으로 구성할 수 있습니다. 다른 사용 사례에서 고유한 발급자 하도록 AD FS에 대 한 인증에 대 한 사용자 클라이언트 인증서 필요 합니다. 

Chrome에 대 한이 구성에 대 한 자세한 내용은이를 참조 하십시오 [링크](http://www.chromium.org/administrators/policy-list-3#AutoSelectCertificateForUrls)합니다.  


## <a name="troubleshooting"></a>문제 해결
- HTTP 204를 사용 하 여 인증서 인증 요청이 실패 하는 경우 "https에서 콘텐츠 없음:\//certauth.fs.contoso.com" 응답 루트 및 중간 CA 인증서 설치 되어 있는지, 각각 신뢰할 수 있는 루트 CA 확인 하 고 중간 CA 인증서는 모든 페더레이션 서버에 저장합니다.
- 클라이언트 인증서를.cer 파일로 내보내기 및 명령을 실행 하 여 인증서 인증 요청을 알 수 없는 이유로 실패 하는 경우 

`certutil -f -urlfetch -verify certificatefilename.cer`

모든 CRL 및 델타 CRL 위치 확인을 확인 합니다.  델타 CRL 위치 발견 되는 참고 자료 CRL의 내용을 기반으로 합니다.

## <a name="reference-complete-list-of-user-certificate-claim-types-and-example-values"></a>참조: 사용자 인증서의 전체 목록은 클레임 형식 및 값 예

|클레임 형식|예를 들어 값
|-----|-----
|https://schemas.microsoft.com/2012/12/certificatecontext/field/x509version | 3
|https://schemas.microsoft.com/2012/12/certificatecontext/field/signaturealgorithm | sha256RSA
|https://schemas.microsoft.com/2012/12/certificatecontext/field/issuer | CN=entca, DC=domain, DC=contoso, DC=com
|https://schemas.microsoft.com/2012/12/certificatecontext/field/issuername | CN=entca, DC=domain, DC=contoso, DC=com
|https://schemas.microsoft.com/2012/12/certificatecontext/field/notbefore | 12/05/2016 20:50:18
|https://schemas.microsoft.com/2012/12/certificatecontext/field/notafter | 12/05/2017 20:50:18
|https://schemas.microsoft.com/2012/12/certificatecontext/field/subject | E=user@contoso.com, CN=user, CN=Users, DC=domain, DC=contoso, DC=com
|https://schemas.microsoft.com/2012/12/certificatecontext/field/subjectname | E=user@contoso.com, CN=user, CN=Users, DC=domain, DC=contoso, DC=com
|https://schemas.microsoft.com/2012/12/certificatecontext/field/rawdata | {Base64로 인코딩된 디지털 인증서 데이터가}
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/keyusage | DigitalSignature
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/keyusage | KeyEncipherment
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/subjectkeyidentifier | 9D11941EC06FACCCCB1B116B56AA97F3987D620A
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/authoritykeyidentifier | KeyID=d6 13 e3 6b bc e5 d8 15 52 0a fd 36 6a d5 0b 51 f3 0b 25 7f
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/certificatetemplatename | 사용자
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/san | 다른 이름: 사용자 이름 =user@contoso.com, RFC822 이름 =user@contoso.com
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/eku | 1.3.6.1.4.1.311.10.3.4


