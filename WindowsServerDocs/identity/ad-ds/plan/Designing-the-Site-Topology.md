---
ms.assetid: eeb919de-e21e-48d8-8186-e42adec6933f
title: 사이트 토폴로지 디자인
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e1d9323ceda478369973f959687d46c9ca3cb88f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888494"
---
# <a name="designing-the-site-topology"></a>사이트 토폴로지 디자인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

디렉터리 서비스 사이트 토폴로지는 실제 네트워크의 논리적 표현입니다. Active Directory Domain Services (AD DS)에 대 한 사이트 토폴로지 디자인 도메인 컨트롤러 배치 및 디자인 사이트, 서브넷, 사이트 링크 및 효율적인 쿼리 및 복제 트래픽 라우팅 되도록 사이트 링크 브리지에 대 한 계획 해야 합니다.  
  
사이트 토폴로지 디자인을 통해 클라이언트 쿼리 및 Active Directory 복제 트래픽을 효율적으로 라우팅할 수 있습니다. 잘 설계 된 사이트 토폴로지는 다음과 같은 이점이 조직에 도움이 됩니다.  
  
-   Active Directory 데이터를 복제 하는 비용을 최소화 합니다.  
  
-   사이트 토폴로지를 유지 관리 하는 데 필요한 관리 노력을 최소화 합니다.  
  
-   사용량이 적은 시간 동안 Active Directory 데이터를 복제할 저속 또는 전화 접속 네트워크 링크를 사용 하 여 위치를 사용 하도록 설정 하는 복제를 예약 합니다.  
  
-   찾은 도메인 컨트롤러 및 파일 시스템 (DFS (분산) 서버와 같은 리소스를 가장 가까운 하는 클라이언트 컴퓨터의 기능을 최적화 합니다. 속도가 느린 광역을 통해 네트워크 트래픽을 줄이기 위해이 사용이 하면 네트워크 (WAN) 링크, 로그온 및 로그 오프 프로세스를 개선 및 파일 다운로드 작업의 속도.  
  
사이트 토폴로지 디자인을 시작 하기 전에 실제 네트워크 구조를 이해 해야 합니다. 또한 관리 계층 구조, 포리스트 계획 및 각 포리스트에 대해 도메인 계획을 포함 하 여 Active Directory 논리 구조를 먼저 디자인 해야 합니다. 또한 AD DS에 대 한 도메인 이름 시스템 (DNS) 인프라 디자인을 완료 해야 합니다. DNS 인프라 고 Active Directory 논리 구조 디자인에 대 한 자세한 내용은 참조 하세요. [는 논리 구조에 대 한 Windows Server 2008 AD DS 디자인](https://technet.microsoft.com/library/cc770806.aspx)합니다.  
  
사이트 토폴로지 디자인을 마친 후 도메인 컨트롤러에 Windows Server 2008 Standard, Windows Server 2008 Enterprise 및 Windows Server 2008 Datacenter의 하드웨어 요구 사항을 충족 하는지 확인 해야 합니다.  
  
## <a name="in-this-guide"></a>이 가이드의 내용  
  
-   [Active Directory 사이트 토폴로지 이해](../../ad-ds/plan/Understanding-Active-Directory-Site-Topology.md)  
  
-   [네트워크 정보를 수집합니다.](../../ad-ds/plan/Collecting-Network-Information.md)  
  
-   [도메인 컨트롤러 배치 계획](../../ad-ds/plan/Planning-Domain-Controller-Placement.md)  
  
-   [사이트 디자인 만들기](../../ad-ds/plan/Creating-a-Site-Design.md)  
  
-   [사이트 링크 디자인 만들기](../../ad-ds/plan/Creating-a-Site-Link-Design.md)  
  
-   [사이트 링크 브리지 디자인 만들기](../../ad-ds/plan/Creating-a-Site-Link-Bridge-Design.md)  
  
-   [Windows Server 2008 Active Directory 사이트 토폴로지 디자인에 대 한 추가 리소스 찾기](../../ad-ds/plan/Finding-Additional-Resources-for-Windows-Server-2008-Active-Directory-Site-Topology-Design.md)  
  


