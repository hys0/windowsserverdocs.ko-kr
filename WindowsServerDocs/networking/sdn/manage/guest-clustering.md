---
title: 게스트 클러스터링 가상 네트워크에서
description: 이 항목은 관리 테 작업 및 Windows Server 2016에 가상 네트워크 방법에 대해 소프트웨어 네트워킹 정의 가이드 일부입니다.
manager: brianlic
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
ms.openlocfilehash: 5cab7e7c0ca0af848b4b58362388701cc4357860
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="guest-clustering-in-a-virtual-network"></a>게스트 클러스터링 가상 네트워크에서

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

가상 컴퓨터 가상 네트워크에 연결 하는 네트워크에서 소통 하기 위해 네트워크 컨트롤러에 할당 IP 주소를 사용 하도록 허용만 됩니다.  즉, 클러스터링 Microsoft 장애 클러스터링 등 부동 IP 주소, 필요한, 제대로 작동 하기 위해 몇 가지 추가 단계를 요구 하는 기술 합니다.

연결할 수 있는 부동 IP 하는 방법은 부하 분산 소프트웨어가 \(SLB\)를 사용 하는 것 가상 IP \(VIP\) 합니다.  소프트웨어 부하 분산 SLB 교통 현재 해당 IP이 컴퓨터에 직접는 되도록 건강 검사에서 해당 IP 포트에서으로 설정 해야 합니다.

## <a name="example-load-balancer-configuration"></a>예: 부하 분산 구성

이 이때 Vm 클러스터 노드에서 되 고 가상 네트워크에 연결 하는 이미 만든 것으로 간주 합니다.  참조 지침을 위해 [VM 만들고 VLAN 또는 테 가상 네트워크에 연결](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create-a-tenant-vm)합니다.  

이 이때에는 가상 IP 주소를 (192.168.2.100) 클러스터의 부동 IP 주소를 대표 하 만들고 구성 TCP 포트 활성 있는 노드를 확인 하려면 59999 모니터링할 건강 검사 합니다.

### <a name="step-1-select-the-vip"></a>1 단계: 선택 VIP
VIP IP 주소를 지정 하 여를 준비 합니다.  이 주소 클러스터 노드에서와 같은 서브넷 모든 예약 하거나 사용 하지 않은 주소 될 수 있습니다.  VIP은 클러스터의 부동 주소와 일치 해야 합니다.

    $VIP = "192.168.2.100"
    $subnet = "Subnet2"
    $VirtualNetwork = "MyNetwork"
    $ResourceId = "MyNetwork_InternalVIP"

### <a name="step-2-create-the-load-balancer-properties-object"></a>2 단계: 부하 분산 속성 개체 만들기

명령은 부하 분산 속성 개체를 만드는 데 사용할 수 있습니다.

    $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties

### <a name="step-3-create-a-front-end-ip-address"></a>3 단계: front\ 최종 IP 주소를 만들려면

Front\ 종료 IP 주소를 만들려면 명령은 사용할 수 있습니다.

    $LoadBalancerProperties.frontendipconfigurations += $FrontEnd = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfiguration
    $FrontEnd.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfigurationProperties
    $FrontEnd.resourceId = "Frontend1"
    $FrontEnd.resourceRef = "/loadBalancers/$ResourceId/frontendIPConfigurations/$($FrontEnd.resourceId)"
    $FrontEnd.properties.subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $FrontEnd.properties.subnet.ResourceRef = "/VirtualNetworks/MyNetwork/Subnets/Subnet2"
    $FrontEnd.properties.privateIPAddress = $VIP
    $FrontEnd.properties.privateIPAllocationMethod = "Static"

### <a name="step-4-create-a-back-end-pool-to-contain-the-cluster-nodes"></a>4 단계: 클러스터 노드에서 포함 back\ 종료 풀 만들기

다음 예 명령을 사용 하 여 back\ 종료 풀 만들기

    $BackEnd = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
    $BackEnd.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties
    $BackEnd.resourceId = "Backend1"
    $BackEnd.resourceRef = "/loadBalancers/$ResourceId/backendAddressPools/$($BackEnd.resourceId)"
    $LoadBalancerProperties.backendAddressPools += $BackEnd

### <a name="step-5-add-a-probe"></a>5 단계: 검색 추가
여 선택기 부동 주소 현재에서 활성화 되는 클러스터 노드에서 감지 하는 데 필요한입니다.

>[!NOTE]
>아래에 정의 된 포트에서 VM의 영구 주소에 대해 검색 쿼리.  포트 활성 노드에서 응답만 해야 합니다. 

    $LoadBalancerProperties.probes += $lbprobe = new-object Microsoft.Windows.NetworkController.LoadBalancerProbe
    $lbprobe.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerProbeProperties

    $lbprobe.ResourceId = "Probe1"
    $lbprobe.resourceRef = "/loadBalancers/$ResourceId/Probes/$($lbprobe.resourceId)"
    $lbprobe.properties.protocol = "TCP"
    $lbprobe.properties.port = "59999"
    $lbprobe.properties.IntervalInSeconds = 5
    $lbprobe.properties.NumberOfProbes = 11

### <a name="step-5-add-the-load-balancing-rules"></a>5 단계: 규칙 균형 추가
이 단계를 부하 분산 TCP 포트 1433 규칙을 만듭니다.  프로토콜 및 필요에 따라 포트 수정할 수 있습니다.  또한이 단계를 반복이 여러 번 추가 포트 및이 VIP에서 protcols 합니다.  이 장소에 원래 VIP 된 노드로 패킷을 보내는 데 부하 분산을 보면 EnableFloatingIP $true로 설정 되어 있는지 반드시 합니다.

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

### <a name="step-5-create-the-load-balancer-in-network-controller"></a>5 단계: 부하 분산 네트워크 컨트롤러에서 만들기

부하 분산 만드는 명령은 사용할 수 있습니다.

    $lb = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $ResourceId -Properties $LoadBalancerProperties -Force

### <a name="step-6-add-the-cluster-nodes-to-the-backend-pool"></a>6 단계: 클러스터 노드에서 백 엔드 풀에 추가

이 이때 두 풀 구성원을 추가 표시 되지만 요구 사항 클러스터에 따라의 노드 풀에 추가할 수 있습니다.

    # Cluster Node 1

    $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid "ClusterNode1_Network-Adapter"
    $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
    $nic = new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid $nic.resourceid -properties $nic.properties -force

    # Cluster Node 2

    $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid "ClusterNode2_Network-Adapter"
    $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
    $nic = new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid $nic.resourceid -properties $nic.properties -force

부하 분산 만들고 한 네트워크 인터페이스 백 엔드 풀에 추가 했 되 면 구성 클러스터 준비가 됩니다.  Microsoft 클러스터 장애 조치를 사용 하는 경우 다음 예제를 계속할 수 있습니다. 

## <a name="example-2-configuring-a-microsoft-failover-cluster"></a>2 예제: Microsoft 장애 클러스터 구성

클러스터 장애 조치 구성 하려면 다음 단계를 사용할 수 있습니다.

### <a name="step-1-install-failover-clustering"></a>1 단계: 클러스터링 설치

설치 하 고 속성 장애 클러스터에 대 한 구성 다음 예제 명령을 사용할 수 있습니다.

    add-windowsfeature failover-clustering -IncludeManagementTools
    Import-module failoverclusters

    $ClusterName = "MyCluster"
   
    $ClusterNetworkName = "Cluster Network 1"
    $IPResourceName =  
    $ILBIP = “192.168.2.100” 

    $nodes = @("DB1", "DB2")

### <a name="step-2-create-the-cluster-on-one-node"></a>2 단계: 한 노드에서 클러스터 만들기

클러스터 노드에서 만드는 명령은 사용할 수 있습니다.

    New-Cluster -Name $ClusterName -NoStorage -Node $nodes[0]

### <a name="step-3-stop-the-cluster-resource"></a>3 단계: 중지 클러스터 리소스

명령은 중지 클러스터 리소스를 사용할 수 있습니다.

    Stop-ClusterResource "Cluster Name" 

### <a name="step-4-set-the-cluster-ip-and-probe-port"></a>4 단계: IP 및 검색 포트 클러스터 설정
IP 주소 이전 예에서 사용 프런트 ip 주소와 일치 해야 하 고 검색 포트 위 예제에서 검색 포트 일치 해야 합니다.

    Get-ClusterResource "Cluster IP Address" | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

### <a name="step-5-start-the-cluster-resources"></a>5 단계: 시작 클러스터 리소스

명령은 시작 클러스터 리소스를 사용할 수 있습니다.

    Start-ClusterResource "Cluster IP Address"  -Wait 60 
    Start-ClusterResource "Cluster Name"  -Wait 60 

### <a name="step-6-add-the-remaining-nodes"></a>6 단계: 나머지 노드의 추가

클러스터 노드에서 추가 명령은 사용할 수 있습니다.

    Add-ClusterNode $nodes[1]

마지막 단계를 완료 되 면 클러스터 활성화 됩니다. 교통 지정된 포트에서 VIP으로 이동에 나오는 이동 합니다.