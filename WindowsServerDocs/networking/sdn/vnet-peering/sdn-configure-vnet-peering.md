---
title: 가상 네트워크 피어링 구성
description: 가상 네트워크 피어 링을 구성 하려면 피어 링를 가져오는 두 개의 가상 네트워크를 만들어야 합니다.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 08/08/2018
ms.openlocfilehash: 4d35501b8d876f2a178a4744d495125dea8da6c7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405816"
---
# <a name="configure-virtual-network-peering"></a>가상 네트워크 피어링 구성

>적용 대상: Windows Server

이 절차에서는 Windows PowerShell을 사용 하 여 각각 하나의 서브넷이 있는 두 개의 가상 네트워크를 만듭니다. 그런 다음 두 가상 네트워크 간에 피어 링을 구성 하 여 두 가상 네트워크 간의 연결을 설정 합니다.

- [1단계. 첫 번째 가상 네트워크 만들기](#step-1-create-the-first-virtual-network)

- [2단계. 두 번째 가상 네트워크 만들기](#step-2-create-the-second-virtual-network)

- [3 단계: 첫 번째 가상 네트워크에서 두 번째 가상 네트워크로의 피어 링 구성](#step-3-configure-peering-from-the-first-virtual-network-to-the-second-virtual-network)

- [4단계. 두 번째 가상 네트워크에서 첫 번째 가상 네트워크로의 피어 링 구성](#step-4-configure-peering-from-the-second-virtual-network-to-the-first-virtual-network)


>[!IMPORTANT]
>사용자 환경에 대 한 속성을 업데이트 해야 합니다.

## <a name="step-1-create-the-first-virtual-network"></a>1단계. 첫 번째 가상 네트워크 만들기

이 단계에서는 Windows PowerShell을 사용 하 여 HNV 공급자 논리 네트워크를 찾아 하나의 서브넷이 있는 첫 번째 가상 네트워크를 만듭니다. 다음 예제 스크립트는 하나의 서브넷이 있는 Contoso의 가상 네트워크를 만듭니다.

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

이 단계에서는 하나의 서브넷을 사용 하 여 두 번째 가상 네트워크를 만듭니다. 다음 예제 스크립트는 하나의 서브넷을 사용 하 여 Woodgrove의 가상 네트워크를 만듭니다.

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

## <a name="step-3-configure-peering-from-the-first-virtual-network-to-the-second-virtual-network"></a>3단계. 첫 번째 가상 네트워크에서 두 번째 가상 네트워크로의 피어 링 구성

이 단계에서는 앞의 두 단계에서 만든 첫 번째 가상 네트워크와 두 번째 가상 네트워크 간의 피어 링을 구성 합니다. 다음 예제 스크립트는 **Contoso_vnet1** 에서 **Woodgrove_vnet1**로의 가상 네트워크 피어 링을 설정 합니다.

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
>이 피어 링을 만들면 vnet 상태가 **시작**됨으로 표시 됩니다.

## <a name="step-4-configure-peering-from-the-second-virtual-network-to-the-first-virtual-network"></a>4단계. 두 번째 가상 네트워크에서 첫 번째 가상 네트워크로의 피어 링 구성

이 단계에서는 두 번째 가상 네트워크와 위의 1 단계와 2 단계에서 만든 첫 번째 가상 네트워크 간의 피어 링을 구성 합니다. 다음 예제 스크립트는 **Woodgrove_vnet1** 에서 **Contoso_vnet1**로의 가상 네트워크 피어 링을 설정 합니다.

```PowerShell
$peeringProperties = New-Object Microsoft.Windows.NetworkController.VirtualNetworkPeeringProperties 
$vnet2=Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Contoso_VNet1"
$peeringProperties.remoteVirtualNetwork = $vnet2 

# Indicates whether communication between the two virtual networks is allowed 
$peeringProperties.allowVirtualnetworkAccess = $true 

# Indicates whether forwarded traffic will be allowed across the vnets
$peeringProperties.allowForwardedTraffic = $true 

# Indicates whether the peer virtual network can access this virtual network's gateway
$peeringProperties.allowGatewayTransit = $false 

# Indicates whether this virtual network will use peer virtual network's gateway
$peeringProperties.useRemoteGateways =$false 

New-NetworkControllerVirtualNetworkPeering -ConnectionUri $uri -VirtualNetworkId “Woodgrove_vnet1” -ResourceId “WoodgrovetoContoso” -Properties $peeringProperties 

```

이 피어 링을 만든 후에는 vnet 피어 링 상태가 두 피어에 대해 모두 **연결 됨** 으로 표시 됩니다. 이제 하나의 가상 네트워크에 있는 가상 머신이 피어 링 가상 네트워크의 가상 머신과 통신할 수 있습니다.

---