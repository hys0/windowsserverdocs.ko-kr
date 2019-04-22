---
title: mklink
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ce4df22-2dbc-48fc-9c16-b721ae85f857
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eabbf159a64ab5df7f45ece390d0c2fdb9956b80
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826334"
---
# <a name="mklink"></a>mklink
기호화 된 링크를 만듭니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
mklink [[/d] | [/h] | [/j]] <Link> <Target>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/d|디렉터리 기호화 된 링크를 만듭니다. 기본적으로 **mklink** 파일 바로 가기 링크를 만듭니다.|
|/h|대신 바로 가기 링크를 하드 링크를 만듭니다.|
|/j|디렉터리 연결을 만듭니다.|
|\<링크 >|생성 중인 기호화 된 링크의 이름을 지정 합니다.|
|\<Target>|새 바로 가기 링크를 참조 하는 경로 (상대 또는 절대)를 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="BKMK_examples"></a>예제

루트 디렉터리에서 MyDocs \Users\User1\Documents 디렉터리 라는 기호화 된 링크를 만들려면 다음을 입력 합니다.
```
mklink /d \MyDocs \Users\User1\Documents
```
## <a name="additional-references"></a>추가 참조
-   [New-Item](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/new-item?view=powershell-6)
