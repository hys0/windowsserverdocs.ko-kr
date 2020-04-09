---
ms.assetid: eeb919de-e21e-48d8-8186-e42adec6933f
title: 사이트 토폴로지 디자인
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: e7b6267946217d5c5fb57496eb6bf54911b61e8a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822603"
---
# <a name="designing-the-site-topology"></a>사이트 토폴로지 디자인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

디렉터리 서비스 사이트 토폴로지는 실제 네트워크를 논리적으로 표현한 것입니다. Active Directory Domain Services (AD DS)에 대 한 사이트 토폴로지 디자인에는 도메인 컨트롤러 배치 계획 및 사이트, 서브넷, 사이트 링크 및 사이트 링크 브리지를 계획 하 여 쿼리 및 복제 트래픽을 효율적으로 라우팅하는 작업이 포함 됩니다.  
  
사이트 토폴로지를 디자인 하면 클라이언트 쿼리를 효율적으로 라우팅하고 복제 트래픽을 Active Directory 수 있습니다. 잘 설계 된 사이트 토폴로지를 사용 하면 조직에서 다음과 같은 이점을 얻을 수 있습니다.  
  
-   Active Directory 데이터를 복제 하는 비용을 최소화 합니다.  
  
-   사이트 토폴로지를 유지 관리 하는 데 필요한 관리 노력을 최소화 합니다.  
  
-   저속 또는 전화 접속 네트워크 연결을 사용 하는 위치에서 사용량이 적은 시간에 Active Directory 데이터를 복제할 수 있는 복제를 예약 합니다.  
  
-   클라이언트 컴퓨터의 기능을 최적화 하 여 도메인 컨트롤러 및 분산 파일 시스템 (DFS) 서버와 같은 가장 근접 한 리소스를 찾습니다. 이를 통해 저속 WAN (광역 네트워크) 링크를 통해 네트워크 트래픽을 줄이고, 로그온 및 로그 오프 프로세스를 개선 하 고, 파일 다운로드 작업 속도를 높일 수 있습니다.  
  
사이트 토폴로지 디자인을 시작 하기 전에 실제 네트워크 구조를 이해 해야 합니다. 또한 먼저 각 포리스트에 대 한 관리 계층, 포리스트 계획 및 도메인 계획을 포함 하 여 Active Directory 논리 구조를 디자인 해야 합니다. AD DS에 대 한 DNS (Domain Name System) 인프라 디자인도 완료 해야 합니다. Active Directory 논리 구조 및 DNS 인프라를 디자인 하는 방법에 대 한 자세한 내용은 [Windows Server 2008에 대 한 논리 구조 디자인 AD DS](https://technet.microsoft.com/library/cc770806.aspx)을 참조 하세요.  
  
사이트 토폴로지 디자인을 완료 한 후에는 도메인 컨트롤러가 Windows Server 2008 Standard, Windows Server 2008 Enterprise 및 Windows Server 2008 Datacenter의 하드웨어 요구 사항을 충족 하는지 확인 해야 합니다.  
  
## <a name="in-this-guide"></a>설명서의 내용  
  
-   [Active Directory 사이트 토폴로지 이해](../../ad-ds/plan/Understanding-Active-Directory-Site-Topology.md)  
  
-   [네트워크 정보 수집](../../ad-ds/plan/Collecting-Network-Information.md)  
  
-   [도메인 컨트롤러 배치 계획](../../ad-ds/plan/Planning-Domain-Controller-Placement.md)  
  
-   [사이트 디자인 만들기](../../ad-ds/plan/Creating-a-Site-Design.md)  
  
-   [사이트 링크 디자인 만들기](../../ad-ds/plan/Creating-a-Site-Link-Design.md)  
  
-   [사이트 링크 브리지 디자인 만들기](../../ad-ds/plan/Creating-a-Site-Link-Bridge-Design.md)  
  
-   [사이트 토폴로지 디자인 Active Directory Windows Server 2008에 대 한 추가 리소스 찾기](../../ad-ds/plan/Finding-Additional-Resources-for-Windows-Server-2008-Active-Directory-Site-Topology-Design.md)  
  


