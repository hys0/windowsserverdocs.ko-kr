---
title: reg compare
description: 지정 된 레지스트리 하위 키 또는 항목을 비교 하는 reg compare 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 177dc6a3-034e-4846-a394-330d03c14e0b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3b508a52d0f110455b09002a1044fefcf1be048a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930734"
---
# <a name="reg-compare"></a>reg compare

비교 하 여 레지스트리 하위 키 또는 항목을 지정 합니다.

## <a name="syntax"></a>구문

```
reg compare <keyname1> <keyname2> [{/v Valuename | /ve}] [{/oa | /od | /os | on}] [/s]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| `<keyname1>` | 하위 키 또는 추가할 항목의 전체 경로 지정 합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름 (형식 `\\<computername>\` )을 *keyname*의 일부로 포함 합니다. 생략 `\\<computername>\` 하면 작업이 로컬 컴퓨터에 기본적으로 설정 됩니다. *Keyname* 은 올바른 루트 키를 포함 해야 합니다. 로컬 컴퓨터의 유효한 루트 키는 **HKLM**, **HKCU**, **HKCR**, **HKU**및 **hkcc**입니다. 원격 컴퓨터를 지정 하는 경우 유효한 루트 키는 **HKLM** 및 **HKU**입니다. 레지스트리 키 이름에 공백이 포함 되어 있으면 키 이름을 따옴표로 묶으십시오. |
| `<keyname2>` | 비교할 두 번째 하위 키의 전체 경로 지정 합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름 (형식 `\\<computername>\` )을 *keyname*의 일부로 포함 합니다. 생략 `\\<computername>\` 하면 작업이 로컬 컴퓨터에 기본적으로 설정 됩니다. *Keyname2* 에 컴퓨터 이름만 지정 하면 작업은 *keyname1*에 지정 된 하위 키에 대 한 경로를 사용 합니다. *Keyname* 은 올바른 루트 키를 포함 해야 합니다. 로컬 컴퓨터의 유효한 루트 키는 **HKLM**, **HKCU**, **HKCR**, **HKU**및 **hkcc**입니다. 원격 컴퓨터를 지정 하는 경우 유효한 루트 키는 **HKLM** 및 **HKU**입니다. 레지스트리 키 이름에 공백이 포함 되어 있으면 키 이름을 따옴표로 묶으십시오. |
| /v`<Valuename>` | 하위 키 아래 비교할 값 이름을 지정 합니다. |
| /s 모든 하위 | Null 값 이름이 있는 항목만 비교 되어야 함을 지정 합니다. |
| /oa | 모든 차이 일치 하는 항목 표시 되도록 지정 합니다. 기본적으로 변경 된 사항만 나열 됩니다. |
| /od | 차이만 표시 되도록 지정 합니다. 이것은 기본적인 동작입니다. |
| /os | 일치만 표시 되도록 지정 합니다. 기본적으로 변경 된 사항만 나열 됩니다. |
| /on | 아무 것도 표시 되도록 지정 합니다. 기본적으로 변경 된 사항만 나열 됩니다. |
| /s | 모든 하위 키와 항목 재귀적으로 비교합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- **Reg compare** 작업의 반환 값은 다음과 같습니다.

    | 값 | 설명 |
    |--|--|
    | 0 | 비교는 성공 하 고 결과 동일 합니다. |
    | 1 | 비교에 실패 했습니다. |
    | 2 | 비교 성공적이 고 차이 찾았습니다. |

- 결과에 표시 되는 기호는 다음과 같습니다.

    | 기호 | 설명 |
    |--|--|
    | = | *KeyName1* 데이터 같으면 *KeyName2* 데이터입니다. |
    | < | *KeyName1* 데이터는 보다 작은 *KeyName2* 데이터입니다. |
    | > | *KeyName1* 데이터 보다 크면 *KeyName2* 데이터입니다. |

### <a name="examples"></a>예

**MyApp** 키 아래의 모든 값을 **Savemyapp**키의 모든 값과 비교 하려면 다음을 입력 합니다.

```
reg compare HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp
```

**MyCo** 키 아래에 있는 버전의 값과 키 **MyCo1**의 버전 값을 비교 하려면 다음을 입력 합니다.

```
reg compare HKLM\Software\MyCo HKLM\Software\MyCo1 /v Version
```

로컬 컴퓨터에서 HKLM\Software\MyCo 아래의 모든 하위 키 및 값을 사용 하 여 컴퓨터에서 HKLM\Software\MyCo 아래의 모든 하위 키와 값을 비교 하려면 다음을 입력 합니다.

```
reg compare \\ZODIAC\HKLM\Software\MyCo \\. /s
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
