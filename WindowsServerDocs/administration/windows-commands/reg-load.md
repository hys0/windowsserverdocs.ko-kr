---
title: reg 로드
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3b0b2b1b-f510-4108-9e9d-7057e924aa6e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: db661e311e3fe8c393750716de5dab375e7817f4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384703"
---
# <a name="reg-load"></a>reg 로드



쓰기 레지스트리에 하위 키와 다른 하위 키에 대 한 항목을 저장 합니다. 문제를 해결 하거나 레지스트리 항목을 편집에 사용 되는 임시 파일에 사용 됩니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
reg load KeyName FileName
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<KeyName >|로드할 하위 키의 전체 경로 지정 합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름을 *KeyName*의 일부로 \\\\ComputerName\) 형식으로 포함 합니다. ComputerName을 \\\\생략 하면 작업이 로컬 컴퓨터를 기본값으로 설정 됩니다. *KeyName* 유효한 루트 키를 포함 해야 합니다. 로컬 컴퓨터에 대 한 유효한 루트 키: HKLM, HKCU, HKCR, HKU, 및 HKCC 합니다. 원격 컴퓨터를 지정 하는 경우 올바른 루트 키가: HKLM 및 HKU 합니다.|
|\<파일 이름 >|로드할 파일의 경로 이름을 지정 합니다. 이 파일을 사용 하 여 사전에 만들 수 있어야는 **reg 저장** 작업과.hiv 확장 합니다.|
|/?|에 대 한 도움말을 표시 **reg 부하** 명령 프롬프트입니다.|

## <a name="remarks"></a>설명

다음 표에 대 한 반환 값은 **reg 부하** 작업 합니다.

|값|설명|
|-----|-----------|
|0|Success|
|1|실패|

## <a name="BKMK_examples"></a>예와

키 만듭니다 TempHive.hiv 라는 파일을 로드 하려면 다음을 입력 합니다.
```
REG LOAD HKLM\TempHive TempHive.hiv
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)