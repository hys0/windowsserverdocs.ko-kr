---
title: bitsadmin geterrorcount
description: 지정 된 작업에서 일시적인 오류가 발생 한 횟수를 검색 하는 bitsadmin geterrorcount 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8840ae78-52b0-4c7e-b592-0547359a237e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 516bd02ed296a2eba75e174c6f084926bde63e90
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718005"
---
# <a name="bitsadmin-geterrorcount"></a>bitsadmin geterrorcount

지정 된 작업에서 일시적인 오류가 발생 한 횟수를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /geterrorcount <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업의 오류 수 정보를 검색 하려면:

```
bitsadmin /geterrorcount myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
