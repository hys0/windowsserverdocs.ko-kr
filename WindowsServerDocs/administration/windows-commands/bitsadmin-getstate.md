---
title: bitsadmin getstate
description: '**Bitsadmin getstate**에 대 한 Windows 명령 항목으로, 지정 된 작업의 상태를 검색 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1252d6cf-14ca-44df-beb2-930ff011f297
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 43cd8c8e614cce65f55b16fc5395b1d37de0cf95
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850466"
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
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="output"></a>출력

출력 값은 다음과 같습니다.

| 상태 | 설명 |
| --------------- | ----------- |
| 대기 | 작업 실행 되기를 기다리고 있습니다. |
| Connecting | 비트에는 서버에 연결 됩니다. |
| 전달 | 비트 데이터를 전송 합니다. |
| 양도할 | BITS가 작업의 모든 파일을 전송 했습니다. |
| Suspended | 작업 일시 중지 됩니다. |
| 오류 | 복구할 수 없는 오류가 발생 했습니다. 전송은 다시 시도 하지 않습니다. |
| Transient_Error | 복구 가능한 오류가 발생 했습니다. 최소 다시 시도 간격에서 만료 되 면 전송 재시도 합니다. |
| 확인 | 작업이 완료 되었습니다. |
| Canceled | 작업이 취소되었습니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 상태를 검색 *myDownloadJob*합니다.

```
C:\>bitsadmin /getstate myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
