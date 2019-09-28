---
title: ver
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a9c6cd4-b67d-4b30-8c56-5f9798eafd2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e48b3b1061edf793c88693b3353753c6a4cedcfc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362717"
---
# <a name="ver"></a>ver



운영 체제 버전 번호를 표시합니다.

이 명령은 Windows 명령 프롬프트 (Cmd.exe)에서 지원 되지만 PowerShell에서는 지원 되지 않습니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
ver
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="BKMK_examples"></a>예와

명령 셸 (cmd.exe)에서 운영 체제의 버전 번호를 가져오려면 다음을 입력 합니다.

```
ver
```

Ver 명령은 PowerShell에서 작동 하지 않습니다. PowerShell에서 OS 버전을 가져오려면 다음을 입력 합니다.

```powershell
$PSVersionTable.BuildVersion
````


#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
