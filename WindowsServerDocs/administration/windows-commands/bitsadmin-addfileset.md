---
title: bitsadmin addfileset
description: 지정 된 작업에 하나 이상의 파일을 추가 하는 bitsadmin addfileset 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 75466994-262f-4724-b14d-f813c5397675
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d610c1330818cf820923b6d4f2e3555dc477444b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718477"
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
| textfile | 텍스트 파일-각 줄에는 원격 및 로컬 파일 이름이 포함 됩니다. **참고:** 이름은 공백으로 구분 되어야 합니다. `#` 문자로 시작 하는 줄은 주석으로 처리 됩니다. |

## <a name="examples"></a>예

```
bitsadmin /addfileset files.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
