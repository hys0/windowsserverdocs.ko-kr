---
title: bitsadmin getbytestotal
description: Windows 명령 항목에 대 한 **bitsadmin getbytestotal** -지정된 된 된 작업의 크기를 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 784e0bfa-7b09-4262-9104-adbc9beb479b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d7a33b02dbdea63e87bd8ce56a2d50e15ca19d05
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882864"
---
# <a name="bitsadmin-getbytestotal"></a>bitsadmin getbytestotal



지정된 된 작업의 크기를 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetBytesTotal <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업의 크기를 검색 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetBytesTotal myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)