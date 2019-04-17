---
ms.assetid: 9ad81367-f3fe-4b2e-bd7c-5900b2b9f77f
title: "디자인 논리 구조"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 8d1b9c27f05faef49f7fd4228f4ebe689b75d30f
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="designing-the-logical-structure"></a>디자인 논리 구조

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Domain Services (AD DS) 조직을 사용자와 리소스 관리에 대 한 확장, 안전 및 관리 하기 쉬운 인프라를 만들 수 있습니다. 디렉터리 사용 응용 프로그램을 지원 하기 위해 사용할 수 있습니다.  
  
잘 설계 된 Active Directory 논리 구조 다음 이점을 제공합니다.  
  
-   많은 수의 개체 포함 된 Microsoft Windows 기반 네트워크의 관리를 간소화  
  
-   통합된 도메인 구조 및 관리 감소 비용  
  
-   위임 리소스를 적절 하 게 관리 제어 하는 기능  
  
-   네트워크 대역폭에 미치는 영향을 제한  
  
-   간소화 된 리소스 공유  
  
-   검색 최적 성능  
  
-   낮은 총 소유 비용도 절감  
  
잘 설계 된 Active Directory 논리 구조 효율적인 통합 그룹 정책, 같은 기능을 이용 데스크톱 잠금. 소프트웨어 배포 됩니다. 시스템에 사용자, 그룹, 워크스테이션 및 서버 관리 하 고 있습니다. 그리고 신중 하 게 디자인된 논리 구조 용이 하 게 통합 Microsoft 및 Microsoft가 아닌 타사 응용 프로그램과 서비스, Microsoft Exchange Server 공개 키 infrastructure (PKI) 등의 도메인 기반 분산 파일 시스템 (DFS) 합니다.  
  
AD DS 배포 하기 전에 Active Directory 논리 구조 디자인할 때 가장 잘 Active Directory 기능을 사용 하 여 배포 프로세스를 최적화할 수 있습니다. Active Directory 논리 구조 디자인을 디자인 팀 먼저 조직에 대 한 요구 사항을 파악 하 고,이 정보에 따라, 위치 숲 및 도메인 경계를 결정 합니다. 그런 다음, 디자인 팀 숲 요구에 맞게 시스템 DNS (도메인 이름) 환경 구성 하는 방법을 결정 합니다. 마지막으로, 디자인 팀 위임 리소스 조직에서 관리 하는 데 필요한 조직 단위 구조를 식별 합니다.  
  
## <a name="in-this-guide"></a>이 가이드  
  
-   [Active Directory 논리 모델을 이해합니다.](../../ad-ds/plan/Understanding-the-Active-Directory-Logical-Model.md)  
  
-   [배포 프로젝트 참가자에 게 확인](../../ad-ds/plan/Identifying-the-Deployment-Project-Participants.md)  
  
-   [숲 디자인 만들기](../../ad-ds/plan/Creating-a-Forest-Design.md)  
  
-   [도메인 디자인 만들기](../../ad-ds/plan/Creating-a-Domain-Design.md)  
  
-   [DNS Infrastructure 디자인 만들기](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md)  
  
-   [조직 디자인](../../ad-ds/plan/Creating-an-Organizational-Unit-Design.md)  
  
-   [부록 a: DNS 인벤토리](../../ad-ds/plan/Appendix-A--DNS-Inventory.md)  
  


