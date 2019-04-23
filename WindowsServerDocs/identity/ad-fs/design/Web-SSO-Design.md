---
ms.assetid: eb778f63-f7be-438e-8c5e-1fd9b194b967
title: 웹 SSO 디자인
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1b8344594c9fc477ed8424c716ec8d7f7fd91ef3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852804"
---
# <a name="web-sso-design"></a>웹 SSO 디자인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

단일 웹\-기호\-온 \(SSO\) Active Directory Federation Services에서 디자인 \(AD FS\), 여러 AD FS에 액세스 하려면 사용자는 한 번만 인증 해야\- 보안된 응용 프로그램 또는 서비스입니다. 이 디자인에서 모든 사용자는 외부 사용자이며, 파트너 조직이 없기 때문에 페더레이션 트러스트가 없습니다. 일반적으로 다음 그림에 나와 있는 것 처럼 인터넷을 통해 하나 이상의 AD FS 보안 서비스 또는 응용 프로그램에 대 한 개별 소비자 또는 고객 액세스를 제공 하려는 경우이 디자인을 배포 합니다.  
  
![웹 sso 디자인](media/adfs2_WebSSODesign.gif)  
  
웹 SSO 디자인을 조직 일반적으로 호스팅하는 AD FS\-보안된 응용 프로그램 또는 서비스 경계 네트워크에 쉽게 고객 격리 경계 네트워크에 고객 계정의 별도 저장소를 유지할 수 있습니다 계정과 직원 계정 합니다.  
  
Active Directory 도메인 서비스를 사용 하 여 경계 네트워크에서에서 고객에 대 한 로컬 계정을 관리할 수 있습니다 \(AD DS\), SQL Server, 또는 사용자 지정 특성 저장소입니다.  
  
이 디자인은 [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)의 배포 목표와 일치합니다.  
  
에서 사용자 웹 SSO 디자인 계획 및 배포에 사용할 수 있는 세부 작업 목록은 참조 하세요. [검사 목록: 웹 SSO 디자인 구현](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md)합니다.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의에서 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
