---
ms.assetid: b7bf7579-ca53-49e3-a26a-6f9f8690762f
title: AD FS 및 웹 응용 프로그램 프록시를 보호 하기 위한 모범 사례
description: 이 문서에서는 보안 계획 및 Active Directory Federation Services (AD FS) 및 웹 응용 프로그램 프록시 배포에 대 한 모범 사례를 제공 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 38de2bca413ce7f8aeda2af4392f9a616641b189
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873074"
---
## <a name="best-practices-for-securing-active-directory-federation-services"></a>Active Directory Federation Services 보안에 대 한 모범 사례

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 문서에서는 보안 계획 및 Active Directory Federation Services (AD FS) 및 웹 응용 프로그램 프록시 배포에 대 한 모범 사례를 제공 합니다.  이러한 구성 요소 및 권장 사항 특정 사용 사례 및 보안 요구 사항을 사용 하 여 조직에 대 한 추가 보안 구성에 대 한 기본 동작에 대 한 정보를 포함 합니다.

이 문서는 AD FS 및 WAP Windows Server 2012 R2 및 Windows Server 2016 (미리 보기)에 적용 됩니다.  이러한 권장 사항은 인프라는 온-프레미스 네트워크에서 또는 Microsoft Azure와 같은 클라우드 호스팅 환경에서 배포 여부를 사용할 수 있습니다.

## <a name="standard-deployment-topology"></a>표준 배포 토폴로지
온-프레미스 환경에서 배포를 DMZ 또는 엑스트라넷 네트워크에 있는 하나 이상의 웹 응용 프로그램 프록시 (WAP) 서버를 사용 하 여 내부 회사 네트워크에 있는 하나 이상의 AD FS 서버로 구성 된 표준 배포 토폴로지를 권장 합니다.  각 계층에서 AD FS 및 WAP, 하드웨어 또는 소프트웨어 부하 분산 장치는 서버 팜의 앞에 배치 됩니다 하 고 트래픽 라우팅을 처리 합니다.  방화벽은 각 (FS 및 프록시) 팜의 앞에 부하 분산 장치의 외부 IP 주소 앞의 필요에 따라 배치 됩니다.

![AD FS 표준 토폴로지](media/Best-Practices-Securing-AD-FS/adfssec1.png)

## <a name="ports-required"></a>필요한 포트
아래 다이어그램 및 AD FS 및 WAP 배포의 구성 요소 간에 사용 되어야 하는 방화벽 포트를 보여 줍니다.  배포에 Azure AD 포함 되어 있지 않으면 / Office 365, 동기화 요구 사항 무시할 수 있습니다.

>포트 49443만는 필요한 경우 사용자 인증서 인증이 사용 되는 Azure AD에 대 한 선택 사항인 및 Office 365입니다.

![AD FS 표준 토폴로지](media/Best-Practices-Securing-AD-FS/adfssec2.png)

### <a name="azure-ad-connect-and-federation-serverswap"></a>Azure AD Connect 및 페더레이션 서버/w a P
이 테이블에는 포트 및 Azure AD Connect 서버와 페더레이션/WAP 서버 간의 통신에 필요한 프로토콜을 설명 합니다.  

프로토콜 |포트 |설명
--------- | --------- |---------
HTTP|80 (TCP/UDP)|Crl (인증서 해지 목록) 확인 SSL 인증서를 다운로드 하는 데 사용 합니다.
HTTPS|443(TCP/UDP)|Azure AD와 동기화 하는 데 사용 합니다.
WinRM|5985| WinRM 수신기

### <a name="wap-and-federation-servers"></a>WAP 및 페더레이션 서버
이 테이블에는 포트 및 페더레이션 서버와 WAP 서버 간의 통신에 필요한 프로토콜을 설명 합니다.

프로토콜 |포트 |설명
--------- | --------- |---------
HTTPS|443(TCP/UDP)|인증에 사용 합니다.

### <a name="wap-and-users"></a>WAP 및 사용자
이 표에서 포트와 사용자 및 WAP 서버 간의 통신에 필요한 프로토콜.

프로토콜 |포트 |설명
--------- | --------- |--------- |
HTTPS|443(TCP/UDP)|장치 인증에 사용 합니다.
TCP|49443 (TCP)|인증서 인증에 사용 합니다.

문서를 참조 하는 하이브리드 배포에 필요한 필수 포트 및 프로토콜에 대 한 자세한 내용은 [여기](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-ports/)합니다.

Azure AD에 대 한 필요한 포트 및 프로토콜에 대 한 자세한 내용은 및 Office 365 배포에 문서를 참조 하세요 [여기](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US)합니다.

### <a name="endpoints-enabled"></a>끝점을 사용할 수

AD FS 및 WAP 설치 되 면 프록시 및 페더레이션 서비스에서 AD FS 끝점의 기본 집합을 사용 하도록 설정 합니다.  이러한 기본값은 가장 일반적으로 필수 및 사용 되는 시나리오에 따라 선택 된 및 변경 하려면 필요는 없습니다.  

### <a name="optional-min-set-of-endpoints-proxy-enabled-for-azure-ad--office-365"></a>[선택 사항] 끝점 프록시를 Azure AD에 대 한 사용의 최소 집합 / Office 365
Azure AD에 대해서만 AD FS 및 WAP를 배포 하는 조직 및 Office 365 시나리오 더욱 최소화 공격 노출 영역을 달성 하기 위해 프록시에 사용 하도록 설정 하는 AD FS 끝점 수가 제한할 수 있습니다.
다음은 이러한 시나리오에서 프록시에 사용 되어야 하는 끝점 목록입니다.

|엔드포인트|용도
|-----|-----
|/adfs/ls|브라우저 기반 인증 흐름 및 Azure AD에 대 한이 끝점을 사용 하는 현재 버전의 Microsoft Office 및 Office 365 인증
|/adfs/services/trust/2005/usernamemixed|Office 2013, 2015 년의 업데이트 보다 이전 Office 클라이언트를 사용 하 여 Exchange Online에 대 한 사용 합니다.  이후 클라이언트 수동 \adfs\ls 끝점을 사용 합니다.
|/adfs/services/trust/13/usernamemixed|Office 2013, 2015 년의 업데이트 보다 이전 Office 클라이언트를 사용 하 여 Exchange Online에 대 한 사용 합니다.  이후 클라이언트 수동 \adfs\ls 끝점을 사용 합니다.
|/adfs/oauth2|이 작업 영역을 사용 되지 않은 (AAD)를 통해 AD FS에 직접 인증 하도록 구성 (온-프레미스 또는 클라우드에서) 최신 앱에 대 한
|/adfs/services/trust/mex|Office 2013, 2015 년의 업데이트 보다 이전 Office 클라이언트를 사용 하 여 Exchange Online에 대 한 사용 합니다.  이후 클라이언트 수동 \adfs\ls 끝점을 사용 합니다.
|/adfs/ls/federationmetadata/2007-06/federationmetadata.xml |모든 수동 흐름;에 대 한 요구 사항 Office 365/azure AD AD FS 인증서를 확인 하려면에서 사용 되 고


다음 PowerShell cmdlet을 사용 하 여 프록시에 AD FS 끝점을 비활성화할 수 있습니다.
    
    PS:\>Set-AdfsEndpoint -TargetAddressPath <address path> -Proxy $false

예를 들어 다음과 같은 가치를 제공해야 합니다.
    
    PS:\>Set-AdfsEndpoint -TargetAddressPath /adfs/services/trust/13/certificatemixed -Proxy $false
    

### <a name="extended-protection-for-authentication"></a>인증에 대 한 확장 된 보호
인증에 대 한 확장 된 보호 기능은 man (mitm 메시지 가로채기) 공격에 대 한 완화 하는 AD FS 사용 하 여 기본적으로 사용 합니다.

#### <a name="to-verify-the-settings-you-can-do-the-following"></a>설정을 확인 하려면 다음을 수행할 수 있습니다.
설정을 사용 하 여 확인할 수 있습니다는 PowerShell commandlet 아래.  
    
   `PS:\>Get-ADFSProperties`

속성은 `ExtendedProtectionTokenCheck`합니다.  기본 설정에는 허용 되므로 기능을 지원 하지 않는 브라우저를 사용 하 여 호환성 문제 없이 보안 이점을 얻을 수 있습니다.  

### <a name="congestion-control-to-protect-the-federation-service"></a>페더레이션 서비스를 보호 하기 위해 정체 제어
페더레이션 서비스 프록시 (WAP의 일부)에서 과도 한 요청을 AD FS 서비스를 보호 하기 위해 정체 제어를 제공 합니다.  웹 응용 프로그램 프록시는 웹 응용 프로그램 프록시와 페더레이션 서버 간의 대기 시간이 감지 된 페더레이션 서버가 오버 로드 된 경우 외부 클라이언트 인증 요청을 거부 합니다.  이 기능은 기본적으로 권장 되는 대기 시간 임계값 수준으로 구성 됩니다.

#### <a name="to-verify-the-settings-you-can-do-the-following"></a>설정을 확인 하려면 다음을 수행할 수 있습니다.
1.  웹 응용 프로그램 프록시 컴퓨터에 관리자 권한 명령 창을 시작 합니다.
2.  % WINDIR%\adfs\config ADFS 디렉터리로 이동 합니다.
3.  해당 기본값에서 정체 제어 설정을 변경 '<congestionControl latencyThresholdInMSec="8000" minCongestionWindowSize="64" enabled="true" />'.
4.  파일을 저장하고 닫습니다.
5.  'Net stop adfssrv' 및 'net start adfssrv'를 실행 하 여 AD FS 서비스를 다시 시작 합니다.
참조용으로이 기능에 대 한 지침을 찾을 수 있습니다 [여기](https://msdn.microsoft.com/en-us/library/azure/dn528859.aspx )합니다.

### <a name="standard-http-request-checks-at-the-proxy"></a>표준 HTTP 요청을 프록시 확인
프록시는 또한 모든 트래픽에 대해 다음 표준 검사를 수행합니다.

- 수명이 짧은 인증서를 통해 AD fs 자체 Fs-p를 인증합니다.  Dmz 서버의 의심 되는 손상 시나리오 "를 해지할 수 프록시 트러스트"는 더 이상 신뢰 들어오는 모든 요청에서 잠재적으로 AD FS 프록시를 손상입니다. AD FS 서버에 목적을 위해 성공적으로 인증할 수 없는 되도록 각 프록시 자체 인증서를 해지 프록시 트러스트를 취소 합니다.
- FS-P는 모든 연결을 종료 하 고 내부 네트워크에서 AD FS 서비스에 새 HTTP 연결을 만듭니다. 외부 장치 및 AD FS 서비스 간의 세션 수준 버퍼를 제공합니다. 외부 장치는 AD FS 서비스에 직접 하지 연결합니다.
- FS-P 특히 AD FS 서비스 필요 하지 않은 HTTP 헤더를 필터링 하는 HTTP 요청 유효성 검사를 수행 합니다.

## <a name="recommended-security-configurations"></a>권장된 보안 구성
AD FS 인프라에 권장 되는 가장 중요 한 보안 방법을 AD FS 및 WAP 서버를 모든 보안 업데이트 뿐만 아니라 해당 옵션을 사용 하 여 최신 상태로 유지 하는 위치에 있는지 확인 하는 것은 최신 업데이트를 수신 하는 모든 AD FS 및 WAP 서버 확인 이 페이지에서 AD FS에 대 한 중요로 지정 된 업데이트 합니다.

AD FS, Azure AD Premium의 기능에 대 한 Azure AD Connect Health를 통해 인프라 것이 모니터링 하 고 최신 상태로 유지 하려면 Azure AD 고객용 좋습니다.  Azure AD Connect Health에는 모니터 및 AD FS 또는 WAP 컴퓨터를 AD FS 및 WAP에 특히 중요 업데이트 중 누락 된 경우 트리거되는 경고를 포함 합니다.

AD FS 용 Azure AD Connect Health를 설치 하는 방법은 [여기](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-health-agent-install/)합니다.

## <a name="additional-security-configurations"></a>추가 보안 구성
기본 배포에서 제공 하는 추가 보호 기능을 제공 하려면 다음과 같은 추가 기능을 필요에 따라 구성할 수 있습니다.

### <a name="extranet-soft-lockout-protection-for-accounts"></a>계정에 대 한 "soft" 엑스트라넷 잠금 보호
엑스트라넷 잠금 기능을 사용 하면 Windows Server 2012 R2에서 AD FS 관리자는 허용 된 최대 수의 실패 한 인증 요청 (ExtranetLockoutThreshold)를 설정할 수 있습니다 및 ' 관찰 창의 기간 (ExtranetObservationWindow). 이 인증 요청의 최대 수 (ExtranetLockoutThreshold)에 도달 하면 AD FS 설정된 기간 (ExtranetObservationWindow)에 대 한 AD FS에 대해 제공 된 계정 자격 증명을 인증 하려는 시도 중지 합니다. 이 작업을 보호이 계정은 AD 계정 잠금에서, 즉,이 계정은 사용자의 인증을 위해 AD FS를 사용 하는 회사 리소스에 대 한 액세스를 손실 보호 합니다. 이러한 설정은 AD FS 서비스를 인증할 수 있는 모든 도메인에 적용 됩니다.

AD FS 엑스트라넷 잠금 (예:)을 설정 하려면 다음 Windows PowerShell 명령을 사용할 수 있습니다. 

    PS:\>Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow ( new-timespan -Minutes 30 )

이 기능의 공개 문서는 참조용 [여기](https://technet.microsoft.com/library/dn486806.aspx )합니다. 

### <a name="differentiate-access-policies-for-intranet-and-extranet-access"></a>인트라넷 및 엑스트라넷 액세스에 대 한 액세스 정책을 구분합니다
AD FS에 프록시를 통해 인터넷에서 제공 하는 로컬, 회사 네트워크 및 요청에서 발생 하는 요청에 대 한 액세스 정책을 구별할 수 있습니다.  이 응용 프로그램 또는 전역으로 수행할 수 있습니다.  높은 비즈니스 응용 프로그램 또는 중요 한 정보나 개인 식별이 가능한 정보를 사용 하 여 응용 프로그램에 대 한 다단계 인증을 요구 하는 것이 좋습니다.  이 AD FS 관리 스냅인을 통해 수행할 수 있습니다.  

### <a name="require-multi-factor-authentication-mfa"></a>다단계 인증 (MFA) 필요 합니다.
AD FS 프록시를 통해 들어오는 요청에 맞게, 개별 응용 프로그램 및 Azure AD에 대 한 조건부 액세스에 대 한 강력한 인증 (예: 다단계 인증)를 요구 하도록 구성할 수 있습니다 / Office 365 및 온-프레미스 리소스입니다.  Mfa 지원 되는 메서드는 Microsoft Azure MFA와 타사 공급자를 포함합니다.  사용자는 추가 정보를 제공 하 라는 메시지가 표시 됩니다 (등을 포함 하는 SMS 문자 코드 시간), 공급자 특정 액세스를 허용 하도록 플러그 인을 사용 하 여 AD FS가 작동 하 고 있습니다.  

에 나열 된 지원 되는 외부 MFA 공급자 포함 [이](https://technet.microsoft.com/library/dn758113.aspx) 페이지 뿐만 아니라 HDI 전역입니다.

### <a name="hardware-security-module-hsm"></a>HSM(하드웨어 보안 모듈)
기본 구성 키 AD FS는 토큰에 서명 하지 인트라넷의 페더레이션 서버를 둡니다.  DMZ에 또는 프록시 컴퓨터에 존재 하지 않습니다.  필요에 따라 추가적인 보호를 제공 하려면 AD FS에 연결 된 하드웨어 보안 모듈에서 이러한 키를 보호할 수 있습니다.  하지만 Microsoft HSM 제품을 생성 하지 않습니다, 몇 가지에 AD FS를 지원 합니다.  이 권장 사항을 구현 하기 위해 X509를 만들려면 공급 업체 지침에 따라 서명 및 암호화를 위한 인증서 같이 사용자 지정 인증서를 지정 하는 AD FS 설치 powershell commandlet을 사용 합니다.

    PS:\>Install-AdfsFarm -CertificateThumbprint <String> -DecryptionCertificateThumbprint <String> -FederationServiceName <String> -ServiceAccountCredential <PSCredential> -SigningCertificateThumbprint <String>

각 항목이 나타내는 의미는 다음과 같습니다.


- `CertificateThumbprint` SSL 인증서는
- `SigningCertificateThumbprint` HSM 보호 키가 있는 서명 인증서는
- `DecryptionCertificateThumbprint` HSM 보호 키가 있는 암호화 인증서는



