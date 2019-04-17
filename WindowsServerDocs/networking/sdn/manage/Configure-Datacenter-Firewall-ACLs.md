---
title: Datacenter 방화벽 액세스 제어 Acl (목록 구성)
description: 이 항목은 관리 테 작업 및 Windows Server 2016에 가상 네트워크 방법에 대해 소프트웨어 네트워킹 정의 가이드 일부입니다.
manager: brianlic
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
ms.openlocfilehash: d5f7c4baad24a720e073857cb6c835167e5b419b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="configure-datacenter-firewall-access-control-lists-acls"></a>Datacenter 방화벽 액세스 제어 Acl (목록 구성)

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

특정 Acl 한 네트워크 인터페이스를 적용할 수 있습니다.  Acl는 설정 된 경우 네트워크 인터페이스 연결 되어 있는 가상 서브넷에 모두 Acl, 적용 되지만 네트워크 인터페이스 Acl 위에 Acl 가상 서브넷 우선 순위가.

이 항목 다음 섹션에 포함 되어 있습니다.

- [예: 네트워크 인터페이스 ACL 추가](#bkmk_addacl)
- [예: Windows Powershell 및 네트워크 컨트롤러 REST API를 사용 하 여 ACL 네트워크 인터페이스에서 제거](#bkmk_removeacl)

##<a name="bkmk_addacl"></a>예: 네트워크 인터페이스 ACL 추가

항목에 [사용 액세스 제어 (Acl 목록) Datacenter 네트워크 교통 이동 관리](Use-Access-Control-Lists--ACLs--to-Manage-Datacenter-Network-Traffic-Flow.md) ACL 만들고 가상 서브넷으로 지정 하는 방법과 합니다.  그러나 경우에 따라 하려는 경우 해당 기본 ACL 개별 네트워크 인터페이스에 대 한 특정 ACL와 virtaul 서브넷에서 무시 합니다.  가상 네트워크 대신 Vlan에 연결 되어 있는 한 네트워크 인터페이스 직접 Acl 적용 해야 합니다.

이 이때는 ACL 가상 네트워크에 추가 하는 방법을 보여 줍니다. 

>[!NOTE]
>ACL 네트워크 인터페이스 만들 동시에 추가 하는 것도 가능 합니다.

###<a name="step-1-get-or-create-the-network-interface-to-which-you-will-add-the-acl"></a>1 단계: 하거나 ACL 추가할는 있는 네트워크 인터페이스 만들기

    $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"

###<a name="step-2-get-or-create-the-acl-you-will-add-to-the-network-interface"></a>2 단계: 하거나 네트워크 인터페이스에 추가한 ACL 만들기
다운로드 하거나 ACL 만들 명령은 사용할 수 있습니다. 

    $acl = get-networkcontrolleraccesscontrollist -ConnectionUri $uri -resourceid "AllowAllACL"

###<a name="step-3-assign-the-acl-to-the-accesscontrollist-property-of-the-network-interface"></a>3 단계: 네트워크 인터페이스 AccessControlList 속성 ACL 지정
명령은 AccessControlList 속성 ACL 할당을 사용할 수 있습니다.

    $nic.properties.ipconfigurations[0].properties.AccessControlList = $acl

###<a name="step-4-add-the-network-interface-in-network-controller"></a>4 단계: 네트워크 컨트롤러에서 네트워크 인터페이스 추가
네트워크 컨트롤러에서 네트워크 인터페이스를 추가 하려면 다음 예 명령을 사용할 수 있습니다.

    new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid


##<a name="bkmk_removeacl"></a>예: Windows Powershell 및 네트워크 컨트롤러 REST API를 사용 하 여 ACL 네트워크 인터페이스에서 제거
이 이때 ACL 제거 하려는 경우 사용할 수 있습니다. ACL 제거 하면 네트워크 인터페이스 규칙의 기본 설정 적용 됩니다.

규칙의 기본 설정 모든 아웃 바운드 교통 수 있게 하지만 인바인드 교통 모두 차단 합니다.

>[!NOTE]
>모든 인바인드 교통량을 허용 하려는 경우 위 예제 모든 인바인드 및 모두 아웃 바운드 교통 수 있도록 해 주는 ACL 추가를 수행 해야 합니다.

###<a name="step-1-get-the-network-interface-from-which-you-will-remove-the-acl"></a>1 단계: ACL을 분리할 네트워크 인터페이스 다운로드
명령은 네트워크 인터페이스 검색을 사용할 수 있습니다.

    $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"

###<a name="step-2-assign-null-to-the-accesscontrollist-property-of-the-ipconfiguration"></a>2 단계:는 ipConfiguration AccessControlList 속성 $NULL 지정
명령은 AccessControlList 속성 $NULL 할당을 사용할 수 있습니다.

    $nic.properties.ipconfigurations[0].properties.AccessControlList = $null

###<a name="step-3-add-the-network-interface-object-in-network-controller"></a>3 단계: 네트워크 인터페이스 개체 네트워크 컨트롤러에서 추가
다음 예 명령을 사용 하 여 네트워크 인터페이스 개체 네트워크 컨트롤러에 추가 하려면

    new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid

