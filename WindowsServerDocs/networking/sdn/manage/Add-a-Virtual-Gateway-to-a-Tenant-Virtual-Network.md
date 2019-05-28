---
title: 테넌트 가상 네트워크에 가상 게이트웨이 추가
description: 테 넌 트의 가상 네트워크에 대 한 사이트 간 연결을 제공 하려면 Windows PowerShell cmdlet 및 스크립트를 사용 하는 방법에 알아봅니다.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9552054-4eb9-48db-a6ce-f36ae55addcd
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: b76019232be5091440c3e0cf5ad85569cbe0d4dc
ms.sourcegitcommit: 21165734a0f37c4cd702c275e85c9e7c42d6b3cb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2019
ms.locfileid: "65034488"
---
# <a name="add-a-virtual-gateway-to-a-tenant-virtual-network"></a>테넌트 가상 네트워크에 가상 게이트웨이 추가 

>적용 대상: Windows Server (반기 채널), Windows Server 2016 

테 넌 트의 가상 네트워크에 대 한 사이트 간 연결을 제공 하려면 Windows PowerShell cmdlet 및 스크립트를 사용 하는 방법에 알아봅니다. 이 항목에서는 테 넌 트 가상 게이트웨이 네트워크 컨트롤러를 사용 하 여 게이트웨이 풀의 구성원 인 RAS 게이트웨이 인스턴스를 추가 합니다. RAS 게이트웨이 각 테 넌 트에 사용 된 대역폭에 따라 최대 1 백 테 넌 트를 지원 합니다. 네트워크 컨트롤러는 자동으로 테 넌 트에 대 한 새 가상 게이트웨이 배포할 때 사용 하는 최상의 RAS 게이트웨이 결정 합니다.  

각 가상 게이트웨이 특정 테 넌 트에 해당 하며 하나 이상의 네트워크 연결 (사이트 간 VPN 터널) 하 고, 필요에 따라 프로토콜 BGP (경계 게이트웨이) 연결 구성 됩니다. 사이트 간 연결을 제공 하는 경우 고객에 게 인터넷, 테 넌 트 엔터프라이즈 네트워크 및 서비스 공급자 네트워크를 사용 하는 등 외부 네트워크에 해당 테 넌 트 가상 네트워크를 연결할 수 있습니다.
  
**테 넌 트 가상 게이트웨이 배포 하는 경우 다음 구성 옵션을 수 있습니다.**  

| 네트워크 연결 옵션 | BGP 구성 옵션  |
|---------|---------|
|<ul><li>IPSec 사이트 간 가상 사설망 (VPN)</li><li>Generic Routing Encapsulation GRE)</li><li>계층 3 전달</li></ul>     |<ul><li>BGP 라우터 구성</li><li>BGP 피어 구성</li><li>BGP 라우팅 정책 구성</li></ul>         |
---

Windows PowerShell 예제 스크립트 및 명령에서이 항목에서는 이러한 각 옵션을 사용 하 여 RAS 게이트웨이에서 테 넌 트 가상 게이트웨이 배포 하는 방법을 보여 줍니다.  
  
   
>[!IMPORTANT]  
>예제에서는 Windows PowerShell 명령 및 제공 하는 스크립트를 실행 하기 전에 값 배포에 대 한 적절 한 되도록 모든 변수 값 변경 해야 합니다.  
  
1.  네트워크 컨트롤러에 게이트웨이 풀 개체가 있는지 확인 합니다. 

    ```PowerShell
    $uri = "https://ncrest.contoso.com"   
      
    # Retrieve the Gateway Pool configuration  
    $gwPool = Get-NetworkControllerGatewayPool -ConnectionUri $uri  
      
    # Display in JSON format  
    $gwPool | ConvertTo-Json -Depth 2   
     
    ```  

2.  네트워크 컨트롤러에서 사용 하는 테 넌 트의 가상 네트워크에서 패킷을 라우팅하려면 서브넷이 있는지 확인 합니다. 테 넌 트 게이트웨이 및 가상 네트워크 간의 라우팅에 사용 하는 가상 서브넷을 검색할 수도 있습니다.  
  
    ```PowerShell 
    $uri = "https://ncrest.contoso.com"   
      
    # Retrieve the Tenant Virtual Network configuration  
    $Vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri  -ResourceId "Contoso_Vnet1"   
      
    # Display in JSON format  
    $Vnet | ConvertTo-Json -Depth 4   
      
    # Retrieve the Tenant Virtual Subnet configuration  
    $RoutingSubnet = Get-NetworkControllerVirtualSubnet -ConnectionUri $uri  -ResourceId "Contoso_WebTier" -VirtualNetworkID $vnet.ResourceId   
      
    # Display in JSON format  
    $RoutingSubnet | ConvertTo-Json -Depth 4   
      
    ```  

3.  테 넌 트 가상 게이트웨이에 대 한 새 개체를 만들고 게이트웨이 풀 참조를 업데이트 합니다.  게이트웨이 및 가상 네트워크 간의 라우팅에 사용 하는 가상 서브넷을 지정할 수도 있습니다.  가상 서브넷을 지정한 후 가상 게이트웨이 개체 속성의 나머지 부분을 업데이트 하 고 테 넌 트에 대 한 새로운 가상 게이트웨이 추가 합니다.
  
    ```PowerShell  
    # Create a new object for Tenant Virtual Gateway  
    $VirtualGWProperties = New-Object Microsoft.Windows.NetworkController.VirtualGatewayProperties   
      
    # Update Gateway Pool reference  
    $VirtualGWProperties.GatewayPools = @()   
    $VirtualGWProperties.GatewayPools += $gwPool   
      
    # Specify the Virtual Subnet that is to be used for routing between the gateway and Virtual Network   
    $VirtualGWProperties.GatewaySubnets = @()   
    $VirtualGWProperties.GatewaySubnets += $RoutingSubnet   
      
    # Update the rest of the Virtual Gateway object properties  
    $VirtualGWProperties.RoutingType = "Dynamic"   
    $VirtualGWProperties.NetworkConnections = @()   
    $VirtualGWProperties.BgpRouters = @()   
      
    # Add the new Virtual Gateway for tenant   
    $virtualGW = New-NetworkControllerVirtualGateway -ConnectionUri $uri  -ResourceId "Contoso_VirtualGW" -Properties $VirtualGWProperties -Force   
      
    ```  
  
4. GRE, IPsec을 사용 하 여 사이트 간 VPN 연결을 만들거나 계층 3 (L3) 전달 합니다.  

   >[!TIP]
   >필요에 따라 위의 모든 단계를 결합 하 고 모든 세 가지 연결 옵션을 사용 하 여 테 넌 트 가상 게이트웨이 구성할 수 있습니다.  자세한 내용은 참조 하세요. [모든 세 가지 연결 형식 (IPsec, GRE L3)를 사용 하 여 게이트웨이 구성 및 BGP](#optional-step-configure-a-gateway-with-all-three-connection-types-ipsec-gre-l3-and-bgp)합니다.
  
   **IPsec VPN 사이트 간 네트워크 연결**
  
   ```PowerShell  
   # Create a new object for Tenant Network Connection  
   $nwConnectionProperties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties   
  
   # Update the common object properties  
   $nwConnectionProperties.ConnectionType = "IPSec"   
   $nwConnectionProperties.OutboundKiloBitsPerSecond = 10000   
   $nwConnectionProperties.InboundKiloBitsPerSecond = 10000   
  
   # Update specific properties depending on the Connection Type  
   $nwConnectionProperties.IpSecConfiguration = New-Object Microsoft.Windows.NetworkController.IpSecConfiguration   
   $nwConnectionProperties.IpSecConfiguration.AuthenticationMethod = "PSK"   
   $nwConnectionProperties.IpSecConfiguration.SharedSecret = "P@ssw0rd"   
  
   $nwConnectionProperties.IpSecConfiguration.QuickMode = New-Object Microsoft.Windows.NetworkController.QuickMode   
   $nwConnectionProperties.IpSecConfiguration.QuickMode.PerfectForwardSecrecy = "PFS2048"   
   $nwConnectionProperties.IpSecConfiguration.QuickMode.AuthenticationTransformationConstant = "SHA256128"   
   $nwConnectionProperties.IpSecConfiguration.QuickMode.CipherTransformationConstant = "DES3"   
   $nwConnectionProperties.IpSecConfiguration.QuickMode.SALifeTimeSeconds = 1233   
   $nwConnectionProperties.IpSecConfiguration.QuickMode.IdleDisconnectSeconds = 500   
   $nwConnectionProperties.IpSecConfiguration.QuickMode.SALifeTimeKiloBytes = 2000   
  
   $nwConnectionProperties.IpSecConfiguration.MainMode = New-Object Microsoft.Windows.NetworkController.MainMode   
   $nwConnectionProperties.IpSecConfiguration.MainMode.DiffieHellmanGroup = "Group2"   
   $nwConnectionProperties.IpSecConfiguration.MainMode.IntegrityAlgorithm = "SHA256"   
   $nwConnectionProperties.IpSecConfiguration.MainMode.EncryptionAlgorithm = "AES256"   
   $nwConnectionProperties.IpSecConfiguration.MainMode.SALifeTimeSeconds = 1234   
   $nwConnectionProperties.IpSecConfiguration.MainMode.SALifeTimeKiloBytes = 2000   
  
   # L3 specific configuration (leave blank for IPSec)  
   $nwConnectionProperties.IPAddresses = @()   
   $nwConnectionProperties.PeerIPAddresses = @()   
  
   # Update the IPv4 Routes that are reachable over the site-to-site VPN Tunnel  
   $nwConnectionProperties.Routes = @()   
   $ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo   
   $ipv4Route.DestinationPrefix = "14.1.10.1/32"   
   $ipv4Route.metric = 10   
   $nwConnectionProperties.Routes += $ipv4Route   
  
   # Tunnel Destination (Remote Endpoint) Address  
   $nwConnectionProperties.DestinationIPAddress = "10.127.134.121"   
  
   # Add the new Network Connection for the tenant  
   New-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -ResourceId "Contoso_IPSecGW" -Properties $nwConnectionProperties -Force   
  
   ```  

   **GRE VPN 사이트 간 네트워크 연결**
  
   ```PowerShell  
   # Create a new object for the Tenant Network Connection  
   $nwConnectionProperties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties   
  
   # Update the common object properties  
   $nwConnectionProperties.ConnectionType = "GRE"   
   $nwConnectionProperties.OutboundKiloBitsPerSecond = 10000   
   $nwConnectionProperties.InboundKiloBitsPerSecond = 10000   
  
   # Update specific properties depending on the Connection Type  
   $nwConnectionProperties.GreConfiguration = New-Object Microsoft.Windows.NetworkController.GreConfiguration   
   $nwConnectionProperties.GreConfiguration.GreKey = 1234   
  
   # Update the IPv4 Routes that are reachable over the site-to-site VPN Tunnel  
   $nwConnectionProperties.Routes = @()   
   $ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo   
   $ipv4Route.DestinationPrefix = "14.2.20.1/32"   
   $ipv4Route.metric = 10   
   $nwConnectionProperties.Routes += $ipv4Route   
  
   # Tunnel Destination (Remote Endpoint) Address  
   $nwConnectionProperties.DestinationIPAddress = "10.127.134.122"   
  
   # L3 specific configuration (leave blank for GRE)  
   $nwConnectionProperties.L3Configuration = New-Object Microsoft.Windows.NetworkController.L3Configuration   
   $nwConnectionProperties.IPAddresses = @()   
   $nwConnectionProperties.PeerIPAddresses = @()   
  
   # Add the new Network Connection for the tenant  
   New-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -ResourceId "Contoso_GreGW" -Properties $nwConnectionProperties -Force   
  
   ```  

   **L3 전달 네트워크 연결**<p>
   L3는에 대 한 네트워크 연결이 제대로 작동 하기를 전달, 해당 논리 네트워크를 구성 해야 합니다.   
  
   1. 논리 네트워크를 L3 전달 네트워크 연결을 구성 합니다.  <br>
  
      ```PowerShell  
      # Create a new object for the Logical Network to be used for L3 Forwarding  
      $lnProperties = New-Object Microsoft.Windows.NetworkController.LogicalNetworkProperties  
      
      $lnProperties.NetworkVirtualizationEnabled = $false  
      $lnProperties.Subnets = @()  
      
      # Create a new object for the Logical Subnet to be used for L3 Forwarding and update properties  
      $logicalsubnet = New-Object Microsoft.Windows.NetworkController.LogicalSubnet  
      $logicalsubnet.ResourceId = "Contoso_L3_Subnet"  
      $logicalsubnet.Properties = New-Object Microsoft.Windows.NetworkController.LogicalSubnetProperties  
      $logicalsubnet.Properties.VlanID = 1001  
      $logicalsubnet.Properties.AddressPrefix = "10.127.134.0/25"  
      $logicalsubnet.Properties.DefaultGateways = "10.127.134.1"  
      
      $lnProperties.Subnets += $logicalsubnet  
      
      # Add the new Logical Network to Network Controller  
      $vlanNetwork = New-NetworkControllerLogicalNetwork -ConnectionUri $uri -ResourceId "Contoso_L3_Network" -Properties $lnProperties -Force  
      
      ```  

   2. 네트워크 연결 JSON 개체를 만들고 네트워크 컨트롤러에 추가 합니다.  
  
      ```PowerShell 
      # Create a new object for the Tenant Network Connection  
      $nwConnectionProperties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties   
      
      # Update the common object properties  
      $nwConnectionProperties.ConnectionType = "L3"   
      $nwConnectionProperties.OutboundKiloBitsPerSecond = 10000   
      $nwConnectionProperties.InboundKiloBitsPerSecond = 10000   
      
      # GRE specific configuration (leave blank for L3)  
      $nwConnectionProperties.GreConfiguration = New-Object Microsoft.Windows.NetworkController.GreConfiguration   
      
      # Update specific properties depending on the Connection Type  
      $nwConnectionProperties.L3Configuration = New-Object Microsoft.Windows.NetworkController.L3Configuration   
      $nwConnectionProperties.L3Configuration.VlanSubnet = $vlanNetwork.properties.Subnets[0]   
      
      $nwConnectionProperties.IPAddresses = @()   
      $localIPAddress = New-Object Microsoft.Windows.NetworkController.CidrIPAddress   
      $localIPAddress.IPAddress = "10.127.134.55"   
      $localIPAddress.PrefixLength = 25   
      $nwConnectionProperties.IPAddresses += $localIPAddress   
      
      $nwConnectionProperties.PeerIPAddresses = @("10.127.134.65")   
      
      # Update the IPv4 Routes that are reachable over the site-to-site VPN Tunnel  
      $nwConnectionProperties.Routes = @()   
      $ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo   
      $ipv4Route.DestinationPrefix = "14.2.20.1/32"   
      $ipv4Route.metric = 10   
      $nwConnectionProperties.Routes += $ipv4Route   
      
      # Add the new Network Connection for the tenant  
      New-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -ResourceId "Contoso_L3GW" -Properties $nwConnectionProperties -Force   
      
      ```  
  
5. 게이트웨이 BGP 라우터로 구성 하 고 네트워크 컨트롤러에 추가 합니다. 
  
   1. 테 넌 트 BGP 라우터를 추가 합니다.  

      ```PowerShell  
      # Create a new object for the Tenant BGP Router  
      $bgpRouterproperties = New-Object Microsoft.Windows.NetworkController.VGwBgpRouterProperties   
      
      # Update the BGP Router properties  
      $bgpRouterproperties.ExtAsNumber = "0.64512"   
      $bgpRouterproperties.RouterId = "192.168.0.2"   
      $bgpRouterproperties.RouterIP = @("192.168.0.2")   
      
      # Add the new BGP Router for the tenant  
      $bgpRouter = New-NetworkControllerVirtualGatewayBgpRouter -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -ResourceId "Contoso_BgpRouter1" -Properties $bgpRouterProperties -Force   
      
      ```  

   2. 이 테 넌 트를 위에서 추가한 사이트 간 VPN 네트워크 연결에 해당 하는 BGP 피어를 추가 합니다.  
  
      ```PowerShell
      # Create a new object for Tenant BGP Peer  
      $bgpPeerProperties = New-Object Microsoft.Windows.NetworkController.VGwBgpPeerProperties   
      
      # Update the BGP Peer properties  
      $bgpPeerProperties.PeerIpAddress = "14.1.10.1"   
      $bgpPeerProperties.AsNumber = 64521   
      $bgpPeerProperties.ExtAsNumber = "0.64521"   
      
      # Add the new BGP Peer for tenant  
      New-NetworkControllerVirtualGatewayBgpPeer -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -BgpRouterName $bgpRouter.ResourceId -ResourceId "Contoso_IPSec_Peer" -Properties $bgpPeerProperties -Force   
      
      ```  

## <a name="optional-step-configure-a-gateway-with-all-three-connection-types-ipsec-gre-l3-and-bgp"></a>(선택적 단계) 모든 세 가지 연결 형식 (IPsec, GRE L3)를 사용 하 여 게이트웨이 구성 및 BGP  
필요에 따라 위의 모든 단계를 결합 하 고 모든 세 가지 연결 옵션을 사용 하 여 테 넌 트 가상 게이트웨이 구성할 수 있습니다.   
  
```PowerShell  
# Create a new Virtual Gateway Properties type object  
$VirtualGWProperties = New-Object Microsoft.Windows.NetworkController.VirtualGatewayProperties  
  
# Update GatewayPool reference  
$VirtualGWProperties.GatewayPools = @()  
$VirtualGWProperties.GatewayPools += $gwPool  
  
# Specify the Virtual Subnet that is to be used for routing between GW and VNET  
$VirtualGWProperties.GatewaySubnets = @()  
$VirtualGWProperties.GatewaySubnets += $RoutingSubnet  
  
# Update some basic properties  
$VirtualGWProperties.RoutingType = "Dynamic"  
  
# Update Network Connection object(s)  
$VirtualGWProperties.NetworkConnections = @()  
  
# IPSec Connection configuration  
$ipSecConnection = New-Object Microsoft.Windows.NetworkController.NetworkConnection  
$ipSecConnection.ResourceId = "Contoso_IPSecGW"  
$ipSecConnection.Properties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties  
$ipSecConnection.Properties.ConnectionType = "IPSec"  
$ipSecConnection.Properties.OutboundKiloBitsPerSecond = 10000  
$ipSecConnection.Properties.InboundKiloBitsPerSecond = 10000  
  
$ipSecConnection.Properties.IpSecConfiguration = New-Object Microsoft.Windows.NetworkController.IpSecConfiguration  
  
$ipSecConnection.Properties.IpSecConfiguration.AuthenticationMethod = "PSK"  
$ipSecConnection.Properties.IpSecConfiguration.SharedSecret = "P@ssw0rd"  
  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode = New-Object Microsoft.Windows.NetworkController.QuickMode  
  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode.PerfectForwardSecrecy = "PFS2048"  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode.AuthenticationTransformationConstant = "SHA256128"  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode.CipherTransformationConstant = "DES3"  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode.SALifeTimeSeconds = 1233  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode.IdleDisconnectSeconds = 500  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode.SALifeTimeKiloBytes = 2000  
  
$ipSecConnection.Properties.IpSecConfiguration.MainMode = New-Object Microsoft.Windows.NetworkController.MainMode  
  
$ipSecConnection.Properties.IpSecConfiguration.MainMode.DiffieHellmanGroup = "Group2"  
$ipSecConnection.Properties.IpSecConfiguration.MainMode.IntegrityAlgorithm = "SHA256"  
$ipSecConnection.Properties.IpSecConfiguration.MainMode.EncryptionAlgorithm = "AES256"  
$ipSecConnection.Properties.IpSecConfiguration.MainMode.SALifeTimeSeconds = 1234  
$ipSecConnection.Properties.IpSecConfiguration.MainMode.SALifeTimeKiloBytes = 2000  
  
$ipSecConnection.Properties.IPAddresses = @()  
$ipSecConnection.Properties.PeerIPAddresses = @()  
  
$ipSecConnection.Properties.Routes = @()  
  
$ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo  
$ipv4Route.DestinationPrefix = "14.1.10.1/32"  
$ipv4Route.metric = 10  
$ipSecConnection.Properties.Routes += $ipv4Route  
  
$ipSecConnection.Properties.DestinationIPAddress = "10.127.134.121"  
  
# GRE Connection configuration  
$greConnection = New-Object Microsoft.Windows.NetworkController.NetworkConnection  
$greConnection.ResourceId = "Contoso_GreGW"  
  
$greConnection.Properties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties  
$greConnection.Properties.ConnectionType = "GRE"  
$greConnection.Properties.OutboundKiloBitsPerSecond = 10000  
$greConnection.Properties.InboundKiloBitsPerSecond = 10000  
  
$greConnection.Properties.GreConfiguration = New-Object Microsoft.Windows.NetworkController.GreConfiguration  
$greConnection.Properties.GreConfiguration.GreKey = 1234  
  
$greConnection.Properties.IPAddresses = @()  
$greConnection.Properties.PeerIPAddresses = @()  
  
$greConnection.Properties.Routes = @()  
  
$ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo  
$ipv4Route.DestinationPrefix = "14.2.20.1/32"  
$ipv4Route.metric = 10  
$greConnection.Properties.Routes += $ipv4Route  
  
$greConnection.Properties.DestinationIPAddress = "10.127.134.122"  
  
$greConnection.Properties.L3Configuration = New-Object Microsoft.Windows.NetworkController.L3Configuration  
  
# L3 Forwarding connection configuration  
$l3Connection = New-Object Microsoft.Windows.NetworkController.NetworkConnection  
$l3Connection.ResourceId = "Contoso_L3GW"  
  
$l3Connection.Properties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties  
$l3Connection.Properties.ConnectionType = "L3"  
$l3Connection.Properties.OutboundKiloBitsPerSecond = 10000  
$l3Connection.Properties.InboundKiloBitsPerSecond = 10000  
  
$l3Connection.Properties.GreConfiguration = New-Object Microsoft.Windows.NetworkController.GreConfiguration  
$l3Connection.Properties.L3Configuration = New-Object Microsoft.Windows.NetworkController.L3Configuration  
$l3Connection.Properties.L3Configuration.VlanSubnet = $vlanNetwork.properties.Subnets[0]  
  
$l3Connection.Properties.IPAddresses = @()  
$localIPAddress = New-Object Microsoft.Windows.NetworkController.CidrIPAddress  
$localIPAddress.IPAddress = "10.127.134.55"  
$localIPAddress.PrefixLength = 25  
$l3Connection.Properties.IPAddresses += $localIPAddress  
  
$l3Connection.Properties.PeerIPAddresses = @("10.127.134.65")  
  
$l3Connection.Properties.Routes = @()  
$ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo  
$ipv4Route.DestinationPrefix = "14.2.20.1/32"  
$ipv4Route.metric = 10  
$l3Connection.Properties.Routes += $ipv4Route  
  
# Update BGP Router Object  
$VirtualGWProperties.BgpRouters = @()  
  
$bgpRouter = New-Object Microsoft.Windows.NetworkController.VGwBgpRouter  
$bgpRouter.ResourceId = "Contoso_BgpRouter1"  
$bgpRouter.Properties = New-Object Microsoft.Windows.NetworkController.VGwBgpRouterProperties  
  
$bgpRouter.Properties.ExtAsNumber = "0.64512"  
$bgpRouter.Properties.RouterId = "192.168.0.2"  
$bgpRouter.Properties.RouterIP = @("192.168.0.2")  
  
$bgpRouter.Properties.BgpPeers = @()  
  
# Create BGP Peer Object(s)  
# BGP Peer for IPSec Connection  
$bgpPeer_IPSec = New-Object Microsoft.Windows.NetworkController.VGwBgpPeer  
$bgpPeer_IPSec.ResourceId = "Contoso_IPSec_Peer"  
  
$bgpPeer_IPSec.Properties = New-Object Microsoft.Windows.NetworkController.VGwBgpPeerProperties  
$bgpPeer_IPSec.Properties.PeerIpAddress = "14.1.10.1"  
$bgpPeer_IPSec.Properties.AsNumber = 64521  
$bgpPeer_IPSec.Properties.ExtAsNumber = "0.64521"  
  
$bgpRouter.Properties.BgpPeers += $bgpPeer_IPSec  
  
# BGP Peer for GRE Connection  
$bgpPeer_Gre = New-Object Microsoft.Windows.NetworkController.VGwBgpPeer  
$bgpPeer_Gre.ResourceId = "Contoso_Gre_Peer"  
  
$bgpPeer_Gre.Properties = New-Object Microsoft.Windows.NetworkController.VGwBgpPeerProperties  
$bgpPeer_Gre.Properties.PeerIpAddress = "14.2.20.1"  
$bgpPeer_Gre.Properties.AsNumber = 64522  
$bgpPeer_Gre.Properties.ExtAsNumber = "0.64522"  
  
$bgpRouter.Properties.BgpPeers += $bgpPeer_Gre  
  
# BGP Peer for L3 Connection  
$bgpPeer_L3 = New-Object Microsoft.Windows.NetworkController.VGwBgpPeer  
$bgpPeer_L3.ResourceId = "Contoso_L3_Peer"  
  
$bgpPeer_L3.Properties = New-Object Microsoft.Windows.NetworkController.VGwBgpPeerProperties  
$bgpPeer_L3.Properties.PeerIpAddress = "14.3.30.1"  
$bgpPeer_L3.Properties.AsNumber = 64523  
$bgpPeer_L3.Properties.ExtAsNumber = "0.64523"  
  
$bgpRouter.Properties.BgpPeers += $bgpPeer_L3  
  
$VirtualGWProperties.BgpRouters += $bgpRouter  
  
# Finally Add the new Virtual Gateway for tenant  
New-NetworkControllerVirtualGateway -ConnectionUri $uri  -ResourceId "Contoso_VirtualGW" -Properties $VirtualGWProperties -Force  
  
```  

## <a name="modify-a-gateway-for-a-virtual-network"></a>가상 네트워크 게이트웨이 수정 합니다.  

  
**구성 요소에 대 한 구성을 검색 하 고 변수에 저장**

```PowerShell  
$nwConnection = Get-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "Contoso_VirtualGW" -ResourceId "Contoso_IPSecGW"  
```  

**필수 속성을 연결 하 고 업데이트 값으로 설정 하려면 변수 구조 탐색**
  
```PowerShell  
$nwConnection.properties.IpSecConfiguration.SharedSecret = "C0mplexP@ssW0rd"  
```  

**네트워크 컨트롤러에서 이전 구성이 대체 하도록 수정 된 구성을 추가 합니다.**
 
```PowerShell  
New-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "Contoso_VirtualGW" -ResourceId $nwConnection.ResourceId -Properties $nwConnection.Properties -Force  
```  


## <a name="remove-a-gateway-from-a-virtual-network"></a>가상 네트워크에서 게이트웨이 제거 합니다. 
개별 게이트웨이 기능 또는 전체 게이트웨이 제거 하려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.  

**네트워크 연결을 제거 합니다.**  
```PowerShell  
Remove-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "Contoso_VirtualGW" -ResourceId "Contoso_IPSecGW" -Force  
```  

**BGP 피어를 제거 합니다.** 
```PowerShell  
Remove-NetworkControllerVirtualGatewayBgpPeer -ConnectionUri $uri -VirtualGatewayId "Contoso_VirtualGW" -BgpRouterName "Contoso_BgpRouter1" -ResourceId "Contoso_IPSec_Peer" -Force  
```  

**BGP 라우터를 제거 합니다.**
```PowerShell  
Remove-NetworkControllerVirtualGatewayBgpRouter -ConnectionUri $uri -VirtualGatewayId "Contoso_VirtualGW" -ResourceId "Contoso_BgpRouter1" -Force  
```

**게이트웨이 제거**  
```PowerShell  
Remove-NetworkControllerVirtualGateway -ConnectionUri $uri -ResourceId "Contoso_VirtualGW" -Force   
```  

---