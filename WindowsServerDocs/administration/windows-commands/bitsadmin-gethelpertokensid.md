---
title: bitsadmin gethelpertokensid
description: BITS 전송 작업의 도우미 토큰 (설정 된 경우)의 SID를 반환 하는 bitsadmin gethelpertokensid 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: b616b9cc80b21c4c6a72fcca55dcdd893fac2730
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928196"
---
# <a name="bitsadmin-gethelpertokensid"></a>bitsadmin gethelpertokensid

설정 된 경우 BITS 전송 작업의 [도우미 토큰](https://docs.microsoft.com/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)에 대 한 SID를 반환 합니다.

> [!NOTE]
> 이 명령은 BITS 3.0 이전 버전에서는 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /gethelpertokensid <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 BITS 전송 작업의 SID를 검색 하려면 다음을 수행 합니다.

```
bitsadmin /gethelpertokensid myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
