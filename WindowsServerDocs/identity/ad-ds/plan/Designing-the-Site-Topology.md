---
ms.assetid: eeb919de-e21e-48d8-8186-e42adec6933f
title: "사이트 토폴로지 디자인"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3f16b5b941ef9c3bd8f4bf742d432afc1b3f559a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="designing-the-site-topology"></a>사이트 토폴로지 디자인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

디렉터리 서비스 사이트 토폴로지는 실제 네트워크 논리를 표시 합니다. 사이트 토폴로지 Active Directory Domain Services (AD DS)에 대 한 디자인 도메인 컨트롤러 배치 및 디자인 사이트, 서브넷, 사이트 링크, 및 쿼리와 복제 트래픽 효율적인 경로 되도록 사이트 링크 다리 계획 해야 합니다.  
  
사이트 토폴로지 디자인 효율적으로 클라이언트 쿼리가 및 Active Directory 복제 교통 수 있습니다. 적합된 사이트 토폴로지는 다음과 같은 혜택 달성 조직 도움이 됩니다.  
  
-   복제 Active Directory 데이터 비용을 최소화 합니다.  
  
-   사이트 토폴로지 유지 하는 데 필요한 관리 작업을 최소화 합니다.  
  
-   복제 사용량이 Active Directory 데이터 복제할 느리거나 전화 접속 네트워크 연결을 사용 하 여 위치 수 있도록 예약 합니다.  
  
-   도메인 컨트롤러 (분산 파일 시스템) 서버의 등 가장 가까운 리소스를 찾는 클라이언트 컴퓨터의 기능을 최적화 합니다. 이 사용이 하면 슬로우 넓은 지역에서 네트워크 사용량을 줄이기 위해 네트워크 WAN 연결 로그온 한 로그 오프 프로세스를 향상 하 고 파일 다운로드 작업 속도 합니다.  
  
사이트 토폴로지의 디자인을 시작 하기 전에 실제 네트워크 구조를 알고 있어야 합니다. 또한 관리 계층, 숲 계획 및 각 숲에 대 한 계획 도메인을 포함 하 여 Active Directory 논리 구조를 디자인 먼저 해야 합니다. 또한 AD DS에 대 한 시스템 DNS (도메인 이름) infrastructure 디자인을 완료 해야 합니다. Active Directory 논리 구조 및 DNS infrastructure 디자인에 대 한 자세한 내용은 참조 [논리 구조 Windows Server 2008 AD DS 디자인](https://technet.microsoft.com/library/cc770806.aspx)합니다.  
  
사이트 토폴로지 디자인을 완료 된 후 도메인 컨트롤러 Windows Server 2008 표준, Windows Server 2008 Enterprise 및 Windows Server 2008 Datacenter 위한 하드웨어 요구 사항을 충족 하는지 확인 해야 합니다.  
  
## <a name="in-this-guide"></a>이 가이드  
  
-   [이해 Active Directory 사이트 토폴로지](../../ad-ds/plan/Understanding-Active-Directory-Site-Topology.md)  
  
-   [네트워크 정보를 수집합니다.](../../ad-ds/plan/Collecting-Network-Information.md)  
  
-   [도메인 컨트롤러 배치 계획](../../ad-ds/plan/Planning-Domain-Controller-Placement.md)  
  
-   [사이트 디자인 만들기](../../ad-ds/plan/Creating-a-Site-Design.md)  
  
-   [사이트 링크 디자인 만들기](../../ad-ds/plan/Creating-a-Site-Link-Design.md)  
  
-   [사이트 링크 다리 디자인 만들기](../../ad-ds/plan/Creating-a-Site-Link-Bridge-Design.md)  
  
-   [Windows Server 2008 Active Directory 사이트 토폴로지 디자인에 대 한 추가 리소스 찾기](../../ad-ds/plan/Finding-Additional-Resources-for-Windows-Server-2008-Active-Directory-Site-Topology-Design.md)  
  


