---
title: ntcmdprompt
description: '**Command.com**대신 명령 인터프리터를 실행 하 고, TSR (tsr)을 실행 하거나, MS-DOS 응용 프로그램 내에서 명령 프롬프트를 시작한 후 명령 **Cmd.exe**인터프리터를 실행 하는 ntcmdprompt 명령에 대 한 참조 문서입니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0063bdbb-dc2b-41c4-99ee-b011603aaa86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a70a8cfdbe6e37bfb8d90bed23e961d100843506
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925341"
---
# <a name="ntcmdprompt"></a>ntcmdprompt

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

실행 명령 인터프리터 **Cmd.exe**, 보다는 **Command.com**, 종료 및 최신 상주 (TSR) 실행 후 또는 MS-DOS 애플리케이션 내에서 명령 프롬프트를 시작 합니다.

## <a name="syntax"></a>구문

```
ntcmdprompt
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- **Command.com** 를 실행 하는 경우 명령 기록의 **doskey** 표시와 같은 **Cmd.exe**의 일부 기능을 사용할 수 없습니다. TSR (TSR)을 시작한 후에 명령 인터프리터를 실행 하거나 MS-DOS 기반 응용 프로그램 내에서 명령 프롬프트를 시작한 후에 **Cmd.exe** 명령 인터프리터를 실행 하는 것을 선호 하는 경우 **ntcmdprompt** 명령을 사용할 수 있습니다. 그러나 염두 하 TSR 하지 못할 사용 하기 위해 실행 하는 경우 **Cmd.exe**합니다. **Config.nt** 파일 또는 응용 프로그램의 Pif (프로그램 정보 파일)에 해당 하는 사용자 지정 시작 파일에 **ntcmdprompt** 명령을 포함할 수 있습니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
