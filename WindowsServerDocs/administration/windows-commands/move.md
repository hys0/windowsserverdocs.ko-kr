---
title: 이동
description: 하나 이상의 파일을 한 디렉터리에서 다른 디렉터리로 이동 하는 move 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fde290a8-d385-450f-8987-ee837fed667d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4cc1f7c04a54b78da7b24dbedad225a7326766cd
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936313"
---
# <a name="move"></a>이동

한 디렉터리에서 하나 이상의 파일을 다른 디렉터리로 이동합니다.

> [!IMPORTANT]
> 암호화 된 파일을 파일 시스템 암호화 (EFS) 결과를 지원 하지 않는 볼륨으로 이동 하면 오류가 발생 합니다. 먼저 파일의 암호를 해독 하거나 EFS를 지 원하는 볼륨으로 이동 해야 합니다.

## <a name="syntax"></a>구문

```
move [{/y|-y}] [<source>] [<target>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| /y | 기존 대상 파일을 덮어쓸 것인지 확인 하는 메시지를 표시 하지 않습니다. 이 매개 변수는/Z 환경 변수에 미리 설정할 수 있습니다. **-Y** 매개 변수를 사용 하 여이 사전 설정을 재정의할 수 있습니다. 기본값은 명령을 일괄 처리 스크립트 내에서 실행 하지 않는 한 파일을 덮어쓰기 전에 확인 하는 것입니다. |
| -y | 기존 대상 파일을 덮어쓸지 묻는 메시지를 표시 하기 시작 합니다. |
| `<source>` | 이동할 파일의 경로와 이름을 지정 합니다. 디렉터리를 이동 하거나 이름을 바꾸려면 *원본은* 현재 디렉터리 경로 및 이름 이어야 합니다. |
| `<target>` | 경로 파일을 이동 하는 이름을 지정 합니다. 디렉터리를 이동 하거나 이름을 바꾸려면 *대상이* 원하는 디렉터리 경로 및 이름 이어야 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

확장명이 .xls 인 모든 파일을 *\Data* 디렉터리에서 *\ Second_Q \reports* 디렉터리로 이동 하려면 다음을 입력 합니다.

```
move \data\*.xls \second_q\reports\
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
