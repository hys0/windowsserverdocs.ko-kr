---
title: netstat
description: 활성 TCP 연결, 컴퓨터가 수신 대기 하는 포트, 이더넷 통계, IP 라우팅 테이블, IPv4 통계 및 IPv6 통계를 표시 하는 netstat 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 60e2718f-93cc-4ceb-bf0e-58a6a6e4fc8b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c53ac83c1037d5f4998bb6efa43d66b418119df8
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934803"
---
# <a name="netstat"></a>netstat

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

활성 TCP 연결을 대기할 컴퓨터는 수신 대기, 이더넷 통계, IP 라우팅 테이블, (IP, ICMP, TCP 및 UDP 프로토콜)에 대 한 IPv4 통계 및 IPv6 (에 대 한 통계는 IPv6, ICMPv6, i p v 6 통해 TCP 및 UDP IPv6 프로토콜을 통해) 포트를 표시 합니다. 이 명령은 매개 변수 없이 사용 되며 활성 TCP 연결을 표시 합니다.

> [!IMPORTANT]
> 이 명령은 네트워크 연결에서 네트워크 어댑터의 속성에 구성 요소로 인터넷 프로토콜 (TCP/IP) 프로토콜을 설치 하는 경우에 사용할 수입니다.

## <a name="syntax"></a>구문

```
netstat [-a] [-b] [-e] [-n] [-o] [-p <Protocol>] [-r] [-s] [<interval>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 지정하지 않을 경우 | 모든 활성 TCP 연결 및 컴퓨터가 수신 대기 하는 TCP 및 UDP 포트를 표시 합니다. |
| -b | 각 연결 또는 수신 대기 포트를 만드는 작업과 관련 된 실행 파일을 표시 합니다. 일부 경우에는 잘 알려진 실행 파일이 여러 독립적인 구성 요소를 호스트 하 고, 이러한 경우 연결 또는 수신 대기 포트를 만드는 데 관련 된 일련의 구성 요소가 표시 됩니다. 이 경우 실행 파일 이름은 아래에 있는 []에 있으며, 맨 위는 TCP/IP에 도달할 때까지 호출 되는 구성 요소입니다. 이 옵션은 시간이 많이 걸릴 수 있으며 충분 한 권한이 없으면 실패 합니다.
| -E | 송 / 수신 패킷 및 바이트의 수와 같은 이더넷 통계를 표시 합니다. 이 매개 변수를 결합할 수 **-s**합니다. |
| -n | 그러나 활성 TCP 연결을 표시 합니다. 주소 및 포트 번호는 수치화 하는 이름을 확인 하려고 시도 하지. |
| -o | 활성 TCP 연결을 표시 하 고 각 연결에 대 한 프로세스 ID (PID)를 포함 합니다. Windows 작업 관리자의 프로세스 탭에서 PID를 기준으로 애플리케이션을 찾을 수 있습니다. 이 매개 변수를 결합할 수 **-**, **-n**, 및 **-p**합니다. |
| -p `<Protocol>` | 에 지정 된 프로토콜에 대 한 연결을 보여 줍니다 *프로토콜*합니다. 이 경우에 *프로토콜* tcp, udp, tcpv6, udpv6를 사용할 수 있습니다. 이 매개 변수를 사용 하는 경우 **-s** 프로토콜에서 통계를 표시 하려면 *프로토콜* tcp, udp, icmp, ip, tcpv6, udpv6, icmpv6, 또는 i p v 6 일 수 있습니다. |
| -S | 프로토콜에서 통계를 표시합니다. 기본적으로 TCP, UDP, ICMP 및 IP 프로토콜에 대 한 통계가 표시 됩니다. IPv6 프로토콜이 설치 되어 있는 경우 통계가 표시 됩니다 TCP에 대 한 IPv6, UDP를 통해 IPv6, ICMPv6, 및 i p v 6을 통해 프로토콜. **-p** 프로토콜의 집합을 지정 하려면 매개 변수를 사용할 수 있습니다. |
| -r | IP 라우팅 테이블의 내용을 표시합니다. Route print 명령을 하는 것과 같습니다. |
| `<interval>` | 선택한 정보를 *간격* (초)으로 모두를 선택 합니다. CTRL + C를 다시 표시 하지 않으려면 키를 누릅니다. 이 매개 변수를 생략 하면이 명령은 선택한 정보를 한 번만 인쇄 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- **Netstat** 명령은 다음에 대 한 통계를 제공 합니다.

    | 매개 변수 | 설명 |
    | --------- | ----------- |
    | X-forwarded-proto | 프로토콜 (TCP 또는 UDP)의 이름입니다. |
    | 로컬 주소 | 사용 중인 로컬 컴퓨터의 IP 주소와 포트 번호입니다. IP 주소에 해당 하는 로컬 컴퓨터의 이름 및 포트의 이름을 확인할 수는 **-n** 매개 변수를 지정 합니다. 포트 연결이 아직 설정 되지 포트 번호는 별표 (*)로 표시 됩니다. |
    | 외부 주소 | 소켓이 연결 된 원격 컴퓨터의 IP 주소와 포트 번호입니다. 않는 한 IP 주소 및 포트에 해당 하는 이름이 표시 됩니다는 **-n** 매개 변수를 지정 합니다. 포트 연결이 아직 설정 되지 포트 번호는 별표 (*)로 표시 됩니다. |
    | 시스템 상태 | 다음을 포함 하 여 TCP 연결의 상태를 나타냅니다.<ul><li>CLOSE_WAIT</li><li>CLOSED</li><li>설정</li><li>FIN_WAIT_1</li><li>FIN_WAIT_2</li><li>LAST_ACK</li><li>들</li><li>SYN_RECEIVED</li><li>SYN_SEND</li><li>TIMED_WAIT</li></ul> |

### <a name="examples"></a>예

이더넷 통계와 모든 프로토콜에 대 한 통계를 표시 하려면 다음을 입력 합니다.

```
netstat -e -s
```

TCP 및 UDP 프로토콜에 대 한 통계를 표시 하려면 다음을 입력 합니다.

```
netstat -s -p tcp udp
```

활성 TCP 연결 및 프로세스 Id 5 초 간격을 표시 하려면 다음을 입력 합니다.

```
netstat -o 5
```

표시할 활성 TCP 연결 및 프로세스에는 숫자 형식을 사용 하 여 Id 입력:

```
netstat -n -o
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
