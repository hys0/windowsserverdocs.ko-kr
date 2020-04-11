---
title: bitsadmin info
description: 지정 된 작업에 대 한 요약 정보를 표시 하는 **bitsadmin 정보**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 20b8358caba3e0c07b0c985cb24e8f7bde43b06c
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123111"
---
# <a name="bitsadmin-info"></a>bitsadmin info

지정된 된 작업에 대 한 요약 정보를 표시 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /info <job> [/verbose]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| /verbose | (선택 사항) 각 작업에 대 한 자세한 정보를 제공 합니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

명명 된 작업에 대 한 정보를 검색 하는 다음 예제에서는 *myDownloadJob*합니다.

```
C:\>bitsadmin /info myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin info](bitsadmin-info.md)