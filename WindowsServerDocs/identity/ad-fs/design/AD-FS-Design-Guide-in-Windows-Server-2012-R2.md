---
ms.assetid: a8558c9d-0606-4881-93b2-f2d2716b18e7
title: "Windows Server 2012 r 2의 지침에 따라 AD FS 디자인"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 498b399818fb8c9e463f9990fa13c87648c0a33d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="ad-fs-design-guide-in-windows-server-2012-r2"></a>Windows Server 2012 r 2의 지침에 따라 AD FS 디자인

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

Active Directory Federation Services \(AD FS\) 최종 사용자에 게 광고 FS\ 보안 엔터프라이즈, federation 파트너 조직 또는 클라우드 내 응용 프로그램에 액세스 하려면 간단한 보안된 id 연합과 웹 단일 sign\ 켜 짐 \(SSO\) 기능을 제공 합니다.  
  
® Windows Server 2012 r 2 ADFS 포함 역할을 제공 하는 federation 서비스 역할 서비스 \ (보안 토큰과 광고 FS\ 신뢰 하는 응용 프로그램을 제공 하기 위해 사용자가 인증) 또는 federation 공급자로 \ (다른 id 공급자 로부터 토큰 소모 하 고 보안 토큰과 광고 FS\ 신뢰 하는 응용 프로그램을 제공 합니다).  
  
엑스트라넷 액세스 응용 프로그램 및 ADFS Windows Server 2012 r 2에 의해 보호 되는 서비스를 제공 하는 기능을 이제 웹 응용 프로그램 프록시 라는 새로운 원격 액세스 역할 서비스가 수행 합니다. 이전 버전의 Windows Server는이 기능이 ADFS federation 서버 프록시 처리 되었는지의 출발입니다. 웹 응용 프로그램 프록시 서버 역할 광고 FS\ 관련 익스트라넷 시나리오 및 기타 익스트라넷에서 대 한 액세스를 제공 하도록 설계 된입니다. 에 대 한 자세한 내용은 웹 응용 프로그램 프록시, [웹 응용 프로그램 프록시 연습 가이드](https://technet.microsoft.com/library/dn280944.aspx)합니다.  
  
## <a name="about-this-guide"></a>이 가이드 정보  
이 가이드에서는 조직의 요구 사항에 따라 Adfs의 새 배포를 계획 하는 데 도움이 되는 추천을 제공 합니다. 이 가이드는 인프라 전문가 또는 시스템 설계자 사용에 대 한 것입니다. ADFS 배포 계획할 주 결정 지점 강조 표시 합니다. 이 가이드를 읽으려면 먼저 ADFS 기능 수준에서 작동 하는 방법을는 잘 알고가 있어야 합니다. 자세한 내용은 참조 [이해 키 광고 FS 개념](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)합니다.  
  
## <a name="in-this-guide"></a>이 가이드  
  
-   [광고 FS 배포 목표에 사용자의 신원을 확인합니다](Identify-Your-AD-FS-Deployment-Goals.md)  
  
-   [해당 AD FS 배포가 계획](Plan-Your-AD-FS-Deployment-Topology.md)  
  
-   [광고 FS 요구 사항](AD-FS-Requirements.md)  
  
  
## <a name="see-also"></a>참조 하십시오  
[광고 FS 디자인](../../ad-fs/AD-FS-Design.md)  
  

