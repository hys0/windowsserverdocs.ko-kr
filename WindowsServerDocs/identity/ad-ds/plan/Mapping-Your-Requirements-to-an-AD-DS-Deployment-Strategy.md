---
ms.assetid: ce3be131-06ad-41dc-a26b-1168fa68c8ed
title: AD DS 배포 전략에 요구 사항 매핑
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: a61e5e6d429acd92e48a353bc829cb620dd66054
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881834"
---
# <a name="mapping-your-requirements-to-an-ad-ds-deployment-strategy"></a>AD DS 배포 전략에 요구 사항 매핑

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

특정 AD DS 배포에 이러한 요구 사항을 검토 하 고 식별 Active Directory Domain Services (AD DS) 디자인을 마친 후 배포 요구 사항을 확인 하는 특정 배포에 관련 된 매핑할 수 있습니다. 전략입니다.  
  
다음 표를 사용 하 여 AD DS 디자인 및 배포의 해당 조합에 매핑되는 AD DS 배포 전략 조직의 요구 사항을 확인 합니다. ("예"는 특정 요구 사항; 배포 전략에 대 한 필요 하다는 의미 "아니요" 의미는 특정 요구 사항 배포 전략에 대 한 필요 하지 않습니다.)  
  
이 테이블은이 가이드에 설명 된 대로 세 가지 주 AD DS 배포 전략에만 참조 합니다.  
  
-   [새 조직에 AD DS 배포](../../ad-ds/plan/Deploying-AD-DS-in-a-New-Organization.md)  
  
-   [Windows Server 2003 조 직에 AD DS 배포](../../ad-ds/plan/Deploying-AD-DS-in-a-Windows-Server-2003-Organization.md)  
  
-   [Windows 2000 조직에 AD DS 배포](../../ad-ds/plan/Deploying-AD-DS-in-a-Windows-2000-Organization.md)  
  
그러나 조직의 요구를 충족 하도록 AD DS 디자인 및 배포 요구 사항의 조합을 사용 하 여 하이브리드 또는 사용자 지정 AD DS 배포 전략을 만들 수 있습니다.  
  
|AD DS 디자인 및 배포 요구 사항|새 조직에서 AD DS 배포|Windows Server 2003 조직에서 AD DS 배포|Windows 2000 조직에서 AD DS 배포|  
|--------------------------------------------|-----------------------------------------|---------------------------------------------------------|--------------------------------------------------|  
|[Windows Server 2008 AD DS 논리 구조 디자인](https://technet.microsoft.com/library/cc770806.aspx)|예|예|예|  
|[Windows Server 2008 AD DS 사이트 토폴로지 디자인](Designing-the-Site-Topology.md)|예|예|예|  
|도메인 컨트롤러 용량 계획|예|예|예|  
|[Windows Server 2008 포리스트 루트 도메인 배포](https://technet.microsoft.com/library/cc731174.aspx)|예|아니오|아니오|  
|[Windows Server 2008 지역 도메인 배포](https://technet.microsoft.com/library/cc755118.aspx)|예|예|예|  
|[AD DS에 대 한 고급 기능을 사용 하도록 설정](../../ad-ds/plan/Enabling-Advanced-Features-for-AD-DS.md)|예|예. 하지만 모든 도메인 컨트롤러 환경에서 도메인 또는 포리스트 기능 수준을 Windows Server 2008로 설정 하기 전에 Windows Server 2008 실행 해야 합니다.|예. 하지만 모든 도메인 컨트롤러 환경에서 도메인 또는 포리스트 기능 수준을 Windows Server 2008로 설정 하기 전에 Windows Server 2008 실행 해야 합니다.|  
|[Active Directory 도메인을 Windows Server 2008 및 Windows Server 2008 R2 AD DS 도메인으로 업그레이드](https://technet.microsoft.com/library/cc731188.aspx)|아니오|예|예|  
|[포리스트 간에 AD DS 도메인 구조 변경](https://go.microsoft.com/fwlink/?LinkId=93678)|예, 프로덕션 환경으로 파일럿 도메인을 마이그레이션하려는 경우 다른 조직과 병합 및 두 가지 정보 기술 (IT) 인프라에서 통합 또는 consolidate Windows에서 업그레이드 하는 리소스 및 계정 도메인 2000 또는 Windows Server 2003 환경입니다.|예, 다른 조직과 병합 및 통합 두 IT 인프라 또는 Windows 2000 또는 Windows Server 2003 환경에서 업그레이드 하는 리소스 및 계정 도메인을 통합 하려는 경우.|예, 다른 조직과 병합 및 통합 두 IT 인프라 또는 Windows 2000 또는 Windows Server 2003 환경에서 업그레이드 하는 리소스 및 계정 도메인을 통합 하려는 경우.|  
|[포리스트 내의 AD DS 도메인 구조 변경](https://go.microsoft.com/fwlink/?LinkId=82740))|아니오|예, 도메인의 수를 줄일 경우 복제 트래픽을 줄이고 양이 필요한 사용자 및 그룹 관리 하거나 그룹 정책 관리를 간소화 합니다.|예, 도메인의 수를 줄일 경우 복제 트래픽을 줄이고 양이 필요한 사용자 및 그룹 관리 하거나 그룹 정책 관리를 간소화 합니다.|  
  


