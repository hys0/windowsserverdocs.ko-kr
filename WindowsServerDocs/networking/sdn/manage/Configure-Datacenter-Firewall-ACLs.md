---
title: 데이터 센터 방화벽 ACL(액세스 제어 목록) 구성
description: 네트워크 인터페이스에 특정 Acl을 적용할 수 있습니다.  네트워크 인터페이스를 연결할 가상 서브넷에 Acl을 설정할 경우 모두 Acl 적용 되었지만 네트워크 인터페이스 Acl은 가상 서브넷 Acl 보다 우선적으로 수행 합니다.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25f18927-a63e-44f3-b02a-81ed51933187
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 77a7706e39da265eedd65342a0ccf2174ab050ea
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853404"
---
# <a name="configure-datacenter-firewall-access-control-lists-acls"></a>액세스 제어 목록 (Acl) 데이터 센터 방화벽 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

ACL을 생성 하 고 가상 서브넷에 할당 하면, 개별 네트워크 인터페이스에 대 한 특정 ACL 사용 하 여 가상 서브넷에 ACL 기본값을 재정의 하는 것이 좋습니다.  이 경우 가상 네트워크는 대신 Vlan에 연결 된 네트워크 인터페이스에 직접 특정 Acl를 적용 합니다. 네트워크 인터페이스에 연결 된 가상 서브넷을 설정 하는 Acl에 있는 경우에 두 Acl 적용 되 고 네트워크 인터페이스가 가상 서브넷 Acl 위에 Acl 우선 순위를 지정 합니다.

>[!IMPORTANT]
>ACL을 생성 하지 있고 가상 네트워크에 할당 하는 경우 참조 [사용 하 여 액세스 제어 목록 (Acl) 데이터 센터 네트워크 트래픽 흐름을 관리 하려면](Use-Access-Control-Lists--ACLs--to-Manage-Datacenter-Network-Traffic-Flow.md) ACL을 만들고 가상 서브넷에 할당 합니다.  

이 항목에서는 살펴보겠습니다 네트워크 인터페이스에 ACL을 추가 하는 방법. 또한 살펴보겠습니다 Windows PowerShell 및 네트워크 컨트롤러 REST API를 사용 하 여 네트워크 인터페이스에서 ACL을 제거 하는 방법.

- [예: ACL을 네트워크 인터페이스 추가](#example-add-an-acl-to-a-network-interface)
- [예: Windows Powershell 및 네트워크 컨트롤러 REST API를 사용 하 여 네트워크 인터페이스에서 ACL을 제거](#example-remove-an-acl-from-a-network-interface-by-using-windows-powershell-and-the-network-controller-rest-api)


## <a name="example-add-an-acl-to-a-network-interface"></a>예: ACL을 네트워크 인터페이스 추가
이 예제에서는 가상 네트워크에 ACL을 추가 하는 방법에 설명 했습니다. 

>[!TIP]
>도 동시 사용자가 만든 네트워크 인터페이스에 ACL을 추가 하는 것이 가능 합니다.

1. 가져오거나 ACL 추가 하려는 네트워크 인터페이스를 만듭니다.
 
   ```PowerShell
   $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```
 
2. 가져오거나 추가 네트워크 인터페이스에 ACL을 만듭니다.
 
   ```PowerShell
   $acl = get-networkcontrolleraccesscontrollist -ConnectionUri $uri -resourceid "AllowAllACL"
   ```
 
3. ACL을 네트워크 인터페이스의 AccessControlList 속성에 할당
 
   ```PowerShell
    $nic.properties.ipconfigurations[0].properties.AccessControlList = $acl
   ```
 
4. 네트워크 컨트롤러에서 네트워크 인터페이스 추가
 
   ```
   new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid
   ```
 
## <a name="example-remove-an-acl-from-a-network-interface-by-using-windows-powershell-and-the-network-controller-rest-api"></a>예: Windows Powershell 및 네트워크 컨트롤러 REST API를 사용 하 여 네트워크 인터페이스에서 ACL을 제거
이 예에서 살펴보겠습니다 ACL을 제거 하는 방법. ACL을 제거 하는 기본 규칙 집합을 네트워크 인터페이스에 적용 됩니다. 기본 규칙 집합의 모든 아웃 바운드 트래픽을 허용 하지만 모든 인바운드 트래픽을 차단 합니다.

>[!NOTE]
>모든 인바운드 트래픽을 허용 하려는 경우 이전 수행 해야 합니다 [예제에서는](#example-add-an-acl-to-a-network-interface) 모든 인바운드 및 아웃 바운드 모든 트래픽을 허용 하는 ACL을 추가 합니다.


1. 네트워크 인터페이스 제거는 ACL을 가져옵니다.<br>
   ```PowerShell
   $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```
 
2. $NULL을 ipConfiguration의 AccessControlList 속성에 할당 합니다.<br>
   ```PowerShell
   $nic.properties.ipconfigurations[0].properties.AccessControlList = $null
   ```
 
3. 네트워크 컨트롤러에서 네트워크 인터페이스 개체를 추가 합니다.<br>
   ```PowerShell
   new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid
   ```
