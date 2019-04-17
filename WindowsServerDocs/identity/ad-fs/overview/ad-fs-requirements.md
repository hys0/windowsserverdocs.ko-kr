---
ms.assetid: 28f4a518-1341-4a10-8a4e-5f84625b314b
title: "광고 FS 2016 요구 사항"
description: "Active Directory Federation Services 설치 하기 위한 요구 합니다."
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/06/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 81b51c751d5f54436b14450ef21bf49feb864290
ms.sourcegitcommit: 556361fe7c73c75d6cdc46a67dc88679fbe89c61
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="ad-fs-requirements"></a>광고 FS 요구 사항

>Windows Server 2016 적용 됩니다.

ADFS 배포를 위해 요구 사항은 다음과 같습니다.  
  
-   [인증서 요구 사항](ad-fs-requirements.md#BKMK_1)  
  
-   [하드웨어 요구 사항](ad-fs-requirements.md#BKMK_2)  
  
-   [프록시 요구 사항](ad-fs-requirements.md#BKMK_3)  
  
-   [광고 DS 요구 사항](ad-fs-requirements.md#BKMK_4)  
  
-   [구성 데이터베이스 요구 사항](ad-fs-requirements.md#BKMK_5)  
  
-   [브라우저 요구 사항](ad-fs-requirements.md#BKMK_6)  

-   [네트워크 요구 사항](ad-fs-requirements.md#BKMK_7)  
  
-   [사용 권한 요구 사항](ad-fs-requirements.md#BKMK_13)  
  
## <a name="BKMK_1"></a>인증서 요구 사항  
  
### <a name="ssl-certificates"></a>SSL 인증서

각 ADFS 및 웹 응용 프로그램 프록시 서버에 요청을 처리 하 HTTPS federation 서비스 SSL 인증서가 합니다.  웹 응용 프로그램 프록시 게시 된 응용 프로그램에 대 한 서비스 요청 하려면 추가 SSL 인증서 있을 수 있습니다.

**권장:** SSL 여 동일한 인증서를 사용 하 여 모든 ADFS federation 서버와 프록시 웹 응용 프로그램에 대 한 합니다. 

**요구 사항:**

Federation 서버의 인증서 SSL 다음 조건을 충족 해야
- 인증서가 (프로덕션 배포용) 공개적으로 신뢰할 수 있는
- 인증서에 값 서버 인증 향상 키 EKU)
- 인증서에 federation 서비스 이름 제목 또는 주체 대신 이름 (산)에서 "fs.contoso.com" 등
- 인증서에 "certauth. \ < federation 서비스 name\ >", "certauth.fs.contoso.com"는 산에 등 사용자 포트 443 인증서 인증을 위해
- 디바이스 등록 하거나 이전 Windows 10 클라이언트를 사용 하 여 프레미스 리소스를 최신 인증을 위해 "enterpriseregistration. \ < upn suffix\ >" 각 upn 사용에서에 대 한 조직에는 산 있어야 합니다.

웹 응용 프로그램 프록시에서 SSL 인증서 다음 조건을 충족 해야
- 프록시 하는 데 사용 되는 경우 Windows 통합 인증을 프록시 SSL 인증서를 사용 하는 프록시 ADFS 요청 동일 해야 (같은 키를 사용 하 여) federation 서버 SSL 인증서로
- 프록시 SSL 인증서 (같은 키를 사용 하 여)와 동일 federation 서버 SSL 인증서 해야 ADFS 속성 "ExtendedProtectionTokenCheck" (기본 adfs에서 설정)를 사용 하도록 설정 하는 경우
- 그렇지 않은 경우에 대 한 프록시 SSL 인증서의 요구와 동일 해당 federation 서버 SSL 인증서에 대 한

### <a name="service-communication-certificate"></a>서비스 통신 인증서
이 인증서가 대부분 ADFS 시나리오를 포함 하 여 Azure AD에 필요한 및 Office 365 합니다. 기본적으로 ADFS 구성 ssl 서비스 통신 인증서도 초기 구성으로 제공 됩니다.

**권장 사항:**
- Ssl 사용 하 여 동일한 인증서를 사용 합니다.  

### <a name="token-signing-certificate"></a>토큰 서명 인증서
이 인증서 신뢰 당사자에 사용 되는 기호 발급 토큰 이므로 신뢰 하는 자사 응용 프로그램과 해야 인증서를 인식 하 고 신뢰할 수 있는 한 알려진 키 연결 되어 있습니다. 토큰 서명 인증서 변경 내용을 등 만료 되기 하면 새 인증서를 구성 신뢰 당사자 모두 업데이트 해야 합니다.

**권장:** 생성 내부적으로 ADFS 기본, 서명한 토큰 서명 인증서를 사용 합니다.  

**요구 사항:**
- 토큰 서명 인증서 PKI 기업에서 사용할 수 해야 하는 경우 이렇게 Install-AdfsFarm cmdlet의 SigningCertificateThumbprint 매개 변수를 사용 합니다.
- 새 인증서 정보로 업데이트는 모든 신뢰 당사자 기본 내부에서 생성 된 인증서를 사용 하 여 외부적으로 등록 된 인증서를 토큰 서명 인증서 하면 변경 될 때 또는 여부를 확인 해야 합니다.  그렇지 않은 경우 업데이트 되지 모든 신뢰 당사자에 대 한 로그온 실패 합니다.

### <a name="token-encryptingdecrypting-certificate"></a>토큰 해독 암호화 인증서
청구 공급자에 게 Adfs에 발급 토큰 암호화 하 여이 인증서를 사용 합니다.

**권장:** 인증서의 암호를 해독 서명한 토큰, 생성 내부적으로 ADFS 기본 사용 합니다.  

**요구 사항:**
- 토큰 서명 인증서 PKI 기업에서 사용할 수 해야 하는 경우 이렇게 Install-AdfsFarm cmdlet의 DecryptingCertificateThumbprint 매개 변수를 사용 합니다.
- 기본 내부에서 생성 된 인증서를 사용 하는지 여부를 또는 외부에서 사용자의 암호를 해독 인증서 토큰 변경 될 때 인증서를 등록 한 모든 클레임 공급자는 새 인증서 정보로 업데이트 확인 해야 합니다.  그렇지 않은 경우 업데이트 되지 공급자 주장 하나를 사용 하 여 로그온 실패 합니다.
  
> [!CAUTION]  
> Token\ 서명 및 decrypting\/암호화 token\에 사용 되는 인증서를 중요 하며, Federation 서비스의 안정성을 개선 합니다. 자신의 token\ 서명 및 token\ decrypting\/암호화 인증서를 관리 하는 고객은 이러한 인증서를 백업 하 고 사용할 수 없는 독립적으로 이벤트를 복구 하는 동안 확인 해야 합니다.  

### <a name="user-certificates"></a>사용자 인증서
- Adfs의 모든 사용자 인증서 통해 사용자 인증서를 인증 ADFS 및 웹 응용 프로그램 프록시 서버에서 신뢰할 수 있는 인증 기관을에 연결 해야 x509 사용 하는 경우.

## <a name="BKMK_2"></a>하드웨어 요구 사항  
ADFS 및 웹 응용 프로그램 프록시 하드웨어 요구 사항은 물리적 또는 가상 용량을 처리 하기 위한 사용자 농장 크기 조정 해야 하기 때문 CPU에서 제어 됩니다.  
- 사용 하는 [ADFS 2016 용량이 계획 스프레드시트](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx) 필요한 ADFS 및 웹 응용 프로그램 프록시 서버의 번호를 확인 합니다.

Adfs의 메모리 및 디스크 요구 사항은 매우 고정, 아래 표 참조:


|**하드웨어 요구 사항**|**최소 요구 사항**|**권장된 요구 사항**|
|----- | ----- |-----|
|RAM|2GB|4GB |
|디스크 공간|32GB|100 G B |

**SQL Server 하드웨어 요구 사항**

SQL Server ADFS 구성 데이터베이스를 사용 하는 경우에 따라 가장 기본적인 SQL Server 추천 SQL Server 크기 조정 합니다.  ADFS 데이터베이스 크기가 매우 적은 고 ADFS 데이터베이스 인스턴스에 중요 한 처리량 저장 하지 않습니다.  그러나 ADFS 하는 연결 데이터베이스에 여러 번은 인증 하는 동안 네트워크 연결 강력한 있어야 합니다.  그러나 유감 SQL Azure ADFS 구성 데이터베이스에 대 한 지원 되지 않습니다.
  
## <a name="BKMK_3"></a>프록시 요구 사항  
  
-   엑스트라넷 액세스를 위해 웹 응용 프로그램 프록시 역할 서비스 배포 해야 \-원격 액세스 거부 그렇습니다. 

-   제 3 자 프록시 지원 해야는 [MS ADFSPIP 프로토콜](https://msdn.microsoft.com/en-us/library/dn392811.aspx) ADFS 프록시도 지원 합니다.  공급 업체 타사 목록에 대 한 참조는 [FAQ](AD-FS-FAQ.md#what-third-party-proxies-are-available-for-ad-fs-that-support-ms-adfspip)합니다.

-   광고 FS 2016 Windows Server 2016에 웹 응용 프로그램 프록시 서버 필요합니다.  하위 프록시 2016 농장 동작 수준에서 실행 되는 광고 FS 2016 농장 구성할 수 없습니다.
  
-   Federation 서버와 웹 응용 프로그램 프록시 역할 서비스 동일한 컴퓨터에 설치할 수 없습니다.  
  
## <a name="BKMK_4"></a>광고 DS 요구 사항  
**도메인 컨트롤러 요구 사항**  
  
- Adfs는 도메인 컨트롤러 Windows Server 2008 이상을 실행 해야 합니다.

- 하나 이상의 Windows Server 2016 도메인 컨트롤러 작업에 대 한 Microsoft Passport 필요 합니다.
  
> [!NOTE]  
> Windows Server 2003 도메인 컨트롤러 관련 환경에 대 한 지원 종료 되었습니다. 방문 [이 페이지](https://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=Windows+Server+2003&Filter=FilterNO) 에 대 한 자세한 내용은 Microsoft 지원 수명 주기 합니다.  
  
**도메인 functional\ 수준 요구 사항**  
  
 - Windows Server 2003 이상 도메인 기능 수준에서 모든 사용자 계정 도메인 및 ADFS 서버 가입 된 도메인 작업 해야 합니다.  
  
 - Windows Server 2008 도메인 기능 이상 수준 경우 필요한 클라이언트 인증서를 인증 인증서가 명시적으로 AD DS에서 사용자의 계정에 매핑됩니다.  
  
**스키마 요구 사항**  
  
-   광고 FS 2016의 새로운 설치 Active Directory 2016 스키마 (최소 버전 85) 필요합니다.

-   ADFS 농장 동작 수준 (FBL) 2016 수준으로 올리기 Active Directory 2016 스키마 (최소 버전 85) 해야 합니다.  

  
**서비스 계정 요구 사항**  
  
-   표준 도메인 계정은 adfs 서비스 계정으로 사용할 수 있습니다. 그룹 관리 서비스 계정도 지원 됩니다. ADFS 구성 런타임에서 요구 하는 권한은 자동으로 추가 됩니다.

-   그룹 관리 서비스 계정 Windows Server 2012 이상 실행 하는 하나 이상의 도메인 컨트롤러가 필요 합니다.  기본 아래에서 GMSA 라이브 해야 ' CN 관리 서비스 계정의 컨테이너 = 합니다.  

-   서비스 사용자 이름 Kerberos 인증용 '`HOST/<adfs\_service\_name>`' ADFS 서비스 계정에 등록 해야 합니다. 기본적으로 Adfs은 구성이 새로운 ADFS 그룹을 만들 때 합니다.  이 오류가 발생 하면와 같은 충돌이 나 권한이 경우 경고 항목이 표시 되며 수동으로 추가 해야 합니다.  
   
**도메인 요구 사항**  
  
-   모든 ADFS 서버 AD DS 도메인에 가입 이어야 합니다.  
  
-   동일한 도메인에 있는 모든 ADFS 서버 농장 내에서 배포 되어야 합니다.  
   
**다중 숲 요구 사항**  
  
-   ADFS 서버 가입 된 도메인 모든 도메인 또는 인증 ADFS 서비스에 사용자가 포함 된 숲 신뢰 해야 합니다.  

-   ADFS 서비스 계정의 회원 있는 숲 모든 사용자의 로그인 숲 신뢰 해야 합니다. 
  
-   ADFS 서비스 계정 ADFS 서비스에 사용자가 인증 포함 된 모든 도메인에 있는 사용자 특성을 읽을 수 있는 권한이 있어야 합니다.  
  
## <a name="BKMK_5"></a>구성 데이터베이스 요구 사항  
이 섹션 요구 사항 및 제한 ADFS 농장으로 사용 하는 각 Windows 내부 데이터베이스 (WID) 또는 SQL Server 데이터베이스에 대해 설명 합니다.  
  
**WID**  
  
-   SAML 2.0 아티팩트 해상도 프로필 WID 그룹에서 지원 되지 않습니다.    

-   토큰 재생 검색 하지는 WID 농장 지원 합니다. (이 기능은 Adfs은 federation 공급자 역할을 하 고 외부 클레임 공급자의 보안 토큰을 사용 하는 경우에만 사용 됩니다.)  
  
다음 표에서 개수 ADFS 서버에 대 한 요약 SQL Server 팜 WID vs에서 지원 됩니다.    
  
  
|| 1-Adfs의 구성 (RP) 파티 신뢰 의존 100 | 100 개 이상의 RP 신뢰 구성  |
| --- |--- | --- |
|AD 1-30 FS 서버|지원 되는 WID|사용 하 여 WID-SQL Server 필요 지원 되지 않습니다 |
|30 AD 이상 FS 서버|사용 하 여 WID-SQL Server 필요 지원 되지 않습니다|사용 하 여 WID-SQL Server 필요 지원 되지 않습니다  
  
**SQL Server**  
  
- Windows Server 2016 ADFS SQL Server 2008 및 높은 버전 지원 됩니다.

- SAML 아티팩트 해상도 및 토큰 재생 검색 SQL Server 팜에서 지원 됩니다.  
  
## <a name="BKMK_6"></a>브라우저 요구 사항  
브라우저나 브라우저 컨트롤을 통해 ADFS 인증을 수행 하세요 브라우저 다음 요구 사항을 준수 해야 합니다.  
  
-   JavaScript은 사용 하도록 설정  
  
-   단일 로그인에 대 한 클라이언트 브라우저에서 쿠키를 허용 하도록 구성 합니다.  
  
-   서버 이름 표시 \(SNI\) 지원 해야  
  
-   사용자 장치 및 인증서 인증서 인증 브라우저 SSL 클라이언트 인증서를 인증을 지원 해야  

-   Windows 통합 인증을 사용 하 여에서 원활 하 게 로그인에 대 한 로컬 인트라넷 영역이 나 신뢰할 수 있는 사이트 영역 federation 서비스 이름 (예: https:\/\/fs.contoso.com)를 구성 합니다.
## <a name="BKMK_7"></a>네트워크 요구 사항  
 
**방화벽 요구 사항**  
  
웹 응용 프로그램 프록시 및 federation 서버 팜은 클라이언트와 웹 응용 프로그램 프록시 방화벽 사이 있는 두 방화벽 TCP 포트 사용 443 있어야 인바인드 합니다.  
  
또한 클라이언트 사용자 인증 인증서 경우 \ (clientTLS 인증 X509를 사용 하 여 사용자 certificates\)가 필요 포트 443 certauth 끝점 사용할 수 없는, 광고 FS 2016 필요 TCP 포트 49443 사용할 수는 클라이언트와 웹 응용 프로그램 프록시 방화벽 인바인드 합니다. 이 필요 하지 않습니다 웹 응용 프로그램 프록시 사이의 federation servers\ 방화벽). 

요구 사항에 대 한 자세한 내용은 하이브리드 포트 표시 [하이브리드 신원을 포트와 프로토콜](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports)합니다. 

자세한 내용은 참조 [모범 사례에 대 한 Active Directory Federation Services 보안](..\deployment\Best-Practices-Securing-AD-FS.md)
  
**DNS 요구 사항**  
  
-   인트라넷 액세스할 수 있도록 내부 회사 네트워크 \(intranet\) 내 ADFS 서비스에 액세스 하는 모든 클라이언트 ADFS 서비스 이름을 부하 분산 ADFS 서버 또는 ADFS 서버를 확인 하려면 수 있어야 합니다.  
  
-   익스트라넷 액세스 회사 네트워크 \(extranet\/internet\) 외부에서 ADFS 서비스에 액세스 하는 모든 클라이언트 ADFS 서비스 이름을 부하 분산 웹 응용 프로그램 프록시 서버 또는 웹 응용 프로그램 프록시 서버에 대 한 해결 있어야 합니다.  
  
-   각 웹 응용 프로그램 프록시 서버에 DMZ ADFS 서비스 이름을 부하 분산 ADFS 서버 또는 ADFS 서버에 대 한 기능을 확인할 수 있어야 합니다. DMZ 네트워크 또는 호스트 파일을 사용 하 여 로컬 서버 해상도 변경 하 여 대체 DNS 서버를 사용 하 여 수행할 수 있습니다.  
  
-   Windows 통합 인증을 위해 해당 federation 서비스 이름을 대 한 A DNS 레코드 \(not CNAME\) 사용 해야 합니다.  

-   포트 443 사용자 인증서 인증, dns 서버 federation 또는 웹 응용 프로그램 프록시 해결 하기 위해 "certauth. \ < federation 서비스 name\ >"을 구성 합니다.

-   디바이스 등록 하거나 이전 Windows 10 클라이언트를 사용 하 여 프레미스 리소스를 최신 인증을 위해 federation 서버 또는 웹 응용 프로그램 프록시 해결 하기 위해 "enterpriseregistration. \ < upn suffix\ >" 각 upn 조직의 사용에서에 대 한 구성 되어야 합니다.

**부하 분산 요구 사항**
- 안 부하 분산 SSL을 종료 합니다. Adfs는 SSL 종료 때의 연결이 끊어집니다 인증 인증서를 여러 사용 하 여 사례를 지원 합니다. 사용 하는 경우에는 SSL 부하 분산 언제 종료 지원 되지 않습니다. 
- 원하는 SNI 부하 분산 기능을 사용 하는 것이 좋습니다. 이벤트에 표시 되지 않는, 0.0.0.0 대체 구속력을 사용 하 여 사용자 Adfs의 / 웹 응용 프로그램 프록시 서버 해결 방법을 제공 합니다.
- (HTTPS) HTTP 건강 검색 끝점 검사를 수행 부하 분산 건강 트래픽을 라우팅하기에 대 한 사용 하는 것이 좋습니다. SNI와 관련 된 문제를 방지할 수 있습니다. 이 검사 끝점에 대 한 응답 HTTP 200 확인 이며 백 엔드 서비스에 대 한 종속성 없는와 로컬로 광고가 합니다. HTTP 검색 HTTP 경로 '/ adfs/검색'을 사용 하 여를 통해 액세스할 수 있습니다.
    - http://&lt;웹 응용 프로그램 프록시 이름&gt;/adfs/검사
    - http://&lt;ADFS 서버 이름&gt;/adfs/검사
    - http://&lt;웹 응용 프로그램 프록시 IP 주소&gt;/adfs/검사
    - http://&lt;ADFS IP 주소&gt;/adfs/검사
- DNS 사용 하는 것이 좋습니다 하지 차례로 잔액을 로드할을 하는 방법입니다. 이러한 유형의 부하 분산를 사용 하 여 자동된으로 노드 부하 분산 건강 검색을 사용 하 여에서 제거 제공 하지 않습니다. 
- 하지 IP 기반 세션 선호도 또는 스티커 세션 인증 교통량 ADFS 부하 분산 이내에 사용 하는 것이 좋습니다. 특정 노드 오버 메일 클라이언트에 대 한 기존 인증 프로토콜을 사용 하 여 Office 365 메일 서비스 (Exchange Online)에 연결할 때 발생할 수 있습니다. 

## <a name="BKMK_13"></a>사용 권한 요구 사항  
Adfs의 초기 구성 하 고 설치를 수행 하는 관리자 ADFS 서버에 로컬 관리자 권한이 있어야 합니다.  도메인 관리자를 먼저 있는 로컬 관리자에 Active directory에서 개체를 만들 수 있는 권한이 없는 경우 필요한 광고 개체 만든 다음 AdminConfiguration 매개 변수를 통해 ADFS 농장 구성 합니다.  
  
  

