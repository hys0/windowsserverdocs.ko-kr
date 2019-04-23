---
ms.assetid: 9ad81367-f3fe-4b2e-bd7c-5900b2b9f77f
title: 논리 구조 디자인
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 82184fe678c05b1d7458584de8eecd0c07ece02f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832334"
---
# <a name="designing-the-logical-structure"></a>논리 구조 디자인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Domain Services (AD DS)를 사용 하면 사용자 및 리소스 관리를 위한 확장 가능 하 고 안전 하며 관리 하기 쉬운 인프라를 만들 수 있도록 합니다. 또한 디렉터리 사용 응용 프로그램을 지원할 수 있습니다.  
  
잘 설계 된 Active Directory 논리 구조는 다음과 같은 이점이 있습니다.  
  
-   많은 수의 개체를 포함 하는 Microsoft Windows 기반 네트워크의 간소화 된 관리  
  
-   통합된 도메인 구조와 축소 된 관리 비용  
  
-   적절 하 게 리소스에 대 한 관리 제어를 위임 하는 기능  
  
-   네트워크 대역폭에 미치는 영향이 감소  
  
-   간소화 된 리소스 공유  
  
-   최적의 검색 성능  
  
-   낮은 총 소유 비용  
  
잘 설계 된 Active Directory 논리 구조를 효율적이 고 통합 된 그룹 정책에 이러한 기능을 용이 하 게 데스크톱 잠금; 소프트웨어 배포. 및 시스템에 사용자, 그룹, 워크스테이션 및 서버 관리 또한 논리 구조를 신중 하 게 설계 된 Microsoft 및 타사 응용 프로그램 및 Microsoft Exchange Server, 공개 키 인프라 (PKI)와 같은 서비스의 통합을 용이 하 게 하 고 파일 시스템 (DFS)를 배포 하는 도메인 기반 합니다.  
  
AD DS를 배포 하기 전에 Active Directory 논리 구조를 디자인할 때 가장 잘 활용 하기 위해 Active Directory 기능 배포 프로세스를 최적화할 수 있습니다. Active Directory 논리 구조를 디자인 하려면 디자인 팀 먼저 조직에 대 한 요구 사항을 파악을이 정보를 기반으로, 포리스트 및 도메인 경계를 배치 하는 위치를 결정 합니다. 그런 다음 디자인 팀 포리스트의 요구 사항에 맞게 도메인 이름 시스템 (DNS) 환경을 구성 하는 방법을 결정 합니다. 마지막으로 디자인 팀의 조직에서 리소스 관리를 위임 하는 데 필요한 조직 구성 단위 (OU) 구조를 식별 합니다.  
  
## <a name="in-this-guide"></a>이 가이드의 내용  
  
-   [Active Directory 논리 모델 이해](../../ad-ds/plan/Understanding-the-Active-Directory-Logical-Model.md)  
  
-   [배포 프로젝트 참가자 식별](../../ad-ds/plan/Identifying-the-Deployment-Project-Participants.md)  
  
-   [포리스트 디자인 만들기](../../ad-ds/plan/Creating-a-Forest-Design.md)  
  
-   [도메인 디자인 만들기](../../ad-ds/plan/Creating-a-Domain-Design.md)  
  
-   [DNS 인프라 디자인 만들기](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md)  
  
-   [조직 구성 단위 디자인 만들기](../../ad-ds/plan/Creating-an-Organizational-Unit-Design.md)  
  
-   [부록 a: DNS 인벤토리](../../ad-ds/plan/Appendix-A--DNS-Inventory.md)  
  


