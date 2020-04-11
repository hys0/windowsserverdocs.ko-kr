---
title: bitsadmin setnoprogresstimeout
description: 서비스에서 일시적인 오류가 발생 한 후 파일을 전송 하려고 시도 하는 시간 (초)을 설정 하는 **bitsadmin setnoprogresstimeout**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7fac50d9-cc6b-46a4-a96f-fab751ee1756
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8adff95b0dbae68634db2e248d4493549c5ac85d
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122874"
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
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| timeoutvalue | 첫 번째 오류가 발생 한 후 BITS가 파일을 전송 하기 위해 대기 하는 시간 (초)입니다. |

## <a name="remarks"></a>주의

- 작업에서 첫 번째 일시적인 오류가 발생할 때 "진행 안 함" 시간 제한 간격이 시작 됩니다.

- 시간 제한 간격 중지 하거나 데이터의 바이트 성공적으로 전송 될 때 다시 설정 합니다.

- "진행 안 함" 시간 제한 간격이 *timeoutvalue*을 초과 하는 경우 작업은 심각한 오류 상태에 배치 됩니다.

## <a name="examples"></a>예

다음 예에서는 *Mydownloadjob*이라는 작업에 대해 "진행 안 함" 시간 제한 값을 20 초로 설정 합니다.

```
C:\>bitsadmin /setnoprogresstimeout myDownloadJob 20
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)