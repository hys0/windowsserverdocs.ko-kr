---
title: bitsadmin listfiles
description: 지정 된 작업의 파일을 나열 하는 bitsadmin listfiles 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ad0d1eaa-3bd8-45e5-8f72-4da7366f0d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6826c1ec2f624a06d11fedcb8ca9f14d86b7ec27
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717413"
---
# <a name="bitsadmin-listfiles"></a>bitsadmin listfiles

지정된 된 작업의 파일을 나열 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /listfiles <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

이름이 *Mydownloadjob*인 작업에 대 한 파일 목록을 검색 하려면 다음을 수행 합니다.

```
bitsadmin /listfiles myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
