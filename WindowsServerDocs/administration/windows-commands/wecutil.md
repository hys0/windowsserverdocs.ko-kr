---
title: wecutil
description: 원격 컴퓨터에서 전달 되는 이벤트에 대 한 구독을 만들고 관리할 수 있는 wecutil에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0c82a6cb-d652-429c-9c3d-0f568c78d54b
author: coreyp-at-msft
ms.author: coreyp
manager: dansimps
ms.openlocfilehash: 6c62d3ce24f539b4176acd6193cbd956ecbf5471
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725868"
---
# <a name="wecutil"></a>wecutil



원격 컴퓨터에서 전달 되는 이벤트에 대 한 구독을 만들고 관리할 수 있습니다. 원격 컴퓨터는 WS 관리 프로토콜을 지원 해야 합니다. 


## <a name="syntax"></a>구문

```
wecutil  [{es | enum-subscription}] 
[{gs | get-subscription} <Subid> [/f:<Format>] [/uni:<Unicode>]] 
[{gr | get-subscriptionruntimestatus} <Subid> [<Eventsource> …]] 
[{ss | set-subscription} [<Subid> [/e:[<Subenabled>]] [/esa:<Address>] [/ese:[<Srcenabled>]] [/aes] [/res] [/un:<Username>] [/up:<Password>] [/d:<Desc>] [/uri:<Uri>] [/cm:<Configmode>] [/ex:<Expires>] [/q:<Query>] [/dia:<Dialect>] [/tn:<Transportname>] [/tp:<Transportport>] [/dm:<Deliverymode>] [/dmi:<Deliverymax>] [/dmlt:<Deliverytime>] [/hi:<Heartbeat>] [/cf:<Content>] [/l:<Locale>] [/ree:[<Readexist>]] [/lf:<Logfile>] [/pn:<Publishername>] [/essp:<Enableport>] [/hn:<Hostname>] [/ct:<Type>]] [/c:<Configfile> [/cun:<Username> /cup:<Password>]]] 
[{cs | create-subscription} <Configfile> [/cun:<Username> /cup:<Password>]] 
[{ds | delete-subscription} <Subid>] 
[{rs | retry-subscription} <Subid> [<Eventsource>…]] 
[{qc | quick-config} [/q:[<Quiet>]]].
```

### <a name="parameters"></a>매개 변수

|매개 변수|Description|
|---------|-----------|
|{es \| enum-subscription}|존재 하는 모든 원격 이벤트 구독의 이름을 표시 합니다.|
|{gs \| get-subscription} \<Subid> [/F:\<Format>] [//:\<Unicode>]|원격 구독 구성 정보를 표시합니다. \<Subid>은 구독을 고유 하 게 식별 하는 문자열입니다. \<Subid>은 구독을 만드는 데 사용 된 XML 구성 파일의 \<SubscriptionId> 태그에 지정 된 문자열과 같습니다.|
|{gr \| get-subscriptionruntimestatus} \<Subid> [\<Eventsource> ...]|구독의 런타임 상태를 표시 합니다. \<Subid>은 구독을 고유 하 게 식별 하는 문자열입니다. \<Subid>은 구독을 만드는 데 사용 된 XML 구성 파일의 \<SubscriptionId> 태그에 지정 된 문자열과 같습니다. \<Eventsource>는 이벤트의 원본으로 사용 되는 컴퓨터를 식별 하는 문자열입니다. \<Eventsource>는 정규화 된 도메인 이름, NetBIOS 이름 또는 IP 주소 여야 합니다.|
|{ss \| 설정-구독} \<Subid> [/e: [\<subid>]] [/esa:\<Address>] [/ese: [\<srcenabled>]] [/ese] [/res] [/un:\<Username>] [/up:\<Password>] [/d:\<Desc>] [/uri:\<uri>] [/Ese:\<configmode>] [/예:\<Expires>] [/q:\<Query>] [/dia:\<언어>] [/tn\<:> 이름] [/tp:\<\<>] [/cdm: deliverymode.persistent>] [/dmi:\<Deliverymax>] [/dmlt:\<경우 deliverytime>] [/sas:\<하트 비트>] [/cf:\<Content>] [/l:\<Locale>] [/Ree: [\<Readexist>]] [/lf:\<Logfile>] [/pn:\<\ername>] [/essp:\<enableport>] [/h n:\<Hostname>] [/sct:\<Type>]</br>또는</br>{ss \| set-subscription/C:\<om> [/cun:\<comusername>/cup:\<compassword>]|등록 구성을 변경합니다. 구독 ID 및 구독 매개 변수를 변경 하려면 적절 한 옵션을 지정할 수 있습니다 또는 구독 매개 변수를 변경 하는 XML 구성 파일을 지정할 수 있습니다.|
|{cs \| 만들기-구독} \<K> [/Cun:\<Username>/컵:\<Password>]|원격 구독을 만듭니다. \<> 구독 구성이 포함 된 XML 파일의 경로를 지정 합니다. 절대 또는 현재 디렉터리에 상대적 경로일 수 있습니다.|
|{ds \| 삭제-구독} \<Subid>|구독을 삭제 하 고 구독에 대 한 이벤트 로그에 이벤트를 전달 하는 모든 이벤트 원본의 등록을 취소 합니다. 이미 수신 하 고 기록 된 모든 이벤트 삭제 되지 않습니다. \<Subid>은 구독을 고유 하 게 식별 하는 문자열입니다. \<Subid>은 구독을 만드는 데 사용 된 XML 구성 파일의 \<SubscriptionId> 태그에 지정 된 문자열과 같습니다.|
|{rs \| 다시 시도-구독} \<Subid> [\<Eventsource> ...]|비활성 구독에 원격 구독 요청을 보내고 연결을 설정 하는 다시 시도 합니다. 모든 이벤트 소스를 다시 활성화 하려고 하거나 이벤트 소스를 지정 합니다. 사용할 수 없는 소스를 다시 시도 하지 않습니다. \<Subid>은 구독을 고유 하 게 식별 하는 문자열입니다. \<Subid>은 구독을 만드는 데 사용 된 XML 구성 파일의 \<SubscriptionId> 태그에 지정 된 문자열과 같습니다. \<Eventsource>는 이벤트의 원본으로 사용 되는 컴퓨터를 식별 하는 문자열입니다. \<Eventsource>는 정규화 된 도메인 이름, NetBIOS 이름 또는 IP 주소 여야 합니다.|
|{qc \| 빠른 구성} [/q: [\<Quiet>]]|구독을 만들고 번 다시 부팅 되어도 계속 해 서 수를 확인 하려면 Windows 이벤트 수집기 서비스를 구성 합니다. 이 다음 단계가 포함 됩니다.</br>1. 사용 하지 않도록 설정 된 경우 ForwardedEvents channel을 사용 하도록 설정 합니다.</br>2. Windows 이벤트 수집기 서비스를 지연 시작으로 설정 합니다.</br>3. Windows 이벤트 수집기 서비스가 실행 되 고 있지 않으면 시작 합니다.|

## <a name="options"></a>옵션

|옵션|설명|
|------|-----------|
|/f:\<형식>|표시 되는 정보의 형식을 지정 합니다. \<서식>은 XML 또는 간결 수 있습니다. 경우 <Format> 는 XML 출력은 XML 형식으로 표시 됩니다. 형식 \<> 간결 하면 출력은 이름-값 쌍에 표시 됩니다. 기본값은 Terse.|
|/c:\<>|구독 구성이 포함 된 XML 파일의 경로를 지정 합니다. 절대 또는 현재 디렉터리에 상대적 경로일 수 있습니다. 이 옵션에만 사용할 수는 **/cun** 및 **컵/** 옵션 및 다른 모든 옵션과 함께 사용할 수 없습니다.|
|/e: [\<subenabled>]|구독을 사용 하지 않도록 설정 하거나 사용 합니다. \<Subenabled> true 또는 false 일 수 있습니다. 이 옵션의 기본값은 true입니다.|
|/esa:\<Address>|이벤트 소스의 주소를 지정 합니다. \<주소>는 정규화 된 도메인 이름, NetBIOS 이름 또는 이벤트의 원본으로 사용 되는 컴퓨터를 식별 하는 IP 주소를 포함 하는 문자열입니다. 이 옵션은 함께 사용할 수는 **/ese**, **/aes**, **/res**, 또는 **/un** 및 **/up** 옵션입니다.|
|/ese: [\<srcenabled>]|이벤트 소스를 사용 하지 않도록 설정 하거나 사용 합니다. \<Srcenabled> true 또는 false 일 수 있습니다. 경우에이 옵션은 사용할 수는 **/esa** 옵션을 지정 합니다. 이 옵션의 기본값은 true입니다.|
|/aes|로 지정 된 이벤트 소스는 **/esa** 없는 구독에 포함 하는 경우. 주소 지정 하는 경우는 **/esa** 옵션 구독에 포함 되어 있으면 오류가 발생 합니다. 경우에이 옵션은 허용 된 **/esa** 옵션을 지정 합니다.|
|/res|로 지정 된 이벤트 소스를 제거는 **/esa** 옵션을 구독에 포함 되어 있습니다. 주소 지정 하는 경우는 **/esa** 옵션을 하지 않으면 구독의 일부 오류가 보고 됩니다. 경우에이 옵션은 허용 **/esa** 옵션을 지정 합니다.|
|/해제:\<사용자 이름>|으로 지정 된 이벤트 소스와 함께 사용 하는 사용자 자격 증명 지정는 **/esa** 옵션입니다. 경우에이 옵션은 허용 된 **/esa** 옵션을 지정 합니다.|
|/up:\<암호>|사용자 자격 증명에 해당 하는 암호를 지정 합니다. 경우에이 옵션은 허용 된 **/un** 옵션을 지정 합니다.|
|/d:\<Desc>|구독에 대 한 설명을 제공합니다.|
|/uri:\<uri>|구독에서 사용 되는 이벤트의 형식을 지정 합니다. \<Uri> 이벤트 소스를 고유 하 게 식별 하기 위해 이벤트 원본 컴퓨터의 주소와 결합 된 URI 문자열을 포함 합니다. 구독에서 모든 이벤트 소스 주소 URI 문자열로 사용 됩니다.|
|/cm:\<configmode>|구성 모드를 설정합니다. \<Configmode>는 일반, 사용자 지정, MinLatency 또는 Minlatency 같은 문자열 중 하나일 수 있습니다. 보통, MinLatency, MinBandwidth 모드 배달 모드, 최대 항목 배달, 하트 비트 간격 및 배달 최대 대기 시간을 설정합니다. **/dm**, **/dmi**, **/hi** 또는 **/dmlt** 옵션만 될 구성 모드가 Custom으로 설정 된 경우 지정 합니다.|
|/ex:\<> 만료|구독이 만료 되는 시간을 설정 합니다. \<만료> 표준 XML 또는 ISO8601 날짜-시간 형식으로 정의 해야 합니다. yyyy-mm-dd [. Yyyy-mm-ddthh: MM: ss [. sss] [Z]. 여기서 T는 시간 구분 기호이 고 Z는 UTC 시간을 나타냅니다.|
|/q:\<쿼리>|구독에 대 한 쿼리 문자열을 지정합니다. \<쿼리> 형식은 URI 값 마다 다를 수 있으며 구독의 모든 원본에 적용 됩니다.|
|/dia:\<언어>|쿼리 문자열에 사용 되는 언어를 정의 합니다.|
|/tn:\<>|원격 이벤트 소스에 연결 하는 데 사용 되는 전송의 이름을 지정 합니다.|
|/tp:\<가 중 포트>|원격 이벤트 소스에 연결할 때 전송에 의해 사용 되는 포트 번호를 설정 합니다.|
|/cdm:\<deliverymode.persistent>|배달 모드를 지정합니다. \<Deliverymode.persistent>는 끌어오기 또는 푸시 일 수 있습니다. 이 옵션은만 유효 하는 경우는 **/cm** 옵션 사용자 지정을 설정 합니다.|
|/dmi:\<Deliverymax>|일괄 처리 된 배달에 대 한 항목의 최대 수를 설정 합니다. 이 옵션은 유효만 경우 **/cm** Custom으로 설정 합니다.|
|/dmlt:\<경우 deliverytime>|이벤트의 일괄 처리를 제공 합니다. 최대 대기 시간을 설정 합니다. \<경우 deliverytime>는 밀리초 수입니다. 이 옵션은 유효만 경우 **/cm** Custom으로 설정 합니다.|
|/hi:\<하트 비트>|하트 비트 간격을 정의합니다. \<하트 비트>는 밀리초 수입니다. 이 옵션은 유효만 경우 **/cm** Custom으로 설정 합니다.|
|/scf:\<Content>|반환 되는 이벤트의 형식을 지정 합니다. \<콘텐츠>는 이벤트 또는 RenderedText 수 있습니다. RenderedText 값을 사용 하는 경우 이벤트 이벤트에 연결 된 지역화 된 문자열 (예: 이벤트 설명)으로 반환 됩니다. 기본값은 RenderedText 합니다.|
|/l:\<Locale>|지역화 된 문자열의 배달에 대 한 로캘을 RenderedText 형식으로 지정 합니다. \<로캘>는 언어 및 국가/지역 식별자입니다 (예: EN-US). 이 옵션은만 유효 하는 경우는 **/cf** 옵션은 RenderedText로 설정 합니다.|
|/ree: [\<Readexist>]|구독에 대해 전달 되는 이벤트를 식별 합니다. \<Readexist> true 또는 false 일 수 있습니다. 경우는 <Readexist> 가 true 이면 모든 기존 이벤트를 구독 이벤트 소스에서 읽고 있습니다. 때는 <Readexist> 가 false 이면 (도착) 이후 이벤트에만 전달 됩니다. 기본값은 true는 **/ree** 값이 없는 옵션입니다. 없으면 **/ree** 옵션을 지정한 경우 기본값은 false입니다.|
|/lf:\<로그 파일>|이벤트 원본에서 받은 이벤트를 저장 하는 데 사용 되는 로컬 이벤트 로그를 지정 합니다.|
|/pn:\<ername>|게시자 이름을 지정합니다. 이 소유 하거나에서 지정 된 로그를 가져오는 게시자 여야는 **/lf** 옵션입니다.|
|/essp:\<enableport>|원격 서비스의 서비스 사용자 이름에 포트 번호를 추가 해야를 지정 합니다. \<Enableport> true 또는 false 일 수 있습니다. 포트 번호 추가 때 <Enableport> 그렇습니다. 포트 번호를 추가 하는 경우 거부 하지 않도록 이벤트 소스에 대 한 액세스를 방지 하기 위해 몇 가지 구성이 필요할 수 있습니다.|
|/h n:\<호스트 이름>|로컬 컴퓨터의 DNS 이름을 지정합니다. 이 이름에 이벤트를 다시 밀어 원격 이벤트 소스에 사용 되 고 밀어넣기 구독에만 사용 해야 합니다.|
|/sct:\<유형>|이 원격 액세스에 대 한 자격 증명 형식을 설정합니다. \<유형>는 기본값, negotiate, digest, basic 또는 localmachine 값 중 하나 여야 합니다. 기본값은 default입니다.|
|/cun:\<comusername>|자체 사용자 자격 증명을 갖지 않는 이벤트 소스에 대해 사용할 공유 사용자 자격 증명을 설정 합니다. 이 옵션은 지정 된 경우는 **/c** 옵션을 사용자 이름 및 사용자 암호 설정을 구성 파일에서 개별 이벤트 소스는 무시 됩니다. 지정 하 여이 값을 재정의 해야 특정 이벤트 원본에 대 한 서로 다른 자격 증명을 사용 하려는 경우는 **/un** 및 **/up** 다른 명령줄에서 특정 이벤트 원본에 대 한 옵션 **ss** 명령입니다.|
|/컵:\<compassword>|공유 사용자 자격 증명에 대 한 사용자 암호를 설정합니다. Compassword>가 * (별표)로 설정 된 경우 \<콘솔에서 암호를 읽습니다. 이 옵션은만 사용할 때의 **/cun** 옵션을 지정 합니다.|
|/q: [\<Quiet>]|구성 프로시저에서 확인 메시지를 표시할지 여부를 지정 합니다. \<자동> true 또는 false 일 수 있습니다. <Quiet> 이 true 이면 구성 프로시저에서 확인 메시지를 표시 하지 않습니다. 이 옵션의 기본값은 false입니다.|

## <a name="remarks"></a>설명

> [!IMPORTANT]
> "RPC 서버를 사용할 수 없습니다." 라는 메시지가 표시 되는 경우 wecutil를 실행 하려고 할 때 Windows 이벤트 수집기 서비스 (wecsvc)를 시작 해야 합니다. Wecsvc를 시작 하려면 net을 관리자 권한 명령 프롬프트 형식에서 wecsvc를 시작 합니다.

- 구성 파일의 내용을 표시 하려면:  
  ```
  <Subscription xmlns=https://schemas.microsoft.com/2006/03/windows/events/subscription>
  <Uri>https://schemas.microsoft.com/wbem/wsman/1/windows/EventLog</Uri>
  <!-- Use Normal (default), Custom, MinLatency, MinBandwidth -->
  <ConfigurationMode>Normal</ConfigurationMode>
  <Description>Forward Sample Subscription</Description>
  <SubscriptionId>SampleSubscription</SubscriptionId>
  <Query><![CDATA[
  <QueryList>
  <Query Path=Application>
  <Select>*</Select>
  </Query>
  </QueryList>
  ]]></Query>
  <EventSources>
  <EventSource Enabled=true>
  <Address>mySource.myDomain.com</Address>
  <UserName>myUserName</UserName>
  <Password>*</Password>
  </EventSource>
  </EventSources>
  <CredentialsType>Default</CredentialsType>
  <Locale Language=EN-US></Locale>
  </Subscription>
  ```

## <a name="examples"></a>예

Sub1 구독에 대 한 구성 정보를 출력 합니다.
```
wecutil gs sub1
```
예제 출력:
```
EventSource[0]:
Address: localhost
Enabled: true
Description: Subscription 1
Uri: wsman:microsoft/logrecord/sel
DeliveryMode: pull
DeliveryMaxSize: 16000
DeliveryMaxItems: 15
DeliveryMaxLatencyTime: 1000
HeartbeatInterval: 10000
Locale:
ContentFormat: renderedtext
LogFile: HardwareEvents
```
Sub1 구독의의 런타임 상태를 표시 합니다.
```
wecutil gr sub1
```
Sub1 WsSelRg2.xml 이라는 새 XML 파일에서 등록 구성을 업데이트 합니다.
```
wecutil ss sub1 /c:%Windir%\system32\WsSelRg2.xml
```
매개 변수가 여러 개이면 sub2 라는 등록 구성을 업데이트 합니다.
```
wecutil ss sub2 /esa:myComputer /ese /un:uname /up:* /cm:Normal
```
ForwardedEvents 로그에 mySource.myDomain.com에서 원격 컴퓨터의 Windows Vista 애플리케이션 이벤트 로그에서 이벤트를 전달 하는 구독 만들기 (구성 파일의 예는 설명 참조).
```
wecutil cs subscription.xml
```
Sub1 라는 구독을 삭제 합니다.
```
wecutil ds sub1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
