---
title: bitsadmin getpriority
description: '**Bitsadmin getpriority**에 대 한 Windows 명령 항목으로, 지정 된 작업의 우선 순위를 검색 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: b27829a0fb852abb88c88a65e61e8d7693ca2df2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850546"
---
# <a name="bitsadmin-getpriority"></a>bitsadmin getpriority

지정된 된 작업의 우선 순위를 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getpriority <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="remarks"></a>주의

이 명령의 우선 순위는 다음과 같을 수 있습니다.

- **전경색**

- **최고**

- **일반적**

- **거의**

- **없습니다**

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 우선 순위를 검색 *myDownloadJob*합니다.

```
C:\>bitsadmin /getpriority myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
