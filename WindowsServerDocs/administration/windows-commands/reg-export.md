---
title: reg export
description: 다른 서버로 전송 하기 위해 로컬 컴퓨터의 지정 된 하위 키, 항목 및 값을 파일에 복사 하는 reg export 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0ad9526f-1e29-4fa5-9d2d-feaa92f12d7c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4c0cad839569651823e1c1a2bcca3c17c5550c8a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934640"
---
# <a name="reg-export"></a>reg export

다른 서버에 전송 하기 위해서는 파일에 지정 된 하위 키, 항목 및 로컬 컴퓨터의 값을 복사합니다.

## <a name="syntax"></a>구문

```
reg export <keyname> <filename> [/y]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|--|--|
| `<keyname>` | 하위 키의 전체 경로 지정합니다. 내보내기 작업은 로컬 컴퓨터 에서만 작동 합니다. *Keyname* 은 올바른 루트 키를 포함 해야 합니다. 로컬 컴퓨터의 유효한 루트 키는 **HKLM**, **HKCU**, **HKCR**, **HKU**및 **hkcc**입니다. 레지스트리 키 이름에 공백이 포함 되어 있으면 키 이름을 따옴표로 묶으십시오. |
| `<filename>` | 작업 중에 만든 파일의 경로 이름을 지정 합니다. 파일은 확장명이.reg 인이 있어야 합니다. |
| /y | 확인 메시지를 *표시 하지 않고 파일 이름* 으로 기존 파일을 덮어씁니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- **Reg export** 작업에 대 한 반환 값은 다음과 같습니다.

    | 값 | 설명 |
    |--|--|
    | 0 | 성공 |
    | 1 | 실패 |

### <a name="examples"></a>예

모든 하위 키의 내용과 MyApp 키의 값 AppBkUp.reg 파일을 내보내려면 다음을 입력 합니다.

```
reg export HKLM\Software\MyCo\MyApp AppBkUp.reg
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
