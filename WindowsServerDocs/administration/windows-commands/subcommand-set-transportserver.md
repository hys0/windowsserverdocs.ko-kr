---
title: 하위 명령 집합-서버
description: 전송 서버에 대 한 구성 설정을 설정 하는 하위 명령 집합-서버에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7863225c-f4b2-4cd0-b929-78a454bef249
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4c73567c58ff920b67f6e37a6f284d58517f5565
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833816"
---
# <a name="subcommand-set-transportserver"></a>하위 명령: 집합 TransportServer

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

전송 서버에 대 한 구성 설정을 지정 합니다.

## <a name="syntax"></a>구문
```
wdsutil [Options] /Set-TransportServer [/Server:<Server name>]
     [/ObtainIpv4From:{Dhcp | Range}]
        [/start:<starting IP address>]
        [/End:<Ending IP address>]
     [/ObtainIpv6From:Range]\n\
        [/start:<start IP address>]\n\
        [/End:<End IP address>]      
     [/startPort:<starting port>
        [/EndPort:<starting port>
     [/Profile:{10Mbps | 100Mbps | 1Gbps | Custom}]    
     [/MulticastSessionPolicy]
             [/Policy:{None | AutoDisconnect | Multistream}]
                 [/Threshold:<Speed in KBps>]
                 [/StreamCount:{2 | 3}]
                 [/Fallback:{Yes | No}]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|전송 서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 전송 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다.|
|[/ ObtainIpv4From: {Dhcp &#124; 범위}]|원본 IPv4 주소를 다음과 같이 설정합니다.<p>-[/start: <IP address>] IP 주소 범위의 시작을 설정 합니다. 이 경우에 유효 옵션을 설정 하 고 이것이 필요 **범위**합니다.<br />-[/ 끝: <IP address>] IP 주소 범위의 끝을 설정 합니다. 이 경우에 유효 옵션을 설정 하 고 이것이 필요 **범위**합니다.<br />-[/Startport: <port>] 포트 범위의 시작을 설정 합니다.<br />-[/ EndPort: <port>] 포트 범위의 끝을 설정 합니다.|
|[/ ObtainIpv6From:Range]|원본 IPv6 주소를 지정합니다. Windows Server 2008 r 2에만 적용 됩니다이 옵션 및 지원 되는 유일한 값은 **범위**합니다.<p>-[/start: <IP address>] IP 주소 범위의 시작을 설정 합니다. 이 경우에 유효 옵션을 설정 하 고 이것이 필요 **범위**합니다.<br />-[/ 끝: <IP address>] IP 주소 범위의 끝을 설정 합니다. 이 경우에 유효 옵션을 설정 하 고 이것이 필요 **범위**합니다.<br />-[/Startport: <port>] 포트 범위의 시작을 설정 합니다.<br />-[/ EndPort: <port>] 포트 범위의 끝을 설정 합니다.|
|[/ 프로필: {10Mbps &#124; 100Mbps &#124; 1Gbps &#124; 사용자 지정}]|사용할 네트워크 프로필을 지정 합니다. 이 옵션은 Windows Server 2008 또는 Windows Server 2003을 실행 하는 서버에 사용할 수만 있습니다.|
|[/MulticastSessionPolicy]|멀티 캐스트 전송에 대 한 전송 설정을 구성합니다. 이 명령은 Windows Server 2008 r 2만 있습니다.<p>-[/ 정책: {None &#124; 자동 연결 끊기 &#124; Multistream}] 느린 클라이언트를 처리 하는 방법을 결정 합니다. **None** 같은 속도로 한 세션에서 모든 클라이언트를 유지할 것을 의미 합니다. **자동 연결 끊기** 즉, 모든 클라이언트는 지정 된 아래로 떨어지면 **/Threshold** 연결이 끊어집니다. **Multistream** 클라이언트에 지정 된 대로 여러 세션으로 구분 됩니다 의미 **/StreamCount**합니다.<br />-[/ 임계값:<Speed in KBps>] 최소 전송 속도를 KBps 단위로 설정 하는 **/Policy:AutoDisconnect**합니다. 이 속도 아래로 떨어지면 클라이언트가 멀티 캐스트 전송에서 연결이 끊어집니다.<br />-[/ StreamCount: {2 및 #124; 3을 (를)] [/ 대체 (fallback): {예 & #124; No}]에 대 한 세션 수를 결정 **/Policy:Multistream**합니다. **2** (고속 및 저속) 두 개의 세션을 의미 하 고 **3** 3 개의 세션 느린, 중간, fast ()를 의미 합니다.<br />-[/ 대체 (fallback): {예 &#124; No}] 결정 클라이언트 tha 연결이 끊어진를 계속할지 여부를 전송 (클라이언트에서 지 원하는) 경우에 다른 메서드를 사용 하 여 합니다. WDS 클라이언트를 사용 하는 경우 컴퓨터 유니캐스트도 대체 됩니다. Wdsmcast.exe 대체 메커니즘을 지원 하지 않습니다. 이 옵션을 지원 하지 않는 클라이언트에도 적용 됩니다 **Multistream**합니다. 이 경우 컴퓨터는 느린 전송 세션으로 이동 하는 대신 다른 메서드로 다시 대체 됩니다.|
## <a name="examples"></a><a name=BKMK_examples></a>예와
서버에 대 한 IPv4 주소 범위를 설정 하려면 다음을 입력 합니다.
```
wdsutil /Set-TransportServer /ObtainIpv4From:Range /start:239.0.0.1 /End:239.0.0.100
```
서버에 대 한 IPv4 주소 범위, 포트 범위 및 프로필을 설정 하려면 다음을 입력 합니다.
```
wdsutil /Set-TransportServer /Server:MyWDSServer /ObtainIpv4From:Range /start:239.0.0.1 /End:239.0.0.100 /startPort:12000 /EndPort:50000 /Profile:10mbps
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
[TransportServer 사용 안 함 명령을 사용 하 여](using-the-disable-transportserver-command.md)
[사용 TransportServer 명령을 사용 하 여](using-the-enable-transportserver-command.md)
[get TransportServer 명령을 사용 하 여](using-the-get-transportserver-command.md)
[하위 명령: 시작 TransportServer](subcommand-start-transportserver.md)
[하위 명령: TransportServer 중지](subcommand-stop-transportserver.md)
