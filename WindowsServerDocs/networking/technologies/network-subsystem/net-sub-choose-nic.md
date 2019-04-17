---
title: 네트워크 어댑터를 선택합니다.
description: 이 항목은 Windows Server 2016 용 네트워크 하위 시스템 성능 조정 가이드의 일부입니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: a6615411-83d9-495f-8a6a-1ebc8b12f164
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4b3b9d206273dfd0e9115ebc27cf28aa960bfb0f
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="choosing-a-network-adapter"></a>네트워크 어댑터를 선택합니다.

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 구매 선택 항목이 영향을 미칠 수 있는 네트워크 어댑터의 기능 중 일부를 알아보려면 사용할 수 있습니다.

네트워크를 많이 사용 응용 프로그램 성능이 네트워크 어댑터가 필요합니다. 이 섹션으로 네트워크 어댑터 네트워크 최상의 성능을 발휘 합니다 서로 다른 네트워크 어댑터 설정을 구성 하는 방법을 선택 하기 위한 몇 가지 사항을 탐색 합니다.

> [!TIP]
>  Windows PowerShell를 사용 하 여 네트워크 어댑터 설정을 구성할 수 있습니다. 자세한 내용은 참조 [Windows powershell에서 네트워크 어댑터 Cmdlet](https://technet.microsoft.com/library/jj134956.aspx)합니다.

##  <a name="bkmk_offload"></a>오프 기능

네트워크 어댑터에 \(CPU\) 작업 중앙 처리 장치에서 오프 로드 시스템 성능을 개선 하는 서버에 cpu를 많이 사용을 줄일 수 있습니다.

Microsoft 제품에는 네트워크 스택에서 하나 오프 로드할 수 줄이거나에 적합 한 네트워크 어댑터를 선택 하는 경우 네트워크 어댑터에 더 많은 작업 기능입니다. 다음 표에서 Windows Server 2016에 사용할 수 있는 다른 오프 로드 기능의 간략하게 설명 합니다.
  
|오프 유형|설명|
|------------------|-----------------|  
|Tcp 검사 계산|네트워크 스택 오프 계산 로드할 수 및에 전송 제어 프로토콜 \(TCP\) 검사 값의 유효성을 검사 코드 경로 주고받을 합니다. 계산 및 IPv4의 유효성을 검사 오프도 수 및에 IPv6 검사 값 코드 경로 주고받을 합니다.|  
|UDP에 대 한 검사 계산 |네트워크 스택 오프 계산 로드할 수와의 사용자 데이터 그램 프로토콜 \(UDP\) 검사 값의 유효성을 검사 코드 경로 주고받을 합니다.|
|I p v 4 검사 계산 |네트워크 스택 계산 및에 검사 값 코드 경로 주고받을 IPv4의 유효성을 검사 오프 수 있습니다. |
|Ipv6 검사 계산 |네트워크 스택 계산과 유효성 검사에 값 코드 경로 주고받을 ipv6 오프 수 있습니다. | 
|큰 TCP 패킷 분할|TCP/IP transport layer 지원 큰 전송 오프 v2 (LSOv2). LSOv2와 TCP/IP transport layer 네트워크 어댑터에 큰 TCP 패킷 분할을 오프 수 있습니다.|  
|수신 측면 \(RSS\) 크기 조정|RSS 네트워크 효율적인 배포 수 있도록 하는 네트워크 드라이버 기술 다중 프로세서 시스템에서 처리 여러 Cpu를 통해 수신입니다. RSS에 대 한 자세한 내용은이 항목 뒷부분에 제공 됩니다.|  
|병합 \(RSC\) 세그먼트 받기|RSC 그룹 패킷을 최소화 처리 하는 헤더에 함께 기능은 호스트 수행 하는 데 필요한입니다. 받은 페이로드 64 KB 최대 처리에 대 한 단일 더 큰 패킷을로 결합 될 수 있습니다. 이 항목 뒷부분에서 RSC에 대 한 자세한 내용을 제공 됩니다.|  
  
###  <a name="bkmk_rss"></a>수신 측면 크기 조정

Windows Server 2016, Windows Server 2012, Windows Server 2012 R2, Windows Server 2008 R2 및 Windows Server 2008 \(RSS\) 측면 크기를 지원합니다. 

일부 서버 하드웨어 리소스를 공유 하는 여러 논리 프로세서도 구성 \ (예: 물리적 core\) 피어 동시 다중 연산을 \(SMT\) 취급 하는 되 고 있습니다. Intel 하이퍼 스레드 기술 예입니다. RSS는 네트워크 처리 최대 1 개 논리 코어 프로세서를 안내합니다. 예를 들어, Intel Hyper 스레드, 4 코어 및 8 논리 프로세서와 서버, RSS 네트워크 처리에 대 한 논리 4 더 이상 프로세서 사용합니다.  

RSS 같은 TCP 연결에 속하는 패킷을 순서를 보존 하는 동일한 논리 프로세서에서 처리 됩니다 되도록 논리 프로세서 들어오는 네트워크 I/O 패킷의 배포 합니다. 

RSS 잔액 UDP 유니캐스트와 멀티 캐스트 교통도 로드 하 고 관련된 흐름 라우팅하기 \ (되는 따른 원본과 대상 addresses\ 해시) 동일한 논리 프로세서 관련된 출근 순서를 유지 합니다. 이렇게 하면 확장성 및 적격 논리 프로세스를 수행 하는 것 보다 더 적은 네트워크 어댑터가 있어야 하는 서버에 대 한 수신 많이 시나리오에 대 한 성능을 개선 합니다. 

#### <a name="configuring-rss"></a>RSS 구성

Windows Server 2016에서 Windows PowerShell cmdlet 및 RSS 프로필을 사용 하 여 RSS 구성할 수 있습니다. 

RSS 프로필을 사용 하 여 정의 수는 **– 프로필** 매개는 **설정 NetAdapterRss** Windows PowerShell cmdlet 합니다.

**RSS 구성에 대 한 Windows PowerShell 명령**

다음 cmdlet 확인 하 고 네트워크 어댑터 별로 RSS 매개 변수를 수정할 수 있습니다.
  
>[!NOTE]
>구문 및 매개 변수를 포함 하 여 각 cmdlet에 대 한 자세한 명령 참조용 다음 링크 클릭할 수 있습니다. 또한에 cmdlet 이름을 전달할 수 있습니다 **Get 도움말** 각 명령에 대 한 자세한 내용은 Windows PowerShell 프롬프트 합니다.  

- [사용 안 함 NetAdapterRss](https://technet.microsoft.com/library/jj130892)합니다. 이 명령을 사용자가 지정 된 네트워크 어댑터에서 RSS 사용 하지 않도록 합니다.

- [사용 NetAdapterRss](https://technet.microsoft.com/library/jj130859)합니다. 이 명령을 RSS를 사용자가 지정 된 네트워크 어댑터에 있습니다.
  
- [Get NetAdapterRss](https://technet.microsoft.com/library/jj130912)합니다. 이 명령을 사용자가 지정 된 네트워크 어댑터의 RSS 속성을 검색 합니다.
  
- [설정 NetAdapterRss](https://technet.microsoft.com/library/jj130863)합니다. 이 명령을 사용자가 지정 된 네트워크 어댑터에서 RSS 속성을 설정 합니다.  

#### <a name="rss-profiles"></a>RSS 프로필

사용할 수는 **– 프로필** 논리 프로세서 네트워크 어댑터에 할당 되어 지정 하려면 설정 NetAdapterRss cmdlet 매개 합니다. 사용 가능한 값이이 매개는 다음과 같습니다.

- **가장 가까운**합니다. 네트워크 어댑터의 기본 RSS 프로세서 가까이 논리 프로세서 번호는 것이 좋습니다. 이 프로필로 운영 체제 수 균형을 다시 조정 로드에 따라 동적으로 논리 프로세서 합니다.
  
- **ClosestStatic**합니다. 네트워크 어댑터의 기본 RSS 프로세서 근처 논리 프로세서 번호는 것이 좋습니다. 이 프로필로 운영 체제는 하지 균형을 다시 조정 로드에 따라 동적으로 논리 프로세서 합니다.
  
- **누 마**합니다. 일반적으로 논리 프로세서 번호를 부하 분산을 다른 누 마 노드에서 선택 합니다. 이 프로필로 운영 체제 수 균형을 다시 조정 로드에 따라 동적으로 논리 프로세서 합니다.
  
- **NUMAStatic**합니다. 이는 **기본 프로필**합니다. 일반적으로 논리 프로세서 번호를 부하 분산을 다른 누 마 노드에서 선택 합니다. 이 프로필로 운영 체제는 하지 균형을 다시 조정 로드에 따라 동적으로 논리 프로세서 합니다.

- **신중**합니다. RSS 로드 지원할 수 있도록 가능한 적은 프로세서를 사용 합니다. 이 옵션 인터럽트의 수를 줄일 수 있습니다.

시나리오 작업의 특징에 따라 다른 매개의을 사용할 수도 있는 **설정 NetAdapterRss** Windows PowerShell cmdlet 다음 지정 하려면:

- 각 네트워크 어댑터 별로 RSS에 대 한 논리 개수 프로세서를 사용할 수 있습니다.
- 시작 오프셋 논리 프로세서 범위입니다.
- 네트워크 어댑터 메모리를 할당 노드 합니다.

다음은 추가 **설정 NetAdapterRss** 매개 RSS 구성 하는 데 사용할 수 있는:

>[!NOTE]
>예제 구문 각 매개 네트워크 어댑터 이름 아래에 **이더넷** 예제 값을으로 사용 되는 **– 이름** 매개는 **설정 NetAdapterRss** 명령을 합니다. Cmdlet 실행할 때 사용 하는 네트워크 어댑터 이름을 귀하의 환경에 대 한 적절 한 있는지 확인 합니다.

- **\ * MaxProcessors**: 사용할 RSS 프로세서 최대 수를 설정 합니다. 이렇게 하면 특정된 인터페이스에서 응용 프로그램 교통 프로세서 최대 수를에 바인딩된입니다. 구문 예는 다음과 같습니다.

     `Set-NetAdapterRss –Name “Ethernet” –MaxProcessors <value>`

- **\ * BaseProcessorGroup**: 누 마 노드 기본 프로세서 그룹을 설정 합니다. RSS에서 사용 되는 프로세서 배열에 영향을 주는 합니다. 구문 예는 다음과 같습니다.

     `Set-NetAdapterRss –Name “Ethernet” –BaseProcessorGroup <value>`
  
- **\ * MaxProcessorGroup**: 누 마 노드 최대 프로세서 그룹을 설정 합니다. RSS에서 사용 되는 프로세서 배열에 영향을 주는 합니다. 이 설정 부하 분산 k 그룹 내 정렬 되도록 최대 프로세서 그룹을 제한 것입니다. 구문 예는 다음과 같습니다.

     `Set-NetAdapterRss –Name “Ethernet” –MaxProcessorGroup <value>`

- **\ * BaseProcessorNumber**: 누 마 노드 기본 프로세서 수를 설정 합니다. RSS에서 사용 되는 프로세서 배열에 영향을 주는 합니다. 이렇게 하면 네트워크 어댑터에 프로세서 분할 됩니다. 이 각 어댑터에 할당 된 RSS 범위 프로세서에서 첫 번째 논리 프로세서 합니다. 구문 예는 다음과 같습니다.

     `Set-NetAdapterRss –Name “Ethernet” –BaseProcessorNumber <Byte Value>`

- **\ * NumaNode**: The 누 마 노드 각 네트워크 어댑터에서 메모리 할당할 수 있습니다. 이 k 그룹 또는 다른 k 그룹 수 있습니다. 구문 예는 다음과 같습니다.

     `Set-NetAdapterRss –Name “Ethernet” –NumaNodeID <value>`

- **\ * NumberofReceiveQueues**: 논리 프로세서 트래픽 받기에 대 한 작업량이 것 \ (예: 작업 Manager\에 표시 된 대로)를 시도해 볼 수 있습니다 네트워크 어댑터에서 지원 되는 최대 2 기본에서 RSS 큐 수가 증가 합니다. 네트워크 어댑터 드라이버의 일환으로 RSS 큐 수 변경 하는 옵션 있을 수 있습니다. 구문 예는 다음과 같습니다.

     `Set-NetAdapterRss –Name “Ethernet” –NumberOfReceiveQueues <value>`

에 대 한 자세한 내용은 다음 다운로드 링크를 클릭 [확장 네트워킹: 처리 장애가 수신 하지 않아도-소개 RSS](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/NDIS_RSS.doc) Word 형식에서 있습니다.
  
#### <a name="understanding-rss-performance"></a>RSS 성능 이해

RSS 조정 구성과 부하 분산 논리를 파악 해야 합니다. RSS 설정을 사항이 적용을 실행 하는 경우 출력을 검토할 수를 확인 하 고 **Get NetAdapterRss** Windows PowerShell cmdlet 합니다. 다음은이 cmdlet의 출력 예입니다.
  
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

에코 설정 된 매개 변수를 뿐만 아니라 출력의 핵심 요소 간접 테이블 출력입니다. 간접 테이블 들어오는 교통 배포 하는 데 사용 하는 콘텐츠의 해시 표 보관 함 표시 됩니다. 여기에서 n:c 표기법 지정 누 마 K-들어오는 전송 하는 데 사용 하는 그룹: CPU 인덱스 페어링. 2 정확 하 게 고유한 항목이 표시 했습니다 (0: 0과 0:4)를는 k 그룹 0/cpu0 및 k 그룹 0/cpu 4 각각 나타냅니다.

이 시스템 (k 그룹 0) 및 n 하나만 k 그룹이 (여기서 n < 128 =) 간접 테이블 항목 합니다. 2만 2 프로세서로 설정 되어 받기 큐 수 있으므로 (0:0, 0:4)는 선택-최대 프로세서 8으로 설정 된 경우에 있습니다. 실제로, 간접 테이블만 사용할 수 있는 8 아웃 2 Cpu를 사용 하 여 수신 교통을 해시은 합니다.

Cpu을 최대한 활용 하려면 최대 프로세서 이상의 RSS 큐 받을 수 있어야 합니다. 이전 예제 8 이상 수신 큐 설정 해야 합니다.

#### <a name="nic-teaming-and-rss"></a>NIC 팀 및 RSS

RSS는 NIC 팀을 사용 하 여 다른 네트워크 인터페이스 카드와 협력 하는 네트워크 어댑터에 사용할 수 있습니다. 이 시나리오에서 RSS 사용 하 여 기본 실제 네트워크 어댑터를 구성할 수 있습니다. 사용자의 조합 된 네트워크 어댑터에 RSS cmdlet을 설정할 수 없습니다.
  
###  <a name="bkmk_rsc"></a>수신 세그먼트 결합 (RSC)

지정 된 시간 동안 받은 데이터 처리 IP 머리글의 줄여 세그먼트 결합 \(RSC\)는 성능을 받습니다. 성능을 높이기 받은 데이터 \(or coalescing\) 그룹화 하 여 더 작은 패킷을에 더 많은 장치를 사용 해야 합니다.

이 방법은 혜택 주로 처리량 향상에 표시 된 대기를 발생할 수 있습니다. RSC 받은 많은 작업을 위해 처리량 강화 하기 좋습니다. 네트워크 어댑터를 지 원하는 RSC 배포 하는 것이 좋습니다. 

이러한 네트워크 어댑터 RSC 켜져 있는지 확인 \ (기본 setting\은), 특정 작업 않은 \ (예: 대기 시간이 짧은, 낮은 처리량 networking\) RSC 해제 중에서 해당 표시 혜택 합니다.

#### <a name="understanding-rsc-diagnostics"></a>이해 RSC 진단

Windows PowerShell cmdlet 사용 하 여 RSC 진단할 수 **Get NetAdapterRsc** 및 **Get NetAdapterStatistics**합니다.

다음은 Get NetAdapterRsc cmdlet 실행 될 때 출력 예입니다.

```  

PS C:\Users\Administrator> Get-NetAdapterRsc  
  
Name                       IPv4Enabled  IPv6Enabled  IPv4Operational IPv6Operational               IPv4FailureReason              IPv6Failure  
                                            Reason  
----                           -----------  -----------  --------------- --------------- ----------------- ------------  
Ethernet                       True         False        True            False                  NoFailure       NicProperties  
  
```  

**다운로드** cmdlet RSC 인터페이스에서 활성화 되어 있는지 여부와 TCP RSC 작동 상태에 사용할 수 있는지 여부를 보여 줍니다. 오류 원인을 RSC 해당 인터페이스에서 사용 하는 오류에 대 한 세부 정보를 제공 합니다.

이전 시나리오에서 IPv4 RSC 인터페이스에서 지원 되 고 작동는 합니다. 진단 오류를 이해 하기 하나 결합 된 바이트 또는 발생 예외를 확인할 수 있습니다. 결합 하는 문제를 나타내는 표시를 제공합니다.

다음은 Get NetAdapterStatistics cmdlet 실행 될 때 출력 예입니다.

```  
PS C:\Users\Administrator> $x = Get-NetAdapterStatistics “myAdapter”   
PS C:\Users\Administrator> $x.rscstatistics  
  
CoalescedBytes       : 0  
CoalescedPackets     : 0  
CoalescingEvents     : 0  
CoalescingExceptions : 0  
  
```  

#### <a name="rsc-and-virtualization"></a>RSC 및 가상화

RSC는 호스트 네트워크 어댑터 Hyper-v의 가상 스위치를 바인딩된 하지 않을 경우에 물리적 호스트만 지원 됩니다. 호스트 Hyper-v의 가상 스위치에 바인딩된 때 RSC는 운영 체제에 사용할 수 없습니다. 또한, 가상 컴퓨터 위해서 RSC 혜택 가상 네트워크 어댑터 RSC를 지원 하지 않으므로 합니다.

단일 루트 입력/출력 Virtualization \(SR-IOV\) 사용 하도록 설정 하면 RSC 가상 컴퓨터에 사용할 수 있습니다. 이 경우 가상 기능 지원 RSC 기능이 있습니다. 따라서 가상 컴퓨터의 RSC 혜택도 받습니다.

##  <a name="bkmk_resources"></a>네트워크 어댑터 리소스

네트워크 어댑터는 몇 가지 성능을 최적화 하려면 자녀의 리소스를 적극적으로 관리 합니다. 몇 가지 네트워크 어댑터를 사용 하면 수동으로 리소스를 사용 하 여 구성 하 고 **네트워킹 고급** 어댑터에 대 한 탭 합니다. 이러한 어댑터에 대 한 매개 변수를 수신 버퍼가 번호를 포함 하 여 숫자 값을 설정할 수 있으며 버퍼가 보낼 수 있습니다.

다음 Windows PowerShell cmdlet 사용 하 여 네트워크 어댑터 리소스 구성 간단해 집니다.

- [Get NetAdapterAdvancedProperty](https://technet.microsoft.com/library/jj130901.aspx)

- [설정 NetAdapterAdvancedProperty](https://technet.microsoft.com/library/jj130894.aspx)

- [NetAdapter 사용](https://technet.microsoft.com/library/jj130876.aspx)

- [NetAdapterBinding 사용](https://technet.microsoft.com/library/jj130913.aspx)

- [NetAdapterChecksumOffload 사용](https://technet.microsoft.com/library/jj130918.aspx)

- [NetAdapterIPSecOffload 사용](https://technet.microsoft.com/library/jj130890.aspx)

- [NetAdapterLso 사용](https://technet.microsoft.com/library/jj130922.aspx)

- [NetAdapterPowerManagement 사용](https://technet.microsoft.com/library/jj130907.aspx)

- [NetAdapterQos 사용](https://technet.microsoft.com/library/jj130866.aspx)

- [NetAdapterRDMA 사용](https://technet.microsoft.com/library/jj130909.aspx)

- [NetAdapterSriov 사용](https://technet.microsoft.com/library/jj130899.aspx)

자세한 내용은 참조 [Windows powershell에서 네트워크 어댑터 Cmdlet](https://technet.microsoft.com/library/jj134956.aspx)합니다.

이 가이드의 모든 항목에 대 한 링크를 참조 하세요. [네트워크 하위 시스템 성능 조정](net-sub-performance-top.md)합니다.