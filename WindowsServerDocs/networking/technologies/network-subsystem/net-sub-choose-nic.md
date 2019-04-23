---
title: 네트워크 어댑터 선택
description: 이 항목은 Windows Server 2016에 대 한 네트워크 하위 시스템 성능 튜닝 지침의 일부입니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: a6615411-83d9-495f-8a6a-1ebc8b12f164
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2b50f4b286e90a450278243c0294ea0aa7f221bc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875854"
---
# <a name="choosing-a-network-adapter"></a>네트워크 어댑터 선택

>적용 대상: Windows Server (반기 채널), Windows Server 2016

구매 선택에 영향을 줄 수 있는 네트워크 어댑터의 기능 중 일부에 대해 알아보려면이 항목에서는 사용할 수 있습니다.

네트워크 집약적인 응용 프로그램에는 고성능 네트워크 어댑터가 필요합니다. 이 섹션에서는 최고의 네트워크 성능을 얻을 수 있도록 다른 네트워크 어댑터 설정을 구성 하는 방법 뿐만 아니라 네트워크 어댑터를 선택 하기 위한 몇 가지 고려 사항을 살펴봅니다.

> [!TIP]
>  Windows PowerShell을 사용 하 여 네트워크 어댑터 설정을 구성할 수 있습니다. 자세한 내용은 [Windows PowerShell의 네트워크 어댑터 Cmdlet](https://technet.microsoft.com/library/jj134956.aspx)합니다.

##  <a name="bkmk_offload"></a> 오프 로드 기능

중앙 처리 장치에서 작업 오프 로딩 \(CPU\) 네트워크 어댑터 전체 시스템 성능이 향상 되는 서버에서 CPU 사용량을 줄일 수 있습니다.

Microsoft 제품의 네트워크 스택에 하나를 오프 로드할 수 또는 네트워크 어댑터에 적합 한 네트워크 어댑터를 선택 하는 경우에 더 많은 작업이 오프 로드 기능이 있습니다. 다음 표에서 Windows Server 2016에서 사용할 수 있는 다른 오프 로드 기능에 간략하게 설명 합니다.
  
|형식 오프 로드|설명|
|------------------|-----------------|  
|TCP에 대 한 체크섬 계산|네트워크 스택을 계산과 Transmission Control Protocol의 유효성 검사를 오프 로드할 수 있습니다 \(TCP\) 체크섬에서 코드 경로 송수신 합니다. 계산 및 ipv4 유효성 검사에도 오프 로드할 수 및 IPv6 체크섬에서 코드 경로 송수신 합니다.|  
|UDP에 대 한 체크섬 계산 |계산 및 유효성 검사의 사용자 데이터 그램 프로토콜 네트워크 스택을 오프 로드할 수 있습니다 \(UDP\) 체크섬에서 코드 경로 송수신 합니다.|
|IPv4에 대 한 체크섬 계산 |네트워크 스택을 계산과 IPv4 보내고 수신 코드 경로에 체크섬의 유효성을 검사 오프 로드할 수 있습니다. |
|IPv6에 대 한 체크섬 계산 |네트워크 스택을 계산과 IPv6 보내고 수신 코드 경로에 체크섬의 유효성을 검사 오프 로드할 수 있습니다. | 
|큰 TCP 패킷의 조각화|TCP/IP 전송 계층 지원 Large Send Offload v2 (LSOv2). LSOv2를 사용 하 여 TCP/IP 전송 계층의 네트워크 어댑터에 큰 TCP 패킷의 조각화 오프 로드할 수 있습니다.|  
|수신측 배율 \(RSS\)|RSS는 네트워크의 효율적인 배포를 사용 하도록 설정 하는 네트워크 드라이버 기술 다중 프로세서 시스템에서 여러 Cpu에서 처리를 수신 합니다. RSS에 대 한 자세한 정보는이 항목의 뒷부분에 제공 됩니다.|  
|수신 세그먼트 병합 \(RSC\)|RSC는 그룹 패킷을 처리 하는 헤더를 최소화 하기 위해 함께 기능은 호스트를 수행 하는 데 필요 합니다. 최대 64KB 받은 페이로드의 처리에 대 한 단일 더 큰 패킷을에 병합할 수 있습니다. RSC에 대 한 자세한 정보는이 항목의 뒷부분에 제공 됩니다.|  
  
###  <a name="bkmk_rss"></a> 수신측 배율

Windows Server 2016, Windows Server 2012, Windows Server 2012 R2, Windows Server 2008 R2 및 Windows Server 2008 지원 수신측 \(RSS\)입니다. 

일부 서버 하드웨어 리소스를 공유 하는 여러 개의 논리적 프로세서를 사용 하 여 구성 됩니다 \(물리적 코어와 같은\) 하는 동시 멀티스레딩로 처리 됩니다 \(SMT\) 피어입니다. Intel 하이퍼 스레딩 기술은 예시입니다. RSS는 네트워크 처리를 단일 논리 프로세서 코어당 라이선스 모델을 전달합니다. 예를 들어 Intel 하이퍼 스레딩, 4 코어, 및 논리 프로세서 8을 사용 하 여 서버에서 RSS는 4 개 이상의 논리적 프로세서 네트워크 처리에 대 한 사용 합니다.  

RSS는 동일한 TCP 연결에 속하는 패킷을 순서 유지는 동일한 논리적 프로세서에서 처리 되는 논리 프로세서 간에 들어오는 네트워크 I/O 패킷이 배포 합니다. 

RSS는 잔액 UDP 유니캐스트 및 멀티 캐스트에도 로드 하 고 관련된 흐름 라우팅합니다 \(는 원본 및 대상 주소 해시에 따라 결정 됩니다\) 동일한 논리적 프로세서에 관련된 도착 순서를 유지 합니다. 이렇게 하면 사용할 수 있는 논리 프로세서 보다 적은 수의 네트워크 어댑터가 있는 서버에 대 한 수신 집약적인 시나리오에 대 한 성능과 확장성을 개선 합니다. 

#### <a name="configuring-rss"></a>RSS 구성

Windows Server 2016에서 Windows PowerShell cmdlet 및 RSS 프로필을 사용 하 여 RSS를 구성할 수 있습니다. 

사용 하 여 RSS 프로필을 정의할 수 있습니다 합니다 **– 프로필** 의 매개 변수를 **Set-netadapterrss** Windows PowerShell cmdlet.

**RSS 구성에 대 한 Windows PowerShell 명령**

다음 cmdlet을 사용 하면 보고 네트워크 어댑터당 RSS 매개 변수를 수정할 수 있습니다.
  
>[!NOTE]
>구문 및 매개 변수를 포함 하 여 각 cmdlet에 대 한 자세한 명령 참조에 대 한 다음 링크를 클릭할 수 있습니다. 또한 cmdlet 이름을 전달할 수 있습니다 **Get-help** 각 명령에 대 한 내용은 Windows PowerShell 프롬프트에서.  

- [Disable-NetAdapterRss](https://technet.microsoft.com/library/jj130892). 이 명령은 지정 된 네트워크 어댑터에서 RSS를 해제 합니다.

- [Enable-NetAdapterRss](https://technet.microsoft.com/library/jj130859). 이 명령은 지정 된 네트워크 어댑터에서 RSS를 설정 합니다.
  
- [Get-NetAdapterRss](https://technet.microsoft.com/library/jj130912). 이 명령은 지정 된 네트워크 어댑터의 RSS 속성을 검색 합니다.
  
- [Set-NetAdapterRss](https://technet.microsoft.com/library/jj130863). 이 명령은 지정 된 네트워크 어댑터에서 RSS 속성을 설정 합니다.  

#### <a name="rss-profiles"></a>RSS 프로필

사용할 수는 **– 프로필** 논리적 프로세서는 네트워크 어댑터에 할당 된 Set-netadapterrss cmdlet의 매개 변수입니다. 이 매개 변수에 대 한 사용 가능한 값은:

- **가장 가까운**합니다. 네트워크 어댑터의 기본 RSS 프로세서 다가오는 논리 프로세서 수는 것이 좋습니다. 이 프로필을 사용 하 여 운영 체제의 부하에 따라 동적으로 논리 프로세서 리 밸런스 수 있습니다.
  
- **ClosestStatic**합니다. 네트워크 어댑터의 기본 RSS 프로세서 거의 논리 프로세서 수는 것이 좋습니다. 이 프로필을 사용 하 여 운영 체제 부하에 따라 동적으로 논리 프로세서 균형 다시 맞추기 하지 않습니다.
  
- **NUMA**. 논리 프로세서 번호 일반적으로 서로 다른 NUMA 노드에 부하를 분산할 선택 됩니다. 이 프로필을 사용 하 여 운영 체제의 부하에 따라 동적으로 논리 프로세서 리 밸런스 수 있습니다.
  
- **NUMAStatic**합니다. 이 **기본 프로필**합니다. 논리 프로세서 번호 일반적으로 서로 다른 NUMA 노드에 부하를 분산할 선택 됩니다. 이 프로필을 사용 하 여 운영 체제 부하에 따라 동적으로 논리 프로세서 균형 다시 맞추기 되지 됩니다.

- **보수적인**합니다. RSS 최대한 적은 프로세서를 사용 하 여 부하를 유지 합니다. 이 옵션 인터럽트의 수를 줄일 수 있습니다.

시나리오 및 워크 로드 특성에 따라 사용할 수도 있습니다의 다른 매개 변수를 **Set-netadapterrss** Windows PowerShell cmdlet은 다음을 지정 합니다.

- 각 네트워크 어댑터 기준으로 얼마나 많은 논리 프로세서 RSS에 대 한 사용할 수 있습니다.
- 논리 프로세서의 범위에 대 한 시작 오프셋입니다.
- 네트워크 어댑터는 메모리를 할당 하는 노드.

다음은 추가적인 **Set-netadapterrss** RSS를 구성 하는 데 사용할 수 있는 매개 변수:

>[!NOTE]
>네트워크 어댑터 이름 아래 각 매개 변수에 대 한 구문 예 **이더넷** 에 대 한 예제 값으로 사용 되는 **– 이름** 의 매개 변수는 **Set-netadapterrss** 명령입니다. Cmdlet을 실행 하는 경우에 네트워크 어댑터 이름을 사용 하는 환경에 적합 한 인지를 확인 합니다.

- **\* MaxProcessors**: 사용할 RSS 프로세서의 최대 수를 설정 합니다. 이렇게 하면 응용 프로그램 트래픽을 지정 된 인터페이스에 프로세서의 최대 수에 바인딩된 것입니다. 구문 예:

     `Set-NetAdapterRss –Name “Ethernet” –MaxProcessors <value>`

- **\* BaseProcessorGroup**: NUMA 노드의 기본 프로세서 그룹을 설정합니다. 이 RSS에서 사용 되는 프로세서 배열에 영향을 줍니다. 구문 예:

     `Set-NetAdapterRss –Name “Ethernet” –BaseProcessorGroup <value>`
  
- **\* MaxProcessorGroup**: NUMA 노드의 최대 프로세서 그룹을 설정합니다. 이 RSS에서 사용 되는 프로세서 배열에 영향을 줍니다. 이 설정은 k 그룹 내에서 정렬 부하 분산 되도록 최대 프로세서 그룹을 제한 됩니다. 구문 예:

     `Set-NetAdapterRss –Name “Ethernet” –MaxProcessorGroup <value>`

- **\* BaseProcessorNumber**: 기본 프로세서 수가 NUMA 노드를 설정합니다. 이 RSS에서 사용 되는 프로세서 배열에 영향을 줍니다. 그러면 네트워크 어댑터에서 프로세서를 분할 합니다. 이 각 어댑터에 할당 되는 범위의 RSS 프로세서의 첫 번째 논리 프로세서. 구문 예:

     `Set-NetAdapterRss –Name “Ethernet” –BaseProcessorNumber <Byte Value>`

- **\* NumaNode**: 각 네트워크 어댑터에서 메모리를 할당할 수는 NUMA 노드. 이 k 그룹 내에서 또는 서로 다른 k 그룹에서 수 있습니다. 구문 예:

     `Set-NetAdapterRss –Name “Ethernet” –NumaNodeID <value>`

- **\* NumberofReceiveQueues**: 논리 프로세서 수 수신 트래픽에 미달 사용 같습니다 \(예를 들어에서 본된 작업 관리자로\), 네트워크 어댑터에서 지원 되는 최대 2의 기본값과에서 RSS 큐 수를 늘릴 수 있습니다 . 네트워크 어댑터 드라이버의 일부로 RSS 큐 수를 변경 하는 옵션이 있을 수 있습니다. 구문 예:

     `Set-NetAdapterRss –Name “Ethernet” –NumberOfReceiveQueues <value>`

자세한 내용은 다운로드 하려면 다음 링크를 클릭 [확장 가능한 네트워킹: 수신 처리 병목 현상을 제거-RSS 소개](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/NDIS_RSS.doc) Word 형식으로 합니다.
  
#### <a name="understanding-rss-performance"></a>RSS 성능 이해

RSS 튜닝 구성 및 로드 밸런싱 논리를 이해 해야 합니다. RSS 설정을 사항이 적용을 실행할 때 출력을 검토할 수를 확인 합니다 **Get-netadapterrss** Windows PowerShell cmdlet. 다음은이 cmdlet의 출력 예입니다.
  
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

설정 된 매개 변수를 출력 하는 것 외에도 출력의 핵심적인 측면은 간접 테이블 출력입니다. 간접 참조 테이블에는 들어오는 트래픽을 분산 하는 데 사용 되는 해시 테이블 버킷의 표시 됩니다. 이 예제에서는 n:c 표기법을 지정 하면 Numa K-들어오는 트래픽을 전달 하는 데 사용 되는 그룹: CPU 인덱스 쌍입니다. 고유 정확히 2 개 항목 표시 (0:0, 0:4)를 k 그룹 0/cpu0 및 k 그룹 0/cpu 4, 각각 나타냅니다.

이 시스템 (k 그룹 0)에 n k 그룹이 하나만 (여기서 n < = 128) 간접 테이블 항목입니다. 수신 큐의 수는 2, 2 개의 프로세서로 설정 되어 있으므로 (0:0, 0:4) 선택-최대 프로세서 8로 설정 되어 있지만 됩니다. 실제로 간접 참조 테이블에만 사용할 수 있는 8에서 2 개 Cpu를 사용 하 여 들어오는 트래픽을 해시 됩니다.

Cpu를 완전히 활용 하려면 RSS 수신 큐의 수는 최대 프로세서 보다 크거나 같은 이어야 합니다. 이전 예제에서는 8 이상에 수신 큐 설정 되어야 합니다.

#### <a name="nic-teaming-and-rss"></a>NIC 팀 및 RSS

NIC 팀을 사용 하 여 다른 네트워크 인터페이스 카드 팀 구성 하는 네트워크 어댑터에서 RSS는 사용할 수 있습니다. 이 시나리오에서는 기본 실제 네트워크 어댑터는 RSS를 사용 하도록 구성할 수 있습니다. 사용자는 팀으로 구성 된 네트워크 어댑터에서 RSS cmdlet을 설정할 수 없습니다.
  
###  <a name="bkmk_rsc"></a> 세그먼트 RSC (수신 통합)

수신 세그먼트 병합 \(RSC\) 수신된 된 데이터의 지정 된 기간 동안 처리 되는 IP 헤더의 수를 줄여 성능에 도움이 됩니다. 그룹화 하 여 수신된 된 데이터의 성능을 확장 하는 데 사용할 \(병합 또는\) 작은 패킷을 더 큰 단위로 합니다.

이 방법은 대부분 처리량 향상을 표시 하는 혜택을 사용 하 여 대기 시간이 발생할 수 있습니다. RSC는 받은 과도 한 워크 로드에 대 한 처리량을 높이기 위한 것이 좋습니다. RSC를 지 원하는 네트워크 어댑터를 배포 하는 것이 좋습니다. 

이러한 네트워크 어댑터, RSC 켜져 있는지 확인 하십시오 \(이것이 기본 설정\)특정 워크 로드는 경우가 아니라면 \(예를 들어, 짧은 대기 시간, 처리량 네트워킹 낮은\) RSC가 off에서 표시 혜택 .

#### <a name="understanding-rsc-diagnostics"></a>RSC 진단 이해

Windows PowerShell cmdlet을 사용 하 여 RSC를 진단할 수 있습니다 **Get NetAdapterRsc** 하 고 **Get NetAdapterStatistics**합니다.

Get-NetAdapterRsc cmdlet을 실행할 때 다음은 예제 출력입니다.

```  

PS C:\Users\Administrator> Get-NetAdapterRsc  
  
Name                       IPv4Enabled  IPv6Enabled  IPv4Operational IPv6Operational               IPv4FailureReason              IPv6Failure  
                                            Reason  
----                           -----------  -----------  --------------- --------------- ----------------- ------------  
Ethernet                       True         False        True            False                  NoFailure       NicProperties  
  
```  

합니다 **가져올** cmdlet RSC 인터페이스에서 사용 되는지 여부 및 TCP를 작동 상태로 되도록 RSC를 사용 하도록 설정 하는지 여부를 보여 줍니다. 실패 이유는 해당 인터페이스에는 RSC를 사용 하도록 설정 하는 데 실패 하는 방법에 대 한 세부 정보를 제공 합니다.

이전 시나리오에서는 IPv4 RSC를 인터페이스에 지원 되는 및 운영있지 않습니다. 진단 오류를 이해 하려면 결합 된 바이트 또는 발생 하는 예외를 볼 수 있습니다. 병합 문제를 나타내는 값을 제공합니다.

Get-NetAdapterStatistics cmdlet을 실행할 때 다음은 예제 출력입니다.

```  
PS C:\Users\Administrator> $x = Get-NetAdapterStatistics “myAdapter”   
PS C:\Users\Administrator> $x.rscstatistics  
  
CoalescedBytes       : 0  
CoalescedPackets     : 0  
CoalescingEvents     : 0  
CoalescingExceptions : 0  
  
```  

#### <a name="rsc-and-virtualization"></a>RSC 및 가상화

호스트 네트워크 어댑터에서 Hyper-v 가상 스위치에 바인딩되지 않은 경우 실제 호스트에 RSC만 지원 됩니다. RSC는 호스트에서 Hyper-v 가상 스위치에 바인딩된 경우 운영 체제에서 비활성화 됩니다. 또한 가상 머신 얻지 RSC의 이점은 가상 네트워크 어댑터는 RSC를 지원 하지 않기 때문입니다.

RSC를 가상 머신에 대해 사용할 수 있습니다 때 단일 루트 입출력 가상화 \(SR-IOV\) 사용 가능 합니다. 이 경우 가상 함수 지원 RSC 기능입니다. 따라서 가상 컴퓨터는 또한 RSC의 혜택을 받습니다.

##  <a name="bkmk_resources"></a> 네트워크 어댑터 리소스

몇 가지 네트워크 어댑터는 적극적으로 최적의 성능을 얻기 위해 해당 리소스를 관리 합니다. 여러 네트워크 어댑터를 사용 하면 수동으로 사용 하 여 리소스를 구성 하는 **고급 네트워킹** 어댑터에 대 한 탭 합니다. 이러한 어댑터에 대 한 수신 버퍼의 수를 포함 하 여 매개 변수의 숫자 값을 설정할 수 있으며 버퍼를 보낼 수 있습니다.

다음 Windows PowerShell cmdlet 사용 하 여 네트워크 어댑터 리소스 구성 간소화 됩니다.

- [Get-NetAdapterAdvancedProperty](https://technet.microsoft.com/library/jj130901.aspx)

- [Set-NetAdapterAdvancedProperty](https://technet.microsoft.com/library/jj130894.aspx)

- [Enable-NetAdapter](https://technet.microsoft.com/library/jj130876.aspx)

- [Enable-NetAdapterBinding](https://technet.microsoft.com/library/jj130913.aspx)

- [Enable-NetAdapterChecksumOffload](https://technet.microsoft.com/library/jj130918.aspx)

- [Enable-NetAdapterIPSecOffload](https://technet.microsoft.com/library/jj130890.aspx)

- [Enable-NetAdapterLso](https://technet.microsoft.com/library/jj130922.aspx)

- [Enable-NetAdapterPowerManagement](https://technet.microsoft.com/library/jj130907.aspx)

- [Enable-NetAdapterQos](https://technet.microsoft.com/library/jj130866.aspx)

- [Enable-NetAdapterRDMA](https://technet.microsoft.com/library/jj130909.aspx)

- [Enable-NetAdapterSriov](https://technet.microsoft.com/library/jj130899.aspx)

자세한 내용은 [Windows PowerShell의 네트워크 어댑터 Cmdlet](https://technet.microsoft.com/library/jj134956.aspx)합니다.

이 가이드의 모든 항목에 대 한 링크를 참조 하세요 [네트워크 하위 시스템 성능 튜닝](net-sub-performance-top.md)합니다.