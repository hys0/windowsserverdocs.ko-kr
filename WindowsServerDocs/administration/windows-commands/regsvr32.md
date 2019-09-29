---
title: regsvr32
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3345e964-7d3e-42b8-abeb-42ed6edfe2b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 444af0ccf7c9bbe21c013f32b396997b7cb2e00f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371634"
---
# <a name="regsvr32"></a>regsvr32



레지스트리에 명령 구성 요소로.dll 파일을 등록합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
regsvr32 [/u] [/s] [/n] [/i[:cmdline]] <DllName>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/u|서버 등록 취소합니다.|
|/s|실행 **Regsvr32** 메시지를 표시 하지 않고 있습니다.|
|/n|실행 **Regsvr32** 호출 하지 않고 **DllRegisterServer**합니다. (필요는 **/i** 매개 변수입니다.)|
|/i: \<cmdline >|선택적 명령줄 문자열을 전달 (*명령줄*)를 **DllInstall**합니다. 와 함께에서이 매개 변수를 사용 하는 경우는 **/u** 호출 매개 변수를 **DllUninstall**합니다.|
|@no__t 0DllName >|가 등록 하는.dll 파일의 이름입니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="BKMK_examples"></a>예와

.Dll Active Directory 스키마를 등록 하려면 다음을 입력 합니다.
```
regsvr32 schmmgmt.dll
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)