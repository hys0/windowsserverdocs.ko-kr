---
ms.assetid: e2ad9e80-a036-4bac-a4fb-afa83756aa1f
title: Windows Server 2012 AD FS 배포 가이드
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 1597230fcfde4fe8a9767f0f14c634bc6fabdceb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408250"
---
# <a name="windows-server-2012-ad-fs-deployment-guide"></a>Windows Server 2012 AD FS 배포 가이드


Windows Server® 2012 운영 체제에서 \(페더레이션\) 서비스 AD FS Active Directory®를 사용 하 여 분산 된 식별, 인증 및를 확장 하는 페더레이션된 id 관리 솔루션을 빌드할 수 있습니다. 조직 및 플랫폼 경계\-에 걸친 웹 기반 응용 프로그램에 대 한 권한 부여 서비스. AD FS를 배포 하 여 조직의 기존 id 관리 기능을 인터넷으로 확장할 수 있습니다.  
  
AD FS를 배포하면 다음이 가능해집니다.  
  
-   직원이 나 고객이 내부적으로 호스트 되는\-웹 사이트 또는 서비스\-에 원격\) 으로 액세스 해야 할 때 웹 기반 sso (single\-sign on \()를 제공 합니다.  
  
-   네트워크 방화벽 내에서 조직 간\-\-웹 사이트 또는 서비스에 액세스할 때 직원이 나 고객에 게 웹 기반 SSO 환경을 제공 합니다.  
  
-   직원이 나 고객이 여러 번 로그온 할 필요 없이 인터넷\-에 있는 모든 페더레이션 파트너 조직의 웹 기반 리소스에 원활 하 게 액세스할 수 있도록 직원 또는 고객에 게 제공 합니다.  
  
-   다른 로그인\-공급자 \(Windows Live ID,\)Liberty 동맹 및 기타를 사용 하지 않고도 직원 또는 고객 id에 대 한 완전 한 제어를 유지 합니다.  
  
## <a name="about-this-guide"></a>이 가이드 정보  
이 가이드는 시스템 관리자 및 시스템 엔지니어용으로 작성되었습니다. 사용자 또는 조직의 인프라 전문가 또는 시스템 설계자가 미리 선택 하 여 AD FS 디자인을 배포 하는 방법에 대 한 자세한 지침을 제공 합니다.  
  
디자인을 아직 선택 하지 않은 경우에는 [Windows Server 2012의 AD FS 디자인 가이드](https://technet.microsoft.com/library/dd807036.aspx) 에서 디자인 옵션을 검토 하 고 다음에 가장 적합 한 디자인을 선택한 후까지이 가이드의 지침을 따르는 것이 좋습니다. 직. 이미 선택한 디자인에이 가이드를 사용 하는 방법에 대 한 자세한 내용은 [AD FS 디자인 계획 구현](Implementing-Your-AD-FS-Design-Plan.md)을 참조 하세요.  
  
디자인 가이드에서 디자인을 선택 하 고 클레임, 토큰 형식, 특성 저장소 및 기타 항목에 대 한 필요한 정보를 수집한 후이 가이드를 사용 하 여 프로덕션 환경에 AD FS 디자인을 배포할 수 있습니다. 이 가이드에서는 다음과 같은 기본 AD FS 디자인 중 하나를 배포 하는 단계를 제공 합니다.  
  
-   웹 SSO  
  
-   페더레이션된 웹 SSO  
  
[AD FS 디자인 계획 구현](Implementing-Your-AD-FS-Design-Plan.md) 의 검사 목록을 사용 하 여이 가이드의 지침을 사용 하 여 특정 디자인을 배포 하는 데 가장 적합 한 방법을 결정 합니다. AD FS 배포를 위한 하드웨어 및 소프트웨어 요구 사항에 대 한 자세한 [내용은 부록 a: AD FS 디자인 가이드](https://technet.microsoft.com/library/ff678034.aspx) 에서 AD FS 요구 사항을 검토 합니다.  
  
### <a name="what-this-guide-does-not-provide"></a>이 가이드에서 설명하지 않는 정보  
이 가이드에서는 다음 정보를 제공하지 않습니다.  
  
-   기존 네트워크 인프라에서 페더레이션 서버, 페더레이션 서버 프록시 또는 웹 서버를 어디에 배치할지와 어디에 대 한 지침을 제공 합니다. 이 정보는 AD FS 디자인 가이드에서 [페더레이션 서버 배치 계획](https://technet.microsoft.com/library/dd807069.aspx) 및 [페더레이션 서버 프록시 배치 계획](https://technet.microsoft.com/library/dd807130.aspx) 을 참조 하세요.  
  
-   인증 기관 \(ca\) 를 사용 하 여 AD FS 설정 하기 위한 지침  
  
-   특정 웹\-기반 응용 프로그램 설정 또는 구성 지침  
  
-   테스트 랩 환경 설정과 관련된 설정 지침.  
  
-   페더레이션된 로그온 화면, web.config 파일 또는 구성 데이터베이스 사용자 지정 방법에 대한 정보입니다.  
  
## <a name="in-this-guide"></a>이 가이드의 내용  
  
-   [AD FS 배포 계획](Planning-to-Deploy-AD-FS.md)  
  
-   [AD FS 디자인 계획 구현](Implementing-Your-AD-FS-Design-Plan.md)  
  
-   [검사 목록: 웹 SSO 디자인 구현](Checklist--Implementing-a-Web-SSO-Design.md)  
  
-   [검사 목록: 페더레이션된 웹 SSO 디자인 구현](Checklist--Implementing-a-Federated-Web-SSO-Design.md)  
  
-   [파트너 조직 구성](Configuring-Partner-Organizations.md)  
  
-   [클레임 규칙 구성](Configuring-Claim-Rules.md)  
  
-   [페더레이션 서버 배포](Deploying-Federation-Servers.md)  
  
-   [페더레이션 서버 프록시 배포](Deploying-Federation-Server-Proxies.md)  
  
-   [AD FS 1.x와 상호 운용](Interoperating-with-AD-FS-1.x.md)  
