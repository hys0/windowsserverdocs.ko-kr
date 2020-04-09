---
title: bitsadmin getcompletiontime
description: '**Bitsadmin getcompletiontime**에 대 한 Windows 명령 항목-작업에서 데이터 전송을 완료 한 시간을 검색 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7a4b3c1c-9832-4724-86b2-cce3c01bfa28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5408e7e8c35135601a4a0af0ab7e9c55cea4c8dd
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850756"
---
# <a name="bitsadmin-getcompletiontime"></a>bitsadmin getcompletiontime

작업에서 데이터 전송을 완료 한 시간을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getcompletiontime <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 *Mydownloadjob* 이라는 작업에서 데이터 전송을 완료 한 시간을 검색 합니다.

```
C:\>bitsadmin /getcompletiontime myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)