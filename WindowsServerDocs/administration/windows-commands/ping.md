---
title: ping
description: Ping을 사용 하 여 네트워크 연결을 확인 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 49272671-2eec-4fa5-881f-65c24cfbef52
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: c9e03b45d889bcac87bd3e533ab69c7a07be74ee
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837556"
---
# <a name="ping"></a>ping

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**Ping** 명령은 ICMP (Internet Control Message Protocol) 에코 요청 메시지를 전송 하 여 다른 tcp/ip 컴퓨터에 대 한 IP 수준 연결을 확인 합니다. 해당 에코 응답 메시지의 수신이 라운드트립 시간과 함께 표시 됩니다. ping은 연결, 연결 가능성 및 이름 확인을 해결 하는 데 사용 되는 기본 TCP/IP 명령입니다. 매개 변수 없이 사용 하 여 **ping** 도움말을 표시 합니다.

## <a name="syntax"></a>구문

```
ping [/t] [/a] [/n <Count>] [/l <Size>] [/f] [/I <TTL>] [/v <TOS>] [/r <Count>] [/s <Count>] [{/j <Hostlist> | /k <Hostlist>}] [/w <timeout>] [/R] [/S <Srcaddr>] [/4] [/6] <TargetName>
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|/t|Ping이 중단 될 때까지 대상에 에코 요청 메시지를 계속 보내도록 지정 합니다. 통계를 중단 하 고 표시 하려면 CTRL + break를 누릅니다. **Ping**을 중단 하 고 종료 하려면 Ctrl + C를 누릅니다.|
|/a|대상 IP 주소에 대해 역방향 이름 확인을 수행 하도록 지정 합니다. 성공할 경우 ping은 해당 호스트 이름을 표시 합니다.|
|/n \<개수\>|전송 된 echo Request 메시지의 수를 지정 합니다. 기본값은 4입니다.|
|/l \<크기\>|전송 된 에코 요청 메시지에 있는 데이터 필드의 길이 (바이트)를 지정 합니다. 기본값은 32입니다. 최대 크기는 65527입니다.|
|/f|IP 헤더에서 1로 설정 된 IP 헤더의 Do not Fragment 플래그를 사용 하 여 에코 요청 메시지를 보내도록 지정 합니다 (IPv4 에서만 사용 가능). 에코 요청 메시지는 대상 경로에 있는 라우터로 조각화 할 수 없습니다. 이 매개 변수는 PMTU (경로 최대 전송 단위) 문제를 해결 하는 데 유용 합니다.|
|/I \<TTL\>|전송 된 echo Request 메시지의 IP 헤더에 있는 TTL 필드의 값을 지정 합니다. 기본값은 호스트의 기본 TTL 값입니다. 최대 *TTL* 은 255입니다.|
|/v \<TOS\>|전송 된 에코 요청 메시지의 IP 헤더에 있는 TOS (서비스 형식) 필드의 값을 지정 합니다 (IPv4 에서만 사용 가능). 기본값은 0입니다. *TOS* 는 0에서 255 사이의 10 진수 값으로 지정 됩니다.|
|/r \<Count\>|IP 헤더의 레코드 경로 옵션을 사용 하 여 에코 요청 메시지 및 해당 에코 응답 메시지에 의해 수행 된 경로를 기록 하도록 지정 합니다 (i p v 4 에서만 사용 가능). 경로의 각 홉은 레코드 경로 옵션의 항목을 사용 합니다. 가능 하면 원본 및 대상 간의 홉 수보다 크거나 같은 *수* 를 지정 합니다. *개수* 는 1 ~ 9 자 여야 합니다.|
|/s \<개수\>|IP 헤더의 인터넷 타임 스탬프 옵션을 사용 하 여 각 홉에 대 한 에코 요청 메시지 및 해당 에코 응답 메시지 도착 시간을 기록 하도록 지정 합니다. *개수* 는 1이 고 최대값은 4 여야 합니다. 링크-로컬 대상 주소에 필요 합니다.|
|/j \<Hostlist\>|Echo Request 메시지에서 *Hostlist* 에 지정 된 중간 대상 집합 (i p v 4 에서만 사용 가능)을 사용 하 여 IP 헤더의 느슨한 원본 경로 옵션을 사용 하도록 지정 합니다. 느슨한 원본 라우팅을 사용 하 여 연속 중간 대상 하나 또는 여러 개의 라우터에 의해 분리할 수 있습니다. 호스트 목록에 있는 주소 또는 이름의 최대 수는 9입니다. 호스트 목록은 공백으로 구분 된 일련의 IP 주소 (점으로 구분 된 10 진수 표기법)입니다.|
|/k \<Hostlist\>|Echo Request 메시지에서 *Hostlist* 에 지정 된 중간 대상 집합 (i p v 4 에서만 사용 가능)을 사용 하 여 IP 헤더의 엄격한 원본 경로 옵션을 사용 하도록 지정 합니다. 엄격한 원본 라우팅을 사용 하는 경우 다음 중간 대상은 직접 연결할 수 있어야 합니다 (라우터의 인터페이스에서 인접 해야 함). 호스트 목록에 있는 주소 또는 이름의 최대 수는 9입니다. 호스트 목록은 공백으로 구분 된 일련의 IP 주소 (점으로 구분 된 10 진수 표기법)입니다.|
|/w \<시간 제한\>|수신 되는 지정 된 에코 요청 메시지에 해당 하는 echo Reply 메시지를 대기 하는 시간 (밀리초)을 지정 합니다. 제한 시간 내에 echo Reply 메시지가 수신 되지 않으면 "요청 시간이 초과 되었습니다." 라는 오류 메시지가 표시 됩니다. 기본 제한 시간은 4000 (4 초)입니다.|
|/R|라운드트립 경로를 추적 하도록 지정 합니다 (i p v 6 에서만 사용 가능).|
|/S \<Srcaddr\>|사용할 원본 주소를 지정 합니다 (i p v 6 에서만 사용 가능).|
|/4|Ping에 IPv4를 사용 하도록 지정 합니다. 이 매개 변수는 IPv4 주소가 있는 대상 호스트를 식별 하는 데 필요 하지 않습니다. 이름으로 대상 호스트를 식별 하는 경우에만 필요 합니다.|
|/6|I p v 6를 사용 하 여 ping 하도록 지정 합니다. 이 매개 변수는 IPv6 주소를 사용 하 여 대상 호스트를 식별 하는 데 필요 하지 않습니다. 이름으로 대상 호스트를 식별 하는 경우에만 필요 합니다.|
|\<TargetName\>|대상의 호스트 이름 또는 IP 주소를 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>주의

-   **Ping** 을 사용 하 여 컴퓨터 이름과 컴퓨터의 IP 주소를 모두 테스트할 수 있습니다. IP 주소를 ping 하는 데 성공 했지만 컴퓨터 이름 ping을 수행할 수 없는 경우 이름 확인 문제가 있을 수 있습니다. 이 경우 DNS (Domain Name System) 쿼리를 사용 하거나 NetBIOS 이름 확인 기술을 통해 지정 하는 컴퓨터 이름을 로컬 호스트 파일을 통해 확인할 수 있는지 확인 합니다.
-   이 명령은 네트워크 연결에서 네트워크 어댑터의 속성에 구성 요소로 인터넷 프로토콜 (TCP/IP) 프로토콜을 설치 하는 경우에 사용할 수입니다.

## <a name="examples"></a><a name="BKMK_Examples"></a>예와

다음 예에서는 **ping** 명령 출력을 보여 줍니다.

```
C:\>ping example.microsoft.com       
         pinging example.microsoft.com [192.168.239.132] with 32 bytes of data:       
         Reply from 192.168.239.132: bytes=32 time=101ms TTL=124       
         Reply from 192.168.239.132: bytes=32 time=100ms TTL=124       
         Reply from 192.168.239.132: bytes=32 time=120ms TTL=124       
         Reply from 192.168.239.132: bytes=32 time=120ms TTL=124
```

대상 10.0.99.221를 ping 하 고 10.0.99.221를 호스트 이름으로 확인 하려면 다음을 입력 합니다.

```
ping /a 10.0.99.221
```

각각 1000 바이트의 데이터 필드를 포함 하는 10 개의 에코 요청 메시지를 사용 하 여 대상 10.0.99.221를 ping 하려면 다음을 입력 합니다.

```
ping /n 10 /l 1000 10.0.99.221
```

대상 10.0.99.221를 ping 하 고 4 홉에 대 한 경로를 기록 하려면 다음을 입력 합니다.

```
ping /r 4 10.0.99.221
```

대상 10.0.99.221를 ping 하 고 10.12.0.1-10.29.3.1-10.1.44.1의 느슨한 원본 경로를 지정 하려면 다음을 입력 합니다.

```
ping /j 10.12.0.1 10.29.3.1 10.1.44.1 10.0.99.221
```

## <a name="additional-references"></a>추가 참조
-   - [명령줄 구문 키](command-line-syntax-key.md)
