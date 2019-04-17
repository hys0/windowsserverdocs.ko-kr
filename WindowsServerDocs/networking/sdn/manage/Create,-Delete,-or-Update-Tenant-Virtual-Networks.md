---
title: 만들기, 삭제 또는 테 가상 네트워크 업데이트
description: 이 항목은 관리 테 작업 및 Windows Server 2016에 가상 네트워크 방법에 대해 소프트웨어 네트워킹 정의 가이드 일부입니다.
manager: brianlic
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
ms.openlocfilehash: 6ef30dcc31593e15c36f846cf6d64afcd4b85f19
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="create-delete-or-update-tenant-virtual-networks"></a>만들기, 삭제 또는 테 가상 네트워크 업데이트

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 만들고, 삭제할 Hyper-v 네트워크 가상 네트워크 가상화 소프트웨어 정의 네트워킹 (SDN)를 배포한 후 업데이트 하는 방법을 알아보려면 사용할 수 있습니다.  
  
네트워크 가상화 Hyper-v를 사용 하는 각 테 네트워크 완전히 개별 항목 간 연결 될 가능성이와 공용 액세스 작업 구성 하지 않을 경우 테 네트워크 분리할 수 있습니다.  
  
테 넌에 대 한 새 가상 네트워크 만들 수 없습니다 하 고 기존 가상 네트워크 수정할 수 거주 더 이상 필요 하지 특정 리소스 또는 테는 고객이 더 이상 테 가상 네트워크 삭제할 수 없습니다.  
  
## <a name="create-a-new-virtual-network"></a>새 가상 네트워크 만들기  
  
가상 네트워크 거주에 대 한를 만들 때 Hyper-v 호스트 고유한 라우팅 도메인에 배치 됩니다.  
  
다음은 새 가상 네트워크 생성 하는 단계입니다.  
  
1. 가상 서브넷을 만들려는 IP 주소 접두사를 확인 합니다.   
2. 테 교통 터널링는 논리 공급자 네트워크 사용자의 신원을 확인 합니다.   
3. 하나 이상의 가상 서브넷 접두사 1 단계에서 정의 각 IP에 대 한 만듭니다.   
  
>[!NOTE]  
>모든 가상 네트워크 아래에 하나 이상의 가상 서브넷 합니다. 가상 서브넷 IP 앞으로 정의 되 고 이전에 정의 된 액세스 제어 목록을 참조 합니다.  
  
필요에 따라이 단계를 완료 한 후 가상 서브넷에 이전에 만든된 액세스 제어 목록을 추가 하거나 수도 테 넌 추가 게이트웨이의 연결 합니다.    
  
다음 표에서 예 서브넷 Id 및 접두사 두 가상 테 넌에 대 한 포함 됩니다. 테 Fabrikam Contoso 테에 세 개의 가상 서브넷 동안 두 가상 서브넷에 있습니다.  
  
  
  
테 이름  |가상 서브넷 ID  |가상 서브넷 접두사    
---------|---------|---------  
Fabrikam    |5001         |24.30.1.0/24           
Fabrikam     |5002         | 24.30.2.0/20          
Contoso    |6001         |  24.30.1.0/24         
Contoso    | 6002        |  24.30.2.0/24         
Contoso     | 6003        | 24.30.3.0/24          
  
다음 예제 스크립트 내보낸에서 Windows PowerShell 명령을 사용 하 여는 **NetworkController** 모듈 Contoso의 가상 네트워크와 한 서브넷 만들 수 있습니다.   
  
```  
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
  
## <a name="modify-an-existing-virtual-network"></a>기존 가상 네트워크 수정  
Windows PowerShell 업데이트는 기존 가상 서브넷 또는 네트워크를 사용할 수 있습니다.   
  
업데이트 된 리소스가 동일한 리소스 id 네트워크 컨트롤러 간단히 다음 예제 스크립트를 실행할 때 테 Contoso에는 새 가상 서브넷 (24.30.2.0 월 24 추가 하려고) 하는 경우 해당 가상 네트워크 또는 Contoso 관리자를 사용할 수 다음 스크립트 합니다.  
  
```  
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
  
## <a name="delete-a-virtual-network"></a>가상 네트워크를 삭제  
  
가상 네트워크를 삭제 하려면 Windows PowerShell 사용할 수 있습니다.  
  
다음 Windows PowerShell 예제 테 가상 네트워크 리소스 id uri HTTP 삭제 하 여 삭제  
  
    Remove-NetworkControllerVirtualNetwork -ResourceId "Contoso_Vnet1" -ConnectionUri $uri  


