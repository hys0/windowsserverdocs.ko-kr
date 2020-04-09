---
title: bitsadmin addfileset
description: '**Bitsadmin addfileset**에 대 한 Windows 명령 항목-지정 된 작업에 하나 이상의 파일을 추가 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 75466994-262f-4724-b14d-f813c5397675
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1c4cff7dc8439fe8e1c54d1f5d231d1b487dc70c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850976"
---
# <a name="bitsadmin-addfileset"></a>bitsadmin addfileset

지정된 된 작업에 하나 이상의 파일을 추가합니다.

## <a name="syntax"></a>구문

```
bitsadmin /addfileset <Job> <TextFile>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 작업 | 작업의 표시 이름 또는 GUID입니다. |
| TextFile | 텍스트 파일-각 줄에는 원격 및 로컬 파일 이름이 포함 됩니다. **참고:** 이름을 공백으로 구분 됩니다. `#` 문자로 시작 하는 줄은 주석으로 처리 됩니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

```
C:\>bitsadmin /addfileset files.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)