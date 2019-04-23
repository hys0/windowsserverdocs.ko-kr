---
title: pathping
description: 네트워크 대기 시간 및 pathping 명령을 사용 하 여 손실 정보를 가져오는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec430125-b1dc-4aad-a7c9-b70f486d9e3c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: db3a0f5cd3c711f7df0a13627969dc7b74b3d605
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837244"
---
# <a name="pathping"></a>pathping

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

네트워크 대기 시간 및 네트워크 연결 끊김 원본과 대상 간의 중간 홉에 대 한 정보를 제공합니다. **pathping** 여러 에코 요청 메시지를 보내고 원본과 대상 간의 각 라우터에 기간 및 각 라우터에서 반환 되는 패킷에 기준으로 결과 계산 합니다. 때문에 **pathping** 정도 표시 합니다. 모든 특정된 라우터 또는 링크, 패킷 손실의 확인할 수 있습니다는 라우터 또는 서브넷 네트워크 문제가 있을 수 있습니다. 

**pathping** 수행과 동일 합니다 **tracert** 어떤 라우터는 경로 식별 하 여 명령을 합니다. 지정 된 기간 동안 주기적으로 모든 라우터에 ping을 보냅니다 하 고 각각에서 반환 된 수를 기준으로 통계를 계산 합니다. 매개 변수 없이 사용 **pathping** 도움말을 표시 합니다. 

## <a name="syntax"></a>구문
```
pathping [/n] [/h] [/g <Hostlist>] [/p <Period>] [/q <NumQueries> [/w <timeout>] [/i <IPaddress>] [/4 <IPv4>] [/6 <IPv6>][<TargetName>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/n|방지 **pathping** 해당 이름으로 중간 라우터의 IP 주소를 확인 하려고 합니다. 이 표시를 신속 하 게 될 수 있습니다 **pathping** 결과입니다.|
|/h \<MaximumHops>|대상 (대상)에 대 한 검색 경로에 최대 홉 수를 지정 합니다. 기본값은 30 홉입니다.|
|/g \<Hostlist >|Echo 느슨한 원본 경로 사용 하 여 요청 메시지에 지정 하는 중간 대상 집합과 IP 헤더 옵션을 지정 *Hostlist*합니다. 느슨한 원본 라우팅을 사용 하 여 연속 중간 대상 하나 또는 여러 개의 라우터에 의해 분리할 수 있습니다. 주소 또는 호스트 목록의 이름은 최대 수는 9입니다. 합니다 *Hostlist* 공백으로 구분 된 일련의 점으로 구분 된 10 진수 표기법으로 IP 주소입니다.|
|/ p \<기간 >|연속 ping 사이 대기할 시간을 밀리초 단위로 지정 합니다. 기본값은 250 밀리초 (1/4 초)입니다.|
|/q \<NumQueries>|Echo 횟수를 지정 경로에서 각 라우터를 전송 된 메시지를 요청 합니다. 기본값은 100 개의 쿼리.|
|/w \<timeout>|각 회신을 기다릴 밀리초 수를 지정 합니다. 기본값은 3000 밀리초 (3 초)입니다.|
|/i \<IPaddress>|원본 주소를 지정합니다.|
|/4 \<IPv4>|해당 pathping는 IPv4만 지정 합니다.|
|/6 \<IPv6>|해당 pathping에서는 IPv6만 지정 합니다.|
|\<TargetName>|대상 지정 IP 주소 또는 호스트 이름으로 식별 하는 됩니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명
-   **pathping** 매개 변수는 대/소문자 구분 합니다.
-   네트워크 정체를 방지 하려면 충분히 느린 속도로 ping은 전송 합니다.
-   버스트 손실의 영향을 최소화 하려면 ping을 너무 자주 보내지 마세요.
-   사용 하는 경우는 **/p** 매개 변수를 ping은 개별적으로 각 중간 홉에 보내집니다. 이 인해 동일한 홉에 전송 하는 두 ping 간격이 *기간* 홉 수를 곱합니다.
-   사용 하는 경우는 **/w** 매개 변수를 여러 ping 동시에 보낼 수 있습니다. 이 때문에 지정 된 시간을 *제한 시간* 매개 변수는에 지정 된 시간 제한 되지를 *기간* ping에 걸리는 대기 시간이 대 한 매개 변수.
-   이 명령은 네트워크 연결에서 네트워크 어댑터의 속성에 구성 요소로 인터넷 프로토콜 (TCP/IP) 프로토콜을 설치 하는 경우에 사용할 수입니다.

## <a name="BKMK_Examples"></a>예제

다음 예와 **pathping** 명령 출력:

```
D:\>pathping /n corp1
Tracing route to corp1 [10.54.1.196]
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
때 **pathping** 는 첫 번째 결과 실행 한 경로 나열 합니다. 사용 하 여 표시 되는 동일한 경로 **tracert** 명령입니다. 다음으로, 약 90 초 (시간은 홉 수에 따라 다름)에 대 한 사용 중인 메시지가 표시 됩니다. 이 시간 동안 정보가 위에 나열 된 모든 라우터 및 링크에서 서로 수집 됩니다. 이 기간 후에 테스트 결과가 표시 됩니다.

위의 샘플 보고서에는 **이 노드/링크**, **손실/Sent입니다. Pct =** 하 고 **주소** 13 172.16.87.218 및 192.168.52.1 간의 링크 삭제는 열에 표시 패킷의 백분율입니다. 라우터 홉 2 및 4에서 패킷이 손실 되, 해결 하지만이 손실에 해결 되지 않은 트래픽을 전달 하기 위한 기능이 영향을 주지 않습니다.

세로 막대로 식별 하는 링크에 대 한 표시는 손실률 (**|**)에 **주소** 열에 전달 되는 패킷 손실을 발생 시키는 링크 정체 됨을 나타냅니다는 경로입니다. (IP 주소로 식별) 라우터에 대해 표시 되는 손실률 이러한 라우터 오버 로드를 나타냅니다.

## <a name="additional-references"></a>추가 참조
-   [명령줄 구문 키](command-line-syntax-key.md)