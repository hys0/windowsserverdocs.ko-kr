---
title: bitsadmin getnoprogresstimeout
description: 일시적인 오류가 발생 한 후 서비스가 파일을 전송 하려고 시도 하는 시간 (초)을 검색 하는 bitsadmin getnoprogresstimeout 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9cd9b19b-cbb4-4352-8419-978080f016b6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 95884f5e6b0dc7ae01575ddf0cc12afea6d212c3
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927003"
---
# <a name="bitsadmin-getnoprogresstimeout"></a>bitsadmin getnoprogresstimeout

일시적인 오류가 발생 한 후 서비스에서 파일을 전송 하려고 시도 하는 시간 (초)을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getnoprogresstimeout <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업에 대 한 진행률 제한 시간 값을 검색 하려면 다음을 수행 합니다.

```
bitsadmin /getnoprogresstimeout myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
