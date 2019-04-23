---
ms.assetid: e2ad9e80-a036-4bac-a4fb-afa83756aa1f
title: Windows Server 2012 AD FS 배포 가이드
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3e555d1003878e12320cb8557bd205ac24e1bbb3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882444"
---
# <a name="windows-server-2012-ad-fs-deployment-guide"></a>Windows Server 2012 AD FS 배포 가이드

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory® Federation Services를 사용할 수 있습니다 \(AD FS\) 배포 된 id를 확장 하는 페더레이션된 id 관리 솔루션을 구축 하는 Windows Server® 2012 운영 체제를 사용 하 여 인증 하 고 권한 부여 서비스를 웹\-조직 및 플랫폼 경계를 넘어 응용 프로그램을 기반으로 합니다. AD FS를 배포하여 조직의 기존 ID 관리 기능을 인터넷으로 확장할 수 있습니다.  
  
AD FS를 배포하면 다음이 가능해집니다.  
  
-   웹을 사용 하 여 직원이 나 고객에 게 제공\-기준, 단일\-로그인\-에 \(SSO\) 환경에 대 한 원격 액세스를 내부적으로 필요할 때 웹 사이트 또는 서비스를 호스트 합니다.  
  
-   웹을 사용 하 여 직원이 나 고객에 게 제공\-간 액세스할 때 SSO 경험을 기반\-조직 웹 사이트 또는 네트워크의 방화벽 내에서 서비스 합니다.  
  
-   웹에 대 한 원활한 액세스를 사용 하 여 직원이 나 고객이 제공\-직원이 나 고객이 여러 번 로그온 할 필요 없이 인터넷에서 페더레이션 파트너 조직의 리소스에에서 기반 합니다.  
  
-   다른 로그인을 사용 하지 않고 완전히 제어할 직원 또는 고객 id 유지\-공급자 \(Windows Live ID, Liberty Alliance 등\)합니다.  
  
## <a name="about-this-guide"></a>이 가이드 정보  
이 가이드는 시스템 관리자 및 시스템 엔지니어용으로 작성되었습니다. 사용자나 조직의 인프라 전문가 또는 시스템 설계자가는 미리 선택 되어 있는 AD FS 디자인을 배포 하기 위한 구체적인된 지침을 제공 합니다.  
  
디자인을 아직 선택 하지 않은 경우의 디자인 옵션을 검토 한 후이 가이드의 지침에 따라 대기 하는 것이 좋습니다 합니다 [Windows Server 2012의 AD FS 디자인 가이드](https://technet.microsoft.com/library/dd807036.aspx) 가장 선택한 조직에 대 한 적절 한 설계 합니다. 이 가이드를 이미 선택 되었습니다. 디자인을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [AD FS 디자인 계획 구현](Implementing-Your-AD-FS-Design-Plan.md)합니다.  
  
디자인 가이드에서 디자인을 선택 하 고 클레임, 토큰 형식, 특성 저장소 및 기타 항목에 대 한 필요한 정보를 수집한 후에 프로덕션 환경에서 AD FS 디자인을 배포 하려면이 가이드를 사용할 수 있습니다. 이 가이드에서는 다음 기본 AD FS 디자인 중 하나를 배포 하는 것에 대 한 단계를 제공 합니다.  
  
-   웹 SSO  
  
-   페더레이션된 웹 SSO  
  
검사 목록을 사용 하 여 [AD FS 디자인 계획 구현](Implementing-Your-AD-FS-Design-Plan.md) 특정 디자인을 배포 하려면이 가이드의 지침을 사용 하 여 최상의 방법을 확인할 수 있습니다. AD FS 배포를 위한 하드웨어 및 소프트웨어 요구 사항에 대 한 자세한 내용은 참조는 [부록 a: AD FS 요구 사항 검토](https://technet.microsoft.com/library/ff678034.aspx) AD FS 디자인 가이드입니다.  
  
### <a name="what-this-guide-does-not-provide"></a>이 가이드에서 설명하지 않는 정보  
이 가이드에서는 다음 정보를 제공하지 않습니다.  
  
-   언제, 어디에 기존 네트워크 인프라에 페더레이션 서버, 페더레이션 서버 프록시 또는 웹 서버를 배치에 대 한 지침입니다. 이 정보를 참조 하세요 [페더레이션 서버 배치 계획](https://technet.microsoft.com/library/dd807069.aspx) 하 고 [페더레이션 서버 프록시 배치 계획](https://technet.microsoft.com/library/dd807130.aspx) AD FS 디자인 가이드에서.  
  
-   인증 기관 사용 하기 위한 지침 \(CAs\) AD FS를 설정 하려면  
  
-   설정 또는 특정 웹 구성 지침\-기반 응용 프로그램  
  
-   테스트 랩 환경 설정과 관련된 설정 지침.  
  
-   페더레이션된 로그온 화면, web.config 파일 또는 구성 데이터베이스 사용자 지정 방법에 대한 정보입니다.  
  
## <a name="in-this-guide"></a>이 가이드의 내용  
  
-   [AD FS 배포 계획](Planning-to-Deploy-AD-FS.md)  
  
-   [계획을 디자인 AD FS를 구현 합니다.](Implementing-Your-AD-FS-Design-Plan.md)  
  
-   [검사 목록: 웹 SSO 디자인 구현](Checklist--Implementing-a-Web-SSO-Design.md)  
  
-   [검사 목록: 페더레이션된 웹 SSO 디자인 구현](Checklist--Implementing-a-Federated-Web-SSO-Design.md)  
  
-   [파트너 조직 구성](Configuring-Partner-Organizations.md)  
  
-   [클레임 규칙 구성](Configuring-Claim-Rules.md)  
  
-   [페더레이션 서버를 배포합니다.](Deploying-Federation-Servers.md)  
  
-   [페더레이션 서버 프록시 배포](Deploying-Federation-Server-Proxies.md)  
  
-   [Interoperating with AD FS 1.x](Interoperating-with-AD-FS-1.x.md)  
