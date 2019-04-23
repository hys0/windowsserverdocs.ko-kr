---
title: reg 저장
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b326482b-c8af-467d-a20c-0481eeda3d5c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2a46dfe081421ed727bd7ffeeab364e6c23dd801
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841084"
---
# <a name="reg-save"></a>reg 저장



지정된 된 파일에 지정 된 하위 키, 항목 및 레지스트리 값의 복사본을 저장합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
reg save <KeyName> <FileName> [/y]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<KeyName>|하위 키의 전체 경로 지정합니다. 원격 컴퓨터를 지정 하는 것에 대 한 컴퓨터 이름을 포함 합니다 (형식에서 \\ \\ComputerName\) 의 일부로 합니다 *KeyName*합니다. 생략 \\ \\ComputerName\ 하면 로컬 컴퓨터에 기본 작업이 있습니다. *KeyName* 유효한 루트 키를 포함 해야 합니다. 로컬 컴퓨터에 대 한 유효한 루트 키 다음과 같습니다. HKLM, HKCU, HKCR, HKU, and HKCC. 원격 컴퓨터를 지정 하는 경우 유효한 루트 키 다음과 같습니다. HKLM 및 HKU 합니다.|
|\<FileName>|생성 되는 파일의 경로 이름을 지정 합니다. 지정 된 경로가 현재 경로가 사용 됩니다.|
|/y|기존 파일 이름으로 덮어씁니다 *FileName* 확인 메시지를 표시 하지 않고 있습니다.|
|/?|에 대 한 도움말을 표시 **reg 저장** 명령 프롬프트입니다.|

## <a name="remarks-optional-section"></a>주의 \<선택적인 섹션 >

-   다음 표에 대 한 반환 값은 **reg 저장** 작업 합니다.

|값|Description|
|-----|-----------|
|0|성공|
|1|실패|
-   레지스트리 항목을 편집 하기 전에 저장 된 부모 하위 키의 **reg 저장** 작업 합니다. 편집에 실패 하면 복원으로 원래 하위 키의 **reg 복원** 작업 합니다.

## <a name="BKMK_examples"></a>예제

현재 폴더에 hive MyApp 중인 라는 파일을 저장 하려면 다음을 입력 합니다.
```
REG SAVE HKLM\Software\MyCo\MyApp AppBkUp.hiv
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)