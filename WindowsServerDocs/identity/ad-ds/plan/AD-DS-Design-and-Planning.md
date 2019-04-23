---
ms.assetid: a91339ef-6ad4-445f-8ecc-a95fbcc04296
title: AD DS 디자인 및 계획
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 24fc96aae268d9847bd3b32460ada33d2c6e0d65
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848694"
---
# <a name="ad-ds-design-and-planning"></a>AD DS 디자인 및 계획

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사용자 환경에서 Windows Server Active Directory Domain Services (AD DS)를 배포 하 여 single sign-on (SSO) 기능은 AD DS를 제공 하는 중앙 집중식, 위임 된 관리 모델을 사용할 수 있습니다. 조직에 대 한 현재 환경과 배포 작업을 식별 한 후에 조직의 요구를 충족 하는 AD DS 배포 전략을 만들 수 있습니다.  
  
## <a name="about-this-guide"></a>이 가이드 정보

이 가이드에서는 조직 및 만들려는 특정 디자인의 요구 사항에 따라 AD DS 배포 전략을 개발 하기 위한 권장 사항을 제공 합니다. 이 가이드는 인프라 전문가 또는 시스템 설계자 사용에 대 한 것입니다. 이 가이드를 읽기 전에 기능 수준에서 AD DS의 작동 방식을 이해를 해야 합니다. 또한 AD DS 배포 전략에 반영할 조직의 요구 사항을 잘 알고가 있어야 합니다.  
  
이 가이드는 몇 가지 가능한 시작점 Windows Server 2008 AD DS 배포에 대 한 작업 집합을 설명합니다. 이 가이드에서는 사용자 환경에 가장 적합 한 배포 전략을 결정 합니다.  
  
이 가이드에 표시 되는 전략은 거의 모든 서버 운영 체제 배포에 대 한 적절 한 이지만 이러한 테스트 되었으며 사용 하 여 100,000 미만의 사용자 및 1,000 개 미만의 사이트를 포함 하는 환경에 맞게 유효성을 검사 28.8 킬로 비트 / 초 (Kbps)의 최소 네트워크 연결입니다. 사용자 환경의 이러한 조건에 맞지 않습니다, 경우에 환경이 더 복잡 한 환경에서 AD DS를 배포 하는 컨설팅 회사를 사용 하 여 하는 것이 좋습니다.  
  
AD DS 배포 프로세스를 테스트 하는 방법에 대 한 자세한 내용은 문서 참조 [테스트 및 배포 프로세스를 확인 하는 중](https://go.microsoft.com/fwlink/?LinkId=100206)합니다.  
  
## <a name="in-this-guide"></a>이 가이드의 내용

[AD DS 디자인 이해](Understanding-AD-DS-Design.md)  
  
[AD DS 디자인 및 배포 요구 사항 식별](Identifying-Your-AD-DS-Design-and-Deployment-Requirements.md)  
  
[AD DS 배포 전략에 요구 사항 매핑](Mapping-Your-Requirements-to-an-AD-DS-Deployment-Strategy.md)  
  
[Windows Server 2008 AD DS 논리 구조 디자인](Designing-the-Logical-Structure.md)  
  
[Windows Server 2008 AD DS 사이트 토폴로지 디자인](Designing-the-Site-Topology.md)  
  
[AD DS에 대 한 고급 기능을 사용 하도록 설정](Enabling-Advanced-Features-for-AD-DS.md)  
  
[AD DS 배포 전략 예제 평가](Evaluating-AD-DS-Deployment-Strategy-Examples.md)  
  
[부록 a: 주요 AD DS 용어 검토](Appendix-A--Reviewing-Key-AD-DS-Terms.md)  
