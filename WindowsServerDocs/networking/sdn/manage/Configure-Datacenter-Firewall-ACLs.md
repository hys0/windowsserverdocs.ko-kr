---
title: 데이터 센터 방화벽 ACL(액세스 제어 목록) 구성
description: 네트워크 인터페이스에 특정 Acl을 적용할 수 있습니다.  네트워크 인터페이스가 연결 된 가상 서브넷에 Acl도 설정 된 경우 두 Acl이 모두 적용 되지만 네트워크 인터페이스 Acl은 가상 서브넷 Acl 위에 우선 순위가 지정 됩니다.
manager: dougkim
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25f18927-a63e-44f3-b02a-81ed51933187
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 2e3f365a820de67dec87ea209cbfeb22d9091616
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406105"
---
# <a name="configure-datacenter-firewall-access-control-lists-acls"></a>데이터 센터 방화벽 Access Control 목록 (Acl) 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

ACL을 만들고 가상 서브넷에 할당 한 후에는 개별 네트워크 인터페이스에 대 한 특정 ACL을 사용 하 여 가상 서브넷에서 해당 기본 ACL을 재정의할 수 있습니다.  이 경우 가상 네트워크 대신 Vlan에 연결 된 네트워크 인터페이스에 특정 Acl을 직접 적용 합니다. 네트워크 인터페이스에 연결 된 가상 서브넷에 설정 된 Acl이 있는 경우 두 Acl이 적용 되 고 가상 서브넷 Acl 위의 네트워크 인터페이스 Acl에 우선 순위가 적용 됩니다.

>[!IMPORTANT]
>ACL을 만들어 가상 네트워크에 할당 하지 않은 경우 acl [(Access Control 목록)을 사용 하 여 데이터 센터 네트워크 트래픽 흐름 관리](Use-Access-Control-Lists--ACLs--to-Manage-Datacenter-Network-Traffic-Flow.md) 를 참조 하 여 acl을 만들고 가상 서브넷에 할당 합니다.  

이 항목에서는 네트워크 인터페이스에 ACL을 추가 하는 방법을 보여 줍니다. 또한 Windows PowerShell 및 네트워크 컨트롤러 REST API를 사용 하 여 네트워크 인터페이스에서 ACL을 제거 하는 방법을 보여 줍니다.

- [예: 네트워크 인터페이스에 ACL 추가](#example-add-an-acl-to-a-network-interface)
- [예: Windows Powershell 및 네트워크 컨트롤러를 사용 하 여 네트워크 인터페이스에서 ACL을 제거 REST API](#example-remove-an-acl-from-a-network-interface-by-using-windows-powershell-and-the-network-controller-rest-api)


## <a name="example-add-an-acl-to-a-network-interface"></a>예: 네트워크 인터페이스에 ACL 추가
이 예제에서는 가상 네트워크에 ACL을 추가 하는 방법을 보여 줍니다. 

>[!TIP]
>네트워크 인터페이스를 만들 때에도 ACL을 추가할 수 있습니다.

1. ACL을 추가할 네트워크 인터페이스를 가져오거나 만듭니다.
 
   ```PowerShell
   $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```
 
2. 네트워크 인터페이스에 추가할 ACL을 가져오거나 만듭니다.
 
   ```PowerShell
   $acl = get-networkcontrolleraccesscontrollist -ConnectionUri $uri -resourceid "AllowAllACL"
   ```
 
3. 네트워크 인터페이스의 AccessControlList 속성에 ACL을 할당 합니다.
 
   ```PowerShell
    $nic.properties.ipconfigurations[0].properties.AccessControlList = $acl
   ```
 
4. 네트워크 컨트롤러에서 네트워크 인터페이스를 추가 합니다.
 
   ```
   new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid
   ```
 
## <a name="example-remove-an-acl-from-a-network-interface-by-using-windows-powershell-and-the-network-controller-rest-api"></a>예: Windows Powershell 및 네트워크 컨트롤러를 사용 하 여 네트워크 인터페이스에서 ACL을 제거 REST API
이 예제에서는 ACL을 제거 하는 방법을 보여 줍니다. ACL을 제거 하면 기본 규칙 집합이 네트워크 인터페이스에 적용 됩니다. 기본 규칙 집합은 모든 아웃 바운드 트래픽을 허용 하지만 모든 인바운드 트래픽을 차단 합니다.

>[!NOTE]
>모든 인바운드 트래픽을 허용 하려면 이전 [예제](#example-add-an-acl-to-a-network-interface) 를 수행 하 여 모든 인바운드 및 아웃 바운드 트래픽을 허용 하는 ACL을 추가 해야 합니다.


1. ACL을 제거할 네트워크 인터페이스를 가져옵니다.<br>
   ```PowerShell
   $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```
 
2. $NULL를 ipConfiguration의 AccessControlList 속성에 할당 합니다.<br>
   ```PowerShell
   $nic.properties.ipconfigurations[0].properties.AccessControlList = $null
   ```
 
3. 네트워크 컨트롤러에서 네트워크 인터페이스 개체를 추가 합니다.<br>
   ```PowerShell
   new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid
   ```
