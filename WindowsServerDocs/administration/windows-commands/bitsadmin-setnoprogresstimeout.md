---
title: bitsadmin setnoprogresstimeout
description: 일시적인 오류가 발생 한 후 서비스에서 파일을 전송 하려고 시도 하는 시간 (초)을 설정 하는 bitsadmin setnoprogresstimeout 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7fac50d9-cc6b-46a4-a96f-fab751ee1756
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9bb7ac4cd03148c533aa27f62a1c9770465673a5
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927677"
---
# <a name="bitsadmin-setnoprogresstimeout"></a>bitsadmin setnoprogresstimeout

첫 번째 일시적인 오류가 발생 한 후 BITS가 파일을 전송 하려고 시도 하는 시간 (초)을 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setnoprogresstimeout <job> <timeoutvalue>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| timeoutvalue | 첫 번째 오류가 발생 한 후 BITS가 파일을 전송 하기 위해 대기 하는 시간 (초)입니다. |

### <a name="remarks"></a>설명

- 작업에서 첫 번째 일시적인 오류가 발생할 때 "진행 안 함" 시간 제한 간격이 시작 됩니다.

- 시간 제한 간격 중지 하거나 데이터의 바이트 성공적으로 전송 될 때 다시 설정 합니다.

- "진행 안 함" 시간 제한 간격이 *timeoutvalue*을 초과 하는 경우 작업은 심각한 오류 상태에 배치 됩니다.

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업에 대해 "진행 안 함" 제한 시간 값을 20 초로 설정 하려면 다음을 수행 합니다.

```
bitsadmin /setnoprogresstimeout myDownloadJob 20
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
