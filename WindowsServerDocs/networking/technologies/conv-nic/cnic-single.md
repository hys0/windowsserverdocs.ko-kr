---
title: 단일 네트워크 어댑터로 수렴 된 NIC 구성
description: 이 항목에서는 하면 Hyper-v 호스트에서 단일 NIC를 사용 하 여 수렴 형 된 NIC를 구성 하는 지침을 사용 하 여 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: eed5c184-fa55-43a8-a879-b1610ebc70ca
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/14/2018
ms.openlocfilehash: 93d317534af46c87c4b2e874a5a5475687e2efa0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447062"
---
# <a name="converged-nic-configuration-with-a-single-network-adapter"></a>단일 네트워크 어댑터로 수렴 된 NIC 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 하면 Hyper-v 호스트에서 단일 NIC를 사용 하 여 수렴 형 된 NIC를 구성 하는 지침을 사용 하 여 합니다.

이 항목의 예제 구성은 두 Hyper-v 호스트를 설명 **Hyper-v 호스트 A**, 및 **Hyper-v 호스트 B**합니다. 두 호스트에 설치 된 단일 실제 NIC (pNIC) 및 Nic top-of-rack에 연결 된 \(ToR\) 물리적 스위치입니다. 또한 호스트 192.168.1.x/24 동일한 서브넷에 있습니다.

![Hyper-V 호스트](../../media/Converged-NIC/1-single-test-conn.jpg)


## <a name="step-1-test-the-connectivity-between-source-and-destination"></a>1단계. 원본과 대상 간의 연결을 테스트

실제 NIC에 연결할 수 있도록 대상 호스트를 확인 합니다. 이 테스트 된 3 계층을 사용 하 여 연결을 보여 줍니다 \(L3\) -또는 IP 계층-2 계층 뿐만 아니라 \(L2\)합니다.

1. 네트워크 어댑터 속성을 봅니다.

   ```PowerShell
   Get-NetAdapter
   ```

   _**결과:** _  


   | 이름 |    InterfaceDescription     | ifIndex | 상태 |    MacAddress     | LinkSpeed |
   |------|-----------------------------|---------|--------|-------------------|-----------|
   |  M1  | Mellanox connectx-3 Pro... |    4    |   위쪽   | 7C-FE-90-93-8F-A1 |  40gbps  |

   ---

2. IP 주소를 비롯 한 추가 어댑터 속성을 봅니다.

   ```PowerShell
   Get-NetAdapter M1 | fl *
   ```

   _**결과:** _

   ```PowerShell   
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
   ``` 

## <a name="step-2-ensure-that-source-and-destination-can-communicate"></a>2단계. 원본 및 대상 통신할 수 있는지 확인

이 단계에서는 사용 하 여는 **Test-netconnection** Windows PowerShell 명령을 사용할 수 있습니다 하지만 **ping** 원할 경우 명령. 

>[!TIP]
>특정 호스트 서로 통신할 수 있는지, 인 경우이 단계를 건너뛸 수 있습니다.

1. 양방향 통신을 확인 합니다.

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**결과:** _


   |        매개 변수         |    값    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.1.5 |
   |      RemoteAddress       | 192.168.1.5 |
   |      InterfaceAlias      |     M1      |
   |      SourceAddress       | 192.168.1.3 |
   |      PingSucceeded       |    True     |
   | PingReplyDetails \(RTT\) |    0ms     |

   ---

   일부 경우에 성공적으로이 테스트를 수행 하려면 고급 보안이 포함 된 Windows 방화벽을 사용 하지 않도록 설정 해야 합니다. 방화벽을 해제 하면 보안을 염두 하 고 구성에 조직의 보안 요구 사항을 충족 하는지 확인 합니다.

2. 모든 방화벽 프로필을 사용 하지 않도록 설정 합니다.

   ```PowerShell
   Set-NetFirewallProfile -All -Enabled False
   ```

3. 방화벽 프로필을 비활성화 한 후 다시 연결을 테스트 합니다. 

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**결과:** _


   |        매개 변수         |    값    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.1.5 |
   |      RemoteAddress       | 192.168.1.5 |
   |      InterfaceAlias      | Test-40G-1  |
   |      SourceAddress       | 192.168.1.3 |
   |      PingSucceeded       |    False    |
   | PingReplyDetails \(RTT\) |    0ms     |

   ---



## <a name="step-3-optional-configure-the-vlan-ids-for-nics-installed-in-your-hyper-v-hosts"></a>3단계. (선택 사항) Hyper-v 호스트에 설치 하는 Nic에 대 한 VLAN Id를 구성 합니다.

다양 한 네트워크 구성 Vlan을 사용 하 고 네트워크에 Vlan을 사용 하려는 경우 구성 하는 Vlan을 사용 하 여 이전 테스트를 반복 해야 합니다. 또한 RDMA 서비스용 RoCE를 사용 하려는 경우 Vlan을 활성화 해야 합니다.

Nic가 있는이 단계에서는 **액세스** 모드입니다. 그러나 Hyper-v 가상 스위치를 만들 때 \(vSwitch\) VLAN 속성을이 가이드의 뒷부분에 나오는 vSwitch 포트 수준에서 적용 됩니다. 

위쪽의 랙에 해야 하는 스위치를 여러 Vlan을 호스팅할 수, 있으므로 \(ToR\) 물리적 스위치 포트를 트렁크 모드로 구성 된 호스트에 연결 되어 있어야 합니다.

>[!NOTE]
>스위치에 트렁크 모드를 구성 하는 방법에 대 한 지침은 ToR 스위치 설명서를 참조 하십시오.

다음 이미지는 실제 네트워크 어댑터가 두 개를 사용 하 여 각 두 Hyper-v 호스트를 표시 및 각 VLAN 101에서 통신 하도록 구성 합니다.

![Virtual local area network 구성](../../media/Converged-NIC/2-single-configure-vlans.jpg)


>[!IMPORTANT]
>로컬 및 대상 서버에서이 수행 합니다. 대상 서버가 구성 되지 않은 로컬 서버와 동일한 VLAN ID를 사용 하 여, 두 통신할 수 없습니다.


1. Hyper-v 호스트에 설치 하는 Nic에 대 한 VLAN ID를 구성 합니다.

   >[!IMPORTANT]
   >이 명령을 실행 하지이이 인터페이스를 통해 원격 호스트에 연결 된 경우 호스트에 액세스 권한이 손실 생성 되므로 합니다.

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name M1 -RegistryKeyword VlanID -RegistryValue "101"
   Get-NetAdapterAdvancedProperty -Name M1 | Where-Object {$_.RegistryKeyword -eq "VlanID"} 
   ```

   _**결과:** _


   | 이름 | DisplayName | DisplayValue | RegistryKeyword | RegistryValue |
   |------|-------------|--------------|-----------------|---------------|
   |  M1  |   VLAN ID   |     101      |     VlanID      |     {101}     |

   ---

2. 네트워크 어댑터에 VLAN ID를 적용 하려면 다시 시작

   ```PowerShell
   Restart-NetAdapter -Name "M1"
   ```

3. 상태 확인 **등록**합니다.

   ```PowerShell
   Get-NetAdapter -Name "M1"
   ```

   _**결과:** _


   | 이름 |          InterfaceDescription           | ifIndex | 상태 |    MacAddress     | LinkSpeed |
   |------|-----------------------------------------|---------|--------|-------------------|-----------|
   |  M1  | Mellanox connectx-3 Pro 이더넷 Ada... |    4    |   위쪽   | 7C-FE-90-93-8F-A1 |  40gbps  |

   ---

   >[!IMPORTANT]
   >다시 시작 하 고 네트워크에서 사용할 수 있게 하는 장치에 대 한 초가 걸릴 수 있습니다. 

4. 연결을 확인 합니다.<p>연결에 실패 하면 동일한 VLAN의 VLAN 구성 또는 대상 참여 스위치를 검사 합니다. 

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

## <a name="step-4-configure-quality-of-service-qos"></a>4단계. 서비스 품질 구성 \(QoS\)

>[!NOTE]
>서로 통신 하려는 모든 호스트에서 모든 다음 DCB 및 QoS 구성 단계를 수행 해야 합니다.

1. 데이터 센터 브리징 설치할 \(DCB\) 각 Hyper-v 호스트.

   - **선택적** iWarp RDMA 서비스를 사용 하는 네트워크 구성에 대 한 합니다.
   - **필요한** RoCE를 사용 하는 네트워크 구성에 대 한 \(버전일\) RDMA 서비스에 대 한 합니다.

   ```PowerShell
   Install-WindowsFeature Data-Center-Bridging
   ```

2. SMB 다이렉트에 대 한 QoS 정책을 설정 합니다.

   - **선택적** iWarp를 사용 하는 네트워크 구성에 대 한 합니다.
   - **필요한** RoCE를 사용 하는 네트워크 구성에 대 한 합니다.

   아래 예제에서는 명령에서 "3" 값은 임의의. QoS 정책을 구성 과정에서 동일한 값을 일관 되 게 사용 하면 1에서 7 사이의 모든 값을 사용할 수 있습니다.

   ```PowerShell
   New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3
   ```

   _**결과:** _


   |   매개 변수    |          값           |
   |----------------|--------------------------|
   |      이름      |           SMB            |
   |     소유자      | 그룹 정책 \(컴퓨터\) |
   | NetworkProfile |           All            |
   |   우선 순위   |           127            |
   |   JobObject    |          &nbsp;          |
   | NetDirectPort  |           445            |
   | PriorityValue  |            3             |

   ---

3. 켜기 RoCE 배포용 **우선 순위 흐름 제어** iWarp 필요 없는 SMB 트래픽입니다.

   ```PowerShell
   Enable-NetQosFlowControl -priority 3
   Get-NetQosFlowControl
   ```

   _**결과:** _


   | Priority | Enabled | PolicySet | IfIndex | IfAlias |
   |----------|---------|-----------|---------|---------|
   |    0     |  False  |  전역   | &nbsp;  | &nbsp;  |
   |    1     |  False  |  전역   | &nbsp;  | &nbsp;  |
   |    2     |  False  |  전역   | &nbsp;  | &nbsp;  |
   |    3     |  True   |  전역   | &nbsp;  | &nbsp;  |
   |    4     |  False  |  전역   | &nbsp;  | &nbsp;  |
   |    5     |  False  |  전역   | &nbsp;  | &nbsp;  |
   |    6     |  False  |  전역   | &nbsp;  | &nbsp;  |
   |    7     |  False  |  전역   | &nbsp;  | &nbsp;  |

   ---

4. 로컬 및 대상 네트워크 어댑터에 QoS를 사용 합니다.

   - **필요 하지 않습니다** iWarp를 사용 하는 네트워크 구성에 대 한 합니다.
   - **필요한** RoCE를 사용 하는 네트워크 구성에 대 한 합니다.

   ```PowerShell
   Enable-NetAdapterQos -InterfaceAlias "M1"
   Get-NetAdapterQos -Name "M1"
   ```

   _**결과:** _

   **이름**: M1  
   **Enabled**: True  

   _**기능:** _   


   |      매개 변수      |   하드웨어   |   현재    |
   |---------------------|--------------|--------------|
   |    MacSecBypass     | NotSupported | NotSupported |
   |     DcbxSupport     |     없음     |     없음     |
   | NumTCs(Max/ETS/PFC) |    8/8/8     |    8/8/8     |

   ---

   _**OperationalTrafficClasses:** _ 


   | TC | TSA | 대역폭 | 우선 순위 |
   |----|-----|-----------|------------|
   | 0  | ETS |    70%    |  0-2,4-7   |
   | 1  | ETS |    30%    |     3      |

   ---

   _**OperationalFlowControl:** _  

   우선 순위 3 사용 하도록 설정  

   _**OperationalClassifications:** _  


   | Protocol  | 포트/유형 | Priority |
   |-----------|-----------|----------|
   |  기본값  |  &nbsp;   |    0     |
   | NetDirect |    445    |    3     |

   ---

5. SMB 다이렉트에 대 한 대역폭의 백분율을 예약 \(RDMA\)합니다.

    이 예제에서는 30% 대역폭 예약이 됩니다. 예상 저장소 트래픽이 필요 여부를 나타내는 값을 선택 해야 합니다. 

   ```PowerShell
   New-NetQosTrafficClass "SMB" -Priority 3 -BandwidthPercentage 30 -Algorithm ETS
   ```

   _**결과:** _


   | 이름 | 알고리즘 | Bandwidth(%) | Priority | PolicySet | IfIndex | IfAlias |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | SMB  |    ETS    |      30      |    3     |  전역   | &nbsp;  | &nbsp;  |

   ---                                      

6. 대역폭 예약 설정을 봅니다.  

   ```PowerShell
   Get-NetQosTrafficClass
   ```

   _**결과:** _


   |   이름    | 알고리즘 | Bandwidth(%) | Priority | PolicySet | IfIndex | IfAlias |
   |-----------|-----------|--------------|----------|-----------|---------|---------|
   | [기본값] |    ETS    |      70      | 0-2,4-7  |  전역   | &nbsp;  | &nbsp;  |
   |    SMB    |    ETS    |      30      |    3     |  전역   | &nbsp;  | &nbsp;  |

   ---

## <a name="step-5-optional-resolve-the-mellanox-adapter-debugger-conflict"></a>5단계. (선택 사항) Mellanox 어댑터 디버거 충돌 해결 

기본적으로 Mellanox 어댑터를 사용 하는 경우, 연결된 된 디버거에 NetQos, 알려진된 문제는 차단 합니다. 따라서 Mellanox에서 어댑터를 사용 하는 디버거를 연결 하려고 하는 경우 사용 하 여 다음 명령을 확인이이 문제입니다. 디버거를 연결 하지 않으려는 경우 또는 Mellanox 어댑터를 사용 하지 않는 경우에이 단계가 필요 하지 않습니다.

   ```PowerShell    
   Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
   ``` 

## <a name="step-6-verify-the-rdma-configuration-native-host"></a>6단계. RDMA 구성 (기본 호스트)를 확인 합니다.

패브릭 vSwitch를 만들고 RDMA (수렴 형 된 NIC)로 전환 하기 전에 올바르게 구성 되어 있는지 확인 해야 합니다. 

다음 이미지는 Hyper-v 호스트의 현재 상태를 표시 합니다.

![RDMA 테스트](../../media/Converged-NIC/4-single-test-rdma.jpg)

1. RDMA 구성을 확인 합니다.

   ```PowerShell
   Get-NetAdapterRdma
   ```
   _**결과:** _


   | 이름 |           InterfaceDescription           | Enabled |
   |------|------------------------------------------|---------|
   |  M1  | Mellanox connectx-3 Pro 이더넷 어댑터 |  True   |

   ---

2. 확인 합니다 **ifIndex** 대상 어댑터의 값입니다.<p>다운로드 한 스크립트를 실행할 때 이후 단계에서이 값을 사용 합니다.

   ```PowerShell
   Get-NetIPConfiguration -InterfaceAlias "M*" | ft InterfaceAlias,InterfaceIndex,IPv4Address
   ```

   _**결과:** _ 


   | InterfaceAlias | InterfaceIndex |  IPv4Address  |
   |----------------|----------------|---------------|
   |       M2       |       14       | {192.168.1.5} |

   ---

3. 다운로드 합니다 [DiskSpd.exe 유틸리티](https://aka.ms/diskspd) C:\TEST를 추출 하 고\.

4. 다운로드 합니다 [테스트 RDMA powershell 스크립트](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1) C:\TEST 예를 들어, 로컬 드라이브에서 테스트 폴더\.

5. 실행 합니다 **테스트 Rdma.ps1** PowerShell 스크립트를 스크립트에 동일한 VLAN에 있는 원격 어댑터의 IP 주소와 함께 ifIndex 값을 전달 합니다.<p>이 예제의 스크립트는 다음과 같이 전달 됩니다. 합니다 **ifIndex** 원격 네트워크 어댑터 IP 주소 192.168.1.5 14의 값입니다.

   ```PowerShell
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
   ```

   >[!NOTE]
   >특히, RDMA 트래픽 실패 RoCE 사례에 대 한 호스트 설정이 일치 해야 하는 적절 한 PFC/ETS 설정에 대 한 구성에 ToR 스위치를 참조 하십시오. 참조 값에 대 한이 문서에서 QoS 섹션을 참조 하세요.

## <a name="step-7-remove-the-access-vlan-setting"></a>7단계. 액세스 VLAN 설정을 제거합니다

스위치는 Hyper-v를 만들기 위한 준비 과정에서 앞서 설치한 VLAN 설정을 제거 해야 합니다.  

1. 잘못 된 VLAN ID를 사용 하 여 송신 트래픽을 자동 태깅에서 NIC를 방지 하기 위해 물리적 NIC에서 ACCESS VLAN 설정을 제거합니다<p>액세스 VLAN ID와 일치 하지 않는 수신 트래픽을 필터링에서 방지도이 설정을 제거

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name M1 -RegistryKeyword VlanID -RegistryValue "0"
   ```    

2. 있는지 확인 합니다 **VlanID 설정을** 0으로 VLAN ID 값을 보여 줍니다.

   ```PowerShell    
   Get-NetAdapterAdvancedProperty -name m1 | Where-Object {$_.RegistryKeyword -eq 'VlanID'} 
   ```  


## <a name="step-8-create-a-hyper-v-vswitch-on-your-hyper-v-hosts"></a>8 단계입니다. Hyper-v 호스트에 Hyper-v vSwitch를 만듭니다

다음 이미지에서는 vSwitch를 사용 하 여 Hyper-v 호스트 1을 보여 줍니다.

![Hyper-v 가상 스위치 만들기](../../media/Converged-NIC/5-single-create-vswitch.jpg)


1. 1. Hyper-v 호스트에서 Hyper-v에 외부 Hyper-v vSwitch를 만듭니다 <p>이 예제에서는 스위치 VMSTEST 라고 합니다. 매개 변수 또한 **AllowManagementOS** 실제 NIC의 MAC 및 IP 주소를 상속 하는 호스트 vNIC를 만듭니다

   ```PowerShell
   New-VMSwitch -Name VMSTEST -NetAdapterName "M1" -AllowManagementOS $true
   ```
   _**결과:** _


   |  이름   | SwitchType |      NetAdapterInterfaceDescription      |
   |---------|------------|------------------------------------------|
   | VMSTEST |  외부  | Mellanox connectx-3 Pro 이더넷 어댑터 |

   ---

2. 네트워크 어댑터 속성을 봅니다.

   ```PowerShell
   Get-NetAdapter | ft -AutoSize
   ```

   _**결과:** _


   |         이름          |        InterfaceDescription         | ifIndex | 상태 |    MacAddress     | LinkSpeed |
   |-----------------------|-------------------------------------|---------|--------|-------------------|-----------|
   | vEthernet \(VMSTEST\) | Hyper-v 가상 이더넷 어댑터 #2 |   27    |   위쪽   | E4-1D-2D-07-40-71 |  40gbps  |

   ---

3. 두 가지 방법 중 하나에서 호스트 vNIC를 관리 합니다. 

   - **NetAdapter** 뷰를 기반으로 작동 하는 "vEthernet \(VMSTEST\)" 이름입니다. 네트워크 어댑터 속성 중 일부만이 뷰에 표시 됩니다.
   - **VMNetworkAdapter** 보기 "vEthernet" 접두사를 삭제 하 고 단순히 vmswitch 이름을 사용 합니다. 좋습니다. 

   ```PowerShell
   Get-VMNetworkAdapter –ManagementOS | ft -AutoSize
   ```

   _**결과:** _


   |         이름         | IsManagementOs |        VMName        |  SwitchName  | MacAddress | 상태 | IPAddresses |
   |----------------------|----------------|----------------------|--------------|------------|--------|-------------|
   | CORP 외부 전환 |      True      | CORP 외부 전환 | 001B785768AA |    {확인}    | &nbsp; |             |
   |       VMSTEST        |      True      |       VMSTEST        | E41D2D074071 |    {확인}    | &nbsp; |             |

   ---

4. 연결을 테스트 합니다.

   ```Powershell    
   Test-NetConnection 192.168.1.5
   ```

   _**결과:** _ 

   ```
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (CORP-External-Switch)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
   ```

5. 할당 하 고 네트워크 어댑터가 VLAN 설정을 확인 합니다.

   ```PowerShell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "VMSTEST" -VlanId "101" -Access -ManagementOS
   Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName "VMSTEST"
   ```    

   _**결과:** _


   | VMName | VMNetworkAdapterName |  모드  | VlanList |
   |--------|----------------------|--------|----------|
   | &nbsp; |       VMSTEST        | 액세스 권한 |   101    |

   ---  

6. 연결을 테스트 합니다.<p>다른 어댑터를 성공적으로 ping 할 수 전에 완료 하는 데 몇 초 정도 걸립니다.  

   ```PowerShell    
   Test-NetConnection 192.168.1.5
   ```

   _**결과:** _

   ```
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (VMSTEST)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
   ```

## <a name="step-9-test-hyper-v-virtual-switch-rdma-mode-2"></a>9단계: Hyper-v 가상 스위치 RDMA (모드 2)를 테스트 합니다.

다음 그림은 Hyper-v 호스트 1에서 vSwitch를 포함 하 여 Hyper-v 호스트의 현재 상태를 보여 줍니다.

![Hyper-v 가상 스위치를 테스트 합니다.](../../media/Converged-NIC/6-single-test-vswitch-rdma.jpg)


1. 호스트 vNIC에 태그를 지정 하는 우선 순위를 설정 합니다.

   ```PowerShell    
   Set-VMNetworkAdapter -ManagementOS -Name "VMSTEST" -IeeePriorityTag on
   Get-VMNetworkAdapter -ManagementOS -Name "VMSTEST" | fl Name,IeeePriorityTag
   ```  

   _**결과:** _

    이름: VMSTEST IeeePriorityTag: 켜짐


2. 네트워크 어댑터가 RDMA 정보를 봅니다. 

   ```PowerShell
   Get-NetAdapterRdma
   ```   

   _**결과:** _


   |         이름          |        InterfaceDescription         | Enabled |
   |-----------------------|-------------------------------------|---------|
   | vEthernet \(VMSTEST\) | Hyper-v 가상 이더넷 어댑터 #2 |  False  |

   ---

   >[!NOTE]
   >경우 매개 변수 **Enabled** 기본값이 **False**, RDMA는 사용 하지 않음을 의미 합니다.


3. 네트워크 어댑터 정보를 봅니다.

   ```PowerShell
   Get-NetAdapter
   ```

   _**결과:** _   


   |        이름         |        InterfaceDescription         | ifIndex | 상태 |    MacAddress     | LinkSpeed |
   |---------------------|-------------------------------------|---------|--------|-------------------|-----------|
   | vEthernet (VMSTEST) | Hyper-v 가상 이더넷 어댑터 #2 |   27    |   위쪽   | E4-1D-2D-07-40-71 |  40gbps  |

   ---


4. 호스트 vNIC에서 RDMA를 사용 하도록 설정 합니다.

   ```PowerShell
   Enable-NetAdapterRdma -Name "vEthernet (VMSTEST)"
   Get-NetAdapterRdma -Name "vEthernet (VMSTEST)"
   ```

   _**결과:** _


   |         이름          |        InterfaceDescription         | Enabled |
   |-----------------------|-------------------------------------|---------|
   | vEthernet \(VMSTEST\) | Hyper-v 가상 이더넷 어댑터 #2 |  True   |

   ---

   >[!NOTE]
   >경우 매개 변수 **Enabled** 기본값이 **True**, RDMA를 사용할 수 있음을 의미 합니다.

5. RDMA 트래픽 테스트를 수행 합니다.

   ```PowerShell    
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
   ```

이 출력의 마지막 줄에서는 "RDMA 트래픽 테스트 성공 합니다. RDMA 트래픽 192.168.1.5, 전송 된"어댑터에서 수렴 된 NIC를 성공적으로 구성 있는지 보여 줍니다.

## <a name="related-topics"></a>관련 항목
- [수렴 형 된 NIC 팀으로 구성 된 NIC 구성](cnic-datacenter.md)
- [수렴 형 된 NIC에 대 한 물리적 스위치 구성](cnic-app-switch-config.md)
- [수렴 형 NIC 구성 문제 해결](cnic-app-troubleshoot.md)
