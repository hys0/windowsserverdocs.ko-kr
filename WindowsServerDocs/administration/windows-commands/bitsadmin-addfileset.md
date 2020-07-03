---
title: bitsadmin addfileset
description: 지정 된 작업에 하나 이상의 파일을 추가 하는 bitsadmin addfileset 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 75466994-262f-4724-b14d-f813c5397675
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 861186dfc7ba1a230e1df05c98378d27bfff26b1
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927082"
---
# <a name="bitsadmin-addfileset"></a>bitsadmin addfileset

지정된 된 작업에 하나 이상의 파일을 추가합니다.

## <a name="syntax"></a>구문

```
bitsadmin /addfileset <job> <textfile>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| textfile | 텍스트 파일-각 줄에는 원격 및 로컬 파일 이름이 포함 됩니다. **참고:** 이름은 공백으로 구분 되어야 합니다. 문자로 시작 하는 줄 `#` 은 주석으로 처리 됩니다. |

## <a name="examples"></a>예

```
bitsadmin /addfileset files.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
