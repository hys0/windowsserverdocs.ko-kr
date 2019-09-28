---
ms.assetid: 692bd2af-deee-44cf-9af9-f364677e267f
title: 도메인 컨트롤러 배치 계획
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: ff0cba67454080db7cca4b012ae0a2d5cb40e412
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408751"
---
# <a name="planning-domain-controller-placement"></a>도메인 컨트롤러 배치 계획

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사이트 토폴로지를 디자인 하는 데 사용 되는 모든 네트워크 정보를 수집한 후에는 포리스트 루트 도메인 컨트롤러, 지역 도메인 컨트롤러, 작업 마스터 역할 소유자를 비롯 한 도메인 컨트롤러를 놓을 위치를 계획 해야 합니다. 글로벌 카탈로그 서버.  
  
Windows Server 2008에서는 Rodc (읽기 전용 도메인 컨트롤러)를 활용할 수도 있습니다. RODC는 Active Directory 데이터베이스의 읽기 전용 파티션을 호스팅하는 새 유형의 도메인 컨트롤러입니다. 계정 암호를 제외 하 고, RODC는 쓰기 가능한 도메인 컨트롤러에서 보유 하는 모든 Active Directory 개체 및 특성을 보유 합니다. 그러나 RODC에 저장 된 데이터베이스는 변경할 수 없습니다. 쓰기 가능한 도메인 컨트롤러에 대 한 변경 내용을 적용 한 다음 RODC에 다시 복제 해야 합니다.  
  
RODC는 주로 상대적으로 적은 수의 사용자, 물리적 보안 저하, 허브 사이트에 대 한 상대적으로 낮은 네트워크 대역폭 및 정보에 대 한 정보를 제한 하는 인력이 있는 원격 또는 지점 환경에 배포 되도록 설계 되었습니다. 기술 (IT). Rodc를 배포 하면 보안을 강화 하 고 네트워크 리소스에 보다 효율적으로 액세스할 수 있습니다. RODC 기능에 대 한 자세한 내용은 AD DS를 참조 하세요. 읽기 전용 도메인 컨트롤러 ([https://go.microsoft.com/fwlink/?LinkID=106616](https://go.microsoft.com/fwlink/?LinkID=106616)). RODC를 배포 하는 방법에 대 한 자세한 내용은 읽기 전용 도메인 컨트롤러에 대 한 단계별 가이드 ([https://go.microsoft.com/fwlink/?LinkID=92728](https://go.microsoft.com/fwlink/?LinkID=92728))를 참조 하세요.  
  
> [!NOTE]  
> 이 가이드에서는 각 사이트에 표시 되는 각 도메인에 대 한 도메인 컨트롤러 및 도메인 컨트롤러의 적절 한 수를 결정 하는 방법에 대해서는 설명 하지 않습니다.  
  
## <a name="in-this-section"></a>단원 내용  
  
-   [포리스트 루트 도메인 컨트롤러 배치 계획](../../ad-ds/plan/Planning-Forest-Root-Domain-Controller-Placement.md)  
  
-   [지역 도메인 컨트롤러 배치 계획](../../ad-ds/plan/Planning-Regional-Domain-Controller-Placement.md)  
  
-   [글로벌 카탈로그 서버 배치 계획](../../ad-ds/plan/Planning-Global-Catalog-Server-Placement.md)  
  
-   [작업 마스터 역할 배치 계획](../../ad-ds/plan/Planning-Operations-Master-Role-Placement.md)  
  


