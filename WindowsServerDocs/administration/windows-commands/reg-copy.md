---
title: reg 복사
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe74213-39ec-4b2d-ba3d-086243eac997
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 11cbfce39433ea18632bec16c524da191def2a07
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867564"
---
# <a name="reg-copy"></a>reg 복사



로컬 또는 원격 컴퓨터의 지정된 된 위치에 레지스트리 항목을 복사합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
reg copy <KeyName1> <KeyName2> [/s] [/f]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<KeyName1>|복사할 하위 키의 전체 경로 지정 합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름을 포함 합니다 (형식에서 \\ \\ComputerName\) 의 일부로 합니다 *KeyName*합니다. 생략 \\ \\ComputerName\ 하면 로컬 컴퓨터에 기본 작업이 있습니다. *KeyName* 유효한 루트 키를 포함 해야 합니다. 로컬 컴퓨터에 대 한 유효한 루트 키 다음과 같습니다. HKLM, HKCU, HKCR, HKU, and HKCC. 원격 컴퓨터를 지정 하는 경우 유효한 루트 키 다음과 같습니다. HKLM 및 HKU 합니다.|
|\<KeyName2>|하위 키 대상의 전체 경로 지정합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름을 포함 합니다 (형식에서 \\ \\ComputerName\) 의 일부로 합니다 *KeyName*합니다. 생략 \\ \\ComputerName\ 하면 로컬 컴퓨터에 기본 작업이 있습니다. *KeyName* 유효한 루트 키를 포함 해야 합니다. 로컬 컴퓨터에 대 한 유효한 루트 키 다음과 같습니다. HKLM, HKCU, HKCR, HKU, and HKCC. 원격 컴퓨터를 지정 하는 경우 유효한 루트 키 다음과 같습니다. HKLM 및 HKU 합니다.|
|/s|모든 하위 키와 지정된 된 하위 키 아래에 항목을 복사합니다.|
|/f|확인 메시지 없이 하위 키를 복사 합니다.|
|/?|에 대 한 도움말을 표시 **reg** 명령 프롬프트에 복사 합니다.|

## <a name="remarks"></a>설명

-   레지스트리 하위 키를 복사 하는 경우 확인을 위해 묻지 않습니다.
-   다음 표에 대 한 반환 값은 **reg 복사** 작업 합니다.

|값|Description|
|-----|-----------|
|0|성공|
|1|실패|

## <a name="BKMK_examples"></a>예제

모든 하위 키와 MyApp 키 아래의 값 SaveMyApp 키를 복사 하려면 다음을 입력 합니다.
```
REG COPY HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp /s
```
현재 컴퓨터에서 키 MyCo1 육십갑자 이라는 컴퓨터의 MyCo 키 아래의 모든 값을 복사 하려면 다음을 입력 합니다.
```
REG COPY \\ZODIAC\HKLM\Software\MyCo HKLM\Software\MyCo1
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)