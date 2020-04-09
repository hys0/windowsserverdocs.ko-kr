---
title: SMB (서버 메시지 블록) 고급 문제 해결
description: 에서는 고급 SMB (서버 메시지 블록) 문제 해결 방법을 소개 합니다.
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 654cb1b0eea65457d521d201739721ed8c3c0203
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815196"
---
# <a name="advanced-troubleshooting-server-message-block-smb"></a>SMB (서버 메시지 블록) 고급 문제 해결

SMB (서버 메시지 블록)는 클라이언트가 서버의 리소스에 액세스할 수 있도록 하는 파일 시스템 작업에 대 한 네트워크 전송 프로토콜입니다. SMB 프로토콜의 주요 목적은 TCP/IP를 통해 두 시스템 간에 원격 파일 시스템 액세스를 사용 하도록 설정 하는 것입니다.

SMB 문제 해결은 매우 복잡할 수 있습니다. 이 문서는 철저 한 문제 해결 가이드는 아니지만 SMB 문제를 효과적으로 해결 하는 방법에 대 한 기본 사항을 이해 하는 것은 간단한 입문입니다.

## <a name="tools-and-data-collection"></a>도구 및 데이터 수집

품질 SMB 문제 해결의 한 가지 주요 측면은 올바른 용어를 전달 하는 것입니다. 따라서이 문서에서는 데이터 수집 및 분석 정확성을 보장 하기 위한 기본 SMB 용어를 소개 합니다.

> [!Note]
> *SMB 서버 (SRV)* 는 파일 서버 라고도 하는 파일 시스템을 호스트 하는 시스템을 말합니다. *SMB 클라이언트 (CLI)는* OS 버전 또는 버전에 관계 없이 파일 시스템에 액세스 하려고 하는 시스템을 나타냅니다.

예를 들어 windows Server 2016를 사용 하 여 Windows 10에서 호스트 되는 SMB 공유에 연결 하는 경우 Windows Server 2016은 smb 클라이언트 및 Windows 10 SMB 서버입니다.

### <a name="collect-data"></a>데이터 수집

SMB 문제를 해결 하기 전에 먼저 클라이언트와 서버 쪽 모두에서 네트워크 추적을 수집 하는 것이 좋습니다. 다음과 같은 지침이 적용됩니다.

- Windows 시스템에서 netshell (netsh), 네트워크 모니터, Message 분석기 또는 Wireshark를 사용 하 여 네트워크 추적을 수집할 수 있습니다.

- 타사 장치에는 일반적으로 tcpdump (Linux/FreeBSD/Unix) 또는 pktt (NetApp)와 같은 기본 패킷 캡처 도구가 있습니다. 예를 들어 SMB 클라이언트 또는 SMB 서버가 Unix 호스트인 경우 다음 명령을 실행 하 여 데이터를 수집할 수 있습니다.
  
  ```cmd
  # tcpdump -s0 -n -i any -w /tmp/$(hostname)-smbtrace.pcap
  ```
  
  키보드에서 **Ctrl + C** 를 사용 하 여 데이터 수집을 중지 합니다.

문제의 원인을 검색 하기 위해 두 개의 측면 추적 (CLI, SRV 또는 between between)을 확인할 수 있습니다.

#### <a name="using-netshell-to-collect-data"></a>Netshell를 사용 하 여 데이터 수집

이 섹션에서는 netshell를 사용 하 여 네트워크 추적을 수집 하는 단계를 제공 합니다.

> [!NOTE]  
> Netsh 추적은 ETL 파일을 만듭니다. ETL 파일은 메시지 분석기 (MA) 및 네트워크 모니터 3.4 에서만 열 수 있습니다 (파서를 네트워크 모니터 파서 \> 창으로 설정).

1. SMB 서버와 SMB 클라이언트 모두에서 드라이브 **C**에 **임시** 폴더를 만듭니다. 그런 다음, 다음 명령을 실행 합니다.

   ```cmd
   netsh trace start capture=yes report=yes scenario=NetConnection level=5 maxsize=1024 tracefile=c:\\Temp\\%computername%\_nettrace.etl**
   ```
   
   PowerShell을 사용 하는 경우 다음 cmdlet을 실행 합니다.
   
   ```PowerShell
   New-NetEventSession -Name trace -LocalFilePath "C:\Temp\$env:computername`_netCap.etl" -MaxFileSize 1024

   Add-NetEventPacketCaptureProvider -SessionName trace -TruncationLength 1500

   Start-NetEventSession trace
   ```
   
2. 문제를 재현합니다.

3. 다음 명령을 실행 하 여 추적을 중지 합니다.

   ```cmd
   netsh trace stop
   ```
   
   PowerShell을 사용 하는 경우 다음 cmdlet을 실행 합니다.

   ```PowerShell
   Stop-NetEventSession trace  
   Remove-NetEventSession trace
   ```

> [!NOTE] 
> 전송 된 데이터의 최소 양만 추적 해야 합니다. 성능 문제에 대해 상황에서 허용 하는 경우 항상 적절 하 고 잘못 된 추적을 수행 합니다.

### <a name="analyze-the-traffic"></a>트래픽 분석

SMB는 네트워크 전송 프로토콜로 TCP/IP를 사용 하는 응용 프로그램 수준 프로토콜입니다. 따라서 SMB 문제는 TCP/IP 문제로 인해 발생할 수도 있습니다.

TCP/IP가 이러한 문제를 경험 하는지 확인 합니다.

1. TCP 3 방향 핸드셰이크가 끝나지 않습니다. 이는 일반적으로 방화벽 블록이 있거나 서버 서비스가 실행 되 고 있지 않음을 나타냅니다.

2. 재전송이 발생 합니다. 이로 인해 복합 TCP 혼잡 제한으로 인해 파일 전송이 느려질 수 있습니다.

3. TCP 다시 설정 후 5 번의 재전송은 시스템 간 연결이 끊어졌거나 SMB 서비스 중 하나가 응답 하지 않거나 작동이 중지 되었음을 의미할 수 있습니다.

4. TCP 수신 기간이 감소 합니다. 이는 속도가 낮은 저장소 또는 다른 문제로 인해 AFD (보조 함수 드라이버) Winsock 버퍼에서 데이터가 검색 되지 않는 경우에 발생할 수 있습니다.

뚜렷한 TCP/IP 문제가 없으면 SMB 오류를 확인 하십시오. 이렇게 하려면 다음 단계를 수행합니다.

1. SMB2 프로토콜 사양에 대해 항상 SMB 오류를 확인 합니다. 많은 SMB 오류는 심각 하지 않습니다 (유해 하지 않음). 다음 정보를 참조 하면 오류가 다음 문제와 관련 된 것으로 결론을 만들기 전에 SMB에서 오류를 반환한 이유를 확인할 수 있습니다.

   - [SMB2 메시지 구문](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/6eaf6e75-9c23-4eda-be99-c9223c60b181) 항목에서는 각 SMB 명령 및 해당 옵션에 대해 자세히 설명 합니다.
    
   - [SMB2 클라이언트 처리](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/df0625a5-6516-4fbe-bf97-01bef451cab2) 항목에서는 SMB 클라이언트가 요청을 만들고 서버 메시지에 응답 하는 방법에 대해 자세히 설명 합니다.

   - [SMB2 서버 처리](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/e1d08834-42e0-41ca-a833-fc26f5132a6f) 항목에서는 SMB 서버가 요청을 만들고 클라이언트 요청에 응답 하는 방법에 대해 자세히 설명 합니다.

2. FSCTL\_유효성을 검사 하\_\_정보 협상 (협상 유효성 검사) 명령의 유효성을 검사 한 후 즉시 TCP 다시 설정 명령을 보낼지 여부를 확인 합니다. 그렇다면 다음 정보를 참조 하세요.

   - 클라이언트 또는 서버에서 Negotiate Validate 프로세스가 실패할 경우 SMB 세션을 종료 (TCP 다시 설정) 해야 합니다.

   - WAN 최적화 프로그램이 SMB Negotiate 패킷을 수정 하 고 있기 때문에이 프로세스가 실패할 수 있습니다.

   - 연결이 중간에 종료 된 경우 클라이언트와 서버 간의 마지막 exchange 통신을 확인 합니다.

#### <a name="analyze-the-protocol"></a>프로토콜 분석

네트워크 추적에서 실제 SMB 프로토콜 세부 정보를 확인 하 여 사용 되는 정확한 명령 및 옵션을 이해 합니다.

> [!NOTE]
> 메시지 분석기만 SMBv3 이상 버전 명령을 구문 분석할 수 있습니다.

- SMB는이에 대 한 지시만 수행 합니다.

- SMB 명령을 검사 하 여 응용 프로그램에서 수행 하려는 작업에 대해 많은 정보를 확인할 수 있습니다.

명령 및 작업을 프로토콜 사양과 비교 하 여 모든 것이 제대로 작동 하는지 확인 합니다. 그렇지 않은 경우에는 더 가까운 또는 더 낮은 수준에서 데이터를 수집 하 여 근본 원인에 대 한 자세한 정보를 확인 합니다. 이렇게 하려면 다음 단계를 수행합니다.

1. 표준 패킷 캡처를 수집 합니다.

2. **Netsh** 명령을 실행 하 여 네트워크 스택에 문제가 있는지 여부에 대 한 세부 정보를 추적 하 고 수집 하거나, 방화벽 또는 바이러스 백신 프로그램과 같은 Windows 필터링 플랫폼 (WFP) 응용 프로그램에 삭제 합니다.

3. 다른 모든 옵션에 오류가 발생 하는 경우 SMB 자체 내에서 문제가 발생 하는 것으로 의심 되는 경우 또는 다른 데이터에서 근본 원인을 식별 하기에 충분 하지 않은 경우에는 t. cmd를 수집 합니다.

예를 들면 다음과 같습니다.

- 단일 파일 서버로 파일을 전송 하는 속도가 느립니다.

- 양면 추적에서는 SRV가 읽기 요청에 느리게 응답 함을 보여 줍니다.

- 바이러스 백신 프로그램을 제거 하면 저속 파일 전송이 확인 됩니다.

- 문제를 해결 하려면 바이러스 백신 프로그램 manufactory에 문의 하십시오.

> [!NOTE]
> 필요에 따라 문제 해결 중에 바이러스 백신 프로그램 **을 일시적으로 제거할 수도 있습니다** .

#### <a name="event-logs"></a>이벤트 로그

다음 스크린샷에 표시 된 것 처럼 SMB 클라이언트와 SMB 서버 모두에 자세한 이벤트 로그 구조가 있습니다. 문제의 근본 원인을 찾는 데 도움이 되는 이벤트 로그를 수집 합니다.

![이벤트 로그](media/troubleshooting-smb-1.png)

## <a name="smb-related-system-files"></a>SMB 관련 시스템 파일

이 섹션에서는 SMB 관련 시스템 파일을 나열 합니다. 시스템 파일을 업데이트 된 상태로 유지 하려면 최신 [업데이트 롤업이](https://support.microsoft.com/help/4498140/windows-10-update-history) 설치 되어 있는지 확인 합니다.

**% Windir%\\system32\\드라이버**에 나열 된 SMB 클라이언트 이진 파일:

- RDBSS

- MRXSMB

- MRXSMB10

- MRXSMB20

- MUP

- SMBdirect

**% Windir%\\system32\\드라이버**에 나열 된 SMB 서버 이진 파일:

- SRVNET

- SRV

- SRV2

- SMBdirect

- **% Windir%\\system32**

- srvsvc

![SMB 구성 요소](media/troubleshooting-smb-2.png)

### <a name="update-suggestions"></a>업데이트 제안

SMB 문제를 해결 하기 전에 다음 구성 요소를 업데이트 하는 것이 좋습니다.

- 파일 서버에 파일 저장소가 필요 합니다. 저장소에 iSCSI 구성 요소가 있는 경우 해당 구성 요소를 업데이트 합니다.

- 네트워크 구성 요소를 업데이트 합니다.

- 성능 및 안정성 향상을 위해 Windows Core를 업데이트 합니다.

## <a name="reference"></a>참조

[Microsoft SMB 프로토콜 패킷 교환 시나리오](https://docs.microsoft.com/windows/win32/fileio/microsoft-smb-protocol-packet-exchange-scenario)