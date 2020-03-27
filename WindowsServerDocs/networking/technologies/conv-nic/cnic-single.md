---
title: 단일 네트워크 어댑터를 사용 하 여 수렴 형 NIC 구성
description: 이 항목에서는 Hyper-v 호스트에서 단일 NIC를 사용 하 여 수렴 형 NIC를 구성 하는 지침을 제공 합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: eed5c184-fa55-43a8-a879-b1610ebc70ca
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/14/2018
ms.openlocfilehash: 5a088df043190de9e7f1df4dccdc2fc832751093
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309628"
---
# <a name="converged-nic-configuration-with-a-single-network-adapter"></a>단일 네트워크 어댑터를 사용 하 여 수렴 형 NIC 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 Hyper-v 호스트에서 단일 NIC를 사용 하 여 수렴 형 NIC를 구성 하는 지침을 제공 합니다.

이 항목의 예제 구성에서는 두 개의 Hyper-v 호스트, **Hyper-v 호스트 A**및 **hyper-v 호스트 B**에 대해 설명 합니다. 두 호스트에 모두 단일 물리적 NIC (pNIC)가 설치 되어 있고 Nic가 랙 \(에 연결 되어\) 실제 스위치를 사용할 수 있습니다. 또한 호스트는 192.168.1/24와 동일한 서브넷에 있습니다.

![Hyper-V 호스트](../../media/Converged-NIC/1-single-test-conn.jpg)


## <a name="step-1-test-the-connectivity-between-source-and-destination"></a>1단계. 원본 및 대상 간의 연결 테스트

실제 NIC가 대상 호스트에 연결할 수 있는지 확인 합니다. 이 테스트는 계층 3 \(L3\) 또는 IP 계층을 사용 하 여 연결을 보여 주며 L2\)\(

1. 네트워크 어댑터 속성을 봅니다.

   ```PowerShell
   Get-NetAdapter
   ```

   _**검색**_  


   | 이름 |    인터페이스 설명     | ifIndex | 상태 |    MacAddress     | /%Linkspeed |
   |------|-----------------------------|---------|--------|-------------------|-----------|
   |  M 1  | Mellanox Connectx-3-3 Pro ... |    4    |   위로   | 7C-FE-90-8F-A1 |  40 Gbps  |

   ---

2. IP 주소를 포함 하 여 추가 어댑터 속성을 봅니다.

   ```PowerShell
   Get-NetAdapter M1 | fl *
   ```

   _**검색**_

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

## <a name="step-2-ensure-that-source-and-destination-can-communicate"></a>2단계. 원본 및 대상이 통신할 수 있는지 확인 합니다.

이 단계에서는 **테스트-NetConnection** Windows PowerShell 명령을 사용 하지만 원하는 경우 **ping** 명령을 사용할 수 있습니다. 

>[!TIP]
>호스트가 서로 통신할 수 있는 것이 확실 한 경우이 단계를 건너뛸 수 있습니다.

1. 양방향 통신을 확인 합니다.

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**검색**_


   |        매개 변수         |    값    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.1.5 |
   |      RemoteAddress       | 192.168.1.5 |
   |      InterfaceAlias      |     M 1      |
   |      SourceAddress       | 192.168.1.3 |
   |      이상 성공       |    True     |
   | PingReplyDetails \(RTT\) |    0 밀리초     |

   ---

   경우에 따라이 테스트를 성공적으로 수행 하려면 고급 보안이 포함 된 Windows 방화벽을 사용 하지 않도록 설정 해야 할 수도 있습니다. 방화벽을 사용 하지 않도록 설정 하는 경우 보안을 염두에 두고 구성이 조직의 보안 요구 사항을 충족 하는지 확인 합니다.

2. 모든 방화벽 프로필을 사용 하지 않도록 설정 합니다.

   ```PowerShell
   Set-NetFirewallProfile -All -Enabled False
   ```

3. 방화벽 프로필을 사용 하지 않도록 설정한 후에는 연결을 다시 테스트 하십시오. 

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**검색**_


   |        매개 변수         |    값    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.1.5 |
   |      RemoteAddress       | 192.168.1.5 |
   |      InterfaceAlias      | 40G-1  |
   |      SourceAddress       | 192.168.1.3 |
   |      이상 성공       |    False    |
   | PingReplyDetails \(RTT\) |    0 밀리초     |

   ---



## <a name="step-3-optional-configure-the-vlan-ids-for-nics-installed-in-your-hyper-v-hosts"></a>3단계. 필드 Hyper-v 호스트에 설치 된 Nic에 대 한 VLAN Id 구성

많은 네트워크 구성에서 Vlan을 사용 하며, 네트워크에서 Vlan을 사용 하려는 경우 Vlan을 구성 하 여 이전 테스트를 반복 해야 합니다. 또한 RDMA 서비스에 RoCE를 사용 하려는 경우 Vlan을 사용 하도록 설정 해야 합니다.

이 단계에서는 Nic가 **액세스** 모드입니다. 그러나이 가이드의 뒷부분에서 Hyper-v 가상 스위치 \(vSwitch\)를 만들 때 VLAN 속성은 vSwitch 포트 수준에서 적용 됩니다. 

스위치는 여러 Vlan을 호스트할 수 있으므로, 랙 \(에\) 물리적 스위치를 설정 하 여 호스트가 트렁크 모드에서 구성 된 포트를 갖도록 해야 합니다.

>[!NOTE]
>스위치에서 트렁크 모드를 구성 하는 방법에 대 한 지침은 해당 하는 스위치 설명서를 참조 하세요.

다음 이미지는 각각 하나의 실제 네트워크 어댑터를 사용 하 고 VLAN 101에서 통신 하도록 구성 된 두 개의 Hyper-v 호스트를 보여 줍니다.

![가상 로컬 영역 네트워크 구성](../../media/Converged-NIC/2-single-configure-vlans.jpg)


>[!IMPORTANT]
>로컬 및 대상 서버에서 모두이를 수행 합니다. 대상 서버가 로컬 서버와 동일한 VLAN ID를 사용 하 여 구성 되지 않은 경우 두 서버는 통신할 수 없습니다.


1. Hyper-v 호스트에 설치 된 Nic에 대 한 VLAN ID를 구성 합니다.

   >[!IMPORTANT]
   >이 인터페이스를 통해 원격으로 호스트에 연결 된 경우에는이 명령을 실행 하지 마십시오. 이렇게 하면 호스트에 대 한 액세스가 손실 됩니다.

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name M1 -RegistryKeyword VlanID -RegistryValue "101"
   Get-NetAdapterAdvancedProperty -Name M1 | Where-Object {$_.RegistryKeyword -eq "VlanID"} 
   ```

   _**검색**_


   | 이름 | DisplayName | DisplayValue | RegistryKeyword | RegistryValue |
   |------|-------------|--------------|-----------------|---------------|
   |  M 1  |   VLAN ID   |     101      |     VlanID      |     {101}     |

   ---

2. 네트워크 어댑터를 다시 시작 하 여 VLAN ID를 적용 합니다.

   ```PowerShell
   Restart-NetAdapter -Name "M1"
   ```

3. 상태가 **Up**인지 확인 합니다.

   ```PowerShell
   Get-NetAdapter -Name "M1"
   ```

   _**검색**_


   | 이름 |          인터페이스 설명           | ifIndex | 상태 |    MacAddress     | /%Linkspeed |
   |------|-----------------------------------------|---------|--------|-------------------|-----------|
   |  M 1  | Mellanox Connectx-3 Pro 이더넷 Ada ... |    4    |   위로   | 7C-FE-90-8F-A1 |  40 Gbps  |

   ---

   >[!IMPORTANT]
   >장치가 다시 시작 되 고 네트워크에서 사용할 수 있게 되는 데 몇 초 정도 걸릴 수 있습니다. 

4. 연결을 확인 합니다.<p>연결에 실패 하면 동일한 VLAN의 스위치 VLAN 구성 또는 대상 참여를 검사 합니다. 

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

## <a name="step-4-configure-quality-of-service-qos"></a>4단계. QoS\) 서비스 품질 \(구성

>[!NOTE]
>서로 통신 하는 모든 호스트에서 다음 DCB 및 QoS 구성 단계를 모두 수행 해야 합니다.

1. 각 Hyper-v 호스트에 데이터 센터 브리징 \(DCB\)를 설치 합니다.

   - RDMA 서비스용 iWarp을 사용 하는 네트워크 구성의 경우 **선택 사항** 입니다.
   - RoCE를 사용 하는 네트워크 구성 \(RDMA 서비스용 모든 버전\) **필요** 합니다.

   ```PowerShell
   Install-WindowsFeature Data-Center-Bridging
   ```

2. SMB 다이렉트에 대 한 QoS 정책을 설정 합니다.

   - IWarp를 사용 하는 네트워크 구성의 경우 **선택 사항** 입니다.
   - RoCE를 사용 하는 네트워크 구성에 **필요** 합니다.

   아래 예제 명령에서 값 "3"은 임의입니다. QoS 정책 구성에서 동일한 값을 일관 되 게 사용 하는 한 1에서 7 사이의 모든 값을 사용할 수 있습니다.

   ```PowerShell
   New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3
   ```

   _**검색**_


   |   매개 변수    |          값           |
   |----------------|--------------------------|
   |      이름      |           SMB            |
   |     소유자      | 그룹 정책 \(Machine\) |
   | NetworkProfile |           모두            |
   |   우선 순위   |           127            |
   |   JobObject    |          &nbsp;          |
   | NetDirectPort  |           445            |
   | PriorityValue  |            3             |

   ---

3. RoCE 배포의 경우 SMB 트래픽에 대해 **우선 순위 흐름 제어** 를 설정 합니다 .이는 iWarp에 필요 하지 않습니다.

   ```PowerShell
   Enable-NetQosFlowControl -priority 3
   Get-NetQosFlowControl
   ```

   _**검색**_


   | Priority | 사용 | PolicySet | ifIndex | IfAlias |
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

4. 로컬 및 대상 네트워크 어댑터에 대 한 QoS를 사용 하도록 설정 합니다.

   - IWarp를 사용 하는 네트워크 구성에는 **필요 하지 않습니다** .
   - RoCE를 사용 하는 네트워크 구성에 **필요** 합니다.

   ```PowerShell
   Enable-NetAdapterQos -InterfaceAlias "M1"
   Get-NetAdapterQos -Name "M1"
   ```

   _**검색**_

   **이름**: M1  
   **사용**: True  

   _**역량**_   


   |      매개 변수      |   하드웨어   |   현재    |
   |---------------------|--------------|--------------|
   |    MacSecBypass     | NotSupported | NotSupported |
   |     DcbxSupport     |     없음     |     없음     |
   | NumTCs (Max/PFC/) |    8/8/8     |    8/8/8     |

   ---

   _**OperationalTrafficClasses:**_ 


   | 간체 | TSA의 | 대역 | 우선순위 |
   |----|-----|-----------|------------|
   | 0  | 요소가 |    70%    |  0-2, 4-7   |
   | 1  | 요소가 |    인치    |     3      |

   ---

   _**OperationalFlowControl:**_  

   우선 순위 3 사용  

   _**OperationalClassifications:**_  


   | 프로토콜  | 포트/유형 | Priority |
   |-----------|-----------|----------|
   |  기본  |  &nbsp;   |    0     |
   | NetDirect |    445    |    3     |

   ---

5. SMB 다이렉트 \(RDMA\)에 대 한 대역폭 비율을 예약 합니다.

    이 예에서는 30% 대역폭 예약이 사용 됩니다. 저장소 트래픽에 필요한 항목을 나타내는 값을 선택 해야 합니다. 

   ```PowerShell
   New-NetQosTrafficClass "SMB" -Priority 3 -BandwidthPercentage 30 -Algorithm ETS
   ```

   _**검색**_


   | 이름 | 알고리즘 | 대역폭 (%) | Priority | PolicySet | ifIndex | IfAlias |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | SMB  |    요소가    |      30      |    3     |  전역   | &nbsp;  | &nbsp;  |

   ---                                      

6. 대역폭 예약 설정을 봅니다.  

   ```PowerShell
   Get-NetQosTrafficClass
   ```

   _**검색**_


   |   이름    | 알고리즘 | 대역폭 (%) | Priority | PolicySet | ifIndex | IfAlias |
   |-----------|-----------|--------------|----------|-----------|---------|---------|
   | [기본값] |    요소가    |      70      | 0-2, 4-7  |  전역   | &nbsp;  | &nbsp;  |
   |    SMB    |    요소가    |      30      |    3     |  전역   | &nbsp;  | &nbsp;  |

   ---

## <a name="step-5-optional-resolve-the-mellanox-adapter-debugger-conflict"></a>5단계. 필드 Mellanox 어댑터 디버거 충돌 해결 

기본적으로 Mellanox 어댑터를 사용 하는 경우 연결 된 디버거는 알려진 문제인 NetQos를 차단 합니다. 따라서 Mellanox에서 어댑터를 사용 하 고 디버거를 연결 하려는 경우 다음 명령을 사용 하 여이 문제를 해결 합니다. 디버거를 연결 하지 않으려는 경우 또는 Mellanox 어댑터를 사용 하지 않는 경우에는이 단계가 필요 하지 않습니다.

   ```PowerShell    
   Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
   ``` 

## <a name="step-6-verify-the-rdma-configuration-native-host"></a>6단계. RDMA 구성 확인 (네이티브 호스트)

VSwitch를 만들고 RDMA (수렴 형 NIC)로 전환 하기 전에 패브릭이 올바르게 구성 되어 있는지 확인 하려고 합니다. 

다음 이미지는 Hyper-v 호스트의 현재 상태를 보여 줍니다.

![RDMA 테스트](../../media/Converged-NIC/4-single-test-rdma.jpg)

1. RDMA 구성을 확인 합니다.

   ```PowerShell
   Get-NetAdapterRdma
   ```
   _**검색**_


   | 이름 |           인터페이스 설명           | 사용 |
   |------|------------------------------------------|---------|
   |  M 1  | Mellanox Connectx-3 Pro 이더넷 어댑터 |  True   |

   ---

2. 대상 어댑터의 **ifIndex** 값을 확인 합니다.<p>다운로드 한 스크립트를 실행 하는 이후 단계에서이 값을 사용 합니다.

   ```PowerShell
   Get-NetIPConfiguration -InterfaceAlias "M*" | ft InterfaceAlias,InterfaceIndex,IPv4Address
   ```

   _**검색**_ 


   | InterfaceAlias | InterfaceIndex |  IPv4Address  |
   |----------------|----------------|---------------|
   |       M2       |       14       | 192.168.1.5 |

   ---

3. [Diskspd .exe 유틸리티](https://aka.ms/diskspd) 를 다운로드 하 고 C:\TEST로 압축을 풉니다\.

4. [테스트 RDMA powershell 스크립트](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1) 를 로컬 드라이브의 테스트 폴더 (예: C:\TEST\.에 다운로드 합니다.

5. **Test-Rdma** PowerShell 스크립트를 실행 하 여 ifIndex 값을 동일한 VLAN에 있는 원격 어댑터의 IP 주소와 함께 스크립트에 전달 합니다.<p>이 예제에서 스크립트는 원격 네트워크 어댑터 IP 주소 192.168.1.5에 **ifIndex** 값 14를 전달 합니다.

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
   >RDMA 트래픽이 실패 하는 경우 RoCE 케이스의 경우 호스트 설정과 일치 해야 하는 적절 한 PFC/설정에 대해 관련 스위치 구성을 참조 하세요. 참조 값은이 문서의 QoS 섹션을 참조 하세요.

## <a name="step-7-remove-the-access-vlan-setting"></a>7단계. 액세스 VLAN 설정 제거

Hyper-v 스위치를 만들기 위한 준비에서는 위에서 설치한 VLAN 설정을 제거 해야 합니다.  

1. NIC가 잘못 된 VLAN ID를 사용 하 여 송신 트래픽에 자동 태그를 지정 하는 것을 방지 하기 위해 실제 NIC에서 액세스 VLAN 설정을 제거 합니다.<p>또한이 설정을 제거 하면 액세스 VLAN ID와 일치 하지 않는 수신 트래픽을 필터링 할 수 없습니다.

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name M1 -RegistryKeyword VlanID -RegistryValue "0"
   ```    

2. **VlanID 설정** 에 VLAN ID 값이 0으로 표시 되는지 확인 합니다.

   ```PowerShell    
   Get-NetAdapterAdvancedProperty -name m1 | Where-Object {$_.RegistryKeyword -eq 'VlanID'} 
   ```  


## <a name="step-8-create-a-hyper-v-vswitch-on-your-hyper-v-hosts"></a>8단계. Hyper-v 호스트에서 Hyper-v vSwitch 만들기

다음 이미지는 vSwitch를 사용 하는 Hyper-v 호스트 1을 보여 줍니다.

![Hyper-v 가상 스위치 만들기](../../media/Converged-NIC/5-single-create-vswitch.jpg)


1. Hyper-v 호스트 A의 Hyper-v에서 외부 Hyper-v vSwitch를 만듭니다. <p>이 예에서는 스위치 이름이 VMSTEST입니다. 또한 **Allowmanagementos** 매개 변수는 실제 NIC의 MAC 및 IP 주소를 상속 하는 호스트 vNIC을 만듭니다.

   ```PowerShell
   New-VMSwitch -Name VMSTEST -NetAdapterName "M1" -AllowManagementOS $true
   ```
   _**검색**_


   |  이름   | SwitchType |      NetAdapterInterfaceDescription      |
   |---------|------------|------------------------------------------|
   | VMSTEST |  외부  | Mellanox Connectx-3 Pro 이더넷 어댑터 |

   ---

2. 네트워크 어댑터 속성을 봅니다.

   ```PowerShell
   Get-NetAdapter | ft -AutoSize
   ```

   _**검색**_


   |         이름          |        인터페이스 설명         | ifIndex | 상태 |    MacAddress     | /%Linkspeed |
   |-----------------------|-------------------------------------|---------|--------|-------------------|-----------|
   | vEthernet \(VMSTEST\) | Hyper-v 가상 이더넷 어댑터 #2 |   27    |   위로   | E4-1D-07-40-71 |  40 Gbps  |

   ---

3. 다음 두 가지 방법 중 하나로 호스트 vNIC를 관리 합니다. 

   - **Get-netadapter** view는 "vEthernet \(VMSTEST\)" 이름에 따라 작동 합니다. 모든 네트워크 어댑터 속성이이 보기에 표시 되는 것은 아닙니다.
   - **VMNetworkAdapter** view는 "vEthernet" 접두사를 삭제 하 고, vm 이름을 사용 하기만 하면 됩니다. 좋습니다. 

   ```PowerShell
   Get-VMNetworkAdapter –ManagementOS | ft -AutoSize
   ```

   _**검색**_


   |         이름         | IsManagementOs |        VMName        |  SwitchName  | MacAddress | 상태 | IPAddresses |
   |----------------------|----------------|----------------------|--------------|------------|--------|-------------|
   | CORP-외부 전환 |      True      | CORP-외부 전환 | 001B785768AA |    확인을    | &nbsp; |             |
   |       VMSTEST        |      True      |       VMSTEST        | E41D2D074071 |    확인을    | &nbsp; |             |

   ---

4. 연결을 테스트 합니다.

   ```Powershell    
   Test-NetConnection 192.168.1.5
   ```

   _**검색**_ 

   ```
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (CORP-External-Switch)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
   ```

5. 네트워크 어댑터 VLAN 설정을 할당 하 고 확인 합니다.

   ```PowerShell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "VMSTEST" -VlanId "101" -Access -ManagementOS
   Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName "VMSTEST"
   ```    

   _**검색**_


   | VMName | VMNetworkAdapterName |  모드  | VlanList |
   |--------|----------------------|--------|----------|
   | &nbsp; |       VMSTEST        | Access |   101    |

   ---  

6. 연결을 테스트 합니다.<p>다른 어댑터를 성공적으로 ping 하려면 완료 하는 데 몇 초 정도 걸릴 수 있습니다.  

   ```PowerShell    
   Test-NetConnection 192.168.1.5
   ```

   _**검색**_

   ```
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (VMSTEST)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
   ```

## <a name="step-9-test-hyper-v-virtual-switch-rdma-mode-2"></a>9단계. Hyper-v 가상 스위치 RDMA 테스트 (모드 2)

다음 이미지는 hyper-v 호스트 1의 vSwitch를 비롯 하 여 Hyper-v 호스트의 현재 상태를 보여 줍니다.

![Hyper-v 가상 스위치 테스트](../../media/Converged-NIC/6-single-test-vswitch-rdma.jpg)


1. 호스트 vNIC의 우선 순위 태그 지정을 설정 합니다.

   ```PowerShell    
   Set-VMNetworkAdapter -ManagementOS -Name "VMSTEST" -IeeePriorityTag on
   Get-VMNetworkAdapter -ManagementOS -Name "VMSTEST" | fl Name,IeeePriorityTag
   ```  

   _**검색**_

    이름: VMSTEST IeeePriorityTag: On


2. 네트워크 어댑터 RDMA 정보를 확인 합니다. 

   ```PowerShell
   Get-NetAdapterRdma
   ```   

   _**검색**_


   |         이름          |        인터페이스 설명         | 사용 |
   |-----------------------|-------------------------------------|---------|
   | vEthernet \(VMSTEST\) | Hyper-v 가상 이더넷 어댑터 #2 |  False  |

   ---

   >[!NOTE]
   >**사용할 수** 있는 매개 변수 값이 **False**이면 RDMA를 사용할 수 없음을 의미 합니다.


3. 네트워크 어댑터 정보를 확인 합니다.

   ```PowerShell
   Get-NetAdapter
   ```

   _**검색**_   


   |        이름         |        인터페이스 설명         | ifIndex | 상태 |    MacAddress     | /%Linkspeed |
   |---------------------|-------------------------------------|---------|--------|-------------------|-----------|
   | vEthernet (VMSTEST) | Hyper-v 가상 이더넷 어댑터 #2 |   27    |   위로   | E4-1D-07-40-71 |  40 Gbps  |

   ---


4. 호스트 vNIC RDMA를 사용 하도록 설정 합니다.

   ```PowerShell
   Enable-NetAdapterRdma -Name "vEthernet (VMSTEST)"
   Get-NetAdapterRdma -Name "vEthernet (VMSTEST)"
   ```

   _**검색**_


   |         이름          |        인터페이스 설명         | 사용 |
   |-----------------------|-------------------------------------|---------|
   | vEthernet \(VMSTEST\) | Hyper-v 가상 이더넷 어댑터 #2 |  True   |

   ---

   >[!NOTE]
   >**사용할 수** 있는 매개 변수 값이 **True**이면 RDMA를 사용할 수 있음을 의미 합니다.

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

이 출력의 마지막 줄 "RDMA 트래픽 테스트 성공: RDMA 트래픽이 192.168.1.5로 전송 되었습니다."는 어댑터에서 수렴 형 NIC를 성공적으로 구성 했음을 보여 줍니다.

## <a name="related-topics"></a>관련 항목
- [수렴 형 NIC 팀 NIC 구성](cnic-datacenter.md)
- [수렴 형 NIC에 대 한 물리적 스위치 구성](cnic-app-switch-config.md)
- [수렴 형 NIC 구성 문제 해결](cnic-app-troubleshoot.md)
