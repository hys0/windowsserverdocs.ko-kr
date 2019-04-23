---
title: type
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c44fe905-a865-4c97-8cc5-fb95fec7d4d5
author: coreyp-at-msft
ms.author: coreyp
manager: dansimp
ms.openlocfilehash: 4ceb7365d34a2aeca21d1a699730a589f98fd549
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887404"
---
# <a name="type"></a>type


Windows 명령 셸에서 **형식** 텍스트 파일의 내용을 표시 하는 명령에서 기본 제공 됩니다. 사용 된 **형식** 수정 하지 않고 텍스트 파일을 보려면 명령입니다.


PowerShell에서 **형식** 별칭을 기본 제공 되는 **[Get-content](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/get-content)** 같지만 서로 다른 구문을 파일의 내용을 표시 하는 cmdlet입니다.


Windows 명령 셸 (Cmd.exe) 내에서이 명령을 사용 하는 방법의 예제를 참조 하세요 [예제](#BKMK_examples)합니다.

## <a name="syntax"></a>구문

```
type [<Drive>:][<Path>]<FileName>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[\<Drive>:][\<Path>]\<FileName>|확인 하려는 파일의 이름과 위치를 지정 합니다. 여러 파일 이름을 공백으로 구분 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   하는 경우 *FileName* 에 공백이 있는 경우 (예를 들어 "파일 이름 포함 된 Spaces.txt") 인용 부호로 묶어야 합니다.
-   이진 파일 또는 프로그램에서 만든 파일을 표시 하는 경우에 용지 공급 문자 및 이스케이프 시퀀스 기호를 포함 하 여 화면에서 이상한 문자가 나타날 수 있습니다. 이러한 문자는 이진 파일에 사용 되는 제어 코드를 나타냅니다. 일반적으로 사용 하 여를 방지 합니다 **형식** 이진 파일을 표시 하는 명령입니다.

## <a name="BKMK_examples"></a>예제

Holiday.mar 라는 파일의 내용을 표시 하려면 다음을 입력 합니다.
```
type holiday.mar 
```
한 번에 한 화면 Holiday.mar 라는 긴 파일의 내용을 표시 하려면 다음을 입력 합니다.
```
type holiday.mar | more 
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
