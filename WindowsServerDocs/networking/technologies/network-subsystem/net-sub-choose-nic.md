---
title: 네트워크 어댑터 선택
description: 이 항목은 Windows Server 2016에 대 한 네트워크 하위 시스템 성능 조정 가이드의 일부입니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: a6615411-83d9-495f-8a6a-1ebc8b12f164
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 5e1ed095b3180f3aebd25381ec9086445bb141ec
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316620"
---
# <a name="choosing-a-network-adapter"></a>네트워크 어댑터 선택

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 구매 선택에 영향을 줄 수 있는 네트워크 어댑터의 일부 기능에 대해 알아볼 수 있습니다.

네트워크를 많이 사용 하는 응용 프로그램에는 고성능 네트워크 어댑터가 필요 합니다. 이 섹션에서는 네트워크 어댑터를 선택 하기 위한 몇 가지 고려 사항 뿐만 아니라 최적의 네트워크 성능을 얻기 위해 다양 한 네트워크 어댑터 설정을 구성 하는 방법을 살펴봅니다.

> [!TIP]
>  Windows PowerShell을 사용 하 여 네트워크 어댑터 설정을 구성할 수 있습니다. 자세한 내용은 [Windows PowerShell의 네트워크 어댑터 cmdlet](https://docs.microsoft.com/powershell/module/netadapter)(영문)을 참조 하세요.

##  <a name="offload-capabilities"></a><a name="bkmk_offload"></a>오프 로드 기능

중앙 처리 장치 \(CPU\)에서 네트워크 어댑터로 작업을 오프 로드 하면 서버에서 CPU 사용량을 줄일 수 있으며이로 인해 전체 시스템 성능이 향상 됩니다.

Microsoft 제품의 네트워크 스택은 적절 한 오프 로드 기능이 있는 네트워크 어댑터를 선택 하는 경우 하나 이상의 작업을 네트워크 어댑터로 오프 로드할 수 있습니다. 다음 표에서는 Windows Server 2016에서 사용할 수 있는 여러 오프 로드 기능에 대해 간략히 설명 합니다.
  
|오프 로드 유형|설명|
|------------------|-----------------|  
|TCP에 대 한 체크섬 계산|네트워크 스택은 송신 및 수신 코드 경로에서 TCP\) 체크섬 \(전송 제어 프로토콜의 계산과 유효성 검사를 오프 로드할 수 있습니다. 송신 및 수신 코드 경로에서 IPv4 및 IPv6 체크섬의 계산과 유효성 검사를 오프 로드할 수도 있습니다.|  
|UDP에 대 한 체크섬 계산 |네트워크 스택은 송신 및 수신 코드 경로에서 UDP\) 체크섬 \(사용자 데이터 그램 프로토콜의 계산과 유효성 검사를 오프 로드할 수 있습니다.|
|IPv4에 대 한 체크섬 계산 |네트워크 스택은 송신 및 수신 코드 경로에서 IPv4 체크섬의 계산과 유효성 검사를 오프 로드할 수 있습니다. |
|IPv6에 대 한 체크섬 계산 |네트워크 스택은 송신 및 수신 코드 경로에서 IPv6 체크섬의 계산과 유효성 검사를 오프 로드할 수 있습니다. | 
|대량 TCP 패킷 조각화|TCP/IP 전송 계층은 LSOv2 (Large Send Offload) v2를 지원 합니다. LSOv2를 사용 하면 TCP/IP 전송 계층이 네트워크 어댑터에 대 한 대량 TCP 패킷의 조각화를 오프 로드할 수 있습니다.|  
|RSS\) \(수신측 배율|RSS는 다중 프로세서 시스템의 여러 Cpu에서 네트워크 수신 처리를 효율적으로 배포할 수 있게 해 주는 네트워크 드라이버 기술입니다. RSS에 대 한 자세한 내용은이 항목의 뒷부분에 제공 됩니다.|  
|RSC\) \(수신 세그먼트 통합|RSC는 호스트를 수행 하는 데 필요한 헤더 처리를 최소화 하기 위해 패킷을 그룹화 하는 기능입니다. 최대 64 KB의 수신 된 페이로드는 처리를 위해 하나의 큰 패킷으로 결합 될 수 있습니다. RSC에 대 한 자세한 내용은이 항목의 뒷부분에 제공 됩니다.|  
  
###  <a name="receive-side-scaling"></a><a name="bkmk_rss"></a>수신측 배율

Windows Server 2016, Windows Server 2012, Windows Server 2012 R2, Windows Server 2008 R2 및 Windows Server 2008에서는 RSS\)\(수신측 크기 조정을 지원 합니다. 

일부 서버는 물리적 코어\)와 같은 \(하드웨어 리소스를 공유 하는 여러 논리 프로세서로 구성 되며, 동시에 다중 스레딩 \(SMT\) 피어로 처리 됩니다. Intel 하이퍼 스레딩 기술은 예입니다. RSS는 네트워크 처리를 코어 당 최대 하나의 논리적 프로세서로 보냅니다. 예를 들어 Intel 하이퍼 스레딩, 4 코어 및 8 개의 논리적 프로세서가 있는 서버에서 RSS는 네트워크 처리를 위해 논리적 프로세서를 4 개 이하로 사용 합니다.  

RSS는 들어오는 네트워크 i/o 패킷을 논리적 프로세서 간에 분산 하 여 동일한 TCP 연결에 속하는 패킷이 동일한 논리 프로세서에서 처리 되도록 하 여 순서를 유지 합니다. 

또한 RSS는 UDP 유니캐스트 및 멀티 캐스트 트래픽의 부하를 분산 하 고, 관련 된 도착 한의 순서를 유지 하면서 원본 및 대상 주소를 동일한 논리 프로세서에\) 해시 하 여 결정 되는 관련 흐름 \(를 라우팅합니다. 이를 통해 적합 한 논리 프로세서를 사용 하는 것 보다 네트워크 어댑터가 더 작은 서버에 대 한 수신 집약적 시나리오의 확장성 및 성능을 향상 시킬 수 있습니다. 

#### <a name="configuring-rss"></a>RSS 구성

Windows Server 2016에서는 Windows PowerShell cmdlet 및 RSS 프로필을 사용 하 여 RSS를 구성할 수 있습니다. 

**Set-netadapterrss** Windows PowerShell cmdlet의 **– Profile** 매개 변수를 사용 하 여 RSS 프로필을 정의할 수 있습니다.

**RSS 구성에 대 한 Windows PowerShell 명령**

다음 cmdlet을 사용 하 여 네트워크 어댑터 별로 RSS 매개 변수를 확인 하 고 수정할 수 있습니다.
  
>[!NOTE]
>구문 및 매개 변수를 포함 하 여 각 cmdlet에 대 한 자세한 명령 참조를 보려면 다음 링크를 클릭 하십시오. 또한 Windows PowerShell 프롬프트에서 cmdlet 이름을 **get-help** 에 전달 하 여 각 명령에 대 한 자세한 내용을 확인할 수 있습니다.  

- [Set-netadapterrss를 사용 하지](https://docs.microsoft.com/powershell/module/netadapter/Disable-NetAdapterRss)않습니다. 이 명령은 지정한 네트워크 어댑터에서 RSS를 사용 하지 않도록 설정 합니다.

- [Set-netadapterrss를 사용](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterRss)합니다. 이 명령은 지정한 네트워크 어댑터에서 RSS를 사용 하도록 설정 합니다.
  
- [Set-netadapterrss](https://docs.microsoft.com/powershell/module/netadapter/Get-NetAdapterRss). 이 명령은 지정한 네트워크 어댑터의 RSS 속성을 검색 합니다.
  
- [Set-netadapterrss를 설정](https://docs.microsoft.com/powershell/module/netadapter/Set-NetAdapterRss)합니다. 이 명령은 지정한 네트워크 어댑터에서 RSS 속성을 설정 합니다.  

#### <a name="rss-profiles"></a>RSS 프로필

Set-netadapterrss cmdlet의 **– Profile** 매개 변수를 사용 하 여 네트워크 어댑터에 할당 되는 논리 프로세서를 지정할 수 있습니다. 이 매개 변수에 사용할 수 있는 값은 다음과 같습니다.

- **가장 가깝습니다**. 네트워크 어댑터의 기본 RSS 프로세서에 가까운 논리 프로세서 번호를 선호 합니다. 이 프로필을 사용 하면 운영 체제에서 로드에 따라 동적으로 논리적 프로세서의 균형을 다시 조정할 수 있습니다.
  
- **Closeststatic**. 네트워크 어댑터의 기본 RSS 프로세서 근처의 논리적 프로세서 수가 선호 됩니다. 이 프로필을 사용 하는 경우 운영 체제는 부하에 따라 논리적 프로세서를 동적으로 균형을 다시 조정 하지 않습니다.
  
- **NUMA**. 논리 프로세서 번호는 일반적으로 부하를 분산 하기 위해 서로 다른 NUMA 노드에서 선택 됩니다. 이 프로필을 사용 하면 운영 체제에서 로드에 따라 동적으로 논리적 프로세서의 균형을 다시 조정할 수 있습니다.
  
- **Numastatic**. 이 프로필은 **기본 프로필**입니다. 논리 프로세서 번호는 일반적으로 부하를 분산 하기 위해 서로 다른 NUMA 노드에서 선택 됩니다. 이 프로필을 사용 하면 운영 체제에서 로드에 따라 논리적 프로세서를 동적으로 균형을 다시 조정 하지 않습니다.

- **보수적인**. RSS는 최대한 적은 수의 프로세서를 사용 하 여 부하를 유지 합니다. 이 옵션은 인터럽트의 수를 줄이는 데 도움이 됩니다.

시나리오 및 워크 로드 특성에 따라 **Set-netadapterrss** Windows PowerShell cmdlet의 다른 매개 변수를 사용 하 여 다음을 지정할 수도 있습니다.

- 네트워크 어댑터를 기준으로 RSS에 사용할 수 있는 논리 프로세서 수입니다.
- 논리적 프로세서 범위의 시작 오프셋입니다.
- 네트워크 어댑터에서 메모리를 할당 하는 노드입니다.

RSS를 구성 하는 데 사용할 수 있는 추가 **set-netadapterrss** 매개 변수는 다음과 같습니다.

>[!NOTE]
>아래 각 매개 변수에 대 한 예제 구문에서 네트워크 어댑터 이름 **이더넷** 은 **Set-netadapterrss** 명령의 **– name** 매개 변수에 대 한 예제 값으로 사용 됩니다. Cmdlet을 실행할 때 사용 하는 네트워크 어댑터 이름이 사용자 환경에 적합 한지 확인 합니다.

- **\* maxprocessors**: 사용할 RSS 프로세서의 최대 수를 설정 합니다. 이렇게 하면 응용 프로그램 트래픽이 지정 된 인터페이스의 최대 프로세서 수에 바인딩됩니다. 구문 예:

     `Set-NetAdapterRss –Name “Ethernet” –MaxProcessors <value>`

- **\* BaseProcessorGroup**: NUMA 노드의 기본 프로세서 그룹을 설정 합니다. 이는 RSS에서 사용 되는 프로세서 배열에 영향을 줍니다. 구문 예:

     `Set-NetAdapterRss –Name “Ethernet” –BaseProcessorGroup <value>`
  
- **\* MaxProcessorGroup**: NUMA 노드의 최대 프로세서 그룹을 설정 합니다. 이는 RSS에서 사용 되는 프로세서 배열에 영향을 줍니다. 이렇게 설정 하면 부하 분산이 k 그룹 내에 정렬 되도록 최대 프로세서 그룹이 제한 됩니다. 구문 예:

     `Set-NetAdapterRss –Name “Ethernet” –MaxProcessorGroup <value>`

- **\* BaseProcessorNumber**: NUMA 노드의 기본 프로세서 번호를 설정 합니다. 이는 RSS에서 사용 되는 프로세서 배열에 영향을 줍니다. 이렇게 하면 네트워크 어댑터 간에 프로세서를 분할할 수 있습니다. 각 어댑터에 할당 되는 RSS 프로세서 범위의 첫 번째 논리 프로세서입니다. 구문 예:

     `Set-NetAdapterRss –Name “Ethernet” –BaseProcessorNumber <Byte Value>`

- **\* NumaNode**: 각 네트워크 어댑터에서 메모리를 할당할 수 있는 NUMA 노드입니다. 이는 k 그룹 내에 있거나 다른 k 그룹에 있을 수 있습니다. 구문 예:

     `Set-NetAdapterRss –Name “Ethernet” –NumaNodeID <value>`

- **\* NumberofReceiveQueues**: 논리 프로세서가 수신 \(트래픽에 대해 미달 사용 되는 것 처럼 보이는 경우, 예를 들어 작업 관리자\)에서 볼 수 있듯이 RSS 큐의 수를 기본값인 2에서 네트워크 어댑터에서 지 원하는 최대 수로 늘릴 수 있습니다. 네트워크 어댑터에는 드라이버의 일부로 RSS 큐의 수를 변경 하는 옵션이 있을 수 있습니다. 구문 예:

     `Set-NetAdapterRss –Name “Ethernet” –NumberOfReceiveQueues <value>`

자세한 내용을 보려면 다음 링크를 클릭 하 여 [확장 가능한 네트워킹을 다운로드 하세요. 수신 처리 병목 현상 제거-](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/NDIS_RSS.doc) Word 형식으로 RSS를 소개 합니다.
  
#### <a name="understanding-rss-performance"></a>RSS 성능 이해

RSS를 튜닝 하려면 구성 및 부하 분산 논리를 이해 해야 합니다. RSS 설정이 적용 되었는지 확인 하려면 **Set-netadapterrss** Windows PowerShell cmdlet을 실행할 때 출력을 검토할 수 있습니다. 다음은이 cmdlet의 예제 출력입니다.
  
```

PS C:\Users\Administrator> get-netadapterrss  
Name                           : testnic 2  
InterfaceDescription           : Broadcom BCM5708C NetXtreme II GigE (NDIS VBD Client) #66
Enabled                        : True
NumberOfReceiveQueues          : 2
Profile                        : NUMAStatic
BaseProcessor: [Group:Number]  : 0:0
MaxProcessor: [Group:Number]   : 0:15
MaxProcessors                  : 8
  
IndirectionTable: [Group:Number]:
     0:0    0:4    0:0    0:4    0:0    0:4    0:0    0:4  
…   
(# indirection table entries are a power of 2 and based on # of processors)  
…   
                          0:0    0:4    0:0    0:4    0:0    0:4    0:0    0:4  
```  

설정 된 매개 변수를 에코 하는 것 외에도 출력의 주요 측면은 간접 테이블 출력입니다. 간접 참조 테이블에는 들어오는 트래픽을 분산 하는 데 사용 되는 해시 테이블 버킷이 표시 됩니다. 이 예에서 n:c 표기법은 들어오는 트래픽을 전달 하는 데 사용 되는 Numa K 그룹: CPU 인덱스 쌍을 지정 합니다. 2 개의 고유 항목 (0:0 및 0:4)이 표시 되며, 각각 k 그룹 0/cpu0 및 k 그룹 0/cpu 4를 나타냅니다.

이 시스템에는 k 그룹 1 개 (k-그룹 0)와 n (where n < = 128) 간접 참조 테이블 항목이 있습니다. 수신 큐의 수를 2로 설정 했기 때문에 최대 프로세서가 8로 설정 된 경우에도 프로세서 2 개 (0:0, 0:4)만 선택 됩니다. 실제로 간접 참조 테이블은 들어오는 트래픽을 해시 하 여 사용할 수 있는 8 개 중에서 Cpu 2 개를 사용 합니다.

Cpu를 완전히 활용 하려면 RSS 수신 큐의 수가 최대 프로세서 수보다 크거나 같아야 합니다. 이전 예제에서 수신 큐는 8 이상으로 설정 해야 합니다.

#### <a name="nic-teaming-and-rss"></a>NIC 팀 및 RSS

NIC 팀을 사용 하 여 다른 네트워크 인터페이스 카드와 팀으로 구성 된 네트워크 어댑터에서 RSS를 사용 하도록 설정할 수 있습니다. 이 시나리오에서는 기본 실제 네트워크 어댑터만 RSS를 사용 하도록 구성할 수 있습니다. 사용자가 팀으로 구성 된 네트워크 어댑터에서 RSS cmdlet을 설정할 수 없습니다.
  
###  <a name="receive-segment-coalescing-rsc"></a><a name="bkmk_rsc"></a>RSC (수신 세그먼트 통합)

지정 된 용량의 수신 데이터에 대해 처리 되는 IP 헤더의 수를 줄여 \(RSC\)의 수신 세그먼트 병합을 사용할 수 있습니다. 이를 사용 하 여 \(를 그룹화 하거나 더 작은 패킷\) 더 큰 단위로 결합 하 여 수신 된 데이터의 성능을 확장할 수 있습니다.

이 접근 방식은 처리량 향상에 주로 표시 되는 이점 때문에 대기 시간에 영향을 줄 수 있습니다. RSC는 받은 작업량이 많은 워크 로드에 대 한 처리량을 늘리는 것이 좋습니다. RSC를 지 원하는 네트워크 어댑터를 배포 하는 것이 좋습니다. 

이러한 네트워크 어댑터에는 rsc의 혜택을 표시 하는 낮은 대기 시간, 낮은 처리량 네트워킹\)와 같이 특정 워크 로드 \(없는 한,\)기본 설정인 RSC가 \(되어 있는지 확인 합니다.

#### <a name="understanding-rsc-diagnostics"></a>RSC 진단 이해

Windows PowerShell cmdlet **NetAdapterRsc** 및 **NetAdapterStatistics**를 사용 하 여 RSC를 진단할 수 있습니다.

다음은 NetAdapterRsc cmdlet을 실행할 때의 예제 출력입니다.

```  

PS C:\Users\Administrator> Get-NetAdapterRsc  
  
Name                       IPv4Enabled  IPv6Enabled  IPv4Operational IPv6Operational               IPv4FailureReason              IPv6Failure  
                                            Reason  
----                           -----------  -----------  --------------- --------------- ----------------- ------------  
Ethernet                       True         False        True            False                  NoFailure       NicProperties  
  
```  

**Get** cmdlet은 인터페이스에서 rsc를 사용 하도록 설정 했는지 여부와 TCP가 rsc를 작동 상태로 설정할 수 있는지 여부를 표시 합니다. 실패 이유는 해당 인터페이스에서 RSC를 사용 하도록 설정 하는 오류에 대 한 세부 정보를 제공 합니다.

이전 시나리오에서 IPv4 RSC는 인터페이스에서 지원 되 고 작동 합니다. 진단 오류를 이해 하기 위해 병합 된 바이트 또는 발생 한 예외를 확인할 수 있습니다. 이는 결합 문제를 나타냅니다.

다음은 NetAdapterStatistics cmdlet을 실행할 때의 예제 출력입니다.

```  
PS C:\Users\Administrator> $x = Get-NetAdapterStatistics “myAdapter”   
PS C:\Users\Administrator> $x.rscstatistics  
  
CoalescedBytes       : 0  
CoalescedPackets     : 0  
CoalescingEvents     : 0  
CoalescingExceptions : 0  
  
```  

#### <a name="rsc-and-virtualization"></a>RSC 및 가상화

RSC는 호스트 네트워크 어댑터가 Hyper-v 가상 스위치에 바인딩되지 않은 경우에만 실제 호스트에서 지원 됩니다. 호스트가 Hyper-v 가상 스위치에 바인딩된 경우 운영 체제에서 RSC를 사용 하지 않도록 설정 합니다. 또한 가상 네트워크 어댑터는 RSC를 지원 하지 않기 때문에 가상 머신은 RSC의 이점을 얻을 수 없습니다.

단일 루트 입/출력 가상화 \(SR-IOV\) 사용 하도록 설정 된 경우 가상 머신에 RSC를 사용 하도록 설정할 수 있습니다. 이 경우 가상 함수는 RSC 기능을 지원 합니다. 따라서 virtual machines에는 RSC의 이점도 제공 됩니다.

##  <a name="network-adapter-resources"></a><a name="bkmk_resources"></a>네트워크 어댑터 리소스

일부 네트워크 어댑터는 최적의 성능을 얻기 위해 리소스를 적극적으로 관리 합니다. 여러 네트워크 어댑터를 사용 하면 어댑터에 대 한 **고급 네트워킹** 탭을 사용 하 여 리소스를 수동으로 구성할 수 있습니다. 이러한 어댑터의 경우 수신 버퍼 수와 송신 버퍼의 수를 포함 하 여 다양 한 매개 변수 값을 설정할 수 있습니다.

다음 Windows PowerShell cmdlet을 사용 하 여 네트워크 어댑터 리소스를 간단 하 게 구성할 수 있습니다.

- [NetAdapterAdvancedProperty](https://docs.microsoft.com/powershell/module/netadapter/Get-NetAdapterAdvancedProperty)

- [NetAdapterAdvancedProperty](https://docs.microsoft.com/powershell/module/netadapter/Set-NetAdapterAdvancedProperty)

- [Get-netadapter](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapte)

- [NetAdapterBinding](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterBinding)

- [NetAdapterChecksumOffload](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterChecksumOffload)

- [NetAdapterIPSecOffload](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterChecksumOffload)

- [NetAdapterLso](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterLso)

- [NetAdapterPowerManagement](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterPowerManagement)

- [Get-netadapterqos](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterQos)

- [NetAdapterRDMA](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterRDMA)

- [이렇게 하려면 get-netadaptersriov](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterSriov)

자세한 내용은 [Windows PowerShell의 네트워크 어댑터 cmdlet](https://docs.microsoft.com/powershell/module/netadapter)(영문)을 참조 하세요.

이 가이드의 모든 항목에 대 한 링크는 [네트워크 하위 시스템 성능 튜닝](net-sub-performance-top.md)을 참조 하세요.
