---
title: bitsadmin addfileset
description: Windows 명령 항목에 대 한 **bitsadmin addfileset** -지정된 된 된 작업에 하나 이상의 파일을 추가 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75466994-262f-4724-b14d-f813c5397675
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8f6ff32dfa6042272c68647477d77183ce9cb76
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889444"
---
# <a name="bitsadmin-addfileset"></a>bitsadmin addfileset

지정된 된 작업에 하나 이상의 파일을 추가합니다.

## <a name="syntax"></a>구문

```
bitsadmin /addfileset <Job> <TextFile>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|TextFile|텍스트 파일을 각 줄의 원격 및 로컬 파일 이름을 포함 합니다.</br>참고: 이름을은 공백으로 구분 됩니다. # ' 문자로 시작 하는 줄을 주석으로 처리 됩니다.|

## <a name="BKMK_examples"></a>예제

```
C:\>bitsadmin /addfileset files.txt
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)