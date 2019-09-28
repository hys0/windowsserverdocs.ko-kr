---
ms.assetid: ce3be131-06ad-41dc-a26b-1168fa68c8ed
title: AD DS 배포 전략에 요구 사항 매핑
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 412e1ccb13b4d92801faf019b1ed6d01eff8b8d4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402535"
---
# <a name="mapping-your-requirements-to-an-ad-ds-deployment-strategy"></a>AD DS 배포 전략에 요구 사항 매핑

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Domain Services (AD DS) 디자인 및 배포 요구 사항을 검토 하 고 파악 한 후 특정 배포와 관련 된 요구 사항을 확인 한 후 해당 요구 사항을 특정 AD DS 배포에 매핑할 수 있습니다. 방식의.  
  
다음 표를 사용 하 여 조직에 대 한 AD DS 설계 및 배포 요구 사항의 적절 한 조합에 매핑할 AD DS 배포 전략을 결정 합니다. "예"는 배포 전략에 필요한 특정 요구 사항이 있음을 의미 합니다. "아니요"는 배포 전략에 대 한 특정 요구 사항이 필요 하지 않음을 의미 합니다.  
  
이 표에서는이 가이드에 설명 된 대로 세 가지 기본 AD DS 배포 전략을 참조 합니다.  
  
-   [새 조직에 AD DS 배포](../../ad-ds/plan/Deploying-AD-DS-in-a-New-Organization.md)  
  
-   [Windows Server 2003 조직에 AD DS 배포](../../ad-ds/plan/Deploying-AD-DS-in-a-Windows-Server-2003-Organization.md)  
  
-   [Windows 2000 조직에 AD DS 배포](../../ad-ds/plan/Deploying-AD-DS-in-a-Windows-2000-Organization.md)  
  
그러나 조직의 요구를 충족 하기 위해 AD DS 디자인 및 배포 요구 사항 조합을 사용 하 여 하이브리드 또는 사용자 지정 AD DS 배포 전략을 만들 수 있습니다.  
  
|AD DS 설계 및 배포 요구 사항|새 조직에서 AD DS 배포|Windows Server 2003 조직에서 AD DS 배포|Windows 2000 조직에서 AD DS 배포|  
|--------------------------------------------|-----------------------------------------|---------------------------------------------------------|--------------------------------------------------|  
|[Windows Server 2008에 대 한 논리 구조 디자인 AD DS](https://technet.microsoft.com/library/cc770806.aspx)|예|예|예|  
|[Windows Server 2008에 대 한 사이트 토폴로지 디자인 AD DS](Designing-the-Site-Topology.md)|예|예|예|  
|도메인 컨트롤러 용량 계획|예|예|예|  
|[Windows Server 2008 포리스트 루트 도메인 배포](https://technet.microsoft.com/library/cc731174.aspx)|예|아니오|아니요|  
|[Windows Server 2008 지역 도메인 배포](https://technet.microsoft.com/library/cc755118.aspx)|예|예|예|  
|[AD DS에 대한 고급 기능 사용](../../ad-ds/plan/Enabling-Advanced-Features-for-AD-DS.md)|예|예, 하지만 도메인 또는 포리스트 기능 수준을 Windows Server 2008로 설정 하기 전에 환경의 모든 도메인 컨트롤러에서 Windows Server 2008를 실행 해야 합니다.|예, 하지만 도메인 또는 포리스트 기능 수준을 Windows Server 2008로 설정 하기 전에 환경의 모든 도메인 컨트롤러에서 Windows Server 2008를 실행 해야 합니다.|  
|[Active Directory 도메인을 Windows Server 2008 및 Windows Server 2008 R2 AD DS 도메인으로 업그레이드](https://technet.microsoft.com/library/cc731188.aspx)|아니요|예|예|  
|[포리스트 간 AD DS 도메인 재구성](https://go.microsoft.com/fwlink/?LinkId=93678)|예, 파일럿 도메인을 프로덕션 환경으로 마이그레이션하고 다른 조직과 병합 하 고 두 IT (정보 기술) 인프라를 통합 하거나 Windows에서 업그레이드 한 리소스 및 계정 도메인을 통합 하려는 경우 2000 또는 Windows Server 2003 환경.|예, 다른 조직과 병합 하 고 두 개의 IT 인프라를 통합 하거나 Windows 2000 또는 Windows Server 2003 환경에서 업그레이드 한 리소스 및 계정 도메인을 통합 하려는 경우입니다.|예, 다른 조직과 병합 하 고 두 개의 IT 인프라를 통합 하거나 Windows 2000 또는 Windows Server 2003 환경에서 업그레이드 한 리소스 및 계정 도메인을 통합 하려는 경우입니다.|  
|[포리스트 내의 AD DS 도메인 재구성](https://go.microsoft.com/fwlink/?LinkId=82740))|아니요|예, 도메인 수를 줄여야 하는 경우 복제 트래픽과 필요한 사용자 및 그룹 관리의 양을 줄이거나 그룹 정책 관리를 간소화 합니다.|예, 도메인 수를 줄여야 하는 경우 복제 트래픽과 필요한 사용자 및 그룹 관리의 양을 줄이거나 그룹 정책 관리를 간소화 합니다.|  
  


