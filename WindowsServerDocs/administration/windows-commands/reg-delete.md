---
title: reg delete
description: 레지스트리에서 하위 키 또는 항목을 삭제 하는 reg delete 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cee05071-1607-4ab1-b8ab-65caebeb85c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c8f90578cdd291f5788fc53223d9dc471f7a1458
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934656"
---
# <a name="reg-delete"></a>reg delete

레지스트리에서 하위 키 또는 항목을 삭제합니다.

## <a name="syntax"></a>구문

```
reg delete <keyname> [{/v Valuename | /ve | /va}] [/f]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|--|--|
| `<keyname1>` | 하위 키 또는 추가할 항목의 전체 경로 지정 합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름 (형식 `\\<computername>\` )을 *keyname*의 일부로 포함 합니다. 생략 `\\<computername>\` 하면 작업이 로컬 컴퓨터에 기본적으로 설정 됩니다. *Keyname* 은 올바른 루트 키를 포함 해야 합니다. 로컬 컴퓨터의 유효한 루트 키는 **HKLM**, **HKCU**, **HKCR**, **HKU**및 **hkcc**입니다. 원격 컴퓨터를 지정 하는 경우 유효한 루트 키는 **HKLM** 및 **HKU**입니다. 레지스트리 키 이름에 공백이 포함 되어 있으면 키 이름을 따옴표로 묶으십시오. |
| /v`<Valuename>` | 하위 키에서 특정 항목을 삭제합니다. 항목이 지정 된 경우 다음 모든 항목 및 하위 키 아래 하위 키 삭제 됩니다. |
| /s 모든 하위 | 값이 없는 항목에만 삭제 될 것 이라는 것을 지정 합니다. |
| /va | 지정된 된 하위 키 아래에서 모든 항목을 삭제합니다. 지정된 된 하위 키 아래에서 하위 키 삭제 되지 않습니다. |
| /f | 확인을 요청 하지 않고 기존 레지스트리 하위 키 또는 항목을 삭제 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- **Reg delete** 작업의 반환 값은 다음과 같습니다.

    | 값 | 설명 |
    |--|--|
    | 0 | 성공 |
    | 1 | 실패 |

### <a name="examples"></a>예

레지스트리 키 제한 시간 및 모든 하위 키와 값을 삭제 하려면 다음을 입력 합니다.

```
reg delete HKLM\Software\MyCo\MyApp\Timeout
```

육십갑자 이라는 컴퓨터의 레지스트리 값에서 HKLM\Software\MyCo MTU를 삭제 하려면 다음을 입력 합니다.

```
reg delete \\ZODIAC\HKLM\Software\MyCo /v MTU
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
