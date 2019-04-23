---
title: 데스크톱 호스팅 참조 아키텍처
description: 데스크톱 호스팅 RDS 및 Azure를 사용 하 여 솔루션을 만들기 위한 아키텍처 지침입니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 11/02/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1bac5dd3-8430-46ee-8bef-10cc4b7cc437
author: lizap
manager: dongill
ms.openlocfilehash: 6f235fd89c34c00601c802f4ea71e440af630169
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890244"
---
# <a name="desktop-hosting-reference-architecture"></a>데스크톱 호스팅 참조 아키텍처

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 문서에서는 Windows 데스크톱 및 응용 프로그램 호스트 되는 원격 데스크톱 서비스 (RDS) 및 Microsoft Azure virtual machines를 사용 하 여 다중 테 넌 트를 만드는 아키텍처 블록의 집합을 정의 "데스크톱 호스팅" 이라고 하는 서비스를 항상 안전 하 고 확장성 있는 안정적인 데스크톱 호스팅 5 ~ 5000 사용자와 소규모 및 중간 규모 조직에 대 한 솔루션을 만들려면이 아키텍처 참조를 사용할 수 있습니다.    
  
이 참조 아키텍처의 주요 사용자는 하려는 호스팅 공급자를 통해 여러 테 넌 트에 데스크톱 호스팅 서비스를 제공 하려면 Microsoft Azure 인프라 서비스 및 Sal (구독자 액세스 라이선스)를 활용 하 여 [ Microsoft 서비스 공급자 라이선스 계약](https://www.microsoft.com/hosting/en/us/licensing/splabenefits.aspx) (SPLA) 프로그램. 이 참조 아키텍처에 대 한 두 번째 대상 그룹을 만들고 사용 하 여 자체 직원에 대 한 Microsoft Azure 인프라 서비스에서 데스크톱 호스팅 솔루션을 관리 하려는 최종 고객은 [RDS 사용자 Cal 확장 권한이 소프트웨어를 통해 Assurance](https://download.microsoft.com/download/6/B/A/6BA3215A-C8B5-4AD1-AA8E-6C93606A4CFB/Windows_Server_2012_R2_Remote_Desktop_Services_Licensing_Datasheet.pdf) (SA).   
  
데스크톱 호스팅 솔루션 호스팅에 전달할 파트너 및 SA 고객에 게는 Windows 사용자는 비즈니스 사용자 및 소비자에 게 친숙 한 응용 프로그램 환경을 제공 하기 위해 Windows Server를 활용 합니다. Windows 10의 토대를 기반으로 Windows Server 2016은 친숙 한 응용 프로그램 지원 및 사용자 경험 합니다.    
  
이 문서의 범위 제한 됩니다.   
  
* 데스크톱 호스팅 서비스에 대 한 아키텍처 설계 지침입니다. 자세한 내용은 배포 절차, 성능 및 용량 계획 같은 별도 문서에 설명 되어 있습니다. Azure 인프라 서비스에 대 한 보다 일반적인 정보를 참조 하세요. [Microsoft Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/)합니다.   
  
* 세션 기반 데스크톱, RemoteApp 응용 프로그램 및 Windows Server 2016 원격 데스크톱 세션 호스트 (RD 세션 호스트)를 사용 하는 서버 기반 개인 데스크톱입니다. Windows 클라이언트 기반 가상 데스크톱 인프라 없는 서비스 공급자 라이선스 계약 SPLA () Windows 클라이언트 운영 체제에 대 한 있기 때문에 다루지 않습니다. Windows Server 기반 가상 데스크톱 인프라는 SPLA에서 허용 되며 특정 시나리오에서 최종 고객 라이선스를 사용 하 여 전용된 하드웨어에서 Windows 클라이언트 기반 가상 데스크톱 인프라 허용 됩니다. 그러나 클라이언트 기반 가상 데스크톱 인프라는 범위를 벗어나는이 문서에 대 한 합니다.   
  
* Microsoft 제품 및 기능을 기본적으로 Windows Server 2016 및 Microsoft Azure 인프라 서비스입니다.   
  
* 다양 한 규모의 5에서 5000 사용자에 게 테 넌 트에 대 한 서비스를 호스팅하는 데스크톱.   더 큰 테 넌 트에 대 한 적절 한 성능을 제공 하기 위해이 아키텍처를 수정 해야 합니다. RDS 서버 관리자 그래픽 사용자 인터페이스 (GUI)를 권장 되지 않습니다 배포용 500 명 이상의 사용자. 500 및 5000 사용자 간의 RDS 배포를 관리 하는 것에 대 한 PowerShell은 사용 하는 것이 좋습니다.   
  
* 구성 요소 및 서비스 하는 데스크톱 호스팅 서비스에 필요한 최소 집합입니다. 선택적 구성 요소 및 서비스를 호스팅하는 데스크톱을 강화 하기 위해 추가할 수 있는 서비스를 많이 있지만 범위를 벗어나는이 문서에 대 한 합니다.    
  
이 문서를 읽은 후 판독기 이해 해야 합니다.   
- 보안성, 안정성, 다중 테 넌 트 데스크톱 호스팅 솔루션을 Microsoft Azure 서비스에 기반을 제공 하는 데 필요한 구성 요소입니다.  
- 각 문서 블록의 용도 및 서로 연결 되는 방법입니다.  
  
여러 가지 방법으로 데스크톱 호스팅이 아키텍처를 기반으로 하는 솔루션을 빌드할 수 있습니다. 이 아키텍처에서는 통합 및 Windows Server 2016을 사용 하 여 Azure의 향상 된 기능을 설명합니다. 다른 배포 옵션을 사용 하 여 사용할 수는 [데스크톱 호스팅 참조 아키텍처 가이드](https://go.microsoft.com/fwlink/p/?LinkId=517389) Windows Server 2012 R2에 대 한 합니다.    
  
이 섹션에서 다루는 항목은 다음과 같습니다.  
- [데스크톱 호스팅 논리 아키텍처](Desktop-hosting-logical-architecture.md)  
- [RDS 역할 이해](Understanding-RDS-roles.md)
- [데스크톱 호스팅 환경 이해](Understanding-the-desktop-hosting-environment.md)  
- [Azure 서비스 및 데스크톱 호스팅에 대 한 고려 사항](Azure-services-and-considerations-for-desktop-hosting.md)
  
 


