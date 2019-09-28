---
title: ntcmdprompt
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0063bdbb-dc2b-41c4-99ee-b011603aaa86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5fef1641bf1b48bd1fe4aaf284ed309ab4d4d5f1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372672"
---
# <a name="ntcmdprompt"></a>ntcmdprompt

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

실행 명령 인터프리터 **Cmd.exe**, 보다는 **Command.com**, 종료 및 최신 상주 (TSR) 실행 후 또는 MS-DOS 응용 프로그램 내에서 명령 프롬프트를 시작 합니다.
## <a name="syntax"></a>구문
```
ntcmdprompt
```
### <a name="parameters"></a>매개 변수

| 매개 변수 |             설명              |
|-----------|--------------------------------------|
|    /?     | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="remarks"></a>설명
- 때 **Command.com** 실행의 일부 기능 **Cmd.exe**, 와 같은 **doskey** 명령 기록의 표시를 사용할 수 없습니다. 실행 하려는 경우는 **Cmd.exe** MS-DOS 기반 응용 프로그램 내에서 명령 프롬프트를 시작 하거나 종료와 최신 상주 (TSR) 시작 하는 한 후 명령 인터프리터를 여는 **ntcmdprompt** 명령입니다. 그러나 염두 하 TSR 하지 못할 사용 하기 위해 실행 하는 경우 **Cmd.exe**합니다. **Config.nt** 파일 또는 응용 프로그램의 Pif (프로그램 정보 파일)에 해당 하는 사용자 지정 시작 파일에 **ntcmdprompt** 명령을 포함할 수 있습니다.
  ## <a name="examples"></a>예
  **Config.nt** 파일 또는 Pif에 지정 된 구성 시작 파일에 **ntcmdprompt** 를 포함 하려면 **ntcmdprompt** 를 입력 합니다.
  ## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)

