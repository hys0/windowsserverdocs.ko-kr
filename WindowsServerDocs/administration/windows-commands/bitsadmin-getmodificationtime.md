---
title: bitsadmin getmodificationtime
description: Windows 명령 항목에 대 한 **bitsadmin getmodificationtime** -검색의 마지막 작업이 수정 된 시간 또는 데이터 전송 했습니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e543945e-92c4-491e-8c2d-344f8a3e342d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4257f0ae4868b2f18221ab99268384f778c4bbbe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837024"
---
# <a name="bitsadmin-getmodificationtime"></a>bitsadmin getmodificationtime



검색 작업이 수정 된 마지막 시간 또는 데이터 전송 했습니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetModificationTime <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 검색 이라는 작업에 대 한 마지막 수정된 시간이 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetModificationTime myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)