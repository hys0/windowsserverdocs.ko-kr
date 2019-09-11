---
title: 팀으로 구성 된 NIC 구성 (데이터 센터)에서 수렴 형 NIC
description: 이 항목에서는 스위치 포함 된 팀 (설정)을 사용 하 여 팀으로 구성 된 NIC 구성에서 수렴 형 NIC를 배포 하기 위한 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f01546f8-c495-4055-8492-8806eee99862
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/17/2018
ms.openlocfilehash: 8229b72d69968d3690ece87d5116b215bdf78a08
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869874"
---
# <a name="converged-nic-in-a-teamed-nic-configuration-datacenter"></a>팀으로 구성 된 NIC 구성 (데이터 센터)에서 수렴 형 NIC

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 스위치 포함 팀 \(집합\)을 사용 하 여 팀으로 구성 된 nic 구성에서 수렴 형 nic를 배포 하기 위한 지침을 제공 합니다. 

이 항목의 예제 구성은 hyper-v 호스트 **1** 및 **hyper-v 호스트 2**의 hyper-v 호스트 2 개에 대해 설명 합니다. 두 호스트에는 두 개의 네트워크 어댑터가 있습니다. 각 호스트에서 하나의 어댑터는 192.168.1/24 서브넷에 연결 되 고, 하나의 어댑터는 192.168.2/24 서브넷에 연결 됩니다.

![Hyper-V 호스트](../../media/Converged-NIC/1-datacenter-test-conn.jpg)

## <a name="step-1-test-the-connectivity-between-source-and-destination"></a>1단계. 원본 및 대상 간의 연결 테스트

실제 NIC가 대상 호스트에 연결할 수 있는지 확인 합니다.  이 테스트는 계층 3 \(L3\) 또는 IP 계층과 계층 2 \(L2\) 가상 lan \(VLAN\)을 사용 하 여 연결을 보여 줍니다.

1. 첫 번째 네트워크 어댑터 속성을 봅니다.

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```

   _**검색**_


   |    이름    |           인터페이스 설명           | ifIndex | 상태 |    Mac     | /%Linkspeed |
   |------------|------------------------------------------|---------|--------|-------------------|-----------|
   | 40G-1 | Mellanox Connectx-3 Pro 이더넷 어댑터 |   11    |   위쪽   | E4-1D-2D-07-43-D0 |  40 Gbps  |

   ---

2. IP 주소를 포함 하 여 첫 번째 어댑터에 대 한 추가 속성을 봅니다. 

   ```PowerShell
   Get-NetIPAddress -InterfaceAlias "Test-40G-1"
   Get-NetIPAddress -InterfaceAlias "TEST-40G-1" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress
   ```

   _**검색**_


   |   매개 변수    |    값    |
   |----------------|-------------|
   |   IP 주소    | 192.168.1.3 |
   | InterfaceIndex |     11      |
   | InterfaceAlias | 40G-1  |
   | AddressFamily  |    IPv4     |
   |      형식      |   유니캐스트   |
   |  PrefixLength  |     24      |

   ---

3. 두 번째 네트워크 어댑터 속성을 봅니다.

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-2" | ft -AutoSize
   ```

   _**검색**_


   |    이름    |          인터페이스 설명           | ifIndex | 상태 |    Mac     | /%Linkspeed |
   |------------|-----------------------------------------|---------|--------|-------------------|-----------|
   | 40G-2 | Mellanox Connectx-3 Pro 이더넷 A ... #2 |   13    |   위쪽   | E4-1D-07-40-70 |  40 Gbps  |

   ---

4. IP 주소를 포함 하 여 두 번째 어댑터에 대 한 추가 속성을 봅니다.

   ```PowerShell
   Get-NetIPAddress -InterfaceAlias "Test-40G-2"
   Get-NetIPAddress -InterfaceAlias "Test-40G-2" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress
   ```

   _**검색**_


   |   매개 변수    |    값    |
   |----------------|-------------|
   |   IP 주소    | 192.168.2.3 |
   | InterfaceIndex |     13      |
   | InterfaceAlias | 40G-2  |
   | AddressFamily  |    IPv4     |
   |      형식      |   유니캐스트   |
   |  PrefixLength  |     24      |

   ---

5. 다른 NIC 팀 또는 SET 구성원 pNICs에 유효한 IP 주소가 있는지 확인 합니다.<p>별도의 서브넷 xxx.xxx을 \(사용 합니다. **2**. xxx vs xxx.xxx. **1**. xxx\)-이 어댑터에서 대상으로 쉽게 보낼 수 있습니다. 그렇지 않고 동일한 서브넷에서 pNICs를 둘 다 찾은 경우 Windows TCP/IP 스택 부하는 인터페이스 간에 부하를 분산 하 고 간단한 유효성 검사는 더 복잡해 집니다.


## <a name="step-2-ensure-that-source-and-destination-can-communicate"></a>2단계. 원본 및 대상이 통신할 수 있는지 확인 합니다.

이 단계에서는 **테스트-NetConnection** Windows PowerShell 명령을 사용 하지만 원하는 경우 **ping** 명령을 사용할 수 있습니다. 

1. 양방향 통신을 확인 합니다.

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


4. 추가 Nic에 대 한 연결을 확인 합니다. NIC 또는 집합 팀에 포함 된 모든 후속 pNICs에 대해 이전 단계를 반복 합니다.

   ```PowerShell    
   Test-NetConnection 192.168.2.5
   ```

   _**검색**_


   |        매개 변수         |    값    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.2.5 |
   |      RemoteAddress       | 192.168.2.5 |
   |      InterfaceAlias      | 40G-2  |
   |      SourceAddress       | 192.168.2.3 |
   |      이상 성공       |    False    |
   | PingReplyDetails \(RTT\) |    0 밀리초     |

   ---

## <a name="step-3-configure-the-vlan-ids-for-nics-installed-in-your-hyper-v-hosts"></a>3단계. Hyper-v 호스트에 설치 된 Nic에 대 한 VLAN Id 구성

많은 네트워크 구성에서 Vlan을 사용 하며, 네트워크에서 Vlan을 사용 하려는 경우 Vlan을 구성 하 여 이전 테스트를 반복 해야 합니다.

이 단계에서는 Nic가 **액세스** 모드입니다. 그러나이 가이드의 뒷부분에서 hyper-v 가상 스위치 \(vSwitch\) 를 만들 때 VLAN 속성은 vSwitch 포트 수준에서 적용 됩니다. 

스위치는 여러 vlan을 호스트할 수 있으므로, 랙 \(\) 연결 물리적 스위치의 상단에 호스트가 트렁크 모드에서 구성 된 포트를 갖도록 해야 합니다.

>[!NOTE]
>스위치에서 트렁크 모드를 구성 하는 방법에 대 한 지침은 해당 하는 스위치 설명서를 참조 하세요.

다음 이미지는 네트워크 어댑터 속성에서 VLAN 101 및 VLAN 102이 구성 된 두 개의 네트워크 어댑터를 포함 하는 두 개의 Hyper-v 호스트를 보여 줍니다.

![가상 로컬 영역 네트워크 구성](../../media/Converged-NIC/2-datacenter-configure-vlans.jpg)


>[!TIP]
>전기 \(및 전자 제품 엔지니어의 협회 IEEE\) 네트워킹 표준에 따라 실제 NIC의 서비스 \(QoS\) 속성의 품질은 포함 된 802.1 p 헤더에 적용 됩니다. vlan ID를 구성할 \(때\) 802.1 q vlan 헤더 내에 있습니다.

1. 첫 번째 NIC 인 40G-1에서 VLAN ID를 구성 합니다.

   ```PowerShell    
   Set-NetAdapterAdvancedProperty -Name "Test-40G-1" -RegistryKeyword VlanID -RegistryValue "101"
   Get-NetAdapterAdvancedProperty -Name "Test-40G-1" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
   ```

   _**검색**_   


   |    이름    | DisplayName | DisplayValue | RegistryKeyword | RegistryValue |
   |------------|-------------|--------------|-----------------|---------------|
   | 40G-1 |   VLAN ID   |     101      |     VlanID      |     {101}     |

   ---

2. 네트워크 어댑터를 다시 시작 하 여 VLAN ID를 적용 합니다.

   ```PowerShell
   Restart-NetAdapter -Name "Test-40G-1"
   ```

3. 상태가 **Up**인지 확인 합니다.

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```

   _**검색**_


   |    이름    |          인터페이스 설명           | ifIndex | 상태 |    Mac     | /%Linkspeed |
   |------------|-----------------------------------------|---------|--------|-------------------|-----------|
   | 40G-1 | Mellanox Connectx-3 Pro 이더넷 Ada ... |   11    |   위쪽   | E4-1D-2D-07-43-D0 |  40 Gbps  |

   ---

4. 두 번째 NIC 40G-2에서 VLAN ID를 구성 합니다.

   ```PowerShell    
   Set-NetAdapterAdvancedProperty -Name "Test-40G-2" -RegistryKeyword VlanID -RegistryValue "102"
   Get-NetAdapterAdvancedProperty -Name "Test-40G-2" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
   ``` 

   _**검색**_


   |    이름    | DisplayName | DisplayValue | RegistryKeyword | RegistryValue |
   |------------|-------------|--------------|-----------------|---------------|
   | 40G-2 |   VLAN ID   |     102      |     VlanID      |     {102}     |

   ---

5. 네트워크 어댑터를 다시 시작 하 여 VLAN ID를 적용 합니다.

   ```PowerShell
   Restart-NetAdapter -Name "Test-40G-2" 
   ```

6. 상태가 **Up**인지 확인 합니다.

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```

   _**검색**_


   |    이름    |          인터페이스 설명           | ifIndex | 상태 |    Mac     | /%Linkspeed |
   |------------|-----------------------------------------|---------|--------|-------------------|-----------|
   | 40G-2 | Mellanox Connectx-3 Pro 이더넷 Ada ... |   11    |   위쪽   | E4-1D-2D-07-43-D1 |  40 Gbps  |

   ---

   >[!IMPORTANT]
   >장치가 다시 시작 되 고 네트워크에서 사용할 수 있게 되는 데 몇 초 정도 걸릴 수 있습니다. 

7. 첫 번째 NIC (40G-1)에 대 한 연결을 확인 합니다.<p>연결에 실패 하면 동일한 VLAN의 스위치 VLAN 구성 또는 대상 참여를 검사 합니다. 

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**검색**_   


   |        매개 변수         |    값    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.1.5 |
   |      RemoteAddress       | 192.168.1.5 |
   |      InterfaceAlias      | 40G-1  |
   |      SourceAddress       | 192.168.1.5 |
   |      이상 성공       |    True     |
   | PingReplyDetails \(RTT\) |    0 밀리초     |

   ---

8. 첫 번째 NIC 인 40G-2에 대 한 연결을 확인 합니다.<p>연결에 실패 하면 동일한 VLAN의 스위치 VLAN 구성 또는 대상 참여를 검사 합니다.

   ```PowerShell    
   Test-NetConnection 192.168.2.5
   ```

   _**검색**_    


   |        매개 변수         |    값    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.2.5 |
   |      RemoteAddress       | 192.168.2.5 |
   |      InterfaceAlias      | 40G-2  |
   |      SourceAddress       | 192.168.2.3 |
   |      이상 성공       |    True     |
   | PingReplyDetails \(RTT\) |    0 밀리초     |

   ---

   >[!IMPORTANT]
   >**Get-netadapter**를 수행한 후 즉시 **테스트 netconnection** 또는 ping 실패가 발생 하는 것은 일반적이 지 않습니다.  따라서 네트워크 어댑터가 완전히 초기화 될 때까지 기다린 후 다시 시도 하십시오.
   >
   >Vlan 101 연결이 작동 하지만 VLAN 102 연결에 문제가 없는 경우 원하는 VLAN에서 포트 트래픽을 허용 하도록 스위치를 구성 해야 할 수 있습니다. 오류 어댑터를 일시적으로 VLAN 101으로 설정 하 고 연결 테스트를 반복 하 여이를 확인할 수 있습니다.


   다음 이미지는 Vlan을 성공적으로 구성한 후의 Hyper-v 호스트를 보여 줍니다.

   ![서비스 품질 구성](../../media/Converged-NIC/3-datacenter-configure-qos.jpg)


## <a name="step-4-configure-quality-of-service-qos"></a>4단계. 서비스 \(품질 QoS 구성\)

>[!NOTE]
>서로 통신 하는 모든 호스트에서 다음 DCB 및 QoS 구성 단계를 모두 수행 해야 합니다.

1. 각 hyper-v 호스트에 \(데이터\) 센터 브리징 DCB를 설치 합니다.

   - IWarp를 사용 하는 네트워크 구성의 경우 **선택 사항** 입니다.
   - RDMA 서비스\) 의 경우 roce \(를 사용 하는 네트워크 구성에 **필요** 합니다.

   ```PowerShell
   Install-WindowsFeature Data-Center-Bridging
   ```

   _**검색**_


   | Success | 다시 시작 필요 | 종료 코드 |     기능 결과     |
   |---------|----------------|-----------|------------------------|
   |  True   |       아니요       |  Success  | {데이터 센터 브리징} |

   ---

2. SMB 다이렉트에 대 한 QoS 정책을 설정 합니다.

   - IWarp를 사용 하는 네트워크 구성의 경우 **선택 사항** 입니다.
   - RDMA 서비스\) 의 경우 roce \(를 사용 하는 네트워크 구성에 **필요** 합니다.

   아래 예제 명령에서 값 "3"은 임의입니다. QoS 정책 구성에서 동일한 값을 일관 되 게 사용 하는 한 1에서 7 사이의 모든 값을 사용할 수 있습니다.

   ```PowerShell
   New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3
   ```

   _**검색**_


   |   매개 변수    |          값           |
   |----------------|--------------------------|
   |      이름      |           SMB            |
   |     소유자      | 그룹 정책 \(컴퓨터\) |
   | NetworkProfile |           모두            |
   |   우선 순위   |           127            |
   |   JobObject    |          &nbsp;          |
   | NetDirectPort  |           445            |
   | PriorityValue  |            3             |

   ---

3. 인터페이스에서 다른 트래픽에 대 한 추가 QoS 정책을 설정 합니다.   

   ```PowerShell
   New-NetQosPolicy "DEFAULT" -Default -PriorityValue8021Action 0
   ```

   _**검색**_   


   |   매개 변수    |          값           |
   |----------------|--------------------------|
   |      이름      |         DEFAULT          |
   |     소유자      | 그룹 정책 \(컴퓨터\) |
   | NetworkProfile |           모두            |
   |   우선 순위   |           127            |
   |    템플릿    |         기본값          |
   |   JobObject    |          &nbsp;          |
   | PriorityValue  |            0             |

   ---

4. SMB 트래픽에 대해 **우선 순위 흐름 제어** 를 설정 합니다 .이는 iWarp에 필요 하지 않습니다.

   ```PowerShell
   Enable-NetQosFlowControl -priority 3
   Get-NetQosFlowControl
   ```

   _**검색**_


   | 우선 순위 | Enabled | PolicySet | IfIndex | IfAlias |
   |----------|---------|-----------|---------|---------|
   |    0     |  False  |  Global   | &nbsp;  | &nbsp;  |
   |    1     |  False  |  Global   | &nbsp;  | &nbsp;  |
   |    2     |  False  |  Global   | &nbsp;  | &nbsp;  |
   |    3     |  True   |  Global   | &nbsp;  | &nbsp;  |
   |    4     |  False  |  Global   | &nbsp;  | &nbsp;  |
   |    5     |  False  |  Global   | &nbsp;  | &nbsp;  |
   |    6     |  False  |  Global   | &nbsp;  | &nbsp;  |
   |    7     |  False  |  Global   | &nbsp;  | &nbsp;  |

   ---

   >**중요** 3이 아닌 항목의 값이 True로 설정 되어 있기 때문에 결과가 이러한 결과와 일치 하지 않는 경우 이러한 클래스에 대해 **Flowcontrol** 을 사용 하지 않도록 설정 해야 합니다.
   >
   >```PowerShell
   >Disable-NetQosFlowControl -priority 0,1,2,4,5,6,7
   >Get-NetQosFlowControl
   >```
   >더 복잡 한 구성에서는 다른 트래픽 클래스가 흐름 제어를 필요로 할 수 있지만 이러한 시나리오는이 가이드의 범위를 벗어납니다.


5. 첫 번째 NIC 인 40G-1에 대해 QoS를 사용 하도록 설정 합니다.

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
   | NumTCs (Max/PFC/) |    8/8/8     |    8/8/8     |

   ---

   _**OperationalTrafficClasses**:_    


   | 간체 |  TSA   | 대역 | 우선순위 |
   |----|--------|-----------|------------|
   | 0  | 높음 |  &nbsp;   |    0-7     |

   ---

   _**OperationalFlowControl**:_  

   우선 순위 3 사용  

   _**OperationalClassifications**:_  


   | 프로토콜  | 포트/유형 | 우선 순위 |
   |-----------|-----------|----------|
   |  기본값  |  &nbsp;   |    0     |
   | NetDirect |    445    |    3     |

   ---

6. 두 번째 NIC 40G-2에 대해 QoS를 사용 하도록 설정 합니다.

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
   | NumTCs (Max/PFC/) |    8/8/8     |    8/8/8     |

   ---

   _**OperationalTrafficClasses**:_  


   | 간체 |  TSA   | 대역 | 우선순위 |
   |----|--------|-----------|------------|
   | 0  | 높음 |  &nbsp;   |    0-7     |

   ---

    _**OperationalFlowControl**:_  

    우선 순위 3 사용  

   _**OperationalClassifications**:_  


   | 프로토콜  | 포트/유형 | 우선 순위 |
   |-----------|-----------|----------|
   |  기본값  |  &nbsp;   |    0     |
   | NetDirect |    445    |    3     |

   ---


7. SMB 다이렉트 \(RDMA에 대역폭 절반을 예약 합니다.\)

   ```PowerShell
   New-NetQosTrafficClass "SMB" -priority 3 -bandwidthpercentage 50 -algorithm ETS
   ```

   _**검색**_  


   | 이름 | 알고리즘 | 대역폭 (%) | 우선 순위 | PolicySet | IfIndex | IfAlias |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | SMB  |    요소가    |      50      |    3     |  Global   | &nbsp;  | &nbsp;  |

   ---

8. 대역폭 예약 설정 보기:   

   ```PowerShell
   Get-NetQosTrafficClass | ft -AutoSize
   ```

   _**검색**_  


   |   이름    | 알고리즘 | 대역폭 (%) | 우선 순위 | PolicySet | IfIndex | IfAlias |
   |-----------|-----------|--------------|----------|-----------|---------|---------|
   | 기본 |    요소가    |      50      | 0-2, 4-7  |  Global   | &nbsp;  | &nbsp;  |
   |    SMB    |    요소가    |      50      |    3     |  Global   | &nbsp;  | &nbsp;  |

   ---

9. 필드 테 넌 트 IP 트래픽에 대 한 두 개의 추가 트래픽 클래스를 만듭니다. 

   >[!TIP]
   >"I P 1" 및 "IP2" 값을 생략할 수 있습니다.

   ```PowerShell
   New-NetQosTrafficClass "IP1" -Priority 1 -bandwidthpercentage 10 -algorithm ETS
   ```

   _**검색**_


   | 이름 | 알고리즘 | 대역폭 (%) | 우선 순위 | PolicySet | IfIndex | IfAlias |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | I P 1  |    요소가    |      10      |    1     |  Global   | &nbsp;  | &nbsp;  |

   ---

   ```PowerShell
   New-NetQosTrafficClass "IP2" -Priority 2 -bandwidthpercentage 10 -algorithm ETS
   ```

   _**검색**_


   | 이름 | 알고리즘 | 대역폭 (%) | 우선 순위 | PolicySet | IfIndex | IfAlias |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | IP2  |    요소가    |      10      |    2     |  Global   | &nbsp;  | &nbsp;  |

   ---

10. QoS 트래픽 클래스를 봅니다.

    ```PowerShell
    Get-NetQosTrafficClass | ft -AutoSize
    ```

    _**검색**_


    |   이름    | 알고리즘 | 대역폭 (%) | 우선 순위 | PolicySet | IfIndex | IfAlias |
    |-----------|-----------|--------------|----------|-----------|---------|---------|
    | 기본 |    요소가    |      30      |  0, 4-7   |  Global   | &nbsp;  | &nbsp;  |
    |    SMB    |    요소가    |      50      |    3     |  Global   | &nbsp;  | &nbsp;  |
    |    I P 1    |    요소가    |      10      |    1     |  Global   | &nbsp;  | &nbsp;  |
    |    IP2    |    요소가    |      10      |    2     |  Global   | &nbsp;  | &nbsp;  |

    ---

11. 필드 디버거를 재정의 합니다.<p>기본적으로 연결 된 디버거는 NetQos를 차단 합니다. 

    ```PowerShell
    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
    Get-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" | ft AllowFlowControlUnderDebugger
    ```

    _**검색**_  

    ```
    AllowFlowControlUnderDebugger
    -----------------------------
    1
    ```

## <a name="step-5-verify-the-rdma-configuration-mode-1"></a>5단계. RDMA 구성 \(모드 1 확인\) 

VSwitch를 만들고 RDMA \(모드 2\)로 전환 하기 전에 패브릭이 올바르게 구성 되어 있는지 확인 하려고 합니다.

다음 이미지는 Hyper-v 호스트의 현재 상태를 보여 줍니다.

![RDMA 테스트](../../media/Converged-NIC/4-datacenter-test-rdma.jpg)


1. RDMA 구성을 확인 합니다.

   ```PowerShell
   Get-NetAdapterRdma | ft -AutoSize
   ```

   _**검색**_


   |    이름    |        인터페이스 설명        | Enabled |
   |------------|------------------------------------|---------|
   | 40G-1 | Mellanox Connectx-3-4 VPI 어댑터 #2 |  True   |
   | 40G-2 |  Mellanox Connectx-3-4 VPI 어댑터   |  True   |

   ---

2. 대상 어댑터의 **ifIndex** 값을 확인 합니다.<p>다운로드 한 스크립트를 실행 하는 이후 단계에서이 값을 사용 합니다.   

   ```PowerShell
   Get-NetIPConfiguration -InterfaceAlias "TEST*" | ft InterfaceAlias,InterfaceIndex,IPv4Address
   ```

   _**검색**_


   | InterfaceAlias | InterfaceIndex |  IPv4Address  |
   |----------------|----------------|---------------|
   |   40G-1   |       14       | {192.168.1.3} |
   |   40G-2   |       13       | {192.168.2.3} |

   ---

3. [Diskspd .exe 유틸리티](https://aka.ms/diskspd) 를 다운로드 하 여 C:\TEST로 압축을 풉니다.\.

4. [테스트 RDMA PowerShell 스크립트](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1) 를 로컬 드라이브의 테스트 폴더 (예: C:\TEST)에 다운로드 합니다.\.

5. **Test-Rdma** PowerShell 스크립트를 실행 하 여 ifIndex 값을 동일한 VLAN에 있는 첫 번째 원격 어댑터의 IP 주소와 함께 스크립트에 전달 합니다.<p>이 예제에서 스크립트는 원격 네트워크 어댑터 IP 주소 192.168.1.5에 **ifIndex** 값 14를 전달 합니다.

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 14 -IsRoCE $true -RemoteIpAddress 192.168.1.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**검색**_ 

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
   >RDMA 트래픽이 실패 하는 경우 RoCE 케이스의 경우 호스트 설정과 일치 해야 하는 적절 한 PFC/설정에 대해 관련 스위치 구성을 참조 하세요. 참조 값은이 문서의 QoS 섹션을 참조 하세요.

6. **Test-Rdma** PowerShell 스크립트를 실행 하 여 ifIndex 값을 동일한 VLAN에 있는 두 번째 원격 어댑터의 IP 주소와 함께 스크립트에 전달 합니다.<p>이 예제에서 스크립트는 원격 네트워크 어댑터 IP 주소 192.168.2.5의 **ifIndex** 값 13을 전달 합니다.

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 13 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**검색**_ 

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

## <a name="step-6-create-a-hyper-v-vswitch-on-your-hyper-v-hosts"></a>6단계. Hyper-v 호스트에서 Hyper-v vSwitch 만들기


다음 이미지는 vSwitch를 사용 하는 Hyper-v 호스트 1을 보여 줍니다.

![Hyper-v 가상 스위치 만들기](../../media/Converged-NIC/5-datacenter-create-vswitch.jpg)

1. Hyper-v 호스트 1에서 설정 모드로 vSwitch를 만듭니다.

   ```PowerShell
   New-VMSwitch –Name "VMSTEST" –NetAdapterName "TEST-40G-1","TEST-40G-2" -EnableEmbeddedTeaming $true -AllowManagementOS $true
   ```

   _**만들어집니다**_


   |  이름   | SwitchType | NetAdapterInterfaceDescription |
   |---------|------------|--------------------------------|
   | VMSTEST |  외부  |        팀으로 구성-인터페이스        |

   ---

2. 집합에서 실제 어댑터 팀을 봅니다.

   ```PowerShell
   Get-VMSwitchTeam -Name "VMSTEST" | fl
   ```

   _**검색**_  

   ```
   Name: VMSTEST  
   Id: ad9bb542-dda2-4450-a00e-f96d44bdfbec  
   NetAdapterInterfaceDescription: {Mellanox ConnectX-3 Pro Ethernet Adapter, Mellanox ConnectX-3 Pro Ethernet Adapter #2}  
   TeamingMode: SwitchIndependent  
   LoadBalancingAlgorithm: Dynamic   
   ```

3. 호스트 vNIC의 두 뷰를 표시 합니다.

   ```PowerShell
    Get-NetAdapter
   ```

   _**검색**_


   |        이름         |        인터페이스 설명         | ifIndex | 상태 |    Mac     | /%Linkspeed |
   |---------------------|-------------------------------------|---------|--------|-------------------|-----------|
   | vEthernet (VMSTEST) | Hyper-v 가상 이더넷 어댑터 #2 |   28    |   위쪽   | E4-1D-07-40-71 |  80 Gbps  |

   ---

4. 호스트 vNIC의 추가 속성을 봅니다. 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**검색**_


   |  이름   | IsManagementOs | VMName  |  SwitchName  | Mac | 상태 | IPAddresses |
   |---------|----------------|---------|--------------|------------|--------|-------------|
   | VMSTEST |      True      | VMSTEST | E41D2D074071 |    확인을    | &nbsp; |             |

   ---


5. 원격 VLAN 101 어댑터에 대 한 네트워크 연결을 테스트 합니다.

   ```PowerShell
   Test-NetConnection 192.168.1.5 
   ```

   _**검색**_  

   ```
   WARNING: Ping to 192.168.1.5 failed -- Status: DestinationHostUnreachable

   ComputerName   : 192.168.1.5
   RemoteAddress  : 192.168.1.5
   InterfaceAlias : vEthernet (CORP-External-Switch)
   SourceAddress  : 10.199.48.170
   PingSucceeded  : False
   PingReplyDetails (RTT) : 0 ms
   ```

## <a name="step-7-remove-the-access-vlan-setting"></a>7단계. 액세스 VLAN 설정 제거

이 단계에서는 실제 NIC에서 액세스 VLAN 설정을 제거 하 고 vSwitch를 사용 하 여 VLANID를 설정 합니다.

송신 트래픽을 잘못 된 VLAN ID로 자동 태깅 하 고 액세스 VLAN ID와 일치 하지 않는 수신 트래픽 필터링을 모두 방지 하려면 액세스 VLAN 설정을 제거 해야 합니다.

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

   _**검색**_  

   ```
   VMName VMNetworkAdapterName Mode   VlanList
   ------ -------------------- ----   --------
          VMSTEST              Access 101     
   ```


3. 네트워크 연결을 테스트 합니다.

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

   >**중요** 결과가 예제 결과와 비슷하며 ping이 실패 하 고 "경고: 192.168.1.5에 Ping을 수행 하지 못했습니다.-상태: DestinationHostUnreachable 수 없음, "" vEthernet (VMSTEST) "에 적절 한 IP 주소가 있는지 확인 합니다.
   >
   >```PowerShell
   >Get-NetIPAddress -InterfaceAlias "vEthernet (VMSTEST)"
   >```
   >
   >IP 주소가 설정 되지 않은 경우 문제를 해결 합니다.
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


4. 관리 NIC의 이름을 바꿉니다.

   ```PowerShell
   Rename-VMNetworkAdapter -ManagementOS -Name “VMSTEST” -NewName “MGT”
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**검색**_ 


   |         이름         | IsManagementOs | VMName |      SwitchName      |  Mac  | 상태 | IPAddresses |
   |----------------------|----------------|--------|----------------------|--------------|--------|-------------|
   | CORP-외부 전환 |      True      | &nbsp; | CORP-외부 전환 | 001B785768AA |  확인을  |   &nbsp;    |
   |         관리          |      True      | &nbsp; |       VMSTEST        | E41D2D074071 |  확인을  |   &nbsp;    |

   ---

5. 추가 NIC 속성을 봅니다.

   ```PowerShell
   Get-NetAdapter
   ```

   _**검색**_


   |      이름       |        인터페이스 설명         | ifIndex | 상태 |    Mac     | /%Linkspeed |
   |-----------------|-------------------------------------|---------|--------|-------------------|-----------|
   | vEthernet (MGT) | Hyper-v 가상 이더넷 어댑터 #2 |   28    |   위쪽   | E4-1D-07-40-71 |  80 Gbps  |

   ---

## <a name="step-8-test-hyper-v-vswitch-rdma"></a>8단계: Hyper-v vSwitch RDMA 테스트

다음 이미지는 hyper-v 호스트 1의 vSwitch를 포함 하 여 Hyper-v 호스트의 현재 상태를 보여 줍니다.

![Hyper-v 가상 스위치 테스트](../../media/Converged-NIC/6-datacenter-test-vswitch-rdma.jpg)

1. 이전 VLAN 설정을 보완 하기 위해 호스트 vNIC 우선 순위 태그 지정을 설정 합니다.

   ```PowerShell    
   Set-VMNetworkAdapter -ManagementOS -Name "MGT" -IeeePriorityTag on
   Get-VMNetworkAdapter -ManagementOS -Name "MGT" | fl Name,IeeePriorityTag
   ```

   _**검색**_  

   이름의 관리  
   IeeePriorityTag:  켜짐  

2. RDMA에 대해 두 개의 호스트 vNICs를 만들고 vSwitch VMSTEST에 연결 합니다.

   ```PowerShell    
   Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB1 –ManagementOS
   Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB2 –ManagementOS
   ```

3. 관리 NIC 속성을 봅니다.

   ```PowerShell    
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**검색**_ 


   |         이름         | IsManagementOs |        VMName        |  SwitchName  | Mac | 상태 | IPAddresses |
   |----------------------|----------------|----------------------|--------------|------------|--------|-------------|
   | CORP-외부 전환 |      True      | CORP-외부 전환 | 001B785768AA |    확인을    | &nbsp; |             |
   |         관리          |      True      |       VMSTEST        | E41D2D074071 |    확인을    | &nbsp; |             |
   |         SMB1         |      True      |       VMSTEST        | 00155D30AA00 |    확인을    | &nbsp; |             |
   |         SMB2         |      True      |       VMSTEST        | 00155D30AA01 |    확인을    | &nbsp; |             |

   ---

## <a name="step-9-assign-an-ip-address-to-the-smb-host-vnics-vethernet-smb1-and-vethernet-smb2"></a>9단계: SMB 호스트 vnics vethernet \(SMB1\) 및 vethernet \(SMB2에 IP 주소 할당\)

40G-1 및 40G 2 실제 어댑터에는 여전히 액세스 VLAN 101 및 102이 구성 되어 있습니다. 이로 인해 어댑터는 트래픽 태그를 만들고 ping이 성공 합니다. 이전에는 pNIC VLAN Id를 모두 0으로 구성한 다음 VMSTEST vSwitch를 VLAN 101으로 설정 했습니다. 그 후에는 MGT vNIC를 사용 하 여 원격 VLAN 101 어댑터를 ping 할 수 있었지만 현재는 VLAN 102 구성원이 없습니다.



1. NIC 트래픽이 잘못 된 VLAN ID를 사용 하 여 자동으로 태그 지정 되는 것을 방지 하 고 액세스 VLAN ID와 일치 하지 않는 수신 트래픽을 필터링 하는 것을 방지 하기 위해 실제 NIC에서 액세스 VLAN 설정을 제거 합니다.

   ```PowerShell    
   New-NetIPAddress -InterfaceAlias "vEthernet (SMB1)" -IPAddress 192.168.2.111 -PrefixLength 24
   ```

   _**검색**_  

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

   _**검색**_  

   ```
   ComputerName   : 192.168.2.5
   RemoteAddress  : 192.168.2.5
   InterfaceAlias : vEthernet (SMB1)
   SourceAddress  : 192.168.2.111
   PingSucceeded  : True
   PingReplyDetails (RTT) : 0 ms
   ```

3. Vethernet \(SMB2\)인터페이스에 대 한 새 IP 주소를 추가 합니다.

   ```PowerShell
   New-NetIPAddress -InterfaceAlias "vEthernet (SMB2)" -IPAddress 192.168.2.222 -PrefixLength 24 
   ```

   _**검색**_ 

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


5. 기존 VLAN 102에 RDMA 호스트 vNICs를 추가 합니다.

   ```PowerShell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB1" -VlanId "102" -Access -ManagementOS
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB2" -VlanId "102" -Access -ManagementOS

   Get-VMNetworkAdapterVlan -ManagementOS
   ```

   _**검색**_ 

   ```   
   VMName VMNetworkAdapterName Mode VlanList
   ------ -------------------- ---- --------
      SMB1 Access   102 
      Mgt  Access   101 
      SMB2 Access   102 
      CORP-External-Switch Untagged
   ```

6. VSwitch 집합 팀의 기본 실제 Nic와 SMB1 및 SMB2의 매핑을 검사 합니다.<p>실제 Nic에 대 한 호스트 vNIC의 연결은 임의로 수행 되며 만들고 소멸 하는 동안 균형을 재조정 하는 데 적용 됩니다. 이 경우 간접 메커니즘을 사용 하 여 현재 연결을 확인할 수 있습니다. SMB1 및 SMB2의 MAC 주소는 NIC 팀 구성원 40G-2와 연결 되어 있습니다. 40G-1에는 연결 된 SMB 호스트 vNIC 없고 SMB 호스트 vNIC가 매핑될 때까지 링크를 통한 RDMA 트래픽 사용률을 허용 하지 않기 때문에이 방법이 적합 하지 않습니다.

   ```PowerShell    
   Get-NetAdapterVPort (Preferred)

   Get-NetAdapterVmqQueue
   ```

   _**검색**_ 

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

   _**검색**_ 

   ```
   Name IsManagementOs VMName SwitchName   MacAddress   Status IPAddresses
   ---- -------------- ------ ----------   ----------   ------ -----------
   CORP-External-Switch True  CORP-External-Switch 001B785768AA {Ok}  
   Mgt  True  VMSTEST  E41D2D074071 {Ok}  
   SMB1 True  VMSTEST  00155D30AA00 {Ok}  
   SMB2 True  VMSTEST  00155D30AA01 {Ok}  
   ```

8. 네트워크 어댑터 팀 매핑을 봅니다.<p>아직 매핑을 수행 하지 않았으므로 결과에서 정보를 반환 해서는 안 됩니다.

   ```PowerShell
   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB1
   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB2
   ```


9. SMB1 및 SMB2를 별도의 실제 NIC 팀 구성원에 매핑하고 작업 결과를 확인 합니다.

   >[!IMPORTANT]
   >계속 하기 전에이 단계를 완료 해야 합니다. 그렇지 않으면 구현이 실패 합니다.

   ```PowerShell
   Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB1" -PhysicalNetAdapterName "Test-40G-1"
   Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB2" -PhysicalNetAdapterName "Test-40G-2"

   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST
   ```

   _**검색**_ 

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

    _**검색**_ 

    ```   
    Name   QueueID MacAddressVlanID Processor VmFriendlyName
    ----   ------- ---------------- --------- --------------
    TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
    TEST-40G-1 2   00-15-5D-30-AA-00 1020:17
    TEST-40G-2 1   00-15-5D-30-AA-01 1020:17
    ```


11. 두 호스트 vnics는 동일한 서브넷에 있고 VLAN ID \(102\)이 동일 하기 때문에 원격 시스템에서 연결을 테스트 합니다.

    ```PowerShell 
    Test-NetConnection 192.168.2.111
    ```

    _**검색**_   

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

    _**검색**_   

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

    _**검색**_   

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

    _**검색**_   

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

    _**검색**_   

    ```
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  True   
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  True  
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False
    ```

## <a name="step-10-validate-the-rdma-functionality"></a>10 단계. RDMA 기능의 유효성을 검사 합니다.

Vswitch 집합 팀의 두 멤버 모두에 대해 원격 시스템에서 vSwitch를 포함 하는 로컬 시스템으로 RDMA 기능의 유효성을 검사 하려고 합니다.<p>호스트 vnics \(SMB1 및 SMB2\) 는 vlan 102에 할당 되기 때문에 원격 시스템에서 vlan 102 어댑터를 선택할 수 있습니다. <p>이 예에서 NIC 40G-2는 SMB1 (192.168.2.111) 및 SMB2 (192.168.2.222)에 RDMA를 수행 합니다.

>[!TIP]
>이 시스템에서 방화벽을 사용 하지 않도록 설정 해야 할 수도 있습니다.  자세한 내용은 패브릭 정책을 참조 하세요.
>
>```PowerShell
>Set-NetFirewallProfile -All -Enabled False
>    
>Get-NetAdapterAdvancedProperty -Name "Test-40G-2"
>```
>
>_**검색**_ 
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

   _**검색**_ 

   ```
   Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
   ----  --------------------------- ------   ---------- ---------
   Test-40G-2Mellanox ConnectX-3 Pro Ethernet A...#3   3 Up   E4-1D-2D-07-43-D140 Gbps
   ```

2. 네트워크 어댑터 RDMA 정보를 확인 합니다.

   ```PowerShell
   Get-NetAdapterRdma
   ```

   _**검색**_  

   ```
   Name  InterfaceDescription Enabled
   ----  -------------------- -------
   Test-40G-2Mellanox ConnectX-3 Pro Ethernet Adap... True   
   ```

3. 첫 번째 실제 어댑터에서 RDMA 트래픽 테스트를 수행 합니다.

   ```PowerShell 
   C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.111 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**검색**_ 

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

   _**검색**_ 

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

5. 로컬에서 원격 컴퓨터로 RDMA 트래픽을 테스트 합니다.

    ```PowerShell
    Get-NetAdapter | ft –AutoSize
    ```

    _**검색**_ 

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

   _**검색**_ 

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

   _**검색**_ 

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

이 출력의 마지막 줄 "RDMA 트래픽 테스트가 성공 했습니다. RDMA 트래픽이 192.168.2.5로 전송 되었습니다. "는 어댑터에서 수렴 형 NIC를 성공적으로 구성 되었음을 보여 줍니다.

## <a name="related-topics"></a>관련 항목 

- [단일 네트워크 어댑터를 사용 하 여 수렴 형 NIC 구성](cnic-single.md)
- [수렴 형 NIC에 대 한 물리적 스위치 구성](cnic-app-switch-config.md)
- [수렴 형 NIC 구성 문제 해결](cnic-app-troubleshoot.md)
