---
title: bitsadmin makecustomheaderswriteonly
description: 작업의 사용자 지정 HTTP 헤더를 쓰기 전용으로 설정 하는 bitsadmin makecustomheaderswriteonly 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 2aeab7e0ee7797b3e0be7be1156920f3bafc84dc
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717411"
---
# <a name="bitsadmin-makecustomheaderswriteonly"></a>bitsadmin makecustomheaderswriteonly

작업의 사용자 지정 HTTP 헤더를 쓰기 전용으로 설정 합니다.

> [!IMPORTANT]
> 이 작업은 실행 취소할 수 없습니다.

## <a name="syntax"></a>구문

```
bitsadmin /makecustomheaderswriteonly <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

사용자 지정 HTTP 헤더를 *Mydownloadjob*이라는 작업에 대해 쓰기 전용으로 설정 하려면 다음을 수행 합니다.

```
bitsadmin /makecustomheaderswriteonly myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
