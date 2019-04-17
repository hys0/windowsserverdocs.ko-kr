---
ms.assetid: 692bd2af-deee-44cf-9af9-f364677e267f
title: "도메인 컨트롤러 배치 계획"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c6d9ca064699f95390e5b95863a6871ea2dc9d6e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="planning-domain-controller-placement"></a>도메인 컨트롤러 배치 계획

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

모든 사이트 토폴로지 디자인, 숲 루트 도메인 컨트롤러 지역 도메인 컨트롤러 등 도메인 컨트롤러를 삽입할 계획 하는 데 사용 될 네트워크 정보의 수집 된 후 작업 역할 소유자와 드 서버 마스터 합니다.  
  
Windows Server 2008에서 사용자도 활용할 수 읽기 전용 Rodc (도메인 컨트롤러). RODC는 도메인 컨트롤러의 Active Directory 데이터베이스 읽기 전용 파티션을 호스트 하는 새로운 유형의입니다. 계정 암호를 제외한 모든 Active Directory 개체와 쓸 수 있는 도메인 컨트롤러 특성 RODC를 보유 합니다. 그러나 변경할 수 없습니다 RODC에 저장 하는 데이터베이스에 있습니다. 변경 쓸 수 있는 도메인 컨트롤러에서 수행 하 고 RODC에 다시 복제할 해야 합니다.  
  
RODC 하도록 주로 원격에 배포 또는 지점 환경 상대적으로 몇 사용자, 낮은 물리적 보안, 허브 사이트 및 개인 정보 it 제한 된 알고 있는 네트워크 저하 대역폭 일반적으로 있는 합니다. 강화 된 보안 및 네트워크 리소스를 더 효율적 액세스 Rodc 결과 배포 합니다. RODC 기능에 대 한 자세한 내용은 참조 AD DS: Read-Only 도메인 컨트롤러 ([https://go.microsoft.com/fwlink/?LinkID=106616](https://go.microsoft.com/fwlink/?LinkID=106616)). RODC 배포 하는 방법에 대 한 정보를 참조 하세요.는 Step-by-Step에 대 한 지침에 따라 Read-Only 도메인 컨트롤러 ([https://go.microsoft.com/fwlink/?LinkID=92728](https://go.microsoft.com/fwlink/?LinkID=92728)).  
  
> [!NOTE]  
> 이 가이드 적절 한 수 도메인 컨트롤러 및 각 사이트에 표시 되는 각 도메인 도메인 컨트롤러 하드웨어 요구 사항을 확인 하는 방법을 설명 하지 않습니다.  
  
## <a name="in-this-section"></a>이 섹션에서  
  
-   [숲 루트 도메인 컨트롤러 배치 계획](../../ad-ds/plan/Planning-Forest-Root-Domain-Controller-Placement.md)  
  
-   [지역 도메인 컨트롤러 배치 계획](../../ad-ds/plan/Planning-Regional-Domain-Controller-Placement.md)  
  
-   [드 서버 배치 계획](../../ad-ds/plan/Planning-Global-Catalog-Server-Placement.md)  
  
-   [작업 마스터 역할 배치 계획](../../ad-ds/plan/Planning-Operations-Master-Role-Placement.md)  
  


