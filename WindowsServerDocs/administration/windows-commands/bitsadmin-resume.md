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
ms.openlocfilehash: 0a3f464ba00c5cc233c42a40c063372dc0d584e9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849756"
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

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 라는 작업을 다시 시작 *myDownloadJob*합니다.

```
C:\>bitsadmin /resume myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)