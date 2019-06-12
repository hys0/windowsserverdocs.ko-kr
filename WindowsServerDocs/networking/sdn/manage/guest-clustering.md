---
title: 가상 네트워크에서 게스트 클러스터링
description: '네트워크 컨트롤러 네트워크에서 통신 하기 위해 할당 된 IP 주소를 사용할 가상 네트워크에 연결 된 가상 컴퓨터 에서만 허용 됩니다.  Microsoft 장애 조치 클러스터링, 예: 부동 IP 주소를 요구 하는 클러스터링 기술에는 제대로 작동 하려면 몇 가지 추가 단계가 필요 합니다.'
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e9e5c81-aa61-479e-abaf-64c5e95f90dc
ms.author: grcusanz
author: shortpatti
ms.date: 08/26/2018
ms.openlocfilehash: 97c20fd07d06b609686daf4d6308a9f248873036
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446345"
---
# <a name="guest-clustering-in-a-virtual-network"></a>가상 네트워크에서 게스트 클러스터링

>적용 대상: Windows Server (반기 채널), Windows Server 2016

네트워크 컨트롤러 네트워크에서 통신 하기 위해 할당 된 IP 주소를 사용할 가상 네트워크에 연결 된 가상 컴퓨터 에서만 허용 됩니다.  Microsoft 장애 조치 클러스터링, 예: 부동 IP 주소를 요구 하는 클러스터링 기술에는 제대로 작동 하려면 몇 가지 추가 단계가 필요 합니다.

부동 IP를 연결할 수 하는 방법은 소프트웨어 부하 분산 장치를 사용 하는 것 \(SLB\) 가상 IP \(VIP\)합니다.  소프트웨어 부하 분산 장치는 현재 해당 IP를가지고 있는 컴퓨터에 SLB 트래픽을 있도록 해당 ip 포트로 상태 프로브를 사용 하 여 구성 되어야 합니다.


## <a name="example-load-balancer-configuration"></a>예: 부하 분산 장치 구성

클러스터 노드로 지정할 및 가상 네트워크에 연결 하는 Vm이 이미 만들었음을 전제로 합니다.  지침을 참조 하세요 [VM 및 테 넌 트 가상 네트워크 또는 VLAN에 연결 만들기](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create-a-tenant-vm)합니다.  

이 예제는 가상 IP 주소 (192.168.2.100)를 클러스터의 부동 IP 주소가 만들고 TCP 포트 59999 인지 활성 노드를 모니터링 하기 위한 상태 프로브를 구성 합니다.

1. VIP를 선택 합니다.<p>클러스터 노드와 동일한 서브넷의 모든 사용 되지 않은 또는 예약 된 주소 수 있는 VIP IP 주소를 할당 하 여 준비 합니다.  VIP는 클러스터의 부동 주소와 일치 해야 합니다.

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

3. 만들 프런트\-끝 IP 주소입니다.

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

4. 백업\-클러스터 노드를 포함 하는 풀을 종료 합니다.

   ```PowerShell
   $BackEnd = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
   $BackEnd.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties
   $BackEnd.resourceId = "Backend1"
   $BackEnd.resourceRef = "/loadBalancers/$ResourceId/backendAddressPools/$($BackEnd.resourceId)"
   $LoadBalancerProperties.backendAddressPools += $BackEnd
   ```

5. 부동 주소에서 현재 활성 중인 클러스터 노드를 검색 하기 위한 프로브를 추가 합니다. 

   >[!NOTE]
   >아래에 정의 된 포트에서 VM의 영구 주소에 대해 프로브 쿼리.  포트는 액티브 노드에서 응답 해야 합니다. 

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

6. 부하 분산 TCP 포트 1433에 대 한 규칙을 추가 합니다.<p>프로토콜 및 필요에 따라 포트를 수정할 수 있습니다.  또한이 단계를 반복이 여러 번 추가 포트 및 protcols이이 VIP에 대 한 합니다.  이렇게 하면 부하 분산 장치의 위치에 원래 VIP 사용 하 여 노드 패킷을 보내기 때문에 대해 EnableFloatingIP $true로 설정 되어 있는지 반드시 합니다.

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

8. 백 엔드 풀에 클러스터 노드를 추가 합니다.<p>클러스터에 필요한 만큼 풀에 대 한 많은 노드를 추가할 수 있습니다.

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

   부하 분산 장치를 생성 하 고 백 엔드 풀에 네트워크 인터페이스를 추가 하면, 클러스터를 구성할 준비가 되었습니다.  

9. (선택 사항) Microsoft 장애 조치 클러스터를 사용 하는 경우 다음 예제를 사용 하 여 계속 합니다. 

## <a name="example-2-configuring-a-microsoft-failover-cluster"></a>예 2: Microsoft 장애 조치 클러스터 구성

장애 조치 클러스터를 구성 하려면 다음 단계를 사용할 수 있습니다.

1. 설치 하 고 장애 조치 클러스터에 대 한 속성을 구성 합니다.

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

4. 클러스터 IP 및 프로브 포트를 설정 합니다.<p>IP 주소에는 이전 예제에서 사용 되는 프런트 엔드 ip 주소와 일치 해야 합니다 및 프로브 포트에는 이전 예제에서 프로브 포트와 일치 해야 합니다.

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

_**클러스터 활성 상태입니다.** _ 현재 노드에서 지정된 된 포트에서 VIP로 트래픽을 전달 됩니다.

---