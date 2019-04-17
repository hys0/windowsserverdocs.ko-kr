---
ms.assetid: ce3be131-06ad-41dc-a26b-1168fa68c8ed
title: "AD DS 배포 전략 요구 사항에 매핑하"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b4f625f06fede5b9dc751282cda19b68d7f9e535
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="mapping-your-requirements-to-an-ad-ds-deployment-strategy"></a>AD DS 배포 전략 요구 사항에 매핑하

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

검토 하 고 식별 Active Directory 도메인 서비스 (AD DS) 디자인을 완료 하 고 배포 요구 고 확인할 수 있는 특정 배포 관련 된 후 특정 AD DS 배포 전략 요구 사항을 매핑할 수 있습니다.  
  
AD DS 디자인 및 배포에서 적절 한 조합 지도 AD DS 배포 전략 조직의 요구 사항을 확인 하려면 다음 표를 사용 합니다. ("예" 특정 요구 사항에 대 한 배포 전략; 필요 하다는 의미 "없음" 의미는 특정 요구 사항을 배포 전략 필요는 없습니다.)  
  
이 가이드에 설명 된 대로 세 가지 주요 AD DS 배포 전략에만이 표 참조 합니다.  
  
-   [새 조직에서 AD DS 배포](../../ad-ds/plan/Deploying-AD-DS-in-a-New-Organization.md)  
  
-   [Windows Server 2003 조직에서 AD DS 배포](../../ad-ds/plan/Deploying-AD-DS-in-a-Windows-Server-2003-Organization.md)  
  
-   [Windows 2000 조직에서 AD DS 배포](../../ad-ds/plan/Deploying-AD-DS-in-a-Windows-2000-Organization.md)  
  
그러나 하이브리드 또는 사용자 지정 AD DS 배포 전략 조직에서 요구 하 AD DS 디자인 및 배포 요구 사항을 조합을 사용 하 여 만들 수 있습니다.  
  
|광고 DS 디자인 및 배포 요구 사항|새 조직에서 AD DS 배포|Windows Server 2003 조직에서 AD DS 배포|Windows 2000 조직에서 AD DS 배포|  
|--------------------------------------------|-----------------------------------------|---------------------------------------------------------|--------------------------------------------------|  
|[Windows Server 2008 AD DS에 대 한 논리 구조 디자인](https://technet.microsoft.com/library/cc770806.aspx)|예|예|예|  
|[Windows Server 2008 AD DS 사이트 토폴로지 디자인](Designing-the-Site-Topology.md)|예|예|예|  
|도메인 컨트롤러 용량 계획|예|예|예|  
|[Windows Server 2008 숲 루트 도메인 배포](https://technet.microsoft.com/library/cc731174.aspx)|예|아니요|아니요|  
|[Windows Server 2008 지역 도메인을 배포합니다.](https://technet.microsoft.com/library/cc755118.aspx)|예|예|예|  
|[AD DS 위한 고급 기능 사용](../../ad-ds/plan/Enabling-Advanced-Features-for-AD-DS.md)|예|예, 그러나 모든 도메인 컨트롤러의 환경에 Windows Server 2008를 도메인 또는 숲 기능 수준을 설정 하기 전에 Windows Server 2008 실행 해야 합니다.|예, 그러나 모든 도메인 컨트롤러의 환경에 Windows Server 2008를 도메인 또는 숲 기능 수준을 설정 하기 전에 Windows Server 2008 실행 해야 합니다.|  
|[Windows Server 2008 및 Windows Server 2008 R2 광고 DS 도메인 Active Directory 도메인 업그레이드](https://technet.microsoft.com/library/cc731188.aspx)|아니요|예|예|  
|[숲 간에 DS 도메인 AD 재구성](https://go.microsoft.com/fwlink/?LinkId=93678)|예, 생산 환경에 시험 도메인 마이그레이션하려 하려는 경우 다른 조직과 병합 하 고 통합 두 정보 it 인프라 또는 Windows 2000 또는 Windows Server 2003 환경의에서 위치에 업그레이드 리소스와 계정을 도메인 통합할 합니다.|예, 다른 조직과 병합 하 고 통합 두 IT 인프라 또는 Windows 2000 또는 Windows Server 2003 환경의에서 위치에 업그레이드 리소스와 계정을 도메인 통합할 하려는 경우 합니다.|예, 다른 조직과 병합 하 고 통합 두 IT 인프라 또는 Windows 2000 또는 Windows Server 2003 환경의에서 위치에 업그레이드 리소스와 계정을 도메인 통합할 하려는 경우 합니다.|  
|[숲 내의 광고 DS 도메인 재구성](https://go.microsoft.com/fwlink/?LinkId=82740))|아니요|예, 도메인의 수를 줄이세요 해야 할 경우 복제 교통 하 고 필요한 사용자 및 그룹 관리 양을 줄이는 또는 그룹 정책 관리를 간소화할 합니다.|예, 도메인의 수를 줄이세요 해야 할 경우 복제 교통 하 고 필요한 사용자 및 그룹 관리 양을 줄이는 또는 그룹 정책 관리를 간소화할 합니다.|  
  


