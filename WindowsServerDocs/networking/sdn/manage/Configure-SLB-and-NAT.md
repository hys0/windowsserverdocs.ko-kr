---
title: 부하 분산 및 NAT(Network Address Translation)에 대한 소프트웨어 부하 분산 장치 구성
description: 이 항목은 Windows Server 2016에서 테 넌 트 워크 로드 및 가상 네트워크를 관리 하는 방법에 대 한 소프트웨어 정의 네트워킹 가이드의 일부입니다.
manager: dougkim
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 73bff8ba-939d-40d8-b1e5-3ba3ed5439c3
ms.author: lizross
author: eross-msft
ms.date: 08/23/2018
ms.openlocfilehash: a12d9a1ea953b587918fed8367ee21626697e256
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309884"
---
# <a name="configure-the-software-load-balancer-for-load-balancing-and-network-address-translation-nat"></a>부하 분산 및 NAT(Network Address Translation)에 대한 소프트웨어 부하 분산 장치 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 소프트웨어 정의 네트워킹 \(SDN\) 소프트웨어 부하\) \(분산 장치를 사용 하는 방법에 대 한 자세한 내용은 \(NAT\), 인바운드 NAT 또는 응용 프로그램의 여러 인스턴스 간 부하 분산을 제공 하는 아웃 바운드 네트워크 주소 변환을 제공 합니다.

## <a name="software-load-balancer-overview"></a>소프트웨어 Load Balancer 개요

SDN 소프트웨어 Load Balancer \(SLB\)는 응용 프로그램에 고가용성 및 네트워크 성능을 제공 합니다. 이는 부하 분산 장치 집합에 정의 된 클라우드 서비스 또는 가상 컴퓨터의 정상 서비스 인스턴스 간에 들어오는 트래픽을 분산 하는 계층 4 \(TCP, UDP\) 부하 분산 장치입니다.

SLB를 구성 하 여 다음을 수행 합니다.

- 가상 네트워크 외부에서 들어오는 트래픽의 부하를 가상 컴퓨터 \(Vm\)(공용 VIP 부하 분산이 라고도 함)에 분산 합니다.
- 가상 네트워크의 Vm 간, 클라우드 서비스의 Vm 간 또는 크로스-프레미스 가상 네트워크의 온-프레미스 컴퓨터와 Vm 간에 들어오는 트래픽의 부하를 분산 합니다. 
- NAT (network address translation)를 사용 하 여 가상 네트워크에서 외부 대상으로 VM 네트워크 트래픽을 전달 합니다 (아웃 바운드 NAT 라고도 함).
- 인바운드 NAT 라고도 하는 특정 VM에 외부 트래픽을 전달 합니다.




## <a name="example-create-a-public-vip-for-load-balancing-a-pool-of-two-vms-on-a-virtual-network"></a>예: 가상 네트워크에서 두 Vm의 풀을 부하 분산 하는 공용 VIP 만들기

이 예제에서는 VIP에 대 한 요청을 처리 하기 위해 공용 VIP와 두 개의 Vm을 풀 멤버로 사용 하 여 부하 분산 장치 개체를 만듭니다. 또한이 예제 코드는 풀 멤버 중 하나가 응답성이 아닌 지를 검색 하는 HTTP 상태 프로브를 추가 합니다.

1. 부하 분산 장치 개체를 준비 합니다.

   ```PowerShell
    import-module NetworkController

    $URI = "https://sdn.contoso.com"

    $LBResourceId = "LB2"

    $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties
   ```

2. 일반적으로 VIP (가상 IP) 라고 하는 프런트 엔드 IP 주소를 할당 합니다.<p>VIP는 부하 분산 장치 관리자에 지정 된 논리 네트워크 IP 풀 중 하나에서 사용 하지 않는 IP에 속해야 합니다. 

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

3. 부하 분산 Vm 집합의 구성원을 구성 하는 동적 Ip (Dip)를 포함 하는 백 엔드 주소 풀을 할당 합니다. 

   ```PowerShell 
    $BackEndAddressPool = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
    $BackEndAddressPool.ResourceId = "BE1"
    $BackEndAddressPool.ResourceRef = "/loadBalancers/$LBResourceId/backendAddressPools/$($BackEndAddressPool.ResourceId)"

    $BackEndAddressPool.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties

    $LoadBalancerProperties.backendAddressPools += $BackEndAddressPool
   ```

4. 부하 분산 장치에서 백 엔드 풀 멤버의 상태를 확인 하는 데 사용 하는 상태 프로브를 정의 합니다.<p>이 예제에서는 "/health.htm."의 RequestPath에 쿼리 하는 HTTP 프로브를 정의 합니다.  쿼리는 IntervalInSeconds 속성에 지정 된 대로 5 초 마다 실행 됩니다.<p>상태 프로브는 백 엔드 IP가 정상 상태를 고려 하기 위해 프로브에 대 한 11 개의 연속 쿼리에 대해 200의 HTTP 응답 코드를 받아야 합니다. 백 엔드 IP가 정상이 아닌 경우 부하 분산 장치에서 트래픽을 수신 하지 않습니다.

   >[!IMPORTANT]
   >백 엔드 IP에 적용 하는 Acl (Access Control 목록)에 대 한 서브넷의 첫 번째 IP로 들어오고 나가는 트래픽을 차단 하지 마십시오 .이는 프로브에 대 한 지점입니다.

   다음 예제를 사용 하 여 상태 프로브를 정의 합니다.

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

5. 프런트 엔드 IP에 도착 하는 트래픽을 백 엔드 IP에 전송 하는 부하 분산 규칙을 정의 합니다.  이 예제에서 백 엔드 풀은 포트 80에 대 한 TCP 트래픽을 수신 합니다.<p>다음 예제를 사용 하 여 부하 분산 규칙을 정의 합니다.

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

6. 네트워크 컨트롤러에 부하 분산 장치 구성을 추가 합니다.<p>다음 예제를 사용 하 여 부하 분산 장치 구성을 네트워크 컨트롤러에 추가 합니다.

   ```PowerShell
    $LoadBalancerResource = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $LBResourceId -Properties $LoadBalancerProperties -Force -PassInnerException
   ```

7. 다음 예제에 따라이 백 엔드 풀에 네트워크 인터페이스를 추가 합니다.


## <a name="example-use-slb-for-outbound-nat"></a>예: 아웃 바운드 NAT에 SLB 사용

이 예제에서는 인터넷에 대 한 아웃 바운드 연결을 위해 가상 네트워크의 개인 주소 공간에 있는 VM에 아웃 바운드 NAT 기능을 제공 하기 위해 백 엔드 풀을 사용 하 여 SLB를 구성 합니다. 

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

3. 네트워크 컨트롤러에 부하 분산 장치 개체를 추가 합니다.

   ```PowerShell
    $LoadBalancerResource = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $LBResourceId -Properties $LoadBalancerProperties -Force -PassInnerException
   ```

4. 인터넷 액세스를 제공 하려는 네트워크 인터페이스를 추가 하려면 다음 예제를 따르세요.

## <a name="example-add-network-interfaces-to-the-back-end-pool"></a>예: 백 엔드 풀에 네트워크 인터페이스 추가
이 예제에서는 백 엔드 풀에 네트워크 인터페이스를 추가 합니다.  VIP에 대 한 요청을 처리할 수 있는 각 네트워크 인터페이스에 대해이 단계를 반복 해야 합니다. 

단일 네트워크 인터페이스에서이 프로세스를 반복 하 여 여러 부하 분산 장치 개체에 추가할 수도 있습니다. 예를 들어 웹 서버 VIP에 대 한 부하 분산 장치 개체와 아웃 바운드 NAT를 제공 하는 별도의 부하 분산 장치 개체가 있는 경우입니다.
    
1. 네트워크 인터페이스를 추가할 백 엔드 풀을 포함 하는 부하 분산 장치 개체를 가져옵니다.

   ```PowerShell
   $lbresourceid = "LB2"
   $lb = get-networkcontrollerloadbalancer -connectionuri $uri -resourceID $LBResourceId -PassInnerException
   ```

2. 네트워크 인터페이스를 가져오고 backendaddress 풀을 loadbalancerbackendaddresspools 배열에 추가 합니다.

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06 -PassInnerException
   $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
   ```  

3. 네트워크 인터페이스를 배치 하 여 변경 내용을 적용 합니다. 

   ```PowerShell
   new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06 -properties $nic.properties -force -PassInnerException
   ``` 


## <a name="example-use-the-software-load-balancer-for-forwarding-traffic"></a>예: 트래픽을 전달 하는 데 Software Load Balancer 사용
개별 포트를 정의 하지 않고 가상 IP를 가상 네트워크의 단일 네트워크 인터페이스에 매핑해야 하는 경우 L3 전달 규칙을 만들 수 있습니다.  이 규칙은 PublicIPAddress 개체에 포함 된 할당 된 VIP를 통해 VM에 대 한 모든 트래픽을 전달 합니다.

VIP 및 DIP를 동일한 서브넷으로 정의한 경우이는 NAT 없이 L3 전달을 수행 하는 것과 같습니다.

>[!NOTE]
>이 프로세스에서는 부하 분산 장치 개체를 만들 필요가 없습니다.  PublicIPAddress를 네트워크 인터페이스에 할당 하면 소프트웨어 Load Balancer 구성을 수행 하는 데 충분 한 정보가 있습니다.


1. VIP를 포함 하는 공용 IP 개체를 만듭니다.

   ```PowerShell
   $publicIPProperties = new-object Microsoft.Windows.NetworkController.PublicIpAddressProperties
   $publicIPProperties.ipaddress = "10.127.134.7"
   $publicIPProperties.PublicIPAllocationMethod = "static"
   $publicIPProperties.IdleTimeoutInMinutes = 4
   $publicIP = New-NetworkControllerPublicIpAddress -ResourceId "MyPIP" -Properties $publicIPProperties -ConnectionUri $uri -Force -PassInnerException
   ```

2. PublicIPAddress를 네트워크 인터페이스에 할당 합니다.

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
   $nic.properties.IpConfigurations[0].Properties.PublicIPAddress = $publicIP
   New-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId $nic.ResourceId -Properties $nic.properties -PassInnerException
   ```

## <a name="example-use-the-software-load-balancer-for-forwarding-traffic-with-a-dynamically-allocated-vip"></a>예: 동적으로 할당 된 VIP를 사용 하 여 트래픽을 전달 하는 데 Software Load Balancer 사용
이 예제는 이전 예제와 동일한 작업을 반복 하지만, 특정 IP 주소를 지정 하는 대신 부하 분산 장치에서 사용 가능한 Vip 풀의 VIP를 자동으로 할당 합니다. 

1. VIP를 포함 하는 공용 IP 개체를 만듭니다.

   ```PowerShell
   $publicIPProperties = new-object Microsoft.Windows.NetworkController.PublicIpAddressProperties
   $publicIPProperties.PublicIPAllocationMethod = "dynamic"
   $publicIPProperties.IdleTimeoutInMinutes = 4
   $publicIP = New-NetworkControllerPublicIpAddress -ResourceId "MyPIP" -Properties $publicIPProperties -ConnectionUri $uri -Force -PassInnerException
   ```

2. PublicIPAddress 리소스를 쿼리하여 할당 된 IP 주소를 확인 합니다.

   ```PowerShell
    (Get-NetworkControllerPublicIpAddress -ConnectionUri $uri -ResourceId "MyPIP").properties
   ```

   IpAddress 속성은 할당 된 주소를 포함 합니다.  출력은 다음과 유사 합니다.
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
 
3. PublicIPAddress를 네트워크 인터페이스에 할당 합니다.

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
   $nic.properties.IpConfigurations[0].Properties.PublicIPAddress = $publicIP
   New-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId $nic.ResourceId -Properties $nic.properties -PassInnerException
   ```
   ## <a name="example-remove-a-publicip-address-that-is-being-used-for-forwarding-traffic-and-return-it-to-the-vip-pool"></a>예: 트래픽을 전달 하는 데 사용 되는 PublicIP 주소를 제거 하 고 VIP 풀로 반환
   이 예제에서는 이전 예제에서 만든 PublicIPAddress 리소스를 제거 합니다.  PublicIPAddress 제거 되 면 PublicIPAddress에 대 한 참조가 네트워크 인터페이스에서 자동으로 제거 되 고, 트래픽이 전달 되지 않으며, 다시 사용 하기 위해 IP 주소가 공용 VIP 풀로 반환 됩니다.  

4. PublicIP 제거

   ```PowerShell
   Remove-NetworkControllerPublicIPAddress -ConnectionURI $uri -ResourceId "MyPIP"
   ```

---


 