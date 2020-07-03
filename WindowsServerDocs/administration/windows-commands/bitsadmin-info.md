---
title: bitsadmin info
description: 지정 된 작업에 대 한 요약 정보를 표시 하는 bitsadmin info 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0b9a284ee1e0ab8501f0fb6bc3417ca399996a08
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926569"
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
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| /verbose | 선택 사항입니다. 각 작업에 대 한 자세한 정보를 제공 합니다. |

## <a name="examples"></a>예

이름이 *Mydownloadjob*인 작업에 대 한 정보를 검색 하려면:

```
bitsadmin /info myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin info](bitsadmin-info.md)
