---
title: SDN RAS 게이트웨이
description: 넌, Windows Server 2016에 테두리 게이트웨이 프로토콜 (BGP) 가능 라우터 소프트웨어 기반 인 RAS 게이트웨이 대해 자세히 알아보려면이 항목을 사용할 수 있습니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a32357a5-ab1a-4a4c-848a-7a4ed65b1921
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 052911dcd52df82ef4e259de0c64078c54f00195
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="ras-gateway-for-sdn"></a>SDN RAS 게이트웨이

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

소프트웨어를 기반으로 넌, 테두리 게이트웨이 프로토콜 (BGP) 가능 라우터 (Csp) 클라우드 서비스 공급자 및 네트워크 가상화 Hyper-v를 사용 하 여 여러 테 가상 네트워크 호스트 하는 기업으로 디자인 된 Windows Server 2016에에서는 RAS 게이트웨이 대 한 자세한 내용은이 항목을 사용할 수 있습니다.  
  
> [!NOTE]  
> 이 항목에서는 뿐만 아니라 다음 RAS 게이트웨이 항목 사용할 수 있습니다.  
>   
> -   [RAS 게이트웨이의 새로운 기능](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md)  
> -   [RAS 게이트웨이 배포 건축물](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-Deployment-Architecture.md)  
> -   [RAS 게이트웨이 높은 공급 일](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)  
> -   [테두리 게이트웨이 프로토콜 & #40; BGP & #41;](../../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)  
> -   [BGP Windows PowerShell 명령 참조](../../../../remote/remote-access/bgp/BGP-Windows-PowerShell-Command-Reference.md)  
  
Windows Server 2016 RAS 게이트웨이 실제 네트워크 및 리소스는 어디에 관계 없이 VM 네트워크 리소스를 간에 네트워크 트래픽을 전송 합니다. RAS 게이트웨이 간에 물리적 및 가상 네트워크 또는 인터넷을 통해 여러 물리적 위치의 실제 위치에서 네트워크 교통 경로 사용할 수 있습니다.  
  
멀티 텐 던 시 여러 소유 가상 컴퓨터 작업을 지원, 아직 같은 인프라에 모든 작업을 실행 하는 동안 서로 격리 클라우드 infrastructure 기능입니다. 개별 테의 여러 작업 interconnect 수 원격으로 관리할 수 있지만 다른 테 넌 작업으로 이러한 시스템 interconnect 하지 않습니다 없으며 다른 테 넌 원격으로 관리할 수 있습니다.  
  
## <a name="prerequisites-for-installing-ras-gateway-for-sdn"></a>RAS 게이트웨이 SDN를 설치 하는 사항  
SDN와 함께 사용할 넌 모드로 RAS 게이트웨이 배포할 때 원격 액세스를 설치 하 여 Windows 인터페이스를 사용할 수 없습니다. 대신 Windows PowerShell 사용 해야 합니다.  
  
하지만 Windows PowerShell 추가를 사용 해야 RAS 게이트웨이 Windows PowerShell를 사용 하 여 설치 하기 전에 **원격 액세스** Windows 기능입니다. 이렇게 하기 위해 Windows PowerShell 프롬프트에서 다음 명령을 실행 합니다.  
  
`Add-WindowsFeature -Name RemoteAccess -IncludeAllSubFeature -IncludeManagementTools`  
  
이 명령을 추가 **원격 액세스** 기능에 대 한 Windows PowerShell 명령 및 기능입니다.  
  
추가 하 고 나면 **원격 액세스** 서버에 대 한 원격 액세스 넌 모드로 RAS 게이트웨이 및 테두리 게이트웨이 프로토콜 (BGP)으로 설치할 수 있습니다.  
  
자세한 내용은 참조 Windows PowerShell 참조 항목 [설치-원격 액세스](https://technet.microsoft.com/library/hh918408.aspx)합니다.  
  
## <a name="ras-gateway-features"></a>RAS 게이트웨이 기능  
다음은 Windows Server 2016에 RAS 게이트웨이 기능입니다. 이러한 기능을 모두 한 번에 사용 하는 높은 가용성 풀의 RAS 게이트웨이 배포할 수 있습니다.  
  
-   **사이트에서 VPN**합니다. 이 RAS 게이트웨이 기능을 사용 하면 사이트에서 VPN 연결을 사용 하 여 인터넷을 통해 두 네트워크 서로 다른 위치에 연결할 수 있습니다. 자신의 데이터 센터에 많은 테 넌 호스트 하는 Csp RAS 게이트웨이 사용자 테 넌 액세스 하 고 원격 사이트에서 VPN 연결에 사이트를 통해 자신의 리소스를 관리할 수 있도록 해 주는 하 고 네트워크 교통 흐름 데이터 센터의 가상 리소스 사이의 물리적 해당 네트워크를 사용할 수 있는 넌 게이트웨이 해결할을 수 있습니다.  
  
-   **사이트에 포인트 VPN**합니다. 이 RAS 게이트웨이 기능 조직 직원이 또는 관리자 원격 위치에서 조직의 네트워크에 연결할 수 있습니다.  넌 배포에 대 한 테 네트워크 관리자 가상 네트워크 리소스 CSP 데이터 센터에 액세스할 수 지점 사이트 VPN 연결을 사용할 수 있습니다.  
  
-   **GRE 터널링**합니다. 일반 경로 캡슐화 (GRE) 터널 사용 테 가상 네트워크와 외부 네트워크 연결이 기반 으로합니다. GRE은 대부분의 네트워크 디바이스에서 사용할 수 있는 GRE 프로토콜 간단 하 고 지원을 이상적입니다. 터널링에 대 한 데이터를 암호화 필요 하지 않습니다 됩니다. 이 항목 뒷부분에 설명 된 대로 (S2S) 터널 사이트의에서 지원 GRE 테 가상 네트워크와 테 외부 네트워크를 사용 하 여 여러 테 게이트웨이 사이의 전달의 문제가 해결 되었습니다.  
  
-   **동적 테두리 게이트웨이 프로토콜 (BGP)와 경로**합니다. 동적 라우팅 프로토콜 고 자동으로 사이트에서 VPN 연결을 사용 하 여 연결 하는 사이트 간에 경로 학습 있기 때문에 BGP 라우터에 수동 경로 구성에 대 한 필요성을 줄입니다. 조직에서는 RAS 게이트웨이 등 BGP 활성화 라우터를 사용 하 여 연결 하는 여러 사이트를 BGP 라우터를 자동으로 계산 하 고 네트워크 중단이 발생 하거나 오류 시 서로 유효한 경로 사용할 수 있게 합니다. 자세한 내용은 참조 [RFC 4271](https://tools.ietf.org/html/rfc4271)합니다.  
  

  


