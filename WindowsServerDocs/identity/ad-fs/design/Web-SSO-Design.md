---
ms.assetid: eb778f63-f7be-438e-8c5e-1fd9b194b967
title: "웹 SSO 디자인"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1b8344594c9fc477ed8424c716ec8d7f7fd91ef3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="web-sso-design"></a>웹 SSO 디자인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

웹에서 Active Directory Federation Services \(AD FS\) Single\ Sign\-켜 짐 \(SSO\) 디자인 사용자 여러 광고 FS\ 보안 응용 프로그램 또는 서비스에 액세스할 한 번만 인증 해야 합니다. 이 디자인 모든 사용자가 외부 및 federation 신뢰 하지 파트너 않았기 때문에 문제가 발생 합니다. 일반적으로 다음과 같이 인터넷을 통해 하나 이상의 FS-보안 서비스 광고 또는 응용 프로그램에 대 한 개별 소비자 또는 고객 액세스를 제공 하려는 경우이 디자인을 배포 됩니다.  
  
![웹 sso 디자인](media/adfs2_WebSSODesign.gif)  
  
웹 SSO 일반적으로 응용 프로그램 광고 FS\ 보안 호스트 하는 조직 디자인 하거나 주변 네트워크의 서비스 격리할 직원 계정에서 고객 계정을 쉽게 주변 네트워크에 있는 고객 계정의 별도 저장소를 유지할 수 있습니다.  
  
Active Directory 도메인 서비스 \(AD DS\), SQL Server 또는 사용자 지정 된 특성 저장소를 사용 하 여 주변 네트워크에 있는 고객을 위한 로컬 계정을 관리할 수 있습니다.  
  
이 디자인에 배포 목표에 맞춰 [제공 나만의 Active Directory 사용자에 대 한 액세스 클레임 인식 나만의 응용 프로그램과 서비스](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)합니다.  
  
계획 하 고 웹 SSO 디자인 배포 사용할 수 있는 작업 자세한 목록은 [검사: 웹 SSO 디자인을 구현](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md)합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
