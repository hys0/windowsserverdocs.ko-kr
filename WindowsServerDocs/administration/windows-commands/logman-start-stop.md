---
title: logman start 및 logman stop
description: Logman start 및 logman stop 명령에 대 한 참조 항목으로, 데이터 수집기를 시작 하 고 시작 시간을 수동으로 설정 하거나 데이터 수집기 집합을 중지 하 고 종료 시간을 수동으로 설정 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a40006a1-876e-474b-aaf1-f365c730deea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: db0111c4f58f0a28ad76affd3e4d8e24d4a927c2
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222912"
---
# <a name="logman-start-and-logman-stop"></a>logman start 및 logman stop

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**Logman start** 명령은 데이터 수집기를 시작 하 고 시작 시간을 수동으로 설정 합니다. **Logman stop** 명령은 데이터 수집기 집합을 중지 하 고 종료 시간을 수동으로 설정 합니다.

## <a name="syntax"></a>구문

```
logman start <[-n] <name>> [options]
logman stop <[-n] <name>> [options]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| -s`<computer name>` | 지정된 된 원격 컴퓨터에서 명령을 수행 합니다. |
| -config`<value>` | 명령 옵션을 포함 하는 설정 파일을 지정 합니다. |
| [-n]`<name>` | 대상 개체의 이름을 지정 합니다. |
| -ets | 저장 하거나 예약 하지 않고 직접 이벤트 추적 세션에 명령을 보냅니다. |
| -으로 | 요청 된 작업을 비동기적으로 수행 합니다. |
| -? | 도움말 상황에 맞는 표시 합니다. |

### <a name="examples"></a>예

데이터 수집기 *perf_log*시작 하려면 원격 컴퓨터 *server_1*에서 다음을 입력 합니다.

```
logman start perf_log -s server_1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [logman 명령](logman.md)
