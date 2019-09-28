---
title: 가상 네트워크에서 네트워크 가상 어플라이언스 사용
description: 이 항목에서는 테 넌 트 가상 네트워크에 네트워크 가상 어플라이언스를 배포 하는 방법에 대해 알아봅니다. 사용자 정의 라우팅 및 포트 미러링 기능을 수행 하는 네트워크에 네트워크 가상 어플라이언스를 추가할 수 있습니다.
manager: dougkim
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.prod: windows-server
ms.technology: networking-sdn
ms.assetid: 3c361575-1050-46f4-ac94-fa42102f83c1
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.openlocfilehash: 158183bab74e6e45c36c579f3259fc2095a939b5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406043"
---
# <a name="use-network-virtual-appliances-on-a-virtual-network"></a>가상 네트워크에서 네트워크 가상 어플라이언스 사용

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 테 넌 트 가상 네트워크에 네트워크 가상 어플라이언스를 배포 하는 방법에 대해 알아봅니다. 사용자 정의 라우팅 및 포트 미러링 기능을 수행 하는 네트워크에 네트워크 가상 어플라이언스를 추가할 수 있습니다.

## <a name="types-of-network-virtual-appliances"></a>네트워크 가상 어플라이언스 유형

다음 두 가지 유형의 가상 어플라이언스 중 하나를 사용할 수 있습니다.

1. **사용자 정의 라우팅** -가상 네트워크의 분산 라우터를 가상 어플라이언스의 라우팅 기능으로 바꿉니다.  사용자 정의 라우팅을 사용 하 여 가상 어플라이언스는 가상 네트워크의 가상 서브넷 간 라우터로 사용 됩니다.

2. **포트 미러링** -모니터링 되는 포트를 입력 하거나 종료 하는 모든 네트워크 트래픽은 복제 되 고 분석을 위해 가상 어플라이언스로 전송 됩니다. 


## <a name="deploying-a-network-virtual-appliance"></a>네트워크 가상 어플라이언스 배포

네트워크 가상 어플라이언스를 배포 하려면 먼저 어플라이언스를 포함 하는 VM을 만든 다음 VM을 적절 한 가상 네트워크 서브넷에 연결 해야 합니다. 자세한 내용은 [테 넌 트 VM 만들기 및 테 넌 트 Virtual Network 또는 VLAN에 연결](Create-a-Tenant-VM.md)을 참조 하세요.

일부 어플라이언스에는 여러 가상 네트워크 어댑터가 필요 합니다. 일반적으로 추가 어댑터는 트래픽을 처리 하는 동안 어플라이언스 관리 전용 네트워크 어댑터 하나를 처리 합니다.  어플라이언스에 네트워크 어댑터가 여러 개 필요한 경우 네트워크 컨트롤러에서 각 네트워크 인터페이스를 만들어야 합니다. 또한 서로 다른 가상 서브넷에 있는 각 추가 어댑터에 대 한 인터페이스 ID를 각 호스트에 할당 해야 합니다.

네트워크 가상 어플라이언스를 배포한 후 정의 된 라우팅, 포팅 미러링 또는 둘 다에 대해 어플라이언스를 사용할 수 있습니다. 


## <a name="example-user-defined-routing"></a>예: 사용자 정의 라우팅

대부분의 환경에서는 가상 네트워크의 분산 라우터가 이미 정의 된 시스템 경로만 필요 합니다. 그러나 다음과 같은 특정 사례에서 라우팅 테이블을 만들고 하나 이상의 경로를 추가 해야 할 수도 있습니다.

- 온-프레미스 네트워크를 통해 인터넷에 터널링을 강제 적용 합니다.
- 사용자 환경에서 가상 어플라이언스를 사용 합니다.

이러한 시나리오의 경우 라우팅 테이블을 만들고 테이블에 사용자 정의 경로를 추가 해야 합니다. 라우팅 테이블을 여러 개 포함할 수 있으며, 동일한 라우팅 테이블을 하나 이상의 서브넷에 연결할 수 있습니다. 각 서브넷을 단일 라우팅 테이블에 연결할 수 있습니다. 서브넷의 모든 Vm은 서브넷에 연결 된 라우팅 테이블을 사용 합니다.

서브넷은 라우팅 테이블이 서브넷에 연결 될 때까지 시스템 경로를 사용 합니다. 연결이 설정 된 후에는 사용자 정의 경로 및 시스템 경로 간의 LPM (가장 긴 접두사 일치)을 기반으로 라우팅이 수행 됩니다. 동일한 LPM 일치를 가진 경로가 둘 이상 있는 경우 사용자 정의 경로가 먼저 선택 됩니다 (시스템 경로 이전).
 
**여기서**

1. 모든 사용자 정의 경로를 포함 하는 경로 테이블 속성을 만듭니다.<p>시스템 경로는 위에 정의 된 규칙에 따라 계속 적용 됩니다.

   ```PowerShell
    $routetableproperties = new-object Microsoft.Windows.NetworkController.RouteTableProperties
   ```

2. 라우팅 테이블 속성에 경로를 추가 합니다.<p>12.0.0.0/8 서브넷으로 향하는 모든 경로는 192.168.1.10에서 가상 어플라이언스로 라우팅됩니다. 어플라이언스에는 네트워크 인터페이스에 할당 된 IP를 사용 하 여 가상 네트워크에 연결 된 가상 네트워크 어댑터가 있어야 합니다.

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
   >경로를 더 추가 하려면 정의 하려는 각 경로에 대해이 단계를 반복 합니다.

3. 네트워크 컨트롤러에 라우팅 테이블을 추가 합니다.

   ```PowerShell
    $routetable = New-NetworkControllerRouteTable -ConnectionUri $uri -ResourceId "Route1" -Properties $routetableproperties
   ```

4. 가상 서브넷에 라우팅 테이블을 적용 합니다.<p>가상 서브넷에 경로 테이블을 적용 하는 경우 Tenant1_Vnet1 네트워크의 첫 번째 가상 서브넷은 경로 테이블을 사용 합니다. 원하는 만큼 가상 네트워크의 서브넷에 경로 테이블을 할당할 수 있습니다.

   ```PowerShell
    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"
    $vnet.properties.subnets[0].properties.RouteTable = $routetable
    new-networkcontrollervirtualnetwork -connectionuri $uri -properties $vnet.properties -resourceId $vnet.resourceid
   ```

라우팅 테이블을 가상 네트워크에 적용 하는 즉시 트래픽이 가상 어플라이언스로 전달 됩니다. 사용자 환경에 적합 한 방식으로 트래픽을 전달 하도록 가상 어플라이언스에서 라우팅 테이블을 구성 해야 합니다.

## <a name="example-port-mirroring"></a>예: 포트 미러링

이 예제에서는 MyVM_Ethernet1에 대 한 트래픽을 미러 Appliance_Ethernet1 구성 합니다.  두 Vm을 어플라이언스로, 다른 vm은 미러링을 사용 하 여 모니터링 하는 VM으로 배포 했다고 가정 합니다. 

어플라이언스에는 관리를 위한 두 번째 네트워크 인터페이스가 있어야 합니다. Appliciance_Ethernet1에서 대상으로 미러링을 사용 하도록 설정한 후에는 더 이상 구성 된 IP 인터페이스로 향하는 트래픽을 수신 하지 않습니다.


**여기서**

1. Vm이 있는 가상 네트워크를 가져옵니다.

   ```PowerShell
   $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"
   ```

2. 미러링 원본 및 대상에 대 한 네트워크 컨트롤러 네트워크 인터페이스를 가져옵니다.

   ```PowerShell
   $dstNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "Appliance_Ethernet1"
   $srcNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```

3. 포트 미러링 규칙과 대상 인터페이스를 나타내는 요소를 포함 하는 serviceinsertionproperties 개체를 만듭니다.

   ```PowerShell
   $portmirror = [Microsoft.Windows.NetworkController.ServiceInsertionProperties]::new()
   $portMirror.Priority = 1
   ```

4. 트래픽을 어플라이언스로 전송 하기 위해 일치 해야 하는 규칙을 포함 하는 serviceinsertionrules 개체를 만듭니다.<p>아래에 정의 된 규칙은 기존의 미러를 나타내는 모든 트래픽과 인바운드 및 아웃 바운드를 일치 시킵니다.  특정 포트 또는 특정 원본/대상을 미러링 하려는 경우 이러한 규칙을 조정할 수 있습니다.

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

5. 미러된 어플라이언스의 네트워크 인터페이스를 포함 하는 serviceinsertionelements 개체를 만듭니다.

   ```PowerShell
   $portmirror.ServiceInsertionElements = [Microsoft.Windows.NetworkController.ServiceInsertionElement[]]::new(1)

   $portmirror.ServiceInsertionElements[0] = [Microsoft.Windows.NetworkController.ServiceInsertionElement]::new()
   $portmirror.ServiceInsertionElements[0].ResourceId = "Element1"
   $portmirror.ServiceInsertionElements[0].Properties = [Microsoft.Windows.NetworkController.ServiceInsertionElementProperties]::new()

   $portmirror.ServiceInsertionElements[0].Properties.Description = "Port Mirror Element"
   $portmirror.ServiceInsertionElements[0].Properties.NetworkInterface = $dstNic
   $portmirror.ServiceInsertionElements[0].Properties.Order = 1
   ```

6. 네트워크 컨트롤러에 서비스 삽입 개체를 추가 합니다.<p>이 명령을 실행 하면 이전 단계에서 지정한 어플라이언스 네트워크 인터페이스에 대 한 모든 트래픽이 중지 됩니다.

   ```PowerShell
   $portMirror = New-NetworkControllerServiceInsertion -ConnectionUri $uri -Properties $portmirror -ResourceId "MirrorAll"
   ```

7. 미러링할 원본의 네트워크 인터페이스를 업데이트 합니다.

   ```PowerShell
   $srcNic.Properties.IpConfigurations[0].Properties.ServiceInsertion = $portMirror
   $srcNic = New-NetworkControllerNetworkInterface -ConnectionUri $uri  -Properties $srcNic.Properties -ResourceId $srcNic.ResourceId
   ```

이러한 단계를 완료 한 후에는 Appliance_Ethernet1 인터페이스가 MyVM_Ethernet1 인터페이스에서 트래픽을 미러링합니다.
 
---