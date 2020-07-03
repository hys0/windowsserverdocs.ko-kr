---
title: tracert
description: 대상에 대 한 참조 문서-ICMP (Internet Control Message Protocol) echo 요청 또는 ICMPv6 메시지를 대상으로 전송 하 여 TTL (time to Live) 필드 값을 점차적으로 증가 시켜 대상에 대해 수행 되는 경로를 결정 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9032a032-2e5e-49d4-9e86-f821600e4ba6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: adc73fdd646b3a9f7202f286912b5295f0c4e140
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933735"
---
# <a name="tracert"></a>tracert

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

TTL (time to Live) 필드 값을 증분 방식으로 증가 시켜 ICMP (Internet Control Message Protocol) echo Request 또는 ICMPv6 메시지를 대상으로 전송 하 여 대상에 사용 되는 경로를 결정 합니다. 표시 된 경로 원본 호스트와 대상 간의 경로에 있는 라우터/쪽 근처 라우터 인터페이스의 목록입니다. 근처/쪽 인터페이스는 경로 있는 송신 호스트에 가장 가까운 라우터 인터페이스입니다. 매개 변수 없이 사용, tracert 도움말을 표시 합니다.


## <a name="syntax"></a>구문

```
tracert [/d] [/h <MaximumHops>] [/j <Hostlist>] [/w <timeout>] [/R] [/S <Srcaddr>] [/4][/6] <TargetName>
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|/d|방지 **tracert** 이름으로 중간 라우터의 IP 주소를 확인 하려고 합니다. 이 수를 빠르게 표시의 **tracert** 결과입니다.|
|/h\<MaximumHops>|대상 (대상)을 검색할 경로의 최대 홉 수를 지정 합니다. 기본값은 30 홉입니다.|
|/j\<Hostlist>|Echo Request 메시지에서 *Hostlist*에 지정 된 중간 대상 집합을 사용 하 여 IP 헤더의 느슨한 원본 경로 옵션을 사용 하도록 지정 합니다. 느슨한 원본 라우팅을 사용 하 여 연속 중간 대상 하나 또는 여러 개의 라우터에 의해 분리할 수 있습니다. 호스트 목록에 있는 주소 또는 이름의 최대 수는 9입니다. *Hostlist* 은 공백으로 구분 된 일련의 IP 주소 (점으로 구분 된 10 진수 표기법)입니다. IPv4 주소를 추적 하는 경우에이 매개 변수를 사용 합니다.|
|/w\<timeout>|받은 ICMP 시간 초과 또는 지정 된 에코 요청 메시지에 해당 하는 echo Reply 메시지에 해당 하는 대기 시간 (밀리초)을 지정 합니다. 제한 시간 내에 받지 못한, 별표 (*)이 표시 됩니다. 기본 제한 시간은 4000 (4 초)입니다.|
|/R|대상를 중간 대상으로 사용 하 고 역방향 경로를 테스트 하 여 로컬 호스트에 에코 요청 메시지를 전송 하는 데 IPv6 라우팅 확장 헤더를 사용 하도록 지정 합니다.|
|/S\<Srcaddr>|에코 요청 메시지에 사용할 원본 주소를 지정 합니다. IPv6 주소를 추적 하는 경우에이 매개 변수를 사용 합니다.|
|/4|tracert.exe이 추적에 IPv4만 사용할 수 있도록 지정 합니다.|
|/6|tracert.exe이 추적에 i p v 6만 사용할 수 있도록 지정 합니다.|
|\<TargetName>|식별 된 대상 지정 IP 주소 또는 호스트 이름으로 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

- 이 진단 도구는 TTL (time to Live) 값이 다양 한 ICMP 에코 요청 메시지를 대상에 전송 하 여 대상에 대해 수행 되는 경로를 결정 합니다. 경로 따라 각 라우터에 필요 IP 패킷에 TTL을 감소 시키기 위해 적어도 1 전달 하기 전에 합니다. 실질적으로 TTL은 최대의 연결 카운터입니다. 패킷의 TTL이 0에 도달 하면 라우터가 원본 컴퓨터에 ICMP 시간 초과 메시지를 반환 합니다. tracert는 TTL이 1 인 첫 번째 에코 요청 메시지를 전송 하 고 대상이 응답 하거나 최대 홉 수에 도달할 때까지 각 후속 전송에서 TTL을 1 씩 증가 시켜 경로를 결정 합니다. 최대 홉 수는 기본적으로 30 및 사용 하 여 지정할 수는 **/h** 매개 변수입니다. 경로는 중간 라우터에서 반환 된 ICMP 시간 초과 메시지와 대상에서 반환 된 echo Reply 메시지를 검사 하 여 결정 됩니다. 그러나 일부 라우터는 TTL 값이 만료 된 패킷에 대 한 시간 초과 메시지를 반환 하지 않으며 tracert 명령에 표시 되지 않습니다. 이 경우 별표 (*)이 홉에 대해 표시 됩니다.
- 경로를 추적 하 고 각 라우터와 연결에 대 한 네트워크 대기 시간 및 패킷 손실을 제공 하려면 [**pathping**](pathping.md) 명령을 사용 합니다.
- 이 명령은 네트워크 연결에서 네트워크 어댑터의 속성에 구성 요소로 인터넷 프로토콜 (TCP/IP) 프로토콜을 설치 하는 경우에 사용할 수입니다.

## <a name="examples"></a>예

Corp7.microsoft.com 명명 된 호스트에 대 한 경로 추적 하려면 다음을 입력 합니다.
```
tracert corp7.microsoft.com
```
Corp7.microsoft.com 명명 된 호스트에 대 한 경로 추적 하 고 해당 이름으로 각 IP 주소 확인을 방지 하려면 다음을 입력 합니다.
```
tracert /d corp7.microsoft.com
```
Corp7.microsoft.com 명명 된 호스트에 대 한 경로 추적 하 고을 느슨한 원본 경로 10.12.0.1/10.29.3.1/10.1.44.1를 사용 하려면 입력 합니다.
```
tracert /j 10.12.0.1 10.29.3.1 10.1.44.1 corp7.microsoft.com
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
