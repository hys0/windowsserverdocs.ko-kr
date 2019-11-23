---
ms.assetid: bb9b9e18-bf2f-4115-be77-9a165944db41
title: 배포 계획
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 607dc34c8f44d8d96a8dc0c9d1ed004edc799167
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407993"
---
# <a name="planning-your-deployment"></a>배포 계획

Active Directory Federation Services \(AD FS를 사용 하는\) 공동 작업을 기반으로 하\-조직 \(페더레이션\-를 계획 하는 경우 먼저 조직에서 인터넷을 통해 다른 조직에서 액세스할 웹 리소스를 호스팅하거나 조직의 직원에 게 웹 리소스에 대 한 액세스 권한을 제공 하는지 확인 합니다.\) 이러한 결정은 AD FS를 배포 하는 방법에 영향을 주며, AD FS 인프라 계획의 기반이 됩니다.  
  
> [!NOTE]  
> 조직이 페더레이션 규약에서 수행하는 역할을 모든 사용자가 명확하게 이해하 고 있는지 확인합니다.  
  
[페더레이션된 웹 SSO 디자인](Federated-Web-SSO-Design.md)의 경우, AD FS *계정 파트너* \(AD FS 관리\-스냅인의 *id 공급자* 라고도 하는 용어를 사용 하 여\)의 \(관리 스냅인에서 신뢰 당사자 *라고도 하며* , AD FS의\-관리 스냅인에서 *신뢰 당사자* 라고도 하며,이를 통해 계정 파트너\) 계정을 호스트 하는 조직이 웹 \(기반 리소스를 호스트 하는 조직에서\)\-리소스 파트너\)입니다.\(  
  
[Web SSO Design](Web-SSO-Design.md)에서는 조직이 사용자에게 해당 응용 프로그램에 대한 액세스 권한을 제공하므로 계정 파트너와 리소스 파트너의 역할을 모두 수행합니다.  
  
다음 항목에서는 AD FS 파트너 조직 개념 중 일부에 대해 설명 합니다. 또한 AD FS 배포 목표에 따라 계정 파트너 조직 및 리소스 파트너 조직의 설정 및 구성에 대 한 정보를 포함 하는 AD FS 배포 가이드의 항목에 대 한 링크도 포함 되어 있습니다.  
  
## <a name="in-this-section"></a>단원 내용  
  
-   [AD FS 보안 계획 및 배포 모범 사례](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)  
  
-   [AD FS 1.x와의 상호 운용성 계획](Planning-for-Interoperability-with-AD-FS-1.x.md)  
  
-   [Id 위임을 사용 하는 경우](When-to-Use-Identity-Delegation.md)  
  
-   [계정 파트너 조직에서 AD FS 배포](Deploying-AD-FS-in-the-Account-Partner-Organization-2012.md)  
  
-   [리소스 파트너 조직에 AD FS 배포](Deploying-AD-FS-in-the-Resource-Partner-Organization-2012.md)  
  
## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)


