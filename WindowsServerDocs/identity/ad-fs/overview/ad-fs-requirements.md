---
ms.assetid: 28f4a518-1341-4a10-8a4e-5f84625b314b
title: AD FS 2016 요구 사항
description: Active Directory Federation Services를 설치 하기 위한 요구 사항입니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/06/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 9a5155dd31b9f8f86fac532aa33cd9f7389d8a48
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815124"
---
# <a name="ad-fs-requirements"></a>AD FS 요구 사항

>적용 대상: Windows Server 2016

다음은 AD FS를 배포 하기 위한 요구 사항:  
  
-   5. 인증서가 RD 게이트웨이에 대한 요구 사항을 충족하면 [설치](ad-fs-requirements.md#BKMK_1)를 클릭합니다.  
  
-   [하드웨어 요구 사항](ad-fs-requirements.md#BKMK_2)  
  
-   [프록시 요구 사항](ad-fs-requirements.md#BKMK_3)  
  
-   [AD DS 요구 사항](ad-fs-requirements.md#BKMK_4)  
  
-   [구성 데이터베이스 요구 사항](ad-fs-requirements.md#BKMK_5)  
  
-   [브라우저 요구 사항](ad-fs-requirements.md#BKMK_6)  

-   [네트워크 요구 사항](ad-fs-requirements.md#BKMK_7)  
  
-   [사용 권한 요구 사항](ad-fs-requirements.md#BKMK_13)  
  
## <a name="BKMK_1"></a>인증서 요구 사항  
  
### <a name="ssl-certificates"></a>SSL 인증서

각 AD FS 및 웹 응용 프로그램 프록시 서버는 페더레이션 서비스에 HTTPS 요청을 서비스에 SSL 인증서를 있습니다.  웹 응용 프로그램 프록시 게시 된 응용 프로그램에 대 한 서비스 요청에 추가 SSL 인증서를 가질 수 있습니다.

**권장 사항:** 모든 AD FS 페더레이션 서버 및 웹 응용 프로그램 프록시에 대 한 동일한 SSL 인증서를 사용 합니다. 

**요구 사항:**

페더레이션 서버에서 SSL 인증서에는 다음 요구 사항을 충족 해야 합니다.
- 인증서 (예: 프로덕션 배포의 경우) 공개적으로 신뢰할 수 있는
- 서버 인증 EKU 향상 키 사용 () 값을 포함 하는 인증서
- 인증서 주체 또는 주체 대체 이름 (SAN)에서 "fs.contoso.com"와 같은 페더레이션 서비스 이름, 포함
- 인증서가 들어 있는 포트 443에서 사용자 인증서 인증을 "certauth.\<페더레이션 서비스 이름\>","certauth.fs.contoso.com"SAN의 예:
- 장치 등록 또는 온-프레미스 리소스 10 이전 windows 클라이언트를 사용 하 여 최신 인증에 대 한 SAN을 포함 해야 "enterpriseregistration.\<upn 접미사\>"에 대해 조직에서 사용 중인 각 UPN 접미사입니다.

웹 응용 프로그램 프록시에 대 한 SSL 인증서는 다음 요구 사항을 충족 해야 합니다.
- 프록시를 사용 하는 경우 Windows 통합 인증을 프록시 SSL 인증서를 사용 하는 AD FS 프록시 요청 동일 해야 (동일한 키를 사용 하 여) 페더레이션 서버 SSL 인증서로
- "ExtendedProtectionTokenCheck"는 AD FS 속성 설정 (기본 AD FS에서 설정), 프록시 SSL 인증서 동일 해야 (동일한 키를 사용 하 여) 페더레이션 서버 SSL 인증서로
- 그렇지 않으면 프록시 SSL 인증서의 요구 사항은 페더레이션 서버 SSL 인증서와 동일

### <a name="service-communication-certificate"></a>서비스 통신 인증서
이 인증서를 Azure AD를 포함 하 여 대부분의 AD FS 시나리오에 필요 없는 및 Office 365입니다. 기본적으로 AD FS 서비스 통신 인증서로 초기 구성 시 제공 된 SSL 인증서를 구성 합니다.

**권장 사항:**
- SSL에 대 한 사용과 같은 인증서를 사용 합니다.  

### <a name="token-signing-certificate"></a>토큰 서명 인증서
이 인증서는 신뢰 당사자 응용 프로그램 인증서를 인식 해야 하 고 키로 알려져 있고 신뢰할 수 있는 연결 된 신뢰 당사자에 발급 된 토큰을 로그인에 사용 됩니다. 토큰 서명 인증서 변경 내용을 만료 될 때 및 사용자와 같은 새 인증서를 구성 하는 경우 모든 신뢰 당사자를 업데이트 해야 합니다.

**권장 사항:** AD FS 기본적으로 내부적으로 생성 된 자체 서명 된 토큰 서명 인증서를 사용 합니다.  

**요구 사항:**
- 조직에서 엔터프라이즈 PKI 인증서를 토큰 서명에 사용할 수는 경우, 이렇게 설치 AdfsFarm cmdlet의 SigningCertificateThumbprint 매개 변수를 사용 합니다.
- 모든 신뢰 당사자는 새 인증서 정보로 업데이트 되며 내부적으로 생성 된 기본 인증서를 사용 하 여 연결 하거나 외부에서 토큰 서명 인증서를 변경 될 때 인증서를 등록 한 있는지 확인 해야 합니다.  그렇지 않은 경우에 업데이트 되지 모든 신뢰 당사자에 대 한 로그온 실패 합니다.

### <a name="token-encryptingdecrypting-certificate"></a>토큰 암호화/암호 해독 인증서
이 인증서는 AD FS에 발급 된 토큰을 암호화 하는 클레임 공급자가 사용 됩니다.

**권장 사항:** AD FS 기본적으로 인증서를 암호 해독 내부적으로 생성 된 자체 서명 된 토큰을 사용 합니다.  

**요구 사항:**
- 조직에서 엔터프라이즈 PKI 인증서를 토큰 서명에 사용할 수는 경우, 이렇게 설치 AdfsFarm cmdlet의 DecryptingCertificateThumbprint 매개 변수를 사용 합니다.
- 내부적으로 생성 된 기본 인증서를 사용 하 여 여부 또는 외부에서 사용자 인증서의 암호를 해독 하는 토큰 변경 될 때 인증서를 등록 한 모든 클레임 공급자는 새 인증서 정보로 업데이트 되며 확인 해야 합니다.  그렇지 않으면 모든 클레임 공급자 업데이트 되지를 사용 하 여 로그온 실패 합니다.
  
> [!CAUTION]  
> 토큰에 사용 되는 인증서\-서명 및 토큰\-해독\/암호화 하는 것은 페더레이션 서비스의 안정성에 중요 합니다. 자신의 토큰을 관리 하는 고객\-서명 및 토큰\-해독\/이러한 인증서는 백업 하 고 사용할 수 없는 독립적으로 복구 이벤트를 사용 하는 동안 확인 해야 인증서를 암호화 합니다.  

### <a name="user-certificates"></a>사용자 인증서
- 사용할 경우 x509 AD FS 모든 사용자 인증서와 사용자 인증서 인증 AD FS 및 웹 응용 프로그램 프록시 서버에서 신뢰할 수 있는 루트 인증 기관에 연결 해야 합니다.

## <a name="BKMK_2"></a>하드웨어 요구 사항  
AD FS 및 웹 응용 프로그램 프록시 하드웨어 요구 사항 (실제 또는 가상) 팜의 처리 용량에 대 한 크기를 지정 해야 하므로 cpu에서 제어 됩니다.  
- 사용 하는 [AD FS 2016의 용량 계획 스프레드시트](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx) 해야 하는 AD FS 및 웹 응용 프로그램 프록시 서버의 수를 결정 합니다.

AD FS에 대 한 메모리 및 디스크 요구 사항은 상당히 정적인 하 고 아래 표를 참조 하십시오.


|**하드웨어 요구 사항**|**최소 요구 사항**|**권장된 요구 사항**|
|----- | ----- |-----|
|RAM|2GB|4GB |
|디스크 공간|32GB|100GB |

**SQL Server에 대 한 하드웨어 요구 사항**

SQL Server AD FS 구성 데이터베이스를 사용 하는 가장 기본적인 SQL Server 권장 사항에 따라 SQL Server의 크기 조정 합니다.  AD FS 데이터베이스 크기는 매우 작은 및 AD FS 데이터베이스 인스턴스에 대 한 중요 한 처리 부하를 넣지 않습니다.  그러나 AD FS, 연결할 데이터베이스 여러 번을 인증 하는 동안 네트워크 연결이 정도로 강력해 야 합니다.  그러나 SQL Azure AD FS 구성 데이터베이스에 대해 지원 되지 않습니다.
  
## <a name="BKMK_3"></a>프록시 요구 사항  
  
-   엑스트라넷 액세스에 대 한 웹 응용 프로그램 프록시 역할 서비스를 배포 해야 \- 원격 액세스 서버 역할의 일부입니다. 

-   제 3 자 프록시를 지원 해야는 [MS ADFSPIP 프로토콜](https://msdn.microsoft.com/en-us/library/dn392811.aspx) AD FS 프록시도 지원 됩니다.  공급 업체 목록을 제 3 자에 대 한 참조를 [FAQ](AD-FS-FAQ.md#what-third-party-proxies-are-available-for-ad-fs-that-support-ms-adfspip)합니다.

-   AD FS 2016에는 Windows Server 2016에서 웹 응용 프로그램 프록시 서버가 필요합니다.  2016 팜 동작 수준에서 실행 하는 AD FS 2016 팜을 대 한 하위 프록시를 구성할 수 없습니다.
  
-   페더레이션 서버 및 웹 응용 프로그램 프록시 역할 서비스를 동일한 컴퓨터에 설치할 수 없습니다.  
  
## <a name="BKMK_4"></a>AD DS 요구 사항  
**도메인 컨트롤러 요구 사항**  
  
- AD FS는 Windows Server 2008 이상을 실행 하는 도메인 컨트롤러가 필요 합니다.

- Windows Server 2016 도메인 컨트롤러가 하나 이상이 작업에 대 한 Microsoft Passport 필요 합니다.
  
> [!NOTE]  
> Windows Server 2003 도메인 컨트롤러와 환경에 대 한 모든 지원을 종료 되었습니다. 방문 [이 페이지](https://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=Windows+Server+2003&Filter=FilterNO) Microsoft 지원 기간에 대 한 추가 정보입니다.  
  
**도메인 기능\-수준 요구 사항**  
  
 - 모든 사용자 계정 도메인 및 AD FS 서버 가입 된 도메인의 Windows Server 2003 이상 도메인 기능 수준에서 작동 해야 합니다.  
  
 - Windows Server 2008 도메인 기능 수준 이상이 경우 필요한 클라이언트 인증서 인증을 위해 AD DS에서에서 사용자의 계정에는 인증서는 명시적으로 매핑됩니다.  
  
**스키마 요구 사항**  
  
-   AD FS 2016 새로 설치 (최소 버전 85) Active Directory 2016 스키마가 필요 합니다.

-   AD FS 팜 동작 수준 (FBL) 2016 수준 올리기 Active Directory 2016 스키마 (최소 버전 85) 필요 합니다.  

  
**서비스 계정 요구 사항**  
  
-   모든 표준 도메인 계정이 AD FS에 대 한 서비스 계정으로 사용할 수 있습니다. 그룹 관리 서비스 계정은 지원 됩니다. AD FS를 구성 하는 경우 런타임에 필요한 사용 권한은 자동으로 추가 됩니다.

-   AD 서비스 계정에 필요한 사용자 권한 할당 '서비스로 로그온'입니다.

-   ' NT Service\adfssrv' 및 ' NT Service\drs'에 필요한 사용자 권한 할당은 보안 감사 생성 ' 및 '서비스로 로그온'입니다.

-   그룹 관리 서비스 계정에는 Windows Server 2012 이상을 실행 하는 도메인 컨트롤러가 하나 이상 필요 합니다.  기본 GMSA 있어야 ' CN = 관리 되는 서비스 계정의 컨테이너입니다.  

-   Kerberos 인증의 경우 서비스 사용자 이름 '`HOST/<adfs\_service\_name>`' AD FS 서비스 계정에 등록 해야 합니다. 기본적으로 AD FS 구성 합니다이 새 AD FS 팜을 만들 때.  와 같은 실패 하면 충돌 또는 사용 권한이 있는 경우 경고가 나타납니다 및 수동으로 추가 해야 합니다.  
   
**도메인 요구 사항**  
  
-   모든 AD FS 서버는 AD DS 도메인에 조인 이어야 합니다.  
  
-   모든 AD FS 서버 팜 내에서 동일한 도메인에 배포 되어야 합니다.  
   
**다중 포리스트 요구 사항**  
  
-   모든 도메인 이나 포리스트의 AD FS 서비스에 인증 하는 사용자가 포함 된 AD FS 서버 가입 된 도메인 신뢰 해야 합니다.  

-   포리스트의 AD FS 서비스 계정으로 구성원 인 모든 사용자 로그인 포리스트를 신뢰 해야 합니다. 
  
-   AD FS 서비스 계정이 AD FS 서비스를 인증 하는 사용자를 포함 하는 모든 도메인 사용자 특성을 읽을 권한이 있어야 합니다.  
  
## <a name="BKMK_5"></a>구성 데이터베이스 요구 사항  
이 섹션에서는 요구 사항 및 사용 하는 각각 내부 데이터베이스 WID (Windows) 또는 SQL Server 데이터베이스와 AD FS 팜에 대 한 제한 사항을 설명 합니다.  
  
**WID**  
  
-   SAML 2.0의 아티팩트 확인 프로필 WID 팜에서 지원 되지 않습니다.    

-   토큰 재생 검색에는 없는 WID 팜 지원 합니다. (이 기능은 AD FS는 페더레이션 공급자 역할을 하 고 외부 클레임 공급자의 보안 토큰을 사용 하는 경우에만 사용 됩니다.)  
  
다음 표에서 AD FS 서버 수에 대 한 요약 제공 WID vs에서 SQL Server 팜을 지원 합니다.    
  
  
|| 1-100 신뢰 당사자 (RP) 트러스트에서 AD FS 구성 | 100 개가 넘는 RP 트러스트 구성  |
| --- |--- | --- |
|1-30 AD FS 서버|WID 지원|WID-필요한 SQL Server를 사용 하 여 지원 되지 않습니다. |
|개 이상의 30 AD FS 서버|WID-필요한 SQL Server를 사용 하 여 지원 되지 않습니다.|WID-필요한 SQL Server를 사용 하 여 지원 되지 않습니다.  
  
**SQL Server**  
  
- Windows Server 2016에서 AD FS에 대 한 SQL Server 2008 및 더 높은 버전 지원 됩니다.

- SAML 아티팩트 확인와 토큰 재생 검색은 SQL Server 팜의에서 지원 됩니다.  
  
## <a name="BKMK_6"></a>브라우저 요구 사항  
브라우저 또는 브라우저 컨트롤을 통해 AD FS 인증을 수행할 때는 브라우저 다음 요구 사항을 준수 해야 합니다.  
  
-   JavaScript은 사용 하도록 설정  
  
-   Single sign on 클라이언트 브라우저가 쿠키를 허용 하도록 구성 해야 합니다.  
  
-   서버 이름 표시 \(SNI\) 지원 되어야 합니다  
  
-   브라우저는 사용자 인증서 및 장치 인증서 인증을 위해 SSL 클라이언트 인증서 인증을 지원 해야 합니다.  

-   Windows 통합 인증을 페더레이션 서비스 이름을 사용 하 여 원활한 로그인 (예: https:\/\/fs.contoso.com) 로컬 인트라넷 영역 또는 신뢰할 수 있는 사이트 영역에서 구성 해야 합니다.
## <a name="BKMK_7"></a>네트워크 요구 사항  
 
**방화벽 요구 사항**  
  
웹 응용 프로그램 프록시 및 페더레이션 서버 팜 및 클라이언트와 웹 응용 프로그램 프록시 간의 방화벽 사이 있는 두 방화벽에는 TCP 포트 443을 사용할 수 있어야 합니다. 인바운드 합니다.  
  
또한 클라이언트 사용자 인증서 인증 하는 경우 \(clientTLS 인증 X509를 사용 하 여 사용자 인증서\) 필요 certauth 끝점 포트 443에서 사용 가능 하지, AD FS 2016 TCP 포트 49443을 설정 하는 것이 필요 하 고 클라이언트와 웹 응용 프로그램 프록시 간의 방화벽에 인바운드 합니다. 이 웹 응용 프로그램 프록시와 페더레이션 서버 간의 방화벽에 필요 하지 않습니다\)합니다. 

하이브리드 포트에 대 한 자세한 요구 사항을 참조 하세요 [하이브리드 Identity 포트 및 프로토콜](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports)합니다. 

추가 정보를 참조 하세요. [Active Directory Federation Services 보안 모범 사례입니다](..\deployment\Best-Practices-Securing-AD-FS.md)
  
**DNS 요구 사항**  
  
-   인트라넷 액세스를 위한 AD FS에 액세스 하는 모든 클라이언트는 내부 회사 네트워크 내에서 서비스 \(인트라넷\) AD FS 서버 또는 AD FS 서버에 대 한 부하 분산 장치에 AD FS 서비스 이름을 확인할 수 있어야 합니다.  
  
-   엑스트라넷 액세스에 대 한 AD FS에 액세스 하는 모든 클라이언트에서 서비스를 회사 네트워크 외부의 \(엑스트라넷\/인터넷\) 웹 응용 프로그램 프록시 서버 또는 웹 응용 프로그램 프록시 서버에 대 한 부하 분산 장치에 AD FS 서비스 이름을 확인할 수 있어야 합니다.  
  
-   각 웹 응용 프로그램 프록시 서버는 DMZ에 AD FS 서버 또는 AD FS 서버에 대 한 부하 분산 장치에 AD FS 서비스 이름을 확인할 수 있어야 합니다. 호스트 파일을 사용 하 여 로컬 서버 해상도 변경 하거나 DMZ 네트워크에 대체 DNS 서버를 사용 하 여 수행할 수 있습니다.  
  
-   Windows 통합 인증에 대 한 DNS A 레코드를 사용 해야 \(하지 CNAME\) 페더레이션 서비스 이름에 대 한 합니다.  

-   포트 443에서 사용자 인증서 인증을 위해 "certauth.\<페더레이션 서비스 이름\>"페더레이션 서버 또는 웹 응용 프로그램 프록시를 확인 하기 위해 DNS에 구성 되어야 합니다.

-   장치 등록 또는 온-프레미스 리소스 10 이전 windows 클라이언트를 사용 하 여 최신 인증을 "enterpriseregistration.\<upn 접미사\>", 페더레이션 서버 또는 웹 응용 프로그램 프록시를 확인 하기 위해 조직에서 사용 중인 각 UPN 접미사를 구성 해야 합니다.

**부하 분산 장치 요구 사항**
- 부하 분산 장치를 안 SSL 종료 합니다. AD FS SSL 종료 발생할 때 중단 하는 인증서 인증을 사용 하 여 여러 사용 사례를 지원 합니다. 부하 분산 장치 SSL 종료 사용 사례에 대 한 지원 되지 않습니다. 
- SNI를 지 원하는 부하 분산 장치를 사용 하는 것이 좋습니다. 이벤트 하지 않는 AD FS에 대 한 바인딩 대체 (fallback) 0.0.0.0을 사용 하 여 웹 응용 프로그램 프록시 서버에는 해결 방법을 제공 해야 합니다.
- 트래픽 라우팅에 대 한 부하 분산 장치 상태 검사를 수행 하려면 HTTP (HTTPS 아님) 상태 프로브 끝점을 사용 하는 것이 좋습니다. 이렇게 하면 SNI와 관련 된 문제가 없습니다. 이러한 프로브 끝점에 대 한 응답에 HTTP 200 OK 이며 백 엔드 서비스에 종속 되지 않음를 사용 하 여 로컬로 제공 됩니다. HTTP 프로브는 '/ adf/프로브' 경로 사용 하 여 HTTP를 통해 액세스할 수 있습니다.
    - http://&lt;웹 응용 프로그램 프록시 이름 &gt; /adf/프로브
    - http://&lt;ADFS 서버 이름을 &gt; /adf/프로브
    - http://&lt;웹 응용 프로그램 프록시 IP 주소 &gt; /adf/프로브
    - http://&lt;ADFS ip &gt; /adf/프로브
- DNS를 사용 하는 것은 권장 되지 부하를 분산 하는 방법으로 라운드 로빈입니다. 이 유형의 부하 분산을 사용 하 여 상태 프로브를 사용 하 여 부하 분산 장치에서 노드를 제거 하는 자동화 된 방법을 제공 하지 않습니다. 
- 하지 인증 트래픽 부하 분산 장치 내에서 AD fs에 대 한 IP 기반 세션 선호도 또는 고정 세션을 사용 하는 것이 좋습니다. 메일 클라이언트에 대 한 레거시 인증 프로토콜을 사용 하 여 Office 365 메일 서비스 (Exchange Online)에 연결할 때 특정 노드가 오버 로드를 발생할 수 있습니다이 있습니다. 

## <a name="BKMK_13"></a>사용 권한 요구 사항  
설치 및 AD FS의 초기 구성을 수행 하는 관리자에는 AD FS 서버에서 로컬 관리자 권한이 있어야 합니다.  먼저 도메인 관리자는 로컬 관리자는 Active Directory에 개체를 만들 권한이 없는 경우 있어야 필요한 AD 개체를 만든 다음 AdminConfiguration 매개 변수를 사용 하 여 AD FS 팜을 구성 합니다.  
  
  

