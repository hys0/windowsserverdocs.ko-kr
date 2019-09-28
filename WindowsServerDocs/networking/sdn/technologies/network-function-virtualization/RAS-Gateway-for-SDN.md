---
title: SDN용 RAS 게이트웨이
description: 이 항목을 사용 하 여 Windows Server 2016에서 사용할 수 있는 소프트웨어 기반, 다중 테 넌 트, 다중 테 넌 트 (Border Gateway Protocol)를 지 원하는 RAS 게이트웨이에 대해 알아볼 수 있습니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a32357a5-ab1a-4a4c-848a-7a4ed65b1921
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 20fc19dc31ee612de0a736bfe989f930a9afa202
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405865"
---
# <a name="ras-gateway-for-sdn"></a>SDN용 RAS 게이트웨이

>적용 대상: Windows Server (반기 채널), Windows Server 2016 # # RAS Gateway for SDN  


RAS 게이트웨이는 Hyper-v 네트워크 가상화를 사용 하 여 여러 테 넌 트 가상 네트워크를 호스팅하는 회사 및 Csp (클라우드 서비스 공급자) 용으로 설계 된 소프트웨어 기반, 다중 테 넌 트 Border Gateway Protocol (BGP) 지원 라우터입니다. RAS 게이트웨이는 위치에 관계 없이 실제 네트워크 리소스와 VM 네트워크 리소스 간에 네트워크 트래픽을 라우팅합니다. 네트워크 트래픽을 동일한 실제 위치 또는 여러 위치에서 라우팅할 수 있습니다.   

배포할지에은 여러 테 넌 트의 가상 컴퓨터 워크 로드를 지원 하 고, 모든 워크 로드를 동일한 인프라에서 실행 하는 클라우드 인프라의 기능입니다. 개별 테넌트의 여러 작업을 상호 연결하고 원격으로 관리할 수는 있지만, 이러한 시스템이 다른 테넌트의 작업과 서로 연결되거나 다른 테넌트에서 이러한 시스템을 원격으로 관리하지는 않습니다.

  
> [!NOTE]  
> 이 항목 외에 다음 RAS 게이트웨이 항목을 사용할 수 있습니다.  
>   
> -   [RAS 게이트웨이의 새로운 기능](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md)  
> -   [RAS 게이트웨이 배포 아키텍처](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-Deployment-Architecture.md)  
> -   [RAS 게이트웨이 고가용성](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)  
> -   [BGP &#40;Border Gateway Protocol&#41;](../../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)  
> -   [BGP Windows PowerShell 명령 참조](../../../../remote/remote-access/bgp/BGP-Windows-PowerShell-Command-Reference.md)  
  
    
## <a name="prerequisites-for-installing-ras-gateway-for-sdn"></a>SDN에 대 한 RAS 게이트웨이 설치를 위한 필수 구성 요소  
SDN에 사용 하기 위해 다중 테 넌 트 모드에서 RAS 게이트웨이를 배포 하려는 경우에는 Windows 인터페이스를 사용 하 여 원격 액세스를 설치할 수 없습니다. 대신 Windows PowerShell을 사용 해야 합니다.  
  
그러나 Windows PowerShell을 사용 하 여 RAS 게이트웨이를 설치 하려면 Windows PowerShell을 사용 하 여 **RemoteAccess** windows 기능을 추가 해야 합니다. 이렇게 하려면 Windows PowerShell 프롬프트에서 다음 명령을 실행 합니다.  
  
`Add-WindowsFeature -Name RemoteAccess -IncludeAllSubFeature -IncludeManagementTools`  
  
이 명령은 기능에 대 한 Windows PowerShell 명령 및 **원격 액세스** 기능을 추가 합니다.  
  
서버 **에 원격 액세스를 추가한 후** 다중 테 넌 트 모드와 BGP (Border Gateway Protocol)를 사용 하 여 원격 액세스를 RAS 게이트웨이로 설치할 수 있습니다.  
  
자세한 내용은 Windows PowerShell 참조 항목 [설치-원격 액세스](https://technet.microsoft.com/library/hh918408.aspx)를 참조 하세요.  
  
## <a name="ras-gateway-features"></a>RAS 게이트웨이 기능  
다음은 Windows Server 2016의 RAS 게이트웨이 기능입니다. 이러한 모든 기능을 한 번에 사용 하는 고가용성 풀에 RAS 게이트웨이를 배포할 수 있습니다.  
  
-   **사이트 간 VPN**. 이 RAS 게이트웨이 기능을 사용 하면 사이트 간 VPN 연결을 사용 하 여 인터넷을 통해 서로 다른 물리적 위치에 있는 두 네트워크를 연결할 수 있습니다. 데이터 센터에서 많은 테 넌 트를 호스팅하는 Csp의 경우, RAS 게이트웨이는 테 넌 트가 원격 사이트에서 사이트 간 VPN 연결을 통해 리소스를 액세스 및 관리할 수 있도록 하 고 네트워크 트래픽 흐름을 허용 하는 다중 테 넌 트 게이트웨이 솔루션을 제공 합니다. 데이터 센터의 가상 리소스와 실제 네트워크  
  
-   **지점 및 사이트 간 VPN**. 이 RAS 게이트웨이 기능을 통해 조직 직원 또는 관리자는 원격 위치에서 조직의 네트워크에 연결할 수 있습니다.  다중 테 넌 트 배포의 경우, 테 넌 트 네트워크 관리자는 지점 및 사이트 간 VPN 연결을 사용 하 여 CSP 데이터 센터의 가상 네트워크 리소스에 액세스할 수 있습니다.  
  
-   **GRE 터널링**. GRE (Generic Routing 캡슐화) 기반 터널을 사용 하면 테 넌 트 가상 네트워크와 외부 네트워크 간의 연결을 설정할 수 있습니다. GRE 프로토콜은 간단하고 대부분의 네트워크 장치에서 GRE가 지원되므로 데이터 암호화가 필요하지 않은 터널링에 이상적입니다. S2S (Site to Site) 터널의 GRE 지원은이 항목의 뒷부분에 설명 된 대로 다중 테 넌 트 게이트웨이를 사용 하는 테 넌 트 가상 네트워크와 테 넌 트 외부 네트워크 간의 전달 문제를 해결 합니다.  
  
-   **BGP (Border Gateway Protocol)를 사용 하는 동적 라우팅** BGP는 동적 라우팅 프로토콜이기 때문에 라우터에서 수동으로 경로를 구성할 필요성이 줄어들고 사이트 간 VPN 연결을 사용하여 연결된 사이트 간 경로를 자동으로 알아냅니다. 조직에 RAS 게이트웨이와 같은 BGP 사용 라우터를 사용 하 여 연결 된 여러 사이트가 있는 경우 BGP를 사용 하면 네트워크 중단 또는 실패가 발생할 경우 라우터가 자동으로 유효한 경로를 계산 하 고 사용할 수 있습니다. 자세한 내용은 [RFC 4271](https://tools.ietf.org/html/rfc4271)을 참조 하세요.  
  

  


