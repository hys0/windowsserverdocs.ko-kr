---
title: bitsadmin 캐시 및 setlimit
description: '**Bitsadmin 캐시 및 setlimit**에 대 한 Windows 명령 항목으로, 캐시 크기 제한을 설정 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 746ee0b69da8f5bd22fec2ccbd432126cc25d94d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850876"
---
# <a name="bitsadmin-cache-and-setlimit"></a>bitsadmin 캐시 및 setlimit

캐시 크기 제한을 설정합니다.

## <a name="syntax"></a>구문

```
bitsadmin /cache /setlimit percent
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| percent | 전체 하드 디스크 공간의 백분율로 정의 된 캐시 제한입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 캐시 크기 50%를 제한합니다.

```
C:\>bitsadmin /cache /setlimit 50
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)