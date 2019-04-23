---
title: 만들기, 삭제 또는 테 넌 트 가상 네트워크를 업데이트 합니다.
description: 이 항목의 만들기, 삭제 및 네트워킹 SDN (소프트웨어)를 배포한 후 Hyper-v 네트워크 가상화에 대 한 가상 네트워크를 업데이트 하는 방법을 알아봅니다. Hyper-v 네트워크 가상화는 각 테 넌 트 네트워크 엔터티를 별도 테 넌 트 네트워크를 격리 하도록 도와줍니다. 각 엔터티에 포함 된 공용 액세스 워크 로드를 구성 하지 않는 한 상호 연결 될 가능성이 없습니다.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a820826-e829-4ef2-9a20-f74235f8c25b
ms.author: pashort
author: shortpatti
ms.date: 08/24/2018
ms.openlocfilehash: a125ec220b4769a57a6be30f1425283afb7f0fe6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838354"
---
# <a name="create-delete-or-update-tenant-virtual-networks"></a>테넌트 가상 네트워크 만들기, 삭제 또는 업데이트

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목의 만들기, 삭제 및 네트워킹 SDN (소프트웨어)를 배포한 후 Hyper-v 네트워크 가상화에 대 한 가상 네트워크를 업데이트 하는 방법을 알아봅니다. Hyper-v 네트워크 가상화는 각 테 넌 트 네트워크 엔터티를 별도 테 넌 트 네트워크를 격리 하도록 도와줍니다. 각 엔터티에 포함 된 공용 액세스 워크 로드를 구성 하지 않는 한 상호 연결 될 가능성이 없습니다.   
  
## <a name="create-a-new-virtual-network"></a>새 가상 네트워크 만들기  
테 넌 트에 대 한 가상 네트워크를 만들 Hyper-v 호스트에 고유 라우팅 도메인에 배치 됩니다. 모든 가상 네트워크 아래에 가상 서브넷을 하나 이상 있습니다. 가상 서브넷에 IP 접두사가 정의 가져올 및 이전에 정의 된 ACL을 참조 합니다.  

새 가상 네트워크를 만드는 단계를 다음과 같습니다.

1. 가상 서브넷을 만들려면 원하는 IP 주소 접두사를 식별 합니다.   
2. 테 넌 트 트래픽을 터널링 됩니다 공급자 논리 네트워크를 식별 합니다.   
3. 1 단계에서 식별 된 각 IP 접두사에 대 한 하나 이상의 가상 서브넷을 만듭니다. 
4. (선택 사항) 가상 서브넷에 이전에 만든된 Acl을 추가 하거나 테 넌 트에 대 한 게이트웨이 연결을 추가 합니다. 

다음 표에서 두 가상의 테 넌 트에 대 한 예제에서는 서브넷 Id 및 접두사를 포함합니다. Fabrikam 테 넌 트를 Contoso 테 넌 트에 세 개의 가상 서브넷에 있는 동안 두 가상 서브넷에 있습니다.  
 
  
테 넌 트 이름  |가상 서브넷 ID  |가상 서브넷 접두사    
---------|---------|---------  
Fabrikam    |5001         |24.30.1.0/24           
Fabrikam     |5002         | 24.30.2.0/20          
Contoso    |6001         |  24.30.1.0/24         
Contoso    | 6002        |  24.30.2.0/24         
Contoso     | 6003        | 24.30.3.0/24          
  
다음 예제 스크립트에서 내보낸 Windows PowerShell 명령을 사용 하 여 **NetworkController** 를 Contoso의 가상 네트워크 및 서브넷 1 개를 만들기 위한 모듈:   
  
```Powershell  
import-module networkcontroller  
$URI = "https://ncrest.contoso.local"  
  
#Find the HNV Provider Logical Network  
  
$logicalnetworks = Get-NetworkControllerLogicalNetwork -ConnectionUri $uri  
foreach ($ln in $logicalnetworks) {  
   if ($ln.Properties.NetworkVirtualizationEnabled -eq "True") {  
      $HNVProviderLogicalNetwork = $ln  
   }  
}   
  
#Find the Access Control List to user per virtual subnet  
  
$acllist = Get-NetworkControllerAccessControlList -ConnectionUri $uri -ResourceId "AllowAll"  
  
#Create the Virtual Subnet  
  
$vsubnet = new-object Microsoft.Windows.NetworkController.VirtualSubnet  
$vsubnet.ResourceId = "Contoso_WebTier"  
$vsubnet.Properties = new-object Microsoft.Windows.NetworkController.VirtualSubnetProperties  
$vsubnet.Properties.AccessControlList = $acllist  
$vsubnet.Properties.AddressPrefix = "24.30.1.0/24"  
  
#Create the Virtual Network  
  
$vnetproperties = new-object Microsoft.Windows.NetworkController.VirtualNetworkProperties  
$vnetproperties.AddressSpace = new-object Microsoft.Windows.NetworkController.AddressSpace  
$vnetproperties.AddressSpace.AddressPrefixes = @("24.30.1.0/24")  
$vnetproperties.LogicalNetwork = $HNVProviderLogicalNetwork  
$vnetproperties.Subnets = @($vsubnet)  
New-NetworkControllerVirtualNetwork -ResourceId "Contoso_VNet1" -ConnectionUri $uri -Properties $vnetproperties  
  
```  
  
## <a name="modify-an-existing-virtual-network"></a>기존 가상 네트워크를 수정 합니다.  
기존 가상 서브넷 또는 네트워크를 업데이트 하려면 Windows PowerShell을 사용할 수 있습니다.   
  
동일한 리소스 ID 사용 하 여 네트워크 컨트롤러에 업데이트 된 리소스는 간단히 말해 다음 예제 스크립트를 실행 하면 Contoso 테 넌 트를 해당 가상 네트워크에 새 가상 서브넷 (24.30.2.0/24)을 추가 하려는 경우 또는 Contoso 관리자 다음 스크립트를 사용할 수 있습니다.  
  
```PowerShell  
$acllist = Get-NetworkControllerAccessControlList -ConnectionUri $uri -ResourceId "AllowAll"  
  
$vnet = Get-NetworkControllerVirtualNetwork -ResourceId "Contoso_VNet1" -ConnectionUri $uri  
  
$vnet.properties.AddressSpace.AddressPrefixes += "24.30.2.0/24"  
  
$vsubnet = new-object Microsoft.Windows.NetworkController.VirtualSubnet  
$vsubnet.ResourceId = "Contoso_DBTier"  
$vsubnet.Properties = new-object Microsoft.Windows.NetworkController.VirtualSubnetProperties  
$vsubnet.Properties.AccessControlList = $acllist  
$vsubnet.Properties.AddressPrefix = "24.30.2.0/24"  
  
$vnet.properties.Subnets += $vsubnet  
  
New-NetworkControllerVirtualNetwork -ResourceId "Contoso_VNet1" -ConnectionUri $uri -properties $vnet.properties  
  
```  
  
## <a name="delete-a-virtual-network"></a>가상 네트워크를 삭제 합니다.  
  
가상 네트워크를 삭제 하려면 Windows PowerShell을 사용할 수 있습니다.  
  
다음 Windows PowerShell 예제 리소스 id uri는 HTTP delete를 실행 하 여 테 넌 트를 가상 네트워크를 삭제 합니다.  

```PowerShell  
Remove-NetworkControllerVirtualNetwork -ResourceId "Contoso_Vnet1" -ConnectionUri $uri  
```

