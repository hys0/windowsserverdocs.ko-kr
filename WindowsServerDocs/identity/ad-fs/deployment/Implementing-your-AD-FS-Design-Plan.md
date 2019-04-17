---
ms.assetid: d04dd17e-a843-46fd-8711-0039918f92d9
title: "요금제 여 ADFS 구현 디자인"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 31c2e048c3c125d0ea60610b049501151d7aa823
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="implementing-your-ad-fs-design-plan"></a>요금제 여 ADFS 구현 디자인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다음 환경 조건 및 요구 사항은 Active Directory Federation Services \(AD FS\) 디자인 요금제 여 구현에서 중요 한 요소는 다음과 같습니다.  
  
-   **파트너 지원:** 파트너 조직에서 작동 하도록 ADFS 일반적으로 사용 됩니다. 신원을 federation를 설정 하기 위해 파트너 관계를 원하는 조직에서 결정 합니다. 광고 기본 FS 배포 장소에 포함 된 후 파트너 추가 하 고, 파트너, 삭제, 파트너 정보를 업데이트 해야 파트너와 함께 작동 합니다. 파트너 관계에 대 한 변경에 대 한 다양 한 이유로 인해 발생할 수 있습니다. 예를 들어, ADFS 배포 파트너의 비즈니스 크게 변경 큰 회사나 조직 연합의 일부가 조직 또는 조직은 다른 회사에서 얻은 경우 간 산학 협동 업데이트 필요할 수 있습니다. 여러 도메인의 id를 연결 하는 모든 시나리오에서 현재 지원 되는 도메인 \(partners\)와 파트너 표현 하는 추가 도메인 알고 해야 합니다.  
  
-   **지원 되는 응용 프로그램 및 서비스 종류:** 일부 응용 프로그램 및 서비스는 "클레임 인식." 운영 체제 리소스에 액세스 해야 것이 종류의 응용 프로그램 및 ADFS 지원 요구 사항을 관리 제시할 수 있도록 하는 서비스를 파악 하는 것이 중요 합니다.  
  
-   **논리와 실제 아키텍처 다이어그램 또는 배포가:** 알아야 합니다.  
  
    -   여부 federation 서버 팜 서버 또는 단일 서버 설정에서 작동 합니다.  
  
    -   여기서 네트워크 방화벽와 프록시를 배포 합니다.  
  
    -   위치 리소스와 사용자가 조직 외부, 조직 또는 둘 다 내에서 리소스에 액세스는 여부입니다.  
  
## <a name="how-to-implement-your-ad-fs-design-using-this-guide"></a>이 가이드를 사용 하 여 ADFS 디자인을 구현 하는 방법  
디자인을 구현의 다음 단계 순서에서 각 배포 작업을 수행 확인 하는 것입니다. 이 가이드 검사를 사용 하 여 요금제 디자인을 구현 하는 여러 서버 및 응용 프로그램 배포 작업 안내 하는 데 도움이. 부모 및 자녀 검사를 나타내는 디자인 처리할 수 있는 작업에 대 한 특정 Adfs의 순서 필요에 따라 사용 됩니다.  
  
가이드의이 섹션의 다음 부모 검사를 사용 하 여 조직의 선호 하는 ADFS 디자인을 구현 하기 위한 배포 작업과 익숙해져야:  
  
-   [웹 SSO 디자인을 구현 검사:](Checklist--Implementing-a-Web-SSO-Design.md)  
  
-   [연합된 웹 SSO 디자인을 구현 검사:](Checklist--Implementing-a-Federated-Web-SSO-Design.md)  
