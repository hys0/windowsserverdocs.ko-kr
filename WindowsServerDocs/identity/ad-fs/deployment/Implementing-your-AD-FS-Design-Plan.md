---
ms.assetid: d04dd17e-a843-46fd-8711-0039918f92d9
title: AD FS 디자인 계획 구현
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 6150b52030734c57b345aea731302650bcbddbfd
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192132"
---
# <a name="implementing-your-ad-fs-design-plan"></a>AD FS 디자인 계획 구현

다음 환경 조건 및 요구 사항을 가지 Active Directory 페더레이션 서비스의 구현에서 중요 한 요인이 \(AD FS\) 디자인 계획:  
  
-   **지원 되는 파트너:** 일반적으로 파트너 조직과 함께 작동 하도록 AD FS를 사용 합니다. Id 페더레이션이를 설정 하려면 파트너 관계를 형성 하려는 조직을 결정 합니다. 기본 AD FS 배포를 배치한 후 파트너를 추가 하 고, 파트너를 삭제 한 다음 파트너 정보를 업데이트 해야 파트너를 사용 하 여 운영 합니다. 파트너 관계 변경에 대 한 다양 한 이유로 발생할 수 있습니다. 예를 통해 AD FS 배포 파트너의 비즈니스를 크게 변경, 조직의 대규모 조직 또는 조직에서 페더레이션 중 일부가 또는 다른 조직을 확보 하는 경우 파트너 관계 업데이트를 요구할 수 있습니다. 회사입니다. 여러 도메인의 id를 페더레이션 하는 모든 시나리오에서 도메인을 확인 해야 합니다 \(파트너\) 현재 지원 되는 파트너를 나타내는 모든 추가 도메인입니다.  
  
-   **지원 되는 응용 프로그램 및 서비스 유형:** 일부 응용 프로그램 및 서비스 이지만 나머지는 "클레임 인식 합니다." 운영 체제 리소스에 액세스 해야 응용 프로그램 및 AD FS 관리 요구 사항을 작성할 수 있도록 지 원하는 서비스 유형을 이해 하는 것이 반드시 합니다.  
  
-   **논리적 및 물리적 아키텍처 다이어그램 또는 배포 토폴로지:** 확인 해야 합니다.  
  
    -   여부 페더레이션 서버 팜 서버 또는 단일 서버 집합에서 작동 합니다.  
  
    -   여기서 네트워크 방화벽 및 프록시를 배포 합니다.  
  
    -   사용자는 조직 또는 둘 다 외부 조직 내에서 리소스를 액세스 하는 여부 및 리소스의 위치입니다.  
  
## <a name="how-to-implement-your-ad-fs-design-using-this-guide"></a>이 가이드를 사용 하 여 AD FS 디자인을 구현 하는 방법  
디자인을 구현 하는 다음 단계는 어떤 순서로 각 배포 작업을 수행 해야 합니다 결정 하는 것입니다. 이 가이드에서는 검사 목록을 사용하여 디자인 계획을 구현하는 데 필요한 다양한 서버 및 응용 프로그램 배포 작업을 단계별로 안내합니다. 부모 및 하위 검사 목록이 디자인 해야 처리는 특정 AD FS에 대 한 작업 순서를 나타내는 데 필요에 따라 사용 됩니다.  
  
이 가이드의이 섹션에서는 다음 부모 검사 목록을 사용 하 여 조직의 기본 AD FS 디자인을 구현 하는 것에 대 한 배포 작업에 익숙해지기 위해:  
  
-   [검사 목록: 웹 SSO 디자인 구현](Checklist--Implementing-a-Web-SSO-Design.md)  
  
-   [검사 목록: 페더레이션된 웹 SSO 디자인 구현](Checklist--Implementing-a-Federated-Web-SSO-Design.md)  
