---
title: 테 넌 트 가상 네트워크 만들기, 삭제 또는 업데이트
description: 이 항목에서는 SDN (소프트웨어 정의 네트워킹)을 배포한 후 Hyper-v 네트워크 가상화 가상 네트워크를 만들고 삭제 하 고 업데이트 하는 방법에 대해 알아봅니다. Hyper-v 네트워크 가상화를 사용 하면 각 테 넌 트 네트워크가 별도의 엔터티가 되도록 테 넌 트 네트워크를 격리할 수 있습니다. 공용 액세스 작업을 구성 하지 않는 한 각 엔터티는 교차 연결 가능성이 없습니다.
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 6a820826-e829-4ef2-9a20-f74235f8c25b
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/24/2018
ms.openlocfilehash: acb663cd33d015c1ce96241abffd4ca260cc5559
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854526"
---
# <a name="create-delete-or-update-tenant-virtual-networks"></a>테넌트 가상 네트워크 만들기, 삭제 또는 업데이트

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 SDN (소프트웨어 정의 네트워킹)을 배포한 후 Hyper-v 네트워크 가상화 가상 네트워크를 만들고 삭제 하 고 업데이트 하는 방법에 대해 알아봅니다. Hyper-v 네트워크 가상화를 사용 하면 각 테 넌 트 네트워크가 별도의 엔터티가 되도록 테 넌 트 네트워크를 격리할 수 있습니다. 공용 액세스 작업을 구성 하지 않는 한 각 엔터티는 교차 연결 가능성이 없습니다.   
  
## <a name="create-a-new-virtual-network"></a>새 가상 네트워크 만들기  
테 넌 트에 대 한 가상 네트워크를 만들면 Hyper-v 호스트의 고유한 라우팅 도메인에 배치 됩니다. 모든 가상 네트워크 아래에는 하나 이상의 가상 서브넷이 있습니다. 가상 서브넷은 IP 접두사로 정의 되며 이전에 정의 된 ACL을 참조 합니다.  

새 가상 네트워크를 만드는 단계는 다음과 같습니다.

1. 가상 서브넷을 만들 IP 주소 접두사를 식별 합니다.   
2. 테 넌 트 트래픽이 터널링 되는 논리 공급자 네트워크를 확인 합니다.   
3. 1 단계에서 확인 한 각 IP 접두사에 대해 하나 이상의 가상 서브넷을 만듭니다. 
4. 필드 이전에 만든 Acl을 가상 서브넷에 추가 하거나 테 넌 트에 대 한 게이트웨이 연결을 추가 합니다. 

다음 표에는 가상의 두 테 넌 트에 대 한 예제 서브넷 Id와 접두사가 포함 되어 있습니다. Fabrikam 테 넌 트에는 두 개의 가상 서브넷이 있고 Contoso 테 넌 트는 3 개의 가상 서브넷을 포함 합니다.  
 
  
테 넌 트 이름  |가상 서브넷 ID  |가상 서브넷 접두사    
---------|---------|---------  
Fabrikam    |5001         |24.30.1.0/24           
Fabrikam     |5002         | 24.30.2.0/20          
Contoso    |6001         |  24.30.1.0/24         
Contoso    | 6002        |  24.30.2.0/24         
Contoso     | 6003        | 24.30.3.0/24          
  
다음 예제 스크립트는 **NetworkController** 모듈에서 내보낸 Windows PowerShell 명령을 사용 하 여 Contoso의 가상 네트워크와 서브넷 하나를 만듭니다.   
  
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
  
## <a name="modify-an-existing-virtual-network"></a>기존 Virtual Network 수정  
Windows PowerShell을 사용 하 여 기존 가상 서브넷 또는 네트워크를 업데이트할 수 있습니다.   
  
다음 예제 스크립트를 실행 하면 업데이트 된 리소스가 동일한 리소스 ID를 가진 네트워크 컨트롤러에 배치 됩니다. 테 넌 트 Contoso가 가상 네트워크에 새 가상 서브넷 (24.30.2.0/24)을 추가 하려는 경우 사용자나 Contoso 관리자는 다음 스크립트를 사용할 수 있습니다.  
  
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
  
## <a name="delete-a-virtual-network"></a>Virtual Network 삭제  
  
Windows PowerShell을 사용 하 여 Virtual Network를 삭제할 수 있습니다.  
  
다음 Windows PowerShell 예에서는 리소스 ID의 URI에 HTTP delete를 실행 하 여 Virtual Network 테 넌 트를 삭제 합니다.  

```PowerShell  
Remove-NetworkControllerVirtualNetwork -ResourceId "Contoso_Vnet1" -ConnectionUri $uri  
```

