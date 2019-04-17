---
ms.assetid: 68979914-8a1c-465a-bd37-08df30722d69
title: "AD FS 디자인에 배포 목표 매핑"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 048bce75c52895b2d9e215bdccef9cb13dc23533
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="mapping-your-deployment-goals-to-an-ad-fs-design"></a>AD FS 디자인에 배포 목표 매핑

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기존 Active Directory Federation Services \(AD FS\) 배포 목표를 검토 하기 배포 관련 목표를 확인 한 후 특정 ADFS 디자인 목표 매핑할 수 있습니다. Adfs에 대 한 자세한 내용은 미리 배포 목표를에 대 한 참고 [AD FS 배포 목표 식별](Identifying-Your-AD-FS-Deployment-Goals.md)합니다.  
  
조직에 대 한 배포 목표 Adfs의 적절 한 조합 하는 ADFS 디자인 지도 확인 하려면 다음 표를 사용 합니다. 이 가이드에 설명 된 대로 두 가지 기본 ADFS 디자인에만이 표 참조 합니다. 그러나 하이브리드 또는 사용자 지정 ADFS 디자인 조직에서 요구 하 ADFS 배포 목표 조합을 사용 하 여 만들 수 있습니다.  
  
|광고 FS 배포 목표입니다.|[웹 SSO 디자인](Web-SSO-Design.md)|[연결 된 웹 SSO 디자인](Federated-Web-SSO-Design.md)|  
|---------------------------------------------------------------------------|----------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|[인식 클레임 응용 프로그램 및 서비스에 사용자 Active Directory 사용자가 액세스할 수 있도록](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)|아니요|예, 계정 파트너|  
|[응용 프로그램 및 서비스에서는 다른 조직의 Active Directory 사용자 액세스를 제공](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)|아니요|예, 계정 파트너의 옵션|  
|[조직에 대 한 또 다른 액세스에 사용자가 인식 클레임 응용 프로그램 및 서비스에 제공](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)|예|예|  

## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
  

