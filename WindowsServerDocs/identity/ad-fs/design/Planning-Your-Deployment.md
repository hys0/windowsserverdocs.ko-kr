---
ms.assetid: bb9b9e18-bf2f-4115-be77-9a165944db41
title: 배포 계획
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5c7cec9ad92605f3dc98f8ce8fb7853a7ae61299
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863694"
---
# <a name="planning-your-deployment"></a>배포 계획

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

계획할 때 교차\-조직 \(페더레이션\-기반\) Active Directory Federation Services를 사용 하 여 공동 작업 \(AD FS\)를 먼저 확인 조직 인터넷을 통해 다른 조직에서 액세스 하는 웹 리소스를 호스트 하는 경우 조직에서 직원에 대 한 웹 리소스에 대 한 액세스를 제공 합니다. 이 결정 AD FS를 배포 하는 방법에 영향을 줍니다. 및 AD FS 인프라에 대 한 계획의 기반이 됩니다.  
  
> [!NOTE]  
> 조직이 페더레이션 규약에서 수행하는 역할을 모든 사용자가 명확하게 이해하 고 있는지 확인합니다.  
  
에 대 한 합니다 [페더레이션된 웹 SSO 디자인](Federated-Web-SSO-Design.md), AD FS와 같은 용어를 사용 합니다 *계정 파트너* \(라고도 *id 공급자* ADFS관리스냅인\-에\) 하 고 *리소스 파트너* \(라고도 *신뢰 당사자* AD FS 관리 스냅인\-에서\) 를 계정을 호스트 하는 조직을 차별화 하는 데 도움이 \(계정 파트너\) 웹 호스트 하는 조직에서\-기반 리소스 \(리소스 파트너\)합니다.  
  
[Web SSO Design](Web-SSO-Design.md)에서는 조직이 사용자에게 해당 응용 프로그램에 대한 액세스 권한을 제공하므로 계정 파트너와 리소스 파트너의 역할을 모두 수행합니다.  
  
다음 항목에서는 AD FS의 일부 파트너 조직 개념을 설명 합니다. 또한 AD FS 배포 가이드에서 설정 및 계정 파트너 조직 및 리소스 파트너 조직의 AD FS 배포 목표에 따라 구성 하는 방법에 대 한 정보가 포함 된 항목의 링크를 포함 합니다.  
  
## <a name="in-this-section"></a>단원 내용  
  
-   [AD FS의 보안 계획 및 배포에 대 한 모범 사례](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)  
  
-   [AD FS와의 상호 운용성에 대 한 계획 1.x](Planning-for-Interoperability-with-AD-FS-1.x.md)  
  
-   [Id 위임을 사용 하는 경우](When-to-Use-Identity-Delegation.md)  
  
-   [계정 파트너 조직에서 AD FS를 배포합니다.](Deploying-AD-FS-in-the-Account-Partner-Organization-2012.md)  
  
-   [리소스 파트너 조직에서 AD FS를 배포합니다.](Deploying-AD-FS-in-the-Resource-Partner-Organization-2012.md)  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의에서 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)


