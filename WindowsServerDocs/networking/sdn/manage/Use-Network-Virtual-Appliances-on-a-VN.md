---
title: 네트워크 가상 장치를 사용 하 여 가상 네트워크에서
description: 이 항목은 관리 테 작업 및 Windows Server 2016에 가상 네트워크 방법에 대해 소프트웨어 네트워킹 정의 가이드 일부입니다.
manager: brianlic
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.assetid: 3c361575-1050-46f4-ac94-fa42102f83c1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: db46189931263d230f013431f319eb2497589dee
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="use-network-virtual-appliances-on-a-virtual-network"></a>네트워크 가상 장치를 사용 하 여 가상 네트워크에서

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

네트워크 가상 장치 테 가상 네트워크에서 배포 하는 방법을 자세히 알아보려면이 항목을 사용할 수 있습니다.

네트워크 가상 기기 사용자 정의 경로 및 기능 미러링 포트 수행 하는 네트워크에 추가할 수 있습니다.

이 항목 다음 섹션에 포함 되어 있습니다.

- [네트워크 가상 장비 유형](#bkmk_types)
- [네트워크 가상 기기 배포](#bkmk_deploy)
- [예: 사용자 정의 경로](#bkmk_routing)
- [예: 포트 미러링](#bkmk_port)

## <a name="bkmk_types"></a>네트워크 가상 장비 유형

두 가지 유형의 가상 네트워크에서 사용할 수 있는 가상 장비는 다음과 같습니다.

1. **사용자 정의 경로**합니다. 사용자 정의 경로 가상 네트워크에서 분산된 라우터를 가상 기기의 라우팅 기능 바꿉니다.  사용자 정의 경로와 가상 기기 가상 네트워크에서 가상 서브넷 사이의 라우터도 사용 됩니다.
2. **포트 미러링**합니다. 포트 미러링와 들어가거나 모니터링된 포트 하는 모든 네트워크 교통 중복 이며 분석을 위해 가상 기기에 전송 합니다. 
## <a name="bkmk_deploy"></a>네트워크 가상 기기 배포

가상 기기를 배포 하는 VM (가상 컴퓨터)는 기기 포함 된 먼저 만든 고 해당 가상 네트워크 서브넷 VM 연결 해야 합니다.

>[!NOTE]
>자세한 내용은 참조 [테 VM 만들고 VLAN 또는 테 가상 네트워크에 연결](Create-a-Tenant-VM.md)

일부 기기 여러 가상 네트워크 어댑터 필요합니다. 일반적으로 네트워크 어댑터는 교통량을 처리 하기 위한 추가 어댑터를 사용 하는 동안 장치 관리에 전념 있습니다. 

기기에 필요한 경우 여러 네트워크 어댑터, 네트워크 컨트롤러에서 각 네트워크 인터페이스를 만들어야 합니다. 

각 서로 다른 가상 서브넷에 추가 어댑터에 대 한 각 호스트 인터페이스 ID을 지정 해야 합니다.

네트워크 가상 기기 배포를 완료 한 후 사용자 정의 경로, 포트 미러링 또는 둘 다에 대 한 기기를 사용할 수 있습니다.

##<a name="bkmk_routing"></a>예: 사용자 정의 경로

대부분의 환경에 대 한 이미 분산 라우터가 가상 네트워크의 정의 시스템 경로만 필요 합니다. 그러나 경로 테이블 만들고와 같은 특정 경우에서 여러 경로 추가 해야 할 수 있습니다.

* 온-프레미스 네트워크를 통해 인터넷에 터널링를 수행 합니다.
* 귀하의 환경의 가상 기기 사용 합니다.

이러한 시나리오 경로 테이블 만들고 사용자 정의 경로 표를 추가 해야 합니다. 여러 경로 테이블 한 경로 테이블 같은 서브넷 하나 이상에 연결 될 수 있습니다. 

각 서브넷만 단일 경로 테이블에 연결할 수 있습니다. 모든 Vm 서브넷에 해당 서브넷 관련 된 경로 표를 사용 합니다.

서브넷 경로 테이블 서브넷에 연결 될 때까지 시스템 경로에 의존 합니다. 연결 존재 경로 기반에 긴 접두사 일치 (LPM) 사용자 정의 경로 및 시스템 경로 중에서 수행 됩니다. 

와 같은 LPM 일치 하는 여러 경로 경우 다음 사용자 정의 경로 먼저 선택-시스템 경로 하기 전에 합니다. 

###<a name="step-1-create-the-route-table-properties"></a>1 단계: 경로 표 속성 만들기

이 경로 테이블 사용자 정의 경로가 모두 포함 됩니다.  시스템 경로 위에 정의 된 규칙에 따라 적용 됩니다.

다음 명령 예 경로 표 속성을 만드는 사용할 수 있습니다.

    $routetableproperties = new-object Microsoft.Windows.NetworkController.RouteTableProperties

###<a name="step-2-add-a-route-to-the-route-table-properties"></a>2 단계: 경로 표 속성을 경로 추가

이 경로 표시 12.0.0.0/8 서브넷 전송 되는 모든 트래픽을 전송 해야 하는 라우팅되지에 192.168.1.10에서 가상 기기 합니다.  것 기기의 한 네트워크 인터페이스에 할당 해당 ip 가상 네트워크에 연결 된 가상 네트워크 어댑터에 중요 합니다.

경로 표 속성을 경로 추가 하려면 다음 예 명령을 사용할 수 있습니다.

    $route = new-object Microsoft.Windows.NetworkController.Route
    $route.ResourceID = "0_0_0_0_0"
    $route.properties = new-object Microsoft.Windows.NetworkController.RouteProperties
    $route.properties.AddressPrefix = "0.0.0.0/0"
    $route.properties.nextHopType = "VirtualAppliance"
    $route.properties.nextHopIpAddress = "192.168.1.10"
    $routetableproperties.routes += $route

각 경로 정의할에 대 한이 단계를 반복 하 여 다른 경로 추가할 수 있습니다.
s
###<a name="step-3-add-the-route-table-to-network-controller"></a>3 단계: 경로 테이블 네트워크 컨트롤러에 추가
네트워크 컨트롤러 경로 표를 추가 하려면 다음 예 명령을 사용할 수 있습니다.

    $routetable = New-NetworkControllerRouteTable -ConnectionUri $uri -ResourceId "Route1" -Properties $routetableproperties

###<a name="step-4-apply-the-route-table-to-the-virtual-subnet"></a>4 단계: 경로 테이블 가상 서브넷 적용
 
경로 테이블 가상 서브넷에 적용 하면 Tenant1_Vnet1 네트워크에 처음 가상 서브넷 경로 표를 사용 합니다. 원하는 만큼 가상 네트워크에서 서브넷 많은을 경로 표를 지정할 수 있습니다.

다음 명령 예 경로 테이블 가상 서브넷을 적용 하 사용할 수 있습니다.

    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"
    $vnet.properties.subnets[0].properties.RouteTable = $routetable
    new-networkcontrollervirtualnetwork -connectionuri $uri -properties $vnet.properties -resourceId $vnet.resourceid

경로 테이블 가상 네트워크에 적용 되는 즉시 교통 가상 기기도 전달 됩니다. 귀하의 환경에 대 한 적절 한 방식으로에서 교통량을 전달 가상 기기의 라우팅 표를 구성 해야 합니다.

##<a name="bkmk_port"></a>예: 포트 미러링

이 이때는 MyVM_Ethernet1의 트래픽 Appliance_Ethernet1 하 고 교통 미러 됩니다 되도록 구성할 수 있습니다.

이 이때 가정 기기도와 미러링를 모니터링 하 고 VM로 Vm 이미 배포 했습니다.

것 미러링를 Appliance_Ethernet1 대상으로 설정한 후 더 이상 받을 수 있는 구성 IP 인터페이스 향하는 교통 때문에 기기에 두 번째 네트워크 인터페이스가 관리에 대 한 중요 합니다.

###<a name="step-1-get-the-virtual-network-on-which-your-vms-are-located"></a>1 단계: Vm 사용자가 있는 가상 네트워크 다운로드
명령은 가상 네트워크를 사용할 수 있습니다.

    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"

###<a name="step-2-get-the-network-controller-network-interfaces-for-the-mirroring-source-and-destination"></a>2 단계: 미러링 소스 및 목적지에 대 한 네트워크 컨트롤러 한 네트워크 인터페이스 다운로드
다음 명령 예 미러링 소스 및 목적지에 대 한 네트워크 컨트롤러 한 네트워크 인터페이스 얻는 사용할 수 있습니다.

    $dstNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "Appliance_Ethernet1"
    $srcNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"

###<a name="step-3-create-a-serviceinsertionproperties-object-to-contain-the-port-mirroring-rules-and-the-element-which-represents-the-destination-interface"></a>3 단계: 규칙과 대상 인터페이스 나타내는 요소 미러링 포트를 포함할 수 serviceinsertionproperties 개체 만들기
다음 명령 예 대상 serviceinsertionproperties 개체를 만들려면 사용할 수 있습니다.

    $portmirror = [Microsoft.Windows.NetworkController.ServiceInsertionProperties]::new()
    $portMirror.Priority = 1

###<a name="step-4-create-a-serviceinsertionrules-object-to-contain-the-rules-that-must-be-matched-in-order-for-the-traffic-to-be-sent-to-the-appliance"></a>4 단계: serviceinsertionrules 개체 기기로 보낼 교통 하기 위해에서 일치 해야 하는 규칙 포함 하도록 만들기

모든 교통, 인바인드 방향과 나가는, 방향 모두 전통적인 미러 나타내는 일치 아래 규칙 정의 됩니다.  이 규칙 미러링 특정 포트 또는 특정 소스/목적지에 관심이 있는 경우 조정할 수 있습니다.

다음 명령 예 serviceinsertionproperties 개체를 만들려면 사용할 수 있습니다.

    $portmirror.ServiceInsertionRules = [Microsoft.Windows.NetworkController.ServiceInsertionRule[]]::new(1)

    $portmirror.ServiceInsertionRules[0] = [Microsoft.Windows.NetworkController.ServiceInsertionRule]::new()
    $portmirror.ServiceInsertionRules[0].ResourceId = "Rule1"
    $portmirror.ServiceInsertionRules[0].Properties = [Microsoft.Windows.NetworkController.ServiceInsertionRuleProperties]::new()

    $portmirror.ServiceInsertionRules[0].Properties.Description = "Port Mirror Rule"
    $portmirror.ServiceInsertionRules[0].Properties.Protocol = "All"
    $portmirror.ServiceInsertionRules[0].Properties.SourcePortRangeStart = "0"
    $portmirror.ServiceInsertionRules[0].Properties.SourcePortRangeEnd = "65535"
    $portmirror.ServiceInsertionRules[0].Properties.DestinationPortRangeStart = "0"
    $portmirror.ServiceInsertionRules[0].Properties.DestinationPortRangeEnd = "65535"
    $portmirror.ServiceInsertionRules[0].Properties.SourceSubnets = "*"
    $portmirror.ServiceInsertionRules[0].Properties.DestinationSubnets = "*"

###<a name="step-5-create-a-serviceinsertionelements-object-to-contain-the-network-interface-of-the-appliance-you-are-mirroring-to"></a>5 단계: serviceinsertionelements 개체를 미러링 기기의 한 네트워크 인터페이스 포함 하도록 만들기
다음 명령 예 네트워크 인터페이스 serviceinsertionelements 개체를 만들려면 사용할 수 있습니다.

    $portmirror.ServiceInsertionElements = [Microsoft.Windows.NetworkController.ServiceInsertionElement[]]::new(1)

    $portmirror.ServiceInsertionElements[0] = [Microsoft.Windows.NetworkController.ServiceInsertionElement]::new()
    $portmirror.ServiceInsertionElements[0].ResourceId = "Element1"
    $portmirror.ServiceInsertionElements[0].Properties = [Microsoft.Windows.NetworkController.ServiceInsertionElementProperties]::new()

    $portmirror.ServiceInsertionElements[0].Properties.Description = "Port Mirror Element"
    $portmirror.ServiceInsertionElements[0].Properties.NetworkInterface = $dstNic
    $portmirror.ServiceInsertionElements[0].Properties.Order = 1

###<a name="step-6-add-the-service-insertion-object-in-network-controller"></a>6 단계: 서비스 삽입 개체 네트워크 컨트롤러에서 추가
이 명령을 모든 교통 기기 네트워크 인터페이스 이전 단계에서 지정 된에 중지 됩니다.

네트워크 컨트롤러에서 서비스 삽입 개체를 추가 하려면 다음 예 명령을 사용할 수 있습니다.

    $portMirror = New-NetworkControllerServiceInsertion -ConnectionUri $uri -Properties $portmirror -ResourceId "MirrorAll"

###<a name="step-7-update-the-network-interface-of-the-source-to-be-mirrored"></a>7 단계: 업데이트 미러링할 소스의 네트워크 인터페이스
다음 명령 예 네트워크 인터페이스 업데이트를 사용할 수 있습니다.

    $srcNic.Properties.IpConfigurations[0].Properties.ServiceInsertion = $portMirror
    $srcNic = New-NetworkControllerNetworkInterface -ConnectionUri $uri  -Properties $srcNic.Properties -ResourceId $srcNic.ResourceId

이러한 단계를 완료 MyVM_Ethernet1 인터페이스에서 교통량 Appliance_Ethernet1 인터페이스 미러 됩니다.
 
