---
ms.assetid: d04dd17e-a843-46fd-8711-0039918f92d9
title: AD FS 디자인 계획 구현
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 6306b87dd06774bfde5ffc3ff98818d47d0c858f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408374"
---
# <a name="implementing-your-ad-fs-design-plan"></a>AD FS 디자인 계획 구현

다음 환경 조건 및 요구 사항은 Active Directory Federation Services \(AD FS\) 디자인 계획을 구현 하는 데 중요 한 요소입니다.  
  
-   **지원 되는 파트너:** 일반적으로 AD FS를 사용 하 여 파트너 조직에서 작업 합니다. Id 페더레이션을 설정 하려면 파트너 관계를 형성 하려는 조직을 결정 합니다. 기준 AD FS 배포가 적용 된 후 파트너를 사용 하려면 파트너를 추가 하 고, 파트너를 삭제 하 고, 파트너 정보를 업데이트 해야 합니다. 파트너 관계에 대 한 변경 사항은 다양 한 이유로 발생할 수 있습니다. 예를 들어 파트너가 비즈니스를 크게 변경 하거나, 조직이 대규모 조직 또는 조직의 페더레이션에 속해 있거나, 다른 환경에서 조직을 획득 한 경우 AD FS 배포에 파트너 관계 업데이트가 필요할 수 있습니다. 회사가. 여러 도메인의 id를 페더레이션 하는 모든 시나리오에서 현재 지원 되는 파트너\) 도메인 \(및 잠재적 파트너를 나타내는 모든 추가 도메인을 알아야 합니다.  
  
-   **지원 되는 응용 프로그램 및 서비스 유형:** 일부 응용 프로그램 및 서비스는 운영 체제 리소스에 액세스 해야 하는 반면, 다른 응용 프로그램 및 서비스는 "클레임 인식" 됩니다. 관리 요구 사항을 작성할 수 있도록 AD FS 지 원하는 응용 프로그램 및 서비스 유형을 이해 하는 것이 중요 합니다.  
  
-   **논리적 및 물리적 아키텍처 다이어그램 또는 배포 토폴로지:** 다음 사항을 알고 있어야 합니다.  
  
    -   팜 서버 집합 또는 단일 서버에서 페더레이션 서버가 작동 하는지 여부입니다.  
  
    -   여기서 네트워크는 방화벽 및 프록시를 배포 합니다.  
  
    -   리소스의 위치 및 사용자가 조직 외부에서 또는 둘 모두에서 리소스에 액세스 하는지 여부  
  
## <a name="how-to-implement-your-ad-fs-design-using-this-guide"></a>이 가이드를 사용 하 여 AD FS 디자인을 구현 하는 방법  
디자인을 구현 하는 다음 단계는 각 배포 작업을 수행 해야 하는 순서를 결정 하는 것입니다. 이 가이드에서는 검사 목록을 사용하여 디자인 계획을 구현하는 데 필요한 다양한 서버 및 응용 프로그램 배포 작업을 단계별로 안내합니다. 부모 및 자식 검사 목록은 특정 AD FS 디자인에 대 한 작업을 처리 해야 하는 순서를 나타내는 데 필요 합니다.  
  
이 가이드의이 섹션에서 설명 하는 다음 부모 검사 목록을 사용 하 여 조직의 기본 설정 AD FS 디자인을 구현 하기 위한 배포 작업을 익힐 수 있습니다.  
  
-   [검사 목록: 웹 SSO 디자인 구현](Checklist--Implementing-a-Web-SSO-Design.md)  
  
-   [검사 목록: 페더레이션된 웹 SSO 디자인 구현](Checklist--Implementing-a-Federated-Web-SSO-Design.md)  
