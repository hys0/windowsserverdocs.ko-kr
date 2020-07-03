---
title: reg add
description: 레지스트리에 새 하위 키 또는 항목을 추가 하는 reg add 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d9ad143e-dc10-4e2e-a229-408393c40079
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: db968e8fb55a4de73f5221f8149f794600f6884e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933512"
---
# <a name="reg-add"></a>reg add

새 하위 키 또는 항목을 레지스트리에 추가합니다.

## <a name="syntax"></a>구문

```
reg add <keyname> [{/v Valuename | /ve}] [/t datatype] [/s Separator] [/d Data] [/f]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|--|--|
| `<keyname>` | 하위 키 또는 추가할 항목의 전체 경로 지정 합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름 (형식 `\\<computername>\` )을 *keyname*의 일부로 포함 합니다. 생략 `\\<computername>\` 하면 작업이 로컬 컴퓨터에 기본적으로 설정 됩니다. *Keyname* 은 올바른 루트 키를 포함 해야 합니다. 로컬 컴퓨터의 유효한 루트 키는 **HKLM**, **HKCU**, **HKCR**, **HKU**및 **hkcc**입니다. 원격 컴퓨터를 지정 하는 경우 유효한 루트 키는 **HKLM** 및 **HKU**입니다. 레지스트리 키 이름에 공백이 포함 되어 있으면 키 이름을 따옴표로 묶으십시오. |
| /v`<Valuename>` | 레지스트리 항목 추가의 이름을 지정 합니다. |
| /s 모든 하위 | 추가 된 레지스트리 항목에 null 값이 있음을 지정 합니다. |
| /t`<Type>` | 레지스트리 항목에 대 한 형식을 지정합니다. *형식* 다음 중 하나 여야 합니다.<ul><li>REG_SZ</li><li>REG_MULTI_SZ</li><li>REG_DWORD_BIG_ENDIAN</li><li>REG_DWORD</li><li>REG_BINARY</li><li>REG_DWORD_LITTLE_ENDIAN</li><li>REG_LINK</li><li>REG_FULL_RESOURCE_DESCRIPTOR</li><li>REG_EXPAND_SZ</li></ul> |
| /s`<Separator>` | **REG_MULTI_SZ** 데이터 형식이 지정 되 고 둘 이상의 항목이 나열 될 때 여러 데이터 인스턴스를 구분 하는 데 사용할 문자를 지정 합니다. 지정 하지 않으면 기본 구분 기호는 **\0**합니다. |
| d`<Data>` | 새 레지스트리 항목에 대 한 데이터를 지정합니다. |
| /f | 확인 메시지 없이 레지스트리 항목을 추가 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 이 작업을 사용 하 여 하위 트리를 추가할 수 없습니다. 이 버전의 **reg** 는 하위 키를 추가할 때 확인 메시지를 표시 하지 않습니다.

- **Reg add** 작업의 반환 값은 다음과 같습니다.

| 값 | 설명 |
|--|--|
| 0 | 성공 |
| 1 | 실패 |

- **REG_EXPAND_SZ** 키 형식에 대해 **^** **%** /d 매개 변수 내에서 캐럿 기호 ()를 사용 합니다.

### <a name="examples"></a>예

원격 컴퓨터 *ABC*에 *HKLM\Software\MyCo* 키를 추가 하려면 다음을 입력 합니다.

```
reg add \\ABC\HKLM\Software\MyCo
```

*HKLM\Software\MyCo에* 에 대 한 레지스트리 항목을 추가 하려면 *data*, type *REG_BINARY*및 *fe340ead*의 데이터를 입력 합니다.

```
reg add HKLM\Software\MyCo /v Data /t REG_BINARY /d fe340ead
```

*HKLM\Software\MyCo* 에 다중값 레지스트리 항목을 추가 하려면 이름에 *MRU*, 형식 *REG_MULTI_SZ*및 *fax\0mail\0\0*의 데이터를 입력 합니다.

```
reg add HKLM\Software\MyCo /v MRU /t REG_MULTI_SZ /d fax\0mail\0\0
```

*HKLM\Software\MyCo* 에 확장 된 레지스트리 항목을 추가 하려면 *Path*, type *REG_EXPAND_SZ*및 *% systemroot%* 의 데이터를 입력 하 고 다음을 입력 합니다.

```
reg add HKLM\Software\MyCo /v Path /t REG_EXPAND_SZ /d ^%systemroot^%
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
