---
title: 네트워크 어댑터 성능 조정
description: 이 항목은 Windows Server 2016에 대 한 네트워크 하위 시스템 성능 조정 가이드의 일부입니다.
audience: Admin - CI ID 111485 - CSSTroubleshoot
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0b9b0f80-415c-4f5e-8377-c09b51d9c5dd
manager: dcscontentpm
ms.author: v-tea
author: Teresa-Motiv
ms.date: 12/23/2019
ms.openlocfilehash: dec88eb81227b62cd0a0ca90810b2598b8f9fd52
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854746"
---
# <a name="performance-tuning-network-adapters"></a>네트워크 어댑터 성능 조정

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server(반기 채널)

이 항목의 정보를 사용 하 여 Windows Server 2016 이상 버전을 실행 하는 컴퓨터에 대 한 성능 네트워크 어댑터를 튜닝할 수 있습니다. 네트워크 어댑터에서 튜닝 옵션을 제공 하는 경우 이러한 옵션을 사용 하 여 네트워크 처리량 및 리소스 사용량을 최적화할 수 있습니다.

네트워크 어댑터에 대 한 올바른 튜닝 설정은 다음 변수에 따라 달라 집니다.

- 네트워크 어댑터와 해당 기능 집합  
- 서버에서 수행 하는 작업의 유형입니다.  
- 서버 하드웨어 및 소프트웨어 리소스  
- 서버에 대한 성능 목표  

다음 섹션에서는 성능 조정 옵션 중 일부에 대해 설명합니다.  

##  <a name="enabling-offload-features"></a><a name="bkmk_offload"></a>오프 로드 기능 사용

일반적으로 네트워크 어댑터 오프로드 기능을 설정하는 것이 좋습니다. 그러나 네트워크 어댑터는 처리량이 높은 오프 로드 기능을 처리할 만큼 강력 하지 않을 수 있습니다.

> [!IMPORTANT]
> 오프 로드 기능 **IPsec 작업 오프 로드** 또는 **TCP Chimney 오프 로드**를 사용 하지 마세요. 이러한 기술은 Windows Server 2016에서 더 이상 사용 되지 않으며 서버 및 네트워킹 성능에 부정적인 영향을 줄 수 있습니다. 또한 이러한 기술은 향후 Microsoft에서 지원 되지 않을 수 있습니다.

예를 들어 하드웨어 리소스가 제한 된 네트워크 어댑터가 있다고 가정 합니다.
이 경우 분할 오프 로드 기능을 사용 하도록 설정 하면 어댑터의 유지 가능한 최대 처리량을 줄일 수 있습니다. 그러나 축소 된 처리량이 허용 되는 경우에는 분할 오프 로드 기능을 사용 하도록 설정 해야 합니다.

> [!NOTE]  
> 일부 네트워크 어댑터에서는 송신 및 수신 경로에 대해 독립적으로 오프 로드 기능을 사용 하도록 설정 해야 합니다.

##  <a name="enabling-receive-side-scaling-rss-for-web-servers"></a><a name="bkmk_rss_web"></a>웹 서버에 대 한 RSS (수신측 배율) 사용

네트워크 어댑터 수가 서버의 논리 프로세서보다 적은 경우 RSS를 통해 웹 확장성과 성능을 개선할 수 있습니다. 모든 웹 트래픽이 RSS 가능 네트워크 어댑터를 통과 하는 경우 서버는 여러 다른 연결에서 들어오는 웹 요청을 여러 Cpu에서 동시에 처리할 수 있습니다.

> [!IMPORTANT]  
> 동일한 서버에서 RSS를 사용 하지 않는 네트워크 어댑터와 RSS 가능 네트워크 어댑터를 모두 사용 하지 않도록 합니다. Rss 및 하이퍼텍스트 전송 프로토콜 (HTTP)의 부하 분산 논리 때문에 rss 지원 네트워크 어댑터가 하나 이상의 RSS 지원 네트워크 어댑터를 포함 하는 서버에서 웹 트래픽을 허용 하는 경우 성능이 심각 하 게 저하 될 수 있습니다. 이 경우 RSS 지원 네트워크 어댑터를 사용하거나 네트워크 어댑터 속성의 **고급 속성** 탭에서 RSS를 사용하지 않도록 설정해야 합니다.
>  
> 네트워크 어댑터가 RSS를 지원하는지 여부를 확인하려면 네트워크 어댑터 속성의 **고급 속성** 탭에서 RSS 정보를 확인하면 됩니다.

### <a name="rss-profiles-and-rss-queues"></a>RSS 프로필 및 RSS 큐

미리 정의 된 기본 RSS 프로필은 **Numastatic**이며, 이전 버전의 Windows에서 사용 하는 기본값과 다릅니다. RSS 프로필 사용을 시작 하기 전에 사용 가능한 프로필을 검토 하 여 유용한 방법과 네트워크 환경 및 하드웨어에 적용 되는 방법을 파악 하십시오.

예를 들어 작업 관리자를 열고 서버에서 논리적 프로세서를 검토 하는 경우 수신 트래픽이 미달 사용 되는 것 처럼 보이는 경우, RSS 큐의 수를 네트워크 어댑터에서 지 원하는 최대 크기의 기본값인 2에서 늘릴 수 있습니다. 네트워크 어댑터에서 드라이버의 일부로 RSS 큐 수를 변경하는 옵션을 제공할 수 있습니다.

##  <a name="increasing-network-adapter-resources"></a><a name="bkmk_resources"></a>네트워크 어댑터 리소스를 늘립니다.

수신 및 송신 버퍼와 같은 리소스를 수동으로 구성할 수 있도록 하는 네트워크 어댑터의 경우 할당 된 리소스를 늘려야 합니다.  

일부 네트워크 어댑터는 호스트에서 할당되는 메모리를 절약하기 위해 수신 버퍼를 낮게 설정합니다. 이러한 값이 낮으면 패킷이 손실되고 성능이 저하될 수 있습니다. 따라서 수신 작업이 많은 시나리오에서는 수신 버퍼 값을 최대값으로 늘리는 것이 좋습니다.

> [!NOTE]  
> 네트워크 어댑터가 수동 리소스 구성을 노출 하지 않는 경우 리소스를 동적으로 구성 하거나 변경할 수 없는 고정 된 값으로 리소스를 설정 합니다.

### <a name="enabling-interrupt-moderation"></a>인터럽트 중재 사용

인터럽트 조정을 제어 하기 위해 일부 네트워크 어댑터는 서로 다른 인터럽트 중재 수준, 다른 버퍼 결합 매개 변수 (경우에 따라 송신 및 수신 버퍼의 경우 별도로) 또는 둘 다를 노출 합니다.

CPU 바인딩된 작업에 대 한 인터럽트 중재를 고려해 야 합니다. 인터럽트 조정을 사용 하는 경우에는 더 많은 인터럽트가 발생 하 고 대기 시간이 줄어들기 때문에 호스트 CPU 절약 시간과 대기 시간 간의 균형을 높이고 호스트 CPU의 절감 액을 높일 것을 고려 하십시오. 네트워크 어댑터가 인터럽트 조정을 수행 하지 않지만 버퍼 병합을 노출 하는 경우 송신 또는 수신 당 더 많은 버퍼를 허용 하도록 병합 된 버퍼의 수를 늘려서 성능을 향상 시킬 수 있습니다.

##  <a name="performance-tuning-for-low-latency-packet-processing"></a><a name="bkmk_low"></a>낮은 대기 시간 패킷 처리를 위한 성능 조정

대부분의 네트워크 어댑터는 운영 체제에서 발생하는 대기 시간을 최적화할 수 있는 옵션을 제공합니다. 대기 시간은 네트워크 드라이버에서 들어오는 패킷을 처리하여 다시 보낼 때까지 소요되는 시간입니다. 이 시간은 일반적으로 마이크로초 단위로 측정됩니다. 비교하자면, 멀리 떨어진 곳으로의 패킷 전송에 사용되는 전송 시간은 일반적으로 몇 배 더 큰 밀리초 단위로 측정됩니다. 이러한 조정은 전송 중에 패킷에서 소요되는 시간을 단축하지 않습니다.

다음은 마이크로초가 중요한 네트워크에 대한 몇 가지 성능 조정 제안 사항입니다.

- 컴퓨터 BIOS를 **고성능**으로 설정하고, C-state는 사용하지 않도록 설정합니다. 그러나 이는 시스템 및 BIOS에 종속되므로 일부 시스템은 운영 체제에서 전원 관리를 제어하는 경우 더 높은 성능을 제공합니다. **설정** 에서 또는 **powercfg** 명령을 사용 하 여 전원 관리 설정을 확인 하 고 조정할 수 있습니다. 자세한 내용은 [Powercfg 명령줄 옵션](https://docs.microsoft.com/windows-hardware/design/device-experiences/powercfg-command-line-options)을 참조 하세요.

- 운영 체제 전원 관리 프로필 설정을 **고성능 시스템**으로 설정합니다.  
   > [!NOTE]  
   > 전원 관리에 대 한 운영 체제 제어를 사용 하지 않도록 시스템 BIOS를 설정한 경우에는이 설정이 제대로 작동 하지 않습니다.

- 정적 오프 로드를 사용 합니다. 예를 들어 UDP 체크섬, TCP 체크섬 및 LSO (Large Offload) 설정을 사용 하도록 설정 합니다.

- 대량 멀티 캐스트 트래픽을 받는 경우와 같이 트래픽이 다중 스트리밍되는 경우 RSS를 사용 하도록 설정 합니다.

- 가능한 가장 짧은 대기 시간이 필요한 네트워크 카드 드라이버에는 **인터럽트 조절** 설정을 사용하지 않습니다. 이 구성은 더 많은 CPU 시간을 사용 하 고 균형을 나타낼 수 있습니다.

- 패킷을 처리하는 프로그램(사용자 스레드)에서 사용 중인 코어와 CPU 캐시를 공유하는 코어 프로세서에서 네트워크 어댑터 인터럽트 및 DPC를 처리합니다. CPU 선호도 조정을 사용하여 RSS 구성과 함께 프로세스를 특정 논리 프로세서로 전달하여 이를 실현할 수 있습니다. 인터럽트, DPC 및 사용자 모드 스레드에 동일한 코어를 사용하면 ISR, DPC 및 스레드가 코어 사용을 경합하기 때문에 로드가 증가하여 성능이 저하됩니다.

##  <a name="system-management-interrupts"></a><a name="bkmk_smi"></a>시스템 관리 인터럽트

많은 하드웨어 시스템은 ECC (오류 수정 코드) 메모리 오류 보고, 레거시 USB 호환성 유지, 팬 제어, BIOS 제어 기능 관리 등의 다양 한 유지 관리 기능을 위해 SMI-S (시스템 관리 인터럽트)를 사용 합니다. 설정.

SMI-S는 시스템에서 우선 순위가 가장 높은 인터럽트 이며 CPU를 관리 모드로 설정 합니다. 이 모드는 다른 모든 활동을 보다 우선, SMI-S는 보통 BIOS에 포함 된 인터럽트 서비스 루틴을 실행 합니다.

불행 하 게이 동작은 100 마이크로초 이상의 대기 시간 급증을 초래할 수 있습니다.

가장 짧은 대기 시간이 필요한 경우 하드웨어 공급자에게 SMI를 가능한 한 최저 수준으로 낮추는 BIOS 버전을 요청해야 합니다. 이러한 BIOS 버전은 종종 "낮은 대기 시간 BIOS" 또는 "SMI-S 무료 BIOS" 라고도 합니다. SMI 작업이 필수 기능(예: 냉각 팬)을 제어하는 데 사용되어 하드웨어 플랫폼에서 SMI 작업을 완전히 제거하는 것이 불가능한 경우도 있습니다.

> [!NOTE]  
> 논리 프로세서가 특수 한 유지 관리 모드에서 실행 되 고 있으므로 운영 체제에서 SMIs를 제어할 수 없습니다 .이로 인해 운영 체제에서 작업을 수행할 수 없습니다.

##  <a name="performance-tuning-tcp"></a><a name="bkmk_tcp"></a>성능 조정 TCP

 다음 항목을 사용 하 여 TCP 성능을 튜닝할 수 있습니다.

###  <a name="tcp-receive-window-autotuning"></a><a name="bkmk_tcp_params"></a>TCP 수신 창 autotuning

Windows Vista, Windows Server 2008 및 이후 버전의 windows에서 Windows 네트워크 스택은 tcp receive *window autotuning level* 이라는 기능을 사용 하 여 tcp 수신 창 크기를 협상 합니다. 이 기능은 TCP 핸드셰이크 중에 모든 TCP 통신에 대해 정의 된 수신 창 크기를 협상할 수 있습니다.

이전 버전의 Windows에서 Windows 네트워크 스택은 연결에 대 한 전체 잠재적 처리량을 제한 하는 고정 크기 수신 창 (65535 바이트)을 사용 했습니다. TCP 연결의 달성 가능한 총 처리량은 네트워크 사용 시나리오를 제한할 수 있습니다. TCP 수신 창 autotuning를 사용 하면 이러한 시나리오에서 네트워크를 완전히 사용할 수 있습니다.

특정 크기가 있는 TCP 수신 창의 경우 다음 수식을 사용 하 여 단일 연결의 총 처리량을 계산할 수 있습니다.

> *처리 가능한 총 처리량 (바이트* ) = *TCP 수신 창 크기 (바이트* ) \* (1/ *연결 대기 시간 (초*))

예를 들어 대기 시간이 10 밀리초 인 연결의 경우 달성 가능한 총 처리량은 51 Mbps입니다. 이 값은 대기업 네트워크 인프라에 적합 합니다. 그러나 autotuning을 사용 하 여 수신 기간을 조정 하면 연결이 1Gbps 연결의 전체 줄 속도로 전송 될 수 있습니다.  

일부 응용 프로그램은 TCP 수신 창의 크기를 정의 합니다. 응용 프로그램에서 수신 창 크기를 정의 하지 않으면 링크 속도에서 다음과 같이 크기를 결정 합니다.

- 초당 1Mbps (초당 메가 비트): 8kb
- 1mbps ~ 100 Mbps: 17kb
- 100 Mbps ~ 초당 기가 비트 (Gbps): 64 KB
- 10gbps 이상: 128 KB

예를 들어 1Gbps 네트워크 어댑터가 설치 된 컴퓨터에서 창 크기는 64 KB 여야 합니다.

또한이 기능을 사용 하면 다른 기능을 모두 사용 하 여 네트워크 성능을 향상 시킬 수 있습니다. 이러한 기능에는 [RFC 1323](https://tools.ietf.org/html/rfc1323)에 정의 된 나머지 TCP 옵션이 포함 됩니다. Windows 기반 컴퓨터는 이러한 기능을 사용 하 여 더 작은 TCP 수신 창 크기를 협상할 수 있지만 구성에 따라 정의 된 값으로 크기가 조정 됩니다. 이 동작을 통해 네트워킹 장치를 보다 쉽게 처리할 수 있습니다.

> [!NOTE]  
> [RFC 1323](https://tools.ietf.org/html/rfc1323) 에 정의 된 대로 네트워크 장치가 **TCP 창 크기 조정 옵션과**호환 되지 않는 문제가 발생할 수 있으므로는 배율 인수를 지원 하지 않습니다. 이러한 경우에 [는이 KB 934430을 참조 하세요. 방화벽 장치에서 Windows Vista를 사용 하려고 할 때 네트워크 연결이 실패 하거나,](https://support.microsoft.com/help/934430/network-connectivity-fails-when-you-try-to-use-windows-vista-behind-a) 네트워크 장치 공급 업체에 대 한 지원 팀에 문의 하세요.  

#### <a name="review-and-configure-tcp-receive-window-autotuning-level"></a>TCP 수신 윈도 autotuning 수준 검토 및 구성

Netsh 명령 또는 Windows PowerShell cmdlet을 사용 하 여 TCP 수신 윈도 autotuning 수준을 검토 하거나 수정할 수 있습니다.

> [!NOTE]  
> 이전에 Windows 10 또는 Windows Server 2019를 사용 하는 Windows 버전과 달리, 더 이상 레지스트리를 사용 하 여 TCP 수신 창 크기를 구성할 수 없습니다. 사용 되지 않는 설정에 대 한 자세한 내용은 [사용 되지 않는 TCP 매개 변수](#deprecated-tcp-parameters)를 참조 하세요.

> [!NOTE]  
> 사용 가능한 autotuning 수준에 대 한 자세한 내용은 [autotuning 수준](#autotuning-levels)을 참조 하세요.

**Netsh를 사용 하 여 autotuning 수준을 검토 하거나 수정 하려면**

현재 설정을 검토 하려면 명령 프롬프트 창을 열고 다음 명령을 실행 합니다.

```cmd
netsh interface tcp show global
```

이 명령의 출력은 다음과 유사 합니다.

```
Querying active state...

TCP Global Parameters  
-----
Receive-Side Scaling State : enabled
Chimney Offload State : disabled
Receive Window Auto-Tuning Level : normal
Add-On Congestion Control Provider : default
ECN Capability : disabled
RFC 1323 Timestamps : disabled
Initial RTO : 3000
Receive Segment Coalescing State : enabled
Non Sack Rtt Resiliency : disabled
Max SYN Retransmissions : 2
Fast Open : enabled
Fast Open Fallback : enabled
Pacing Profile : off
```

설정을 수정 하려면 명령 프롬프트에서 다음 명령을 실행 합니다.

```cmd
netsh interface tcp set global autotuninglevel=<Value>
```

> [!NOTE]  
> 이전 명령에서 \<*값*> 자동 튜닝 수준의 새 값을 나타냅니다.

이 명령에 대 한 자세한 내용은 [Interface 전송 제어 프로토콜에 대 한 Netsh 명령](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731258(v=ws.10))을 참조 하세요.

**Powershell을 사용 하 여 autotuning 수준을 검토 하거나 수정 하려면**

현재 설정을 검토 하려면 PowerShell 창을 열고 다음 cmdlet을 실행 합니다.

```PowerShell
Get-NetTCPSetting | Select SettingName,AutoTuningLevelLocal
```

이 cmdlet의 출력은 다음과 유사 합니다.

```
SettingName           AutoTuningLevelLocal
-----------          --------------------
Automatic
InternetCustom       Normal
DatacenterCustom     Normal
Compat               Normal
Datacenter           Normal
Internet             Normal
```

설정을 수정 하려면 PowerShell 명령 프롬프트에서 다음 cmdlet을 실행 합니다.

```PowerShell
Set-NetTCPSetting -AutoTuningLevelLocal <Value>
```

> [!NOTE]  
> 이전 명령에서 \<*값*> 자동 튜닝 수준의 새 값을 나타냅니다.

이러한 cmdlet에 대 한 자세한 내용은 다음 문서를 참조 하세요.

- [NetTCPSetting](https://docs.microsoft.com/powershell/module/nettcpip/get-nettcpsetting?view=win10-ps)
- [NetTCPSetting](https://docs.microsoft.com/powershell/module/nettcpip/set-nettcpsetting?view=win10-ps)

#### <a name="autotuning-levels"></a>Autotuning 수준

수신 창 autotuning을 5 가지 수준 중 하나로 설정할 수 있습니다. 기본 수준은 **Normal**입니다. 다음 표에서는 수준에 대해 설명 합니다.

|Level |16 진수 값 |설명 |
| --- | --- | --- |
|보통(기본 설정) |0x8 (8의 배율 인수) |거의 모든 시나리오를 수용할 수 있도록 TCP 수신 기간을 확장 하도록 설정 합니다. |
|사용 안 함 |사용 가능한 배율 인수 없음 |TCP 수신 기간을 기본값으로 설정 합니다. |
|Restricted (제한됨) |0x4 (4의 배율 인수) |TCP 수신 창이 기본값 이상으로 증가 하도록 설정 하지만 일부 시나리오에서는 이러한 증가가 제한 됩니다. |
|매우 제한 |0x2 (배율 인수 2) |TCP 수신 창이 기본값 이상으로 증가 하도록 설정 하지만 매우 신중 하 게 수행 해야 합니다. |
|시험용 |0xE (배율 인수 14) |극단적인 시나리오를 수용할 수 있도록 TCP 수신 윈도를 증가 하도록 설정 합니다. |

응용 프로그램을 사용 하 여 네트워크 패킷을 캡처하는 경우 응용 프로그램은 다른 window autotuning 수준 설정에 대해 다음과 유사한 데이터를 보고 해야 합니다.

- Autotuning level: **Normal (기본 상태)**

   ```
   Frame: Number = 492, Captured Frame Length = 66, MediaType = ETHERNET
   + Ethernet: Etype = Internet IP (IPv4),DestinationAddress:[D8-FE-E3-65-F3-FD],SourceAddress:[C8-5B-76-7D-FA-7F]
   + Ipv4: Src = 192.169.0.5, Dest = 192.169.0.4, Next Protocol = TCP, Packet ID = 2667, Total IP Length = 52
   - Tcp: [Bad CheckSum]Flags=......S., SrcPort=60975, DstPort=Microsoft-DS(445), PayloadLen=0, Seq=4075590425, Ack=0, Win=64240 ( Negotiating scale factor 0x8 ) = 64240
   SrcPort: 60975
   DstPort: Microsoft-DS(445)
   SequenceNumber: 4075590425 (0xF2EC9319)
   AcknowledgementNumber: 0 (0x0)
   + DataOffset: 128 (0x80)
   + Flags: ......S. ---------------------------------------------------------> SYN Flag set
   Window: 64240 ( Negotiating scale factor 0x8 ) = 64240 ---------> TCP Receive Window set as 64K as per NIC Link bitrate. Note it shows the 0x8 Scale Factor.
   Checksum: 0x8182, Bad
   UrgentPointer: 0 (0x0)
   - TCPOptions:
   + MaxSegmentSize: 1
   + NoOption:
   + WindowsScaleFactor: ShiftCount: 8 -----------------------------> Scale factor, defined by AutoTuningLevel
   + NoOption:
   + NoOption:
   + SACKPermitted:
   ```

- Autotuning 수준: **사용 안 함**

   ```
   Frame: Number = 353, Captured Frame Length = 62, MediaType = ETHERNET
   + Ethernet: Etype = Internet IP (IPv4),DestinationAddress:[D8-FE-E3-65-F3-FD],SourceAddress:[C8-5B-76-7D-FA-7F]
   + Ipv4: Src = 192.169.0.5, Dest = 192.169.0.4, Next Protocol = TCP, Packet ID = 2576, Total IP Length = 48
   - Tcp: [Bad CheckSum]Flags=......S., SrcPort=60956, DstPort=Microsoft-DS(445), PayloadLen=0, Seq=2315885330, Ack=0, Win=64240 ( ) = 64240
   SrcPort: 60956
   DstPort: Microsoft-DS(445)
   SequenceNumber: 2315885330 (0x8A099B12)
   AcknowledgementNumber: 0 (0x0)
   + DataOffset: 112 (0x70)
   + Flags: ......S. ---------------------------------------------------------> SYN Flag set
   Window: 64240 ( ) = 64240 ----------------------------------------> TCP Receive Window set as 64K as per NIC Link bitrate. Note there is no Scale Factor defined. In this case, Scale factor is not being sent as a TCP Option, so it will not be used by Windows.
   Checksum: 0x817E, Bad
   UrgentPointer: 0 (0x0)
   - TCPOptions:
   + MaxSegmentSize: 1
   + NoOption:
   + NoOption:
   + SACKPermitted:
   ```

- Autotuning level: **제한** 됨

   ```
   Frame: Number = 3, Captured Frame Length = 66, MediaType = ETHERNET
   + Ethernet: Etype = Internet IP (IPv4),DestinationAddress:[D8-FE-E3-65-F3-FD],SourceAddress:[C8-5B-76-7D-FA-7F]
   + Ipv4: Src = 192.169.0.5, Dest = 192.169.0.4, Next Protocol = TCP, Packet ID = 2319, Total IP Length = 52
   - Tcp: [Bad CheckSum]Flags=......S., SrcPort=60890, DstPort=Microsoft-DS(445), PayloadLen=0, Seq=1966088568, Ack=0, Win=64240 ( Negotiating scale factor 0x4 ) = 64240
   SrcPort: 60890
   DstPort: Microsoft-DS(445)
   SequenceNumber: 1966088568 (0x75302178)
   AcknowledgementNumber: 0 (0x0)
   + DataOffset: 128 (0x80)
   + Flags: ......S. ---------------------------------------------------------> SYN Flag set
   Window: 64240 ( Negotiating scale factor 0x4 ) = 64240 ---------> TCP Receive Window set as 64K as per NIC Link bitrate. Note it shows the 0x4 Scale Factor.
   Checksum: 0x8182, Bad
   UrgentPointer: 0 (0x0)
   - TCPOptions:
   + MaxSegmentSize: 1
   + NoOption:
   + WindowsScaleFactor: ShiftCount: 4 -------------------------------> Scale factor, defined by AutoTuningLevel.
   + NoOption:
   + NoOption:
   + SACKPermitted:
   ```

- Autotuning level: **항상 제한** 됨

   ```
   Frame: Number = 115, Captured Frame Length = 66, MediaType = ETHERNET
   + Ethernet: Etype = Internet IP (IPv4),DestinationAddress:[D8-FE-E3-65-F3-FD],SourceAddress:[C8-5B-76-7D-FA-7F]
   + Ipv4: Src = 192.169.0.5, Dest = 192.169.0.4, Next Protocol = TCP, Packet ID = 2388, Total IP Length = 52
   - Tcp: [Bad CheckSum]Flags=......S., SrcPort=60903, DstPort=Microsoft-DS(445), PayloadLen=0, Seq=1463725706, Ack=0, Win=64240 ( Negotiating scale factor 0x2 ) = 64240
   SrcPort: 60903
   DstPort: Microsoft-DS(445)
   SequenceNumber: 1463725706 (0x573EAE8A)
   AcknowledgementNumber: 0 (0x0)
   + DataOffset: 128 (0x80)
   + Flags: ......S. ---------------------------------------------------------> SYN Flag set
   Window: 64240 ( Negotiating scale factor 0x2 ) = 64240 ---------> TCP Receive Window set as 64K as per NIC Link bitrate. Note it shows the 0x2 Scale Factor.
   Checksum: 0x8182, Bad
   UrgentPointer: 0 (0x0)
   - TCPOptions:
   + MaxSegmentSize: 1
   + NoOption:
   + WindowsScaleFactor: ShiftCount: 2 ------------------------------> Scale factor, defined by AutoTuningLevel
   + NoOption:
   + NoOption:
   + SACKPermitted:
   ```

- Autotuning 수준: **실험적**

   ```
   Frame: Number = 238, Captured Frame Length = 66, MediaType = ETHERNET
   + Ethernet: Etype = Internet IP (IPv4),DestinationAddress:[D8-FE-E3-65-F3-FD],SourceAddress:[C8-5B-76-7D-FA-7F]
   + Ipv4: Src = 192.169.0.5, Dest = 192.169.0.4, Next Protocol = TCP, Packet ID = 2490, Total IP Length = 52
   - Tcp: [Bad CheckSum]Flags=......S., SrcPort=60933, DstPort=Microsoft-DS(445), PayloadLen=0, Seq=2095111365, Ack=0, Win=64240 ( Negotiating scale factor 0xe ) = 64240
   SrcPort: 60933
   DstPort: Microsoft-DS(445)
   SequenceNumber: 2095111365 (0x7CE0DCC5)
   AcknowledgementNumber: 0 (0x0)
   + DataOffset: 128 (0x80)
   + Flags: ......S. ---------------------------------------------------------> SYN Flag set
   Window: 64240 ( Negotiating scale factor 0xe ) = 64240 ---------> TCP Receive Window set as 64K as per NIC Link bitrate. Note it shows the 0xe Scale Factor.
   Checksum: 0x8182, Bad
   UrgentPointer: 0 (0x0)
   - TCPOptions:
   + MaxSegmentSize: 1
   + NoOption:
   + WindowsScaleFactor: ShiftCount: 14 -----------------------------> Scale factor, defined by AutoTuningLevel
   + NoOption:
   + NoOption:
   + SACKPermitted:
   ```

#### <a name="deprecated-tcp-parameters"></a>사용 되지 않는 TCP 매개 변수

Windows Server 2003의 다음 레지스트리 설정은 더 이상 지원 되지 않으며 이후 버전에서 무시 됩니다.

- **TcpWindowSize**
- **NumTcbTablePartitions**  
- **MaxHashTableSize**  

이러한 설정은 모두 다음 레지스트리 하위 키에 있습니다.

> **HKEY_LOCAL_MACHINE \System\CurrentControlSet\Services\Tcpip\Parameters**  

###  <a name="windows-filtering-platform"></a><a name="bkmk_wfp"></a>Windows 필터링 플랫폼

Windows Vista 및 Windows Server 2008에는 WFP (Windows 필터링 플랫폼)가 도입 되었습니다. WFP는 타사 Isv (독립 소프트웨어 공급 업체)에 게 패킷 처리 필터를 만들 수 있는 Api를 제공 합니다. 예를 들어 방화벽 및 바이러스 백신 소프트웨어가 여기에 해당합니다.

> [!NOTE]  
> 제대로 작성 되지 않은 WFP 필터는 서버의 네트워킹 성능을 크게 낮출 수 있습니다. 자세한 내용은 Windows 개발자 센터에서 [패킷 처리 드라이버 및 응용 프로그램을 WFP로 포팅](https://docs.microsoft.com/windows-hardware/drivers/network/porting-packet-processing-drivers-and-apps-to-wfp) 을 참조 하세요.

이 가이드의 모든 항목에 대 한 링크는 [네트워크 하위 시스템 성능 튜닝](net-sub-performance-top.md)을 참조 하세요.
