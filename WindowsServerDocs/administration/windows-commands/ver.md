---
title: ver
description: 운영 체제 버전 번호를 표시 하는 ver에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5a9c6cd4-b67d-4b30-8c56-5f9798eafd2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7050dddda6cc27c50980f2e44f40e1f682c1d375
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720308"
---
# <a name="ver"></a>ver



운영 체제 버전 번호를 표시합니다.

이 명령은 Windows 명령 프롬프트 (Cmd.exe)에서 지원 되지만 PowerShell에서는 지원 되지 않습니다.



## <a name="syntax"></a>구문

```
ver
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="examples"></a>예

명령 셸 (cmd.exe)에서 운영 체제의 버전 번호를 가져오려면 다음을 입력 합니다.

```
ver
```

Ver 명령은 PowerShell에서 작동 하지 않습니다. PowerShell에서 OS 버전을 가져오려면 다음을 입력 합니다.

```powershell
$PSVersionTable.BuildVersion
````


## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
