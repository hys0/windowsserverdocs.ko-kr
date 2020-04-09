---
title: reg 쿼리
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0e6a0d7c-ed9b-4318-833d-33f265a81f39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bf21933e1ce9928048f0f07ed502dfcab75d1783
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836396"
---
# <a name="reg-query"></a>reg 쿼리



다음 계층의 하위 키와 레지스트리에 지정된 된 하위 키 아래에 있는 항목의 목록을 반환 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
reg query <KeyName> [{/v <ValueName> | /ve}] [/s] [/se <Separator>] [/f <Data>] [{/k | /d}] [/c] [/e] [/t <Type>] [/z]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<KeyName >|하위 키의 전체 경로 지정합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름을 *KeyName*의 일부로 \\\\ComputerName\) 형식으로 포함 합니다. ComputerName을 \\\\생략 하면 작업이 로컬 컴퓨터를 기본값으로 설정 됩니다. *KeyName* 유효한 루트 키를 포함 해야 합니다. 로컬 컴퓨터에 대 한 유효한 루트 키: HKLM, HKCU, HKCR, HKU, 및 HKCC 합니다. 원격 컴퓨터를 지정 하는 경우 올바른 루트 키가: HKLM 및 HKU 합니다.|
|/v \<ValueName >|쿼리할 수 있는 레지스트리 값 이름을 지정 합니다. 에 대 한 이름을 생략 하면 모든 값 *KeyName* 반환 됩니다. *ValueName* 이 매개 변수는 선택 사항에 대 한 경우는 **/f** 옵션이 사용 됩니다.|
|/s 모든 하위|비어 있는 값 이름에 대 한 쿼리를 실행 합니다.|
|/s|모든 하위 키 및 값 이름 재귀적으로 쿼리를 지정 합니다.|
|/se \<구분 기호 >|값 이름에 입력 REG_MULTI_SZ 검색할 단일 값 구분 기호를 지정 합니다. 경우 *구분 기호* 를 지정 하지 않으면 **\0** 사용 됩니다.|
|/f \<데이터 >|데이터 또는 패턴에 대 한 검색을 지정 합니다. 문자열에 공백이 있으면 큰따옴표를 사용 합니다. 지정 하지 않으면 와일드 카드 ( **&#42;** )가 검색 패턴으로 사용 됩니다.|
|/k|키 이름만에서 검색 하도록 지정 합니다.|
|/d|데이터 에서만 검색 하도록 지정 합니다.|
|/c|쿼리 대/소문자 구분 임을 지정 합니다. 기본적으로 쿼리는 대 소문자를 구분 하지 않습니다.|
|/e|만 정확히 일치를 반환 하도록 지정 합니다. 기본적으로 일치 항목을 모두 반환 됩니다.|
|/t \<형식 >|검색할 레지스트리 형식을 지정 합니다. 올바른 유형은: REG_SZ, REG_MULTI_SZ, REG_EXPAND_SZ, REG_DWORD, REG_BINARY, 해결책입니다. 지정 하지 않으면 모든 형식은 검색 됩니다.|
|/z|검색 결과에 레지스트리 형식에 대 한 해당 숫자를 포함 하도록 지정 합니다.|
|/?|에 대 한 도움말을 표시 **레지스트리 쿼리** 명령 프롬프트입니다.|

## <a name="remarks-optional-section"></a>설명 \<선택적 섹션 >

다음 표에 대 한 반환 값은 **레지스트리 쿼리** 작업 합니다.

|값|설명|
|-----|-----------|
|0|성공|
|1|실패|

## <a name="examples"></a><a name=BKMK_examples></a>예와

HKLM\Software\Microsoft\ResKit 키의 버전 이름 값의 값을 표시 하려면 다음을 입력 합니다.
```
REG QUERY HKLM\Software\Microsoft\ResKit /v Version
```
모든 하위 키와 HKLM\Software\Microsoft\ResKit\Nt\Setup 키 아래의 값 ABC 라는 원격 컴퓨터를 표시 하려면 다음을 입력 합니다.
```
REG QUERY \\ABC\HKLM\Software\Microsoft\ResKit\Nt\Setup /s
```
모든 하위 키와 사용 하는 형식의 REG_MULTI_SZ 값을 표시 하려면 **#** 구분 기호를 입력 합니다.
```
REG QUERY HKLM\Software\Microsoft\ResKit\Nt\Setup /se #
```
키를 표시 하려면 값과 정확히 일치 및 대/소문자 구분에 대 한 데이터 일치 시스템의 HKLM 루트 데이터 종류 REG_SZ, 형식에 해당 합니다.
```
REG QUERY HKLM /f SYSTEM /t REG_SZ /c /e
```
키, 값 및 일치 하는 데이터를 표시 하려면 **0F** HKCU 루트 키 데이터의 데이터에서 REG_BINARY를 입력 합니다.
```
REG QUERY HKCU /f 0F /d /t REG_BINARY
```
값 및 값 이름 HKLM\SOFTWARE에서 null (기본값)에 대 한 데이터를 표시 하려면 다음을 입력 합니다.
```
REG QUERY HKLM\SOFTWARE /ve
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)