---
title: bitsadmin resume
description: '**Bitsadmin 다시 시작**에 대 한 Windows 명령 항목으로, 전송 큐에서 새 작업 또는 일시 중단 된 작업을 활성화 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c7540a9-a11a-4910-923a-2a2a61cbf11d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e81bd80232cd4ec8fbba70c86cd97bb9695680f8
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123075"
---
# <a name="bitsadmin-resume"></a>bitsadmin resume

전송 큐에 새로운 또는 일시 중단 된 작업을 활성화합니다.

## <a name="syntax"></a>구문

```
bitsadmin /resume <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

다음 예제에서는 라는 작업을 다시 시작 *myDownloadJob*합니다.

```
C:\>bitsadmin /resume myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)