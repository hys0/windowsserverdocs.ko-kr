---
title: 가상 네트워크에서 게스트 클러스터링
description: 가상 네트워크에 연결 된 가상 컴퓨터는 네트워크에서 통신 하기 위해 네트워크 컨트롤러가 할당 한 IP 주소만 사용할 수 있습니다.  Microsoft 장애 조치 (Failover) 클러스터링과 같이 부동 IP 주소를 필요로 하는 클러스터링 기술을 제대로 작동 하려면 몇 가지 추가 단계가 필요 합니다.
manager: dougkim
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e9e5c81-aa61-479e-abaf-64c5e95f90dc
ms.author: grcusanz
author: shortpatti
ms.date: 08/26/2018
ms.openlocfilehash: 05704beeae27bd9de9ad0c5cf578581c650a976f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406033"
---
# <a name="guest-clustering-in-a-virtual-network"></a>가상 네트워크에서 게스트 클러스터링

>적용 대상: Windows Server(반기 채널), Windows Server 2016

가상 네트워크에 연결 된 가상 컴퓨터는 네트워크에서 통신 하기 위해 네트워크 컨트롤러가 할당 한 IP 주소만 사용할 수 있습니다.  Microsoft 장애 조치 (Failover) 클러스터링과 같이 부동 IP 주소를 필요로 하는 클러스터링 기술을 제대로 작동 하려면 몇 가지 추가 단계가 필요 합니다.

부동 IP에 연결할 수 있도록 하는 방법은 소프트웨어 Load Balancer \(SLB @ no__t-1 가상 IP \(VIP @ no__t-3을 사용 하는 것입니다.  SLB가 현재 해당 IP를 보유 하 고 있는 컴퓨터로 트래픽을 전송 하도록 해당 IP의 포트에 대 한 상태 프로브를 사용 하 여 소프트웨어 부하 분산 장치를 구성 해야 합니다.


## <a name="example-load-balancer-configuration"></a>예: 부하 분산 장치 구성

이 예에서는 클러스터 노드가 되 고 Virtual Network에 연결 된 Vm을 이미 만든 것으로 가정 합니다.  지침은 [VM 만들기 및 테 넌 트 Virtual Network 또는 VLAN에 연결](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create-a-tenant-vm)을 참조 하세요.  

이 예제에서는 클러스터의 부동 IP 주소를 나타내는 가상 IP 주소 (192.168.2.100)를 만들고 TCP 포트 59999을 모니터링 하는 상태 프로브를 구성 하 여 활성 노드를 확인 합니다.

1. VIP를 선택 합니다.<p>VIP IP 주소를 할당 하 여 준비 합니다 .이 주소는 클러스터 노드와 동일한 서브넷에 있는 사용 되지 않는 주소 또는 예약 된 주소일 수 있습니다.  VIP는 클러스터의 부동 주소와 일치 해야 합니다.

   ```PowerShell
   $VIP = "192.168.2.100"
   $subnet = "Subnet2"
   $VirtualNetwork = "MyNetwork"
   $ResourceId = "MyNetwork_InternalVIP"
   ```

2. 부하 분산 장치 속성 개체를 만듭니다.

   ```PowerShell
   $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties
   ```

3. 프런트 @ no__t-0 끝 IP 주소를 만듭니다.

   ```PowerShell
   $LoadBalancerProperties.frontendipconfigurations += $FrontEnd = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfiguration
   $FrontEnd.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfigurationProperties
   $FrontEnd.resourceId = "Frontend1"
   $FrontEnd.resourceRef = "/loadBalancers/$ResourceId/frontendIPConfigurations/$($FrontEnd.resourceId)"
   $FrontEnd.properties.subnet = new-object Microsoft.Windows.NetworkController.Subnet
   $FrontEnd.properties.subnet.ResourceRef = "/VirtualNetworks/MyNetwork/Subnets/Subnet2"
   $FrontEnd.properties.privateIPAddress = $VIP
   $FrontEnd.properties.privateIPAllocationMethod = "Static"
   ```

4. 클러스터 노드를 포함 하는 back @ no__t-0end 풀을 만듭니다.

   ```PowerShell
   $BackEnd = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
   $BackEnd.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties
   $BackEnd.resourceId = "Backend1"
   $BackEnd.resourceRef = "/loadBalancers/$ResourceId/backendAddressPools/$($BackEnd.resourceId)"
   $LoadBalancerProperties.backendAddressPools += $BackEnd
   ```

5. 프로브를 추가 하 여 부동 주소가 현재 활성 상태인 클러스터 노드를 검색 합니다. 

   >[!NOTE]
   >아래 정의 된 포트에서 VM의 영구 주소에 대 한 프로브 쿼리입니다.  활성 노드에서만 포트가 응답 해야 합니다. 

   ```PowerShell
   $LoadBalancerProperties.probes += $lbprobe = new-object Microsoft.Windows.NetworkController.LoadBalancerProbe
   $lbprobe.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerProbeProperties

   $lbprobe.ResourceId = "Probe1"
   $lbprobe.resourceRef = "/loadBalancers/$ResourceId/Probes/$($lbprobe.resourceId)"
   $lbprobe.properties.protocol = "TCP"
   $lbprobe.properties.port = "59999"
   $lbprobe.properties.IntervalInSeconds = 5
   $lbprobe.properties.NumberOfProbes = 11
   ```

6. TCP 포트 1433에 대 한 부하 분산 규칙을 추가 합니다.<p>필요에 따라 프로토콜 및 포트를 수정할 수 있습니다.  이 VIP에서 추가 포트 및 protcols에 대해이 단계를 여러 번 반복할 수도 있습니다.  대해 enablefloatingip을 $true로 설정 하는 것이 중요 합니다 .이는 부하 분산 장치에서 원래 VIP가 있는 노드로 패킷을 보내도록 지시 하는 것입니다.

   ```PowerShell
   $LoadBalancerProperties.loadbalancingRules += $lbrule = new-object Microsoft.Windows.NetworkController.LoadBalancingRule
   $lbrule.properties = new-object Microsoft.Windows.NetworkController.LoadBalancingRuleProperties
   $lbrule.ResourceId = "Rules1"

   $lbrule.properties.frontendipconfigurations += $FrontEnd
   $lbrule.properties.backendaddresspool = $BackEnd 
   $lbrule.properties.protocol = "TCP"
   $lbrule.properties.frontendPort = $lbrule.properties.backendPort = 1433 
   $lbrule.properties.IdleTimeoutInMinutes = 4
   $lbrule.properties.EnableFloatingIP = $true
   $lbrule.properties.Probe = $lbprobe
   ```

7. 네트워크 컨트롤러에서 부하 분산 장치를 만듭니다.

   ```PowerShell
   $lb = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $ResourceId -Properties $LoadBalancerProperties -Force
   ```

8. 백 엔드 풀에 클러스터 노드를 추가 합니다.<p>클러스터에 필요한 만큼 노드를 풀에 추가할 수 있습니다.

   ```PowerShell
   # Cluster Node 1

   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid "ClusterNode1_Network-Adapter"
   $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
   $nic = new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid $nic.resourceid -properties $nic.properties -force

    # Cluster Node 2

   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid "ClusterNode2_Network-Adapter"
   $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
   $nic = new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid $nic.resourceid -properties $nic.properties -force
   ```

   부하 분산 장치를 만들고 네트워크 인터페이스를 백 엔드 풀에 추가한 후에는 클러스터를 구성할 준비가 된 것입니다.  

9. 필드 Microsoft 장애 조치 (Failover) 클러스터를 사용 하는 경우 다음 예제를 계속 합니다. 

## <a name="example-2-configuring-a-microsoft-failover-cluster"></a>예 2: Microsoft 장애 조치 (failover) 클러스터 구성

다음 단계를 사용 하 여 장애 조치 (failover) 클러스터를 구성할 수 있습니다.

1. 장애 조치 (failover) 클러스터의 속성을 설치 하 고 구성 합니다.

   ```PowerShell
   add-windowsfeature failover-clustering -IncludeManagementTools
   Import-module failoverclusters

   $ClusterName = "MyCluster"
   
   $ClusterNetworkName = "Cluster Network 1"
   $IPResourceName =  
   $ILBIP = “192.168.2.100” 

   $nodes = @("DB1", "DB2")
   ```

2. 한 노드에서 클러스터를 만듭니다.

   ```PowerShell
   New-Cluster -Name $ClusterName -NoStorage -Node $nodes[0]
   ```

3. 클러스터 리소스를 중지 합니다.

   ```PowerShell
   Stop-ClusterResource "Cluster Name" 
   ```

4. 클러스터 IP 및 프로브 포트를 설정 합니다.<p>IP 주소는 이전 예제에서 사용 된 프런트 엔드 ip 주소와 일치 해야 하며, 프로브 포트는 이전 예제에서 프로브 포트와 일치 해야 합니다.

   ```PowerShell
   Get-ClusterResource "Cluster IP Address" | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

5. 클러스터 리소스를 시작 합니다.

   ```PowerShell
    Start-ClusterResource "Cluster IP Address"  -Wait 60 
    Start-ClusterResource "Cluster Name"  -Wait 60 
   ```

6. 나머지 노드를 추가 합니다.

   ```PowerShell
   Add-ClusterNode $nodes[1]
   ```

_**클러스터가 활성 상태입니다.**_ 지정 된 포트의 VIP로 이동 하는 트래픽은 활성 노드에 전달 됩니다.

---