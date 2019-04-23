---
ms.assetid: 692bd2af-deee-44cf-9af9-f364677e267f
title: 도메인 컨트롤러 배치 계획
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 68406d4973dd585bf0a98562c987c1b1512c095c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883364"
---
# <a name="planning-domain-controller-placement"></a>도메인 컨트롤러 배치 계획

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

포리스트 루트 도메인 컨트롤러, 지역 도메인 컨트롤러, 작업 마스터 역할 소유자를 포함 하 여 도메인 컨트롤러를 배치 하려는 모든 사이트 토폴로지를 디자인 하는 데 사용할 네트워크 정보를 수집한 후 계획 및 글로벌 카탈로그 서버입니다.  
  
Windows Server 2008에도 읽기 전용 도메인 컨트롤러 (Rodc) 활용을 걸릴 수 있습니다. RODC는 Active Directory 데이터베이스의 읽기 전용 파티션을 호스팅하는 도메인 컨트롤러의 새 형식입니다. 계정 암호를 제외 하 고 RODC 모든 Active Directory 개체와 쓰기 가능한 도메인 컨트롤러를 보유 하는 특성을 포함 합니다. 그러나 변경 내용은 RODC에 저장 된 데이터베이스 연결할 수 없습니다. 변경 내용 쓰기 가능한 도메인 컨트롤러에서 변경 하 고 RODC에 다시 복제 해야 합니다.  
  
RODC는 기본적으로 배포 되도록 설계 원격에서 또는 지점 환경에는 일반적으로 비교적 적은 사용자, 낮은 수준의 물리적 보안, 허브 사이트에 제한적인된 지식 정보를 사용 하 여 직원을 비교적 낮은 네트워크 대역폭 기술 (IT)입니다. 향상 된 보안 및 네트워크 리소스에 더 효율적으로 액세스 Rodc 결과 배포 합니다. RODC 기능에 대 한 자세한 내용은 AD DS를 참조 하세요. 읽기 전용 도메인 컨트롤러 ([https://go.microsoft.com/fwlink/?LinkID=106616](https://go.microsoft.com/fwlink/?LinkID=106616)). RODC를 배포 하는 방법에 대 한 자세한 내용은 단계별 가이드를 읽기 전용 도메인 컨트롤러에 대 한 참조 ([https://go.microsoft.com/fwlink/?LinkID=92728](https://go.microsoft.com/fwlink/?LinkID=92728)).  
  
> [!NOTE]  
> 이 가이드에서 도메인 컨트롤러 및 도메인 컨트롤러 하드웨어 요구 사항 각 사이트에 표시 되는 각 도메인에 대 한 적절 한 수를 확인 하는 방법을 설명 하지 않습니다.  
  
## <a name="in-this-section"></a>단원 내용  
  
-   [포리스트 루트 도메인 컨트롤러 배치 계획](../../ad-ds/plan/Planning-Forest-Root-Domain-Controller-Placement.md)  
  
-   [지역 도메인 컨트롤러 배치 계획](../../ad-ds/plan/Planning-Regional-Domain-Controller-Placement.md)  
  
-   [글로벌 카탈로그 서버 배치 계획](../../ad-ds/plan/Planning-Global-Catalog-Server-Placement.md)  
  
-   [작업 마스터 역할 배치 계획](../../ad-ds/plan/Planning-Operations-Master-Role-Placement.md)  
  


