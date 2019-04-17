---
ms.assetid: 204f5fe9-3611-4da0-b057-a386004b4598
title: "주요 Active Directory Federation Services 개념을 이해합니다."
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 27282c6b88b0457af3b4cf031fdadced7b40268c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="understanding-key-ad-fs-concepts"></a>주요 광고 FS 개념을 이해합니다.
Active Directory Federation Services에 대 한 중요 한 개념 알아봅니다 하 고 그 기능 집합 익힐 것이 좋습니다.  
  
> [!TIP]  
> 추가 ADFS 리소스 링크에서 찾을 수는 [광고 FS 콘텐츠 지도](https://social.technet.microsoft.com/wiki/contents/articles/2735.aspx) Microsoft TechNet wiki 페이지 합니다. 이 페이지는 광고 FS 커뮤니티의 회원 하 여 관리 되 고 광고 FS 제품 팀에서를 정기적으로 모니터링 합니다.  
  
## <a name="ad-fs-terminology-used-in-this-guide"></a>이 가이드에 사용 되는 광고 FS 용어  
  
|광고 FS 용어|정의|  
|--------------|--------------|  
|계정 파트너 조직|표시 되는 Federation 서비스에 클레임 공급자 신뢰 하는 federation 파트너 조직 합니다. 계정 파트너 조직 리소스 파트너에 Web\ 기반 응용 프로그램에 액세스 하는 사용자가 포함 되어 있습니다.|  
|계정 federation 서버|계정 파트너 조직에서 federation 서버 합니다. 계정 federation 서버 인증 사용자에 따라 사용자에 게 보안 토큰 문제입니다. 서버에서 사용자를 인증, 관련 특성과 특성 저장소 그룹 구성원 정보를 추출, 청구에이 정보가 및 생성 및 보안 토큰 서명 \ (의 claims\ 포함)는 사용자에 게 돌아가려면-자체 조직에서 사용할 수 있도록 하거나 파트너 조직에 전송 되어야 합니다.|  
|광고 FS 구성 데이터베이스|단일 인스턴스 ADFS 또는 Federation 서비스를 나타내는 데이터베이스 구성 모든 데이터를 저장 하는 데 사용 합니다. 이 구성 데이터 SQL Server 데이터베이스에 저장 될 수 있는 또는 Windows Server 2016, Windows Server 2012 및 2012 R2, 및 Windows Server 2008, 2008 R2 포함 내부 데이터베이스 Windows 기능을 사용 합니다. </br></br>ADFS 구성 데이터베이스 Fsconfig.exe command\ 선 도구를 사용 하 여 SQL Server 하 고 Windows 내부 데이터베이스 AD FS Federation 서버 구성 마법사를 사용 하 여 만들 수 있습니다.|  
|청구 공급자|클레임을 사용자에 게 제공 하는 조직의 합니다. 계정 파트너 조직을 참조 하십시오.|  
|청구 공급자 보안|Snap\에서 광고 FS 관리, 청구 제공자 신뢰는 신뢰 개체 계정의 리소스 파트너 조직에서 리소스에 액세스할 수는 보안 관계에는 조직 나타내는 데 리소스 파트너 조직에서 일반적으로 만듭니다. 청구 공급자 신뢰 개체 식별자, 이름과 로컬 Federation 서비스에는이 파트너 식별 하는 규칙의 다양 한 구성 됩니다.|  
|로컬 클레임 공급자 보안|신뢰 개체 광고 LDS third\ 자 LDAP\ 기반의 또는 디렉터리 ADFS 농장 나타내는입니다. 로컬 주장 공급자 신뢰 개체 식별자, 이름과이 LDAP\ 기반 디렉터리 로컬 Federation 서비스를 식별 하는 규칙의 다양 한 구성 됩니다.|  
|Federation 메타 데이터|청구 공급자와 당사자를 클레임 제공자 신뢰 하 고 신뢰 파티 신뢰의 적절 한 구성 돕기 위해 간의 구성 정보 교환 데이터 형식 있습니다. 데이터 형식 보안 설정 Markup Language \(SAML\) 2.0에에서 정의 되 고 WS\ 연합에서 확장 됩니다.|  
|Federation 서버|Windows Server AD FS Federation 서버 구성 마법사를 사용 하 여 federation 서버 역할을 수행할 구성 된 합니다. Federation 서버 토큰 고 Federation 서비스의 일부로 제공 됩니다.|  
|Federation 서버 프록시|AD Federation 서버 FS 프록시 구성을 마법사를 사용 하 여 역할을 구성 하는 Windows Server 중간 프록시 인터넷 클라이언트와 회사 네트워크에서 방화벽을 뒤에 있는 Federation 서비스 간의 서비스 합니다.|  
|기본 federation 서버|Windows 서버 AD FS Federation 서버 구성 마법사를 사용 하 여 federation 서버 역할에서 구성 되어 있고 ADFS 구성 데이터베이스 read\/쓰기 복사본입니다. </br></br> 기본 federation 서버 AD FS Federation 서버 구성 마법사를 사용 하 고 새 Federation 서비스를 만들고 그룹에서 해당 컴퓨터 첫 번째 federation 서버를 확인 하는 옵션을 선택 하면 만들어집니다. 이 그룹에 다른 모든 federation 서버를 read\ 전용 로컬로 저장 되어 있는 ADFS 구성 데이터베이스의 기본 federation 서버에 변경한 복제 해야 합니다. ADFS 구성 데이터베이스 동일 하 게 읽기 하 고 SQL Server에 저장 된 구성 데이터베이스에 쓸 수 있는 모든 federation 서버 SQL 데이터베이스에 저장 된 경우에 "주 federation 서버" 라는 용어 적용 되지 않습니다.|  
|당사자|수신 하 고 처리 하는 클레임 조직입니다. 파트너 조직을 리소스를 참조 하십시오.|  
|파티 신뢰 사용|snap\ AD FS 관리에 의존 파티 신뢰는 신뢰 개체 일반적으로에 만들어집니다.<br /><br />계정 파트너 조직 계정의 리소스 파트너 조직에서 리소스에 액세스할 수는 보안 관계에는 조직 일을 합니다.<br />파트너 조직 Federation 서비스 간의 단일 web\ 기반 응용 프로그램이 신뢰를 나타내는 데 리소스 합니다.<br /><br />신뢰 파티 신뢰 개체 식별자, 이름과이 파트너 또는 로컬 Federation 서비스 web\ 응용 프로그램을 식별 하는 규칙의 다양 한 구성 됩니다.|  
|리소스 federation 서버|Federation 서버 리소스 파트너 조직에서 합니다. 리소스 federation 서버는 일반적으로 계정 federation 서버에서 발행 보안 토큰에 따라 사용자에 게 보안 토큰 문제 합니다. 서버 보안 토큰 수신, 서명을 확인, 클레임 규칙 논리를 원하는 보내는 클레임 생성할 패키지가 해제 클레임에 적용 됩니다., 새 보안 토큰 생성 \ 수신 보안 토큰의 정보에 따라 (와 보내는 claims\) 및 사용자에 게을 반환 하는 새로운 토큰 서명 및 결국 웹 응용 프로그램입니다.|  
|파트너 조직 리소스|표시 되는 Federation 서비스에 신뢰 파티 신뢰 하는 federation 파트너 합니다. 리소스 파트너 사용자의 계정 파트너에 액세스할 수 있는 게시 Web\ 기반 응용 프로그램이 포함 된 보안 claims\ 기반 토큰 발행 합니다.|  
  
## <a name="overview-of-ad-fs"></a>Adfs의 개요  
ADFS 클라이언트 컴퓨터를 제공 하는 id 액세스 솔루션은 \ (내부 또는 외부에 network\) 보호 Internet\ 연결 응용 프로그램 또는 서비스 사용자 계정 및 응용 프로그램 조직 또는 완전히 다른 네트워크에 있는 경우에 원활 하 게 SSO 액세스할 수 있는 합니다.  
  
응용 프로그램 또는 서비스가 한 네트워크에는 다른 네트워크에 사용자 계정이 될 때 일반적으로 사용자가 메시지가 표시 되 면 보조 자격 증명을 응용 프로그램 또는 서비스에 액세스 하려고 할 때입니다. 이러한 보조 자격 증명 응용 프로그램 또는 서비스가 있는 영역에는 사용자의 id를 나타냅니다. 일반적으로에서 요구 하는 가장 적합 한 승인 결정을 내릴 수 있도록 응용 프로그램 또는 서비스 호스트 하는 웹 서버 합니다.  
  
ADFS 조직 이러한 조직의 신뢰할 수 있는 파트너에 대 한 사용자의 디지털 id 및 액세스 권한을 프로젝 팅 하는 데 사용할 수 있는 보안 관계 \(federation trusts\) 제공 하 여 보조 자격 증명에 대 한 요청을 우회할 수 있습니다. 이 연결 된 환경에서 각 조직 계속 고유 id 관리 하지만 각 조직 안전 하 게 프로젝 팅 하 고 다른 조직의 id를에서 수락 합니다.  
  
-   [역할의 특성 스토어](The-Role-of-Attribute-Stores.md)  
  
-   [AD FS 구성 데이터베이스의 역할](The-Role-of-the-AD-FS-Configuration-Database.md)  
  
-   [클레임 역할](The-Role-of-Claims.md)  
  
-   [클레임은 규칙의 역할](The-Role-of-Claim-Rules.md)  
  
-   [클레임 엔진 역할](The-Role-of-the-Claims-Engine.md)  
  
-   [클레임 파이프라인 역할](The-Role-of-the-Claims-Pipeline.md)  
  
-   [클레임은 규칙 언어의 역할](The-Role-of-the-Claim-Rule-Language.md)  
  
-   [사용 하 여 청구 규칙 서식 파일 형식을 확인합니다](Determine-the-Type-of-Claim-Rule-Template-to-Use.md)  
  
-   [Adfs의 Uri 사용 방법](How-URIs-Are-Used-in-AD-FS.md)  
  

