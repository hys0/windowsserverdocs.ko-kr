---
title: logman 쿼리
description: 데이터 수집기 또는 데이터 수집기 집합 속성을 쿼리 하는 logman 쿼리 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1116a0f0-5415-4369-a045-12f79f8f66de
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ea436ec676ee8097a0df80467744b76f2deeca42
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922317"
---
# <a name="logman-query"></a>logman 쿼리

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

데이터 수집기 또는 데이터 수집기 집합 속성을 쿼리 합니다.

## <a name="syntax"></a>구문

```
logman query [providers|Data Collector Set name] [options]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| -s`<computer name>` | 지정된 된 원격 컴퓨터에서 명령을 수행 합니다. |
| -config`<value>` | 명령 옵션을 포함 하는 설정 파일을 지정 합니다. |
| [-n]`<name>` | 대상 개체의 이름입니다. |
| -ets | 는 이벤트 추적 세션에 명령을 저장 하거나 일정을 예약 하지 않고 직접 보냅니다. |
| /? | 도움말 상황에 맞는 표시 합니다. |

### <a name="examples"></a>예

대상 시스템에 구성 된 모든 데이터 수집기 집합을 나열 하려면 다음을 입력 합니다.

```
logman query
```

*Perf_log*이라는 데이터 수집기 집합에 포함 된 데이터 수집기를 나열 하려면 다음을 입력 합니다.

```
logman query perf_log
```

대상 시스템에서 사용 가능한 데이터 수집기 공급자를 모두 나열 하려면 다음을 입력 합니다.

```
logman query providers
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [logman 명령](logman.md)
