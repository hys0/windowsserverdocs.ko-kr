---
ms.assetid: 39ecc468-77c5-4938-827e-48ce498a25ad
title: "부록 A 검토 광고 FS 요구 사항"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d5cfb5de77843eebfc152b9c79ac55bab1fa7727
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="appendix-a-reviewing-ad-fs-requirements"></a>부록 a: 검토 광고 FS 요구 사항

>적용 대상: Windows Server 2012

조직 파트너 Active Directory Federation Services (ADFS) 배포에 성공적으로 공동 작업할 수 있도록 회사 네트워크 infrastructure ADFS 요구 이름 확인 계정과 인증서에 대 한 지원 하기 위해 구성 되어 있는지 확인 먼저 해야. Adfs는 다음과 같은 유형의 요구 사항은 다음과 같습니다.  
  
> [!TIP]  
> 추가 ADFS 리소스 링크에서 찾을 수는 [광고 FS 콘텐츠 지도](https://social.technet.microsoft.com/wiki/contents/articles/2735.aspx) Microsoft TechNet wiki 페이지 합니다. 이 페이지는 광고 FS 커뮤니티의 회원 하 여 관리 되 고 광고 FS 제품 팀에서를 정기적으로 모니터링 합니다.  
  
## <a name="hardware-requirements"></a>하드웨어 요구 사항  
다음과 같은 최소 및 권장 하드웨어 요구 사항을 federation 서버와 federation 서버 프록시 컴퓨터에 적용 됩니다.  
  
|하드웨어 요구 사항|최소 요구 사항|권장된 요구 사항|  
|------------------------|-----------------------|---------------------------|  
|CPU 속도|단일 코어 1ghz)|4 개의 코어, 2 g h z|  
|RAM|1GB|4GB|  
|디스크 공간|50MB|100 M B|  
  
## <a name="software-requirements"></a>소프트웨어 요구 사항  
ADFS® Windows Server 2012 운영 체제에 내장 된 기능 서버에 의존 합니다.  
  
> [!NOTE]  
> Federation 서비스와 Federation 서비스 프록시 역할 서비스 동일한 컴퓨터에 함께 사용할 수 없습니다.  
  
## <a name="certificate-requirements"></a>인증서 요구 사항  
인증서는 federation 서버, federation 서버 프록시, 인식 클레임 응용 프로그램, 웹 하는 클라이언트와 커뮤니케이션 보호 가장 중요 한 역할을 재생 합니다. 인증서에 대 한 요구 사항 여부를 설정 하는 federation 서버 또는 federation 서버 프록시 컴퓨터가이 섹션에 설명 된 대로 따라 다릅니다.  
  
### <a name="federation-server-certificates"></a>Federation 서버 인증서  
Federation 서버 다음 표에서 인증서 필요합니다.  
  
|인증서 종류|설명|배포 하기 전에 알아야|  
|--------------------|---------------|------------------------------------------|  
|보안 (SSL) Sockets Layer 인증서|하는 클라이언트와 federation 어떻게 커뮤니케이션 보호 하기 위한 사용 되는 표준 소켓 SSL (Secure Layer) 인증서를입니다.|이 인증서를 기본 웹 사이트에서 정보 IIS (인터넷 서비스) Federation 서버 또는 Federation 프록시 서버에 연결 해야 합니다.  Federation 서버 프록시 Federation 프록시 서버 구성 마법사를 성공적으로 실행 하기 전에 구속력 iis에서 구성 합니다.<br /><br />**권장:** 사용 되는 공개 (제 3 자) 인증 기관에서 발급 (캐나다), 예를 들어 VeriSign 서버 인증 인증서가이 인증서 Adfs의 클라이언트 신뢰할 수 있어야 합니다. **팁:** 이 인증서의 제목 이름 배포 하기는 Adfs의 각 인스턴스 Federation 서비스 이름 나타내는 데 사용 됩니다. 이러한 이유로 이름을 회사 또는 조직이 파트너에 게 가장 잘 나타내는 새로운 캘리포니아 발급 된 인증서를 제목 이름 선택 고려해 야 할 수 있습니다.|  
|서비스 통신 인증서|이 인증서 federation 서버 간에 커뮤니케이션 보호 하기 위한 WCF 메시지 보안을 수 있습니다.|기본적으로 ssl 서비스 통신 인증서도 사용 됩니다.  AD FS Management console을 사용 하 여 변경할 수 있습니다.|  
|토큰 서명 인증서|이 표준 X509 모든 토큰 연합 서버 발급을 안전 하 게 로그인 하는 것에 사용 되는 인증서 합니다.|토큰 서명 인증서 개인 키 있어야 하 고 신뢰할 수 있는 루트 Federation 서비스에 연결 해야 합니다. 기본적으로 ADFS 자체 서명된 인증서를 만듭니다. 그러나 변경할 수 있습니다이 나중에 캐나다 발급 된 인증서를 AD FS 관리 스냅인 조직의 요구에 따라 사용 하 여.|  
|토큰 암호 해독 인증서|파트너 federation 서버의 암호화 된 모든 들어오는 토큰 암호를 해독 하는 데 사용 되는 표준 SSL 인증서입니다. 또한 federation 메타 데이터에 게시 됩니다.|기본적으로 ADFS 자체 서명된 인증서를 만듭니다. 그러나 변경할 수 있습니다이 나중에 캐나다 발급 된 인증서를 AD FS 관리 스냅인 조직의 요구에 따라 사용 하 여.|  
  
> [!CAUTION]  
> 토큰 서명 하 고 토큰 해독에 사용 되는 인증서를 중요 하며, Federation 서비스의 안정성을 개선 합니다. 손실이 나이 위해 구성 된 인증서를 예상치 못한 제거 서비스가 중단 될 수 있습니다을 하기 때문에이 위해 구성 된 인증서를 백업 해야 합니다.  
  
Federation 서버를 사용 하는 인증서에 대 한 자세한 내용은 참조 [Federation 서버의 인증서 요구](Certificate-Requirements-for-Federation-Servers.md)합니다.  
  
### <a name="federation-server-proxy-certificates"></a>Federation 서버 프록시 인증서  
Federation 서버 프록시 다음 표에 인증서가 필요 합니다.  
  
|인증서 종류|설명|배포 하기 전에 알아야|  
|--------------------|---------------|------------------------------------------|  
|서버 인증 인증서가|Federation 서버 프록시와 인터넷 클라이언트 간 통신 컴퓨터 보안에 사용 되는 표준 소켓 SSL (Secure Layer) 인증서를입니다.|AD Federation 서버 FS 프록시 구성을 마법사를 성공적으로 실행 하기 전에이 인증서를 기본 웹 사이트에서 정보 IIS (인터넷 서비스)을 연결 해야 합니다.<br /><br />**권장:** 사용 되는 공개 (제 3 자) 인증 기관에서 발급 (캐나다), 예를 들어 VeriSign 서버 인증 인증서가이 인증서 Adfs의 클라이언트 신뢰할 수 있어야 합니다.<br /><br />**팁:** 이 인증서의 제목 이름 배포 하기는 Adfs의 각 인스턴스 Federation 서비스 이름 나타내는 데 사용 됩니다. 이러한 이유로 이름을 회사 또는 조직이 파트너에 게 가장 잘 나타내는 주체 이름을 선택 고려해 야 할 수 있습니다.|  
  
Federation 서버 프록시 사용 하는 인증서에 대 한 자세한 내용은 참조 [인증서 요구 사항에 대 한 Federation 서버 프록시](Certificate-Requirements-for-Federation-Server-Proxies.md)합니다.  
  
## <a name="browser-requirements"></a>브라우저 요구 사항  
ADFS 클라이언트도 작동 하도록에서 JavaScript 기능이 있는 현재 웹 브라우저를 만들 수 있지만 기본적으로 제공 되는 웹 페이지 7.0, 8.0과 9.0, Mozilla Firefox 3.0 및 Safari 3.1 Windows에서 Internet Explorer 버전에 대해서만 거친 합니다. JavaScript을 사용할 수 있어야 하 고 쿠키 브라우저 기반 로그인에 사용할 수 있으며 제대로 작동 하려면 로그 아웃 해야 합니다.  
  
성공적으로 Microsoft의 ADFS 제품 팀 다음 표에서 운영 체제 및 브라우저 구성을 테스트합니다.  
  
|브라우저|Windows 7|Windows Vista|  
|-----------|-------------|-----------------|  
|Internet Explorer 7.0|X|X|  
|Internet Explorer 8.0|X|X|  
|Internet Explorer 9.0|X|테스트는 수행 되지|  
|FireFox 3.0|X|X|  
|Safari 3.1|X|X|  
  
> [!NOTE]  
> Adfs의 위의 표에 보여 주는 모든 브라우저에서 32 비트 및 64 비트 버전을 지원 합니다.  
  
### <a name="cookies"></a>쿠키  
ADFS 로그인, 로그 아웃, single sign-on (SSO) 및 기타 기능을 제공 하는 클라이언트에서 저장 해야 하는 쿠키 및 영구 세션 기반 만듭니다. 따라서 클라이언트 브라우저에서 쿠키를 허용 하도록 설정 해야 합니다. 인증에 사용 되는 쿠키는 항상 보안 하이퍼텍스트 전송 Protocol (HTTPS) 세션 하는 쿠키는 원래 서버에 기록 됩니다. 이러한 쿠키를 허용 하도록 클라이언트 브라우저 구성 되지 않았습니다를 ADFS 올바르게 작동할 수 없습니다. 영구 쿠키 사용자 클레임 공급자의 선택을 유지 하는 데 사용 합니다. 이러한 구성 설정을 ADFS 로그인 페이지에 대 한 구성 파일을 사용 하 여 비활성화할 수 있습니다.  
  
TLS/SSL에 대 한 지원이 보안상의 이유로 필요 합니다.  
  
## <a name="network-requirements"></a>네트워크 요구 사항  
다음 네트워크 서비스를 적절 하 게 구성이 성공적인 ADFS 조직에서 배포에 대 한 중요 합니다.  
  
### <a name="tcpip-network-connectivity"></a>TCP/IP 네트워크에 연결  
Adfs 기능을 클라이언트; 간에 TCP/IP 네트워크 연결이 있어야 도메인 컨트롤러; 그리고 Federation 서비스, (하는 경우) Federation 서비스 프록시 및 ADFS 웹 에이전트 호스트 하는 컴퓨터 합니다.  
  
### <a name="dns"></a>DNS  
ADFS 이외의 Active Directory 도메인 서비스 (AD DS) 작업 중요 하며 기본 네트워크 서비스 시스템 DNS (도메인 이름)은 합니다. DNS 배포 되는 경우 사용자 컴퓨터 및 기타 리소스에 IP 네트워크에 연결 하려면 기억 하기 쉬운는 친절 한 컴퓨터 이름을 사용할 수 있습니다.  
  
 Windows Server 2008 DNS 요구 사항 기반 네트워크에 사용 된 Windows 이름 WINS (인터넷 서비스) NetBIOS 이름 확인 하는 대신 이름 확인을 위해 사용 합니다. WINS 해야 하는 응용 프로그램에 대 한 사용 수는 있습니다. 그러나 광고 DS 및 ADFS DNS 이름 확인을 요구 합니다.  
  
ADFS 지원 하기 위해 DNS 구성 프로세스 여부에 따라 달라 집니다.  
  
-   조직에는 기존 DNS 인프라가 있는 합니다. 가장 시나리오에서 DNS 이미 구성 네트워크를 통해 웹 브라우저 클라이언트 회사 네트워크에 인터넷에 액세스할 수 있습니다. 인터넷 액세스 하 고 이름을 확인 Adfs의 요구 사항, 때문에이 인프라 ADFS 배포에 대 한 것으로 간주 됩니다.  
  
-   회사 네트워크에 연결 된 서버 추가 하려고 합니다. 회사 네트워크에서 사용자를 인증을 위해 Federation 서비스를 실행 하는 내부 서버 CNAME 돌아가려면 회사 네트워크 숲 속의 내부 DNS 서버를 구성 합니다. 자세한 내용은 참조 [이름을 확인 요구 사항을 Federation 서버에 대 한](Name-Resolution-Requirements-for-Federation-Servers.md)합니다.  
  
-   주변 네트워크에 연결 된 서버 프록시 추가 하려고 합니다. 신원 파트너 회사의 회사 네트워크에 있는 사용자 계정 인증 하려는 경우 내부 federation 서버 프록시 CNAME을 반환 하 여 회사 네트워크 숲 속의 내부 DNS 서버를 구성 합니다. DNS 서버 프록시 federation 추가 지원를 구성 하는 방법에 대 한 내용은 [이름 해상도 요구 사항을 Federation 서버 프록시](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)합니다.  
  
-   DNS를 테스트 랩 환경에 대 한 설정 됩니다. 없이 단일 루트 DNS 서버를 신뢰할 수 있는 ADFS 테스트 랩 환경에서 사용 하려는 경우이 상태일 쿼리 두 개 이상의 숲 간의 이름을 적절 하 게 전달 됩니다 되도록 DNS 전달자를 설정 해야 합니다. ADFS 테스트 랩 환경을 설정 하는 방법에 대 한 일반 정보를 참조 하세요. [ADFS 단계별 및 가이드에 어떻게](https://go.microsoft.com/fwlink/?LinkId=180357)합니다.  
  
## <a name="attribute-store-requirements"></a>특성 스토어 요구 사항  
Adfs는 사용자가 인증 하 고 사용자에 대해 보안 클레임 압축에 사용 되는 하나 이상의 특성 스토어가 필요 합니다. 특성 목록이 ADFS 지원 저장, 참조 [The 역할의 특성을 저장](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md) AD FS 디자인 가이드에 있습니다.  
  
> [!NOTE]  
> Adfs는 기본적으로 된 Active Directory 특성 저장소를 자동으로 만들어집니다.  
  
특성 스토어 요구 사항을 조직 (호스트 연결 된 사용자가) 계정 파트너 또는 (호스트 연결 된 응용 프로그램) 리소스 파트너로 작동 하는 있는지 여부에 따라 다릅니다.  
  
### <a name="ad-ds"></a>광고 DS  
Adfs 성공적으로 작동 하도록 Windows Server 2003 SP1, Windows Server 2003 R2, Windows Server 2008 또는 Windows Server 2012에서 계정 파트너 회사나 리소스 파트너 조직 도메인 컨트롤러를 실행 합니다.  
  
ADFS 설치 되 고 도메인에 가입 하는 컴퓨터에서 구성, 해당 도메인에 대 한 Active Directory 사용자 계정의 스토어 사용할 수를 선택할 수 있는 특성 저장소로 합니다.  
  
> [!IMPORTANT]  
> Adfs의 정보 IIS (인터넷 서비스) 설치 하므로 보안상의 이유로 생산 환경에서 도메인 컨트롤러에서 ADFS 소프트웨어를 설치 하지는 것이 좋습니다. 그러나이 구성 Microsoft 고객 서비스 지원에서 지원 됩니다.  
  
#### <a name="schema-requirements"></a>스키마 요구 사항  
Adfs는 스키마 변경 또는 광고 DS 기능 수준 개조 필요 하지 않습니다.  
  
#### <a name="functional-level-requirements"></a>기능 수준 요구 사항  
대부분의 ADFS 기능이 제대로 작동 하려면 광고 DS 기능 수준 수정 필요 하지 않습니다. 그러나 Windows Server 2008 도메인 기능 이상 수준가 필요 클라이언트 인증서 인증 인증서가 명시적으로 AD DS에는 사용자의 계정을에 매핑됩니다 경우 성공적으로 작동 하도록 합니다.  
  
#### <a name="service-account-requirements"></a>서비스 계정 요구 사항  
Federation 서버 팜 만드는 경우 전용된 도메인 기반 서비스 계정을 Federation 서비스에서 사용할 수 있는 AD ds 만들어야 합니다. 나중에이 계정을 사용 하 여 팜에서 각 federation 서버를 구성 합니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 [수동으로 서비스 계정을 Federation 서버 팜에 대 한 구성](../../ad-fs/deployment/Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md) AD FS 배포 가이드에 있습니다.  
  
### <a name="ldap"></a>LDAP  
다른 특성 경량 디렉터리 Access Protocol LDAP 기반 저장소와 함께 작업 하는 경우를 지 원하는 Windows 통합 인증 LDAP 서버에 연결 해야 합니다. LDAP 연결 문자열 RFC 2255에 설명 된 대로 LDAP URL을 형식으로 작성도 합니다.  
  
### <a name="sql-server"></a>SQL Server  
ADFS 성공적으로 작동 하도록에 대 한 Microsoft SQL Server 2005 또는 SQL Server 2008 구조적 쿼리 SQL (언어) 서버 특성 저장소 호스트 하는 컴퓨터 실행 해야 합니다. 특성 SQL 기반 저장소와 함께 작업 하는 경우 연결 문자열 또한 구성 해야 합니다.  
  
### <a name="custom-attribute-stores"></a>사용자 지정 된 특성 스토어  
사용자 지정 된 특성 스토어 고급 시나리오를 개발할 수 있습니다. Adfs에 기본 제공 되는 정책 언어를 다음 중 하나를 향상 시킬 수 있습니다 특성 사용자 지정 상점 참조할 수 있습니다.  
  
-   로컬 인증된 사용자에 대 한 주장 만들기  
  
-   보충 외부적으로 인증된 된 사용자에 대 한 주장  
  
-   사용자가 토큰을 가져올 수 승인  
  
-   서비스는 사용자의 동작에 토큰 얻는 승인  
  
사용자 지정 된 특성 저장소와 함께 작업 하는 경우 연결 문자열 구성 해야 수 있습니다. 이 경우 사용자 지정 된 특성 스토어에 대 한 연결을 사용 하는 사용자가 좋아할 사용자 지정 코드를 입력할 수 있습니다. 이 경우에는 연결 문자열 사용자 지정 된 특성 스토어 개발자가 구현으로 해석 하는 이름 값/쌍 집합입니다.  
  
개발 하 고 사용 하 여 사용자 지정 된 특성 스토어에 대 한 자세한 내용은 참조 [특성 스토어 개요](https://go.microsoft.com/fwlink/?LinkId=190782)합니다.  
  
## <a name="application-requirements"></a>응용 프로그램 요구 사항  
Federation 서버 인식 클레임 응용 프로그램 등의 federation 응용 프로그램 보호와 통신할 수 있습니다.  
  
## <a name="authentication-requirements"></a>인증 요구 사항  
ADFS 통합 된 기존 Windows 인증 자연스럽 게 예를 들어, Kerberos 인증과 NTLM, 스마트 카드 X.509 v3 클라이언트 측 인증서 합니다. Federation 서버 표준 Kerberos 인증을 사용 하 여 도메인에 대 한 사용자의 신원을 확인 합니다. 인증, 스마트 카드 인증 인증 구성 하는 방법에 따라 Windows 통합 인증을 사용 하 여 클라이언트 인증할 수 있습니다.  
  
ADFS federation 서버 프록시 역할은 사용자 SSL 클라이언트 인증을 사용 하 여 외부에서 인증 하는 경우 가능 합니다. SSL 클라이언트 인증을 요구 하도록 federation 서버 역할을 구성할 수도, 일반적으로 가장 원활 하 게 사용자 환경을 있지만 Windows 통합 인증을 위해 계정 federation 서버 구성 하 여 수행 됩니다. 이 경우 ADFS 제어할 수 없거나 Windows 데스크톱 로그온에 대 한 사용 하는 어떤 자격 증명에 있습니다.  
  
### <a name="smart-card-logon"></a>스마트 카드 로그온  
ADFS (암호, SSL 클라이언트 인증 또는 인증 Windows 통합)를 인증에 사용 하 여 자격 증명 입력을 적용 수 있지만 직접을 적용 하지 않습니다 스마트 카드로 인증 합니다. 따라서 ADFS 개인 식별 스마트 카드 번호 (PIN) 자격 증명을 가져올는 클라이언트 쪽 UI (사용자 인터페이스)를 제공 하지 않습니다. Windows 기반 클라이언트 federation 또는 웹 서버에 사용자 자격 증명 세부 정보를 의도적으로 제공 하지 않는 하기 때문입니다.  
  
### <a name="smart-card-authentication"></a>스마트 카드 인증  
스마트 카드 인증 Kerberos 프로토콜 계정 federation 서버 인증을 사용 합니다. ADFS 새 인증 방법을 추가 하려면 확장할 수 없습니다. 스마트 카드에 인증서 체인 클라이언트 컴퓨터에서 신뢰할 수 있는 루트 최대 필요 하지 않습니다. 스마트 카드 기반 ADFS 된 인증서를 사용 하는 다음과 같은 필요합니다.  
  
-   브라우저를 컴퓨터에 판독기 및 암호화 CSP (서비스 공급자) 스마트 카드에 대 한 작업 해야 합니다.  
  
-   스마트 카드 인증서 신뢰할 수 있는 루트 계정 federation 서버 프록시와 계정 federation 서버에 연결 해야 합니다.  
  
-   인증서 AD ds에서 사용자 계정에 다음 방법 중 하나 하 여 지도 해야 합니다.  
  
    -   인증서 제목 LDAP 고유 광고 DS의 사용자 계정 이름으로 해당합니다.  
  
    -   인증서 주제 altname 확장 (UPN) 사용자 계정 이름 AD ds에서 사용자 계정에 있습니다.  
  
특정 인증 강도 요구 일부 시나리오에서를 지원 하기 위해 사용자가 인증 어떻게 나타내는 클레임 만드는 ADFS 구성할 수 이기도 합니다. 신뢰가이 클레임 사용 하 여 인증 방법을 결정할 수 있습니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
