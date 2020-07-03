---
title: irftp
description: 적외선 링크를 통해 파일을 전송 하는 irftp 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e15c60a7-546d-4e9f-9871-43aaa1b569d6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 92bb484650245555597121c8b6f6378d3c09209c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924347"
---
# <a name="irftp"></a>irftp

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

적외선 연결을 통해 파일을 전송합니다.

> [!IMPORTANT]
> 적외선 연결을 통해 통신 하는 장치에 적외선 기능이 사용 하도록 설정 되어 있고 제대로 작동 하는지 확인 합니다. 또한 장치 간에 적외선 연결이 설정 되어 있는지 확인 합니다.

## <a name="syntax"></a>구문

```
irftp [<drive>:\] [[<path>] <filename>] [/h][/s]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<drive>:\` | 적외선 연결을 통해 전송 하려는 파일이 있는 드라이브를 지정 합니다. |
| `[path]<filename>` | 파일의 이름 또는 집합 적외선 연결을 통해 전송 하려는 경우 파일의 위치를 지정 합니다. 파일 집합을 지정 하면 각 파일에 대 한 전체 경로 지정 해야 합니다. |
| /h | 숨김된 모드를 지정합니다. 숨김된 모드를 사용 하면 무선 연결 대화 상자를 표시 하지 않고 파일 전송 됩니다. |
| /s | 명령줄을 사용 하 여 드라이브, 경로 및 파일 이름을 지정 하지 않고 전송 하려는 파일이 나 파일 집합을 선택할 수 있도록 **무선 연결** 대화 상자를 엽니다. **무선 연결** 대화 상자는 매개 변수 없이이 명령을 사용 하는 경우에도 열립니다. |

### <a name="examples"></a>예

적외선 링크를 통해 *c:\example.txt* 을 보내려면 다음을 입력 합니다.

```
irftp c:\example.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
