---
ms.assetid: bb16e39d-566d-436c-b957-394c06d556db
title: "Windows Server 2012의에서 지침에 따라 AD FS 디자인"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e660c1dabcc5a683fa74068ea148fd4efbeee569
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="ad-fs-design-guide-in-windows-server-2012"></a>Windows Server 2012의에서 지침에 따라 AD FS 디자인

>적용 대상: Windows Server 2012
  
> [!NOTE]  
> Windows Server 2012 r 2에서 ADFS 배포 하는 방법에 대 한 내용은 [Windows Server 2012 r 2 광고 FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)합니다.  
  
원활 하 게 만들거나 외부 신뢰 또는 숲 신뢰 하 고 사용자를 두 번의 로그인에 대 한 필요 없이 모두 조직 네트워크 사이의 유지 하는 관리자에 대 한 필요성 없이 리소스 파트너 회사에 거주 하는 응용 프로그램 또는 Web\ 기반 서비스에 사용자가 인증 Active Directory Federation 서비스® \(AD FS\) federation 서비스 공급자 역할에서® Windows Server 2012 운영 체제에 사용할 수 있습니다. 다른 네트워크 리소스에 액세스 하는 동안 한 네트워크에 인증 과정-반복된 로그온 작업 하 여 사용자의 부담 없이-단일 sign\ \(SSO\)로 알려져 있습니다.  
  
## <a name="about-this-guide"></a>이 가이드 정보  
이 가이드에서는 조직의 요구 사항에 따라 Adfs의 새 배포를 계획 하는 데 도움이 되는 엔터프라이즈 \ (함 배포 goals\로이 가이드에서) 만들려는 특정 디자인 하 고 있습니다. 이 가이드는 인프라 전문가 또는 시스템 설계자 사용에 대 한 것입니다. ADFS 배포 계획할 주 결정 지점 강조 표시 합니다. 이 가이드를 읽으려면 먼저 ADFS 기능 수준에서 작동 하는 방법을는 잘 알고가 있어야 합니다. 또한 ADFS 디자인 구성 요구 사항이 반영 될 수 있는는 잘 알고가 있어야 합니다.  
  
이 가이드는 일련의 세 가지 주요 ADFS 디자인을 기반으로 하는 배포 목표에 설명 하 고 귀하의 환경에 대 한 가장 적합 한 디자인 결정 하는 데 도움이 됩니다. 이러한 배포 목표에 다음과 같은 포괄적인 ADFS 디자인 또는 귀하의 환경의 요구를 충족 하는 사용자 지정 디자인 중 하나를 사용할 수 있습니다.  
  
-   연결 된 웹 SSO business\ to\ 비즈니스 \(B2B\) 시나리오를 지원 하 고 숲 독립적으로 업무 단위 간에 공동 작업을 지원 하기 위해  
  
-   웹 SSO business\ to\ 소비자 \(B2C\) 시나리오에서 고객 응용 프로그램에 대 한 액세스를 지원 하기 위해  
  
각 디자인에 대 한 필요한 귀하의 환경에 대 한 데이터 수집에 대 한 지침을 볼 수 있습니다. 그런 다음 계획 및 ADFS 배포 디자인 다음이 지침을 사용할 수 있습니다. 이 가이드 하 고 수집, 기록 및 회사의 요구 사항에 매핑하 완료 한 후 Adfs의 지침을 사용 하 여 배포를 시작 하는 데 필요한 정보는는 [Windows Server 2012 광고 FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-AD-FS-Deployment-Guide.md)합니다.  
  
## <a name="in-this-guide"></a>이 가이드  
  
-   [광고 FS 배포 목표에 확인](Identifying-Your-AD-FS-Deployment-Goals.md)  
  
-   [AD FS 디자인에 배포 목표 매핑](Mapping-Your-Deployment-Goals-to-an-AD-FS-Design.md)  
  
-   [해당 AD FS 배포가 확인](Determine-Your-AD-FS-Deployment-Topology.md)  
  
-   [배포를 계획](Planning-Your-Deployment.md)  
  
-   [Federation 서버 배치 계획](Planning-Federation-Server-Placement.md)  
  
-   [Federation 서버 프록시 배치 계획](Planning-Federation-Server-Proxy-Placement.md)  
  
-   [광고 FS 서버 용량에 대 한 계획](Planning-for-AD-FS-Server-Capacity.md)  
  
-   [부록 a: 검토 광고 FS 요구 사항](Appendix-A--Reviewing-AD-FS-Requirements.md)  
  

