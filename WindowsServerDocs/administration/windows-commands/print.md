---
title: print
description: 프린터에 텍스트 파일을 전송 하는 인쇄 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: aa2325d5-a993-4ed3-b996-255165452db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2d9cbb4230976572ddd7a26565d616c87ce2ea8d
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472318"
---
# <a name="print"></a>print

텍스트 파일을 프린터로 보냅니다. 파일은 로컬 컴퓨터의 직렬 또는 병렬 포트에 연결 된 프린터로 보낼 경우 백그라운드에서 인쇄할 수 있습니다.

> [!NOTE]
> 명령 프롬프트에서 병렬 또는 직렬 포트에 연결 된 프린터 구성, 프린터 상태 표시 또는 코드 페이지 전환에 대 한 프린터 준비를 포함 하 여 여러 구성 [작업을 수행할](mode.md)수 있습니다.

## <a name="syntax"></a>구문

```
print [/d:<printername>] [<drive>:][<path>]<filename>[ ...]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| d`<printername>` | 작업을 인쇄 하려는 프린터를 지정 합니다. 로컬로 연결 된 프린터로 인쇄 하려면 프린터가 연결 된 컴퓨터의 포트를 지정 합니다. 병렬 포트에 유효한 값은 **LPT1**, **LPT2**및 **LPT3**입니다. 직렬 포트에 대 한 유효한 값은 **COM1**, **COM2**, **COM3**및 **COM4**입니다. 해당 큐 이름 ()을 사용 하 여 네트워크 프린터를 지정할 수도 있습니다 `\\server_name\printer_name` . 프린터를 지정 하지 않으면 기본적으로 인쇄 작업이 **LPT1** 에 전송 됩니다. |
| `<drive>`: | 인쇄 하려는 파일이 있는 논리적 또는 물리적 드라이브를 지정 합니다. 인쇄 하려는 파일이 현재 드라이브에 있는 경우에는이 매개 변수가 필요 하지 않습니다. |
| `<path>` | 인쇄 하려는 파일의 위치를 지정 합니다. 인쇄 하려는 파일이 현재 디렉터리에 있는 경우에는이 매개 변수가 필요 하지 않습니다. |
| `<filename>[ ...]` | 필수 사항입니다. 인쇄 하려는 파일을 지정 합니다. 하나의 명령에 여러 파일을 포함할 수 있습니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예제

현재 디렉터리에 있는 **report.txt** 파일을 로컬 컴퓨터의 **lpt2** 에 연결 된 프린터에 보내려면 다음을 입력 합니다.

```
print /d:lpt2 report.txt
```

**C:\accounting** 디렉터리에 있는 **report.txt** 파일을 **/d: \\ copyroom** 서버의 **printer1** print 큐에 보내려면 다음을 입력 합니다.

```
print /d:\\copyroom\printer1 c:\accounting\report.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [인쇄 명령 참조](print-command-reference.md)

- [모드 명령](mode.md)