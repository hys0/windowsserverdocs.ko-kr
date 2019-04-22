---
title: 가상 네트워크 피어링 구성
description: 가상 네트워크 피어 링 구성 가져오기 피어 링 하는 두 가상 네트워크를 만드는 것입니다.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 08/08/2018
ms.openlocfilehash: 3ef3db879080e3372e7b287dcc55ae052c1fe109
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816394"
---
# <a name="configure-virtual-network-peering"></a>가상 네트워크 피어링 구성

>적용 대상: Windows Server

이 절차에서는 Windows PowerShell를 사용 하 여 하나의 서브넷이 있는 각 두 가상 네트워크를 만들 수 있습니다. 그런 다음 간의 연결을 사용 하도록 설정 하려면 두 가상 네트워크 간에 피어 링 구성 합니다.

- [1 단계입니다. 첫 번째 가상 네트워크 만들기](#step-1-create-the-first-virtual-network)

- [2 단계입니다. 두 번째 가상 네트워크 만들기](#step-2-create-the-second-virtual-network)

- [3 단계: 첫 번째 가상 네트워크에서 두 번째 가상 네트워크로 피어 링 구성](#step-3-configure-peering-from-the-first-virtual-network-to-the-second-virtual-network)

- [4 단계입니다. 두 번째 가상 네트워크에서 첫 번째 가상 네트워크로 피어 링 구성](#step-4-configure-peering-from-the-second-virtual-network-to-the-first-virtual-network)


>[!IMPORTANT]
>사용자 환경에 대 한 속성을 업데이트 해야 합니다.

## <a name="step-1-create-the-first-virtual-network"></a>1단계. 첫 번째 가상 네트워크 만들기

이 단계를 사용 하 여 Windows PowerShell 찾기는 HNV 공급자 논리 네트워크 서브넷 1 개를 사용 하 여 첫 번째 가상 네트워크를 만듭니다. 다음 예제 스크립트는 하나의 서브넷이 있는 Contoso의 가상 네트워크를 만듭니다.

``` PowerShell
#Find the HNV Provider Logical Network  

$logicalnetworks = Get-NetworkControllerLogicalNetwork -ConnectionUri $uri  
foreach ($ln in $logicalnetworks) {  
   if ($ln.Properties.NetworkVirtualizationEnabled -eq "True") {  
      $HNVProviderLogicalNetwork = $ln  
   }  
}   

#Create the Virtual Subnet  

$vsubnet = new-object Microsoft.Windows.NetworkController.VirtualSubnet  
$vsubnet.ResourceId = "Contoso"  
$vsubnet.Properties = new-object Microsoft.Windows.NetworkController.VirtualSubnetProperties  
$vsubnet.Properties.AddressPrefix = "24.30.1.0/24"
$uri=”https://restserver”  

#Create the Virtual Network  

$vnetproperties = new-object Microsoft.Windows.NetworkController.VirtualNetworkProperties  
$vnetproperties.AddressSpace = new-object Microsoft.Windows.NetworkController.AddressSpace  
$vnetproperties.AddressSpace.AddressPrefixes = @("24.30.1.0/24")  
$vnetproperties.LogicalNetwork = $HNVProviderLogicalNetwork  
$vnetproperties.Subnets = @($vsubnet)  
New-NetworkControllerVirtualNetwork -ResourceId "Contoso_VNet1" -ConnectionUri $uri -Properties $vnetproperties
```

## <a name="step-2-create-the-second-virtual-network"></a>2단계. 두 번째 가상 네트워크 만들기

이 단계에서는 하나의 서브넷이 있는 두 번째 가상 네트워크를 만듭니다. 다음 예제 스크립트는 하나의 서브넷이 있는 Woodgrove의 가상 네트워크를 만듭니다.

``` PowerShell

#Create the Virtual Subnet  

$vsubnet = new-object Microsoft.Windows.NetworkController.VirtualSubnet  
$vsubnet.ResourceId = "Woodgrove"  
$vsubnet.Properties = new-object Microsoft.Windows.NetworkController.VirtualSubnetProperties  
$vsubnet.Properties.AddressPrefix = "24.30.2.0/24"  
$uri=”https://restserver”

#Create the Virtual Network  

$vnetproperties = new-object Microsoft.Windows.NetworkController.VirtualNetworkProperties  
$vnetproperties.AddressSpace = new-object Microsoft.Windows.NetworkController.AddressSpace  
$vnetproperties.AddressSpace.AddressPrefixes = @("24.30.2.0/24")  
$vnetproperties.LogicalNetwork = $HNVProviderLogicalNetwork  
$vnetproperties.Subnets = @($vsubnet)  
New-NetworkControllerVirtualNetwork -ResourceId "Woodgrove_VNet1" -ConnectionUri $uri -Properties $vnetproperties
```

## <a name="step-3-configure-peering-from-the-first-virtual-network-to-the-second-virtual-network"></a>3단계. 첫 번째 가상 네트워크에서 두 번째 가상 네트워크로 피어 링 구성

이 단계에서는 첫 번째 가상 네트워크와 앞의 두 단계에서 만든 두 번째 가상 네트워크 간에 피어 링을 구성 합니다. 다음 예제 스크립트에서 가상 네트워크 피어 링 설정 **Contoso_vnet1** 하 **Woodgrove_vnet1**합니다.

```PowerShell
$peeringProperties = New-Object Microsoft.Windows.NetworkController.VirtualNetworkPeeringProperties
$vnet2 = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Woodgrove_VNet1"
$peeringProperties.remoteVirtualNetwork = $vnet2

#Indicate whether communication between the two virtual networks
$peeringProperties.allowVirtualnetworkAccess = $true

#Indicates whether forwarded traffic is allowed across the vnets
$peeringProperties.allowForwardedTraffic = $true

#Indicates whether the peer virtual network can access this virtual networks gateway
$peeringProperties.allowGatewayTransit = $false

#Indicates whether this virtual network uses peer virtual networks gateway
$peeringProperties.useRemoteGateways =$false

New-NetworkControllerVirtualNetworkPeering -ConnectionUri $uri -VirtualNetworkId “Contoso_vnet1” -ResourceId “ContosotoWoodgrove” -Properties $peeringProperties

```

>[!IMPORTANT]
>이 피어 링을 만든 후 vnet 상태를 보여 줍니다 **Initiated**합니다.

## <a name="step-4-configure-peering-from-the-second-virtual-network-to-the-first-virtual-network"></a>4단계. 두 번째 가상 네트워크에서 첫 번째 가상 네트워크로 피어 링 구성

이 단계에서는 두 번째 가상 네트워크와 위의 1, 2 단계에서 만든 첫 번째 가상 네트워크 간에 피어 링을 구성 합니다. 다음 예제 스크립트에서 가상 네트워크 피어 링 설정 **Woodgrove_vnet1** 하 **Contoso_vnet1**합니다.

```PowerShell
$peeringProperties = New-Object Microsoft.Windows.NetworkController.VirtualNetworkPeeringProperties 
$vnet2=Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Contoso_VNet1"
$peeringProperties.remoteVirtualNetwork = $vnet2 

# Indicates whether communication between the two virtual networks is allowed 
$peeringProperties.allowVirtualnetworkAccess = $true 

# Indicates whether forwarded traffic will be allowed across the vnets
$peeringProperties.allowForwardedTraffic = $true 

# Indicates whether the peer virtual network can access this virtual network’s gateway
$peeringProperties.allowGatewayTransit = $false 

# Indicates whether this virtual network will use peer virtual network’s gateway
$peeringProperties.useRemoteGateways =$false 

New-NetworkControllerVirtualNetworkPeering -ConnectionUri $uri -VirtualNetworkId “Woodgrove_vnet1” -ResourceId “WoodgrovetoContoso” -Properties $peeringProperties 

```

상태를 피어 링 vnet이 피어 링을 만든 후 보여 줍니다 **Connected** 두 피어에 대 한 합니다. 이제 가상 컴퓨터에 하나의 가상 네트워크 피어 링된 된 가상 네트워크에서 가상 머신과 통신할 수 있습니다.

---