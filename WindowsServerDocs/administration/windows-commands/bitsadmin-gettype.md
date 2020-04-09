---
title: bitsadmin gettype
description: 지정 된 작업의 작업 유형을 검색 하는 **bitsadmin gettype**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 66a1fc5b0478e1eec26557dc9a7f76d50abcb8b6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850446"
---
# <a name="bitsadmin-gettype"></a>bitsadmin gettype

지정된 된 작업의 작업 유형을 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /gettype <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="output"></a>출력

출력 값은 다음과 같습니다.

| 형식 | 설명 |
| --------------- | ----------- |
| 다운로드 | 작업은 다운로드입니다. |
| 업로드 | 업로드가 작업입니다. |
| 업로드-회신 | 작업은 업로드 회신입니다. |
| 알 수 없음 | 작업의 유형을 알 수 없습니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 작업 유형을 검색 *myDownloadJob*합니다.

```
C:\>bitsadmin /gettype myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)