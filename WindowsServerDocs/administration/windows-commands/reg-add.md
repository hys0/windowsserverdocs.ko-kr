---
title: Reg 추가
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9ad143e-dc10-4e2e-a229-408393c40079
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 61ed9273c0225477d8bd6043dfc599e3e3ae6228
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868884"
---
# <a name="reg-add"></a>Reg 추가


새 하위 키 또는 항목을 레지스트리에 추가합니다.

## <a name="syntax"></a>구문

```
reg add <KeyName> [{/v ValueName | /ve}] [/t DataType] [/s Separator] [/d Data] [/f]
```
이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<KeyName*>*|하위 키 또는 추가할 항목의 전체 경로 지정 합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름을 포함 합니다 (형식에서 \\ \\ \<ComputerName >\) 의 일부로 합니다 *KeyName*합니다. 생략 \\ \\ComputerName\ 하면 로컬 컴퓨터에 기본 작업이 있습니다. *KeyName* 유효한 루트 키를 포함 해야 합니다. 로컬 컴퓨터에 대 한 유효한 루트 키 다음과 같습니다. HKLM, HKCU, HKCR, HKU, and HKCC. 원격 컴퓨터를 지정 하는 경우 유효한 루트 키 다음과 같습니다. HKLM 및 HKU 합니다. 레지스트리 키 이름에 공백이 있으면 키 이름을 따옴표로 묶습니다.|
|/v \<ValueName>|지정된 된 하위 키 아래에 추가 될 레지스트리 항목의 이름을 지정 합니다.|
|/s 모든 하위|레지스트리에 추가 된 레지스트리 항목이 null 값을 갖도록 지정 합니다.|
|/t \<형식 >|레지스트리 항목에 대 한 형식을 지정합니다. *형식* 다음 중 하나 여야 합니다.</br>REG_SZ</br>REG_MULTI_SZ</br>REG_DWORD_BIG_ENDIAN</br>REG_DWORD</br>REG_BINARY</br>REG_DWORD_LITTLE_ENDIAN</br>REG_LINK</br>REG_FULL_RESOURCE_DESCRIPTOR</br>REG_EXPAND_SZ|
|/s \<구분 >|REG_MULTI_SZ 데이터 형식이 지정 되 고 하나 이상의 항목을 나열 해야 하는 경우 데이터의 여러 인스턴스를 구분 하는 데 사용할 문자를 지정 합니다. 지정 하지 않으면 기본 구분 기호는 **\0**합니다.|
|/d \<데이터 >|새 레지스트리 항목에 대 한 데이터를 지정합니다.|
|/f|확인 메시지 없이 레지스트리 항목을 추가 합니다.|
|/?|에 대 한 도움말을 표시 **reg 추가** 명령 프롬프트입니다.|

## <a name="remarks"></a>설명

-   이 작업을 하위 트리를 추가할 수 없습니다. 이 버전의 **reg** 하위 키를 추가 하는 경우 확인을 위해 묻지 않습니다.
-   다음 표에 대 한 반환 값은 **reg 추가** 작업 합니다.

|값|Description|
|-----|-----------|
|0|성공|
|1|실패|
-   REG_EXPAND_SZ 키 형식에 대 한 캐럿 기호를 사용 하 여 ( **^** )와 **%**/d 매개 변수 "내

## <a name="BKMK_examples"></a>예제

원격 컴퓨터 ABC에서 HKLM\Software\MyCo 키를 추가 하려면 다음을 입력 합니다.
```
REG ADD \\ABC\HKLM\Software\MyCo
```
명명 된 값을 가진 HKLM\Software\MyCo 레지스트리 항목을 추가 하려면 **데이터** 의 REG_BINARY와의 데이터 입력 **fe340ead**, 유형:
```
REG ADD HKLM\Software\MyCo /v Data /t REG_BINARY /d fe340ead
```
값 이름을 가진 HKLM\Software\MyCo 다중값된 레지스트리 항목을 추가 하려면 **MRU** 의 REG_MULTI_SZ와의 데이터 입력 **fax\0mail\0\0**, 유형:
```
REG ADD HKLM\Software\MyCo /v MRU /t REG_MULTI_SZ /d fax\0mail\0\0
```
값 이름을 가진 HKLM\Software\MyCo에 확장 된 레지스트리 항목을 추가 하려면 **경로** 의 REG_EXPAND_SZ와의 데이터 입력 **%systemroot%**, 유형:
```
REG ADD HKLM\Software\MyCo /v Path /t REG_EXPAND_SZ /d ^%systemroot^%
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
