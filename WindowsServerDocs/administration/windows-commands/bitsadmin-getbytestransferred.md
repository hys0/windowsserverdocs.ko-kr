---
title: bitsadmin getbytestransferred
description: Windows 명령 항목에 대 한 **bitsadmin getbytestransferred** -지정된 된 된 작업에 대해 전송 된 바이트 수를 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47bbf184-e06f-4be0-b2ba-d32b10d82002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cce2c051af169385c43fdff4efdeff46d8422926
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814614"
---
# <a name="bitsadmin-getbytestransferred"></a>bitsadmin getbytestransferred



지정된 된 된 작업에 대 한 전송 된 바이트 수를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetBytesTransferred <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 검색 이라는 작업에 대해 전송 된 바이트 수가 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetBytesTransferred myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)