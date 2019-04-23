---
title: bitsadmin getowner
description: Windows 명령 항목에 대 한 **bitsadmin getowner** -지정된 된 된 작업의 소유자를 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5203f84c-a879-4f31-ae3e-7ea74bd63ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1381bc1268b2b81e2bde18d0d8e17bd760345e0f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886714"
---
# <a name="bitsadmin-getowner"></a>bitsadmin getowner

표시 이름 또는 지정된 된 작업의 소유자의 GUID를 표시합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetOwner <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업에 대 한 소유자 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetOwner myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)