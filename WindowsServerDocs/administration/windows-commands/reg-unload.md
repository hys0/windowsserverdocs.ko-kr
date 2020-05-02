---
title: 레지스트리 언로드
description: Reg 로드 작업을 사용 하 여 로드 된 레지스트리의 섹션을 제거 하는 reg unload 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1d07791d-ca27-454e-9797-27d7e84c5048
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 029b9225f8a437be18c3056d97e153075d9df7c9
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722497"
---
# <a name="reg-unload"></a>레지스트리 언로드



사용 하 여 로드 레지스트리의 섹션을 제거는 **reg 부하** 작업 합니다.



## <a name="syntax"></a>구문

```
reg unload <KeyName>
```

### <a name="parameters"></a>매개 변수

|매개 변수|Description|
|---------|-----------|
|\<KeyName>|언로드해야 하는 하위 키의 전체 경로 지정 합니다. 원격 컴퓨터를 지정 하는 경우 컴퓨터 이름을 *KeyName*의 일부로 ComputerName \\ \\\) 형식으로 포함 합니다. ComputerName \\ \\을 생략 하면 작업이 로컬 컴퓨터에 기본값으로 설정 됩니다. *KeyName* 은 올바른 루트 키를 포함 해야 합니다. 로컬 컴퓨터에 대 한 유효한 루트 키 HKLM, HKCU, HKCR, HKU, 및 HKCC 됩니다. 원격 컴퓨터를 지정 하는 경우 HKLM 및 HKU 유효한 루트 키가 있습니다.|
|/?|에 대 한 도움말을 표시 **reg 언로드** 명령 프롬프트입니다.|

## <a name="remarks"></a>설명

다음 표에 대 한 반환 값은 **reg 언로드** 옵션이 있습니다.

|값|설명|
|-----|-----------|
|0|Success|
|1|실패|

## <a name="examples"></a>예

HKLM 파일에서 TempHive 하이브 언로드 작업을 입력 합니다.
```
REG UNLOAD HKLM\TempHive
```

> [!CAUTION]
> 편집 하지 마십시오 레지스트리 직접 대체 하지 않으면. 레지스트리 편집기의 성능이 저하, 하면 시스템이 손상 또는 Windows를 다시 설치 해야 할 수 있는 설정을 허용 표준 보호를 무시 합니다. 안전 하 게 제어판 또는 Microsoft Management Console (MMC)에서 프로그램을 사용 하 여 대부분의 레지스트리 설정을 변경할 수 있습니다. 레지스트리를 직접 편집 해야 하는 경우 먼저 백업 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [reg load 명령](reg-load.md)