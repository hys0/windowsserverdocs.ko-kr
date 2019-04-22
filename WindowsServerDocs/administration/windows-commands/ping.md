---
title: ping
description: Ping을 사용 하 여 네트워크 연결을 확인 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49272671-2eec-4fa5-881f-65c24cfbef52
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 1ac02a148061cd6eb8480c67f15e934f5fd57768
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816754"
---
# <a name="ping"></a>ping

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

합니다 **ping** 명령 제어 메시지 ICMP (Internet Protocol) 에코 요청 메시지를 전송 하 여 다른 TCP/IP 컴퓨터에 대 한 IP 수준 연결을 확인 합니다. 수신 해당 echo Reply 메시지의 왕복 시간이 함께 표시 됩니다. ping은 연결, 연결 가능성, 및 이름 확인 문제를 해결 하는 데 사용 되는 기본 TCP/IP 명령입니다. 매개 변수 없이 사용 **ping** 도움말을 표시 합니다.

## <a name="syntax"></a>구문

```
ping [/t] [/a] [/n <Count>] [/l <Size>] [/f] [/I <TTL>] [/v <TOS>] [/r <Count>] [/s <Count>] [{/j <Hostlist> | /k <Hostlist>}] [/w <timeout>] [/R] [/S <Srcaddr>] [/4] [/6] <TargetName>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|/t|중단 될 때까지 대상에 에코 요청 메시지를 보내고 해당 ping 계속 지정 합니다. 중단 하 고 통계를 표시 하려면 CTRL + break를 누릅니다. 중단 및 종료 **ping**, CTRL + C를 누릅니다.|
|/ a|대상 IP 주소에 역방향 이름 확인 수행 되도록 지정 합니다. 이 연결이 성공 하면 ping 해당 호스트 이름을 표시 합니다.|
|/n \<Count\>|Echo의 수를 지정 합니다. 전송 된 메시지를 요청 합니다. 기본값은 4입니다.|
|/l \<Size\>|길이 지정 합니다 (바이트)를 에코 데이터 필드의 보낸 메시지를 요청 합니다. 기본값은 32입니다. 최대 크기가 65,527을 보여 줍니다.|
|/f|수행 된 요청 메시지를 보낼 에코 하는 지정 되지 않습니다 (IPv4만 가능 함) 1로 설정 된 IP 헤더의 플래그를 조각. 대상 경로에 라우터에서 에코 요청 메시지를 조각화 할 수 없습니다. 이 매개 변수는 경로 최대 전송 단위 (PMTU) 문제 해결에 유용 합니다.|
|/I \<TTL\>|에코에 대 한 IP 헤더에서 TTL 필드의 값을 지정 합니다. 전송 된 메시지를 요청 합니다. 기본값은 호스트에 대 한 기본 TTL 값입니다. 최대 *TTL* 은 255입니다.|
|/v \<TOS\>|Echo에 대 한 IP 헤더에서 형식의 TOS (서비스) 필드의 값을 지정 합니다. (IPv4만 가능 함) 전송 된 메시지를 요청 합니다. 기본값은 0입니다. *TOS* 0부터 255 까지의 10 진수 값으로 지정 됩니다.|
|/r \<Count\>|IP 헤더의 레코드 경로 옵션이 에코 요청 메시지에서 사용 된 경로 기록 하는 데 사용 됩니다 하 고 해당 echo Reply 메시지 (IPv4만 가능 함)을 지정 합니다. 경로의 각 홉 레코드 경로 옵션의 항목을 사용 합니다. 가능한 경우 지정는 *개수* 원본과 대상 간의 홉의 수보다 크거나 같은입니다. 합니다 *개수* 최소 1 자에서 9 여야 합니다.|
|/s \<Count\>|IP 헤더의 인터넷 타임 스탬프 옵션이 에코 요청 메시지에 대 한 도착 시간을 기록 하는 데 사용 됩니다 하 고 해당 echo Reply 메시지의 각 홉을 지정 합니다. 합니다 *개수* 최소 1 자에서 4 이어야 합니다. 대상 링크-로컬 주소에 대 한 필수입니다.|
|/j \<Hostlist\>|Echo 느슨한 원본 경로 사용 하 여 요청 메시지에 지정 하는 중간 대상 집합과 IP 헤더 옵션을 지정 *Hostlist* (IPv4만 가능 함). 느슨한 원본 라우팅을 사용 하 여 연속 중간 대상 하나 또는 여러 개의 라우터에 의해 분리할 수 있습니다. 주소 또는 호스트 목록의 이름은 최대 수는 9입니다. 호스트 목록은 공백으로 구분 하 여 일련의 점으로 구분 된 10 진수 표기법으로 IP 주소입니다.|
|/k \<Hostlist\>|echo 엄격한 원본 경로 사용 하 여 요청 메시지에 지정 하는 중간 대상 집합과 IP 헤더 옵션 지정 *Hostlist* (IPv4만 가능 함). 엄격한 원본 라우팅을 사용 하 여 다음 중간 대상 직접 연결할 수 있어야 합니다 (인접 라우터 인터페이스에서 이어야 함). 주소 또는 호스트 목록의 이름은 최대 수는 9입니다. 호스트 목록은 공백으로 구분 하 여 일련의 점으로 구분 된 10 진수 표기법으로 IP 주소입니다.|
|/w \<timeout\>|밀리초 에코 응답 메시지를 받이 지정된 에코 요청 메시지에 해당 하는 대기 시간을 지정 합니다. Echo Reply 메시지의 제한 시간 내에 받지 "요청 시간 초과" 오류 메시지가 표시 됩니다. 기본 제한 시간은 4000 (4 초)입니다.|
|/R|왕복 경로가 (ipv6만 사용 가능) 추적을 지정 합니다.|
|/S \<Srcaddr\>|(Ipv6만 사용 가능)를 사용 하는 원본 주소를 지정 합니다.|
|/4|IPv4 ping 사용 되도록 지정 합니다. 이 매개 변수는 IPv4 주소를 사용 하 여 대상 호스트를 식별할 필요가 없습니다. 이름으로 대상 호스트를 확인할 필요만 해당 합니다.|
|/6|IPv6 ping 사용 되도록 지정 합니다. 이 매개 변수는 IPv6 주소를 사용 하 여 대상 호스트를 식별할 필요가 없습니다. 이름으로 대상 호스트를 확인할 필요만 해당 합니다.|
|\<TargetName\>|호스트 이름 또는 대상의 IP 주소를 지정합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   사용할 수 있습니다 **ping** 컴퓨터 이름 및 컴퓨터의 IP 주소를 테스트 합니다. IP 주소를 ping 성공 하지만 되지 컴퓨터 이름을 ping 하는 경우에 이름 확인 문제가 해야 합니다. 이 경우 도메인 이름 시스템 (DNS) 쿼리를 사용 하 여 로컬 호스트 파일을 통해 해결할 수 있습니다 또는 NetBIOS를 통해 문제 해결 기술 이름을 지정 하는 컴퓨터 이름을 확인 합니다.
-   이 명령은 네트워크 연결에서 네트워크 어댑터의 속성에 구성 요소로 인터넷 프로토콜 (TCP/IP) 프로토콜을 설치 하는 경우에 사용할 수입니다.

## <a name="BKMK_Examples"></a>예제

다음 예와 **ping** 명령 출력:

```
C:\>ping example.microsoft.com       
         pinging example.microsoft.com [192.168.239.132] with 32 bytes of data:       
         Reply from 192.168.239.132: bytes=32 time=101ms TTL=124       
         Reply from 192.168.239.132: bytes=32 time=100ms TTL=124       
         Reply from 192.168.239.132: bytes=32 time=120ms TTL=124       
         Reply from 192.168.239.132: bytes=32 time=120ms TTL=124
```

Ping 대상 10.0.99.221 10.0.99.221 호스트 이름에를 입력 합니다.

```
ping /a 10.0.99.221
```

대상 10.0.99.221 10 에코 요청 메시지를 사용 하 여 1000 바이트의 데이터 필드에 각각 ping을 입력 합니다.

```
ping /n 10 /l 1000 10.0.99.221
```

대상 10.0.99.221을 ping 하 고 4 개의 홉에 대 한 경로 기록 하려면 입력 합니다.

```
ping /r 4 10.0.99.221
```

Ping 대상 10.0.99.221 10.12.0.1-10.29.3.1-10.1.44.1의 느슨한 원본 경로 지정을 입력 합니다.

```
ping /j 10.12.0.1 10.29.3.1 10.1.44.1 10.0.99.221
```

## <a name="additional-references"></a>추가 참조
-   [명령줄 구문 키](command-line-syntax-key.md)
