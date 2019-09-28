---
ms.assetid: bb16e39d-566d-436c-b957-394c06d556db
title: Windows Server 2012의 AD FS 디자인 가이드
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d9d7ec6f4ff575d3aac30b7127e591b78f5ef49b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359210"
---
# <a name="ad-fs-design-guide-in-windows-server"></a>Windows Server의 AD FS 디자인 가이드 


  
> [!NOTE]  
> Windows Server 2012 r 2에서 AD FS를 배포 하는 방법에 대 한 자세한 내용은 [Windows server 2012 r2 AD FS Deployment Guide](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)를 참조 하십시오.  
  
페더레이션 서비스 공급자 역할의 Windows Server® 2012 운영 체제와 함께 Active Directory® Federation Services \(AD FS @ no__t-1을 사용 하 여 사용자를 웹 @ no__t-2 기반 서비스 또는에 상주 하는 응용 프로그램에 원활 하 게 인증할 수 있습니다. 리소스 파트너 조직에서 두 조직의 네트워크 간에 외부 트러스트 또는 포리스트 트러스트를 만들거나 유지 관리할 필요 없이 사용자가 두 번 로그온 할 필요 없이 리소스 파트너 조직입니다. 사용자의 반복적인 로그온 작업 부담 없이 다른 네트워크의 리소스에 액세스 하는 동안 한 네트워크에 인증 하는 프로세스는 \(SSO @ no__t-2에서 single sign @ no__t-0on 알려져 있습니다.  
  
## <a name="about-this-guide"></a>이 가이드 정보  
이 가이드는 조직의 요구 사항에 따라 AD FS의 새 배포를 계획 하는 데 도움이 되는 권장 사항을 제공 합니다 .이 가이드에서는 배포 목표 @ no__t-1과 만들려는 특정 디자인으로 @no__t. 이 가이드는 인프라 전문가 또는 시스템 설계자용으로 작성되었습니다. AD FS 배포를 계획할 때 주요 결정 사항을 강조 표시 합니다. 이 가이드를 읽기 전에 AD FS 기능 수준에서 작동 하는 방식에 대해 잘 알고 있어야 합니다. 또한 AD FS 설계에 반영 될 조직의 요구 사항에 대해 잘 알고 있어야 합니다.  
  
이 가이드에서는 세 가지 기본 AD FS 디자인을 기반으로 하는 배포 목표 집합을 설명 하 고 사용자 환경에 가장 적합 한 디자인을 결정 하는 데 도움을 줍니다. 이러한 배포 목표를 사용 하 여 다음과 같은 포괄적인 AD FS 디자인 중 하나 또는 환경의 요구 사항을 충족 하는 사용자 지정 디자인을 구성할 수 있습니다.  
  
-   비즈니스 @ no__t-0to @ no__t-1business \(B2B @ no__t 시나리오를 지원 하 고 독립 포리스트를 사용 하는 비즈니스 단위 간의 공동 작업을 지원 하기 위한 페더레이션된 웹 SSO  
  
-   비즈니스의 응용 프로그램에 대 한 고객 액세스를 지 원하는 웹 SSO @ no__t-0to @ no__t-1consumer \(B2C @ no__t 시나리오  
  
각 디자인에 대해 필요한 사용자 환경 관련 데이터를 수집하는 지침을 확인합니다. 그런 다음 이러한 지침을 사용 하 여 AD FS 배포를 계획 하 고 디자인할 수 있습니다. 이 가이드를 읽고 조직 요구 사항의 수집, 문서화 및 매핑을 완료 한 후에는 [Windows Server 2012 AD FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-AD-FS-Deployment-Guide.md)의 지침을 사용 하 여 AD FS 배포를 시작 하는 데 필요한 정보를 제공 합니다.  
  
## <a name="in-this-guide"></a>이 가이드의 내용  
  
-   [AD FS 배포 목표 확인](Identifying-Your-AD-FS-Deployment-Goals.md)  
  
-   [AD FS 디자인에 배포 목표 매핑](Mapping-Your-Deployment-Goals-to-an-AD-FS-Design.md)  
  
-   [AD FS 배포 토폴로지 결정](Determine-Your-AD-FS-Deployment-Topology.md)  
  
-   [배포 계획](Planning-Your-Deployment.md)  
  
-   [페더레이션 서버 배치 계획](Planning-Federation-Server-Placement.md)  
  
-   [페더레이션 서버 프록시 배치 계획](Planning-Federation-Server-Proxy-Placement.md)  
  
-   [AD FS 서버 용량 계획](Planning-for-AD-FS-Server-Capacity.md)  
  
-   [부록 A: AD FS 요구 사항 검토](Appendix-A--Reviewing-AD-FS-Requirements.md)  
  

