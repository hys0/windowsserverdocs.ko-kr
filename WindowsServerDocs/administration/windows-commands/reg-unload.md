---
title: Reg 언로드
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d07791d-ca27-454e-9797-27d7e84c5048
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aaa7d7a9fa82db2968d988e3b7b3fb8275a72337
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834984"
---
# <a name="reg-unload"></a>Reg 언로드



사용 하 여 로드 레지스트리의 섹션을 제거는 **reg 부하** 작업 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
reg unload <KeyName>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<KeyName>|언로드해야 하는 하위 키의 전체 경로 지정 합니다. 원격 컴퓨터를 지정 하는 것에 대 한 컴퓨터 이름을 포함 합니다 (형식에서 \\ \\ComputerName\) 의 일부로 합니다 *KeyName*합니다. 생략 \\ \\ComputerName\ 하면 로컬 컴퓨터에 기본 작업이 있습니다. *KeyName* 유효한 루트 키를 포함 해야 합니다. 로컬 컴퓨터에 대 한 유효한 루트 키 HKLM, HKCU, HKCR, HKU, 및 HKCC 됩니다. 원격 컴퓨터를 지정 하는 경우 HKLM 및 HKU 유효한 루트 키가 있습니다.|
|/?|에 대 한 도움말을 표시 **reg 언로드** 명령 프롬프트입니다.|

## <a name="remarks"></a>설명

다음 표에 대 한 반환 값은 **reg 언로드** 옵션이 있습니다.

|값|Description|
|-----|-----------|
|0|성공|
|1|실패|

## <a name="BKMK_examples"></a>예제

HKLM 파일에서 TempHive 하이브 언로드 작업을 입력 합니다.
```
REG UNLOAD HKLM\TempHive
```

> [!CAUTION]
> 편집 하지 마십시오 레지스트리 직접 대체 하지 않으면. 레지스트리 편집기의 성능이 저하, 하면 시스템이 손상 또는 Windows를 다시 설치 해야 할 수 있는 설정을 허용 표준 보호를 무시 합니다. 안전 하 게 제어판 또는 Microsoft Management Console (MMC)에서 프로그램을 사용 하 여 대부분의 레지스트리 설정을 변경할 수 있습니다. 레지스트리를 직접 편집 해야 하는 경우 먼저 백업 합니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)