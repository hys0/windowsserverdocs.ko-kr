---
title: mode
description: 시스템 상태를 표시 하거나, 시스템 설정을 변경 하거나, 포트 또는 장치를 다시 설정 하는 모드 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b59b04f2-b41d-42df-b5be-19c3721445b1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5794b80f7457b133d3e5b599cb12613469ad58eb
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936054"
---
# <a name="mode"></a>mode

시스템 상태를 표시 하 고, 시스템 설정을 변경 또는 포트 또는 디바이스를 다시 구성 합니다. 매개 변수 없이 사용 하는 경우 **모드** 콘솔 및 사용 가능한 COM 디바이스 제어할 수 있는 모든 특성을 표시 합니다.

## <a name="serial-port"></a>직렬 포트

직렬 통신 포트를 구성 하 고 출력 핸드셰이크를 설정 합니다.

### <a name="syntax"></a>구문

```
mode com<m>[:] [baud=<b>] [parity=<p>] [data=<d>] [stop=<s>] [to={on|off}] [xon={on|off}] [odsr={on|off}] [octs={on|off}] [dtr={on|off|hs}] [rts={on|off|hs|tg}] [idsr={on|off}]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수  | 설명 |
| ---------- | ----------- |
| `com<m>[:]` | Async Prncnfg.vbshronous 통신 포트 번호를 지정합니다. |
| `baud=<b>`  | 비트 / 초 전송 속도 지정합니다. 유효한 값은 다음과 같습니다.<ul><li>**11** -110 보드</li><li>**15** -150 전송</li><li>**30** -300 보드</li><li>**60** -600 전송</li><li>**12** -1200 보드</li><li>**24** -2400 전송</li><li>**48** -4800 전송</li><li>**96** -9600 전송</li><li>**19** -19200 전송</li></ul> |
| `parity=<p>` | 시스템 전송 오류를 검사 패리티 비트를 사용 하는 방법을 지정 합니다. 유효한 값은 다음과 같습니다.<ul><li>**n** -없음</li><li>**e** -짝수 (기본값)</li><li>**o** -홀수</li><li>**m** -표시</li><li>**s** -space</li></ul>모든 장치에서 **m** 또는 **s** 매개 변수 사용을 지 원하는 것은 아닙니다. |
| `data=<d>` | 문자에서 데이터 비트의 수를 지정합니다. 유효한 값의 범위는 **5** 에서 **8**사이입니다. 기본값은 **7**입니다. 모든 장치에서 **5** 와 **6**값을 지원 하지는 않습니다. |
| `stop=<s>` | 문자 끝을 정의 하는 정지 비트 수 (1, **1.5**또는 **2** **)** 를 지정 합니다. 전송 속도가 **110**인 경우 기본값은 **2**입니다. 그렇지 않으면 기본값은 **1**입니다. 모든 장치에서 **1.5**값을 지원 하지는 않습니다. |
| `to={on | off}` | 장치에서 무한 시간 제한 처리를 사용 하는지 여부를 지정 합니다. 기본값은 **off**입니다. **에서** 이 옵션을 설정 하면 장치가 호스트 또는 클라이언트 컴퓨터에서 응답을 받기 위해 대기 하지 않습니다. |
| `xon={on | off}` | 시스템이 XON/XOFF 프로토콜을 허용 하는지 여부를 지정 합니다. 이 프로토콜은 직렬 통신에 대 한 흐름 제어를 제공 하 여 안정성을 향상 하지만 성능을 저하 시킵니다. |
| `odsr={on | off}` | 시스템이 DSR (Data Set Ready) 출력 핸드셰이크를 켤 지 여부를 지정 합니다. |
| `octs={on | off}` | 시스템에서 CTS (Clear to Send) 출력 핸드셰이크를 켤 지 여부를 지정 합니다. |
| `dtr={on | off | hs}` | 시스템이 DTR (Data Terminal Ready) 출력 핸드셰이크를 켤 지 여부를 지정 합니다. 이 값을 **on** 모드로 설정 하면 터미널에서 데이터를 보낼 준비가 되었음을 표시 하는 상수 신호를 제공 합니다. 이 값을 **hs** 모드로 설정 하면 두 터미널 간의 핸드셰이크 신호를 제공 합니다. |
| `rts={on | off | hs | tg}` | 시스템이 RTS (Request to Send) 출력 핸드셰이크를 켤 지 여부를 지정 합니다. 이 값을 **on** 모드로 설정 하면 터미널에서 데이터를 보낼 준비가 되었음을 표시 하는 상수 신호를 제공 합니다. 이 값을 **hs** 모드로 설정 하면 두 터미널 간의 핸드셰이크 신호를 제공 합니다. 이 값을 **tg** 모드로 설정 하면 준비 됨 상태와 준비 되지 않음 상태 사이를 전환 하는 방법이 제공 됩니다. |
| `idsr={on | off}` | 시스템이 DSR 민감도를 켤 지 여부를 지정 합니다. DSR 핸드셰이킹을 사용 하려면이 옵션을 설정 해야 합니다.
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="device-status"></a>디바이스 상태

지정 된 장치의 상태를 표시 합니다. 매개 변수 없이 사용 하는 경우 **모드** 시스템에 설치 된 모든 장치의 상태를 표시 합니다.

### <a name="syntax"></a>구문

```
mode [<device>] [/status]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<device>` | 상태를 표시 하려는 디바이스의 이름을 지정 합니다. 표준 이름에는 LPT1: ~ LPT3:, COM1: ~ COM9: 및 CON이 포함 됩니다. |
| /status | 리디렉션된 모든 병렬 프린터의 상태를 요청 합니다. **/Sta** 를이 명령의 축약 된 버전으로 사용할 수도 있습니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="redirect-printing"></a>인쇄 리디렉션

프린터 출력을 리디렉션합니다. 인쇄를 리디렉션할 Administrators 그룹의 구성원 이어야 합니다.

> [!NOTE]
병렬 프린터 출력을 직렬 프린터로 보낼 수 있도록 시스템을 설정 하려면 사용 해야는 **모드** 명령을 두 번입니다. 처음에는 **모드** 를 사용 하 여 직렬 포트를 구성 해야 합니다. 두 번째로, **모드** 를 사용 하 여 병렬 프린터 출력을 첫 번째 **모드** 명령에 지정한 직렬 포트로 리디렉션해야 합니다.

### <a name="syntax"></a>구문

```
mode LPT<n>[:]=COM<m>[:]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| LPT `<n>` [:] | 구성할 LPT의 번호를 지정 합니다. 일반적으로이는 시스템에 특별 한 병렬 포트 지원이 포함 되지 않은 경우 **LTP1: ~ LTP3:를 통해**값을 제공 하는 것을 의미 합니다. 이 매개 변수는 필수입니다.|
| COM `<m>` [:] | 구성할 COM 포트를 지정 합니다. 일반적으로 시스템에 추가 COM 포트에 대 한 특수 하드웨어가 있는 경우를 제외 하 고는 **COM9:부터 COM1**의 값을 제공 하는 것을 의미 합니다. 이 매개 변수는 필수입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다.|

#### <a name="examples"></a>예

4800에서 작동 하는 직렬 프린터를 짝수 패리티를 사용 하 여 리디렉션하고 COM1 포트 (컴퓨터의 첫 번째 직렬 연결)에 연결 하려면 다음을 입력 합니다.

```
mode com1 48,e,,,b
mode lpt1=com1
```

LPT1에서 COM1으로 병렬 프린터 출력을 리디렉션하고 LPT1을 사용 하 여 파일을 인쇄 하려면 파일을 인쇄 하기 전에 다음 명령을 입력 합니다.

```
mode lpt1
```

이 명령은 c o m 1에 p t 1에서 파일을 리디렉션할 수 없습니다.

## <a name="select-code-page"></a>코드 페이지 선택

선택한 장치에 대 한 코드 페이지 정보를 구성 하거나 쿼리 합니다.

### <a name="syntax"></a>구문

```
mode <device> codepage select=<yyy>
mode <device> codepage [/status]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<device>` |코드 페이지를 선택 하려는 디바이스를 지정 합니다. 디바이스에만 유효한 이름인 CON 합니다. 이 매개 변수는 필수입니다. |
| codepage | 지정된 된 디바이스를 사용 하는 코드 페이지를 지정 합니다. 이 명령의 축약 된 버전으로 **cp** 를 사용할 수도 있습니다. 이 매개 변수는 필수입니다. |
| select =`<yyy>` | 장치에 사용할 코드 페이지 번호를 지정 합니다. 국가/지역 또는 언어에 따라 지원 되는 코드 페이지에는 다음이 포함 됩니다.<ul><li>**437:** 미국</li><li>**850:** 다국어 (라틴어 I)</li><li>**852:** 슬라브어 (라틴어 II)</li><li>**855:** 키릴 자모 (러시아어)</li><li>**857:** 터키어</li><li>**860:** 포르투갈어</li><li>**861:** 아이슬란드어</li><li>**863:** 캐나다-프랑스어</li><li>**865:** 북유럽어</li><li>**866:** 러시아어</li><li>**869:** 현대 그리스어</li></ul> 이 매개 변수는 필수입니다. |
| /status | 지정된 된 디바이스에 대해 선택한 현재 코드 페이지의 번호를 표시 합니다. **/Sta** 를이 명령의 축약 된 버전으로 사용할 수도 있습니다. **/Status**를 지정 하는지 여부에 관계 없이 **모드 코드** 페이지 명령에는 지정 된 장치에 대해 선택한 코드 페이지 수가 표시 됩니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="display-mode"></a>디스플레이 모드

명령 프롬프트 화면 버퍼의 크기를 변경 합니다.

### <a name="syntax"></a>구문

```
mode con[:] [cols=<c>] [lines=<n>]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| con [:] | 명령 프롬프트 창에 변경 내용을 적용 된다는 것을 나타냅니다. 이 매개 변수는 필수입니다. |
| cols =`<c>` | 명령 프롬프트 화면 버퍼에서 열 수를 지정합니다. 기본 설정은 80 열 이지만이 값을 임의의 값으로 설정할 수 있습니다. 기본값을 사용 하지 않는 경우 일반적인 값은 40 및 135 열입니다. 비표준 값을 사용 하면 명령 프롬프트 앱 문제가 발생할 수 있습니다. |
| 줄 =`<n>` | 명령 프롬프트 화면 버퍼에서 줄의 수를 지정합니다. 기본값은 25 이지만이 값을 임의의 값으로 설정할 수 있습니다. 기본값을 사용 하지 않는 경우 다른 일반적인 값은 50 줄입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="typematic-rate"></a>입력 rate

키보드 입력 rate를 설정 합니다. 입력 속도는 키보드에서 키를 누를 때 Windows에서 문자를 반복 하는 속도입니다.

> [!NOTE]
> 일부 키보드는이 명령을 인식 하지 못합니다.

### <a name="syntax"></a>구문

```
mode con[:] [rate=<r> delay=<d>]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| con [:] | 키보드를 지정 합니다. 이 매개 변수는 필수입니다. |
| rate =`<r>` | 키를 누르고 있을 때 화면에 문자가 반복 되는 속도 지정 합니다. 기본값은 IBM 호환 키보드의 경우 초당 20 자이 고 IBM PS/2 호환 키보드의 경우 21 이지만 1에서 32 사이의 값을 사용할 수 있습니다. 이 매개 변수를 설정 하는 경우 **delay** 매개 변수도 설정 해야 합니다.|
| delay =`<d>` | 키를 눌러 문자 출력 되풀이 전에 키를 누른 후에 걸리는 시간을 지정 합니다. 기본값은 2 (. 50 초) 이지만 1 (. 25 초), 3 (75 초) 또는 4 (1 초)를 사용할 수도 있습니다. 이 매개 변수를 설정 하는 경우 **rate** 매개 변수도 설정 해야 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)