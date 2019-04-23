---
title: reg 복원
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a51f1c0c-969b-4b76-930a-c8bb14dea26e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0025a37ed8ca50b47e7750501a7362659b500537
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858774"
---
# <a name="reg-restore"></a>reg 복원



쓰기 저장 된 하위 키와 항목 레지스트리를 백업합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
Reg restore <KeyName> <FileName>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<KeyName>|복원 해야 하는 하위 키의 전체 경로 지정 합니다. 복원 작업이 로컬 컴퓨터 에서만 작동합니다. 키 이름에는 유효한 루트 키를 포함 해야 합니다. 유효한 루트 키가 있습니다. HKLM, HKCU, HKCR, HKU, and HKCC.|
|\<FileName>|콘텐츠를 레지스트리에 쓸 수 있는 파일의 경로 이름을 지정 합니다. 으로이 파일을 사전에 생성 되어야 합니다는 **reg 저장** .hiv 확장을 사용 하 여 작업 합니다.|
|/?|에 대 한 도움말을 표시 **reg 복원** 명령 프롬프트입니다.|

## <a name="remarks"></a>설명

-   레지스트리 항목을 편집 하기 전에 저장 된 부모 하위 키의 **reg 저장** 작업 합니다. 편집에 실패 하면 복원으로 원래 하위 키의 **reg 복원** 작업 합니다.
-   다음 표에 대 한 반환 값은 **reg 복원** 작업 합니다.

|값|Description|
|-----|-----------|
|0|성공|
|1|실패|

## <a name="BKMK_examples"></a>예제

HKLM\Software\Microsoft\ResKit 키로 NTRKBkUp.hiv 라는 파일을 복원 하는 키의 기존 내용을 덮어씁니다 다음을 입력 합니다.
```
REG RESTORE HKLM\Software\Microsoft\ResKit NTRKBkUp.hiv
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)