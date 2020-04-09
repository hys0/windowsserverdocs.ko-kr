---
title: regsvr32
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3345e964-7d3e-42b8-abeb-42ed6edfe2b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d3b775b0c49e4191a9fee6dc9e2e91f968142085
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836216"
---
# <a name="regsvr32"></a>regsvr32



레지스트리에 명령 구성 요소로.dll 파일을 등록합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
regsvr32 [/u] [/s] [/n] [/i[:cmdline]] <DllName>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/u|서버 등록 취소합니다.|
|/s|실행 **Regsvr32** 메시지를 표시 하지 않고 있습니다.|
|/n|실행 **Regsvr32** 호출 하지 않고 **DllRegisterServer**합니다. (필요는 **/i** 매개 변수입니다.)|
|/i:\<명령줄 >|선택적 명령줄 문자열을 전달 (*명령줄*)를 **DllInstall**합니다. 와 함께에서이 매개 변수를 사용 하는 경우는 **/u** 호출 매개 변수를 **DllUninstall**합니다.|
|\<DllName >|가 등록 하는.dll 파일의 이름입니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="examples"></a><a name=BKMK_examples></a>예와

.Dll Active Directory 스키마를 등록 하려면 다음을 입력 합니다.
```
regsvr32 schmmgmt.dll
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)