---
ms.assetid: bb9b9e18-bf2f-4115-be77-9a165944db41
title: "배포를 계획"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5c7cec9ad92605f3dc98f8ce8fb7853a7ae61299
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="planning-your-deployment"></a>배포를 계획

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

\(AD FS\) Active Directory Federation Services를 사용 하 여 cross\ 조직 \(federation\-based\) 공동 작업에 대 한 계획 하는 경우 먼저 확인 조직 웹 리소스에는 인터넷을 통해 다른 조직에서 액세스할 수 호스팅할 또는 조직에서 직원 웹 리소스에 대 한 액세스를 제공 됩니다. 이 결정 Adfs을 배포 하는 방법에 영향을 아니며 ADFS 인프라 계획 기반이 합니다.  
  
> [!NOTE]  
> 역할 조직에는 federation 계약 모든 참가자가 명확 하 게 이해할가 있는지 확인 합니다.  
  
에 대 한는 [웹 SSO 디자인 연방](Federated-Web-SSO-Design.md), ADFS 사용 약관와 같은 *계정 파트너* \ (라고도 함 *id 공급자* AD FS 관리 snap\ in\에서) 및 *리소스 파트너* \ (라고도 함 *당사자* AD FS 관리 snap\ in\에서) 계정을 호스트 조직 구별 하기 위해 \(the account partner\) Web\ 기반 리소스 호스트 하는 조직에서 \(the resource partner\) 합니다.  
  
에 [웹 SSO 디자인](Web-SSO-Design.md), 사용자에 게 해당 응용 프로그램에 대 한 액세스를 제공 하므로 조직 계정 파트너 및 리소스 파트너 역할 둘 다에서 작동 합니다.  
  
조직 개념 파트너는 Adfs의 몇 가지 다음 항목에 설명 합니다. 또한 광고 FS 배포 가이드 설정 및 계정 파트너 조직 및 리소스 파트너 조직 ADFS 배포 목표에 따라 구성에 관한 정보가 포함 된 항목에 대 한 링크가 포함 합니다.  
  
## <a name="in-this-section"></a>이 섹션에서  
  
-   [보안 및 배포 Adfs의에 대 한 유용한](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)  
  
-   [Adfs의 상호 운용성 계획 1.x](Planning-for-Interoperability-with-AD-FS-1.x.md)  
  
-   [신원을 위임 사용 하는 경우](When-to-Use-Identity-Delegation.md)  
  
-   [계정 파트너 조직에서 ADFS 배포](Deploying-AD-FS-in-the-Account-Partner-Organization-2012.md)  
  
-   [ADFS 리소스 파트너 조직에서 배포](Deploying-AD-FS-in-the-Resource-Partner-Organization-2012.md)  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)


