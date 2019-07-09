---
title: 데스크톱 호스팅 참조 아키텍처
description: RDS 및 Azure를 사용하여 데스크톱 호스팅 솔루션 솔루션을 만들기 위한 아키텍처 지침입니다.
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
ms.openlocfilehash: 01560a3758963c17c4ea0cb94b806c3b99193464
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "63749239"
---
# <a name="desktop-hosting-reference-architecture"></a>데스크톱 호스팅 참조 아키텍처

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

이 문서에서는 RDS(Remote Desktop Services) 및 Microsoft Azure Virtual Machines를 사용하여 다중 테넌트, 호스트된 Windows 데스크톱 및 애플리케이션 서비스(“데스크톱 호스팅”이라고 함)를 만들기 위한 아키텍처 블록 세트를 정의합니다. 이 아키텍처 참조를 사용하여 사용자가 5~5,000명인 중소기업을 위해 안전하고 확장 가능하며 안정적인 데스크톱 호스팅 솔루션을 만들 수 있습니다.    
  
이 참조 아키텍처의 주요 대상은 [SPLA(Microsoft Service Provider Licensing Agreement)](https://www.microsoft.com/hosting/en/us/licensing/splabenefits.aspx) 프로그램을 통해 여러 테넌트에 데스크톱 호스팅 서비스와 SAL(Subscriber Access License)을 제공하기 위해 Microsoft Azure Infrastructure Services를 활용하려는 호스팅 공급 기업입니다. 이 참조 아키텍처의 두 번째 고객은 직원들이 [SA(Software Assurance)를 통해 RDS 사용자 단위 CAL 확장 권한](https://download.microsoft.com/download/6/B/A/6BA3215A-C8B5-4AD1-AA8E-6C93606A4CFB/Windows_Server_2012_R2_Remote_Desktop_Services_Licensing_Datasheet.pdf)을 사용할 수 있도록 Microsoft Azure Infrastructure Services에서 데스크톱 호스팅 솔루션을 생성하고 관리하고자 하는 최종 고객입니다.   
  
데스크톱 호스팅 솔루션을 제공하기 위해 호스팅 파트너 및 SA 고객은 Windows Server를 사용하여 Windows 사용자에게 비즈니스 사용자와 소비자에게 익숙한 애플리케이션 환경을 제공합니다. Windows 10의 토대를 기반으로 Windows Server 2016은 친숙한 애플리케이션 지원 및 사용자 환경을 제공합니다.    
  
이 문서의 범위는 다음으로 제한됩니다.   
  
* 데스크톱 호스팅 서비스에 대한 아키텍처 설계 지침. 배포 절차, 성능 및 용량 계획과 같은 자세한 내용은 별도 문서에 설명되어 있습니다. Azure Infrastructure Services에 대한 더 일반적인 정보는 [Microsoft Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/)를 참조하세요.   
  
* 세션 기반 데스크톱, RemoteApp 애플리케이션 및 Windows Server 2016 RD Session Host(원격 데스크톱 세션 호스트)를 사용하는 서버 기반 개인 데스크톱. Windows 클라이언트 기반 가상 데스크톱 인프라는 Windows 클라이언트 운영 체제에 대한 SPLA(Service Provider License Agreement)가 없기 때문에 적용되지 않습니다. Windows 서버 기반 가상 데스크톱 인프라는 SPLA에 따라 허용되며, Windows 클라이언트 기반 가상 데스크톱 인프라는 특정 시나리오에서 최종 고객 라이선스가 있는 전용 하드웨어에서 허용됩니다. 단, 클라이언트 기반 가상 데스크톱 인프라는 이 문서에서 다루지 않습니다.   
  
* Microsoft 제품 및 기능, 기본적으로 Windows Server 2016 및 Microsoft Azure Infrastructure Services.   
  
* 사용자 수가 5~5000명인 테넌트를 위한 데스크톱 호스팅 서비스.   대규모 테넌트의 경우, 적절한 성능을 제공하기 위해서는 이 아키텍처를 수정해야 할 수도 있습니다. 사용자가 500명 이상인 배포에는 서버 관리자 RDS GUI(그래픽 사용자 인터페이스)가 권장되지 않습니다. 사용자가 500명에서 5000명 사이인 RDS 배포를 관리하려면 PowerShell이 권장됩니다.   
  
* 데스크톱 호스팅 서비스에 필요한 최소 구성 요소 및 서비스 세트. 데스크톱 호스팅 서비스를 향상시키기 위해 추가할 수 있는 선택적 구성 요소와 서비스가 많이 있지만, 이 문서에서는 다루지 않습니다.    
  
이 문서를 읽은 후에는 다음을 이해해야 합니다.   
- Microsoft Azure Services에 기반을 둔 안전하고 안정적인 다중 테넌트 데스크톱 호스팅 솔루션을 제공하는 데 필요한 구성 요소.  
- 각 구성 요소의 목적 및 서로 얼마나 적합한지.  
  
이 아키텍처를 기반으로 데스크톱 호스팅 솔루션을 빌드하는 방법은 여러 가지가 있습니다. 이 아키텍처는 Windows Server 2016과의 Azure의 통합 및 개선 사항을 간략히 설명합니다. 다른 배포 옵션은 Windows Server 2012 R2용 [데스크톱 호스팅 참조 아키텍처 가이드](https://go.microsoft.com/fwlink/p/?LinkId=517389)에서 사용할 수 있습니다.    
  
이 섹션에서 다루는 항목은 다음과 같습니다.  
- [데스크톱 호스팅 논리 아키텍처](Desktop-hosting-logical-architecture.md)  
- [RDS 역할 이해](Understanding-RDS-roles.md)
- [데스크톱 호스팅 환경 이해](Understanding-the-desktop-hosting-environment.md)  
- [데스크톱 호스팅을 위한 Azure 서비스 및 고려 사항](Azure-services-and-considerations-for-desktop-hosting.md)
  
 


