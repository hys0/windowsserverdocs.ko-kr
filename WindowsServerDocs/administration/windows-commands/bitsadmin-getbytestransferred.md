---
title: bitsadmin getbytestransferred
description: 지정 된 작업에 대해 전송 된 바이트 수를 검색 하는 **bitsadmin getbytestransferred**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 47bbf184-e06f-4be0-b2ba-d32b10d82002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 957b3e60bf8a5e41b3964f4d762633472606654d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850776"
---
# <a name="bitsadmin-getbytestransferred"></a>bitsadmin getbytestransferred

지정 된 작업에 대해 전송 된 바이트 수를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getbytestransferred <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예에서는 이름이 *Mydownloadjob*인 작업에 대해 전송 된 바이트 수를 검색 합니다.

```
C:\>bitsadmin /getbytestransferred myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)