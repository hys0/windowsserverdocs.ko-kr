---
ms.assetid: e2ad9e80-a036-4bac-a4fb-afa83756aa1f
title: "Windows Server 2012 광고 FS 배포 가이드"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3e555d1003878e12320cb8557bd205ac24e1bbb3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="windows-server-2012-ad-fs-deployment-guide"></a>Windows Server 2012 광고 FS 배포 가이드

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

빌드 조직 및 플랫폼 경계 전체 분산된 id, 인증, 및 인증 Web\ 기반 응용 프로그램 서비스를 확장 하 여 연결 된 id 관리 솔루션 Active Directory Federation 서비스® \(AD FS\)® Windows Server 2012 운영 체제에 사용할 수 있습니다. Adfs을 배포 하 여 인터넷에 기존 신원을 관리 기능 조직의 확장할 수 있습니다.  
  
ADFS 배포할 수 있습니다.  
  
-   호스팅된 내부적으로 웹 사이트 또는 서비스에 대 한 원격 액세스 필요할 때 직원 나 고객 Web\ 기반, single\ sign\-켜 짐 \(SSO\) 환경이 제공 합니다.  
  
-   조직 cross\ 웹 사이트 또는 서비스에서 내 네트워크 방화벽 액세스할 때 직원 나 고객 Web\ 기반 SSO 환경이 제공 합니다.  
  
-   두 번 이상 로그인에 사용한 직원 나 고객을 않고도 인터넷에서 모든 federation 파트너 조직의 Web\ 기반 리소스를 원활 하 게 액세스할 수 있는 직원 나 고객을 제공 합니다.  
  
-   다른 sign\에서 공급자를 사용 하지 않고 직원 또는 고객이 id 완전히 제어할 유지 \ (Windows Live ID, 자유롭게 Alliance 및 others\).  
  
## <a name="about-this-guide"></a>이 가이드 정보  
이 가이드는 시스템 관리자 및 시스템 엔지니어 사용에 대 한 것입니다. 배포 하는 또는 조직에서 인프라 전문가 또는 시스템 설계자 미리 선택 되어 있는 ADFS 디자인에 대 한 자세한 지침을 제공 합니다.  
  
디자인 아직 선택 하지 않은 경우 지침을 따르지 될 때까지이 가이드에서 옵션 디자인을 검토 한 후 기다리는 것이 좋습니다는 [Windows Server 2012에서 광고 FS 디자인 가이드](https://technet.microsoft.com/library/dd807036.aspx) 하 고 조직에 대 한 가장 적합 한 디자인 선택한 합니다. 이 가이드를 사용 하 여 이미 선택 하는 디자인에 대 한 자세한 내용은 참조 [AD FS 디자인 계획 구현](Implementing-Your-AD-FS-Design-Plan.md)합니다.  
  
디자인 가이드에서 디자인을 선택 하 고 필요한 클레임, 토큰 형식, 특성 저장소 및 기타 항목에 대 한 정보를 수집 후 ADFS 디자인 생산 환경에서 배포 하는이 가이드를 사용할 수 있습니다. 이 가이드 다음과 같은 기본 ADFS 디자인 중 하나가 배포를 위해 단계를 제공 합니다.  
  
-   웹 SSO  
  
-   연결 된 웹 SSO  
  
검사에서 목록을 사용 [AD FS 디자인 계획 구현](Implementing-Your-AD-FS-Design-Plan.md) 을 배포 하는 특정 디자인이 가이드에서는 지침을 사용 하는 방법을 찾습니다. ADFS 배포 하기 위한 하드웨어 및 소프트웨어 요구 사항에 대 한 정보를 참조 하세요.는 [FS 요구 부록 a: 검토 AD](https://technet.microsoft.com/library/ff678034.aspx) AD FS 디자인 가이드에 있습니다.  
  
### <a name="what-this-guide-does-not-provide"></a>이 가이드 제공 하지 않는 항목  
이 가이드 제공 하지 않습니다.  
  
-   위치 기존 네트워크 인프라에 federation 서버, federation 서버 프록시 또는 웹 서버를 및 시기에 대해 안내 합니다. 이 정보를 참조 하세요. [계획 Federation 서버 배치](https://technet.microsoft.com/library/dd807069.aspx) 및 [Federation 서버 프록시 배치](https://technet.microsoft.com/library/dd807130.aspx) AD FS 디자인 가이드에 있습니다.  
  
-   인증 기관 \(CAs\) Adfs를 설정 하는 데 사용 되는 지침  
  
-   설정 하거나 특정 Web\ 기반 응용 프로그램 구성에 대 한 지침  
  
-   설치 지침 테스트 랩 환경을 설정 관련 된 합니다.  
  
-   로그온 연결 된 화면, web.config 파일 또는 구성 데이터베이스를 사용자 지정 하는 방법에 대 한 정보입니다.  
  
## <a name="in-this-guide"></a>이 가이드  
  
-   [ADFS 배포를 계획 하](Planning-to-Deploy-AD-FS.md)  
  
-   [요금제 여 ADFS 구현 디자인](Implementing-Your-AD-FS-Design-Plan.md)  
  
-   [웹 SSO 디자인을 구현 검사:](Checklist--Implementing-a-Web-SSO-Design.md)  
  
-   [연합된 웹 SSO 디자인을 구현 검사:](Checklist--Implementing-a-Federated-Web-SSO-Design.md)  
  
-   [파트너 조직 구성](Configuring-Partner-Organizations.md)  
  
-   [클레임은 규칙 구성](Configuring-Claim-Rules.md)  
  
-   [Federation 서버를 배포](Deploying-Federation-Servers.md)  
  
-   [Federation 서버 프록시 배포](Deploying-Federation-Server-Proxies.md)  
  
-   [Adfs와 상호 작용 1.x](Interoperating-with-AD-FS-1.x.md)  
