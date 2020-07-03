---
title: reg save
description: 지정 된 파일에 지정 된 하위 키, 항목 및 레지스트리 값의 복사본을 저장 하는 reg save 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b326482b-c8af-467d-a20c-0481eeda3d5c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4051d69819cfd3550d094de8e9d4bc73f77c4e4b
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931033"
---
# <a name="reg-save"></a>reg save

지정된 된 파일에 지정 된 하위 키, 항목 및 레지스트리 값의 복사본을 저장합니다.

## <a name="syntax"></a>구문

```
reg save <keyname> <filename> [/y]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|--|--|
| `<keyname>` | 하위 키의 전체 경로 지정합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름 (형식 `\\<computername>\` )을 *keyname*의 일부로 포함 합니다. 생략 `\\<computername>\` 하면 작업이 로컬 컴퓨터에 기본적으로 설정 됩니다. *Keyname* 은 올바른 루트 키를 포함 해야 합니다. 로컬 컴퓨터의 유효한 루트 키는 **HKLM**, **HKCU**, **HKCR**, **HKU**및 **hkcc**입니다. 원격 컴퓨터를 지정 하는 경우 유효한 루트 키는 **HKLM** 및 **HKU**입니다. 레지스트리 키 이름에 공백이 포함 되어 있으면 키 이름을 따옴표로 묶으십시오. |
| `<filename>` | 만든 파일의 이름 및 경로를 지정 합니다. 지정 된 경로가 현재 경로가 사용 됩니다. |
| /y | 확인 메시지를 *표시 하지 않고 파일 이름* 으로 기존 파일을 덮어씁니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 레지스트리 항목을 편집 하기 전에 **reg 저장** 명령을 사용 하 여 부모 하위 키를 저장 해야 합니다. 편집에 실패 하는 경우 **reg restore** 작업을 사용 하 여 원래 하위 키를 복원할 수 있습니다.

- **Reg 저장** 작업의 반환 값은 다음과 같습니다.

    | 값 | 설명 |
    |--|--|
    | 0 | 성공 |
    | 1 | 실패 |

### <a name="examples"></a>예

현재 폴더에 hive MyApp 중인 라는 파일을 저장 하려면 다음을 입력 합니다.

```
reg save HKLM\Software\MyCo\MyApp AppBkUp.hiv
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [reg restore 명령](reg-restore.md)