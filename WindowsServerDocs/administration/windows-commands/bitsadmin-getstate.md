---
title: bitsadmin getstate
description: 지정 된 작업의 상태를 검색 하는 bitsadmin getstate 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1252d6cf-14ca-44df-beb2-930ff011f297
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ab014c96c6d5d62232243d704d41d33cfcfc50f0
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717535"
---
# <a name="bitsadmin-getstate"></a>bitsadmin getstate

지정된 된 작업의 상태를 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getstate <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

#### <a name="output"></a>출력

반환 된 출력 값은 다음과 같을 수 있습니다.

| 시스템 상태 | 설명 |
| --------------- | ----------- |
| Queued | 작업 실행 되기를 기다리고 있습니다. |
| Connecting | 비트에는 서버에 연결 됩니다. |
| 전송 중 | 비트 데이터를 전송 합니다. |
| 양도할 | BITS가 작업의 모든 파일을 전송 했습니다. |
| 일시 중단 | 작업 일시 중지 됩니다. |
| Error | 복구할 수 없는 오류가 발생 했습니다. 전송은 다시 시도 하지 않습니다. |
| Transient_Error | 복구 가능한 오류가 발생 했습니다. 최소 다시 시도 간격에서 만료 되 면 전송 재시도 합니다. |
| 확인됨 | 작업이 완료 되었습니다. |
| 취소됨 | 작업이 취소되었습니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업 상태를 검색 하려면 다음을 수행 합니다.

```
bitsadmin /getstate myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
