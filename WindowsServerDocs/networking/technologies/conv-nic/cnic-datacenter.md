---
title: 집약된 NIC 어댑터당된 NIC 구성
description: 이 항목에서 Windows Server 2016 datacenter 구성을 수렴 NIC 구성 하는 방법에 대해 설명 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f01546f8-c495-4055-8492-8806eee99862
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1ac6c2915301b1cf64486f24c197ebbf22bb5e2e
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="converged-nic-teamed-nic-configuration"></a>집약된 NIC 어댑터당된 NIC 구성

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

다음 섹션에서는 수렴 NIC 스위치 Embedded 팀 \(SET\)와 협력 NIC 구성에서 배포 하기 위한 지침입니다. 이 가이드 구성 예에서는 2 Hyper-v 호스트, Hyper-v 호스트 1 및 Hyper-v 호스트 2 보여 줍니다.

## <a name="test-connectivity-between-source-and-destination"></a>원본와 목적지 연결이 테스트

이 섹션 간 원본과 대상 Hyper-v 호스트 연결 테스트 하는 데 필요한 단계를 제공 합니다.

다음 표에 두 Hyper-v 호스트 **Hyper-v 호스트 1** 및 **Hyper-v 호스트 2**합니다. 

모두 Hyper-v 호스트 두 네트워크 어댑터가 있어야 합니다. 각 호스트 한 어댑터 192.168.1.x/24 서브넷에 연결 되어 있고 하나 어댑터가 192.168.2.x/24 서브넷에 연결 되어 있습니다.

![Hyper-v 호스트](../../media/Converged-NIC/1-datacenter-test-conn.jpg)

### <a name="test-nic-connectivity-to-the-hyper-v-virtual-switch"></a>Hyper-v 가상 스위치를 NIC 연결 테스트

이 단계를 사용 하 여 Hyper-v 가상 스위치를 만들 나중에 물리적 NIC 대상 호스트에 연결할 수 있는지 확인할 수 있습니다. 

이 테스트 계층 3 \(L3\)-또는 IP 계층-뿐만 아니라 2 계층 \(L2\) 가상 로컬 영역 네트워크를 사용 하 여 연결을 보여 줍니다 \(VLAN\) 합니다.

네트워크 어댑터의 속성을 가져오려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.

    Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
     
이 명령의 예 결과 다음과 같은 합니다.

|이름|InterfaceDescription|ifIndex|상태|MacAddress|회선 속도|
|-----|--------------------|-------|-----|----------|---------|
|
|테스트 40 G 1|Mellanox ConnectX 3 Pro 이더넷 어댑터|11|위로|E4-1D-2D-07-43-D0|G b 40 p s|

IP 주소를 포함 하 여 추가 어댑터 속성을 가져오려면 뒤 다음 명령을 중 하나를 사용할 수 있습니다.

    Get-NetIPAddress -InterfaceAlias "Test-40G-1"

    Get-NetIPAddress -InterfaceAlias "TEST-40G-1" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress
    
다음은 이러한 명령 예제 결과 합니다.

|매개|값|
|---------|-----|
|
|Ip 주소| 192.168.1.3|
|InterfaceIndex|11|
|InterfaceAlias|테스트 40 G 1|
|AddressFamily|I p v 4|
|입력| 유니캐스트|
|PrefixLength|24|

### <a name="verify-that-nic-team-member-has-a-valid-ip-address"></a>NIC 팀의 구성원에 유효한 IP 주소가 있는지 확인

\(SET\) 스위치 Embedded 팀 멤버 물리적 Nic \(pNICs\)도 유효한 IP 주소가 또는 다른 NIC 팀 되어 있는지 확인 하려면이 단계를 사용할 수 있습니다.

이 단계는 별도 서브넷 사용할 수 있습니다 \ (xxx.xxx.** 2**.xxx vs xxx.xxx 합니다. **1**. xxx\)을 대상으로에서이 어댑터 보내기 쉽게 합니다. 

그렇지 않은 경우 같은 서브넷에 모두 pNICs을 찾았으면 Windows TCP/IP 스택 부하 분산 인터페이스 간에 및 간단한 유효성 검사 더 복잡해 집니다.

네트워크 어댑터가 속성을 가져오려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.

    Get-NetAdapter -Name "Test-40G-2" | ft -AutoSize

이 명령의 예 결과 다음과 같은 합니다.

|이름 |InterfaceDescription |ifIndex |상태 |MacAddress |회선 속도|
|----|--------------------|-------|------|----------|---------|
|
|테스트 40 G 2 |Mellanox ConnectX 3 Pro 이더넷 대답:... \ 2 |13 |위로 |E4-1D-2D-07-40-70 |G b 40 p s|

IP 주소를 포함 하 여 추가 어댑터 속성을 가져오려면 뒤 다음 명령을 중 하나를 사용할 수 있습니다.

    Get-NetIPAddress -InterfaceAlias "Test-40G-2"

    Get-NetIPAddress -InterfaceAlias "Test-40G-2" | Where-Object {$\_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress

다음은 이러한 명령 예제 결과 합니다.

|매개|값|
|---------|-----|
|
|Ip 주소|192.168.2.3|
|InterfaceIndex|13|
|InterfaceAlias|테스트 40 G 2|
|AddressFamily|I p v 4|
|입력|유니캐스트|
|PrefixLength|24|

### <a name="verify-that-additional-nics-have-valid-ip-addresses"></a>추가 Nic 유효한 IP 주소를 받았는지 확인

다른 NIC에서 유효한 IP 주소를 사용 하도록 하려면이 단계를 사용할 수 있습니다.

이 단계는 별도 서브넷 사용할 수 있습니다 \ (xxx.xxx.** 2**.xxx vs xxx.xxx 합니다. **1**. xxx\)을 대상으로에서이 어댑터 보내기 쉽게 합니다. 

그렇지 않은 경우 같은 서브넷에 모두 pNICs을 찾았으면 Windows TCP/IP 스택 부하 분산 인터페이스 간에 및 간단한 유효성 검사 더 복잡해 집니다.

네트워크 어댑터가 속성을 가져오려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.

    Get-NetAdapter -Name "Test-40G-2" | ft -AutoSize

이 명령의 예 결과 다음과 같은 합니다.

|이름 |InterfaceDescription |ifIndex |상태 |MacAddress |회선 속도|
|----|--------------------|-------|------|----------|---------|
|
|테스트 40 G 2 |Mellanox ConnectX 3 Pro 이더넷 대답:... \ 2 |13 |위로 |E4-1D-2D-07-40-70 |G b 40 p s|

IP 주소를 포함 하 여 추가 어댑터 속성을 가져오려면 뒤 다음 명령을 중 하나를 사용할 수 있습니다.
    
    Get-NetIPAddress -InterfaceAlias "Test-40G-2"

    Get-NetIPAddress -InterfaceAlias "Test-40G-2" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress

다음은 이러한 명령 예제 결과 합니다.

|매개|값|
|---------|-----|
|
|Ip 주소|192.168.2.3|
|InterfaceIndex|13|
|InterfaceAlias|테스트 40 G 2|
|AddressFamily|I p v 4|
|입력|유니캐스트|
|PrefixLength|24|

### <a name="ensure-that-source-and-destination-can-communicate"></a>원본과 대상 통신할 수 있는지 확인

이 단계를 사용 하 여 확인 양방향 통신 \ (목적지를 모두 systems\에 반대의 소스에서 ping).  다음 예제에서는 **테스트 NetConnection** Windows PowerShell 명령을 사용 하는 경우 사용할 수 있는 것이 좋습니다 하지만 **ping** 명령을 합니다. 

    Test-NetConnection 192.168.1.5

이 명령의 예 결과 다음과 같은 합니다.

|매개|값|
|---------|-----|
|
|컴퓨터 이름|192.168.1.5|
|RemoteAddress|192.168.1.5|
|InterfaceAlias|테스트 40 G 1|
|원본|192.168.1.3|
|PingSucceeded|False|
|PingReplyDetails \(RTT\)|0 ms|

경우에 따라 성공적으로이 테스트를 수행 하려면이 고급 보안이 포함된 Windows 방화벽 해제 해야 할 수 있습니다. 방화벽을 해제 보안 점을 명심에서 하 고 구성에 조직의 보안 요구 사항을 충족 하는지 확인 합니다.

명령은 모든 방화벽 프로필을 사용 하지 않도록 설정할 수 있습니다.

    Set-NetFirewallProfile -All -Enabled False
    
방화벽을 해제 하면 다음 명령을 연결 테스트를 사용할 수 있습니다.

    Test-NetConnection 192.168.1.5

이 명령의 예 결과 다음과 같은 합니다.

|매개|값|
|---------|-----|
|
|컴퓨터 이름|192.168.1.5|
|RemoteAddress|192.168.1.5|
|InterfaceAlias|테스트 40 G 1|
|원본|192.168.1.3|
|PingSucceeded|False|
|PingReplyDetails \(RTT\)|0 ms|

### <a name="verify-connectivity-for-additional-nics"></a>Nic 추가 대 한 연결을 확인 합니다.

이 단계를 설정 하거나 NIC 팀에 포함 된 모든 이후 pNICs에 대 한 이전 단계를 반복 합니다.

다음 명령을 연결 테스트를 사용할 수 있습니다.
    
    Test-NetConnection 192.168.2.5

이 명령의 예 결과 다음과 같은 합니다.

|매개|값|
|---------|-----|
|
|컴퓨터 이름|192.168.2.5|
|RemoteAddress|192.168.2.5|
|InterfaceAlias|테스트 40 G 2|
|원본|192.168.2.3|
|PingSucceeded|False|
|PingReplyDetails \(RTT\)|0 ms|


## <a name="configure-vlans"></a>Vlan 구성

이 단계는 Nic에는 **액세스** 모드입니다. 그러나 Hyper-v의 가상 스위치 \(vSwitch\) 뒷부분에서를 만들 때 VLAN 속성 vSwitch 포트 수준에 적용 됩니다. 

스위치 여러 Vlan 호스트할 수, 되므로 구성 트렁크 모드에 그 포트를 랙 위에 \(ToR\) 물리적 스위치를 합니다.

트렁크 모드 스위치를 구성 하는 방법에 대 한 지침은 스위치 설명서를 참조 하십시오.

다음 그림 각 있는 VLAN 101 두 네트워크 어댑터와 두 Hyper-v 호스트 보여 주며 VLAN 102 네트워크 어댑터 속성에서 구성 합니다.

![가상 영역 로컬 네트워크 구성](../../media/Converged-NIC/2-datacenter-configure-vlans.jpg)

### <a name="configure-the-vlan-ids-for-both-nics"></a>Nic 둘 다에 대 한 VLAN Id 구성

이 단계 Nic Hyper-v 호스트에 설치 된 용 VLAN Id를 구성할 지를 사용할 수 있습니다.

전기 연구소 및 전자 제품 엔지니어 \(IEEE\) 네트워킹 표준에 따라 서비스 품질 \(QoS\) 속성 물리적에 NIC 활용 하는 802.1 q에 포함 된 802.1 p 헤더 \(VLAN\) 헤더 VLAN ID를 구성 하는 경우

#### <a name="configure-nic-test-40g-1"></a>NIC 테스트 40 G 1 구성

다음 명령을 사용 하 여 VLAN ID 첫 번째 NIC, 테스트-40 G 1, 다음 결과 구성을 보기에 대 한 구성 합니다.

    
    Set-NetAdapterAdvancedProperty -Name "Test-40G-1" -RegistryKeyword VlanID -RegistryValue "101"
    Get-NetAdapterAdvancedProperty -Name "Test-40G-1" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
    
이 명령의 예 결과 다음과 같은 합니다.

|이름 |표시 이름| DisplayValue| RegistryKeyword |RegistryValue|
|----|-----------|------------|---------------|-------------|
|
|테스트 40 G 1|VLAN ID|101|VlanID|{101}|


네트워크 어댑터를 다시 시작 하려면 다음 명령을 사용 하 여 VLAN ID은 독립적으로 네트워크 어댑터 구현 적용 있는지 확인 합니다.

    Restart-NetAdapter -Name "Test-40G-1"

다음 명령을 사용 하 여 네트워크 어댑터 상태 인지 확인 하려면 **위로** 진행 하기 전에 합니다.

    Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize

이 명령의 예 결과 다음과 같은 합니다.

|이름|InterfaceDescription|ifIndex| 상태|MacAddress|회선 속도|
|----|--------------------|-------|------|----------| ---------|
|
|테스트 40 G 1|Pro 이더넷 Mellanox ConnectX 3의...|11|위로|E4-1D-2D-07-43-D0|G b 40 p s|

#### <a name="configure-nic-test-40g-2"></a>구성 NIC 테스트 40 G 2

다음 명령을 사용 하 여 두 번째 NIC, 2 테스트 40 G-, 다음 결과 구성을 보기에 대 한 VLAN ID를 구성 합니다.

    
    Set-NetAdapterAdvancedProperty -Name "Test-40G-2" -RegistryKeyword VlanID -RegistryValue "102"
    Get-NetAdapterAdvancedProperty -Name "Test-40G-2" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
    

이 명령의 예 결과 다음과 같은 합니다.

|이름 |표시 이름| DisplayValue| RegistryKeyword |RegistryValue|
|----|-----------|------------|---------------|-------------|
|
|테스트 40 G 2|VLAN ID|102|VlanID|{102}|

네트워크 어댑터를 다시 시작 하려면 다음 명령을 사용 하 여 VLAN ID은 독립적으로 네트워크 어댑터 구현 적용 있는지 확인 합니다.

`Restart-NetAdapter -Name "Test-40G-2"  `              

다음 명령을 사용 하 여 네트워크 어댑터 상태 인지 확인 하려면 **위로** 진행 하기 전에 합니다.

    Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize

이 명령의 예 결과 다음과 같은 합니다.

|이름|InterfaceDescription|ifIndex| 상태|MacAddress|회선 속도|
|----|--------------------|-------|------|----------| ---------|
|
|테스트 40 G 2 |Pro 이더넷 Mellanox ConnectX 3의... |11 |위로 |E4-1D-2D-07-43-D1 |G b 40 p s|


### <a name="verify-connectivity"></a>연결 상태를 확인합니다

이 섹션 연결을 확인 하려면 네트워크 어댑터를 다시 시작 된 후에 사용할 수 있습니다. 연결 VLAN 태그 두 어댑터에 적용 한 후에 확인할 수 있습니다. 연결이 실패 하는 경우 동일한 VLAN VLAN 구성 또는 대상 참여 스위치를 검사할 수 있습니다. 

>[!IMPORTANT]
>이전 섹션의 단계를 수행한 후 다시 시작 하 고 네트워크에 사용할 수 있게 하는 디바이스에 대 한 몇 초 동안 걸릴 수 있습니다.

#### <a name="verify-connectivity-for-nic-test-40g-1"></a>NIC 테스트-40 G-1에 대 한 연결을 확인

첫 번째 nic 연결을 확인 하려면 다음 명령의 실행할 수 있습니다.

    Test-NetConnection 192.168.1.5
    
이 명령의 예 결과 다음과 같은 합니다.

|매개|값|
|---------|-----|
|
|컴퓨터 이름|192.168.1.5|
|RemoteAddress|192.168.1.5|
|InterfaceAlias|테스트 40 G 1|
|원본|192.168.1.5|
|PingSucceeded|진정한|
|PingReplyDetails \(RTT\)|0 ms|

#### <a name="verify-connectivity-for-nic-test-40g-2"></a>NIC 테스트-40 G-2에 대 한 연결을 확인

이 섹션 NIC 테스트-40 G-2에 대 한 연결 테스트를 사용할 수 있습니다.

다음 명령을 사용 하 여 연결을 테스트 두 번째 대체 합니다.
    
    Test-NetConnection 192.168.2.5
    
이 명령의 예 결과 다음과 같은 합니다.

|매개|값|
|---------|-----|
|
|컴퓨터 이름|192.168.2.5|
|RemoteAddress|192.168.2.5|
|InterfaceAlias|테스트 40 G 2|
|원본|192.168.2.3|
|PingSucceeded|진정한|
|PingReplyDetails \(RTT\)|0 ms|

A **테스트 NetConnection** 오류 또는 ping 오류를 수행한 직후 발생 하는 **다시 NetAdapter** 일반적, 하므로를 완전히 초기화할 네트워크 어댑터에 대 한 기다린 후 다시 시도 합니다.

VLAN 101 연결 문제가 해결 VLAN 102 연결이 작동 하지 않는 경우, 문제 스위치 원하는 VLAN에서 포트 교통 수 있도록 구성 해야 한다는 수 있습니다. 일시적으로 실패 어댑터 VLAN 101 설정 하 고 연결 테스트를 반복 하 여이를 확인할 수 있습니다.

## <a name="configure-quality-of-service-qos"></a>서비스 \(QoS\)의 품질을 구성 합니다.

다음 단계 Windows Server 2016 기능 데이터 센터 브리지 \(DCB\) 처음 설치 해야 하는 서비스 품질 \(QoS\) 구성 하는 것입니다.

다음 그림에서는 성공적으로 Vlan 이전 단계에서 구성 Hyper-v 호스트를 보여 줍니다.

![서비스의 품질을 구성 합니다.](../../media/Converged-NIC/3-datacenter-configure-qos.jpg)

### <a name="install-data-center-bridging-dcb"></a>설치 \(DCB\) 브리지 데이터 센터

설치 하 고 DCB 사용이 단계를 사용할 수 있습니다. 대부분의 경우가이 단계는 iWarp 구현에 대 한 옵션 이지만 간 랙 시나리오 같이 패브릭 크기로 필요 합니다.

다음 명령을 각 Hyper-v 호스트 DCB 설치에 사용할 수 있습니다. 

    Install-WindowsFeature Data-Center-Bridging

이 명령의 예 결과 다음과 같은 합니다.

|성공 |다시 시작 필요 |코드를 종료 합니다.|기능 결과|
|------- |-------------- |--------- |-------------- |
|
|진정한 |아니요 |성공| {데이터 센터 브리지}|

### <a name="set-the-qos-policies-for-smb-direct"></a>직접 SMB QoS 정책 설정 

다음 명령을 SMB 직접 용 QoS 정책을 구성할 지를 사용할 수 있습니다.

    New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3

이 명령의 예 결과 다음과 같은 합니다.

|매개|값|
|---------|-----|
|
|이름 |SMB|
|소유자|그룹 정책 \(Machine\)|
|NetworkProfile|모든|
|우선 순위가|127|
|JobObject|&nbsp;| 
|NetDirectPort|445
|PriorityValue|3

### <a name="set-policies-for-other-traffic-on-the-interface"></a>다른 교통에 대 한 정책을 인터페이스 설정 

다음 명령을 추가 QoS 정책 설정에 사용할 수 있습니다.

    New-NetQosPolicy "DEFAULT" -Default -PriorityValue8021Action 0
 
이 명령의 예 결과 다음과 같은 합니다.

|매개|값|
|---------|-----|
|
|이름 | 기본|
|소유자|그룹 정책 \(Machine\)|
|NetworkProfile|모든|
|우선 순위가|127|
|서식| 기본|
|JobObject| &nbsp;|
|PriorityValue|0|

### <a name="turn-on-flow-control-for-smb"></a>흐름 제어 SMB에 대 한 켜기 

다음 명령을 SMB 흐름 제어를 사용 하도록 설정 하 고 결과를 보려면 사용할 수 있습니다.

    Enable-NetQosFlowControl -priority 3
    Get-NetQosFlowControl

이 명령의 예 결과 다음과 같은 합니다.

|우선 순위 부여|사용 하도록 설정|PolicySet|IfIndex|IfAlias|
|---------|-----|--------- |-------| -------|
|
|0 |False |전 세계|&nbsp;|&nbsp;|
|1 |False |전 세계|&nbsp;|&nbsp;|
|2 |False |전 세계|&nbsp;|&nbsp;|
|3 |진정한 |전 세계|&nbsp;|&nbsp;|
|4 |False |전 세계|&nbsp;|&nbsp;|
|5 |False |전 세계|&nbsp;|&nbsp;|
|6 |False |전 세계|&nbsp;|&nbsp;|
|7 |False |전 세계|&nbsp;|&nbsp;|

결과 3 이외의 항목 진정한의 사용 값 때문에이 결과 일치 하지 않는, 경우 다음 단계를 수행 해야 합니다. 다음을 수행 하지 필요가 결과가 들어 결과물와 일치 하는 경우 항목만 3 참의 사용 값은, 단계를 때까지 아래로 건너뛸 수 **대상 대상 네트워크 어댑터에 대 한 사용 QoS**합니다.

### <a name="ensure-flow-control-is-disabled-for-other-traffic-classes-optional"></a>다른 교통 클래스 \(Optional\) 제어 플로 사용할 수 없게 됩니다 확인

이 단계를 수행 해야 **흐름 제어** 교통 클래스 0,1,2,4,5,6, 및 7 사용할 수 없습니다.

하는 경우 **흐름 제어** 3 아닌 다른 모든 교통 클래스에 이미 설정 되어 \ (0,1,2,4,5,6, 그리고 7\), 사용 하지 않도록 설정 해야 **흐름 제어** 이러한 클래스 합니다. 

>[!NOTE]
>그러나 더 복잡 한 구성에서 다른 교통 클래스이 가이드가 범위를 벗어나는 이러한 시나리오 흐름 제어가 필요할 수 있습니다.

교통 클래스 0,1,2,4,5,6, 및 7 SMB 흐름 제어를 사용 하지 않도록 설정 하 고 결과를 보려면 다음 명령을 사용할 수 있습니다.

    Disable-NetQosFlowControl -priority 0,1,2,4,5,6,7
    Get-NetQosFlowControl

이 명령의 예 결과 다음과 같은 합니다.

|우선 순위 부여|사용 하도록 설정|PolicySet|IfIndex|IfAlias|
|---------|-----|--------- |-------| -------|
|
|0 |False |전 세계|&nbsp;|&nbsp;|
|1 |False |전 세계|&nbsp;|&nbsp;|
|2 |False |전 세계|&nbsp;|&nbsp;|
|3 |진정한 |전 세계|&nbsp;|&nbsp;|
|4 |False |전 세계|&nbsp;|&nbsp;|
|5 |False |전 세계|&nbsp;|&nbsp;|
|6 |False |전 세계|&nbsp;|&nbsp;|
|7 |False |전 세계|&nbsp;|&nbsp;|

### <a name="enable-qos-for-the-local-and-destination-network-adapters"></a>QoS 로컬 대상 네트워크 어댑터에 대 한 사용 하도록 설정 

이 단계를 QoS 로컬와 대상 네트워크 어댑터에 대 한 사용할 수 있습니다. Hyper-v 호스트 둘 다에서 다음이 명령을 실행 하는 있는지 확인 합니다.

#### <a name="enable-qos-for-nic-test-40g-1"></a>NIC 테스트 40 G 1 QoS 사용

다음 명령을 QoS 사용 하도록 설정 하 고 구성에 결과 보기를 사용할 수 있습니다.

    Enable-NetAdapterQos -InterfaceAlias "Test-40G-1"
    Get-NetAdapterQos -Name "Test-40G-1"

이 명령의 예 결과 다음과 같은 합니다.

**이름**: 테스트 40 G 1 **활성화**: 진정한 **기능**:   

|매개|하드웨어|현재|
|---------|--------|-------|
|
|MacSecBypass|NotSupported|NotSupported|
|DcbxSupport|없음|없음|
|NumTCs(Max/ETS/PFC)|8/8/8|8/8/8|
 
**OperationalTrafficClasses**: 

|TC|TSA|대역폭이|우선 순위|
|----|-----|--------|-------|
|
|0| 무과실|&nbsp;|0-7|

**OperationalFlowControl**: 우선 순위 활성화 3 **OperationalClassifications**:

|프로토콜|포트/유형|우선 순위 부여|
|--------|---------|--------|
|
|기본|&nbsp;|0|
|NetDirect| 445|3|

#### <a name="enable-qos-for-nic-test-40g-2"></a>QoS NIC 테스트 40 G 2를 사용 하도록 설정

다음 명령을 QoS 사용 하도록 설정 하 고 구성에 결과 보기를 사용할 수 있습니다.

    Enable-NetAdapterQos -InterfaceAlias "Test-40G-2"
    Get-NetAdapterQos -Name "Test-40G-2"

 
이 명령의 예 결과 다음과 같은 합니다.

**이름**: 테스트 40 G 2 **활성화**: 진정한 **기능**:   

|매개|하드웨어|현재|
|---------|--------|-------|
|
|MacSecBypass|NotSupported|NotSupported|
|DcbxSupport|없음|없음|
|NumTCs(Max/ETS/PFC)|8/8/8|8/8/8|
 
**OperationalTrafficClasses**: 

|TC|TSA|대역폭이|우선 순위|
|----|-----|--------|-------|
|
|0| 무과실|&nbsp;|0-7|

**OperationalFlowControl**: 우선 순위 활성화 3 **OperationalClassifications**:

|프로토콜|포트/유형|우선 순위 부여|
|--------|---------|--------|
|
|기본|&nbsp;|0|
|NetDirect| 445|3|


### <a name="allocate-50-of-the-bandwidth-reservation-to-smb-direct-rdma"></a>50%의 대역폭 예약 SMB 직접 \(RDMA\)에 할당

다음 명령을 SMB 직접 절반 대역폭 예약 할당을 사용할 수 있습니다.

    New-NetQosTrafficClass "SMB" -priority 3 -bandwidthpercentage 50 -algorithm ETS

이 명령의 예 결과 다음과 같은 합니다.

|이름|알고리즘 |Bandwidth(%)| 우선 순위 부여 |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|SMB | ETS     | 50 |3 |전 세계 |&nbsp;|&nbsp;|                                      
 
다음 명령을 대역폭 예약 정보를 사용할 수 있습니다.

    Get-NetQosTrafficClass | ft -AutoSize

이 명령의 예 결과 다음과 같은 합니다.
 
|이름|알고리즘 |Bandwidth(%)| 우선 순위 부여 |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|[기본]| ETS|50 |0-2,4-7|  전 세계|&nbsp;|&nbsp;| 
SMB |ETS|50 |3 |전 세계|&nbsp;|&nbsp;| 

### <a name="create-traffic-classes-for-tenant-ip-traffic-optional"></a>테 IP 교통에 대 한 교통량 클래스 만들기 \(optional\)

테 IP 교통 하기 위한 두 개의 추가 교통 클래스 만드는이 단계를 사용할 수 있습니다. 

예제 뒤 다음 명령을 실행 하면 원하는 경우 "i p 1" 및 "IP2" 값 생략 수 있습니다.

    New-NetQosTrafficClass "IP1" -Priority 1 -bandwidthpercentage 10 -algorithm ETS

이 명령의 예 결과 다음과 같은 합니다.

|이름|알고리즘 |Bandwidth(%)| 우선 순위 부여 |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|I P 1 |ETS |10 |1 |전 세계|&nbsp;|&nbsp;|


    New-NetQosTrafficClass "IP2" -Priority 2 -bandwidthpercentage 10 -algorithm ETS

이 명령의 예 결과 다음과 같은 합니다.

|이름|알고리즘 |Bandwidth(%)| 우선 순위 부여 |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|IP2 |ETS |10 |2 |전 세계|&nbsp;|&nbsp;|

다음 명령을 보려면 QoS 교통 클래스 사용할 수 있습니다.

    Get-NetQosTrafficClass | ft -AutoSize

이 명령의 예 결과 다음과 같은 합니다.

|이름|알고리즘 |Bandwidth(%)| 우선 순위 부여 |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|[기본] |ETS |30 |0,4-7 |전 세계|&nbsp;|&nbsp;|
|SMB |ETS |50 |3 |전 세계|&nbsp;|&nbsp;|
|I P 1 |ETS |10 |1 |전 세계|&nbsp;|&nbsp;|
|IP2 |ETS |10 |2 |전 세계|&nbsp;|&nbsp;|

## <a name="configure-debugger-optional"></a>디버거 \(Optional\) 구성

이 단계 디버거 구성에 사용할 수 있습니다.

기본적으로 연결된 디버거 NetQos 차단합니다. 다음 명령을 디버거 무시 하 고 검색 결과 보기를 사용할 수 있습니다.

    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
    
    Get-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" | ft AllowFlowControlUnderDebugger

이 명령의 예 결과 다음과 같은 합니다.

    AllowFlowControlUnderDebugger
    -----------------------------
    1

## <a name="test-rdma-mode-1"></a>테스트 RDMA \(Mode 1\)

패브릭 vSwitch를 만들고 RDMA \(Mode 2\)로 전환 되는 이전 올바르게 구성 되어 있는지 확인 하려면이 단계를 사용할 수 있습니다.

다음 그림에서는 Hyper-v 호스트 현재 상태를 보여 줍니다.

![테스트 RDMA](../../media/Converged-NIC/4-datacenter-test-rdma.jpg)

RDMA 구성을 확인 하려면 다음 명령의 실행할 수 있습니다.

    Get-NetAdapterRdma | ft -AutoSize

이 명령의 예 결과 다음과 같은 합니다.

|이름 |InterfaceDescription |사용 하도록 설정|
|----|--------------------|-------|
|
|테스트 40 G 1| 4 Mellanox ConnectX VPI 어댑터 2 |진정한|
|테스트 40 G 2| 4 Mellanox ConnectX VPI 어댑터 |진정한|


### <a name="determine-the-ifindex-value-of-your-target-adapter"></a>대상 어댑터의 ifIndex 값을 확인

다음 명령을 대상 어댑터의 ifIndex 값 검색 하는 데 사용할 수 있습니다.

    Get-NetIPConfiguration -InterfaceAlias "TEST*" | ft InterfaceAlias,InterfaceIndex,IPv4Address

이 명령의 예 결과 다음과 같은 합니다.

|InterfaceAlias |InterfaceIndex |IPv4Address|
|-------------- |-------------- |-----------|
|테스트 40 G 1 |14 |{192.168.1.3}|
|테스트 40 G 2 | 13 |{192.168.2.3}|

### <a name="download-diskspdexe-and-a-powershell-script"></a>DiskSpd.exe 및는 PowerShell 스크립트 다운로드

계속 하려면 먼저 다음 항목을 다운로드 해야 합니다.

- DiskSpd.exe 유틸리티를 다운로드 하 고 압축 C:\TEST\에 유틸리티[http://tinyurl.com/z68h3rc](http://tinyurl.com/z68h3rc)

- Test-RDMA powershell 스크립트 C:\TEST\로 다운로드 [https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)

### <a name="run-the-powershell-script"></a>PowerShell 스크립트를 실행합니다

Test-Rdma.ps1 Windows PowerShell 스크립트를 실행할 때와 같은 VLAN에서 원격 어댑터의 IP 주소 스크립트 ifIndex 값을 전달할 수 있습니다.

명령은 스크립트를 실행할 14 ifIndex로 네트워크 어댑터 192.168.1.5에서 사용할 수 있습니다.
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 14 -IsRoCE $true -RemoteIpAddress 192.168.1.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter TEST-40G-1 is a physical adapter
    VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
    VERBOSE: QoS/DCB/PFC configuration is correct.
    VERBOSE: RDMA configuration is correct.
    VERBOSE: Checking if remote IP address, 192.168.1.5, is reachable.
    VERBOSE: Remote IP 192.168.1.5 is reachable.
    VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
    VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 662979201 RDMA bytes written per second
    VERBOSE: 37561021 RDMA bytes sent per second
    VERBOSE: 1023098948 RDMA bytes written per second
    VERBOSE: 8901349 RDMA bytes sent per second
    VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
    VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.1.5
    

>[!NOTE]
>특히, RDMA 교통 실패 RoCE 사례에 대 한 경우에 스위치 구성을 호스트 설정 일치 해야 하는 올바른 PFC/ETS 설정에 대 한 참조 하십시오. 참조 값이 문서의 QoS 섹션을 참조 하세요.

### <a name="determine-the-ifindex-value-of-your-target-adapter"></a>대상 어댑터의 ifIndex 값을 확인

다음 명령을 대상 어댑터의 ifIndex 값 검색 하는 데 사용할 수 있습니다.

    Get-NetIPConfiguration -InterfaceAlias "TEST*" | ft InterfaceAlias,InterfaceIndex,IPv4Address

이 명령의 예 결과 다음과 같은 합니다.

|InterfaceAlias |InterfaceIndex |IPv4Address|
|-------------- |-------------- |-----------|
|테스트 40 G 1 |14 |{192.168.1.3}|
|테스트 40 G 2 | 13 |{192.168.2.3}|

명령은 스크립트를 실행할 13 ifIndex로 네트워크 어댑터 192.168.2.5에서 사용할 수 있습니다.

    
    C:\TEST\Test-RDMA.PS1 -IfIndex 13 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter TEST-40G-2 is a physical adapter
    VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
    VERBOSE: QoS/DCB/PFC configuration is correct.
    VERBOSE: RDMA configuration is correct.
    VERBOSE: Checking if remote IP address, 192.168.2.5, is reachable.
    VERBOSE: Remote IP 192.168.2.5 is reachable.
    VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
    VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 541185606 RDMA bytes written per second
    VERBOSE: 34821478 RDMA bytes sent per second
    VERBOSE: 954717307 RDMA bytes written per second
    VERBOSE: 35040816 RDMA bytes sent per second
    VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
    VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.5
    

## <a name="create-a-hyper-v-virtual-switch"></a>Hyper-v 가상 스위치를 만들기

이 섹션 Hyper-v 호스트의 Hyper-v의 가상 스위치 \(vSwitch\)를 사용할 수 있습니다.

다음 표에 vSwitch를 Hyper-v 호스트 1.

![Hyper-v 가상 스위치를 만들기](../../media/Converged-NIC/5-datacenter-create-vswitch.jpg)

### <a name="create-a-vswitch-in-switch-embedded-teaming-set-mode"></a>스위치 Embedded 팀 \(SET\) 모드로 vSwitch를 만들기

다음 예 명령을 사용 하 여 라는 설정 스위치 독립 팀을 만들 **VMSTEST** Hyper-v 호스트 1. 네트워크 어댑터 테스트 40 G 1과 2로 테스트-40 G-이 컴퓨터에 둘 다이 명령 설정 팀에 추가 됩니다.
    
    New-VMSwitch –Name "VMSTEST" –NetAdapterName "TEST-40G-1","TEST-40G-2" -EnableEmbeddedTeaming $true -AllowManagementOS $true
    
이 명령의 예 결과 다음과 같은 합니다.

|이름 |SwitchType |NetAdapterInterfaceDescription|
|---- |---------- |------------------------------|
|VMSTEST |외부 |협력 인터페이스|

이 명령을 보려면 실제 어댑터 팀 설정에 사용할 수 있습니다.

    Get-VMSwitchTeam -Name "VMSTEST" | fl

이 명령의 예 결과 다음과 같은 합니다.

**이름**: VMSTEST **Id**: ad9bb542-dda2-4450-a00e-f96d44bdfbec **NetAdapterInterfaceDescription**: {Mellanox ConnectX 3 Pro 이더넷 어댑터, Mellanox ConnectX 3 Pro 이더넷 어댑터 2} **TeamingMode**: SwitchIndependent **LoadBalancingAlgorithm**: 동적

#### <a name="display-two-views-of-the-host-vnic"></a>두 가지 호스트 vNIC 보기 표시

다음과 같은 두 가지 명령 호스트 vNIC의 두 가지 보기를 사용할 수 있습니다.

이 명령을 호스트 vNIC의 속성을 표시 사용할 수 있습니다.

    Get-NetAdapter

이 명령의 예 결과 다음과 같은 합니다.

| 이름 | InterfaceDescription | ifIndex | 상태 | MacAddress | 회선 속도 | |------|---|---|---|---| | | (VMSTEST) vEthernet | Hyper-V 가상 이더넷 어댑터 2 | 28 | 위로 | G b E4-1D-2D-07-40-71|80 p s |

이 명령을 호스트 vNIC의 추가 속성을 표시 하려면 사용할 수 있습니다.

    Get-VMNetworkAdapter -ManagementOS

이 명령의 예 결과 다음과 같은 합니다.

|이름 |IsManagementOs |VMName |SwitchName |MacAddress |상태 |IPAddresses|
|----|--------------|------|----------|----------|------|-----------|
|
|VMSTEST|진정한 |VMSTEST |E41D2D074071| {확인}|&nbsp;|

#### <a name="test-the-network-connection-to-the-remote-vlan-101-adapter"></a>원격 VLAN 101 어댑터 네트워크 연결이 테스트

이 명령을 원격 VLAN 101 어댑터에 대 한 연결 테스트를 사용할 수 있습니다.

`Test-NetConnection 192.168.1.5` 

이 명령의 예 결과 다음과 같은 합니다.

    WARNING: Ping to 192.168.1.5 failed -- Status: DestinationHostUnreachable
    
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (CORP-External-Switch)
    SourceAddress  : 10.199.48.170
    PingSucceeded  : False
    PingReplyDetails (RTT) : 0 ms
    
### <a name="reconfigure-vlans"></a>다시 구성 Vlan

액세스 VLAN 설정을 실제 NIC에서 제거 하 고 하 고 vSwitch를 사용 하 여 VLANID 설정이 단계를 사용할 수 있습니다.

액세스 VLAN 설정을 모두 자동-태그 잘못 VLAN id 송신 교통 방지 제거 하 고 수신 필터링에서 액세스 VLAN ID 맞지 교통 해야

다음 명령을 액세스 VLAN 설정을 제거를 사용할 수 있습니다.
    
    Set-NetAdapterAdvancedProperty -Name "Test-40G-1" -RegistryKeyword VlanID -RegistryValue "0"
    Set-NetAdapterAdvancedProperty -Name "Test-40G-2" -RegistryKeyword VlanID -RegistryValue "0"
    

이 작업 결과를 확인 하 고 vSwitch 특정 Windows PowerShell 명령을 사용 하 여 VLANID 설정 하려면 뒤 다음 명령을 사용할 수 있습니다.

    
    Set-VMNetworkAdapterVlan -VMNetworkAdapterName "VMSTEST" -VlanId "101" -Access -ManagementOS
    Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName "VMSTEST"
    

이 명령의 예 결과 다음과 같은 합니다.

VMName VMNetworkAdapterName 모드 VlanList
------ -------------------- ----   --------
       VMSTEST              Access 101     

네트워크 연결을 테스트 하 고 결과 확인 하려면 다음 명령을 사용할 수 있습니다.

    Test-NetConnection 192.168.1.5
    
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (VMSTEST)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    

결과가 들어 결과 유사한 되며 ping 메시지와 함께 실패 하는 경우 "경고: 실패 했습니다 Ping 192.168.1.5를-상태: DestinationHostUnreachable," 다음 명령을 실행 하 여 "(VMSTEST) vEthernet"에 적절 한 IP 주소가 있는지 확인 합니다.

    
    Get-NetIPAddress -InterfaceAlias "vEthernet (VMSTEST)"
    

IP 주소를 설정 하지 않은 경우 문제를 해결 하 고 이러한 작업 결과 보려면 다음 명령을 사용할 수 있습니다.

    
    New-NetIPAddress -InterfaceAlias "vEthernet (VMSTEST)" -IPAddress 192.168.1.3 -PrefixLength 24
    
    IPAddress : 192.168.1.3
    InterfaceIndex: 37
    InterfaceAlias: vEthernet (VMSTEST)
    AddressFamily : IPv4
    Type  : Unicast
    PrefixLength  : 24
    PrefixOrigin  : Manual
    SuffixOrigin  : Manual
    AddressState  : Tentative
    ValidLifetime : Infinite ([TimeSpan]::MaxValue)
    PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
    SkipAsSource  : False
    PolicyStore   : ActiveStore
    
#### <a name="rename-the-management-nic"></a>NIC 관리 이름 바꾸기

이 섹션 관리 NIC 이름을 바꾸려면 사용할 수 있으며 나중에 RDMA에 대 한 별도 호스트 vNIC 인스턴스를 사용 하 여.

다음 명령을 관리 NIC 바꾸고 볼 몇 가지 NIC 속성을 실행할 수 있습니다.

    Rename-VMNetworkAdapter -ManagementOS -Name “VMSTEST” -NewName “MGT”
    Get-VMNetworkAdapter -ManagementOS

이 명령의 예 결과 다음과 같은 합니다.

|이름 |IsManagementOs |VMName |SwitchName |MacAddress |상태 |IPAddresses
|----|--------------|------|----------|----------|------|-----------|
|
|CORP 외부 전환 |진정한 |&nbsp;|CORP 외부 전환 |001B785768AA |{확인}|&nbsp;|
|MGT |진정한 |&nbsp;|VMSTEST |E41D2D074071 |{확인}|&nbsp;|

다음 명령을 볼 몇 가지 추가 NIC 속성을 실행할 수 있습니다.

    Get-NetAdapter

이 명령의 예 결과 다음과 같은 합니다.

|이름 |InterfaceDescription |ifIndex |상태 |MacAddress |회선 속도|
|----|--------------------|------|----------|---------|------|
|
|vEthernet (MGT) |Hyper-v 가상 이더넷 어댑터 2 |28 |위로 | E4-1D-2D-07-40-71 |G b 80 p s|

## <a name="test-hyper-v-virtual-switch-rdma"></a>Hyper-v 가상 스위치 RDMA 테스트

다음 그림에서는 Hyper-v 호스트, Hyper-v 호스트 1 vSwitch를 포함 하 여 현재 상태를 보여 줍니다.

![Hyper-v 가상 스위치를 테스트 합니다.](../../media/Converged-NIC/6-datacenter-test-vswitch-rdma.jpg)

### <a name="set-priority-tagging-on-the-host-vnic-to-complement-the-previous-vlan-settings"></a>우선 순위 부여 호스트 vNIC에 태그를 이전 VLAN 설정 보충 설정

호스트 vNIC에 태그 우선 순위를 설정 하 고 이러한 작업 결과 보려면 다음 예 명령을 사용할 수 있습니다.
    
    Set-VMNetworkAdapter -ManagementOS -Name "MGT" -IeeePriorityTag on
    Get-VMNetworkAdapter -ManagementOS -Name "MGT" | fl Name,IeeePriorityTag
    

    Name: MGT
    IeeePriorityTag : On
    
### <a name="create-two-host-vnics-for-rdma"></a>두 개의 호스트 vNICs RDMA 만들려면

다음 명령 예 RDMA에 대 한 두 가지 호스트 vNICs 만들고 VMSTEST vSwitch에 연결 하 사용할 수 있습니다.
    
    Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB1 –ManagementOS
    Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB2 –ManagementOS
    
관리 NIC 속성을 보려면 다음 예 명령을 사용할 수 있습니다.
    
    Get-VMNetworkAdapter -ManagementOS
    
이 명령의 예 결과 다음과 같은 합니다.

|이름 |IsManagementOs |VMName |SwitchName |MacAddress |상태 |IPAddresses|
|----|--------------|------|----------|----------|------|-----------|
|
|CORP 외부 전환 |진정한 |CORP 외부 전환 |001B785768AA|{확인} |&nbsp;| 
|Mgt |진정한 |VMSTEST |E41D2D074071 |{확인} |&nbsp;|
|SMB1 |진정한 |VMSTEST |00155D30AA00 |{확인} |&nbsp;|
|SMB2 |진정한 |VMSTEST |00155D30AA01 |{확인} |&nbsp;|

### <a name="assign-an-ip-address-to-the-smb-host-vnics"></a>SMB 호스트 vNICs에 IP 주소를 지정 합니다.

이 섹션을 사용 하 여 IP addressrd SMB 호스트 vNICs vEthernet에 할당 \(SMB1\) 및 vEthernet \(SMB2\) 합니다.

테스트 40 G 1 및 테스트 40 G 2 실제 어댑터 101 및 구성 102 액세스 VLAN 되지 않았습니다. 이 인해 어댑터 태그 교통-및 ping에 성공 하면 됩니다.

이전에 0 모두 pNIC VLAN Id 구성 다음 VMSTEST vSwitch VLAN 101로 설정 합니다. 그런 다음 여전히 MGT vNIC를 사용 하 여 원격 VLAN 101 어댑터 ping 할 수는 있지만 현재 VLAN 102 구성원이 있습니다.

이제 다음 예 명령을 사용 하 여 실제 NIC 두 자동-태그 잘못 VLAN id 송신 교통 하지 못하도록 하 고 수신 교통 필터링를 방지 하려면에서 액세스 VLAN 설정을 제거 하려면 액세스 VLAN ID 일치 하지 않은

(SMB1) vEthernet 인터페이스를 새로 IP 주소를 추가 하 여 이러한 목표를 달성 하는 다음 예제 명령을 사용 하 고 결과 볼 수 있습니다.

    
    New-NetIPAddress -InterfaceAlias "vEthernet (SMB1)" -IPAddress 192.168.2.111 -PrefixLength 24
    
    IPAddress : 192.168.2.111
    InterfaceIndex: 40
    InterfaceAlias: vEthernet (SMB1)
    AddressFamily : IPv4
    Type  : Unicast
    PrefixLength  : 24
    PrefixOrigin  : Manual
    SuffixOrigin  : Manual
    AddressState  : Invalid
    ValidLifetime : Infinite ([TimeSpan]::MaxValue)
    PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
    SkipAsSource  : False
    PolicyStore   : PersistentStore
    

원격 VLAN 102 어댑터를 테스트 하 고 검색 결과 보는 명령은 사용할 수 있습니다.
    
    Test-NetConnection 192.168.2.5 
    
    ComputerName   : 192.168.2.5
    RemoteAddress  : 192.168.2.5
    InterfaceAlias : vEthernet (SMB1)
    SourceAddress  : 192.168.2.111
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    
다음 예 명령을 사용 하 여 새 인터페이스 vEthernet IP 주소를 추가 하려면 \(SMB2\), 결과 확인 하 고 있습니다.
    
    New-NetIPAddress -InterfaceAlias "vEthernet (SMB2)" -IPAddress 192.168.2.222 -PrefixLength 24 
    
    IPAddress : 192.168.2.222
    InterfaceIndex: 44
    InterfaceAlias: vEthernet (SMB2)
    AddressFamily : IPv4
    Type  : Unicast
    PrefixLength  : 24
    PrefixOrigin  : Manual
    SuffixOrigin  : Manual
    AddressState  : Invalid
    ValidLifetime : Infinite ([TimeSpan]::MaxValue)
    PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
    SkipAsSource  : False
    PolicyStore   : PersistentStore
    
통신이 설정 때문에 다시 연결 테스트 필요가 없습니다.

### <a name="place-the-rdma-host-vnics-on-vlan-102"></a>장소 VLAN 102에도 RDMA 호스트 vNICs

이 섹션 RDMA 호스트 vNICs VLAN 102에 할당을 사용할 수 있습니다.

"MGT" 호스트 vNIC VLAN 101에 있으므로 RDMA 호스트 vNICs 기존 VLAN 102에 배치 하 고 이러한 작업 결과 확인 하려면 다음 예 명령을 사용할 수 있습니다.

    
    Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB1" -VlanId "102" -Access -ManagementOS
    Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB2" -VlanId "102" -Access -ManagementOS
    
    Get-VMNetworkAdapterVlan -ManagementOS
    
    VMName VMNetworkAdapterName Mode VlanList
    ------ -------------------- ---- --------
       SMB1 Access   102 
       Mgt  Access   101 
       SMB2 Access   102 
       CORP-External-Switch Untagged
    
### <a name="inspect-the-mapping-of-smb1-and-smb2-to-the-underlying-physical-nics"></a>SMB1의 매핑와 기본 실제 Nic에 SMB2 검사

이 섹션 SMB1 및 기본 물리적 Nic 팀 설정 vSwitch 아래에 SMB2 매핑 검사를 사용할 수 있습니다.  실제 Nic에 호스트 vNIC 연결이 임의 및 작성 및 소멸 중에 재조정 따릅니다.

이 경우 현재 연결을 확인 하려면 간접 메커니즘을 사용할 수 있습니다.

SMB1 및 SMB2의 MAC 주소 테스트 40 G 2 NIC 팀 멤버와 연결 되어 있습니다. 테스트 40 G 1 관련된 SMB 호스트 vNIC, 없고에서는 RDMA 교통 활용에 대 한 링크를 통해 SMB 호스트 vNIC 매핑됩니다 될 때까지 하기 때문에 하지 이상적입니다.

이 정보를 보려면 다음 예 명령을 사용할 수 있습니다.

    
    Get-NetAdapterVPort (Preferred)
    
    Get-NetAdapterVmqQueue
    
    Name   QueueID MacAddressVlanID Processor VmFriendlyName
    ----   ------- ---------------- --------- --------------
    TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
    TEST-40G-2 1   00-15-5D-30-AA-00 1020:17
    TEST-40G-2 2   00-15-5D-30-AA-01 1020:17
    
    Get-VMNetworkAdapter -ManagementOS
    
    Name IsManagementOs VMName SwitchName   MacAddress   Status IPAddresses
    ---- -------------- ------ ----------   ----------   ------ -----------
    CORP-External-Switch True  CORP-External-Switch 001B785768AA {Ok}  
    Mgt  True  VMSTEST  E41D2D074071 {Ok}  
    SMB1 True  VMSTEST  00155D30AA00 {Ok}  
    SMB2 True  VMSTEST  00155D30AA01 {Ok}  
    

지도 수행 하지 않은 때문에 모두 명령 아래 정보는 없음 반환 해야 합니다.
    
    Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB1
    Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB2
    
다음 명령 예 SMB1 및 SMB2 물리적 NIC 팀원을 분리 하 고 이러한 작업 결과를 보려면 지도를 사용할 수 있습니다.

>[!IMPORTANT]
>계속 하기 전에이 단계를 완료 또는 구현 못합니다 있는지 확인 합니다.
    
    Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB1" -PhysicalNetAdapterName "Test-40G-1"
    Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB2" -PhysicalNetAdapterName "Test-40G-2"
    
    Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST
    
    NetAdapterName : Test-40G-1
    NetAdapterDeviceId : {BAA9A00F-A844-4740-AA93-6BD838F8CFBA}
    ParentAdapter  : VMInternalNetworkAdapter, Name = 'SMB1'
    IsTemplate : False
    CimSession : CimSession: .
    ComputerName   : 27-3145G0803
    IsDeleted  : False
    
    NetAdapterName : Test-40G-2
    NetAdapterDeviceId : {B7AB5BB3-8ACB-444B-8B7E-BC882935EBC8}
    ParentAdapter  : VMInternalNetworkAdapter, Name = 'SMB2'
    IsTemplate : False
    CimSession : CimSession: .
    ComputerName   : 27-3145G0803
    IsDeleted  : False
    
### <a name="confirm-the-mac-associations"></a>MAC 연결 확인

이전에 만든 MAC 연결을 확인 하려면 다음 예 명령을 사용할 수 있습니다.
    
    Get-NetAdapterVmqQueue
    
    Name   QueueID MacAddressVlanID Processor VmFriendlyName
    ----   ------- ---------------- --------- --------------
    TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
    TEST-40G-1 2   00-15-5D-30-AA-00 1020:17
    TEST-40G-2 1   00-15-5D-30-AA-01 1020:17
    

모두 호스트 vNICs 같은 서브넷에 거주 하 고 동일한 VLAN ID \(102\), 원격 시스템에서 통신의 유효성을 검사 하 고 이러한 작업 결과 볼 수 있습니다.

>[!IMPORTANT]
>원격 컴퓨터에서 다음 명령을 실행 합니다.

    
    Test-NetConnection 192.168.2.111
    
    
    ComputerName   : 192.168.2.111
    RemoteAddress  : 192.168.2.111
    InterfaceAlias : Test-40G-2
    SourceAddress  : 192.168.2.5
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    
    Test-NetConnection 192.168.2.222
    
    ComputerName   : 192.168.2.222
    RemoteAddress  : 192.168.2.222
    InterfaceAlias : Test-40G-2
    SourceAddress  : 192.168.2.5
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms 
    
        
    Set-VMNetworkAdapter -ManagementOS -Name "SMB1" -IeeePriorityTag on
    Set-VMNetworkAdapter -ManagementOS -Name "SMB2" -IeeePriorityTag on
    Get-VMNetworkAdapter -ManagementOS -Name "SMB*" | fl Name,SwitchName,IeeePriorityTag,Status
    
    Name: SMB1
    SwitchName  : VMSTEST
    IeeePriorityTag : On
    Status  : {Ok}
    
    Name: SMB2
    SwitchName  : VMSTEST
    IeeePriorityTag : On
    Status  : {Ok}
    

    Get-NetAdapterRdma -Name "vEthernet*" | sort Name | ft -AutoSize
    
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  False  
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  False  
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False   
    
    
    Enable-NetAdapterRdma -Name "vEthernet (SMB1)"
    Enable-NetAdapterRdma -Name "vEthernet (SMB2)"
    Get-NetAdapterRdma -Name "vEthernet*" | sort Name | fl *
    
    
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  True   
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  True  
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False
      

### <a name="validate-rdma-functionality-from-the-remote-system"></a>원격 시스템에서 RDMA 기능을 확인

이 섹션의 유효성을 검사할 vSwitch에 있는 로컬 시스템 원격 시스템에서 RDMA 기능이 있으므로 vSwitch 설정 팀의 구성원 두 어댑터를 테스트 사용할 수 있습니다.

때문에 모두 호스트 vNICs \ (SMB1 및 SMB2\) VLAN 102에 할당 된를 원격 시스템 VLAN 102 어댑터를 선택할 수 있습니다.  

NIC 테스트-40 G-2 SMB1에 RDMA 않는이 프로세스에 (192.168.2.111) 및 SMB2 (192.168.2.222).

옵션: 해야 할 수 있습니다이 시스템에 방화벽을 해제 합니다.  패브릭 정책에 대 한 자세한 내용은 참조 하십시오.

    
    Set-NetFirewallProfile -All -Enabled False
    
    Get-NetAdapterAdvancedProperty -Name "Test-40G-2"
    
    Name  DisplayNameDisplayValue   RegistryKeyword RegistryValue  
    ----  -----------------------   --------------- -------------  
    .
    .
    Test-40G-2VLAN ID102VlanID  {102} 
    
    Get-NetAdapter
    
    Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
    ----  --------------------------- ------   ---------- ---------
    Test-40G-2Mellanox ConnectX-3 Pro Ethernet A...#3   3 Up   E4-1D-2D-07-43-D140 Gbps
    
    
    Get-NetAdapterRdma
    
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    Test-40G-2Mellanox ConnectX-3 Pro Ethernet Adap... True   
    
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.111 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter Test-40G-2 is a physical adapter
    VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
    VERBOSE: QoS/DCB/PFC configuration is correct.
    VERBOSE: RDMA configuration is correct.
    VERBOSE: Checking if remote IP address, 192.168.2.111, is reachable.
    VERBOSE: Remote IP 192.168.2.111 is reachable.
    VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
    VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
    VERBOSE: 34251744 RDMA bytes sent per second
    VERBOSE: 967346308 RDMA bytes written per second
    VERBOSE: 35698177 RDMA bytes sent per second
    VERBOSE: 976601842 RDMA bytes written per second
    VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
    VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.111
    
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.222 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter Test-40G-2 is a physical adapter
    VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
    VERBOSE: QoS/DCB/PFC configuration is correct.
    VERBOSE: RDMA configuration is correct.
    VERBOSE: Checking if remote IP address, 192.168.2.222, is reachable.
    VERBOSE: Remote IP 192.168.2.222 is reachable.
    VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
    VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 485137693 RDMA bytes written per second
    VERBOSE: 35200268 RDMA bytes sent per second
    VERBOSE: 939044611 RDMA bytes written per second
    VERBOSE: 34880901 RDMA bytes sent per second
    VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
    VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.222
    
### <a name="test-for-rdma-traffic-from-the-local-to-the-remote-computer"></a>원격 컴퓨터에 RDMA 교통량에서 로컬 테스트

이 섹션에 원격 컴퓨터에 RDMA 교통 로컬 컴퓨터에서 보낸이 확인할 수 있습니다.

다음 명령 예 테스트 하 고 교통 흐름 보는 사용할 수 있습니다.

    
    Get-NetAdapter | ft –AutoSize
    
    Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
    ----  --------------------------- ------   ---------- ---------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  45 Up   00-15-5D-30-AA-0380 Gbps
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  41 Up   00-15-5D-30-AA-0280 Gbps
    
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 41 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter vEthernet (SMB1) is a virtual adapter
    VERBOSE: Retrieving vSwitch bound to the virtual adapter
    VERBOSE: Found vSwitch: VMSTEST
    VERBOSE: Found the following physical adapter(s) bound to vSwitch: TEST-40G-1, TEST-40G-2
    VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
    VERBOSE: QoS/DCB/PFC configuration is correct.
    VERBOSE: RDMA configuration is correct.
    VERBOSE: Checking if remote IP address, 192.168.2.5, is reachable.
    VERBOSE: Remote IP 192.168.2.5 is reachable.
    VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
    VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 15250197 RDMA bytes sent per second
    VERBOSE: 896320913 RDMA bytes written per second
    VERBOSE: 33947559 RDMA bytes sent per second
    VERBOSE: 912160540 RDMA bytes written per second
    VERBOSE: 34091930 RDMA bytes sent per second
    VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
    VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.5
    
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 45 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter vEthernet (SMB2) is a virtual adapter
    VERBOSE: Retrieving vSwitch bound to the virtual adapter
    VERBOSE: Found vSwitch: VMSTEST
    VERBOSE: Found the following physical adapter(s) bound to vSwitch: TEST-40G-1, TEST-40G-2
    VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
    VERBOSE: QoS/DCB/PFC configuration is correct.
    VERBOSE: RDMA configuration is correct.
    VERBOSE: Checking if remote IP address, 192.168.2.5, is reachable.
    VERBOSE: Remote IP 192.168.2.5 is reachable.
    VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
    VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 385169487 RDMA bytes written per second
    VERBOSE: 33902277 RDMA bytes sent per second
    VERBOSE: 907354685 RDMA bytes written per second
    VERBOSE: 33923662 RDMA bytes sent per second
    VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
    VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.5
    
이 출력 최종 줄 "RDMA 교통 테스트 성공: RDMA 교통 192.168.2.5로 전송 된" 어댑터에 수렴 NIC를 성공적으로 구성 있는지 보여 줍니다.

## <a name="all-topics-in-this-guide"></a>이 가이드의 모든 항목

이 가이드는 다음 항목이 포함 되어 있습니다.

- [단일 네트워크 어댑터를 사용 하 여 집약된 NIC 구성](cnic-single.md)
- [집약된 NIC 어댑터당된 NIC 구성](cnic-datacenter.md)
- [실제 스위치 구성 집약 nic](cnic-app-switch-config.md)
- [NIC 구성 수렴 문제 해결](cnic-app-troubleshoot.md)
