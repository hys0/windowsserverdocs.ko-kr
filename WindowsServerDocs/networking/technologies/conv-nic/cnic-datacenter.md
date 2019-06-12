---
title: NIC 팀 구성 (데이터 센터)에서 수렴 형 된 NIC
description: 이 항목에서는 제공 수렴 된 NIC는 NIC 팀 구성을 사용 하 여 스위치 포함 된 팀 (SET)에 배포 하기 위한 지침입니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f01546f8-c495-4055-8492-8806eee99862
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/17/2018
ms.openlocfilehash: 58c4483c092c30a892ea6bdde20794270340fa8e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447018"
---
# <a name="converged-nic-in-a-teamed-nic-configuration-datacenter"></a>NIC 팀 구성 (데이터 센터)에서 수렴 형 된 NIC

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 있습니다 NIC 팀 구성 스위치 포함 된 팀에서 수렴 된 NIC를 배포 하기 위한 지침 \(설정\)합니다. 

이 항목의 예제 구성은 두 Hyper-v 호스트를 설명 **Hyper-v 호스트 1** 하 고 **Hyper-v 호스트 2**합니다. 두 호스트에 2 개의 네트워크 어댑터입니다. 각 호스트에서 하나의 어댑터만 192.168.1.x/24 서브넷에 연결 되어 및 192.168.2.x/24 서브넷에 연결 되어 하나의 어댑터.

![Hyper-V 호스트](../../media/Converged-NIC/1-datacenter-test-conn.jpg)

## <a name="step-1-test-the-connectivity-between-source-and-destination"></a>1단계. 원본과 대상 간의 연결을 테스트

실제 NIC에 연결할 수 있도록 대상 호스트를 확인 합니다.  이 테스트 된 3 계층을 사용 하 여 연결을 보여 줍니다 \(L3\) -또는-IP 계층, 계층 2 뿐만 \(L2\) virtual local area network \(VLAN\)합니다.

1. 첫 번째 네트워크 어댑터 속성을 봅니다.

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```

   _**결과:** _


   |    이름    |           InterfaceDescription           | ifIndex | 상태 |    MacAddress     | LinkSpeed |
   |------------|------------------------------------------|---------|--------|-------------------|-----------|
   | Test-40G-1 | Mellanox connectx-3 Pro 이더넷 어댑터 |   11    |   위쪽   | E4-1D-2D-07-43-D0 |  40gbps  |

   ---

2. 첫 번째 어댑터의 경우 IP 주소를 포함 하 여 추가 속성을 봅니다. 

   ```PowerShell
   Get-NetIPAddress -InterfaceAlias "Test-40G-1"
   Get-NetIPAddress -InterfaceAlias "TEST-40G-1" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress
   ```

   _**결과:** _


   |   매개 변수    |    값    |
   |----------------|-------------|
   |   IP 주소    | 192.168.1.3 |
   | InterfaceIndex |     11      |
   | InterfaceAlias | Test-40G-1  |
   | AddressFamily  |    IPv4     |
   |      형식      |   유니캐스트   |
   |  PrefixLength  |     24      |

   ---

3. 두 번째 네트워크 어댑터 속성을 봅니다.

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-2" | ft -AutoSize
   ```

   _**결과:** _


   |    이름    |          InterfaceDescription           | ifIndex | 상태 |    MacAddress     | LinkSpeed |
   |------------|-----------------------------------------|---------|--------|-------------------|-----------|
   | TEST-40G-2 | Mellanox connectx-3 Pro 이더넷 A... #2 |   13    |   위쪽   | E4-1D-2D-07-40-70 |  40gbps  |

   ---

4. 두 번째 어댑터의 경우 IP 주소를 포함 하 여 추가 속성을 봅니다.

   ```PowerShell
   Get-NetIPAddress -InterfaceAlias "Test-40G-2"
   Get-NetIPAddress -InterfaceAlias "Test-40G-2" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress
   ```

   _**결과:** _


   |   매개 변수    |    값    |
   |----------------|-------------|
   |   IP 주소    | 192.168.2.3 |
   | InterfaceIndex |     13      |
   | InterfaceAlias | TEST-40G-2  |
   | AddressFamily  |    IPv4     |
   |      형식      |   유니캐스트   |
   |  PrefixLength  |     24      |

   ---

5. 다른 NIC 팀 또는 집합 멤버 pNICs 해당에 유효한 IP 주소를 확인 합니다.<p>별도 서브넷을 사용 하 여 \(xxx.xxx. **2**.xxx vs xxx.xxx. **1**.xxx\),이 어댑터에서 대상으로 보낼 수 있도록 합니다. 이 고, 그렇지를 동일한 서브넷에 모두 pNICs을 찾으면 Windows TCP/IP 스택을 부하를 분산 하는 인터페이스 간에 및 간단한 유효성 검사 더 복잡해 집니다.


## <a name="step-2-ensure-that-source-and-destination-can-communicate"></a>2단계. 원본 및 대상 통신할 수 있는지 확인

이 단계에서는 사용 하 여는 **Test-netconnection** Windows PowerShell 명령을 사용할 수 있습니다 하지만 **ping** 원할 경우 명령. 

1. 양방향 통신을 확인 합니다.

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


4. 추가 Nic에 대 한 연결을 확인 합니다. NIC 또는 집합 팀에 포함 된 모든 후속 pNICs에 대해 이전 단계를 반복 합니다.

   ```PowerShell    
   Test-NetConnection 192.168.2.5
   ```

   _**결과:** _


   |        매개 변수         |    값    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.2.5 |
   |      RemoteAddress       | 192.168.2.5 |
   |      InterfaceAlias      | 테스트-40 G-2  |
   |      SourceAddress       | 192.168.2.3 |
   |      PingSucceeded       |    False    |
   | PingReplyDetails \(RTT\) |    0ms     |

   ---

## <a name="step-3-configure-the-vlan-ids-for-nics-installed-in-your-hyper-v-hosts"></a>3단계. Hyper-v 호스트에 설치 하는 Nic에 대 한 VLAN Id를 구성 합니다.

다양 한 네트워크 구성 Vlan을 사용 하 고 네트워크에 Vlan을 사용 하려는 경우 구성 하는 Vlan을 사용 하 여 이전 테스트를 반복 해야 합니다.

Nic가 있는이 단계에서는 **액세스** 모드입니다. 그러나 Hyper-v 가상 스위치를 만들 때 \(vSwitch\) VLAN 속성을이 가이드의 뒷부분에 나오는 vSwitch 포트 수준에서 적용 됩니다. 

위쪽의 랙에 해야 하는 스위치를 여러 Vlan을 호스팅할 수, 있으므로 \(ToR\) 물리적 스위치 포트를 트렁크 모드로 구성 된 호스트에 연결 되어 있어야 합니다.

>[!NOTE]
>스위치에 트렁크 모드를 구성 하는 방법에 대 한 지침은 ToR 스위치 설명서를 참조 하십시오.

다음 이미지는 각 VLAN 101 및 있는 네트워크 어댑터 속성에 구성 된 VLAN 102는 두 개의 네트워크 어댑터를 사용 하 여 두 Hyper-v 호스트를 보여줍니다.

![Virtual local area network 구성](../../media/Converged-NIC/2-datacenter-configure-vlans.jpg)


>[!TIP]
>에 따라 Institute of Electrical and Electronics Engineers \(IEEE\) 서비스의 품질 표준 네트워킹 \(QoS\) 실제 NIC에는 속성 포함 된 802.1p 헤더에서 작동 내는 802.1Q \(VLAN\) VLAN ID를 구성할 때 헤더

1. 첫 번째 NIC를 테스트-40 G-1에서 VLAN ID를 구성 합니다.

   ```PowerShell    
   Set-NetAdapterAdvancedProperty -Name "Test-40G-1" -RegistryKeyword VlanID -RegistryValue "101"
   Get-NetAdapterAdvancedProperty -Name "Test-40G-1" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
   ```

   _**결과:** _   


   |    이름    | DisplayName | DisplayValue | RegistryKeyword | RegistryValue |
   |------------|-------------|--------------|-----------------|---------------|
   | TEST-40G-1 |   VLAN ID   |     101      |     VlanID      |     {101}     |

   ---

2. 네트워크 어댑터에 VLAN ID를 적용 하려면 다시 시작

   ```PowerShell
   Restart-NetAdapter -Name "Test-40G-1"
   ```

3. 상태 확인 **등록**합니다.

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```

   _**결과:** _


   |    이름    |          InterfaceDescription           | ifIndex | 상태 |    MacAddress     | LinkSpeed |
   |------------|-----------------------------------------|---------|--------|-------------------|-----------|
   | Test-40G-1 | Mellanox connectx-3 Pro 이더넷 Ada... |   11    |   위쪽   | E4-1D-2D-07-43-D0 |  40gbps  |

   ---

4. 두 번째 NIC 테스트-40 G-2에서 VLAN ID를 구성 합니다.

   ```PowerShell    
   Set-NetAdapterAdvancedProperty -Name "Test-40G-2" -RegistryKeyword VlanID -RegistryValue "102"
   Get-NetAdapterAdvancedProperty -Name "Test-40G-2" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
   ``` 

   _**결과:** _


   |    이름    | DisplayName | DisplayValue | RegistryKeyword | RegistryValue |
   |------------|-------------|--------------|-----------------|---------------|
   | TEST-40G-2 |   VLAN ID   |     102      |     VlanID      |     {102}     |

   ---

5. 네트워크 어댑터에 VLAN ID를 적용 하려면 다시 시작

   ```PowerShell
   Restart-NetAdapter -Name "Test-40G-2" 
   ```

6. 상태 확인 **등록**합니다.

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```

   _**결과:** _


   |    이름    |          InterfaceDescription           | ifIndex | 상태 |    MacAddress     | LinkSpeed |
   |------------|-----------------------------------------|---------|--------|-------------------|-----------|
   | 테스트-40 G-2 | Mellanox connectx-3 Pro 이더넷 Ada... |   11    |   위쪽   | E4-1D-2D-07-43-D1 |  40gbps  |

   ---

   >[!IMPORTANT]
   >다시 시작 하 고 네트워크에서 사용할 수 있게 하는 장치에 대 한 초가 걸릴 수 있습니다. 

7. 첫 번째 NIC를 테스트-40 G-1에 대 한 연결을 확인 합니다.<p>연결에 실패 하면 동일한 VLAN의 VLAN 구성 또는 대상 참여 스위치를 검사 합니다. 

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**결과:** _   


   |        매개 변수         |    값    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.1.5 |
   |      RemoteAddress       | 192.168.1.5 |
   |      InterfaceAlias      | Test-40G-1  |
   |      SourceAddress       | 192.168.1.5 |
   |      PingSucceeded       |    True     |
   | PingReplyDetails \(RTT\) |    0ms     |

   ---

8. 첫 번째 NIC를 테스트-40 G-2에 대 한 연결을 확인 합니다.<p>연결에 실패 하면 동일한 VLAN의 VLAN 구성 또는 대상 참여 스위치를 검사 합니다.

   ```PowerShell    
   Test-NetConnection 192.168.2.5
   ```

   _**결과:** _    


   |        매개 변수         |    값    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.2.5 |
   |      RemoteAddress       | 192.168.2.5 |
   |      InterfaceAlias      | 테스트-40 G-2  |
   |      SourceAddress       | 192.168.2.3 |
   |      PingSucceeded       |    True     |
   | PingReplyDetails \(RTT\) |    0ms     |

   ---

   >[!IMPORTANT]
   >도 드물지 않습니다를 **Test-netconnection** 또는 ping 실패를 수행한 후에 즉시 되려면 **다시 시작 NetAdapter**합니다.  따라서 네트워크 어댑터를 완전히 초기화 완료 될 때까지 기다린 후 다시 시도 하십시오.
   >
   >VLAN 101 연결할 VLAN 102 연결 하지 않습니다 하지만 스위치 원하는 VLAN에서 포트 트래픽을 허용 하도록 구성 해야 하는 문제 수 있습니다. 일시적으로 실패 한 어댑터를 VLAN 101로 설정 하 고 연결 테스트를 반복 하 여이 확인할 수 있습니다.


   다음 이미지는 성공적으로 Vlan을 구성한 후 Hyper-v 호스트를 보여줍니다.

   ![서비스 품질 구성](../../media/Converged-NIC/3-datacenter-configure-qos.jpg)


## <a name="step-4-configure-quality-of-service-qos"></a>4단계. 서비스 품질 구성 \(QoS\)

>[!NOTE]
>서로 통신 하려는 모든 호스트에서 모든 다음 DCB 및 QoS 구성 단계를 수행 해야 합니다.

1. 데이터 센터 브리징 설치할 \(DCB\) 각 Hyper-v 호스트.

   - **선택적** iWarp를 사용 하는 네트워크 구성에 대 한 합니다.
   - **필요한** RoCE를 사용 하는 네트워크 구성에 대 한 \(버전일\) RDMA 서비스에 대 한 합니다.

   ```PowerShell
   Install-WindowsFeature Data-Center-Bridging
   ```

   _**결과:** _


   | 성공 | 다시 시작 필요 | 종료 코드 |     기능 결과     |
   |---------|----------------|-----------|------------------------|
   |  True   |       아니오       |  성공  | {0} 데이터 센터 브리징} |

   ---

2. SMB 다이렉트에 대 한 QoS 정책을 설정 합니다.

   - **선택적** iWarp를 사용 하는 네트워크 구성에 대 한 합니다.
   - **필요한** RoCE를 사용 하는 네트워크 구성에 대 한 \(버전일\) RDMA 서비스에 대 한 합니다.

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

3. 인터페이스에서 다른 트래픽에 대 한 추가 QoS 정책을 설정 합니다.   

   ```PowerShell
   New-NetQosPolicy "DEFAULT" -Default -PriorityValue8021Action 0
   ```

   _**결과:** _   


   |   매개 변수    |          값           |
   |----------------|--------------------------|
   |      이름      |         DEFAULT          |
   |     소유자      | 그룹 정책 \(컴퓨터\) |
   | NetworkProfile |           All            |
   |   우선 순위   |           127            |
   |    템플릿    |         기본값          |
   |   JobObject    |          &nbsp;          |
   | PriorityValue  |            0             |

   ---

4. 켜기 **우선 순위 흐름 제어** iWarp 필요 없는 SMB 트래픽입니다.

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

   >**중요** 결과 3 외에 다른 항목을 사용 값이 true 때문에 이러한 결과 일치 하지 않으면를 해제 해야 합니다 **흐름 제어** 이러한 클래스에 대 한 합니다.
   >
   >```PowerShell
   >Disable-NetQosFlowControl -priority 0,1,2,4,5,6,7
   >Get-NetQosFlowControl
   >```
   >더 복잡 한 구성에서 이러한 시나리오는이 가이드에서 다루지 않지만 다른 트래픽 클래스 흐름 제어에 필요할 수 있습니다.


5. 첫 번째 NIC를 테스트-40 G-1에 대 한 QoS를 사용 합니다.

   ```PowerShell
   Enable-NetAdapterQos -InterfaceAlias "Test-40G-1"
   Get-NetAdapterQos -Name "Test-40G-1"

   Name: TEST-40G-1 
   Enabled: True
   ```
   _**기능**:_   


   |      매개 변수      |   하드웨어   |   현재    |
   |---------------------|--------------|--------------|
   |    MacSecBypass     | NotSupported | NotSupported |
   |     DcbxSupport     |     없음     |     없음     |
   | NumTCs(Max/ETS/PFC) |    8/8/8     |    8/8/8     |

   ---

   _**OperationalTrafficClasses**:_    


   | TC |  TSA   | 대역폭 | 우선 순위 |
   |----|--------|-----------|------------|
   | 0  | 높음 |  &nbsp;   |    0-7     |

   ---

   _**OperationalFlowControl**:_  

   우선 순위 3 사용 하도록 설정  

   _**OperationalClassifications**:_  


   | Protocol  | 포트/유형 | Priority |
   |-----------|-----------|----------|
   |  기본값  |  &nbsp;   |    0     |
   | NetDirect |    445    |    3     |

   ---

6. 두 번째 NIC 테스트-40 G-2에 대 한 QoS를 사용 합니다.

   ```PowerShell
   Enable-NetAdapterQos -InterfaceAlias "Test-40G-2"
   Get-NetAdapterQos -Name "Test-40G-2"

   Name: TEST-40G-2 
   Enabled: True 
   ```

   _**기능**:_ 


   |      매개 변수      |   하드웨어   |   현재    |
   |---------------------|--------------|--------------|
   |    MacSecBypass     | NotSupported | NotSupported |
   |     DcbxSupport     |     없음     |     없음     |
   | NumTCs(Max/ETS/PFC) |    8/8/8     |    8/8/8     |

   ---

   _**OperationalTrafficClasses**:_  


   | TC |  TSA   | 대역폭 | 우선 순위 |
   |----|--------|-----------|------------|
   | 0  | 높음 |  &nbsp;   |    0-7     |

   ---

    _**OperationalFlowControl**:_  

    우선 순위 3 사용 하도록 설정  

   _**OperationalClassifications**:_  


   | Protocol  | 포트/유형 | Priority |
   |-----------|-----------|----------|
   |  기본값  |  &nbsp;   |    0     |
   | NetDirect |    445    |    3     |

   ---


7. SMB 다이렉트에 대 한 절반 대역폭 예약 \(RDMA\)

   ```PowerShell
   New-NetQosTrafficClass "SMB" -priority 3 -bandwidthpercentage 50 -algorithm ETS
   ```

   _**결과:** _  


   | 이름 | 알고리즘 | Bandwidth(%) | Priority | PolicySet | IfIndex | IfAlias |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | SMB  |    ETS    |      50      |    3     |  전역   | &nbsp;  | &nbsp;  |

   ---

8. 대역폭 예약 설정을 봅니다.   

   ```PowerShell
   Get-NetQosTrafficClass | ft -AutoSize
   ```

   _**결과:** _  


   |   이름    | 알고리즘 | Bandwidth(%) | Priority | PolicySet | IfIndex | IfAlias |
   |-----------|-----------|--------------|----------|-----------|---------|---------|
   | [기본값] |    ETS    |      50      | 0-2,4-7  |  전역   | &nbsp;  | &nbsp;  |
   |    SMB    |    ETS    |      50      |    3     |  전역   | &nbsp;  | &nbsp;  |

   ---

9. (선택 사항) 테 넌 트 IP 트래픽에 대 한 두 개의 추가 트래픽 클래스를 만듭니다. 

   >[!TIP]
   >"IP1" 및 "IP2" 값을 생략할 수 있습니다.

   ```PowerShell
   New-NetQosTrafficClass "IP1" -Priority 1 -bandwidthpercentage 10 -algorithm ETS
   ```

   _**결과:** _


   | 이름 | 알고리즘 | Bandwidth(%) | Priority | PolicySet | IfIndex | IfAlias |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | IP1  |    ETS    |      10      |    1     |  전역   | &nbsp;  | &nbsp;  |

   ---

   ```PowerShell
   New-NetQosTrafficClass "IP2" -Priority 2 -bandwidthpercentage 10 -algorithm ETS
   ```

   _**결과:** _


   | 이름 | 알고리즘 | Bandwidth(%) | Priority | PolicySet | IfIndex | IfAlias |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | IP2  |    ETS    |      10      |    2     |  전역   | &nbsp;  | &nbsp;  |

   ---

10. QoS 트래픽 클래스를 봅니다.

    ```PowerShell
    Get-NetQosTrafficClass | ft -AutoSize
    ```

    _**결과:** _


    |   이름    | 알고리즘 | Bandwidth(%) | Priority | PolicySet | IfIndex | IfAlias |
    |-----------|-----------|--------------|----------|-----------|---------|---------|
    | [기본값] |    ETS    |      30      |  0,4-7   |  전역   | &nbsp;  | &nbsp;  |
    |    SMB    |    ETS    |      50      |    3     |  전역   | &nbsp;  | &nbsp;  |
    |    IP1    |    ETS    |      10      |    1     |  전역   | &nbsp;  | &nbsp;  |
    |    IP2    |    ETS    |      10      |    2     |  전역   | &nbsp;  | &nbsp;  |

    ---

11. (선택 사항) 디버거를 재정의 합니다.<p>기본적으로 연결된 된 디버거에 NetQos를 차단합니다. 

    ```PowerShell
    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
    Get-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" | ft AllowFlowControlUnderDebugger
    ```

    _**결과:** _  

    ```
    AllowFlowControlUnderDebugger
    -----------------------------
    1
    ```

## <a name="step-5-verify-the-rdma-configuration-mode-1"></a>5단계. RDMA 구성 확인 \(모드 1\) 

패브릭 vSwitch를 만들고 RDMA를 전환 하기 전에 올바르게 구성 되어 있는지 확인 하려고 \(모드 2\)합니다.

다음 이미지는 Hyper-v 호스트의 현재 상태를 표시 합니다.

![RDMA 테스트](../../media/Converged-NIC/4-datacenter-test-rdma.jpg)


1. RDMA 구성을 확인 합니다.

   ```PowerShell
   Get-NetAdapterRdma | ft -AutoSize
   ```

   _**결과:** _


   |    이름    |        InterfaceDescription        | Enabled |
   |------------|------------------------------------|---------|
   | TEST-40G-1 | Mellanox ConnectX 4 VPI 어댑터 #2 |  True   |
   | TEST-40G-2 |  Mellanox ConnectX 4 VPI 어댑터   |  True   |

   ---

2. 확인 합니다 **ifIndex** 대상 어댑터의 값입니다.<p>다운로드 한 스크립트를 실행할 때 이후 단계에서이 값을 사용 합니다.   

   ```PowerShell
   Get-NetIPConfiguration -InterfaceAlias "TEST*" | ft InterfaceAlias,InterfaceIndex,IPv4Address
   ```

   _**결과:** _


   | InterfaceAlias | InterfaceIndex |  IPv4Address  |
   |----------------|----------------|---------------|
   |   TEST-40G-1   |       14       | {192.168.1.3} |
   |   TEST-40G-2   |       13       | {192.168.2.3} |

   ---

3. 다운로드 합니다 [DiskSpd.exe 유틸리티](https://aka.ms/diskspd) C:\TEST를 추출 하 고\.

4. 다운로드 합니다 [테스트 RDMA PowerShell 스크립트](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1) C:\TEST 예를 들어, 로컬 드라이브에서 테스트 폴더\.

5. 실행 합니다 **테스트 Rdma.ps1** PowerShell 스크립트를 스크립트에 동일한 VLAN에 있는 첫 번째 원격 어댑터의 IP 주소와 함께 ifIndex 값을 전달 합니다.<p>이 예제의 스크립트는 다음과 같이 전달 됩니다. 합니다 **ifIndex** 원격 네트워크 어댑터 IP 주소 192.168.1.5 14의 값입니다.

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 14 -IsRoCE $true -RemoteIpAddress 192.168.1.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**결과:** _ 

   ```   
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
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

6. 실행 합니다 **테스트 Rdma.ps1** PowerShell 스크립트를 스크립트에 동일한 VLAN의 두 번째 원격 어댑터의 IP 주소와 함께 ifIndex 값을 전달 합니다.<p>이 예제의 스크립트는 다음과 같이 전달 됩니다. 합니다 **ifIndex** 값 13 192.168.2.5 원격 네트워크 어댑터 IP 주소입니다.

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 13 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**결과:** _ 

   ```   
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
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
   ``` 

## <a name="step-6-create-a-hyper-v-vswitch-on-your-hyper-v-hosts"></a>6단계. Hyper-v 호스트에 Hyper-v vSwitch를 만듭니다


다음 이미지에서 Hyper-v 호스트 1 vSwitch를 보여 줍니다.

![Hyper-v 가상 스위치 만들기](../../media/Converged-NIC/5-datacenter-create-vswitch.jpg)

1. Hyper-v 호스트 1에서 모드 설정에서에서 vSwitch를 만듭니다.

   ```PowerShell
   New-VMSwitch –Name "VMSTEST" –NetAdapterName "TEST-40G-1","TEST-40G-2" -EnableEmbeddedTeaming $true -AllowManagementOS $true
   ```

   _**결과:** _


   |  이름   | SwitchType | NetAdapterInterfaceDescription |
   |---------|------------|--------------------------------|
   | VMSTEST |  외부  |        팀 인터페이스        |

   ---

2. 집합의 실제 어댑터 팀을 봅니다.

   ```PowerShell
   Get-VMSwitchTeam -Name "VMSTEST" | fl
   ```

   _**결과:** _  

   ```
   Name: VMSTEST  
   Id: ad9bb542-dda2-4450-a00e-f96d44bdfbec  
   NetAdapterInterfaceDescription: {Mellanox ConnectX-3 Pro Ethernet Adapter, Mellanox ConnectX-3 Pro Ethernet Adapter #2}  
   TeamingMode: SwitchIndependent  
   LoadBalancingAlgorithm: Dynamic   
   ```

3. 호스트 vNIC의 두 가지 보기를 표시 합니다.

   ```PowerShell
    Get-NetAdapter
   ```

   _**결과:** _


   |        이름         |        InterfaceDescription         | ifIndex | 상태 |    MacAddress     | LinkSpeed |
   |---------------------|-------------------------------------|---------|--------|-------------------|-----------|
   | vEthernet (VMSTEST) | Hyper-v 가상 이더넷 어댑터 #2 |   28    |   위쪽   | E4-1D-2D-07-40-71 |  80 요금 5gbps  |

   ---

4. 호스트 vNIC의 추가 속성을 봅니다. 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**결과:** _


   |  이름   | IsManagementOs | VMName  |  SwitchName  | MacAddress | 상태 | IPAddresses |
   |---------|----------------|---------|--------------|------------|--------|-------------|
   | VMSTEST |      True      | VMSTEST | E41D2D074071 |    {확인}    | &nbsp; |             |

   ---


5. 원격 VLAN 101 어댑터에 네트워크 연결을 테스트 합니다.

   ```PowerShell
   Test-NetConnection 192.168.1.5 
   ```

   _**결과:** _  

   ```
   WARNING: Ping to 192.168.1.5 failed -- Status: DestinationHostUnreachable

   ComputerName   : 192.168.1.5
   RemoteAddress  : 192.168.1.5
   InterfaceAlias : vEthernet (CORP-External-Switch)
   SourceAddress  : 10.199.48.170
   PingSucceeded  : False
   PingReplyDetails (RTT) : 0 ms
   ```

## <a name="step-7-remove-the-access-vlan-setting"></a>7단계. 액세스 VLAN 설정을 제거합니다

이 단계에서는 실제 NIC에서 및 vSwitch를 사용 하 여 VLANID를 설정 하려면 ACCESS VLAN 설정을 제거 합니다.

모두 자동 태깅 잘못 된 VLAN ID를 사용 하 여 송신 트래픽을 방지 하기 위해 ACCESS VLAN 설정을 제거 하 고 액세스 VLAN ID와 일치 하지 않습니다는 트래픽 수신 필터링

1. 설정을 제거 합니다.

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name "Test-40G-1" -RegistryKeyword VlanID -RegistryValue "0"
   Set-NetAdapterAdvancedProperty -Name "Test-40G-2" -RegistryKeyword VlanID -RegistryValue "0"
   ```

2. VLAN ID를 설정 합니다.

   ```PowerShell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "VMSTEST" -VlanId "101" -Access -ManagementOS
   Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName "VMSTEST"
   ```

   _**결과:** _  

   ```
   VMName VMNetworkAdapterName Mode   VlanList
   ------ -------------------- ----   --------
          VMSTEST              Access 101     
   ```


3. 네트워크 연결을 테스트 합니다.

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

   >**중요 한** 결과 예제 결과 유사 되며 메시지를 사용 하 여 ping이 실패 하는 경우 "경고: 192.168.1.5에 대 한 Ping 실패-상태: DestinationHostUnreachable,""vEthernet (VMSTEST)"에 적절 한 IP 주소가 있는지 확인 합니다.
   >
   >```PowerShell
   >Get-NetIPAddress -InterfaceAlias "vEthernet (VMSTEST)"
   >```
   >
   >IP 주소를 설정 하지 않으면 문제를 해결 합니다.
   >
   >```PowerShell
   >New-NetIPAddress -InterfaceAlias "vEthernet (VMSTEST)" -IPAddress 192.168.1.3 -PrefixLength 24
   >
   >IPAddress : 192.168.1.3
   >InterfaceIndex: 37
   >InterfaceAlias: vEthernet (VMSTEST)
   >AddressFamily : IPv4
   >Type  : Unicast
   >PrefixLength  : 24
   >PrefixOrigin  : Manual
   >SuffixOrigin  : Manual
   >AddressState  : Tentative
   >ValidLifetime : Infinite ([TimeSpan]::MaxValue)
   >PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
   >SkipAsSource  : False
   >PolicyStore   : ActiveStore
   >```  


4. 관리 NIC. 이름 바꾸기

   ```PowerShell
   Rename-VMNetworkAdapter -ManagementOS -Name “VMSTEST” -NewName “MGT”
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**결과:** _ 


   |         이름         | IsManagementOs | VMName |      SwitchName      |  MacAddress  | 상태 | IPAddresses |
   |----------------------|----------------|--------|----------------------|--------------|--------|-------------|
   | CORP 외부 전환 |      True      | &nbsp; | CORP 외부 전환 | 001B785768AA |  {확인}  |   &nbsp;    |
   |         MGT          |      True      | &nbsp; |       VMSTEST        | E41D2D074071 |  {확인}  |   &nbsp;    |

   ---

5. NIC 속성을 추가 하는 보기입니다.

   ```PowerShell
   Get-NetAdapter
   ```

   _**결과:** _


   |      이름       |        InterfaceDescription         | ifIndex | 상태 |    MacAddress     | LinkSpeed |
   |-----------------|-------------------------------------|---------|--------|-------------------|-----------|
   | vEthernet (MGT) | Hyper-v 가상 이더넷 어댑터 #2 |   28    |   위쪽   | E4-1D-2D-07-40-71 |  80 요금 5gbps  |

   ---

## <a name="step-8-test-hyper-v-vswitch-rdma"></a>8 단계입니다. Hyper-v vSwitch RDMA를 테스트 합니다.

다음 이미지는 Hyper-v 호스트 1에서 vSwitch를 포함 하 여 Hyper-v 호스트의 현재 상태를 표시 합니다.

![Hyper-v 가상 스위치를 테스트 합니다.](../../media/Converged-NIC/6-datacenter-test-vswitch-rdma.jpg)

1. 이전 VLAN 설정을 보완 하기 위해 호스트 vNIC에 태그를 지정 하는 우선 순위를 설정 합니다.

   ```PowerShell    
   Set-VMNetworkAdapter -ManagementOS -Name "MGT" -IeeePriorityTag on
   Get-VMNetworkAdapter -ManagementOS -Name "MGT" | fl Name,IeeePriorityTag
   ```

   _**결과:** _  

   이름: MGT  
   IeeePriorityTag :  켜짐  

2. RDMA에 대 한 두 호스트 Vnic를 만들고 VMSTEST vSwitch를 연결할 수 있습니다.

   ```PowerShell    
   Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB1 –ManagementOS
   Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB2 –ManagementOS
   ```

3. 관리 NIC 속성을 봅니다.

   ```PowerShell    
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**결과:** _ 


   |         이름         | IsManagementOs |        VMName        |  SwitchName  | MacAddress | 상태 | IPAddresses |
   |----------------------|----------------|----------------------|--------------|------------|--------|-------------|
   | CORP 외부 전환 |      True      | CORP 외부 전환 | 001B785768AA |    {확인}    | &nbsp; |             |
   |         Mgt          |      True      |       VMSTEST        | E41D2D074071 |    {확인}    | &nbsp; |             |
   |         SMB1         |      True      |       VMSTEST        | 00155D30AA00 |    {확인}    | &nbsp; |             |
   |         SMB2         |      True      |       VMSTEST        | 00155D30AA01 |    {확인}    | &nbsp; |             |

   ---

## <a name="step-9-assign-an-ip-address-to-the-smb-host-vnics-vethernet-smb1-and-vethernet-smb2"></a>9단계: SMB 호스트 Vnic vEthernet에 IP 주소를 할당할 \(SMB1\) vEthernet 및 \(SMB2\)

테스트-40 G-1 및 2-테스트-40 G 실제 어댑터는 ACCESS VLAN 101 및 102 구성 되지 않았습니다. 따라서 어댑터 트래픽-태그를 지정 하 고 ping 성공 합니다. 이전에 모두 pNIC VLAN Id를 0으로 구성 된 다음 VMSTEST vSwitch VLAN 101로 설정 합니다. 그 후 여전히 MGT vNIC를 사용 하 여 원격 VLAN 101 어댑터를 ping 할 수는 있지만 현재 VLAN 102 멤버가 있습니다.



1. 모두 자동 태깅 잘못 된 VLAN ID를 사용 하 여 송신 트래픽 하지 못하도록 하 고 액세스 VLAN ID와 일치 하지 않는 수신 트래픽을 필터링 하지 못하도록 물리적 NIC에서 ACCESS VLAN 설정을 제거합니다

   ```PowerShell    
   New-NetIPAddress -InterfaceAlias "vEthernet (SMB1)" -IPAddress 192.168.2.111 -PrefixLength 24
   ```

   _**결과:** _  

   ```   
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
   ```

2. 원격 VLAN 102 어댑터를 테스트 합니다.

   ```PowerShell
   Test-NetConnection 192.168.2.5 
   ```

   _**결과:** _  

   ```
   ComputerName   : 192.168.2.5
   RemoteAddress  : 192.168.2.5
   InterfaceAlias : vEthernet (SMB1)
   SourceAddress  : 192.168.2.111
   PingSucceeded  : True
   PingReplyDetails (RTT) : 0 ms
   ```

3. 인터페이스 vEthernet에 대 한 새 IP 주소를 추가 \(SMB2\)합니다.

   ```PowerShell
   New-NetIPAddress -InterfaceAlias "vEthernet (SMB2)" -IPAddress 192.168.2.222 -PrefixLength 24 
   ```

   _**결과:** _ 

   ```
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
   ```

4. 연결을 다시 테스트 합니다.    


5. 기존 VLAN 102에 RDMA 호스트 Vnic를 배치 합니다.

   ```PowerShell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB1" -VlanId "102" -Access -ManagementOS
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB2" -VlanId "102" -Access -ManagementOS

   Get-VMNetworkAdapterVlan -ManagementOS
   ```

   _**결과:** _ 

   ```   
   VMName VMNetworkAdapterName Mode VlanList
   ------ -------------------- ---- --------
      SMB1 Access   102 
      Mgt  Access   101 
      SMB2 Access   102 
      CORP-External-Switch Untagged
   ```

6. 매핑의 SMB1 및 vSwitch 팀 설정에서 기본 물리적 Nic에 SMB2를 검사 합니다.<p>호스트 vNIC 실제 Nic의 연결이 임의 및 생성 및 소멸 하는 동안 리 밸 러 싱 될 수 있습니다. 이 경우에 현재 연결을 확인 하는 간접 메커니즘을 사용할 수 있습니다. SMB1 및 SMB2 MAC 주소를 NIC 팀 멤버가 테스트-40 G-2에 연결 됩니다. 이 테스트-40 G-1 SMB 호스트 vNIC를 연결된 되지 않은 허용 하지 않으므로 RDMA 트래픽 사용률에 대 한 링크를 통해 SMB 호스트 vNIC를 매핑할 때까지 적합 하지 않습니다.

   ```PowerShell    
   Get-NetAdapterVPort (Preferred)

   Get-NetAdapterVmqQueue
   ```

   _**결과:** _ 

   ```
   Name   QueueID MacAddressVlanID Processor VmFriendlyName
   ----   ------- ---------------- --------- --------------
   TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
   TEST-40G-2 1   00-15-5D-30-AA-00 1020:17
   TEST-40G-2 2   00-15-5D-30-AA-01 1020:17
   ```

7. VM 네트워크 어댑터 속성을 봅니다.

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**결과:** _ 

   ```
   Name IsManagementOs VMName SwitchName   MacAddress   Status IPAddresses
   ---- -------------- ------ ----------   ----------   ------ -----------
   CORP-External-Switch True  CORP-External-Switch 001B785768AA {Ok}  
   Mgt  True  VMSTEST  E41D2D074071 {Ok}  
   SMB1 True  VMSTEST  00155D30AA00 {Ok}  
   SMB2 True  VMSTEST  00155D30AA01 {Ok}  
   ```

8. 네트워크 어댑터 팀 매핑을 확인 합니다.<p>결과 매핑 아직 수행 하지 않은 때문에 정보를 반환 하지 해야 합니다.

   ```PowerShell
   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB1
   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB2
   ```


9. SMB1 및 SMB2 물리적 NIC 팀 멤버를 구분 하 고 작업의 결과 보려면를 매핑하십시오.

   >[!IMPORTANT]
   >계속 하기 전에이 단계를 완료 하면 구현 실패 확인 합니다.

   ```PowerShell
   Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB1" -PhysicalNetAdapterName "Test-40G-1"
   Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB2" -PhysicalNetAdapterName "Test-40G-2"

   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST
   ```

   _**결과:** _ 

   ```   
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
   ```

10. 이전에 만든 MAC 연결을 확인 합니다.

    ```PowerShell    
    Get-NetAdapterVmqQueue
    ```

    _**결과:** _ 

    ```   
    Name   QueueID MacAddressVlanID Processor VmFriendlyName
    ----   ------- ---------------- --------- --------------
    TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
    TEST-40G-1 2   00-15-5D-30-AA-00 1020:17
    TEST-40G-2 1   00-15-5D-30-AA-01 1020:17
    ```


11. 두 호스트 Vnic 동일한 서브넷에 있고 동일한 VLAN ID가 있기 때문에 원격 시스템에서 연결 테스트 \(102\)합니다.

    ```PowerShell 
    Test-NetConnection 192.168.2.111
    ```

    _**결과:** _   

    ```
    ComputerName   : 192.168.2.111
    RemoteAddress  : 192.168.2.111
    InterfaceAlias : Test-40G-2
    SourceAddress  : 192.168.2.5
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    ```

    ```PowerShell   
    Test-NetConnection 192.168.2.222
    ```

    _**결과:** _   

    ```
    ComputerName   : 192.168.2.222
    RemoteAddress  : 192.168.2.222
    InterfaceAlias : Test-40G-2
    SourceAddress  : 192.168.2.5
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms 
    ```
12. 이름, 스위치 이름 및 우선 순위 태그를 설정 합니다.   

    ```PowerShell
    Set-VMNetworkAdapter -ManagementOS -Name "SMB1" -IeeePriorityTag on
    Set-VMNetworkAdapter -ManagementOS -Name "SMB2" -IeeePriorityTag on
    Get-VMNetworkAdapter -ManagementOS -Name "SMB*" | fl Name,SwitchName,IeeePriorityTag,Status
    ```

    _**결과:** _   

    ```
    Name: SMB1
    SwitchName  : VMSTEST
    IeeePriorityTag : On 
    Status  : {Ok}

    Name: SMB2
    SwitchName  : VMSTEST
    IeeePriorityTag : On
    Status  : {Ok}
    ```

13. VEthernet 네트워크 어댑터 속성을 봅니다.

    ```PowerShell
    Get-NetAdapterRdma -Name "vEthernet*" | sort Name | ft -AutoSize
    ```

    _**결과:** _   

    ```
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  False  
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  False  
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False   
    ```

14. VEthernet 네트워크 어댑터를 사용 하도록 설정 합니다.  

    ```PowerShell
    Enable-NetAdapterRdma -Name "vEthernet (SMB1)"
    Enable-NetAdapterRdma -Name "vEthernet (SMB2)"
    Get-NetAdapterRdma -Name "vEthernet*" | sort Name | fl *
    ```

    _**결과:** _   

    ```
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  True   
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  True  
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False
    ```

## <a name="step-10-validate-the-rdma-functionality"></a>10 단계입니다. RDMA 기능을 확인 합니다.

VSwitch를 모두 vSwitch 집합 팀의 구성원에 있는 로컬 시스템에 원격 시스템에서 RDMA 기능의 유효성을 검사 해야 합니다.<p>때문에 두 호스트 Vnic \(SMB1 및 SMB2\) 할당 된 VLAN 102 원격 시스템에서 VLAN 102 어댑터를 선택할 수 있습니다. <p>이 예제에서는 NIC 테스트-40 G-2가 RDMA SMB1 (192.168.2.111) 및 SMB2 (192.168.2.222).

>[!TIP]
>이 시스템에서 방화벽을 사용 하지 않도록 설정 해야 합니다.  자세한 내용은 fabric 정책을 참조 하세요.
>
>```PowerShell
>Set-NetFirewallProfile -All -Enabled False
>    
>Get-NetAdapterAdvancedProperty -Name "Test-40G-2"
>```
>
>_**결과:** _ 
>   
>```
>Name  DisplayNameDisplayValue   RegistryKeyword RegistryValue  
>----  -----------------------   --------------- -------------  
> .
> .
>Test-40G-2VLAN ID102VlanID  {102} 
>```

1. 네트워크 어댑터 속성을 봅니다.

   ```PowerShell
   Get-NetAdapter
   ```

   _**결과:** _ 

   ```
   Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
   ----  --------------------------- ------   ---------- ---------
   Test-40G-2Mellanox ConnectX-3 Pro Ethernet A...#3   3 Up   E4-1D-2D-07-43-D140 Gbps
   ```

2. 네트워크 어댑터가 RDMA 정보를 봅니다.

   ```PowerShell
   Get-NetAdapterRdma
   ```

   _**결과:** _  

   ```
   Name  InterfaceDescription Enabled
   ----  -------------------- -------
   Test-40G-2Mellanox ConnectX-3 Pro Ethernet Adap... True   
   ```

3. 첫 번째 실제 어댑터에서 RDMA 트래픽 테스트를 수행 합니다.

   ```PowerShell 
   C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.111 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**결과:** _ 

   ```
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
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
   ```

4. 두 번째 실제 어댑터에서 RDMA 트래픽 테스트를 수행 합니다.

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.222 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**결과:** _ 

   ```
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
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
   ```

5. 원격 컴퓨터에 로컬에서 RDMA 트래픽에 대 한 테스트입니다.

    ```PowerShell
    Get-NetAdapter | ft –AutoSize
    ```

    _**결과:** _ 

    ```
    Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
    ----  --------------------------- ------   ---------- ---------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  45 Up   00-15-5D-30-AA-0380 Gbps
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  41 Up   00-15-5D-30-AA-0280 Gbps
    ```

6. 첫 번째 가상 어댑터에서 RDMA 트래픽 테스트를 수행 합니다.    

   ```
   C:\TEST\Test-RDMA.PS1 -IfIndex 41 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**결과:** _ 

   ```
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
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
   ```

7. 두 번째 가상 어댑터에서 RDMA 트래픽 테스트를 수행 합니다.

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 45 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**결과:** _ 

   ```
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
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
   ```

이 출력의 마지막 줄에서는 "RDMA 트래픽 테스트 성공 합니다. RDMA 트래픽 192.168.2.5, 전송 된"어댑터에서 수렴 된 NIC를 성공적으로 구성 있는지 보여 줍니다.

## <a name="related-topics"></a>관련 항목 

- [단일 네트워크 어댑터로 수렴 형 된 NIC 구성](cnic-single.md)
- [수렴 형 된 NIC에 대 한 물리적 스위치 구성](cnic-app-switch-config.md)
- [수렴 형 NIC 구성 문제 해결](cnic-app-troubleshoot.md)
