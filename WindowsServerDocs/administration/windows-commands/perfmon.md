---
title: perfmon
description: 특정 독립 실행형 모드에서 Windows 안정성 및 성능 모니터를 시작 하는 perfmon 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9a8d5eca-8473-463e-a6e0-7bbd590b18e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/25/2018
ms.openlocfilehash: 5beaa1692f3fc4aa66eae81069f0ead5839d22e3
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922835"
---
# <a name="perfmon"></a>perfmon

특정 독립 실행형 모드에서 Windows 안정성 및 성능 모니터를 시작 합니다.

## <a name="syntax"></a>구문

```
perfmon </res|report|rel|sys>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| /res | 리소스 뷰를 시작 합니다. |
| /report | 시스템 진단 데이터 수집기 집합을 시작 하 고 결과에 대 한 보고서를 표시 합니다. |
| /rel | 안정성 모니터를 시작 합니다. |
| /sys | 성능 모니터를 시작 합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [Windows 성능 모니터](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc749154(v%3dws.11))
