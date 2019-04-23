---
title: Reg delete
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cee05071-1607-4ab1-b8ab-65caebeb85c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 369ef3bda37ab8e143a14f0f9707b9bbf14bd5f8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877084"
---
# <a name="reg-delete"></a>Reg delete



레지스트리에서 하위 키 또는 항목을 삭제합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
Reg delete <KeyName> [{/v ValueName | /ve | /va}] [/f]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<KeyName>|삭제할 항목을 확인 하는 하위 키의 전체 경로 지정 합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름을 포함 합니다 (형식에서 \\ \\ComputerName\) 의 일부로 합니다 *KeyName*합니다. 생략 \\ \\ComputerName\ 하면 로컬 컴퓨터에 기본 작업이 있습니다. *KeyName* 유효한 루트 키를 포함 해야 합니다. 로컬 컴퓨터에 대 한 유효한 루트 키 다음과 같습니다. HKLM, HKCU, HKCR, HKU, and HKCC. 원격 컴퓨터를 지정 하는 경우 유효한 루트 키 다음과 같습니다. HKLM 및 HKU 합니다.|
|/v \<ValueName>|하위 키에서 특정 항목을 삭제합니다. 항목이 지정 된 경우 다음 모든 항목 및 하위 키 아래 하위 키 삭제 됩니다.|
|/s 모든 하위|값이 없는 항목에만 삭제 될 것 이라는 것을 지정 합니다.|
|/va|지정된 된 하위 키 아래에서 모든 항목을 삭제합니다. 지정된 된 하위 키 아래에서 하위 키 삭제 되지 않습니다.|
|/f|확인을 요청 하지 않고 기존 레지스트리 하위 키 또는 항목을 삭제 합니다.|
|/?|에 대 한 도움말을 표시 **reg 삭제** 명령 프롬프트입니다.|

## <a name="remarks"></a>설명

다음 표에 대 한 반환 값은 **reg 삭제** 작업 합니다.

|값|Description|
|-----|-----------|
|0|성공|
|1|실패|

## <a name="BKMK_examples"></a>예제

레지스트리 키 제한 시간 및 모든 하위 키와 값을 삭제 하려면 다음을 입력 합니다.
```
REG DELETE HKLM\Software\MyCo\MyApp\Timeout
```
육십갑자 이라는 컴퓨터의 레지스트리 값에서 HKLM\Software\MyCo MTU를 삭제 하려면 다음을 입력 합니다.
```
REG DELETE \\ZODIAC\HKLM\Software\MyCo /v MTU
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)