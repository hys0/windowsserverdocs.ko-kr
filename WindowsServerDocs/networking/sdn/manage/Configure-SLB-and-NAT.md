---
title: 부하 분산 및 NAT(Network Address Translation)에 대한 소프트웨어 부하 분산 장치 구성
description: 이 항목은 테 넌 트 워크 로드 관리 및 Windows Server 2016에서 가상 네트워크에는 방법은 소프트웨어 정의 네트워킹 가이드의 일부입니다.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 73bff8ba-939d-40d8-b1e5-3ba3ed5439c3
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 4d53c4bcbe1f37f532f2861d5669201959a9f091
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446673"
---
# <a name="configure-the-software-load-balancer-for-load-balancing-and-network-address-translation-nat"></a>부하 분산 및 NAT(Network Address Translation)에 대한 소프트웨어 부하 분산 장치 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

소프트웨어 정의 네트워킹을 사용 하는 방법을 알아보려면이 항목을 사용할 수 있습니다 \(SDN\) 소프트웨어 부하 분산 장치 \(SLB\) 아웃 바운드 네트워크 주소 변환 수 있도록 \(NAT\), 인바운드 NAT 또는 부하는 응용 프로그램의 여러 인스턴스 간에 분산 합니다.

## <a name="software-load-balancer-overview"></a>소프트웨어 부하 분산 장치 개요

SDN 소프트웨어 부하 분산 장치 \(SLB\) 응용 프로그램에 고가용성 및 네트워크 성능을 제공 합니다. 레이어 4 것 \(TCP, UDP\) 부하 분산 장치는 들어오는 트래픽을 클라우드 서비스 또는 부하 분산 장치 집합에 정의 된 virtual machines의 정상적인 서비스 인스턴스에 분산 합니다.

다음을 수행 하는 SLB를 구성 합니다.

- 들어오는 트래픽을 부하 분산 가상 컴퓨터에 가상 네트워크에 외부 \(Vm\), 공용 VIP 부하 분산을 라고도 합니다.
- 부하 들어오는 트래픽을 가상 네트워크의 Vm 간, 클라우드 서비스의 Vm 간 또는 온-프레미스 컴퓨터와 크로스-프레미스 가상 네트워크의 Vm 간에 분산 합니다. 
- 가상 네트워크에서 아웃 바운드 NAT. 라고도 네트워크 주소 변환 (NAT)를 사용 하 여 외부 대상 VM 네트워크 트래픽을 전달합니다
- 외부 트래픽을 특정 VM에 인바운드 NAT. 라고도 전달




## <a name="example-create-a-public-vip-for-load-balancing-a-pool-of-two-vms-on-a-virtual-network"></a>예: 부하 분산 가상 네트워크에 두 Vm의 풀에 대 한 공용 VIP 만들기

이 예제에서는 VIP로 요청을 처리 하는 풀 구성원으로 공용 VIP와 두 개의 Vm을 사용 하 여 부하 분산 장치 개체를 만듭니다. 이 예제 코드는 또한 풀 멤버 중 하나가 응답 하지 않는 있는지 여부를 검색 하는 HTTP 상태 프로브를 추가 합니다.

1. 부하 분산 장치 개체를 준비 합니다.

   ```PowerShell
    import-module NetworkController

    $URI = "https://sdn.contoso.com"

    $LBResourceId = "LB2"

    $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties
   ```

2. 일반적으로 참조 가상 IP (VIP)로 프런트 엔드 IP 주소를 할당 합니다.<p>VIP는 부하 분산 장치 관리자에 지정 된 논리 네트워크 IP 풀 중 하나에서 사용 되지 않는 ip 여야 합니다. 

   ```PowerShell
    $VIPIP = "10.127.134.5"
    $VIPLogicalNetwork = get-networkcontrollerlogicalnetwork -ConnectionUri $uri -resourceid "PublicVIP" -PassInnerException
    
    $FrontEndIPConfig = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfiguration
    $FrontEndIPConfig.ResourceId = "FE1"
    $FrontEndIPConfig.ResourceRef = "/loadBalancers/$LBResourceId/frontendIPConfigurations/$($FrontEndIPConfig.ResourceId)"

    $FrontEndIPConfig.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfigurationProperties
    $FrontEndIPConfig.Properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $FrontEndIPConfig.Properties.Subnet.ResourceRef = $VIPLogicalNetwork.Properties.Subnets[0].ResourceRef
    $FrontEndIPConfig.Properties.PrivateIPAddress = $VIPIP
    $FrontEndIPConfig.Properties.PrivateIPAllocationMethod = "Static"
      
    $LoadBalancerProperties.FrontEndIPConfigurations += $FrontEndIPConfig
   ```

3. Vm의 부하 분산 된 집합의 멤버를 구성 하는 동적 Ip (Dip)를 포함 하는 백 엔드 주소 풀을 할당 합니다. 

   ```PowerShell 
    $BackEndAddressPool = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
    $BackEndAddressPool.ResourceId = "BE1"
    $BackEndAddressPool.ResourceRef = "/loadBalancers/$LBResourceId/backendAddressPools/$($BackEndAddressPool.ResourceId)"

    $BackEndAddressPool.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties

    $LoadBalancerProperties.backendAddressPools += $BackEndAddressPool
   ```

4. 부하 분산 장치 백 엔드 풀 멤버의 상태를 확인 하기 위해 사용 하는 상태 프로브를 정의 합니다.<p>이 예제에서의 RequestPath을 쿼리 하는 HTTP 프로브 정의 "/ health.htm."  쿼리는 IntervalInSeconds 속성에 지정 된 대로 5 초 마다 실행 됩니다.<p>상태 프로브에 200 정상 백 엔드 IP를 고려해 야 할 프로브에 대 한 11 연속 된 쿼리에 대 한 HTTP 응답 코드를 받아야 합니다. 백 엔드 IP를 정상 없는 경우 해당 트래픽을 수신 하지 않습니다 부하 분산 장치에서.

   >[!IMPORTANT]
   >모든 액세스 제어 목록 (Acl) 프로브에 대 한 보내는 위치 이기 때문에 백 엔드 IP에 적용 되는 서브넷의 첫 번째 IP 간에 트래픽을 차단 하지 않습니다.

   상태 프로브를 정의 하려면 다음 예제를 사용 합니다.

   ```PowerShell
    $Probe = new-object Microsoft.Windows.NetworkController.LoadBalancerProbe
    $Probe.ResourceId = "Probe1"
    $Probe.ResourceRef = "/loadBalancers/$LBResourceId/Probes/$($Probe.ResourceId)"

    $Probe.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerProbeProperties
    $Probe.properties.Protocol = "HTTP"
    $Probe.properties.Port = "80"
    $Probe.properties.RequestPath = "/health.htm"
    $Probe.properties.IntervalInSeconds = 5
    $Probe.properties.NumberOfProbes = 11

    $LoadBalancerProperties.Probes += $Probe
   ```

5. 부하 분산 프런트 엔드 IP를 백 엔드 ip에 도착 하는 트래픽을 전송 하는 규칙을 정의 합니다.  이 예제에서는 백 엔드 풀에 포트 80에 TCP 트래픽을 받습니다.<p>부하 분산 규칙을 정의 하려면 다음 예제를 사용 합니다.

   ```PowerShell
   $Rule = new-object Microsoft.Windows.NetworkController.LoadBalancingRule
   $Rule.ResourceId = "webserver1"

   $Rule.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancingRuleProperties
   $Rule.Properties.FrontEndIPConfigurations += $FrontEndIPConfig
   $Rule.Properties.backendaddresspool = $BackEndAddressPool 
   $Rule.Properties.protocol = "TCP"
   $Rule.Properties.FrontEndPort = 80
   $Rule.Properties.BackEndPort = 80
   $Rule.Properties.IdleTimeoutInMinutes = 4
   $Rule.Properties.Probe = $Probe

   $LoadBalancerProperties.loadbalancingRules += $Rule
   ```

6. 네트워크 컨트롤러에 부하 분산 장치 구성을 추가 합니다.<p>네트워크 컨트롤러에 부하 분산 장치 구성을 추가 하려면 다음 예제를 사용 합니다.

   ```PowerShell
    $LoadBalancerResource = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $LBResourceId -Properties $LoadBalancerProperties -Force -PassInnerException
   ```

7. 이 백 엔드 풀으로 네트워크 인터페이스를 추가 하려면 다음 예제를 따릅니다.


## <a name="example-use-slb-for-outbound-nat"></a>예: SLB를 사용 하 여 아웃 바운드 NAT에 대 한

이 예제에서는 인터넷에 아웃 바운드 연결할 가상 네트워크의 개인 주소 공간에서 VM에 대 한 아웃 바운드 NAT 기능을 제공 하는 것에 대 한 백 엔드 풀을 사용 하 여 SLB를 구성 합니다. 

1. 부하 분산 장치 속성, 프런트 엔드 IP 및 백 엔드 풀을 만듭니다.

   ```PowerShell
    import-module NetworkController
    $URI = "https://sdn.contoso.com"

    $LBResourceId = "OutboundNATMMembers"
    $VIPIP = "10.127.134.6"

    $VIPLogicalNetwork = get-networkcontrollerlogicalnetwork -ConnectionUri $uri -resourceid "PublicVIP" -PassInnerException

    $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties

    $FrontEndIPConfig = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfiguration
    $FrontEndIPConfig.ResourceId = "FE1"
    $FrontEndIPConfig.ResourceRef = "/loadBalancers/$LBResourceId/frontendIPConfigurations/$($FrontEndIPConfig.ResourceId)"

    $FrontEndIPConfig.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfigurationProperties
    $FrontEndIPConfig.Properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $FrontEndIPConfig.Properties.Subnet.ResourceRef = $VIPLogicalNetwork.Properties.Subnets[0].ResourceRef
    $FrontEndIPConfig.Properties.PrivateIPAddress = $VIPIP
    $FrontEndIPConfig.Properties.PrivateIPAllocationMethod = "Static"

    $LoadBalancerProperties.FrontEndIPConfigurations += $FrontEndIPConfig

    $BackEndAddressPool = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
    $BackEndAddressPool.ResourceId = "BE1"
    $BackEndAddressPool.ResourceRef = "/loadBalancers/$LBResourceId/backendAddressPools/$($BackEndAddressPool.ResourceId)"
    $BackEndAddressPool.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties

    $LoadBalancerProperties.backendAddressPools += $BackEndAddressPool
   ```

2. 아웃 바운드 NAT 규칙을 정의 합니다.

   ```PowerShell
    $OutboundNAT = new-object Microsoft.Windows.NetworkController.LoadBalancerOutboundNatRule
    $OutboundNAT.ResourceId = "onat1"
    
    $OutboundNAT.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerOutboundNatRuleProperties
    $OutboundNAT.properties.frontendipconfigurations += $FrontEndIPConfig
    $OutboundNAT.properties.backendaddresspool = $BackEndAddressPool
    $OutboundNAT.properties.protocol = "ALL"

    $LoadBalancerProperties.OutboundNatRules += $OutboundNAT
   ```

3. 네트워크 컨트롤러에서 부하 분산 장치 개체를 추가 합니다.

   ```PowerShell
    $LoadBalancerResource = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $LBResourceId -Properties $LoadBalancerProperties -Force -PassInnerException
   ```

4. 인터넷 액세스를 제공 하려는 네트워크 인터페이스를 추가 하려면 다음 예제를 따릅니다.

## <a name="example-add-network-interfaces-to-the-back-end-pool"></a>예: 백 엔드 풀에 네트워크 인터페이스 추가
이 예제에서는 백 엔드 풀에 네트워크 인터페이스를 추가 합니다.  VIP에 대 한 요청을 처리할 수 있는 각 네트워크 인터페이스에 대해이 단계를 반복 해야 합니다. 

또한 여러 부하 분산 장치 개체에 추가할 단일 네트워크 인터페이스에 대해이 프로세스를 반복할 수 있습니다. 예를 들어, 웹 서버 VIP에 대 한 부하 분산 장치 개체 및 아웃 바운드 NAT.를 제공 하는 별도 부하 분산 장치 개체에 있는 경우
    
1. 네트워크 인터페이스를 추가 하려면 백 엔드 풀이 포함 된 부하 분산 장치 개체를 가져옵니다.

   ```PowerShell
   $lbresourceid = "LB2"
   $lb = get-networkcontrollerloadbalancer -connectionuri $uri -resourceID $LBResourceId -PassInnerException
   ```

2. 네트워크 인터페이스를 가져와 loadbalancerbackendaddresspools 배열 backendaddress 풀을 추가 합니다.

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06 -PassInnerException
   $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
   ```  

3. 변경 내용을 적용 하려면 네트워크 인터페이스를 배치 합니다. 

   ```PowerShell
   new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06 -properties $nic.properties -force -PassInnerException
   ``` 


## <a name="example-use-the-software-load-balancer-for-forwarding-traffic"></a>예: 소프트웨어 부하 분산 장치를 사용 하 여 트래픽 전달
개별 포트를 정의 하지 않고 단일 네트워크 인터페이스를 가상 네트워크에 가상 IP에 매핑할 경우 L3 전달 규칙을 만들 수 있습니다.  이 규칙을 PublicIPAddress 개체에 포함 된 할당 된 VIP 통해 VM에서 모든 트래픽을 전달 합니다.

VIP 및 DIP를 정의 하는 경우 동일한 서브넷으로 다음 같습니다 NAT. 없이 L3 전달 수행

>[!NOTE]
>이 프로세스는 부하 분산 장치 개체를 만들 수 있습니다 필요가 없습니다.  해당 구성을 수행 하려면 소프트웨어 부하 분산 장치에 대 한 충분 한 정보는 PublicIPAddress 네트워크 인터페이스에 할당 합니다.


1. VIP를 포함 하는 공용 IP 개체를 만듭니다.

   ```PowerShell
   $publicIPProperties = new-object Microsoft.Windows.NetworkController.PublicIpAddressProperties
   $publicIPProperties.ipaddress = "10.127.134.7"
   $publicIPProperties.PublicIPAllocationMethod = "static"
   $publicIPProperties.IdleTimeoutInMinutes = 4
   $publicIP = New-NetworkControllerPublicIpAddress -ResourceId "MyPIP" -Properties $publicIPProperties -ConnectionUri $uri -Force -PassInnerException
   ```

2. PublicIPAddress 네트워크 인터페이스에 할당 합니다.

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
   $nic.properties.IpConfigurations[0].Properties.PublicIPAddress = $publicIP
   New-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId $nic.ResourceId -Properties $nic.properties -PassInnerException
   ```

## <a name="example-use-the-software-load-balancer-for-forwarding-traffic-with-a-dynamically-allocated-vip"></a>예: 소프트웨어 부하 분산 장치를 사용 하 여 동적으로 할당 된 VIP를 사용 하 여 트래픽 전달
이 예제에서는 이전 예와 동일한 작업을 반복 하지만 자동으로 특정 IP 주소를 지정 하는 대신 부하 분산 장치 Vip의 사용 가능한 풀에서 VIP를 할당 합니다. 

1. VIP를 포함 하는 공용 IP 개체를 만듭니다.

   ```PowerShell
   $publicIPProperties = new-object Microsoft.Windows.NetworkController.PublicIpAddressProperties
   $publicIPProperties.PublicIPAllocationMethod = "dynamic"
   $publicIPProperties.IdleTimeoutInMinutes = 4
   $publicIP = New-NetworkControllerPublicIpAddress -ResourceId "MyPIP" -Properties $publicIPProperties -ConnectionUri $uri -Force -PassInnerException
   ```

2. 할당 된 IP 주소를 확인 하려면 PublicIPAddress 리소스를 쿼리 합니다.

   ```PowerShell
    (Get-NetworkControllerPublicIpAddress -ConnectionUri $uri -ResourceId "MyPIP").properties
   ```

   Ip 주소 속성은 할당된 된 주소를 포함 합니다.  출력은 다음과 유사 하 게 표시 됩니다.
   ```
    Counters                 : {}
    ConfigurationState       :
    IpAddress                : 10.127.134.2
    PublicIPAddressVersion   : IPv4
    PublicIPAllocationMethod : Dynamic
    IdleTimeoutInMinutes     : 4
    DnsSettings              :
    ProvisioningState        : Succeeded
    IpConfiguration          :
    PreviousIpConfiguration  :
   ```
 
3. PublicIPAddress 네트워크 인터페이스에 할당 합니다.

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
   $nic.properties.IpConfigurations[0].Properties.PublicIPAddress = $publicIP
   New-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId $nic.ResourceId -Properties $nic.properties -PassInnerException
   ```
   ## <a name="example-remove-a-publicip-address-that-is-being-used-for-forwarding-traffic-and-return-it-to-the-vip-pool"></a>예: 트래픽 전달 되는 PublicIP 주소를 제거 하 고 VIP 풀으로 반환
   이 예제에서는 이전 예제를 통해 만든 PublicIPAddress 리소스를 제거 합니다.  PublicIPAddress에 대 한 참조는 네트워크 인터페이스에서 자동으로 제거 됩니다 PublicIPAddress 제거 되 면 전달 되는 트래픽이 중지 됩니다 및 IP 주소 다시 사용 하기 위해 공용 VIP 풀으로 반환 됩니다.  

4. PublicIP를 제거 합니다.

   ```PowerShell
   Remove-NetworkControllerPublicIPAddress -ConnectionURI $uri -ResourceId "MyPIP"
   ```

---


 