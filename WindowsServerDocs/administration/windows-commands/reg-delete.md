---
title: reg 삭제
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cee05071-1607-4ab1-b8ab-65caebeb85c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 726a3c700a9278dbc7abb1873aae7ea3c957bbb5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836506"
---
# <a name="reg-delete"></a>reg 삭제



레지스트리에서 하위 키 또는 항목을 삭제합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
Reg delete <KeyName> [{/v ValueName | /ve | /va}] [/f]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<KeyName >|삭제할 항목을 확인 하는 하위 키의 전체 경로 지정 합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름을 *KeyName*의 일부로 \\\\ComputerName\) 형식으로 포함 합니다. ComputerName을 \\\\생략 하면 작업이 로컬 컴퓨터를 기본값으로 설정 됩니다. *KeyName* 유효한 루트 키를 포함 해야 합니다. 로컬 컴퓨터에 대 한 유효한 루트 키: HKLM, HKCU, HKCR, HKU, 및 HKCC 합니다. 원격 컴퓨터를 지정 하는 경우 올바른 루트 키가: HKLM 및 HKU 합니다.|
|/v \<ValueName >|하위 키에서 특정 항목을 삭제합니다. 항목이 지정 된 경우 다음 모든 항목 및 하위 키 아래 하위 키 삭제 됩니다.|
|/s 모든 하위|값이 없는 항목에만 삭제 될 것 이라는 것을 지정 합니다.|
|/va|지정된 된 하위 키 아래에서 모든 항목을 삭제합니다. 지정된 된 하위 키 아래에서 하위 키 삭제 되지 않습니다.|
|/f|확인을 요청 하지 않고 기존 레지스트리 하위 키 또는 항목을 삭제 합니다.|
|/?|에 대 한 도움말을 표시 **reg 삭제** 명령 프롬프트입니다.|

## <a name="remarks"></a>주의

다음 표에 대 한 반환 값은 **reg 삭제** 작업 합니다.

|값|설명|
|-----|-----------|
|0|성공|
|1|실패|

## <a name="examples"></a><a name=BKMK_examples></a>예와

레지스트리 키 제한 시간 및 모든 하위 키와 값을 삭제 하려면 다음을 입력 합니다.
```
REG DELETE HKLM\Software\MyCo\MyApp\Timeout
```
육십갑자 이라는 컴퓨터의 레지스트리 값에서 HKLM\Software\MyCo MTU를 삭제 하려면 다음을 입력 합니다.
```
REG DELETE \\ZODIAC\HKLM\Software\MyCo /v MTU
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)