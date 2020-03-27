---
title: 네트워크 컨트롤러
description: 이 항목에서는 Windows Server 2016의 네트워크 컨트롤러에 대 한 개요를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 31f3fa4e-cd25-4bf3-89e9-a01a6cec7893
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ad13e41e756f0185a748fe9e17df64c71a8754bc
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317076"
---
# <a name="network-controller"></a>네트워크 컨트롤러

>적용 대상: Windows Server(반기 채널), Windows Server 2016

새로운 네트워크 컨트롤러에서 Windows Server 2016 관리, 구성, 모니터링 및 데이터 센터의 가상 및 실제 네트워크 인프라의 문제를 해결 하는 자동화의 프로그래밍 가능한 중앙된 위치를 제공 합니다. 

네트워크 컨트롤러를 사용하여 네트워크 장치 및 서비스를 수동으로 구성하는 대신 네트워크 인프라의 구성을 자동화할 수 있습니다.

> [!NOTE]
> 이 항목 외에 다음과 같은 네트워크 컨트롤러 설명서를 사용할 수 있습니다.
> - [네트워크 컨트롤러 고가용성](network-controller-high-availability.md)
> - [네트워크 컨트롤러 배포를 위한 설치 및 준비 요구 사항](../../plan/Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md)  
> - [Windows PowerShell을 사용하여 네트워크 컨트롤러 배포](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)  
> - [서버 관리자를 사용하여 네트워크 컨트롤러 서버 역할 설치](Install-the-Network-Controller-server-role-using-Server-Manager.md)
> - [네트워크 컨트롤러에 대 한 배포 후 단계](post-deploy-steps-nc.md)
> - [네트워크 컨트롤러 Cmdlet](https://technet.microsoft.com/library/mt576401.aspx) 

## <a name="network-controller-overview"></a><a name="bkmk_overview"></a>네트워크 컨트롤러 개요

네트워크 컨트롤러는 항상 사용 가능 하 고 확장 가능한 서버 역할이 며, 네트워크 컨트롤러에서 네트워크와 통신할 수 있도록 하는 API\)와 네트워크 컨트롤러와 통신할 수 있도록 하는 두 번째 API \(하나의 응용 프로그램 프로그래밍 인터페이스를 제공 합니다.

도메인 및 비도메인 환경 모두에서 네트워크 컨트롤러를 배포할 수 있습니다. 도메인 환경에서 네트워크 컨트롤러 및 네트워크 디바이스에 사용자가 사용 하 여 인증 Kerberos; 도메인이 아닌 환경에서 인증에 인증서를 배포 해야 합니다.

>[!IMPORTANT]
>실제 호스트에 네트워크 컨트롤러 서버 역할을 배포 하지 마십시오. 네트워크 컨트롤러를 배포 하려면 hyper-v 호스트에 설치 된 VM\) \(Hyper-v 가상 컴퓨터에 네트워크 컨트롤러 서버 역할을 설치 해야 합니다. 3 개의 서로 다른\-Hyper-v 호스트에 Vm에 네트워크 컨트롤러를 설치한 후 Windows PowerShell 명령 **NetworkControllerServer**를 사용 하 여 네트워크 컨트롤러에 호스트를 추가 하 여 소프트웨어 정의 네트워킹 \(SDN\)에 대 한 하이퍼\-V 호스트를 사용 하도록 설정 해야 합니다. 이렇게 하면 SDN 소프트웨어 Load Balancer 기능을 사용할 수 있습니다. 자세한 내용은 [NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver)를 참조 하세요.

네트워크 컨트롤러는 Southbound API를 사용하여 네트워크 디바이스, 서비스 및 구성 요소와 통신합니다. Southbound API를 사용하여 네트워크 컨트롤러는 네트워크 디바이스를 검색하고, 서비스 구성을 검색하고, 네트워크에 대해 필요한 모든 정보를 수집할 수 있습니다. 또한 Southbound API는 네트워크 컨트롤러가 구성 변경 사항 등의 정보를 네트워크 인프라에 전송할 수 있는 경로도 제공합니다.

네트워크 컨트롤러 Northbound API는 네트워크 컨트롤러에서 네트워크 정보를 수집하여 이 정보를 사용하여 네트워크를 모니터링하고 구성할 수 있는 기능을 제공합니다.

네트워크 컨트롤러 Northbound API를 사용 하면 Windows PowerShell, Representational State Transfer \(REST\) API를 사용 하 여 네트워크에서 새 장치를 구성, 모니터링, 문제 해결 및 배포할 수 있으며, System Center Virtual Machine Manager 등의 그래픽 사용자 인터페이스를 사용 하 여 관리 응용 프로그램을 배포할 수 있습니다.

>[!NOTE]
>네트워크 컨트롤러 Northbound API는 REST 인터페이스로 구현됩니다.

네트워크 컨트롤러에서 제어 하는 네트워크 인프라를 구성, 모니터링, 프로그래밍 및 문제를 해결할 수 있기 때문에 System Center Virtual Machine Manager \(SCVMM\)및 System Center Operations Manager \(SCOM\)와 같은 관리 응용 프로그램을 사용 하 여 네트워크 컨트롤러에서 데이터 센터 네트워크를 관리할 수 있습니다.

Windows PowerShell, REST API 또는 관리 애플리케이션을 사용하여 네트워크 컨트롤러에서 다음과 같은 물리 및 가상 네트워크 인프라를 관리할 수 있습니다.

- Hyper-V VM 및 가상 스위치

- 데이터 센터 방화벽

- 원격 액세스 서비스 \(RAS\) 다중 테 넌 트 게이트웨이, 가상 게이트웨이 및 게이트웨이 풀

- 소프트웨어 부하 분산 장치

다음은 관리자가 네트워크 컨트롤러를 직접 조작하는 관리 도구를 사용하는 그림입니다. 네트워크 컨트롤러는 가상 및 실제 인프라의 관리 도구를 포함 하 여 네트워크 인프라에 대 한 정보를 제공 하 고 관리자의 작업 도구를 사용 하는 경우에 따라 구성 변경을 수행 합니다.  

![네트워크 컨트롤러 개요](../../../media/Network-Controller/NetController_overview.png)  

테스트 랩 환경에서 네트워크 컨트롤러를 배포 하는 경우 hyper-v 호스트에 설치 된 VM\) \(Hyper-v 가상 머신에서 네트워크 컨트롤러 서버 역할을 실행할 수 있습니다.

대규모 데이터 센터에서 고가용성을 위해 세 개 이상의 Hyper-v 호스트에 설치 된 세 개의 Vm을 사용 하 여 클러스터를 배포할 수 있습니다. 자세한 내용은 [네트워크 컨트롤러 고가용성](network-controller-high-availability.md)을 참조 하세요.

## <a name="network-controller-features"></a><a name="bkmk_features"></a>네트워크 컨트롤러 기능

다음과 같은 네트워크 컨트롤러 기능을 사용하여 가상 및 실제 네트워크 디바이스와 서비스를 구성하고 관리할 수 있습니다.  
  
-   [방화벽 관리](#bkmk_firewall)  
  
-   [소프트웨어 Load Balancer 관리](#bkmk_slb)  
  
-   [Virtual Network 관리](#bkmk_virtual)  
  
-   [RAS 게이트웨이 관리](#bkmk_gateway)

>[!IMPORTANT]
>네트워크 컨트롤러 백업 및 복원 Windows Server 2016에서 현재 사용할 수 없는 경우
  
### <a name="firewall-management"></a><a name="bkmk_firewall"></a>방화벽 관리

이 네트워크 컨트롤러 기능을 사용하면 데이터 센터에서 동/서 및 남/북 네트워크 트래픽에 대해 워크로드 VM의 허용/거부 방화벽 Access Control 규칙을 구성하고 관리할 수 있습니다. 방화벽 규칙은 작업 부하 VM의 vSwitch 포트에 배관되므로 데이터 센터에서 작업 부하 전체적으로 분포됩니다. Northbound API를 사용하여 작업 부하 VM의 들어오는 트래픽과 나가는 트래픽 모두에 대해 방화벽 규칙을 정의할 수 있습니다. 또한 규칙에 의해 허용 또는 거부된 트래픽을 기록하도록 각 방화벽 규칙을 구성할 수 있습니다.  

자세한 내용은 참조 [데이터 센터 방화벽 개요](../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)합니다.

### <a name="software-load-balancer-management"></a><a name="bkmk_slb"></a>소프트웨어 Load Balancer 관리

이 네트워크 컨트롤러 기능을 사용하면 여러 서버에서 동일 작업 부하를 호스트하여 고가용성과 확장성을 제공하도록 만들 수 있습니다.  
  
자세한 내용은 참조 [소프트웨어 부하 분산 및 #40; SLB & #41; SDN에 대 한](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)합니다.  
  
### <a name="virtual-network-management"></a><a name="bkmk_virtual"></a>Virtual Network 관리

이 네트워크 컨트롤러 기능을 사용하면 개별 VM에서 Hyper-V 가상 스위치 및 가상 네트워크 어댑터를 포함하여 Hyper-V 네트워크 가상화를 배포 및 구성하며 가상 네트워크 정책을 저장 및 배포할 수 있습니다.

네트워크 컨트롤러는 NVGRE(네트워크 가상화 Generic Routing Encapsulation) 및 VXLAN(Virtual eXtensible Local Area Network)을 지원합니다.

### <a name="ras-gateway-management"></a><a name="bkmk_gateway"></a>RAS 게이트웨이 관리

이 네트워크 컨트롤러 기능을 사용 하면 RAS 게이트웨이 풀의 구성원 인 Vm (가상 컴퓨터)을 배포, 구성 및 관리 하 여 테 넌 트에 게이트웨이 서비스를 제공할 수 있습니다. 네트워크 컨트롤러를 사용 하면 자동으로 다음 게이트웨이 기능을 통해 RAS 게이트웨이 실행 하는 Vm을 배포할 수 있습니다.

> [!NOTE]
> System Center Virtual Machine Manager에서 RAS 게이트웨이 Windows Server 게이트웨이 이름은입니다.

- 클러스터에서 게이트웨이 VM을 추가 및 제거하고 필요한 백업 수준을 지정합니다.

- IPsec을 사용하여 원격 테넌트 네트워크와 데이터 센터 사이에 사이트 간 VPN(가상 사설망) 게이트웨이 연결을 설정합니다.

- GRE(Generic Routing Encapsulation)를 사용하여 원격 테넌트 네트워크와 데이터 센터 사이에 사이트 간 VPN 게이트웨이 연결을 설정합니다.

- 계층 3 전달 기능

- 프로토콜 BGP (Border Gateway) 라우팅, 테 넌 트의 VM 네트워크와 해당 원격 사이트 간의 네트워크 트래픽 라우팅을 관리할 수 있습니다.

네트워크 컨트롤러는 테 넌 트의 서로 다른 연결을 별도의 게이트웨이에 놓을 수 있습니다. 모든 게이트웨이 연결에 단일 공용 IP를 사용 하거나, 연결의 하위 집합에 대 한 공용 IP가 서로 다를 수 있습니다. 네트워크 컨트롤러는 감사 및 문제 해결을 위해 사용할 수 있는 모든 게이트웨이 구성 및 상태 변경 내용을 기록 합니다.

BGP에 대 한 자세한 내용은 참조 하십시오. [경계 게이트웨이 프로토콜 & #40; BGP (& a) #41;](../../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)합니다.

RAS 게이트웨이에 대 한 자세한 내용은 참조 하십시오. [SDN RAS 게이트웨이](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)합니다.

## <a name="network-controller-deployment-options"></a>네트워크 컨트롤러 배포 옵션

VMM\)\(System Center Virtual Machine Manager을 사용 하 여 네트워크 컨트롤러를 배포 하려면 [vmm 패브릭에서 SDN 네트워크 컨트롤러 설정](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller)을 참조 하세요.

스크립트를 사용 하 여 네트워크 컨트롤러를 배포 하려면 [스크립트를 사용 하 여 소프트웨어 정의 네트워크 인프라 배포](../../deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)를 참조 하세요.

Windows PowerShell을 사용 하 여 네트워크 컨트롤러를 배포 하려면 [Windows powershell을 사용 하 여 네트워크 컨트롤러 배포](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md) 를 참조 하세요.
