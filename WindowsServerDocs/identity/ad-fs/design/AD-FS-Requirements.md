---
ms.assetid: 8ce6e7c4-cf8e-4b55-980c-048fea28d50f
title: "Federation 서버 팜 SQL Server를 사용 하 여"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e23154b20dfcd642178a5ac0de17f1b6a490f91f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ad-fs-requirements"></a>광고 FS 요구 사항

>Windows Server 2012 r 2에 적용 됩니다.

ADFS 배포할 때을 준수 해야 하는 다양 한 요구 사항은 다음과 같습니다.  
  
-   [인증서 요구 사항](AD-FS-Requirements.md#BKMK_1)  
  
-   [하드웨어 요구 사항](AD-FS-Requirements.md#BKMK_2)  
  
-   [소프트웨어 요구 사항](AD-FS-Requirements.md#BKMK_3)  
  
-   [광고 DS 요구 사항](AD-FS-Requirements.md#BKMK_4)  
  
-   [구성 데이터베이스 요구 사항](AD-FS-Requirements.md#BKMK_5)  
  
-   [브라우저 요구 사항](AD-FS-Requirements.md#BKMK_6)  
  
-   [익스트라넷 요구 사항](AD-FS-Requirements.md#BKMK_extranet)  
  
-   [네트워크 요구 사항](AD-FS-Requirements.md#BKMK_7)  
  
-   [특성 스토어 요구 사항](AD-FS-Requirements.md#BKMK_8)  
  
-   [응용 프로그램 요구 사항](AD-FS-Requirements.md#BKMK_9)  
  
-   [인증 요구 사항](AD-FS-Requirements.md#BKMK_10)  
  
-   [회사 가입 요구 사항](AD-FS-Requirements.md#BKMK_11)  
  
-   [암호화 요구 사항](AD-FS-Requirements.md#BKMK_12)  
  
-   [사용 권한 요구 사항](AD-FS-Requirements.md#BKMK_13)  
  
## <a name="BKMK_1"></a>인증서 요구 사항  
인증서는 federation 서버, 웹 응용 프로그램 프록시, claims\ 인식 응용 프로그램 및 웹 클라이언트 간 통신 보안에서 가장 중요 한 역할을 재생 합니다. 인증서에 대 한 요구 사항 여부를 설정 하는 federation 서버 또는 프록시 컴퓨터가이 섹션에 설명 된 대로 따라 다릅니다.  
  
**Federation 서버 인증서**  
  
|||  
|-|-|  
|**인증서 종류**|**요구 사항, 지원 및 것을 알고**|  
|**보안 주소 \(SSL\) 인증서:** federation 서버 하는 클라이언트와 커뮤니케이션 보호 하기 위한 사용 되는 표준 SSL 인증서입니다.|-이 인증서를 공개적으로 trusted\ * X509 v3 인증서 합니다.<br />-모든 ADFS 끝점 액세스 하는 모든 클라이언트가이 인증서를 신뢰 해야 합니다. 공용 \(third\-party\) 인증 기관에서 발급 된 인증서를 사용 하는 것이 좋습니다 강력한 \(CA\) 합니다. SSL self\ 서명 인증서를 테스트 랩 환경에서 federation 서버에 성공적으로 사용할 수 있습니다. 하지만, 생산 환경에서 공개 캘리포니아 인증서를 얻는 것이 좋습니다.<br />-Windows Server 2012 r 2가 SSL 인증서에 대 한 지원 되는 모든 주요 크기를 지원 합니다.<br />-CNG 키를 사용 하는 지원 인증서 하지 않습니다.<br />-회사 Join\/디바이스 등록 서비스와 함께 사용 하는 경우 조직의 enterpriseregistration.contoso.com 등의 사용자 이름 \(UPN\) 접미사 뒤에 나오는 값 enterpriseregistration ADFS 서비스에 대 한 다른 이름과 SSL 인증서의 제목 있어야 합니다.<br />-와일드 카드 인증서가 지원 됩니다. ADFS 서비스에 대 한 서비스 이름을 입력 하 라는 메시지가 표시 ADFS 그룹을 만들 때 \ (예를 들어, **adfs.contoso.com**합니다.<br />-웹 응용 프로그램 프록시 동일한 SSL 인증서를 사용 하 여 좋습니다 것입니다. 그러나이 **필요한** 같을 때 추가 보호 인증 \(default setting\) 켜져 있을 때를 통해 웹 응용 프로그램 프록시 Windows 통합 인증 끝점 지원 합니다.<br />-이 인증서의 제목 이름 배포 하기는 Adfs의 각 인스턴스 Federation 서비스 이름을 나타내는 데 사용 됩니다. 이러한 이유로 이름을 회사 또는 조직이 파트너에 게 가장 잘 나타내는 새로운 CA\ 발급 된 인증서를 제목 이름 선택 고려해 야 할 수 있습니다.<br />    인증서의 id 해당 federation 서비스 이름을 일치 해야 \ (예를 들어 fs.contoso.com\). Id가 유형 dNSName의 중 하나는 대상 대체 이름 확장명 하거나 일반 이름으로 대상 이름이 지정 제목을 대체 이름 항목이 인 합니다. 여러 제목을 대체 이름 항목 중 하나 일치 해당 federation 서비스 이름을 제공한는 인증서에 사용할 수 있습니다.<br />-   **중요:** ADFS 농장에 있는 모든 웹 응용 프로그램 프록시 뿐만 아니라 모든 노드 ADFS 농장의에서 동일한 SSL 인증서를 사용 하도록 좋습니다 했습니다.|  
|**서비스 통신 인증서:** 이 인증서 federation 서버 간에 커뮤니케이션 보호 하기 위한 WCF 메시지 보안을 사용 합니다.|-기본적으로 ssl 서비스 통신 인증서도 사용 됩니다.  하지만 다른 인증서 서비스 통신 인증서도 구성할 수 있는 옵션이 있습니다.<br />-   **중요:** SSL 인증서가 만료 될 때 ssl 서비스 통신 인증서를 사용 하는, 경우로 서비스 통신 인증서 갱신된 SSL 인증서를 구성할 수 있는지 확인 합니다. 이 자동으로 발생 하지 않습니다.<br />-Adfs WCF 메시지 보안을 사용 하는 클라이언트가이 인증서 신뢰할 수 있어야 합니다.<br />-공용 \(third\-party\) 인증 기관에서 발급 서버 인증 인증서를 사용 하는 것이 좋습니다 저희 \(CA\) 합니다.<br />-서비스 통신 인증서 CNG 키를 사용 하는 인증서 수 없습니다.<br />-이 인증서 AD FS Management console을 사용 하 여 관리할 수 있습니다.|  
|**Token\ 서명 인증서:** 이것은 표준 X509 모든 토큰 연합 서버 발급을 안전 하 게 로그인 하는 것에 사용 되는 인증서 합니다.|-기본적으로 ADFS 2048 약간 키가 있는 self\ 서명 인증서를 만듭니다.<br />-캐나다 발급 된 인증서도 지원 하 고 snap\에서 AD FS 관리를 사용 하 여 변경할 수 있습니다.<br />-캐나다 발급 된 인증서를 저장 및 CSP 암호화 공급자를 통해 액세스할 수 있어야 합니다.<br />토큰 서명 인증서-CNG 키를 사용 하는 인증서 수 없습니다.<br />-ADFS 토큰 서명 인증서 외부적으로 등록 된 필요 하지 않습니다.<br />    ADFS 자동으로 갱신 이러한 self\ 서명 인증서 만료 되기 전에 먼저 보조 인증서를 사용 하는 파트너 될 수 있도록 새로운 인증서를 구성 다음 자동 인증서 롤오버 이라는 프로세스의 주요에 플리핑 합니다. 기본적으로 자동으로 생성 된 토큰 서명 인증서를 사용 하는 것이 좋습니다.<br />    조직에서는 토큰 서명 구성 다른 인증서 해야 하는 정책, Powershell를 사용 하 여 설치 시 인증서를 지정할 수 있습니다 \ (Install\ AdfsFarm cmdlet\의-SigningCertificateThumbprint 매개 사용).  설치 후 보고 하 고 토큰 서명 인증서 AD FS Management console 또는 Powershell cmdlet Set\ AdfsCertificate Get\ AdfsCertificate 사용을 관리할 수 있습니다.<br />    토큰 서명 외부 등록된 인증서를 사용할 때 자동으로 인증 또는 롤오버 ADFS 수행 하지 않습니다.  관리자 권한으로이 프로세스를 수행 해야 합니다.<br />    하나 인증서가 만료 가까운 때 인증서 롤오버에 대 한 허용할, adfs에서 보조 토큰 서명 인증서를 구성할 수 있습니다. 기본적으로 모든 토큰 서명 인증서 federation 메타 데이터에 게시 있지만 기본 token\ 서명 인증서만은 ADFS 실제로 토큰 서명 하는 데 사용 됩니다.|  
|**Token\ decryption\/암호화 인증서:** 이것은 표준 X509 즉 인증서 모든 들어오는 토큰 decrypt\/암호화 하는 데 사용 합니다. 또한 federation 메타 데이터에 게시 됩니다.|-기본적으로 ADFS 2048 약간 키가 있는 self\ 서명 인증서를 만듭니다.<br />-캐나다 발급 된 인증서도 지원 하 고 snap\에서 AD FS 관리를 사용 하 여 변경할 수 있습니다.<br />-캐나다 발급 된 인증서를 저장 및 CSP 암호화 공급자를 통해 액세스할 수 있어야 합니다.<br />-Token\ decryption\/암호화 인증서 CNG 키를 사용 하는 인증서 수 없습니다.<br />-기본적으로 ADFS 생성 하 고 토큰 해독에 대 한 자체적으로 내부에서 생성 된 및 self\ 서명 인증서를 사용 합니다.  Adfs이이 목적을 위해 외부적으로 등록 된 인증서를 필요 하지 않습니다.<br />    또한 ADFS 자동으로 갱신 이러한 self\ 서명 인증서 만료 되기 전에 합니다.<br />    **기본적으로 토큰 암호 해독에 자동으로 생성 된 인증서를 사용 하는 것이 좋습니다.**<br />    조직에서는 토큰 암호 해독 구성 다른 인증서 해야 하는 정책, Powershell를 사용 하 여 설치 시 인증서를 지정할 수 있습니다 \ (Install\ AdfsFarm cmdlet\의-DecryptionCertificateThumbprint 매개 사용).  설치 후 볼 수 있으며 토큰 해독 인증서 AD FS Management console 또는 Powershell cmdlet Set\ AdfsCertificate 및 Get\ AdfsCertificate 사용 하 여 관리할 수 있습니다.<br />    **외부 등록된 인증서 토큰 암호 해독을 사용 하는 ADFS 인증서 자동 갱신을 수행 하지 않습니다. 관리자가이 프로세스를 수행 해야**합니다.<br />-ADFS 서비스 계정 로컬 컴퓨터의 개인 스토어에서 개인 키 token\ 서명 인증서에 액세스할 수 있어야 합니다. 이의 처리 하 여 설치 합니다. 또한 이후에 token\ 서명 인증서를 변경 하면이 액세스할 수 있도록 snap\에서 AD FS 관리를 사용할 수 있습니다.|  
  
> [!CAUTION]  
> Token\ 서명 및 decrypting\/암호화 token\에 사용 되는 인증서를 중요 하며, Federation 서비스의 안정성을 개선 합니다. 자신의 token\ 서명 및 token\ decrypting\/암호화 인증서를 관리 하는 고객은 이러한 인증서를 백업 하 고 사용할 수 없는 독립적으로 이벤트를 복구 하는 동안 확인 해야 합니다.  
  
> [!NOTE]  
> Adfs의 SHA\ 1 또는 SHA\ 256 \(more secure\)에 디지털 서명이에 사용 되는 Secure Hash Algorithm \(SHA\) 수준을 변경할 수 있습니다. ADFS m d 5 같은 다른 해시 방법으로 인증서의 사용을 지원 하지 않습니다 \ (기본 hash 알고리즘 Makecert.exe command\ 줄 tool\ 함께 사용 되는). 최적의 보안을 유지 SHA\ 256 사용 하는 것이 좋습니다 \ (default\로 설정 된)에 대 한 모든 서명이 합니다. Adfs의 non\ Microsoft 제품 또는 레거시 버전 같은 SHA\ 256를 사용 하 여 통신을 지원 하지 않는 제품 작용 해야 하는 경우에만 사용할 수 있도록 SHA\ 1이 좋습니다.  
  
> [!NOTE]  
> 인증서에 캐나다에서를 받은 후 로컬 컴퓨터의 개인 인증서 스토어에 모든 인증서를 가져오는 있는지 확인 합니다. 인증서에 snap\ 인증서 mmc 개인용 저장소를 가져올 수 있습니다.  
  
## <a name="BKMK_2"></a>하드웨어 요구 사항  
Windows Server 2012 r 2의 ADFS federation 서버에 다음과 같은 최소 및 권장 하드웨어 요구 사항을 적용 됩니다.  
  
||||  
|-|-|-|  
|**하드웨어 요구 사항**|**최소 요구 사항**|**권장된 요구 사항**|  
|CPU 속도|1.4 g h z 64\ 비트 프로세서|Quad\ 코어, 2 g h z|  
|RAM|512MB|4GB|  
|디스크 공간|32GB|100 G B|  
  
## <a name="BKMK_3"></a>소프트웨어 요구 사항  
서버 기능® Windows Server 2012 r 2 운영 체제에 기본 제공을 위해 다음 ADFS 요구 사항은 다음과 같습니다.  
  
-   엑스트라넷 액세스를 위해 웹 응용 프로그램 프록시 역할 서비스 배포 해야 \-® Windows Server 2012 r 2에 대 한 원격 액세스 거부 그렇습니다. 이전 버전의 federation 서버 프록시® Windows Server 2012 r 2에 Adfs로 지원 되지 않습니다.  
  
-   Federation 서버와 웹 응용 프로그램 프록시 역할 서비스 동일한 컴퓨터에 설치할 수 없습니다.  
  
## <a name="BKMK_4"></a>광고 DS 요구 사항  
**도메인 컨트롤러 요구 사항**  
  
모든 사용자 도메인 및 ADFS 서버 가입 된 도메인 도메인 컨트롤러에 2008 이상을 Windows Server를 실행 해야 합니다.  
  
> [!NOTE]  
> 연장 지원 종료 날짜에 대 한 Windows Server 2003 후 Windows Server 2003 도메인 컨트롤러 관련 환경에 대 한 지원 종료 됩니다. 고객은 가능한 한 빨리 해당 도메인 컨트롤러 업그레이드 좋습니다. 방문 [이 페이지](https://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=Windows+Server+2003&Filter=FilterNO) 에 대 한 자세한 내용은 Microsoft 지원 수명 주기 합니다. 발견 하는 문제에 대 한 하는 Windows Server 2003 도메인 컨트롤러의 환경에 고유한, 수정 발생 하는 보안 문제에 대 한 및 문제를 해결 하는 경우 Windows에 대 한 지원을 추가 Server 2003 만료 되기 전에 실행 될 수 있습니다.  
  
**도메인 functional\ 수준 요구 사항**  
  
Windows Server 2003 이상 도메인 기능 수준에서 모든 사용자 계정 도메인 및 ADFS 서버 가입 된 도메인 작업 해야 합니다.  
  
대부분의 ADFS 기능이 제대로 작동 하려면 AD DS functional\ 수준 수정 필요 하지 않습니다. 그러나 Windows Server 2008 도메인 기능 이상 수준가 필요 클라이언트 인증서 인증 인증서가 명시적으로 AD DS에는 사용자의 계정을에 매핑됩니다 경우 성공적으로 작동 하도록 합니다.  
  
**스키마 요구 사항**  
  
-   Adfs는 스키마 변경 또는 AD DS functional\ 수준 개조 필요 하지 않습니다.  
  
-   회사에 참여 하는 기능을 사용 하려면 Windows Server 2012 r 2에 ADFS 서버에 가입한 숲 스키마를 설정 해야 합니다.  
  
**서비스 계정 요구 사항**  
  
-   표준 서비스 계정은 adfs 서비스 계정으로 사용할 수 있습니다. 그룹 관리 서비스 계정도 지원 됩니다. 이 위해서는 하나 이상 도메인 컨트롤러 \ (두 개를 배포 하는 것이 좋습니다 또는 more\) Windows Server 2012 이상 실행 합니다.  
  
-   Kerberos 인증 domain\ 가입 클라이언트 ADFS와 기능에는 ' HOST\ / < adfs\_service\_name >'으로 SPN 서비스 계정에 등록 해야 합니다. 기본적으로 Adfs은 구성이이 작업을 수행할 수 있는 권한이 경우 새 ADFS 농장 만들 때 합니다.  
  
-   사용자가 인증 ADFS 서비스를 포함 하는 모든 사용자 도메인에 ADFS 서비스 계정 신뢰할 수 있어야 합니다.  
  
**도메인 요구 사항**  
  
-   모든 ADFS 서버 AD DS 도메인에 가입 이어야 합니다.  
  
-   모든 ADFS 서버 농장 내 단일 도메인에 배포할 수 있어야 합니다.  
  
-   도메인에 가입한 ADFS 서버 인증 ADFS 서비스에 사용자가 포함 된 모든 사용자 계정을 도메인이 신뢰 해야 합니다.  
  
**다중 숲 요구 사항**  
  
-   모든 사용자 계정 도메인 또는 인증 ADFS 서비스에 사용자가 포함 된 숲 ADFS 서버에 가입 된 도메인 신뢰 해야 합니다.  
  
-   사용자가 인증 ADFS 서비스를 포함 하는 모든 사용자 도메인에 ADFS 서비스 계정 신뢰할 수 있어야 합니다.  
  
## <a name="BKMK_5"></a>구성 데이터베이스 요구 사항  
구성 스토어의 종류에 따라 적용 되는 제한 및 요구 사항은 다음과 같습니다.  
  
**WID**  
  
-   100 이하의 신뢰 파티 신뢰 하는 경우 WID 농장은 30 federation 서버 제한 됩니다.  
  
-   SAML 2.0에서 아티팩트 해상도 프로필 WID 구성 데이터베이스에는 지원 되지 않습니다.  토큰 재생 검색 WID 구성 데이터베이스에는 지원 되지 않습니다. 이 기능은 Adfs은 federation 공급자 역할을 하 고 외부 클레임 공급자의 보안 토큰을 사용 하는 경우에만 사용 됩니다.  
  
-   장애 조치 센터 서로 다른 데이터에서 ADFS 서버를 배포 하거나 지리적 부하 분산 30 서버 수를 초과 하지 않도록으로 지원 됩니다.  
  
다음 표에서 WID 농장 사용에 대 한 요약 정보를 제공 합니다.  구현을 계획을 사용 하세요.  
  
||||  
|-|-|-|  
||1 \-100 RP 신뢰|100 개 이상의 RP 신뢰|  
|1 \-30 광고 FS 노드|지원 되는 WID|사용 하 여 WID 지원 되지 않습니다 \-SQL 필요|  
|30 AD 이상 FS 노드|사용 하 여 WID 지원 되지 않습니다 \-SQL 필요|사용 하 여 WID 지원 되지 않습니다 \-SQL 필요|  
  
**SQL Server**  
  
Windows Server 2012 r 2 ADFS SQL Server 2008 및 이상 사용할 수 있습니다.  
  
## <a name="BKMK_6"></a>브라우저 요구 사항  
브라우저나 브라우저 컨트롤을 통해 ADFS 인증을 수행 하세요 브라우저 다음 요구 사항을 준수 해야 합니다.  
  
-   JavaScript은 사용 하도록 설정  
  
-   쿠키를 켜야 합니다.  
  
-   서버 이름 표시 \(SNI\) 지원 해야  
  
-   사용자 장치 및 인증서 인증서 인증에 대 한 \ (회사 가입 functionality\) 브라우저 클라이언트 인증서 인증 SSL을 지원 해야 합니다  
  
몇 가지 주요 브라우저와 플랫폼 유효성 검사는의 세부 정보는 아래에 나열 된 렌더링 및 기능에 대 한 마쳤으며 합니다. 위에 나열 된 요구 사항을 충족 하는지 브라우저와이 표에 포함 되지 장치 지원 계속 됩니다.  
  
|||  
|-|-|  
|**브라우저**|**플랫폼**|  
|IE 10.0|Windows 7, Windows 8.1, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 r 2|  
|IE 11.0|Windows7, Windows 8.1, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 r 2|  
|Windows 웹 인증 중개 업체|Windows 8.1|  
|Firefox \[v21\]|Windows 7, Windows 8.1|  
|Safari \[v7\]|Mac OS\ X 10.7 6, iOS|  
|Chrome \[v27\]|Windows 7, Windows 8.1, Windows Server 2012, Windows Server 2012 R2, Mac OS\ X 10.7|  
  
> [!IMPORTANT]  
> 알려진 문제 \-Firefox: 장치 인증서를 사용 하 여 장치를 식별 하는 회사에 참여 기능 Windows 플랫폼에서 작동 하지 않습니다. Firefox는 SSL 클라이언트 인증서 인증을 수행 하도록 Windows 클라이언트의 사용자 인증서 스토어 프로 비전 인증서를 사용 하 여 현재 지원 되지 않습니다.  
  
**쿠키**  
  
Adfs는 sign\에서 제공 하는 클라이언트 컴퓨터, sign\ 아웃, 단일 sign\ 켜 짐 \(SSO\), 및 기타 기능에 대해 저장 해야 하는 쿠키 및 영구 session\ 기반 만듭니다. 따라서 클라이언트 브라우저에서 쿠키를 허용 하도록 설정 해야 합니다. 인증에 사용 되는 쿠키는 항상 하이퍼텍스트 전송 프로토콜 보안 \(HTTPS\) 세션 하는 쿠키는 원래 서버에 기록 됩니다. 이러한 쿠키를 허용 하도록 클라이언트 브라우저 구성 되지 않았습니다를 ADFS 올바르게 작동할 수 없습니다. 영구 쿠키 사용자 클레임 공급자의 선택을 유지 하는 데 사용 합니다. 이러한 구성 설정을 ADFS sign\-페이지에 대 한 구성 파일을 사용 하 여 비활성화할 수 있습니다. TLS\/SSL에 대 한 지원은 보안상의 이유로 필요 합니다.  
  
## <a name="BKMK_extranet"></a>익스트라넷 요구 사항  
ADFS 서비스에 대 한 익스트라넷 액세스를 제공 하기 위해 배포 해야 웹 응용 프로그램 프록시 역할 서비스 엑스트라넷 향하는 역할을는 프록시 인증 요청 ADFS 서비스에 안전 하 게에서 됩니다. 이 통해 ADFS 서비스 끝점 격리 뿐 아니라 격리 보안 키를 모두 \ (예: 토큰 서명 certificates\) 요청을 처리 하는 인터넷에서 가져온 것일에서 합니다. 또한 부드러운 익스트라넷 계정 잠금을 같은 기능 웹 응용 프로그램 프록시 사용을 해야 합니다. 웹 응용 프로그램 프록시에 대 한 자세한 내용은 참조 [웹 응용 프로그램 프록시](https://technet.microsoft.com/library/dn584107.aspx)합니다.  
  
이 third\ 자 프록시에 정의 된 프로토콜을 지원 해야 third\ 자 프록시 익스트라넷 액세스에 사용 하려는 경우 [http:///\/download.microsoft.com\/download\/9\/5\/E\/95EF66AF\-9026\-4BB0\-A41D\-A4F81802D92C\/%5bMS\-ADFSPIP%5d.pdf](https://download.microsoft.com/download/9/5/E/95EF66AF-9026-4BB0-A41D-A4F81802D92C/%5bMS-ADFSPIP%5d.pdf)합니다.  
  
## <a name="BKMK_7"></a>네트워크 요구 사항  
다음 네트워크 서비스를 적절 하 게 구성 성공적인 ADFS 조직에서 배포에 대 한 중요 한는 다음과 같습니다.  
  
**회사 방화벽 구성**  
  
웹 응용 프로그램 프록시 및 federation 서버 팜은 클라이언트와 웹 응용 프로그램 프록시 방화벽 사이 있는 두 방화벽 TCP 포트 사용 443 있어야 인바인드 합니다.  
  
또한 클라이언트 사용자 인증 인증서 경우 \ (clientTLS 인증 X509를 사용 하 여 사용자 certificates\)가 필요, Windows Server 2012 r 2에서 ADFS 설정 해야 하 TCP 포트 49443는 클라이언트와 웹 응용 프로그램 프록시 방화벽 인바인드 합니다. 이 필요 하지 않습니다 웹 응용 프로그램 프록시 사이의 federation servers\ 방화벽).  
  
**DNS 구성**  
  
-   인트라넷 액세스할 수 있도록 모든 클라이언트 내부 회사 네트워크 \(intranet\) 내 ADFS 서비스에 액세스할 수 있어야 ADFS 서비스 이름을 확인 하려면 \ (SSL certificate\ 제공한 이름) ADFS 서버 또는 ADFS 서버에 대 한 부하 분산을 합니다.  
  
-   익스트라넷 액세스에 대 한 모든 클라이언트 회사 네트워크 \(extranet\/internet\) 외부에서 ADFS 서비스에 액세스할 수 있어야 ADFS 서비스 이름을 확인 하려면 \ (SSL certificate\ 제공한 이름) 웹 응용 프로그램 프록시 서버 또는 웹 응용 프로그램 프록시 서버에 대 한 부하 분산을 합니다.  
  
-   제대로 작동 하려면 익스트라넷 액세스에 대 한 각 웹 응용 프로그램 프록시 서버에 DMZ ADFS 서비스 이름을 확인할 수 있어야 \ (SSL certificate\ 제공한 이름) 부하 분산 ADFS 서버 또는 ADFS 서버에 대해을 합니다. DMZ 네트워크 또는 호스트 파일을 사용 하 여 로컬 서버 해상도 변경 하 여 대체 DNS 서버를 사용 하 여 수행할 수 있습니다.  
  
-   네트워크 내부 및 외부 끝점 웹 응용 프로그램 프록시 통해의 하위 집합에 대 한 네트워크 작동 하도록 Windows 통합 인증에 대 한 A 기록 \(not CNAME\) 부하 분산 가리키도록 사용 해야 합니다.  
  
구성 회사 DNS federation 서비스 및 디바이스 등록 서비스에 대 한 참고 [Federation 서비스 및 DRS 회사 DNS 구성](https://technet.microsoft.com/library/dn486786.aspx)합니다.  
  
회사 DNS 프록시 웹 응용 프로그램에 대 한 구성에 대 한에서 "을 구성 DNS" 섹션 참조 [1 단계: 구성 웹 응용 프로그램 프록시 인프라](https://technet.microsoft.com/library/dn383644.aspx)합니다.  
  
클러스터 IP 주소를 구성 하거나 클러스터 FQDN NLB 사용 하는 방법에 대 한 정보를 참조에 클러스터 매개 지정 [http:///\/go.microsoft.com\/fwlink\/ 있나요? LinkId\ 75282 =](https://go.microsoft.com/fwlink/?LinkId=75282)합니다.  
  
## <a name="BKMK_8"></a>특성 스토어 요구 사항  
Adfs는 사용자가 인증 하 고 사용자에 대해 보안 클레임 압축에 사용 되는 하나 이상의 특성 스토어가 필요 합니다. 특성 목록이 ADFS 지원 저장, 참조 [The 역할의 특성을 저장](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)합니다.  
  
> [!NOTE]  
> Adfs는 기본적으로 "Active Directory" 특성 스토어를 자동으로 만들어집니다. 조직 계정 파트너와 작동 하는 있는지 여부에 따라 달라 특성 스토어 요구 사항을 \ (연합된 users\ 호스트) 또는 리소스 파트너 \ (연합된 application\ 호스트).  
  
**LDAP 특성 저장소**  
  
다른 경량 디렉터리 Access Protocol 작업할 때 \ (LDAP\) \-based 특성 스토어를 지 원하는 Windows 통합 인증 LDAP 서버에 연결 해야 합니다. LDAP 연결 문자열 RFC 2255에 설명 된 대로 LDAP URL을 형식으로 작성도 합니다.  
  
또한 ADFS 서비스에 대 한 서비스 계정에 LDAP 특성 스토어에서 사용자 정보를 검색할 수 있는 권한을 요구 합니다.  
  
**SQL Server 특성 저장소**  
  
Windows Server 2012 r 2 성공적으로 작동 하도록 ADFS SQL Server 특성 저장소 호스트 하는 컴퓨터 실행 중 이어야 합니다 Microsoft SQL Server 2008 이상 합니다. 특성 SQL\ 기반 저장소와 함께 작업 하는 경우 연결 문자열 또한 구성 해야 합니다.  
  
**사용자 지정 특성 스토어**  
  
사용자 지정 된 특성 스토어 고급 시나리오를 개발할 수 있습니다.  
  
-   Adfs에 기본 제공 되는 정책 언어를 다음 중 하나를 향상 시킬 수 있습니다 특성 사용자 지정 상점 참조할 수 있습니다.  
  
    -   로컬 인증된 사용자에 대 한 주장 만들기  
  
    -   보충 외부적으로 인증된 된 사용자에 대 한 주장  
  
    -   사용자가 토큰을 가져올 수 승인  
  
    -   서비스는 사용자의 동작에 토큰 얻는 승인  
  
    -   ADFS 신뢰 당사자에서 발급 보안 토큰에서 추가 데이터를 실행 합니다.  
  
-   모든 사용자 지정 된 특성 스토어.NET 4.0 위에 이상 구축 해야 합니다.  
  
사용자 지정 된 특성 저장소와 함께 작업 하는 경우 연결 문자열 구성 해야 될 수 있습니다. 이 경우 사용자 지정 된 특성 스토어에 대 한 연결을 사용 하는 사용자가 선택한 사용자 지정 코드를 입력할 수 있습니다. 이 경우에는 연결 문자열 name\/값 쌍 사용자 지정 된 특성 스토어 개발자가 구현으로 해석 하는 설정입니다. 개발 하 고 사용 하 여 사용자 지정 된 특성 스토어에 대 한 자세한 내용은 참조 [특성 스토어 개요](https://go.microsoft.com/fwlink/?LinkId=190782)합니다.  
  
## <a name="BKMK_9"></a>응용 프로그램 요구 사항  
ADFS 다음 프로토콜을 사용 하는 claims\ 인식 응용 프로그램을 지원 합니다.  
  
-   WS\ Federation  
  
-   WS\ 보안  
  
-   SAML 2.0 프로토콜 IDPLite, SPLite 및 eGov1.5 프로필을 사용 합니다.  
  
-   OAuth 2.0 승인 부여 프로필  
  
또한 ADFS 프록시 웹 응용 프로그램에서 지원 되는 모든 non\ claims\ 인식 응용 프로그램에 대 한 인증과 지원 합니다.  
  
## <a name="BKMK_10"></a>인증 요구 사항  
**AD DS 인증 \(Primary Authentication\)**  
  
인트라넷 액세스를 위해 광고 ds 다음 표준 인증 메커니즘 지원 됩니다.  
  
-   Windows 통합 인증 Kerberos 및 NTLM 협상을 사용 하 여  
  
-   양식 인증 username\/암호를 사용 하 여  
  
-   인증서 인증 AD DS의 사용자 계정에 매핑됩니다 인증서를 사용 하 여  
  
다음 인증 메커니즘 익스트라넷 액세스에 대해 지원 됩니다.  
  
-   양식 인증 username\/암호를 사용 하 여  
  
-   인증서 인증 인증서가 광고 DS 있는 사용자 계정에 사용 하 여  
  
-   Windows 통합 인증 동의 WS\ 신뢰 끝점 협상 \(NTLM only\)를 사용 하 여 Windows 통합 인증 합니다.  
  
인증서 인증 합니다.  
  
-   스마트 카드 보호 pin 될 수 있는를 확장 합니다.  
  
-   해당 pin을 입력 하 고 사용자에 대 한 GUI ADFS 제공한 고 TLS 클라이언트를 사용 하는 경우 표시 되는 클라이언트 운영 체제의 참여 하는 데 필요한 합니다.  
  
-   뷰어 및 암호화 서비스 공급자 브라우저 있는 컴퓨터에서 \(CSP\) 스마트 카드에 대 한 작업 해야 합니다.  
  
-   스마트 카드 인증서 신뢰할 수 있는 루트 모든 ADFS 서버와 웹 응용 프로그램 프록시 서버에 연결 해야 합니다.  
  
-   인증서 AD ds에서 사용자 계정에 다음 방법 중 하나 하 여 지도 해야 합니다.  
  
    -   인증서 제목 LDAP 고유 광고 DS의 사용자 계정 이름으로 해당합니다.  
  
    -   인증서 주제 altname 확장 사용자가 \(UPN\) AD ds에서 사용자 계정 이름을 지정 합니다.  
  
Windows의 원활 하 게 통합 인증에 대 한 Kerberos 인트라넷에서 사용 하 여  
  
-   신뢰할 수 있는 사이트 또는 로컬 인트라넷 사이트의 일부로 서비스 이름을 필요 합니다.  
  
-   또한는 HOST\ / < adfs\_service\_name > ADFS 팜에서 실행 되는 서비스 계정을에 SPN 설정 해야 합니다.  
  
**Multi\ 단계 인증**  
  
추가 인증을 지원 ADFS \ vendors\/고객 관리자 등록 하 고 로그인 시 사용할 수 있는 자신의 multi\ 팩터 인증 어댑터를 만들 수는 그 모델 공급자를 사용 하 여 기본 인증 DS\ 광고에 의해 지원) (외 합니다.  
  
모든 MFA 어댑터.NET 4.5 위에 구축 해야 합니다.  
  
에 대 한 자세한 내용은 MFA, [민감한 응용 프로그램에 대 한 추가 다단계 인증 관리 위험](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)합니다.  
  
**디바이스 인증**  
  
Adfs의 해당 장치에 참여 하는 최종 사용자 회사 act 하는 동안 디바이스 등록 서비스에 의해 프로 비전 인증서를 사용 하 여 디바이스 인증을 지원 합니다.  
  
## <a name="BKMK_11"></a>회사 가입 요구 사항  
최종 사용자에 게 장치를 사용 하 여 ADFS 조직 회사 가입 수 있습니다. 이것은 adfs에서 디바이스 등록 서비스에 의해 지원 됩니다. 결과적으로, 최종 사용자에 게 이용할 수 추가 SSO Adfs에서 지 원하는 응용 프로그램입니다. 또한 관리자 조직에 가입 회사 되었던 디바이스에만 응용 프로그램에 대 한 액세스를 제한 하 여 위험을 관리할 수 있습니다. 다음 요구 사항을이 문제를 아래에 있습니다.  
  
-   ADFS 회사 가입 Windows 8.1 및 iOS 5\ + 장치에 대 한 지원  
  
-   회사에 참여 하는 기능을 사용 하려면 ADFS 서버에 가입한 숲 속의 스키마 Windows Server 2012 r 2 해야 합니다.  
  
-   ADFS 서비스에 대 한 다른 이름과 SSL 인증서의 제목 조직의 enterpriseregistration.corp.contoso.com 등의 사용자 이름 \(UPN\) 접미사 뒤에 나오는 값 enterpriseregistration이 있어야 합니다.  
  
## <a name="BKMK_12"></a>암호화 요구 사항  
다음 표에서 ADFS 토큰 서명, 토큰 encryption\/해독 기능에 대해 추가 암호화 지원 정보:  
  
||||  
|-|-|-|  
|**알고리즘**|**키 길이**|**메모/Applications\ Protocols\ /**|  
|TripleDES – 기본 192 \ (지원 되는 192 – 256\) \- [http:///\/ www.w3.org \/2001\/04\/xmlenc\#tripledes\-cbc](http://www.w3.org/2001/04/xmlenc)|>\= 192|지원 되는 알고리즘 보안 토큰 암호화입니다.|  
|AES128 \-http:///\/ www.w3.org \/2001\/04\/xmlenc\#aes128\-cbc|128|지원 되는 알고리즘 보안 토큰 암호화입니다.|  
|AES192 \-http:///\/ www.w3.org \/2001\/04\/xmlenc\#aes192\-cbc|192|지원 되는 알고리즘 보안 토큰 암호화입니다.|  
|AES256 \- [http:///\/ www.w3.org \/2001\/04\/xmlenc\#aes256\-cbc](http://www.w3.org/2001/04/xmlenc)|256|**기본**합니다. 지원 되는 알고리즘 보안 토큰 암호화입니다.|  
|TripleDESKeyWrap \-http:///\/ www.w3.org \/2001\/04\/xmlenc\#kw\-tripledes|.NET 4.0\+에서 지 원하는 모든 키 크기|암호화 보안 토큰 암호화 대칭 키에 대해 알고리즘을 지원 됩니다.|  
|AES128KeyWrap \- [http:///\/ www.w3.org \/2001\/04\/xmlenc\#kw\-aes128](http://www.w3.org/2001/04/xmlenc)|128|암호화 보안 토큰 암호화 대칭 키에 대해 알고리즘을 지원 됩니다.|  
|AES192KeyWrap \- [http:///\/ www.w3.org \/2001\/04\/xmlenc\#kw\-aes192](http://www.w3.org/2001/04/xmlenc)|192|암호화 보안 토큰 암호화 대칭 키에 대해 알고리즘을 지원 됩니다.|  
|AES256KeyWrap \- [http:///\/ www.w3.org \/2001\/04\/xmlenc\#kw\-aes256](http://www.w3.org/2001/04/xmlenc)|256|암호화 보안 토큰 암호화 대칭 키에 대해 알고리즘을 지원 됩니다.|  
|RsaV15KeyWrap \-http:///\/ www.w3.org \/2001\/04\/xmlenc\#rsa\-1\_5|1024|암호화 보안 토큰 암호화 대칭 키에 대해 알고리즘을 지원 됩니다.|  
|RsaOaepKeyWrap \- [http:///\/ www.w3.org \/2001\/04\/xmlenc\#rsa\-oaep\-mgf1p](http://www.w3.org/2001/04/xmlenc)|1024|기본 합니다. 암호화 보안 토큰 암호화 대칭 키에 대해 알고리즘을 지원 됩니다.|  
|SHA1\ http: / / / \ / www.w3.org \/PICS\/DSig\/SHA1\_1\_0.html|N\/A|광고 FS 서버 아티팩트 SourceId 세대에서 사용 하는: STS이이 시나리오에서 SHA1 사용 \ (당 SAML 2.0 standard\에서 권장) 아티팩트 sourceiD에 대 한 간단한 160 비트 값을 생성 합니다.<br /><br />또한 웹 ADFS 에이전트 사용 \ (WS2003 timeframe\의 이전 구성 요소) "마지막 업데이트" 시간에 변경 내용을 확인 하 값 STS에서 정보를 업데이트 해야 하는 경우 알 수 있도록 합니다.|  
|SHA1withRSA\-<br /><br />http:///\/ www.w3.org \/PICS\/DSig\/RSA\-SHA1\_1\_0.html|N\/A|아티팩트 해상도 요청 또는 응답 로그인, token\ 서명 인증서를 만드는 경우에는 데 광고 FS 서버 SAML AuthenticationRequest 서명의 유효성을 검사.<br /><br />이러한 경우 대체로 SHA256 기본적으로 이며 SHA1 파트너 \(relying party\) SHA256 지원 되지 SHA1 사용 해야 하는 경우에 사용 됩니다.|  
  
## <a name="BKMK_13"></a>사용 권한 요구 사항  
Adfs의 초기 구성 하 고 설치를 수행 하는 관리자 관리자 권한이 있어야 도메인 로컬 도메인에 \ (즉, federation 서버가 연결 되어 있는 도메인. \)  
  
## <a name="see-also"></a>참조 하십시오  
[Windows Server 2012 r 2의 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

