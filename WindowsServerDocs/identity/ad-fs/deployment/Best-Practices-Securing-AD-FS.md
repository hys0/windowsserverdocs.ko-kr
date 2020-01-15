---
ms.assetid: b7bf7579-ca53-49e3-a26a-6f9f8690762f
title: AD FS 및 웹 응용 프로그램 프록시 보안 설정에 대 한 모범 사례
description: 이 문서에서는 Active Directory Federation Services (AD FS) 및 웹 응용 프로그램 프록시의 보안 계획 및 배포에 대 한 모범 사례를 제공 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: abbc9cf76056af4ac421d9a38381bd8d8f666e4c
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949537"
---
# <a name="best-practices-for-securing-active-directory-federation-services"></a>Active Directory Federation Services 보안에 대 한 모범 사례

이 문서에서는 Active Directory Federation Services (AD FS) 및 웹 응용 프로그램 프록시의 보안 계획 및 배포에 대 한 모범 사례를 제공 합니다.  이러한 구성 요소의 기본 동작 및 특정 사용 사례 및 보안 요구 사항을 포함 하는 조직의 추가 보안 구성에 대 한 권장 사항에 대 한 정보가 포함 되어 있습니다.

이 문서는 Windows Server 2012 R2 및 Windows Server 2016 (preview)의 AD FS 및 WAP에 적용 됩니다.  이러한 권장 사항은 인프라를 온-프레미스 네트워크에 배포할지 아니면 Microsoft Azure와 같은 클라우드 호스팅 환경에 배포할지를 사용 하는 데 사용할 수 있습니다.

## <a name="standard-deployment-topology"></a>표준 배포 토폴로지
온-프레미스 환경에 배포 하는 경우 DMZ 또는 엑스트라넷 네트워크에 하나 이상의 WAP (웹 응용 프로그램 프록시) 서버를 사용 하 여 내부 회사 네트워크에서 하나 이상의 AD FS 서버로 구성 된 표준 배포 토폴로지를 사용 하는 것이 좋습니다.  각 계층, AD FS 및 WAP에서 하드웨어 또는 소프트웨어 부하 분산 장치는 서버 팜 앞에 배치 되 고 트래픽 라우팅을 처리 합니다.  방화벽은 각 (FS 및 프록시) 팜 앞에 있는 부하 분산 장치의 외부 IP 주소 앞에 필요에 따라 배치 됩니다.

![AD FS 표준 토폴로지](media/Best-Practices-Securing-AD-FS/adfssec1.png)

## <a name="ports-required"></a>필요한 포트
아래 다이어그램은 AD FS 및 WAP 배포의 구성 요소 간에 사용 하도록 설정 해야 하는 방화벽 포트를 나타냅니다.  배포에 Azure AD/Office 365이 포함 되지 않은 경우 동기화 요구 사항을 무시 해도 됩니다.

>포트 49443은 사용자 인증서 인증을 사용 하는 경우에만 필요 하며,이는 Azure AD 및 Office 365의 선택 사항입니다.

![AD FS 표준 토폴로지](media/Best-Practices-Securing-AD-FS/adfssec2.png)

>[!NOTE]
> 포트 808 (Windows Server 2012R2) 또는 포트 1501 (Windows Server 2016 +)은 로컬 WCF 끝점에서 서비스 프로세스 및 Powershell로 구성 데이터를 전송 하는 데 사용 하는 Net.tcp 포트 AD FS입니다. 이 포트는 Set-adfsproperties |를 실행 하 여 볼 수 있습니다. NetTcpPort를 선택 합니다. 방화벽에서 열 필요는 없지만 포트 검색에 표시 되는 로컬 포트입니다. 

### <a name="azure-ad-connect-and-federation-serverswap"></a>Azure AD Connect 및 페더레이션 서버/WAP
이 테이블은 Azure AD Connect 서버 및 페더레이션 서버/WAP 서버 간의 통신에 필요한 포트와 프로토콜에 대해 설명합니다.  

프로토콜 |Ports(포트) |설명
--------- | --------- |---------
HTTP|80(TCP/UDP)|CRL(인증서 해지 목록)를 다운로드하여 SSL 인증서를 확인하는 데 사용합니다.
HTTPS|443(TCP/UDP)|Azure AD와 동기화하는 데 사용합니다.
WinRM|5985| WinRM 수신기

### <a name="wap-and-federation-servers"></a>WAP 및 페더레이션 서버
이 테이블은 페더레이션 서버 및 WAP 서버 간의 통신에 필요한 포트와 프로토콜에 대해 설명합니다.

프로토콜 |Ports(포트) |설명
--------- | --------- |---------
HTTPS|443(TCP/UDP)|인증에 사용합니다.

### <a name="wap-and-users"></a>WAP 및 사용자
이 테이블은 사용자 및 WAP 서버 간의 통신에 필요한 포트와 프로토콜에 대해 설명합니다.

프로토콜 |Ports(포트) |설명
--------- | --------- |--------- |
HTTPS|443(TCP/UDP)|디바이스 인증에 사용합니다.
TCP|49443(TCP)|인증서 인증에 사용합니다.

하이브리드 배포에 필요한 포트 및 프로토콜에 대 한 자세한 내용은 [여기](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-ports/)문서를 참조 하세요.

Azure AD 및 Office 365 배포에 필요한 포트 및 프로토콜에 대 한 자세한 내용은 [여기](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US)문서를 참조 하세요.

### <a name="endpoints-enabled"></a>끝점 사용

AD FS 및 WAP가 설치 되 면 페더레이션 서비스 및 프록시에서 기본 AD FS 끝점 집합이 사용 됩니다.  이러한 기본값은 가장 일반적으로 필요한 시나리오와 사용 되는 시나리오를 기반으로 선택 되었으며 변경할 필요가 없습니다.  

### <a name="optional-min-set-of-endpoints-proxy-enabled-for-azure-ad--office-365"></a>필드 Azure AD/Office 365에 대해 사용 하도록 설정 된 최소 끝점 프록시 집합
Azure AD 및 Office 365 시나리오에 대 한 AD FS 및 WAP만 배포 하는 조직은 최소한의 공격 노출 영역을 얻기 위해 프록시에 사용 되는 AD FS 끝점의 수를 제한할 수 있습니다.
다음은 이러한 시나리오에서 프록시를 사용 하도록 설정 해야 하는 끝점 목록입니다.

|끝점|용도
|-----|-----
|/adfs/ls|브라우저 기반 인증 흐름 및 현재 버전의 Microsoft Office Azure AD 및 Office 365 인증에이 끝점을 사용 합니다.
|/adfs/services/trust/2005/usernamemixed|Office 2013 이전 버전의 Office 클라이언트에서 Exchange Online에 사용 되는 2015 업데이트 일 수 있습니다.  이후 클라이언트는 passive \adfs\ls 끝점을 사용 합니다.
|/adfs/services/trust/13/usernamemixed|Office 2013 이전 버전의 Office 클라이언트에서 Exchange Online에 사용 되는 2015 업데이트 일 수 있습니다.  이후 클라이언트는 passive \adfs\ls 끝점을 사용 합니다.
|/adfs/oauth2|이는 AD FS (예: AAD를 통해)에 직접 인증 하도록 구성 된 모든 최신 앱 (예: 프레미스 또는 클라우드에서)에 사용 됩니다.
|/adfs/services/trust/mex|Office 2013 이전 버전의 Office 클라이언트에서 Exchange Online에 사용 되는 2015 업데이트 일 수 있습니다.  이후 클라이언트는 passive \adfs\ls 끝점을 사용 합니다.
|/adfs/ls/federationmetadata/2007-06/federationmetadata.xml |수동 흐름에 대 한 요구 사항 그리고 Office 365/Azure AD에서 AD FS 인증서를 확인 하는 데 사용 됩니다.


다음 PowerShell cmdlet을 사용 하 여 프록시에서 AD FS 끝점을 사용 하지 않도록 설정할 수 있습니다.
    
    PS:\>Set-AdfsEndpoint -TargetAddressPath <address path> -Proxy $false

예를 들어 다음과 같은 가치를 제공해야 합니다.
    
    PS:\>Set-AdfsEndpoint -TargetAddressPath /adfs/services/trust/13/certificatemixed -Proxy $false
    

### <a name="extended-protection-for-authentication"></a>인증에 대한 확장된 보호
인증에 대 한 확장 된 보호는 MITM (중간) 공격 으로부터 완화 하 고 기본적으로 AD FS 사용 하도록 설정 하는 기능입니다.

#### <a name="to-verify-the-settings-you-can-do-the-following"></a>설정을 확인 하려면 다음을 수행할 수 있습니다.
아래 PowerShell 이상을 사용 하 여 설정을 확인할 수 있습니다.  
    
   `PS:\>Get-ADFSProperties`

속성은 `ExtendedProtectionTokenCheck`합니다.  기본 설정은 허용 이므로 기능을 지원 하지 않는 브라우저와의 호환성 문제 없이 보안 이점을 얻을 수 있습니다.  

### <a name="congestion-control-to-protect-the-federation-service"></a>페더레이션 서비스를 보호 하는 정체 제어
페더레이션 서비스 프록시 (WAP의 일부)는 정체 제어를 제공 하 여 많은 요청에서 AD FS 서비스를 보호 합니다.  웹 응용 프로그램 프록시는 웹 응용 프로그램 프록시와 페더레이션 서버 간의 대기 시간으로 검색 된 대로 페더레이션 서버가 오버 로드 되는 경우 외부 클라이언트 인증 요청을 거부 합니다.  이 기능은 기본적으로 권장 되는 대기 시간 임계값 수준으로 구성 됩니다.

#### <a name="to-verify-the-settings-you-can-do-the-following"></a>설정을 확인 하려면 다음을 수행할 수 있습니다.
1.  웹 응용 프로그램 프록시 컴퓨터에서 관리자 권한 명령 창을 시작합니다.
2.  %WINDIR%\adfs\config.에서 ADFS 디렉터리로 이동 합니다.
3.  정체 제어 설정을 기본값에서 '<congestionControl latencyThresholdInMSec="8000" minCongestionWindowSize="64" enabled="true" />'로 변경 합니다.
4.  파일을 저장한 후 닫습니다.
5.  ' Net stop adfssrv ' 및 ' net start adfssrv '를 실행 하 여 AD FS 서비스를 다시 시작 합니다.
참조용으로이 기능에 대 한 지침은 [여기](https://msdn.microsoft.com/library/azure/dn528859.aspx )에서 찾을 수 있습니다.

### <a name="standard-http-request-checks-at-the-proxy"></a>프록시에서 표준 HTTP 요청 검사
또한 프록시는 모든 트래픽에 대해 다음과 같은 표준 검사를 수행 합니다.

- FS는 수명이 짧은 인증서를 통해 AD FS을 인증 합니다.  Dmz 서버 손상이 의심 되는 경우 잠재적으로 손상 된 프록시에서 들어오는 모든 요청을 더 이상 신뢰 하지 않도록 "프록시 트러스트를 해지할" AD FS 수 있습니다. 프록시 트러스트를 취소 하면 AD FS 서버에 대 한 모든 용도에 대 한 인증을 성공적으로 수행할 수 없도록 각 프록시의 자체 인증서를 해지 합니다.
- FS-P는 모든 연결을 종료 하 고 내부 네트워크의 AD FS 서비스에 대 한 새 HTTP 연결을 만듭니다. 이는 외부 장치와 AD FS 서비스 간의 세션 수준 버퍼를 제공 합니다. 외부 장치는 AD FS 서비스에 직접 연결 되지 않습니다.
- FS-P는 AD FS 서비스에 필요 하지 않은 HTTP 헤더를 특별히 필터링 하는 HTTP 요청 유효성 검사를 수행 합니다.

## <a name="recommended-security-configurations"></a>권장 보안 구성
모든 AD FS 및 WAP 서버가 최신 업데이트를 수신 하는지 확인 AD FS 인프라의 가장 중요 한 보안 권장 사항은 모든 보안 업데이트와 함께 AD FS 및 WAP 서버를 최신 상태로 유지 하 고 해당 옵션을 선택 하는 것이 좋습니다. 이 페이지의 AD FS에 대 한 업데이트를 중요 한 것으로 지정 합니다.

Azure AD 고객이 인프라를 모니터링 하 고 최신 상태로 유지 하는 데 권장 되는 방법은 Azure AD Premium의 기능인 AD FS에 대 한 Azure AD Connect Health를 통하는 것입니다.  Azure AD Connect Health에는 AD FS 또는 WAP 컴퓨터에 AD FS 및 WAP 전용 중요 업데이트 중 하나가 없는 경우 트리거되는 모니터 및 경고가 포함 되어 있습니다.

AD FS에 대 한 Azure AD Connect Health 설치에 대 한 정보는 [여기](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-health-agent-install/)를 참조 하세요.

## <a name="additional-security-configurations"></a>추가 보안 구성
다음 추가 기능을 선택적으로 구성 하 여 기본 배포에서 제공 되는 추가 기능에 대 한 추가 보호를 제공할 수 있습니다.

### <a name="extranet-soft-lockout-protection-for-accounts"></a>계정에 대 한 엑스트라넷 "소프트" 잠금 보호
Windows Server 2012 r 2에서 엑스트라넷 잠금 기능을 사용 하면 AD FS 관리자는 허용 되는 최대 인증 요청 수 (ExtranetLockoutThreshold) 및 ' 관찰 기간의 ExtranetObservationWindow (기간)를 설정할 수 있습니다. 인증 요청의이 최대 수 (ExtranetLockoutThreshold)에 도달 하면 AD FS는 ExtranetObservationWindow (설정 된 기간)에 대해 제공 된 계정 자격 증명을 AD FS에 대 한 인증 시도를 중지 합니다. 이 작업은 AD 계정 잠금에서이 계정을 보호 합니다. 즉,이 계정은 사용자 인증을 위해 AD FS를 사용 하는 회사 리소스에 대 한 액세스 권한을 잃지 않도록 보호 합니다. 이러한 설정은 AD FS 서비스가 인증할 수 있는 모든 도메인에 적용 됩니다.

다음 Windows PowerShell 명령을 사용 하 여 AD FS 엑스트라넷 잠금 (예)을 설정할 수 있습니다. 

    PS:\>Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow ( new-timespan -Minutes 30 )

이 기능에 대 한 공개 설명서는 [여기](https://technet.microsoft.com/library/dn486806.aspx )에 있습니다. 

### <a name="disable-ws-trust-windows-endpoints-on-the-proxy-ie-from-extranet"></a>프록시 (예: 엑스트라넷)에서 WS-TRUST Windows 끝점 사용 안 함

WS-TRUST Windows 끝점 ( */adfs/services/trust/2005/windowstransport* 및 */ADFS/SERVICES/TRUST/13/WINDOWSTRANSPORT*)은 HTTPS에서 WIA 바인딩을 사용 하는 인트라넷 연결 끝점 으로만 사용 됩니다. 이러한 끝점에 대 한 요청이 이러한 끝점에 대 한 요청을 허용 하 여 잠금 보호를 우회할 수 있습니다. 다음 PowerShell 명령을 사용 하 여 AD 계정 잠금을 보호 하기 위해 프록시 (예: 엑스트라넷에서 사용 안 함)에서 이러한 끝점을 사용 하지 않도록 설정 해야 합니다. 프록시에서 이러한 끝점을 사용 하지 않도록 설정 하면 알려진 최종 사용자에 게 영향을 주지 않습니다.

    PS:\>Set-AdfsEndpoint -TargetAddressPath /adfs/services/trust/2005/windowstransport -Proxy $false
    PS:\>Set-AdfsEndpoint -TargetAddressPath /adfs/services/trust/13/windowstransport -Proxy $false
    
### <a name="differentiate-access-policies-for-intranet-and-extranet-access"></a>인트라넷 및 엑스트라넷 액세스에 대 한 액세스 정책 구분
AD FS에는 프록시를 통해 인터넷에서 들어오는 로컬, 회사 네트워크 및 요청에서 발생 하는 요청에 대 한 액세스 정책을 구별할 수 있는 기능이 있습니다.  이러한 작업은 응용 프로그램 별로 또는 전체적으로 수행할 수 있습니다.  중요 하거나 개인적으로 식별이 가능한 정보가 포함 된 비즈니스 가치 응용 프로그램 또는 응용 프로그램의 경우 multi-factor authentication을 요구 하는 것이 좋습니다.  AD FS 관리 스냅인을 통해이 작업을 수행할 수 있습니다.  

### <a name="require-multi-factor-authentication-mfa"></a>MFA (Multi-factor authentication) 필요
프록시, 개별 응용 프로그램 및 Azure AD/Office 365 및 온-프레미스 리소스 모두에 대 한 조건부 액세스를 위해 특히 강력한 인증 (예: multi-factor authentication)을 요구 하도록 구성할 수 있습니다. AD FS  MFA의 지원 되는 방법에는 Microsoft Azure MFA와 타사 공급자가 모두 포함 됩니다.  사용자에 게는 추가 정보 (예: 한 번의 코드를 포함 하는 SMS 텍스트)를 입력 하 라는 메시지가 표시 되 고, AD FS는 공급자 관련 플러그 인과 함께 작동 하 여 액세스를 허용 합니다.  

지원 되는 외부 MFA 공급자에는 [이](https://technet.microsoft.com/library/dn758113.aspx) 페이지에 나열 된 것과 Hdi Global이 포함 됩니다.

### <a name="hardware-security-module-hsm"></a>HSM(하드웨어 보안 모듈)
기본 구성에서 토큰에 서명 하는 데 사용 하 AD FS 키는 페더레이션 서버를 인트라넷에 그대로 두지 않습니다.  DMZ 또는 프록시 컴퓨터에는 표시 되지 않습니다.  필요에 따라 추가 보호를 제공 하기 위해 AD FS에 연결 된 하드웨어 보안 모듈에서 이러한 키를 보호할 수 있습니다.  Microsoft는 HSM 제품을 생성 하지 않지만 AD FS를 지 원하는 시장에는 여러 가지가 있습니다.  이 권장 사항을 구현 하려면 공급 업체 지침에 따라 서명 및 암호화에 대 한 X509 인증서를 만든 다음, 다음과 같이 사용자 지정 인증서를 지정 하 여 AD FS 설치 powershell commandlets을 사용 합니다.

    PS:\>Install-AdfsFarm -CertificateThumbprint <String> -DecryptionCertificateThumbprint <String> -FederationServiceName <String> -ServiceAccountCredential <PSCredential> -SigningCertificateThumbprint <String>

각 항목은 다음을 의미합니다.


- SSL 인증서 `CertificateThumbprint`
- `SigningCertificateThumbprint`는 서명 인증서 (HSM 보호 키 포함)입니다.
- `DecryptionCertificateThumbprint`는 암호화 인증서 (HSM 보호 키 포함)입니다.



