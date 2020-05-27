---
title: logman 만들기
description: 카운터, 추적, 구성 데이터 수집기 또는 API를 만드는 logman create 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 972f0126-7bc4-4b14-9265-062864f3ffd4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1d4bffd68d5b74d1d6f36750967911dfec3f299a
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820593"
---
# <a name="logman-create"></a>logman 만들기

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

카운터, 추적, 구성 데이터 수집기 또는 API를 만듭니다.

## <a name="syntax"></a>구문

```
logman create <counter | trace | alert | cfg | api> <[-n] <name>> [options]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| [logman 카운터 만들기](logman-create-counter.md) | 카운터 데이터 수집기를 만듭니다. |
| [logman 추적 만들기](logman-create-trace.md) | 추적 데이터 수집기를 만듭니다. |
| [logman 경고 만들기](logman-create-alert.md) | 경고 데이터 수집기를 만듭니다. |
| [logman cfg 만들기](logman-create-cfg.md) | 구성 데이터 수집기를 만듭니다. |
| [logman api 만들기](logman-create-api.md) | API 추적 데이터 수집기를 만듭니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)