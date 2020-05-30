---
title: logman 삭제
description: 기존 데이터 수집기를 삭제 하는 logman delete 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8f3b2422-3dce-4fb4-adbb-8536b1d7da2b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 18739f3d7ab5af38dbe369e45aca8393ba3a3152
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222941"
---
# <a name="logman-delete"></a>logman 삭제

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기존 데이터 수집기를 삭제 합니다.

## <a name="syntax"></a>구문

```
logman delete <[-n] <name>> [options]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| -s`<computer name>` | 지정 된 원격 컴퓨터에서 명령을 수행 합니다. |
| -config`<value>` | 명령 옵션을 포함 하는 설정 파일을 지정 합니다. |
| [-n]`<name>` | 대상 개체의 이름입니다. |
| -ets | 는 이벤트 추적 세션에 명령을 저장 하거나 일정을 예약 하지 않고 직접 보냅니다. |
| -[-] u`<user [password]>` | 사용자 계정으로 실행을 지정합니다. 암호에 대해를 입력 하면 \* 암호를 묻는 메시지가 생성 됩니다. 암호는 암호 프롬프트에 입력할 때 표시되지 않습니다. |
| /? | 도움말 상황에 맞는 표시 합니다. |

### <a name="examples"></a>예

데이터 수집기 *perf_log*를 삭제 하려면 다음을 입력 합니다.

```
logman delete perf_log
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [logman 명령](logman.md)
