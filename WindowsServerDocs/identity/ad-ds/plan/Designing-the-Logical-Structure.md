---
ms.assetid: 9ad81367-f3fe-4b2e-bd7c-5900b2b9f77f
title: 논리 구조 디자인
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: de56205c163abff1b05d57ea90954fa93606abce
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822616"
---
# <a name="designing-the-logical-structure"></a>논리 구조 디자인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Domain Services (AD DS)를 사용 하면 조직에서 사용자 및 리소스 관리를 위해 확장 가능 하 고 안전 하며 관리 하기 쉬운 인프라를 만들 수 있습니다. 또한 디렉터리 사용 응용 프로그램을 지원할 수 있습니다.  
  
잘 설계 된 Active Directory 논리 구조는 다음과 같은 이점을 제공 합니다.  
  
-   많은 수의 개체를 포함 하는 Microsoft Windows 기반 네트워크의 간소화 된 관리  
  
-   통합 도메인 구조 및 관리 비용 절감  
  
-   리소스에 대 한 관리 제어를 적절 하 게 위임 하는 기능  
  
-   네트워크 대역폭에 대 한 영향 감소  
  
-   간소화 된 리소스 공유  
  
-   최적의 검색 성능  
  
-   낮은 총 소유 비용  
  
잘 설계 된 Active Directory 논리 구조는 그룹 정책와 같은 기능을 효율적으로 통합 하는 데 도움이 됩니다. 데스크톱 잠금 소프트웨어 배포 사용자, 그룹, 워크스테이션 및 서버 관리를 시스템에 사용 합니다. 또한 신중 하 게 디자인 된 논리적 구조를 사용 하면 microsoft Exchange Server, PKI (공개 키 인프라) 및 도메인 기반 DFS (분산 파일 시스템)와 같은 microsoft 및 타사 응용 프로그램과 서비스를 쉽게 통합할 수도 있습니다.  
  
AD DS를 배포 하기 전에 Active Directory 논리 구조를 디자인 하는 경우 배포 프로세스를 최적화 하 여 Active Directory 기능을 가장 잘 활용할 수 있습니다. Active Directory 논리 구조를 디자인 하기 위해 디자인 팀은 먼저 조직의 요구 사항을 식별 하 고,이 정보에 따라 포리스트와 도메인 경계를 넣을 위치를 결정 합니다. 그런 다음, 디자인 팀은 포리스트 요구에 맞게 DNS (Domain Name System) 환경을 구성 하는 방법을 결정 합니다. 마지막으로, 설계 팀은 조직에서 리소스 관리를 위임 하는 데 필요한 OU (조직 구성 단위) 구조를 식별 합니다.  
  
## <a name="in-this-guide"></a>설명서의 내용  
  
-   [Active Directory 논리 모델 이해](../../ad-ds/plan/Understanding-the-Active-Directory-Logical-Model.md)  
  
-   [배포 프로젝트 참가자 식별](../../ad-ds/plan/Identifying-the-Deployment-Project-Participants.md)  
  
-   [포리스트 디자인 만들기](../../ad-ds/plan/Creating-a-Forest-Design.md)  
  
-   [도메인 디자인 만들기](../../ad-ds/plan/Creating-a-Domain-Design.md)  
  
-   [DNS 인프라 디자인 만들기](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md)  
  
-   [조직 구성 단위 디자인 만들기](../../ad-ds/plan/Creating-an-Organizational-Unit-Design.md)  
  
-   [부록 A: DNS 인벤토리](../../ad-ds/plan/Appendix-A--DNS-Inventory.md)  
  


