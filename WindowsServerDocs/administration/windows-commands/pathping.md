---
title: pathping
description: 원본 및 대상 간의 중간 홉에서 네트워크 대기 시간 및 네트워크 손실에 대 한 정보를 가져오는 pathping 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ec430125-b1dc-4aad-a7c9-b70f486d9e3c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 887a819c28d546f8c73d07fedbefbe27b65e7a5a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931397"
---
# <a name="pathping"></a>pathping

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원본 및 대상 간의 중간 홉에서 네트워크 대기 시간 및 네트워크 손실에 대 한 정보를 제공 합니다. 이 명령은 여러 에코 요청 메시지를 일정 기간 동안 원본 및 대상 간에 각 라우터에 보낸 다음 각 라우터에서 반환 된 패킷을 기반으로 결과를 계산 합니다. 이 명령은 지정 된 라우터 또는 링크에서 패킷 손실의 정도를 표시 하기 때문에 네트워크 문제가 발생할 수 있는 라우터 또는 서브넷을 확인할 수 있습니다. 매개 변수 없이 사용 됩니다 .이 명령은 도움말을 표시 합니다.

> [!NOTE]
> 이 명령은 네트워크 연결에서 네트워크 어댑터의 속성에 구성 요소로 인터넷 프로토콜 (TCP/IP) 프로토콜을 설치 하는 경우에 사용할 수입니다.
>
> 또한이 명령은 [tracert 명령을](tracert.md)사용 하는 것과 동일한 경로에 있는 라우터를 식별 합니다. Howevever이 명령은 지정 된 기간 동안 모든 라우터에 정기적으로 ping을 전송 하 고 각각에서 반환 된 숫자를 기준으로 통계를 계산 합니다.

## <a name="syntax"></a>구문

```
pathping [/n] [/h <maximumhops>] [/g <hostlist>] [/p <Period>] [/q <numqueries> [/w <timeout>] [/i <IPaddress>] [/4 <IPv4>] [/6 <IPv6>][<targetname>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| /n | **Pathping** 에서 중간 라우터의 IP 주소를 해당 이름으로 확인 하려고 시도 하지 않도록 합니다. 이렇게 하면 **pathping** 결과를 신속 하 게 표시할 수 있습니다. |
| /h`<maximumhops>` | 대상 (대상)을 검색할 경로의 최대 홉 수를 지정 합니다. 기본값은 30 홉입니다. |
| /g`<hostlist>` | Echo Request 메시지에서 *hostlist*에 지정 된 중간 대상 집합을 사용 하 여 IP 헤더의 **느슨한 원본 경로** 옵션을 사용 하도록 지정 합니다. 느슨한 원본 라우팅을 사용 하 여 연속 중간 대상 하나 또는 여러 개의 라우터에 의해 분리할 수 있습니다. 호스트 목록에 있는 주소 또는 이름의 최대 수는 **9**입니다. *Hostlist* 은 공백으로 구분 된 일련의 IP 주소 (점으로 구분 된 10 진수 표기법)입니다. |
| /p`<period>` | 연속 된 ping 사이에 대기 하는 시간 (밀리초)을 지정 합니다. 기본값은 250 밀리초 (1/4 초)입니다. 이 매개 변수는 각 중간 홉에 개별 ping을 보냅니다. 이로 인해 동일한 홉으로 전송 되는 두 ping 사이의 간격에는 홉 수에 따라 *마침표* 를 곱합니다. |
| /q`<numqueries>` | 경로의 각 라우터에 전송 되는 에코 요청 메시지의 수를 지정 합니다. 기본값은 100 쿼리입니다. |
| /w`<timeout>` | 각 회신을 대기할 시간 (밀리초)을 지정 합니다. 기본값은 3000 밀리초 (3 초)입니다. 이 매개 변수는 여러 ping을 동시에 보냅니다. 이로 인해 *timeout* 매개 변수에 지정 된 시간 크기는 ping을 대기 하기 위해 *period* 매개 변수에 지정 된 시간 만큼 제한 되지 않습니다. |
| /i`<IPaddress>` | 소스 주소를 지정합니다. |
| /4`<IPv4>` | Pathping이 i p v 4만 사용 하도록 지정 합니다. |
| /6`<IPv6>` | Pathping에서 i p v 6만 사용 하도록 지정 합니다. |
| `<targetname>` | IP 주소 또는 호스트 이름으로 식별 되는 대상을 지정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 모든 매개 변수는 대/소문자를 구분 합니다.

- 네트워크 정체를 방지 하 고 버스트 손실로 인 한 영향을 최소화 하려면 충분 한 속도로 ping을 전송 해야 합니다.

### <a name="example-of-the-pathping-command-output"></a>Pathping 명령 출력의 예

```
D:\>pathping /n contoso1
Tracing route to contoso1 [10.54.1.196]
over a maximum of 30 hops:
  0  172.16.87.35
  1  172.16.87.218
  2  192.168.52.1
  3  192.168.80.1
  4  10.54.247.14
  5  10.54.1.196
computing statistics for 125 seconds...
            Source to Here   This Node/Link
Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct  address
  0                                           172.16.87.35
                                0/ 100 =  0%   |
  1   41ms     0/ 100 =  0%     0/ 100 =  0%  172.16.87.218
                               13/ 100 = 13%   |
  2   22ms    16/ 100 = 16%     3/ 100 =  3%  192.168.52.1
                                0/ 100 =  0%   |
  3   24ms    13/ 100 = 13%     0/ 100 =  0%  192.168.80.1
                                0/ 100 =  0%   |
  4   21ms    14/ 100 = 14%     1/ 100 =  1%  10.54.247.14
                                0/ 100 =  0%   |
  5   24ms    13/ 100 = 13%     0/ 100 =  0%  10.54.1.196
Trace complete.
```

**Pathping** 을 실행 하면 첫 번째 결과에 경로가 나열 됩니다. 다음으로는 약 90 초 동안 사용 중 메시지가 표시 됩니다. 시간은 홉 수에 따라 달라 집니다. 이 시간 동안 이전에 나열 된 모든 라우터와 이러한 정보 간의 링크에서 정보가 수집 됩니다. 이 기간이 끝나면 테스트 결과가 표시 됩니다.

위의 샘플 보고서에서 **이 노드/링크**, **Lost/Sent = Pct** 및 **address** 열은 *172.16.87.218* 와 *192.168.52.1* 간의 링크가 패킷의 13%를 삭제 하 고 있음을 보여 줍니다. 홉 2와 4의 라우터 역시 주소가 지정 된 패킷을 삭제 하지만이 손실은 주소가 지정 되지 않은 트래픽을 전달 하는 기능에는 영향을 주지 않습니다.

주소 열에서 세로 막대 ()로 식별 되는 링크에 대해 표시 되는 손실 율은 **|** 경로에서 전달 되는 패킷의 손실을 유발 하는 링크 정체를 표시 합니다. **address** IP 주소로 식별 되는 라우터에 대해 표시 되는 손실 요금은 이러한 라우터가 오버 로드 될 수 있음을 표시 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [tracert 명령](tracert.md)
