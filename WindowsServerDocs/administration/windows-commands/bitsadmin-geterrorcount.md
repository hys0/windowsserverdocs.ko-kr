---
title: bitsadmin geterrorcount
description: 지정 된 작업에서 일시적인 오류가 발생 한 횟수를 검색 하는 **bitsadmin geterrorcount**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8840ae78-52b0-4c7e-b592-0547359a237e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ef0bf043517d4edfa8d72888746ca5d9c92ecc21
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123133"
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
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 오류 개수 정보를 검색 *Mydownloadjob*합니다.

```
C:\>bitsadmin /geterrorcount myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)