---
title: bitsadmin getcreationtime
description: Windows 명령 항목에 대 한 **bitsadmin getcreationtime** -지정된 된 된 작업에 대 한 생성 시간을 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: be409cb5-ce72-41d9-aafa-edd4e230fd14
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d8cc0f02933c6a890ae8bf40361d859ad508b319
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858474"
---
# <a name="bitsadmin-getcreationtime"></a>bitsadmin getcreationtime



지정된 된 된 작업에 대 한 생성 시간을 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetCreationTime <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 검색 이라는 작업에 대 한 생성 시간 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetCreationTime myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)