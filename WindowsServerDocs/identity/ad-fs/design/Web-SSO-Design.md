---
ms.assetid: eb778f63-f7be-438e-8c5e-1fd9b194b967
title: 웹 SSO 디자인
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 47c946ac617cc64c224c1bc3153fcaf55c2d069c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858516"
---
# <a name="web-sso-design"></a>웹 SSO 디자인

Active Directory Federation Services \(AD FS\)의 SSO\) 디자인에서 웹 Single\-Sign \(\-에서 한 번만 인증 해야 AD FS 보안 응용 프로그램 또는 서비스에 액세스할 수 있습니다.\- 이 디자인에서 모든 사용자는 외부 사용자이며, 파트너 조직이 없기 때문에 페더레이션 트러스트가 없습니다. 일반적으로 다음 그림에 나와 있는 것 처럼 인터넷을 통해 하나 이상의 AD FS 보안 서비스 또는 애플리케이션에 대 한 개별 소비자 또는 고객 액세스를 제공 하려는 경우이 디자인을 배포 합니다.  
  
![웹 sso 디자인](media/adfs2_WebSSODesign.gif)  
  
웹 SSO 디자인을 사용 하면 일반적으로 경계 네트워크에서 AD FS\-보안 응용 프로그램 또는 서비스를 호스트 하는 조직이 경계 네트워크에 고객 계정의 별도 저장소를 유지할 수 있으므로 고객 계정과 직원 계정을 쉽게 격리할 수 있습니다.  
  
Active Directory Domain Services \(AD DS\), SQL Server 또는 사용자 지정 특성 저장소 중 하나를 사용 하 여 경계 네트워크에 있는 고객의 로컬 계정을 관리할 수 있습니다.  
  
이 디자인은 [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)의 배포 목표와 일치합니다.  
  
계획 및 웹 SSO 디자인을 배포 하는 데 사용할 수 있는 세부 작업 목록은 참조 하십시오. [검사 목록: 웹 SSO 디자인 구현](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md)합니다.  
  
## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
