---
title: 가상 네트워크에서 네트워크 가상 어플라이언스 사용
description: 이 항목에서는 테 넌 트 가상 네트워크에서 네트워크 가상 어플라이언스를 배포 하는 방법을 알아봅니다. 사용자 정의 경로 및 포트 미러링 함수를 수행 하는 네트워크에 네트워크 가상 어플라이언스를 추가할 수 있습니다.
manager: dougkim
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.assetid: 3c361575-1050-46f4-ac94-fa42102f83c1
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.openlocfilehash: e715a782651a5b9867f3b45251fd6ea6e4a9e4f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847374"
---
# <a name="use-network-virtual-appliances-on-a-virtual-network"></a>가상 네트워크에서 네트워크 가상 어플라이언스 사용

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 테 넌 트 가상 네트워크에서 네트워크 가상 어플라이언스를 배포 하는 방법을 알아봅니다. 사용자 정의 경로 및 포트 미러링 함수를 수행 하는 네트워크에 네트워크 가상 어플라이언스를 추가할 수 있습니다.

## <a name="types-of-network-virtual-appliances"></a>네트워크 가상 어플라이언스의 형식

가상 어플라이언스의 두 형식 중 하나를 사용할 수 있습니다.

1. **사용자 정의 라우팅** -가상 어플라이언스의 라우팅 기능을 사용 하 여 가상 네트워크에 분산된 라우터를 대체 합니다.  사용자 정의 라우팅을 사용 하 여 가상 어플라이언스는 가상 네트워크에 가상 서브넷 간의 라우터로 사용 됩니다.

2. **포트 미러링** -모든 네트워크 트래픽 들어오는 경우 또는 중복 되어 분석에 대 한 가상 어플라이언스로 전송 모니터링 되는 포트를 종료 합니다. 


## <a name="deploying-a-network-virtual-appliance"></a>네트워크 가상 어플라이언스를 배포합니다.

네트워크 가상 어플라이언스를 배포 하려면 먼저 어플라이언스를 포함 하는 VM을 만들어야 하며 다음 적절 한 가상 네트워크 서브넷에 VM을 연결 합니다. 자세한 내용은 참조 하세요. [테 넌 트 VM 및 테 넌 트 가상 네트워크 또는 VLAN에 연결 만들기](Create-a-Tenant-VM.md)합니다.

일부 어플라이언스에는 여러 가상 네트워크 어댑터가 필요합니다. 일반적으로 전용인 하나의 네트워크 어댑터 장치 관리에 어댑터 추가 트래픽을 처리 하는 동안.  어플라이언스에서 여러 네트워크 어댑터에 필요한 경우 네트워크 컨트롤러에서 각 네트워크 인터페이스를 만들어야 합니다. 또한 각 추가 어댑터는 여러 가상 서브넷에 있는 각 호스트에서 인터페이스 ID를 할당 해야 합니다.

네트워크 가상 어플라이언스를 배포한 후에 정의 된 라우팅, 이식 미러링 또는 둘 다에 대 한 어플라이언스를 사용할 수 있습니다. 


## <a name="example-user-defined-routing"></a>예: 사용자 정의 라우팅

대부분의 환경에서 가상 네트워크의 분산된 라우터를 이미 정의한 시스템 경로 필요 합니다. 그러나 라우팅 테이블을 만들고와 같은 특정 경우에 하나 이상의 경로 추가 해야 합니다.

- 온-프레미스 네트워크를 통해 인터넷에 터널링을 강제 합니다.
- 사용자 환경에서 가상 어플라이언스 사용 합니다.

이러한 시나리오에 대 한 라우팅 테이블을 만들고 테이블에 사용자 정의 경로 추가 합니다. 여러 라우팅 테이블에 있고 동일한 라우팅 테이블을 하나 이상의 서브넷에 연결할 수 있습니다. 단일 라우팅 테이블에 각 서브넷에만 연결할 수 있습니다. 서브넷의 모든 Vm 서브넷에 연결 된 라우팅 테이블을 사용 합니다.

라우팅 테이블을 가져옵니다 서브넷에 연결 될 때까지 서브넷은 시스템 경로에 의존 합니다. 연결이 후 라우팅은 LPM을 기반으로 가장 긴 접두사 일치 () 사용자 정의 경로 및 시스템 경로 간에 수행 됩니다. LPM 일치가 동일한 경로가 둘 이상인 경우 다음 사용자 정의 경로 먼저 하기 전에 선택한 시스템 경로입니다.
 
**절차:**

1. 만들 경로 테이블 속성을 포함 하는 모든 사용자 정의 경로.<p>시스템 경로 여전히 위에 정의 된 규칙에 따라 적용 됩니다.

   ```PowerShell
    $routetableproperties = new-object Microsoft.Windows.NetworkController.RouteTableProperties
   ```

2. 라우팅 테이블 속성에 경로 추가 합니다.<p>12.0.0.0/8 서브넷으로 보내는 모든 경로 192.168.1.10에서 가상 어플라이언스로 라우팅됩니다. 어플라이언스는 네트워크 인터페이스에 할당 된 해당 IP를 사용 하 여 가상 네트워크에 연결 하는 가상 네트워크 어댑터가 있어야 합니다.

   ```PowerShell
    $route = new-object Microsoft.Windows.NetworkController.Route
    $route.ResourceID = "0_0_0_0_0"
    $route.properties = new-object Microsoft.Windows.NetworkController.RouteProperties
    $route.properties.AddressPrefix = "0.0.0.0/0"
    $route.properties.nextHopType = "VirtualAppliance"
    $route.properties.nextHopIpAddress = "192.168.1.10"
    $routetableproperties.routes += $route
   ```
   >[!TIP]
   >정의 하려는 각 경로 대 한 자세한 경로 추가 하려는 경우이 단계를 반복 합니다.

3. 네트워크 컨트롤러에 라우팅 테이블을 추가 합니다.

   ```PowerShell
    $routetable = New-NetworkControllerRouteTable -ConnectionUri $uri -ResourceId "Route1" -Properties $routetableproperties
   ```

4. 가상 서브넷에 라우팅 테이블을 적용 합니다.<p>가상 서브넷에 경로 테이블을 적용 하면 Tenant1_Vnet1 네트워크의 첫 번째 가상 서브넷 경로 테이블을 사용 합니다. 원하는 수 만큼의 가상 네트워크 서브넷에 경로 테이블을 할당할 수 있습니다.

   ```PowerShell
    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"
    $vnet.properties.subnets[0].properties.RouteTable = $routetable
    new-networkcontrollervirtualnetwork -connectionuri $uri -properties $vnet.properties -resourceId $vnet.resourceid
   ```

가상 네트워크에 라우팅 테이블을 적용 하는 즉시 가상 어플라이언스로 트래픽을 전달 가져옵니다. 사용자 환경에 적합 한 방식으로 트래픽을 전달 하도록 가상 어플라이언스의 라우팅 테이블을 구성 해야 합니다.

## <a name="example-port-mirroring"></a>예: 포트 미러링

이 예제에서는 미러 서버로 Appliance_Ethernet1 MyVM_Ethernet1에 대 한 트래픽을 구성합니다.  어플라이언스 및 미러링을 모니터링 하려면 VM과 다른 하나는 두 개의 Vm을 배포한 가정 합니다. 

어플라이언스 관리에 대 한 두 번째 네트워크 인터페이스에 있어야 합니다. 미러링을 Appliciance_Ethernet1에서 대상으로 사용 하도록 설정 하면 더 이상 구성 되어 IP 인터페이스에 대 한 트래픽은 받습니다.


**절차:**

1. Vm이 있는 가상 네트워크를 가져옵니다.

   ```PowerShell
   $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"
   ```

2. 미러링 하는 원본 및 대상에 대 한 네트워크 컨트롤러 네트워크 인터페이스를 가져옵니다.

   ```PowerShell
   $dstNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "Appliance_Ethernet1"
   $srcNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```

3. 포트 미러링 대상 인터페이스를 나타내는 요소와 규칙을 포함 하도록 serviceinsertionproperties 개체를 만듭니다.

   ```PowerShell
   $portmirror = [Microsoft.Windows.NetworkController.ServiceInsertionProperties]::new()
   $portMirror.Priority = 1
   ```

4. 어플라이언스로 전송 될 트래픽에 대해 순서 대로 일치 되어야 하는 규칙을 포함 하도록 serviceinsertionrules 개체를 만듭니다.<p>규칙 아래에 정의 된 일치 모든 트래픽 인바운드 및 아웃 바운드 기존 미러에 나타냅니다.  특정 원본/대상 또는 특정 포트 미러링에 관심이 있는 경우 이러한 규칙을 조정할 수 있습니다.

   ```PowerShell
   $portmirror.ServiceInsertionRules = [Microsoft.Windows.NetworkController.ServiceInsertionRule[]]::new(1)

   $portmirror.ServiceInsertionRules[0] = [Microsoft.Windows.NetworkController.ServiceInsertionRule]::new()
   $portmirror.ServiceInsertionRules[0].ResourceId = "Rule1"
   $portmirror.ServiceInsertionRules[0].Properties = [Microsoft.Windows.NetworkController.ServiceInsertionRuleProperties]::new()

   $portmirror.ServiceInsertionRules[0].Properties.Description = "Port Mirror Rule"
   $portmirror.ServiceInsertionRules[0].Properties.Protocol = "All"
   $portmirror.ServiceInsertionRules[0].Properties.SourcePortRangeStart = "0"
   $portmirror.ServiceInsertionRules[0].Properties.SourcePortRangeEnd = "65535"
   $portmirror.ServiceInsertionRules[0].Properties.DestinationPortRangeStart = "0"
   $portmirror.ServiceInsertionRules[0].Properties.DestinationPortRangeEnd = "65535"
   $portmirror.ServiceInsertionRules[0].Properties.SourceSubnets = "*"
   $portmirror.ServiceInsertionRules[0].Properties.DestinationSubnets = "*"
   ```

5. 미러된 어플라이언스의 네트워크 인터페이스를 포함 하도록 serviceinsertionelements 개체를 만듭니다.

   ```PowerShell
   $portmirror.ServiceInsertionElements = [Microsoft.Windows.NetworkController.ServiceInsertionElement[]]::new(1)

   $portmirror.ServiceInsertionElements[0] = [Microsoft.Windows.NetworkController.ServiceInsertionElement]::new()
   $portmirror.ServiceInsertionElements[0].ResourceId = "Element1"
   $portmirror.ServiceInsertionElements[0].Properties = [Microsoft.Windows.NetworkController.ServiceInsertionElementProperties]::new()

   $portmirror.ServiceInsertionElements[0].Properties.Description = "Port Mirror Element"
   $portmirror.ServiceInsertionElements[0].Properties.NetworkInterface = $dstNic
   $portmirror.ServiceInsertionElements[0].Properties.Order = 1
   ```

6. 네트워크 컨트롤러에서 서비스 삽입 개체를 추가 합니다.<p>이 명령을 실행 하는 경우 모든 트래픽은 어플라이언스 네트워크 이전 단계 중지에 지정 된 인터페이스입니다.

   ```PowerShell
   $portMirror = New-NetworkControllerServiceInsertion -ConnectionUri $uri -Properties $portmirror -ResourceId "MirrorAll"
   ```

7. 미러링할 원본 네트워크 인터페이스를 업데이트 합니다.

   ```PowerShell
   $srcNic.Properties.IpConfigurations[0].Properties.ServiceInsertion = $portMirror
   $srcNic = New-NetworkControllerNetworkInterface -ConnectionUri $uri  -Properties $srcNic.Properties -ResourceId $srcNic.ResourceId
   ```

다음이 단계를 완료 한 후 Appliance_Ethernet1 인터페이스 MyVM_Ethernet1 인터페이스에서 트래픽의 미러링합니다.
 
---