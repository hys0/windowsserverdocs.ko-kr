---
title: type
description: 텍스트 파일의 내용을 표시 하는 형식에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c44fe905-a865-4c97-8cc5-fb95fec7d4d5
author: coreyp-at-msft
ms.author: coreyp
manager: dansimp
ms.openlocfilehash: d96aa066d9d9510d677d9750eb9e926a9d91cd65
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721219"
---
# <a name="type"></a>type

Windows 명령 셸에서 **형식** 은 텍스트 파일의 내용을 표시 하는 기본 제공 명령입니다. **형식** 명령을 사용 하 여 텍스트 파일을 수정 하지 않고 볼 수 있습니다.

PowerShell에서 **형식은** 파일의 콘텐츠도 표시 하 고 다른 구문을 사용 하 여 **[Get Content](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/get-content)** cmdlet에 대 한 기본 제공 별칭입니다.

## <a name="syntax"></a>구문

```
type [<Drive>:][<Path>]<FileName>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[\<드라이브>:] [\<경로>] \<파일 이름>|보려는 파일의 위치와 이름을 지정 합니다. 여러 파일 이름을 공백으로 구분 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   *파일* 이름에 공백이 포함 된 경우 공백을 포함 하는 파일 이름 처럼 따옴표로 묶습니다.
-   프로그램에 의해 생성 된 이진 파일 또는 파일을 표시 하는 경우 폼 피드 문자 및 이스케이프 시퀀스 기호를 포함 하 여 화면에 이상한 문자가 표시 될 수 있습니다. 이러한 문자는 이진 파일에 사용 되는 제어 코드를 나타냅니다. 일반적으로 **형식** 명령을 사용 하 여 이진 파일을 표시 하지 마십시오.

## <a name="examples"></a>예

이름이 a 3 인 파일의 콘텐츠를 표시 하려면 다음을 입력 합니다.
```
type holiday.mar 
```
한 번에 한 화면씩 이름이 지정 된 긴 파일의 콘텐츠를 표시 하려면 다음을 입력 합니다.
```
type holiday.mar | more 
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
