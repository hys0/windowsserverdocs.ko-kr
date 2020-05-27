---
title: logman
description: Logman 명령에 대 한 참조 항목으로, 이벤트 추적 세션 및 성능 로그를 만들고 관리 하며 명령줄에서 성능 모니터의 많은 기능을 지원 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 574a5203-5b3b-4759-a678-f26d00dde447
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 44b5e134440d71eed61ca8e03739abcc962df1f9
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820553"
---
# <a name="logman"></a>logman

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이벤트 추적 세션과 성능 로그를 만들고 관리하며 명령줄에서 성능 모니터의 많은 기능을 지원합니다.

## <a name="syntax"></a>구문

```
logman [create | query | start | stop | delete| update | import | export | /?] [options]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| [logman create](logman-create.md) | 카운터, 추적, 구성 데이터 수집기 또는 API를 만듭니다. |
| [logman query](logman-query.md) | 데이터 수집기 속성을 쿼리 합니다. |
| [logman start &#124; stop](logman-start-stop.md) | 데이터 수집을 시작 하거나 중지 합니다. |
| [logman delete](logman-delete.md) | 기존 데이터 수집기를 삭제 합니다. |
| [logman update](logman-update.md) | 기존 데이터 수집기의 속성을 업데이트 합니다. |
| [logman import &#124; export](logman-import-export.md) | XML 파일에서 데이터 수집기 집합을 가져오거나 데이터 수집기 집합을 XML 파일로 내보냅니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)