---
ms.assetid: bb16e39d-566d-436c-b957-394c06d556db
title: Windows Server 2012의 AD FS 디자인 가이드
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e660c1dabcc5a683fa74068ea148fd4efbeee569
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890214"
---
# <a name="ad-fs-design-guide-in-windows-server-2012"></a>Windows Server 2012의 AD FS 디자인 가이드

>적용 대상: Windows Server 2012
  
> [!NOTE]  
> Windows Server 2012 R2에서 AD FS를 배포 하는 방법에 대 한 자세한 내용은 [Windows Server 2012 R2 AD FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)합니다.  
  
Active Directory® Federation Services를 사용할 수 있습니다 \(AD FS\) Windows Server® 2012를 사용 하 여 페더레이션에서 운영 체제 서비스를 원활 하 게 웹 사용자가 인증 공급자 역할\-기반 서비스 또는 만들거나 외부 트러스트 또는 포리스트 트러스트를 한 번에 로그온 할 필요가 없으며 두 조직의 네트워크 간에 유지 하기 위해 관리자에 대 한 필요 없이 리소스 파트너 조직에 상주 하는 응용 프로그램입니다. 다른 네트워크의 리소스에 액세스 하는 동안 하나의 네트워크에 인증 하는 프로세스-사용자가 반복 된 로그온 동작 부담 없이-single 이라고\-온 \(SSO\)합니다.  
  
## <a name="about-this-guide"></a>이 가이드 정보  
이 가이드에서는 조직의 요구 사항에 따라 AD FS의 새 배포를 계획 하기 위한 권장 사항을 \(에이 가이드의 배포 목표 라고도\) 및 만들려는 특정 디자인 합니다. 이 가이드는 인프라 전문가 또는 시스템 설계자용으로 작성되었습니다. AD FS 배포를 계획할 때 필요한 주요 의사 결정 사항을 강조 합니다. 이 가이드를 읽기 전에 기능 수준에서 AD FS의 작동 방식을 이해를 해야 합니다. 또한 AD FS 디자인에 반영할 조직의 요구 사항을 잘 알고가 있어야 합니다.  
  
이 가이드에서는 세 가지 기본 AD FS 디자인을 기반으로 하는 배포 목표의 집합을 설명 하 고 사용자 환경에 가장 적합 한 디자인을 결정 도와줍니다. 이러한 배포 목표 폼 포괄적인 다음 AD FS 디자인 또는 환경의 요구 사항을 충족 하는 사용자 지정 디자인 중 하나를 사용할 수 있습니다.  
  
-   페더레이션된 웹 SSO 비즈니스를 지원 하기 위해\-하\-비즈니스 \(B2B\) 시나리오 및 독립 포리스트를 사용 하 여 사업부 간의 공동 작업을 지원 하기 위해  
  
-   비즈니스에서 응용 프로그램에 대 한 고객 액세스를 지원 하기 위해 SSO 웹\-하\-소비자 \(B2C\) 시나리오  
  
각 디자인에 대해 필요한 사용자 환경 관련 데이터를 수집하는 지침을 확인합니다. 다음 계획 및 AD FS 배포를 디자인 하려면 이러한 지침을 사용할 수 있습니다. 이 가이드를 읽고 완료 수집, 문서화 및 매핑을 조직의 요구 사항을 갖게 됩니다의 지침을 사용 하 여 AD FS 배포를 시작 하는 데 필요한 정보를 [Windows Server 2012 AD FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-AD-FS-Deployment-Guide.md).  
  
## <a name="in-this-guide"></a>이 가이드의 내용  
  
-   [AD FS 배포 목표 식별](Identifying-Your-AD-FS-Deployment-Goals.md)  
  
-   [AD FS 디자인에 배포 목표 매핑](Mapping-Your-Deployment-Goals-to-an-AD-FS-Design.md)  
  
-   [AD FS 배포 토폴로지 결정](Determine-Your-AD-FS-Deployment-Topology.md)  
  
-   [배포 계획](Planning-Your-Deployment.md)  
  
-   [페더레이션 서버 배치 계획](Planning-Federation-Server-Placement.md)  
  
-   [페더레이션 서버 프록시 배치 계획](Planning-Federation-Server-Proxy-Placement.md)  
  
-   [AD FS 서버 용량 계획](Planning-for-AD-FS-Server-Capacity.md)  
  
-   [부록 a: AD FS 요구 사항 검토](Appendix-A--Reviewing-AD-FS-Requirements.md)  
  

