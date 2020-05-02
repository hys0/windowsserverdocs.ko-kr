---
title: bitsadmin info
description: 지정 된 작업에 대 한 요약 정보를 표시 하는 bitsadmin info 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 904f70c82ab4bcc4fb25f759898674cc719b1954
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717434"
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
| /verbose | (선택 사항) 각 작업에 대 한 자세한 정보를 제공 합니다. |

## <a name="examples"></a>예

이름이 *Mydownloadjob*인 작업에 대 한 정보를 검색 하려면:

```
bitsadmin /info myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin info](bitsadmin-info.md)
