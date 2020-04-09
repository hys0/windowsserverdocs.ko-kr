---
ms.assetid: 68979914-8a1c-465a-bd37-08df30722d69
title: AD FS 디자인에 배포 목표 매핑
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 4154f46bdb1a7b3a2c81eba6882a6a095a16ee45
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853056"
---
# <a name="mapping-your-deployment-goals-to-an-ad-fs-design"></a>AD FS 디자인에 배포 목표 매핑


기존 Active Directory Federation Services \(AD FS\) 배포 목표 검토를 완료 하 고 배포에 관련 된 목표를 확인 한 후 해당 목표를 특정 AD FS 디자인에 매핑할 수 있습니다. AD FS 미리 정의 된 배포 목표에 대 한 자세한 내용은 [AD FS 배포 목표 파악](Identifying-Your-AD-FS-Deployment-Goals.md)을 참조 하세요.  
  
다음 표를 사용 하 여 조직에 대 한 AD FS 배포 목표의 적절 한 조합에 매핑할 AD FS 디자인을 결정 합니다. 이 표에서는이 가이드에 설명 된 대로 두 가지 기본 AD FS 설계만 참조 합니다. 그러나 조직의 요구를 충족 하기 위해 AD FS 배포 목표 조합을 사용 하 여 하이브리드 또는 사용자 지정 AD FS 디자인을 만들 수 있습니다.  
  
|AD FS 배포 목표|[웹 SSO 디자인](Web-SSO-Design.md)|[페더레이션된 웹 SSO 디자인](Federated-Web-SSO-Design.md)|  
|---------------------------------------------------------------------------|----------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|[Active Directory 사용자에게 클레임 인식 애플리케이션 및 서비스에 대한 액세스 제공](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)|아니요|예, 계정 파트너에서|  
|[Active Directory 사용자에게 다른 조직의 애플리케이션 및 서비스에 대한 액세스 제공](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)|아니요|예, 계정 파트너에서 선택 사항|  
|[다른 조직의 사용자에게 클레임 인식 애플리케이션 및 서비스에 대한 액세스 제공](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)|예|예|  

## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
  

