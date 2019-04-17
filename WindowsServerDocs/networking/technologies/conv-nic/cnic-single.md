---
title: 단일 네트워크 어댑터를 사용 하 여 집약된 NIC 구성
description: 이 항목 수렴 NIC 단일 네트워크 어댑터 Windows Server 2016에 배포 하는 방법에 대해 설명 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: eed5c184-fa55-43a8-a879-b1610ebc70ca
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d6663a966026afb301a4bad90a9573d16fc82875
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="converged-nic-configuration-with-a-single-network-adapter"></a>단일 네트워크 어댑터를 사용 하 여 집약된 NIC 구성

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

다음 섹션 수렴 NIC Hyper-v 호스트에서 단일 NIC와 구성에 대 한 지침을 제공 합니다.

이 가이드 구성 예 두 Hyper-v 호스트 보여 주며 **Hyper-v 호스트 A**, 및 **Hyper-v 호스트 B**합니다.

## <a name="test-connectivity-between-source-and-destination"></a>원본와 목적지 연결이 테스트

이 섹션 간 원본과 대상 Hyper-v 호스트 연결 테스트 하는 데 필요한 단계를 제공 합니다.

다음 표에 두 Hyper-v 호스트 **Hyper-v 호스트 A** 및 **Hyper-v 호스트 B**합니다. 

서버 모두 설치 단일 실제 NIC (pNIC) 있고 Nic 랙 \(ToR\) 물리적 스위치 위쪽에 연결 되어 있습니다. 또한 192.168.1.x/24은 같은 서브넷 서버 있습니다.

![Hyper-v 호스트](../../media/Converged-NIC/1-single-test-conn.jpg)


### <a name="test-nic-connectivity-to-the-hyper-v-virtual-switch"></a>테스트 NIC 연결 Hyper\ V 가상 스위치를

이 단계를 사용 하 여 Hyper\ V 가상 스위치를 만들 나중에 물리적 NIC 대상 호스트에 연결할 수 있는지 확인할 수 있습니다. 

이 테스트 계층 3 \(L3\)-또는 IP 계층-물론 \(L2\) 계층 2를 사용 하 여 연결을 보여 줍니다.

네트워크 어댑터의 속성을 가져오려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.

    Get-NetAdapter
     
이 명령의 예 결과 다음과 같은 합니다.

|이름|InterfaceDescription|ifIndex|상태|MacAddress|회선 속도|
|-----|--------------------|-------|-----|----------|---------|
|
|M1|Mellanox ConnectX 3 Pro...| 4| 위로|7C-FE-90-93-8F-A1|G b 40 p s|

IP 주소를 포함 하 여 추가 어댑터 속성을 가져오려면 뒤 다음 명령을 중 하나를 사용할 수 있습니다.

    Get-NetAdapter M1 | fl *

이 명령의 편집된 예 결과 다음과 같은 합니다.
    
    MacAddress   : 7C-FE-90-93-8F-A1
    Status   : Up
    LinkSpeed: 40 Gbps
    MediaType: 802.3
    PhysicalMediaType: 802.3
    AdminStatus  : Up
    MediaConnectionState : Connected
    DriverInformation: Driver Date 2016-08-28 Version 5.25.12665.0 NDIS 6.60
    DriverFileName   : mlx4eth63.sys
    NdisVersion  : 6.60
    ifOperStatus : Up
    ifAlias  : M1
    InterfaceAlias   : M1
    ifIndex  : 4
    ifDesc   : Mellanox ConnectX-3 Pro Ethernet Adapter
    ifName   : ethernet_32773
    DriverVersion: 5.25.12665.0
    LinkLayerAddress : 7C-FE-90-93-8F-A1
    Caption  :
    Description  :
    ElementName  :
    InstanceID   : {39B58B4C-8833-4ED2-A2FD-E105E7146D43}
    CommunicationStatus  :
    DetailedStatus   :
    HealthState  :
    InstallDate  :
    Name : M1
    OperatingStatus  :
    OperationalStatus:
    PrimaryStatus:
    StatusDescriptions   :
    AvailableRequestedStates :
    EnabledDefault   : 2
    EnabledState : 5
    OtherEnabledState:
    RequestedState   : 12
    TimeOfLastStateChange:
    TransitioningToState : 12
    AdditionalAvailability   :
    Availability :
    CreationClassName: MSFT_NetAdapter
    

### <a name="ensure-that-source-and-destination-can-communicate"></a>원본과 대상 통신할 수 있는지 확인

이 단계를 사용 하 여 확인 양방향 통신 \ (목적지를 모두 systems\에 반대의 소스에서 ping).  다음 예제에서는 **테스트 NetConnection** Windows PowerShell 명령을 사용 하는 경우 사용할 수 있는 것이 좋습니다 하지만 **ping** 명령을 합니다. 

>[!NOTE]
>호스트 서로 통신할 수 있는 특정을 경우이 단계를 건너뛸 수 있습니다.

    Test-NetConnection 192.168.1.5

이 명령의 예 결과 다음과 같은 합니다.

|매개|값|
|---------|-----|
|
|컴퓨터 이름|192.168.1.5|
|RemoteAddress|192.168.1.5|
|InterfaceAlias|M1|
|원본|192.168.1.3|
|PingSucceeded|진정한|
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

## <a name="configure-vlans-optional"></a>Vlan \(Optional\) 구성

다양 한 네트워크 구성 Vlan을 사용 하 여 확인 합니다. 사용자의 네트워크 안에 Vlan를 사용 하 여 계획 하는 경우 이전 테스트 Vlan 구성 된 반복 해야 합니다. \ (RoCE RDMA 서비스에 대 한 사용 하려는 경우 Vlan 설정 해야 합니다. \)

이 단계는 Nic에는 **액세스** 모드입니다. 그러나 Hyper-v의 가상 스위치 \(vSwitch\) 뒷부분에서를 만들 때 VLAN 속성 vSwitch 포트 수준에 적용 됩니다. 

스위치 여러 Vlan 호스트할 수, 되므로 랙 위에 \(ToR\) 물리적 스위치 포트 호스트 트렁크 모드로 구성에 연결 되어 있어야 합니다.

>[!NOTE]
>트렁크 모드 스위치를 구성 하는 방법에 대 한 지침은 스위치 설명서를 참조 하십시오.

다음 그림 실제 네트워크 어댑터가 하나 각각 두 Hyper-v 호스트 보여 주며 VLAN 101의 통신을 구성 합니다.

![가상 영역 로컬 네트워크 구성](../../media/Converged-NIC/2-single-configure-vlans.jpg)

### <a name="configure-the-vlan-id"></a>구성 VLAN ID

이 단계 Nic Hyper-v 호스트에 설치 된 용 VLAN Id를 구성할 지를 사용할 수 있습니다.

#### <a name="configure-nic-m1"></a>NIC M1 구성

다음 명령을 VLAN ID 첫 번째 NIC M1에 대 한 구성 다음 결과 구성 보기.

>[!IMPORTANT]
>이 명령을 실행 하지 마십시오이이 인터페이스를 통해 원격으로 호스트에 연결 되어 있는 경우는 발생할 수 있으므로 액세스 손실 호스트 하기 때문입니다.
    
    Set-NetAdapterAdvancedProperty -Name M1 -RegistryKeyword VlanID -RegistryValue "101"
    Get-NetAdapterAdvancedProperty -Name M1 | Where-Object {$_.RegistryKeyword -eq "VlanID"} 
    
이 명령의 예 결과 다음과 같은 합니다.

|이름 |표시 이름| DisplayValue| RegistryKeyword |RegistryValue|
|----|-----------|------------|---------------|-------------|
|
|M1|VLAN ID|101|VlanID|{101}|


네트워크 어댑터를 다시 시작 하려면 다음 명령을 사용 하 여 VLAN ID은 독립적으로 네트워크 어댑터 구현 적용 있는지 확인 합니다.

    Restart-NetAdapter -Name "M1"

다음 명령을 사용 하 여 네트워크 어댑터 상태 인지 확인 하려면 **위로** 진행 하기 전에 합니다.

    Get-NetAdapter -Name "M1"

이 명령의 예 결과 다음과 같은 합니다.

|이름|InterfaceDescription|ifIndex| 상태|MacAddress|회선 속도|
|----|--------------------|-------|------|----------| ---------|
|
|M1|Pro 이더넷 Mellanox ConnectX 3의...|4|위로|7C-FE-90-93-8F-A1|G b 40 p s|

로컬와 목적지 서버의이 단계를 수행 해야 합니다. 두 개의 경우 대상 하지 구성 로컬 서버와 같은 VLAN ID와, 통신할 수 없습니다.

### <a name="verify-connectivity"></a>연결 상태를 확인합니다

이 섹션 연결을 확인 하려면 네트워크 어댑터를 다시 시작 된 후에 사용할 수 있습니다. 연결 VLAN 태그 두 어댑터에 적용 한 후에 확인할 수 있습니다. 연결이 실패 하는 경우 동일한 VLAN VLAN 구성 또는 대상 참여 스위치를 검사할 수 있습니다. 

>[!IMPORTANT]
>이전 섹션의 단계를 수행한 후 다시 시작 하 고 네트워크에 사용할 수 있게 하는 디바이스에 대 한 몇 초 동안 걸릴 수 있습니다.

#### <a name="verify-connectivity-for-nic-test-40g-1"></a>NIC 테스트-40 G-1에 대 한 연결을 확인

첫 번째 nic 연결을 확인 하려면 다음 명령의 실행할 수 있습니다.

    Test-NetConnection 192.168.1.5
    
## <a name="configure-data-center-bridging-dcb"></a>구성 \(DCB\) 브리지 데이터 센터

다음 단계 설치 하면 처음 Windows Server 2016 기능 DCB DCB 및 서비스 품질 \(QoS\) 구성 하는 것입니다.

>[!NOTE]
>다른 사용자와 소통 하는 것은 모든 서버의 DCB 및 QoS 구성 다음 단계를 모두를 수행 해야 합니다.

### <a name="install-data-center-bridging-dcb"></a>설치 \(DCB\) 브리지 데이터 센터

설치 하 고 DCB 사용이 단계를 사용할 수 있습니다. 

>[!IMPORTANT]
>- 설치 및 구성 DCB는 **선택적** iWarp RDMA 서비스에 대 한 사용 하는 네트워크 구성에 대 한 합니다.
>- 설치 및 구성 DCB는 **필요한** RoCE \(any version\) RDMA 서비스에 대 한 사용 하는 네트워크 구성에 대 한 합니다.


다음 명령을 각 Hyper-v 호스트 DCB 설치에 사용할 수 있습니다. 

    Install-WindowsFeature Data-Center-Bridging

### <a name="set-the-qos-policies-for-smb-direct"></a>직접 SMB QoS 정책 설정 

다음 명령을 SMB 직접 용 QoS 정책을 구성할 지를 사용할 수 있습니다.

>[!IMPORTANT]
>- 이 단계는 iWarp 사용 하는 네트워크 구성에 대 한 옵션 합니다.
>- 이 단계는 RoCE 사용 하는 네트워크 구성에 대 한 필요 합니다.
>- 아래의 예제 명령 "3" 임의의입니다. 전체 QoS 정책에서 구성 동일한 값을 지속적으로 사용 가능한 1 사이의 7 값을 사용할 수 있습니다.

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

### <a name="for-roce-deployments-turn-on-priority-flow-control-for-smb-traffic"></a>우선 순위 흐름 제어 SMB 교통량 RoCE 배포 설정에 대 한 

RoCE RDMA 서비스를 사용 하는 경우 SMB 흐름 제어를 사용 하도록 설정 하 고 결과를 보려면 다음 명령을 사용할 수 있습니다. 우선 순위 플로 컨트롤 RoCE, 해야 하지만 iWarp를 사용 하는 경우 필요 하지 않습니다.

    Enable-NetQosFlowControl -priority 3
    Get-NetQosFlowControl

예 결과 다음과 같은 **Get NetQosFlowControl** 명령을 합니다.

|우선 순위 부여|사용 하도록 설정|PolicySet|IfIndex|IfAlias|
|---------|-----|--------- |-------| -------|
|
|0 |False |전 세계|&nbsp;|&nbsp;|
|1 |False |전 세계|&nbsp;|&nbsp;|
|2 |False |전 세계|&nbsp;|&nbsp;|
|3 |진정한  |전 세계|&nbsp;|&nbsp;|
|4 |False |전 세계|&nbsp;|&nbsp;|
|5 |False |전 세계|&nbsp;|&nbsp;|
|6 |False |전 세계|&nbsp;|&nbsp;|
|7 |False |전 세계|&nbsp;|&nbsp;|

### <a name="enable-qos-for-the-local-and-destination-network-adapters"></a>QoS 로컬 대상 네트워크 어댑터에 대 한 사용 하도록 설정
이 단계를 DCB 특정 네트워크 어댑터에 사용할 수 있습니다.

>[!IMPORTANT]
>-  이 단계 iWarp를 사용 하는 네트워크 구성에 대 한 필요 하지 않습니다.
>-  이 단계는 RoCE 사용 하는 네트워크 구성에 대 한 필요 합니다.




#### <a name="enable-qos-for-nic-m1"></a>QoS NIC M1를 사용 하도록 설정

다음 명령을 QoS 사용 하도록 설정 하 고 구성에 결과 보기를 사용할 수 있습니다.

    Enable-NetAdapterQos -InterfaceAlias "M1"
    Get-NetAdapterQos -Name "M1"

이 명령의 예 결과 다음과 같은 합니다.

**이름**: M1 **활성화**: 진정한 **기능**:   

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
|0| ETS|70%|0-2,4-7|
|1|ETS|30%|3

**OperationalFlowControl**: 우선 순위 활성화 3 **OperationalClassifications**:

|프로토콜|포트/유형|우선 순위 부여|
|--------|---------|--------|
|
|기본|&nbsp;|0|
|NetDirect| 445|3|

### <a name="reserve-a-percentage-of-the-bandwidth-for-smb-direct-rdma"></a>직접 SMB \(RDMA\) 대역폭 비율로 예약

다음 명령을 SMB direct 대역폭 비율로 예약 하 사용할 수 있습니다.  

여기에서 30% 대역폭 예약 사용 됩니다. 예상과 저장소 교통 필요 합니다 나타내는 값을 선택 해야 합니다. 값은 **-bandwidthpercentage** 매개 10% 여러 이어야 합니다.

    New-NetQosTrafficClass "SMB" -Priority 3 -BandwidthPercentage 30 -Algorithm ETS

이 명령의 예 결과 다음과 같은 합니다.

|이름|알고리즘 |Bandwidth(%)| 우선 순위 부여 |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|SMB | ETS     | 30 |3 |전 세계 |&nbsp;|&nbsp;|                                      
 
다음 명령을 대역폭 예약 정보를 사용할 수 있습니다.

    Get-NetQosTrafficClass

이 명령의 예 결과 다음과 같은 합니다.
 
|이름|알고리즘 |Bandwidth(%)| 우선 순위 부여 |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|[기본]|ETS|70 |0-2,4-7| 전 세계|&nbsp;|&nbsp;| 
|SMB      |ETS|30 |3 |전 세계|&nbsp;|&nbsp;| 

## <a name="remove-debugger-conflict-mellanox-adapter-only"></a>디버거 충돌 제거 \(Mellanox adapter only\)

Mellanox에서 어댑터를 사용 하는 경우 디버거 구성 하려면이 단계를 수행 해야 합니다. 기본적으로 Mellanox 어댑터를 사용 하 고, 연결 된 디버거 NetQos 차단 합니다. 다음 명령을 디버거 재정의을 사용할 수 있습니다.

    
    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
    

## <a name="test-rdma-native-host"></a>테스트 RDMA (기본 호스트)

패브릭 vSwitch를 만들고 RDMA \(Converged NIC\)로 전환 되는 이전 올바르게 구성 되어 있는지 확인 하려면이 단계를 사용할 수 있습니다.

다음 그림에서는 Hyper-v 호스트 현재 상태를 보여 줍니다.

![테스트 RDMA](../../media/Converged-NIC/4-single-test-rdma.jpg)

RDMA 구성을 확인 하려면 다음 명령의 실행할 수 있습니다.

    Get-NetAdapterRdma

이 명령의 예 결과 다음과 같은 합니다.

|이름 |InterfaceDescription |사용 하도록 설정|
|----|--------------------|-------|
|
|M1| Mellanox ConnectX 3 Pro 이더넷 어댑터 |진정한|

### <a name="download-diskspdexe-and-a-powershell-script"></a>DiskSpd.exe 및는 PowerShell 스크립트 다운로드

계속 하려면 먼저 다음 항목을 다운로드 해야 합니다.

- DiskSpd.exe 유틸리티를 다운로드 하 고 C:\TEST\에 유틸리티 압축 [Diskspd 유틸리티: A 강력한 저장소 테스트 도구 (SQLIO 대체)](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223)

- Test-RDMA powershell 스크립트 C:\TEST\로 다운로드 [https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)

### <a name="determine-the-ifindex-value-of-your-target-adapter"></a>대상 어댑터의 ifIndex 값을 확인

다음 명령을 대상 어댑터의 ifIndex 값 검색 하는 데 사용할 수 있습니다. 이 값 다운로드 한 스크립트를 실행 하는 경우 다음 단계에 사용할 수 있습니다.

    Get-NetIPConfiguration -InterfaceAlias "M*" | ft InterfaceAlias,InterfaceIndex,IPv4Address

이 명령의 예 결과 다음과 같은 합니다.

|InterfaceAlias |InterfaceIndex |IPv4Address|
|-------------- |-------------- |-----------|
|
|M 2 |14 |{192.168.1.5}|

### <a name="run-the-powershell-script"></a>PowerShell 스크립트를 실행합니다

Test-Rdma.ps1 Windows PowerShell 스크립트를 실행할 때와 같은 VLAN에서 원격 어댑터의 IP 주소 스크립트 ifIndex 값을 전달할 수 있습니다.

명령은 스크립트를 실행할 14 ifIndex로 네트워크 어댑터 192.168.1.5에서 사용할 수 있습니다.
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 14 -IsRoCE $true -RemoteIpAddress 192.168.1.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter M2 is a physical adapter
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

## <a name="remove-the-access-vlan-setting"></a>액세스 VLAN 설정 제거

Hyper-v 스위치를 만들기 위한 준비 과정에서 위에 설치 VLAN 설정이 제거 해야 합니다.  다음 명령을 사용 하 여 실제 NIC에서 액세스 VLAN 설정을 제거 하려면 이 작업을이 수행 NIC 자동 태그 송신 교통 잘못 VLAN ID를 사용 하는 것을 방지합니다 하 고 또한 액세스 VLAN ID와 일치 하지 않는 수신 교통 필터링에서 방지

    
    Set-NetAdapterAdvancedProperty -Name M1 -RegistryKeyword VlanID -RegistryValue "0"
    

VlanID 설정을 확인 하 고 0 VLAN ID 값이 표시 되는 결과 보려면 다음 예 명령을 사용할 수 있습니다.

    
    Get-NetAdapterAdvancedProperty -name m1 | Where-Object {$_.RegistryKeyword -eq 'VlanID'} 
    


## <a name="create-a-hyper-v-virtual-switch"></a>Hyper-v 가상 스위치를 만들기

이 섹션 Hyper-v 호스트의 Hyper-v의 가상 스위치 \(vSwitch\)를 사용할 수 있습니다.

다음 표에 vSwitch를 Hyper-v 호스트 1.

![Hyper-v 가상 스위치를 만들기](../../media/Converged-NIC/5-single-create-vswitch.jpg)


### <a name="create-an-external-hyper-v-virtual-switch"></a>Hyper-v 가상 스위치를 외부 만들기

이 섹션을 사용 하 여 외부 vSwitch Hyper-v 호스트 a Hyper-v의 만들기

라는 VMSTEST 스위치를 만들려면 명령은 사용할 수 있습니다.

>[!NOTE]
>매개 **AllowManagementOS** 다음 명령을 만듭니다 MAC 주소와 물리적 NIC의 IP 주소 상속 호스트 vNIC

    New-VMSwitch -Name VMSTEST -NetAdapterName "M1" -AllowManagementOS $true

이 명령의 예 결과 다음과 같은 합니다.

|이름 |SwitchType |NetAdapterInterfaceDescription|
|---- |---------- |------------------------------|
|VMSTEST |외부 |Mellanox ConnectX 3 Pro 이더넷 어댑터|

네트워크 어댑터의 속성을 보려면 다음 명령을 사용할 수 있습니다.

    Get-NetAdapter | ft -AutoSize

이 명령의 예 결과 다음과 같은 합니다.

|이름 |InterfaceDescription | ifIndex |상태 |MacAddress |회선 속도|
|---- |-------------------- |-------| ------|----------|---------|
|
|vEthernet \(VMSTEST\) |Hyper-v 가상 이더넷 어댑터 2|27 |위로 |E4-1D-2D-07-40-71 |G b 40 p s|


두 가지 방법으로 호스트 vNIC 관리할 수 있습니다. 한 가지 방법은 **NetAdapter** 보기 작동 하는 기반의 "vEthernet \(VMSTEST\)" 이름입니다.

또 다른 방법은는 **VMNetworkAdapter** 보기 "vEthernet" 접두사 삭제 하 고 사용 하 여 vmswitch 이름입니다.

**VMNetworkAdapter** 보기 표시으로 표시 되지 않는 네트워크 어댑터 속성 일부는 **NetAdapter** 명령을 합니다.

다음 명령을 사용 하 여의 결과 볼 수 있는 **VMNetworkAdapter** 방법입니다.

    Get-VMNetworkAdapter –ManagementOS | ft -AutoSize

이 명령의 예 결과 다음과 같은 합니다.

|이름 |IsManagementOs |VMName |SwitchName |MacAddress |상태 |IPAddresses|
|----|-------------- |------ |----------|----------|------ |-----------|
|
|CORP 외부 전환 |진정한 |CORP 외부 전환| 001B785768AA |{확인} |&nbsp;|
|VMSTEST |진정한 |VMSTEST | E41D2D074071| {확인} | &nbsp;| 

### <a name="test-the-connection"></a>연결 테스트

연결 테스트 하 고 결과 보려면 다음 예 명령을 사용할 수 있습니다.
    
    Test-NetConnection 192.168.1.5

    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (CORP-External-Switch)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    
다음 명령 예 지정 하 고 네트워크 어댑터 VLAN 설정 보기를 사용할 수 있습니다.
    
    Set-VMNetworkAdapterVlan -VMNetworkAdapterName "VMSTEST" -VlanId "101" -Access -ManagementOS
    Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName "VMSTEST"
    

|VMName |VMNetworkAdapterName |모드 |VlanList|
|------ |-------------------- |---- |--------|
|
|&nbsp;|VMSTEST |액세스 |101     
 
### <a name="test-the-connection"></a>연결 테스트

기억하실 변경 다른 어댑터를 했습니다 ping 할 수 되기 전에 완료 몇 초 동안을 걸릴 수 있습니다.

연결 테스트 하 고 결과 보려면 다음 예 명령을 사용할 수 있습니다.
    
    Test-NetConnection 192.168.1.5
     
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (VMSTEST)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    

## <a name="test-hyper-v-virtual-switch-rdma-mode-2"></a>Hyper-v 가상 스위치 RDMA (모드 2)를 테스트 합니다.

다음 그림에서는 Hyper-v 호스트, Hyper-v 호스트 1 vSwitch를 포함 하 여 현재 상태를 보여 줍니다.

![Hyper-v 가상 스위치를 테스트 합니다.](../../media/Converged-NIC/6-single-test-vswitch-rdma.jpg)


### <a name="set-priority-tagging-on-the-host-vnic"></a>호스트 vNIC에 태그 우선 순위를 설정

호스트 vNIC에 태그 우선 순위를 설정 하 고 이러한 작업 결과 보려면 다음 예 명령을 사용할 수 있습니다.
    
    Set-VMNetworkAdapter -ManagementOS -Name "VMSTEST" -IeeePriorityTag on
    Get-VMNetworkAdapter -ManagementOS -Name "VMSTEST" | fl Name,IeeePriorityTag
    
    Name: VMSTEST
    IeeePriorityTag : On
    
네트워크 어댑터 RDMA 정보를 보려면 다음 예 명령을 사용할 수 있습니다. 결과에서 때 매개 **사용** 값 **False**, 의미 RDMA 사용할 수 없습니다.
    
    Get-NetAdapterRdma
    
|이름 |InterfaceDescription |사용 하도록 설정 |
|---- |-------------------- |-------|
|
|vEthernet \(VMSTEST\)| Hyper-v 가상 이더넷 어댑터 2|False|

### <a name="enable-rdma-on-the-host-vnic"></a>RDMA 호스트 vNIC에서 사용 하도록 설정

네트워크 어댑터 속성 보고 RDMA 어댑터를 사용 하도록 설정 하 고 네트워크 어댑터 RDMA 정보를 보려면 다음 다음 예제 명령을 사용할 수 있습니다.
    
    Get-NetAdapter
    
|이름 |InterfaceDescription |ifIndex |상태 |MacAddress |회선 속도|
|----|--------------------|-------|------|----------|---------|
|
|vEthernet (VMSTEST)|Hyper-v 가상 이더넷 어댑터 2|27|위로|E4-1D-2D-07-40-71|G b 40 p s|

    Enable-NetAdapterRdma -Name "vEthernet (VMSTEST)"
    Get-NetAdapterRdma -Name "vEthernet (VMSTEST)"

다음 결과에서 때 매개 **사용** 값 **진정한**, RDMA를 사용할 수 있도록 것을 의미 합니다.

|이름 |InterfaceDescription |사용 하도록 설정 |
|---- |-------------------- |-------|
|
|vEthernet \(VMSTEST\)| Hyper-v 가상 이더넷 어댑터 2|진정한|


    
    Get-NetAdapter 
    

|이름 |InterfaceDescription |ifIndex |상태 |MacAddress |회선 속도|
|----|--------------------|-------|------|----------|---------|
|
|vEthernet (VMSTEST)|Hyper-v 가상 이더넷 어댑터 2|27|위로|E4-1D-2D-07-40-71|G b 40 p s|

### <a name="perform-rdma-traffic-test-by-using-the-script"></a>스크립트를 사용 하 여 RDMA 교통 테스트를 수행 합니다.

다운로드 한 스크립트 실행 하 고 결과 보려면 다음 명령을 사용할 수 있습니다.
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 27 -IsRoCE $true -RemoteIpAddress 192.168.1.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter vEthernet (VMSTEST) is a virtual adapter
    VERBOSE: Retrieving vSwitch bound to the virtual adapter
    VERBOSE: Found vSwitch: VMSTEST
    VERBOSE: Found the following physical adapter(s) bound to vSwitch: TEST-40G-1
    VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
    VERBOSE: QoS/DCB/PFC configuration is correct.
    VERBOSE: RDMA configuration is correct.
    VERBOSE: Checking if remote IP address, 192.168.1.5, is reachable.
    VERBOSE: Remote IP 192.168.1.5 is reachable.
    VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
    VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 9162492 RDMA bytes sent per second
    VERBOSE: 938797258 RDMA bytes written per second
    VERBOSE: 34621865 RDMA bytes sent per second
    VERBOSE: 933572610 RDMA bytes written per second
    VERBOSE: 35035861 RDMA bytes sent per second
    VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
    VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.1.5
    
이 출력 최종 줄 "RDMA 교통 테스트 성공: RDMA 교통 192.168.1.5로 전송 된" 어댑터에 수렴 NIC를 성공적으로 구성 있는지 보여 줍니다.

## <a name="all-topics-in-this-guide"></a>이 가이드의 모든 항목

이 가이드는 다음 항목이 포함 되어 있습니다.

- [단일 네트워크 어댑터를 사용 하 여 집약된 NIC 구성](cnic-single.md)
- [집약된 NIC 어댑터당된 NIC 구성](cnic-datacenter.md)
- [실제 스위치 구성 집약 nic](cnic-app-switch-config.md)
- [NIC 구성 수렴 문제 해결](cnic-app-troubleshoot.md)
