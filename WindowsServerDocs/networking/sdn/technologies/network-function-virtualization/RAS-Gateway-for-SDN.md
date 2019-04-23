---
title: SDN용 RAS 게이트웨이
description: 다중 테 넌 트, Windows Server 2016에서 프로토콜 BGP (경계 게이트웨이) 가능 라우터는 소프트웨어 기반 인 RAS 게이트웨이 대해 자세히 알아보려면이 항목에서는 사용할 수 있습니다.
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
ms.openlocfilehash: 4f1ad0b3f0b5921a53faa8a45baae9f0b8711873
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856274"
---
# <a name="ras-gateway-for-sdn"></a>SDN용 RAS 게이트웨이

>적용 대상: Windows Server (반기 채널) SDN에 대 한 Windows Server 2016 # # RAS 게이트웨이  


RAS 게이트웨이 소프트웨어 기반 다중 테 넌 트를 프로토콜 BGP (경계 게이트웨이) 가능 라우터를 위한 클라우드 서비스 공급자 (Csp) 및 기업 해당 호스트에서 Hyper-v 네트워크 가상화를 사용 하 여 여러 테 넌 트 가상 네트워크. RAS 게이트웨이 위치에 관계 없이 실제 네트워크와 VM 네트워크 리소스 간에 네트워크 트래픽을 라우팅합니다. 동일한 실제 위치 또는 여러 다른 위치에서 네트워크 트래픽을 라우팅할 수 있습니다.   

다중 테 넌 트 지원은 여러 테 넌 트의 가상 머신 워크 로드 지원, 아직 동일한 인프라에서 실행 하는 모든 워크 로드를 서로 격리 하는 클라우드 인프라의 기능입니다. 개별 테넌트의 여러 작업을 상호 연결하고 원격으로 관리할 수는 있지만, 이러한 시스템이 다른 테넌트의 작업과 서로 연결되거나 다른 테넌트에서 이러한 시스템을 원격으로 관리하지는 않습니다.

  
> [!NOTE]  
> 이 항목 외에 다음 항목에서는 RAS 게이트웨이 사용할 수 있습니다.  
>   
> -   [RAS 게이트웨이의 새로운 기능](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md)  
> -   [RAS 게이트웨이 배포 아키텍처](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-Deployment-Architecture.md)  
> -   [RAS 게이트웨이 고가용성](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)  
> -   [경계 게이트웨이 프로토콜 &#40;BGP&#41;](../../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)  
> -   [BGP Windows PowerShell 명령 참조](../../../../remote/remote-access/bgp/BGP-Windows-PowerShell-Command-Reference.md)  
  
    
## <a name="prerequisites-for-installing-ras-gateway-for-sdn"></a>SDN 용 RAS 게이트웨이 설치 하기 위한 필수 구성 요소  
SDN 사용에 대 한 다중 테 넌 트 모드에서 RAS 게이트웨이 배포 하려는 경우 원격 액세스를 설치 하려면 Windows 인터페이스를 사용할 수 없습니다. 대신 Windows PowerShell을 사용 해야 합니다.  
  
하지만 Windows PowerShell을 사용 하 여 RAS 게이트웨이 설치할 수 있습니다, 전에 추가할 Windows PowerShell을 사용 해야 합니다 **RemoteAccess** Windows 기능입니다. 이렇게 하려면 Windows PowerShell 프롬프트에서 다음 명령을 실행 합니다.  
  
`Add-WindowsFeature -Name RemoteAccess -IncludeAllSubFeature -IncludeManagementTools`  
  
이 명령은 추가 합니다 **RemoteAccess** 기능 및 기능에 대 한 Windows PowerShell 명령입니다.  
  
추가한 후 **RemoteAccess** 서버에 RAS 게이트웨이 다중 테 넌 트 모드로 게이트웨이 프로토콜 BGP (경계)와 원격 액세스를 설치할 수 있습니다.  
  
자세한 내용은 Windows PowerShell 참조 항목을 참조 하세요 [Install-remoteaccess](https://technet.microsoft.com/library/hh918408.aspx)합니다.  
  
## <a name="ras-gateway-features"></a>RAS 게이트웨이 기능  
다음은 Windows Server 2016에서 RAS 게이트웨이 기능입니다. 이러한 모든 기능을 한 번에 사용 하는 고가용성 풀에서 RAS 게이트웨이 배포할 수 있습니다.  
  
-   **사이트 간 VPN**합니다. 이 RAS 게이트웨이 기능을 사용 하면 사이트 간 VPN 연결을 사용 하 여 인터넷을 통해 서로 다른 물리적 위치에 있는 두 네트워크를 연결할 수 있습니다. 데이터 센터에서 여러 테 넌 트를 호스팅하는 Csp에 대 한 RAS 게이트웨이 테 넌 트가 액세스 하 고 원격 사이트에서 사이트 간 VPN 연결을 통해 해당 리소스를 관리할 수 있도록 하 고 간의 네트워크 트래픽 흐름을 허용 하는 다중 테 넌 트 게이트웨이 솔루션 제공 데이터 센터와 물리적 네트워크의 가상 리소스입니다.  
  
-   **지점 대 사이트간 VPN**합니다. 이 RAS 게이트웨이 기능에는 조직의 직원이 또는 관리자가 원격 위치에서 조직의 네트워크에 연결할 수 있습니다.  다중 테 넌 트 배포에 대 한 테 넌 트 네트워크 관리자 지점-사이트 간 VPN 연결을 사용 하 여 CSP 데이터 센터에서 가상 네트워크 리소스에 액세스할 수 있습니다.  
  
-   **GRE 터널링**합니다. 캡슐화 GRE (generic Routing) 기반 테 넌 트 가상 네트워크와 외부 네트워크 간에 터널이 사용 연결 합니다. GRE 프로토콜은 간단하고 대부분의 네트워크 장치에서 GRE가 지원되므로 데이터 암호화가 필요하지 않은 터널링에 이상적입니다. 이 항목의 뒷부분에 설명 된 대로 사이트 간 (S2S) 터널의 GRE 지원은 테 넌 트 가상 네트워크 및 다중 테 넌 트 게이트웨이 사용 하 여 테 넌 트 외부 네트워크 간의 전달 문제를 해결 합니다.  
  
-   **동적 라우팅을 사용 하 여 프로토콜 BGP (경계 게이트웨이)** 합니다. BGP는 동적 라우팅 프로토콜이기 때문에 라우터에서 수동으로 경로를 구성할 필요성이 줄어들고 사이트 간 VPN 연결을 사용하여 연결된 사이트 간 경로를 자동으로 알아냅니다. 조직이 등 RAS 게이트웨이 BGP 사용 라우터를 사용 하 여 연결 된 여러 사이트를 BGP 라우터를 자동으로 계산 하 고 네트워크 중단 또는 오류가 발생할 경우 서로에 대 한 유효한 경로 사용 하 여 허용 합니다. 자세한 내용은 [RFC 4271](https://tools.ietf.org/html/rfc4271)합니다.  
  

  


