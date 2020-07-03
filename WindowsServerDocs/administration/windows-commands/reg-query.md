---
title: reg query
description: 레지스트리의 지정 된 하위 키 아래에 있는 하위 키와 항목의 다음 계층 목록을 반환 하는 reg 쿼리 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0e6a0d7c-ed9b-4318-833d-33f265a81f39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 18b7c5223227e0cf19de22f8bc9886ae798f027f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931059"
---
# <a name="reg-query"></a>reg query

다음 계층의 하위 키와 레지스트리에 지정된 된 하위 키 아래에 있는 항목의 목록을 반환 합니다.

## <a name="syntax"></a>구문

```
reg query <keyname> [{/v <Valuename> | /ve}] [/s] [/se <separator>] [/f <data>] [{/k | /d}] [/c] [/e] [/t <Type>] [/z]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|--|--|
| `<keyname>` | 하위 키의 전체 경로 지정합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름 (형식 `\\<computername>\` )을 *keyname*의 일부로 포함 합니다. 생략 `\\<computername>\` 하면 작업이 로컬 컴퓨터에 기본적으로 설정 됩니다. *Keyname* 은 올바른 루트 키를 포함 해야 합니다. 로컬 컴퓨터의 유효한 루트 키는 **HKLM**, **HKCU**, **HKCR**, **HKU**및 **hkcc**입니다. 원격 컴퓨터를 지정 하는 경우 유효한 루트 키는 **HKLM** 및 **HKU**입니다. 레지스트리 키 이름에 공백이 포함 되어 있으면 키 이름을 따옴표로 묶으십시오. |
| /v`<Valuename>` | 쿼리할 수 있는 레지스트리 값 이름을 지정 합니다. 생략 하면 *keyname* 의 모든 값 이름이 반환 됩니다. **/F** 옵션도 사용 하는 경우이 매개 변수의 *Valuename* 은 선택 사항입니다. |
| /s 모든 하위 | 비어 있는 값 이름에 대 한 쿼리를 실행 합니다. |
| /s | 모든 하위 키 및 값 이름 재귀적으로 쿼리를 지정 합니다. |
| /se`<separator>` | **REG_MULTI_SZ**값 이름 형식에서 검색할 단일 값 구분 기호를 지정 합니다. *구분 기호* 를 지정 하지 않으면 **\ 0** 이 사용 됩니다. |
| /f `<data>` | 데이터 또는 패턴에 대 한 검색을 지정 합니다. 문자열에 공백이 있으면 큰따옴표를 사용 합니다. 지정 하지 않으면 와일드 카드 (**&#42;**)가 검색 패턴으로 사용 됩니다. |
| /k | 키 이름만에서 검색 하도록 지정 합니다. |
| /d | 데이터 에서만 검색 하도록 지정 합니다. |
| /C | 쿼리 대/소문자 구분 임을 지정 합니다. 기본적으로 쿼리는 대 소문자를 구분 하지 않습니다. |
| /e | 만 정확히 일치를 반환 하도록 지정 합니다. 기본적으로 일치 항목을 모두 반환 됩니다. |
| /t`<Type>` | 검색할 레지스트리 형식을 지정 합니다. 유효한 형식은 **REG_SZ**, **REG_MULTI_SZ**, **REG_EXPAND_SZ**, **REG_DWORD**, **REG_BINARY**, **REG_NONE**입니다. 지정 하지 않으면 모든 형식은 검색 됩니다. |
| /z | 검색 결과에 레지스트리 형식에 대 한 해당 숫자를 포함 하도록 지정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- **Reg 쿼리** 작업의 반환 값은 다음과 같습니다.

    | 값 | 설명 |
    |--|--|
    | 0 | 성공 |
    | 1 | 실패 |

### <a name="examples"></a>예

HKLM\Software\Microsoft\ResKit 키의 버전 이름 값의 값을 표시 하려면 다음을 입력 합니다.

```
reg query HKLM\Software\Microsoft\ResKit /v Version
```

모든 하위 키와 HKLM\Software\Microsoft\ResKit\Nt\Setup 키 아래의 값 ABC 라는 원격 컴퓨터를 표시 하려면 다음을 입력 합니다.

```
reg query \\ABC\HKLM\Software\Microsoft\ResKit\Nt\Setup /s
```

구분 기호로를 사용 하 REG_MULTI_SZ 형식의 모든 하위 키와 값을 표시 하려면 **#** 다음을 입력 합니다.

```
reg query HKLM\Software\Microsoft\ResKit\Nt\Setup /se #
```

키를 표시 하려면 값과 정확히 일치 및 대/소문자 구분에 대 한 데이터 일치 시스템의 HKLM 루트 데이터 종류 REG_SZ, 형식에 해당 합니다.

```
reg query HKLM /f SYSTEM /t REG_SZ /c /e
```

**0f에서** 데이터 REG_BINARY 형식에 대 한 HKCU 루트 키 아래의 데이터에 일치 하는 키, 값 및 데이터를 표시 하려면 다음을 입력 합니다.

```
reg query HKCU /f 0F /d /t REG_BINARY
```

값 및 값 이름 HKLM\SOFTWARE에서 null (기본값)에 대 한 데이터를 표시 하려면 다음을 입력 합니다.

```
reg query HKLM\SOFTWARE /ve
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
