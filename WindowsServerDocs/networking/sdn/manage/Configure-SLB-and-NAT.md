---
title: 부하 분산 소프트웨어가 부하 분산 구성 및 네트워크 NAT (주소 변환)
description: 이 항목은 관리 테 작업 및 Windows Server 2016에 가상 네트워크 방법에 대해 소프트웨어 네트워킹 정의 가이드 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 73bff8ba-939d-40d8-b1e5-3ba3ed5439c3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7f0393db564061caa0bc8f18b1d623f24749b46c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="configure-the-software-load-balancer-for-load-balancing-and-network-address-translation-nat"></a>부하 분산 소프트웨어가 부하 분산 구성 및 네트워크 NAT (주소 변환)

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목을 사용 하 여 소프트웨어 부하 분산 소프트웨어가 네트워킹 정의 \(SDN\) 사용 하는 방법을 알아보세요 \(SLB\) 아웃 바운드 네트워크 주소 변환 NAT 인바인드 NAT가 제공 하거나 부하 분산 응용 프로그램을 여러 개 사이 있습니다.

이 항목 다음 섹션에 포함 되어 있습니다.

- [소프트웨어 부하 분산 개요](#bkmk_slbover)
- [예: 부하 분산 가상 네트워크에 두 개의 vm 풀에 공개 VIP 만들기](#bkmk_publicvip)
- [예: 사용 SLB 아웃 바운드 nat](#bkmk_obnat)
- [예: 한 네트워크 인터페이스 백 엔드 풀에 추가](#bkmk_backend)
- [예: 부하 분산 소프트웨어가 교통 전달 하기 위해 사용 하 여](#bkmk_forward)

## <a name="bkmk_slbover"></a>소프트웨어 부하 분산 개요

SDN 소프트웨어 부하 분산 \(SLB\) 사용 가능 여부와 네트워크 고성능 응용 프로그램을 제공합니다. 것은 계층 4 \ (TCP, UDP\) 부하 분산 트래픽을 부하 분산 집합에 정의 된 가상 컴퓨터 또는 클라우드 서비스의 정상적인 서비스 인스턴스 사이에서 배포 하는 합니다.

다음을 수행 SLB 구성할 수 있습니다.

* 가상 컴퓨터 \(VMs\) 가상 네트워크에 들어오는 교통 외부 잔액을 로드 합니다. 공용 VIP 부하 분산 라고 합니다.
* 로드 들어오는 교통 가상 네트워크에서 Vm, 클라우드 서비스의 Vm 간에 또는 온-프레미스 컴퓨터와 Vm 간 온-프레미스 가상 네트워크에 잔액 합니다. 
* 앞으로 VM 네트워크 교통 가상 네트워크의 네트워크 NAT (주소 변환)를 사용 하 여 외부 대상으로 합니다.  이 아웃 바운드 NAT. 라고
* 특정 VM 외부 교통을 전달 됩니다.  이 인바인드 NAT. 라고

>[!IMPORTANT]
>알려진된 문제가 Windows Server 2016 5에 제대로 작동 NetworkController Windows PowerShell 모듈에 부하 분산 개체 수 없습니다. 동적 해시 표 및 호출 WebRequest 대신 사용 하는 문제가 해결이 됩니다. 이 방법은 다음 예제에서 보여 줍니다.


## <a name="bkmk_publicvip"></a>예: 부하 분산 가상 네트워크에 두 개의 vm 풀에 공개 VIP 만들기

이 이때 VIP에 요청을 처리 하기 위해 풀 구성원과 공개 VIP와 두 Vm 부하 분산 개체를 만드는 데 사용할 수 있습니다.  또한이 예제 코드 풀 구성원 중 하나 응답 하지 않는 수 있는지 여부를 감지 하 HTTP 건강 검색을 추가 합니다.

###<a name="step-1-prepare-the-load-balancer-object"></a>1 단계: 부하 분산 개체 준비
다음 예제 부하 분산 개체 준비를 사용할 수 있습니다.

    $lbresourceId = "LB2"

    $lbproperties = @{}
    $lbproperties.frontendipconfigurations = @()
    $lbproperties.backendAddressPools = @()
    $lbproperties.probes = @()
    $lbproperties.loadbalancingRules = @()
    $lbproperties.OutboundNatRules = @()

###<a name="step-2-assign-a-front-end-ip"></a>2 단계: 지정 프런트 IP
프런트 IP 일반적으로 라고 가상 IP (VIP)로 합니다.  IP 풀 부하 분산 장치 관리자에 게 이전에 지정 된 논리 네트워크 중 하나를 사용 하지 않는 IP에서 VIP 수행 해야 합니다.

프런트 IP 주소를 지정 하려면 다음 예제를 사용할 수 있습니다.

    $vipip = "10.127.132.5"
    $vipln = get-networkcontrollerlogicalnetwork -ConnectionUri $uri -resourceid "f8f67956-3906-4303-94c5-09cf91e7e311"

    $fe = @{}
    $fe.resourceId = "FE1"
    $fe.resourceRef = "/loadBalancers/$lbresourceId/frontendIPConfigurations/$($fe.resourceId)"
    $fe.properties = @{}
    $fe.properties.subnet = @{}
    $fe.properties.subnet.ResourceRef = $vipln.properties.Subnets[0].ResourceRef
    $fe.properties.privateIPAddress = $vipip
    $fe.properties.privateIPAllocationMethod = "Static"
    $lbproperties.frontendipconfigurations += $fe

###<a name="step-3-allocate-a-backend-address-pool"></a>3 단계: 할당 백 엔드 주소 풀
백 엔드 주소 풀 vm 부하가 설정의 회원 구성 동적 IPs (Dip)를 포함 합니다. 이 단계에서 사용자만 할당 풀; IP 구성 나중에 추가 됩니다.

백 엔드 주소 풀을 할당 다음 예제를 사용할 수 있습니다.
 
    $backend = @{}
    $backend.resourceId = "BE1"
    $backend.resourceRef = "/loadBalancers/$lbresourceId/backendAddressPools/$($backend.resourceId)"
    $lbproperties.backendAddressPools += $backend

###<a name="step-4-define-a-health-probe"></a>4 단계: 정의 건강 검색
건강 조사 부하 분산 백 엔드 풀 회원의 상태를 확인 하려면 사용 됩니다. 이 들어와의 RequestPath에 HTTP 검색 쿼리에 정의 "/ health.htm" 합니다.  쿼리는 IntervalInSeconds 속성을 기준으로 5 초 마다 수행 됩니다.

건강 검사를 고려 백 엔드 IP 정상적인 검색에 대 한 연속 11 쿼리가 대 한 200 HTTP 응답 코드를 받아야 합니다. 부하 분산은 백 엔드 IP, 건강 한 경우에 IP 교통을 보내지 않습니다.

>[!Note]
>이 고 조사에 대해 보내는 위치 때문입니다 중요 한 모든 액세스를 제어 목록 백 엔드 IP 적용할 수 있는 교통 서브넷에서 첫 번째 IP 하거나 차단 하지 않습니다.

이때 건강 검색 정의를 사용할 수 있습니다.
 
    $lbprobe = @{}
    $lbprobe.ResourceId = "Probe1"
    $lbprobe.resourceRef = "/loadBalancers/$lbresourceId/Probes/$($lbprobe.resourceId)"
    $lbprobe.properties = @{}
    $lbprobe.properties.protocol = "HTTP"
    $lbprobe.properties.port = "80"
    $lbprobe.properties.RequestPath = "/health.htm"
    $lbprobe.properties.IntervalInSeconds = 5
    $lbprobe.properties.NumberOfProbes = 11
    $lbproperties.probes += $lbprobe

###<a name="step-5-define-a-load-balancing-rule"></a>5 단계: 정의 부하 분산 규칙
이 부하 분산 규칙 백 엔드 IP에 전송 되어야 합니다 교통 프런트 IP에 도착 하는 방법을 정의 합니다.  여기에서 포트 80 TCP 교통 백 엔드 풀에 전송 됩니다.

다음 예제를 정의할 부하 분산 규칙 사용할 수 있습니다.

    $lbrule = @{}
    $lbrule.ResourceId = "webserver1"
    $lbrule.properties = @{}
    $lbrule.properties.FrontEndIPConfigurations = @()
    $lbrule.properties.FrontEndIPConfigurations += $fe
    $lbrule.properties.backendaddresspool = $backend 
    $lbrule.properties.protocol = "TCP"
    $lbrule.properties.frontendPort = 80
    $lbrule.properties.Probe = $lbprobe
    $lbproperties.loadbalancingRules += $lbrule

###<a name="step-6-add-the-load-balancer-configuration-to-network-controller"></a>6 단계: 네트워크 컨트롤러 부하 분산 구성을 추가합니다
지금까지 여기에서 Windows PowerShell 세션의 메모리에서 모든 만든된 개체 됩니다. 이 단계 개체 네트워크 컨트롤러를 추가 합니다.

네트워크 컨트롤러에 부하 분산 구성을 추가 하려면 다음 예제를 사용할 수 있습니다.

    $lb = @{}
    $lb.ResourceId = $lbresourceid
    $lb.properties = $lbproperties

    $body = convertto-json $lb -Depth 100

    Invoke-WebRequest -Headers @{"Accept"="application/json"} -ContentType "application/json; charset=UTF-8" -Method "Put" -Uri "$uri/Networking/v1/loadbalancers/$lbresourceid" -Body $body -DisableKeepAlive -UseBasicParsing

이 단계를 수행한 후 예제 한 네트워크 인터페이스가 백 엔드 풀에 추가 하려면 다음을 수행 해야 합니다.

## <a name="bkmk_obnat"></a>예: 사용 SLB 아웃 바운드 nat

이 이때 백 엔드 풀 가상 네트워크 개인 주소 공간에서 인터넷에 연결할 vm 아웃 바운드 NAT 기능을 제공 하는 데 사용 하 여 SLB 구성에 사용할 수 있습니다.

###<a name="step-1-create-the-loadbalancer-properties-front-end-ip-and-backend-pool"></a>1 단계: loadbalancer 속성 프런트 IP 및 백 엔드 풀 만들기.
이때 loadbalancer 속성 프런트 IP 및 백 엔드 풀 만들기를 사용할 수 있습니다.

    $lbresourceId = "OutboundNATMembers"
    $vipip = "10.127.132.7"

    $vipln = get-networkcontrollerlogicalnetwork -ConnectionUri $uri -resourceid "f8f67956-3906-4303-94c5-09cf91e7e311"

    $lbproperties = @{}
    $lbproperties.frontendipconfigurations = @()
    $lbproperties.backendAddressPools = @()
    $lbproperties.probes = @()
    $lbproperties.loadbalancingRules = @()
    $lbproperties.OutboundNatRules = @()

    $fe = @{}
    $fe.resourceId = "FE1"
    $fe.resourceRef = "/loadBalancers/$lbresourceId/frontendIPConfigurations/$($fe.resourceId)"
    $fe.properties = @{}
    $fe.properties.subnet = @{}
    $fe.properties.subnet.ResourceRef = $vipln.properties.Subnets[0].ResourceRef
    $fe.properties.privateIPAddress = $vipip
    $fe.properties.privateIPAllocationMethod = "Static"
    $lbproperties.frontendipconfigurations += $fe

    $backend = @{}
    $backend.resourceId = "BE1"
    $backend.resourceRef = "/loadBalancers/$lbresourceId/backendAddressPools/$($backend.resourceId)"
    $lbproperties.backendAddressPools += $backend

###<a name="step-2-define-the-outbound-nat-rule"></a>2 단계: 정의 아웃 바운드 NAT 규칙
이때 아웃 바운드 NAT 규칙 정의를 사용할 수 있습니다. 

    $onat = @{}
    $onat.ResourceId = "onat1"
    $onat.properties = @{}
    $onat.properties.frontendipconfigurations = @()
    $onat.properties.frontendipconfigurations += $fe
    $onat.properties.backendaddresspool = $backend
    $onat.properties.protocol = "ALL"
    $lbproperties.OutboundNatRules += $onat

###<a name="step-3-add-the-load-balancer-object-in-network-controller"></a>3 단계: 부하 분산 개체 네트워크 컨트롤러에서 추가
네트워크 컨트롤러에서 부하 분산 개체를 추가 하려면 다음 예제를 사용할 수 있습니다.

    $lb = @{}
    $lb.ResourceId = $lbresourceid
    $lb.properties = $lbproperties

    $body = convertto-json $lb -Depth 100

    Invoke-WebRequest -Headers @{"Accept"="application/json"} -ContentType "application/json; charset=UTF-8" -Method "Put" -Uri "$uri/Networking/v1/loadbalancers/$lbresourceid" -Body $body -DisableKeepAlive -UseBasicParsing

다음 단계에 인터넷 액세스를 제공 하려는 한 네트워크 인터페이스 추가할 수 있습니다.

## <a name="bkmk_backend"></a>예: 한 네트워크 인터페이스 백 엔드 풀에 추가
네트워크 인터페이스 백 엔드 풀에 추가 하려면이 예제를 사용할 수 있습니다.

이 단계를 처리할 수 있는 네트워크 인터페이스 각에 대 한 요청 VIP을 수행 하는 반복 해야 합니다. 여러 부하 분산 개체에 추가 하는 한 네트워크 인터페이스에이 프로세스를 반복 수도 있습니다. 예를 들어 VIP 웹 서버에 대 한 부하 분산 개체와 아웃 바운드 NAT. 제공 하기 위해 별도 부하 분산 개체 있는 경우
    
### <a name="step-1-get-the-load-balancer-object-containing-the-back-end-pool-to-which-you-will-add-a-network-interface"></a>1 단계: 백 엔드 풀에 추가한 네트워크 인터페이스 포함 된 부하 분산 개체를 다운로드
다음 예제 부하 분산 개체를 검색 사용할 수 있습니다.

    $lbresourceid = "LB2"
    $lb = (Invoke-WebRequest -Headers @{"Accept"="application/json"} -ContentType "application/json; charset=UTF-8" -Method "Get" -Uri "$uri/Networking/v1/loadbalancers/$lbresourceid" -DisableKeepAlive -UseBasicParsing).content | convertfrom-json 

### <a name="step-2-get-the-network-interface-and-add-the-backendaddress-pool-to-the-loadbalancerbackendaddresspools-array"></a>2 단계: 네트워크 인터페이스 가져오고 backendaddress 풀 loadbalancerbackendaddresspools 배열에 추가 합니다.
이때 네트워크 인터페이스 고 loadbalancerbackendaddresspools 배열 backendaddress 풀 추가를 사용할 수 있습니다.

    $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
    $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
    
### <a name="step-3-put-the-network-interface-to-apply-the-change"></a>3 단계: 배치 네트워크 인터페이스는 변경 내용을 적용 하려면
다음 예제 변경 내용을 적용 하려면 네트워크 인터페이스를 사용할 수 있습니다.

    new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06 -properties $nic.properties -force
 
## <a name="bkmk_forward"></a>예: 부하 분산 소프트웨어가 교통 전달 하기 위해 사용 하 여
개별 포트 정의 하지 않고 가상 IP 한 네트워크 인터페이스 가상 네트워크에 매핑하 필요한 경우 l 3 전달 규칙을 만들 수 있습니다.  이 규칙 PublicIPAddress 개체에 포함 되어 있어야 하는 지정 된 VIP 통해 VM에서 모든 교통을 전달 합니다.

같은 서브넷으로 VIP 및 담그고 정의 된 경우 다음 같습니다 NAT. 없이 l 3 전달 수행

>[!NOTE]
>이 프로세스 하지 않아도 부하 분산 개체를 만들 수 있습니다.  해당 구성을 수행 하도록 부하 분산 소프트웨어에 대 한 충분 한 정보는 네트워크 인터페이스에 있는 PublicIPAddress 할당 합니다.

###<a name="step-1-create-a-public-ip-object-to-contain-the-vip"></a>1 단계: VIP 포함 하는 공개 IP 개체 만들기
공용 IP 개체를 만들려면 다음 예제를 사용할 수 있습니다.

    $publicIPProperties = new-object Microsoft.Windows.NetworkController.PublicIpAddressProperties
    $publicIPProperties.ipaddress = "10.127.132.6"
    $publicIPProperties.PublicIPAllocationMethod = "static"
    $publicIPProperties.IdleTimeoutInMinutes = 4
    $publicIP = New-NetworkControllerPublicIpAddress -ResourceId "MyPIP" -Properties $publicIPProperties -ConnectionUri $uri

####<a name="step-2-assign-the-publicipaddress-to-a-network-interface"></a>2 단계: 네트워크 인터페이스에 있는 PublicIPAddress 지정
네트워크 인터페이스에 있는 PublicIPAddress 지정 하려면 다음 예제를 사용할 수 있습니다.

    $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
    $nic.properties.IpConfigurations[0].Properties.PublicIPAddress = $publicIP
    New-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId $nic.ResourceId -Properties $nic.properties



 