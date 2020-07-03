---
title: reg load
description: 레지스트리의 다른 하위 키에 저장 된 하위 키와 항목을 기록 하는 reg load 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3b0b2b1b-f510-4108-9e9d-7057e924aa6e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ba298ec5743022034f9576b50ff75e20b6f2d3e3
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931090"
---
# <a name="reg-load"></a>reg load

쓰기 레지스트리에 하위 키와 다른 하위 키에 대 한 항목을 저장 합니다. 이 명령은 문제를 해결 하거나 레지스트리 항목을 편집 하는 데 사용 되는 임시 파일을 사용 하기 위한 것입니다.

## <a name="syntax"></a>구문

```
reg load <keyname> <filename>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|--|--|
| `<keyname>` | 로드할 하위 키의 전체 경로 지정 합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름 (형식 `\\<computername>\` )을 *keyname*의 일부로 포함 합니다. 생략 `\\<computername>\` 하면 작업이 로컬 컴퓨터에 기본적으로 설정 됩니다. *Keyname* 은 올바른 루트 키를 포함 해야 합니다. 로컬 컴퓨터의 유효한 루트 키는 **HKLM**, **HKCU**, **HKCR**, **HKU**및 **hkcc**입니다. 원격 컴퓨터를 지정 하는 경우 유효한 루트 키는 **HKLM** 및 **HKU**입니다. 레지스트리 키 이름에 공백이 포함 되어 있으면 키 이름을 따옴표로 묶으십시오.  |
| `<filename>` | 로드할 파일의 경로 이름을 지정 합니다. 이 파일은 **reg 저장** 명령을 사용 하 여 미리 만들어야 하며 확장명이 하이브 여야 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- **Reg 로드** 작업에 대 한 반환 값은 다음과 같습니다.

    | 값 | 설명 |
    |--|--|
    | 0 | 성공 |
    | 1 | 실패 |

### <a name="examples"></a>예

키 만듭니다 TempHive.hiv 라는 파일을 로드 하려면 다음을 입력 합니다.

```
reg load HKLM\TempHive TempHive.hiv
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [reg 저장 명령](reg-save.md)
