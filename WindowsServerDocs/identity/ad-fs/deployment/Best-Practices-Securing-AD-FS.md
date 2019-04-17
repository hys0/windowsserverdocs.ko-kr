---
ms.assetid: b7bf7579-ca53-49e3-a26a-6f9f8690762f
title: "ADFS 및 웹 응용 프로그램 프록시 보안에 대 한 유용한"
description: "이 문서는 보안 계획 및 Active Directory Federation Services (ADFS) 및 웹 응용 프로그램 프록시 배포에 대 한 유용한 정보를 제공합니다."
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6026246228b22fdea6001528ab7621a1704f1983
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
## <a name="best-practices-for-securing-active-directory-federation-services"></a>모범 사례에 대 한 Active Directory Federation Services 보안

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 문서는 보안 계획 및 Active Directory Federation Services (ADFS) 및 웹 응용 프로그램 프록시 배포에 대 한 유용한 정보를 제공합니다.  이러한 구성 요소 및 추천을 제공 된 경우에 특정 사용 및 보안 요구 사항을 조직에 대 한 추가 보안 구성에 대 한 기본 동작에 대 한 정보를 포함 합니다.

이 문서 ADFS 및 Windows Server 2012 R2 및 Windows Server 2016 (미리 보기) WAP 적용 됩니다.  이러한 권장 인프라에 프레미스 네트워크 또는 등 Microsoft Azure 클라우드 호스트 환경 배포는 여부를 사용할 수 있습니다.

## <a name="standard-deployment-topology"></a>표준 배포가
온-프레미스 환경에서 배포용 DMZ 또는 엑스트라넷 네트워크에서 하나 이상의 웹 프록시 WAP (응용 프로그램) 서버와 함께 내부 회사 네트워크에 있는 하나 이상의 ADFS 서버 이루어진 표준 배포가 것이 좋습니다.  각 계층 Adfs와 WAP에서 하드웨어 또는 소프트웨어 부하 분산 서버 농장 앞에 위치 하 고 교통 경로 처리 합니다.  방화벽 각 (FS 및 프록시) 농장 앞 부하 분산의 IP 주소 외부의 앞에 필요한 저장 됩니다.

![AD FS 표준 토폴로지](media/Best-Practices-Securing-AD-FS/adfssec1.png)

## <a name="ports-required"></a>필요한 포트
다이어그램 아래 간에 및 구성 요소 Adfs와 WAP 배포 사이에서 사용 해야 하 고 방화벽 포트 보여 줍니다.  배포 Azure AD 포함 되어 있지 않으면 / Office 365를 동기화 요구 무시할 수 있습니다.

>포트 49443만이 필요한 경우 사용자 인증서 인증을 사용 하는 Azure AD에 대 한 옵션은 및 Office 365 합니다.

![AD FS 표준 토폴로지](media/Best-Practices-Securing-AD-FS/adfssec2.png)

### <a name="azure-ad-connect-and-federation-serverswap"></a>Azure AD 연결 및 Federation 서버/WAP
이 표에서 포트와 Azure AD 연결 서버와 Federation/WAP 서버 간 통신에 필요한 프로토콜 설명 합니다.  

프로토콜 |포트 |설명
--------- | --------- |---------
HTTP|80 (TCP/UDP)|다운로드 Crl (인증서 해지 나열) SSL 인증서를 확인 하는 데 사용 합니다.
HTTPS|443(TCP/UDP)|Azure AD와 동기화 하는 데 사용 합니다.
WinRM|5985| WinRM 수신기

### <a name="wap-and-federation-servers"></a>WAP 및 Federation 서버
이 표에서 포트와 Federation 서버와 WAP 서버 간 통신에 필요한 프로토콜 설명 합니다.

프로토콜 |포트 |설명
--------- | --------- |---------
HTTPS|443(TCP/UDP)|인증에 사용.

### <a name="wap-and-users"></a>WAP 및 사용자에 게
이 표에 포트 및 사용자와 WAP 서버의 간 통신에 필요한 프로토콜 되어 있습니다.

프로토콜 |포트 |설명
--------- | --------- |--------- |
HTTPS|443(TCP/UDP)|디바이스 인증 사용합니다.
TCP|49443 (TCP)|인증 인증서 사용합니다.

필요한 포트 및 하이브리드 배포 문서를 참조 필요한 프로토콜에 대 한 자세한 내용은 [여기](https://azure.microsoft.com/en-us/documentation/articles/active-directory-aadconnect-ports/)합니다.

포트를 Azure AD에 필요한 프로토콜에 대 한 자세한 내용은 및 문서를 참조 Office 365 배포 [여기](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US)합니다.

### <a name="endpoints-enabled"></a>끝점 사용

Adfs와 WAP, 설치 시 federation 서비스에 대 한 프록시에 ADFS 끝점의 기본 설정 사용 하도록 설정 합니다.  가장 일반적으로 필요 하 고 사용 하는 경우에 따라 이러한 기본값 선택 하 고 변경 필요는 없습니다.  

### <a name="optional-min-set-of-endpoints-proxy-enabled-for-azure-ad--office-365"></a>[선택적] Azure AD에 대 한 사용 끝점 프록시 분 집합 / Office 365
조직 Adfs와 WAP Azure AD에 대 한 배포 및 Office 365 시나리오를 추가로 ADFS 끝점 더 최소한의 공격을 달성 하기 위해 프록시에서 사용할 수 제한할 수 있습니다.
아래에서 이러한 시나리오에서 프록시 설정 해야 하는 끝점 목록에는 다음과 같습니다.

|Endpoint|목적
|-----|-----
|1/adfs /!|브라우저 기반 인증 흐름 및 Azure AD에 대 한이 끝점 사용 하 여 현재 버전의 Microsoft Office 및 Office 365 인증
|/adfs/services/trust/2005/usernamemixed|Office 2013 2015 년 5 월 업데이트 보다 오래 된 Office 고객과 Exchange Online을 사용 합니다.  이후 클라이언트 수동 \adfs\ls 끝점을 사용합니다.
|/adfs/services/trust/13/usernamemixed|Office 2013 2015 년 5 월 업데이트 보다 오래 된 Office 고객과 Exchange Online을 사용 합니다.  이후 클라이언트 수동 \adfs\ls 끝점을 사용합니다.
|/ adfs/oauth2|이 사용 하지 즉, (AAD)를 통해 Adfs에 직접 인증 구성 (프레미스 또는 클라우드에) 최신 앱에 대 한
|/adfs/services/trust/mex|Office 2013 2015 년 5 월 업데이트 보다 오래 된 Office 고객과 Exchange Online을 사용 합니다.  이후 클라이언트 수동 \adfs\ls 끝점을 사용합니다.
|/adfs/ls/federationmetadata/2007-06/federationmetadata.xml |수동 된 흐름;에 대 한 요구 사항 Office 365 / Azure AD ADFS 인증서를 확인 하 여 사용 하 고


광고 FS 끝점 다음 PowerShell cmdlet를 사용 하 여 프록시에서 해제할 수 있습니다.
    
    PS:\>Set-AdfsEndpoint -TargetAddressPath <address path> -Proxy $false

예를 들어:
    
    PS:\>Set-AdfsEndpoint -TargetAddressPath /adfs/services/trust/13/certificatemixed -Proxy $false
    

### <a name="extended-protection-for-authentication"></a>인증에 대 한 연장된 보호
인증에 대 한 연장된 보호 남자 들기 (MITM) 공격에서 으로부터 완화 하 고 Adfs와 기본적으로 활성화 되어 하는 기능입니다.

#### <a name="to-verify-the-settings-you-can-do-the-following"></a>설정을 확인 하려면 다음을 수행할 수 있습니다.
설정을 사용 하 여 확인할 수 있는 PowerShell commandlet 아래 합니다.  
    
   `PS:\>Get-ADFSProperties`

속성 `ExtendedProtectionTokenCheck`합니다.  기본 설정 하는 기능을 지원 하지 않는 브라우저와의 호환성 걱정 없이 보안 혜택 얻을 수 있도록 허용을입니다.  

### <a name="congestion-control-to-protect-the-federation-service"></a>혼잡 제어 federation 서비스를 보호 하기
(일부는 WAP의) federation 서비스 프록시 으로부터 보호 하기 위해 ADFS 서비스 과도 한 요청을 혼잡 컨트롤을 제공 합니다.  웹 응용 프로그램 프록시 서버 federation 사이의 지연이에서 감지 federation 서버 오버 로드 되 웹 응용 프로그램 프록시 외부 클라이언트 인증 요청을 거부 합니다.  이 기능은 권장된 대기 임계값 수준으로 기본적으로 구성 됩니다.

#### <a name="to-verify-the-settings-you-can-do-the-following"></a>설정을 확인 하려면 다음을 수행할 수 있습니다.
1.  웹 응용 프로그램 프록시 컴퓨터에서 관리자 권한 명령 창을 시작 합니다.
2.  ADFS 디렉터리 WINDIR%\adfs\config %로 이동 합니다.
3.  기본값을에서 혼잡 컨트롤 설정 변경 '<congestionControl latencyThresholdInMSec="8000" minCongestionWindowSize="64" enabled="true" />' 합니다.
4.  저장 한 파일을 닫습니다.
5.  ADFS 서비스 'net 중지 adfssrv'을 'net 시작 adfssrv'를 선택한 다음을 실행 하 여 다시 시작 합니다.
참조를 위해이 기능에 대 한 지침을 찾을 수 있는 [여기](https://msdn.microsoft.com/en-us/library/azure/dn528859.aspx )합니다.

### <a name="standard-http-request-checks-at-the-proxy"></a>프록시에 표준 HTTP 요청을 확인합니다.
또한 프록시 모든 교통에 대 한 다음 표준 검사를 수행합니다.

- 자체 FS P 수명이 짧은 인증서를 통해 Adfs를 인증합니다.  Dmz 서버 의심 스러운 손상 될 경우, "해지할 수 프록시 신뢰" 이상 신뢰에서 모든 요청 될 수 있도록 ADFS 프록시 손상 합니다. ADFS 서버에 목적 성공적으로 인증 수 있도록 각각 프록시의 인증서 해지 해지 프록시 보안
- FS P 모두 연결을 종료 하 고 내부 네트워크에 새 HTTP 서비스에 연결 하는 ADFS 만듭니다. 외부 디바이스와 ADFS 서비스 간의 세션 수준 버퍼가 제공합니다. 외부 디바이스 절대 ADFS 서비스에 직접 연결합니다.
- FS P 특히 ADFS 서비스 필요 하지 HTTP 헤더를 필터링 하는 HTTP 요청 유효성 검사를 수행 합니다.

## <a name="recommended-security-configurations"></a>권장 되는 보안 구성
모든 ADFS 확인 하 고 WAP 서버 가장 중요 한 보안 ADFS 인프라에 대해 하는 것을 확보 하는 수단 ADFS 및 WAP 서버 Adfs이 페이지에 대 한 중요 한로 지정 이러한 선택적 업데이트 뿐만 아니라 모든 보안 업데이트를 최신 상태로 유지 하는 장소에 최신 업데이트를 수신 합니다.

Azure AD 고객 모니터링 하 고 최신 상태로 유지 하는 권장된 방법 인프라 ADFS Azure AD 프리미엄의 기능에 대 한 Azure AD 연결 상태를 통해입니다.  Azure AD 연결 상태 모니터 및 ADFS 또는 WAP 기계 없는 경우 중요 업데이트 중 하나 Adfs와 WAP에 대해 특별히 트리거하 경고를 포함 합니다.

ADFS 찾을 수 있는 Azure AD 연결 상태 설치에 대 한 내용은 [여기](https://azure.microsoft.com/en-us/documentation/articles/active-directory-aadconnect-health-agent-install/)합니다.

## <a name="additional-security-configurations"></a>추가 보안 구성
기본 배포에서 제공 되는 사람에 게 추가 보호를 제공 하기 위해 다음과 같은 추가 기능이 필요한 경우 구성할 수 있습니다.

### <a name="extranet-soft-lockout-protection-for-accounts"></a>계정에 대 한 보호 익스트라넷 "부드러운" 잠금
ADFS 관리자 실패 인증 요청 (ExtranetLockoutThreshold)의 수를 허용 하는 데 최대 익스트라넷 잠금 기능을 사용 하면 Windows Server 2012 r 2에서 설정 및 ' 관찰 창 기간 (ExtranetObservationWindow). 이 인증 요청의 최대 수 (ExtranetLockoutThreshold)에 도달 하면 ADFS (ExtranetObservationWindow) 설정된 된 시간 동안 Adfs에 대해 제공된 계정 자격 증명 인증 하려고 중지 합니다. 이 계정에서 사용자의 인증용 Adfs에 의존 하는 회사 리소스에 액세스 권한 손실 보호 즉, 광고 계정 잠금이 계정을 보호 하는이 작업을이 수행 합니다. 이러한 설정은 ADFS 서비스 인증할 수 있는 모든 도메인에 적용 됩니다.

다음 Windows PowerShell 명령을 ADFS 엑스트라넷 잠금 (예:)를 설정 하려면 사용할 수 있습니다. 

    PS:\>Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow ( new-timespan -Minutes 30 )

참조를 위해이 기능이 공개 문서는 [여기](https://technet.microsoft.com/en-us/library/dn486806.aspx )합니다. 

### <a name="differentiate-access-policies-for-intranet-and-extranet-access"></a>인트라넷과 엑스트라넷 액세스에 대 한 액세스 정책을 구분 합니다.
ADFS 요청은 인터넷에서 프록시를 통해 제공 되는 로컬, 회사 네트워크와 요청 내의 대 한 액세스 정책을 구분 수가 있습니다.  응용 프로그램 또는 전체적으로 수행할 수 있습니다.  높은 비즈니스 값 응용 프로그램 또는 중요 한 개인 정보 응용 프로그램에 대 한 다중 요소 인증 요구 하는 것이 좋습니다.  이 통해 ADFS 관리 스냅인 수행할 수 있습니다.  

### <a name="require-multi-factor-authentication-mfa"></a>다중 요소 인증 MFA)
ADFS 프록시 통해 들어오는 요청에 대해 특별히, 개별 응용 프로그램 및 두 Azure AD에 대 한 조건 액세스 (다중 요소 인증)와 같은 강력한 인증을 요구 하도록 구성할 수 있습니다 / Office 365 및 프레미스 리소스에 있습니다.  지원 되는 방식을 MFA Azure MFA Microsoft 및 제 3 자 공급자를 포함합니다.  사용자는 추가 정보를 제공 하 라는 메시지가 표시 됩니다 (에 포함 된 SMS 텍스트 등 코드 시간), ADFS 공급자 특정 액세스할 수 있도록 플러그 인와 함께 작동 하 고 있습니다.  

지원 되는 외부 MFA 공급자에 보이는 회사를 포함 [이](https://technet.microsoft.com/en-us/library/dn758113.aspx) 페이지도 HDI 글로벌 합니다.

### <a name="hardware-security-module-hsm"></a>하드웨어 보안 HSM (모듈)
기본 구성에서 절대 토큰 서명 하는 데 ADFS 키 사용 하는 federation 서버 인트라넷 둡니다.  DMZ 또는 프록시 컴퓨터에 있는 되지 않습니다.  필요에 따라 추가 보호 기능을 제공 하려면 Adfs에 부착 된 하드웨어 보안 모듈에서 이러한 키를 보호할 수 있습니다.  그러나는 여러 가지, Microsoft는 HSM 제품 생성 하지 않습니다 ADFS 지원 지역/국가에서 합니다.  이 권장을 구현 하기 위해는 X509 만들 수는 공급 업체 지침에 따라 인증서 서명 및 암호화를 사용 하 여 사용자 지정 인증서 다음과 같은 지정 ADFS 설치 powershell commandlets 다음과 같습니다.

    PS:\>Install-AdfsFarm -CertificateThumbprint <String> -DecryptionCertificateThumbprint <String> -FederationServiceName <String> -ServiceAccountCredential <PSCredential> -SigningCertificateThumbprint <String>

위치:


- `CertificateThumbprint` SSL 인증서가
- `SigningCertificateThumbprint` 키가 있는 보호 HSM 서명 인증서가
- `DecryptionCertificateThumbprint` 키가 있는 보호 HSM 암호화 인증서가



