---
title: reg restore
description: 레지스트리에 저장 된 하위 키와 항목을 다시 기록 하는 reg restore 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a51f1c0c-969b-4b76-930a-c8bb14dea26e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1483fc6998d7b286a81dc3cb1df021afb7e66650
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931043"
---
# <a name="reg-restore"></a>reg restore

쓰기 저장 된 하위 키와 항목 레지스트리를 백업합니다.

## <a name="syntax"></a>구문

```
reg restore <keyname> <filename>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|--|--|
| `<keyname>` | 복원 해야 하는 하위 키의 전체 경로 지정 합니다. 복원 작업은 로컬 컴퓨터 에서만 작동 합니다. *Keyname* 은 올바른 루트 키를 포함 해야 합니다. 로컬 컴퓨터의 유효한 루트 키는 **HKLM**, **HKCU**, **HKCR**, **HKU**및 **hkcc**입니다. 레지스트리 키 이름에 공백이 포함 되어 있으면 키 이름을 따옴표로 묶으십시오. |
| `<filename>` | 콘텐츠를 레지스트리에 쓸 수 있는 파일의 경로 이름을 지정 합니다. 이 파일은 **reg 저장** 명령을 사용 하 여 미리 만들어야 하며 확장명이 하이브 여야 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 레지스트리 항목을 편집 하기 전에 **reg 저장** 명령을 사용 하 여 부모 하위 키를 저장 해야 합니다. 편집에 실패 하는 경우 **reg restore** 작업을 사용 하 여 원래 하위 키를 복원할 수 있습니다.

- **Reg 복원** 작업의 반환 값은 다음과 같습니다.

    | 값 | 설명 |
    |--|--|
    | 0 | 성공 |
    | 1 | 실패 |

### <a name="examples"></a>예

HKLM\Software\Microsoft\ResKit 키로 NTRKBkUp.hiv 라는 파일을 복원 하는 키의 기존 내용을 덮어씁니다 다음을 입력 합니다.

```
reg restore HKLM\Software\Microsoft\ResKit NTRKBkUp.hiv
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [reg 저장 명령](reg-save.md)
