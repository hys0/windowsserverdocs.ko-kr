---
title: bitsadmin gettype
description: 지정 된 작업의 작업 유형을 검색 하는 bitsadmin gettype 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c7224add1b503d9ec50e84879a47442c12447e5d
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926641"
---
# <a name="bitsadmin-gettype"></a>bitsadmin gettype

지정된 된 작업의 작업 유형을 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /gettype <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

#### <a name="output"></a>출력

반환 된 출력 값은 다음과 같을 수 있습니다.

| 형식 | 설명 |
| --------------- | ----------- |
| 다운로드 | 작업은 다운로드입니다. |
| 업로드 | 업로드가 작업입니다. |
| 업로드-회신 | 작업은 업로드 회신입니다. |
| 알 수 없음 | 작업의 유형을 알 수 없습니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업에 대 한 작업 유형을 검색 하려면:

```
bitsadmin /gettype myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
