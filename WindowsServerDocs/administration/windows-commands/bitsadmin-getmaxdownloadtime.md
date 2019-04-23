---
title: bitsadmin getmaxdownloadtime
description: Windows 명령 항목에 대 한 **bitsadmin getmaxdownloadtime** -시간 (초)의 다운로드 제한 시간을 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdce64f6-7125-489d-be3c-4af1dfc8c46a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 868f7ac58a69c067681bf0597524fbaa5a25984f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842424"
---
#<a name="bitsadmin-getmaxdownloadtime"></a>bitsadmin getmaxdownloadtime

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다운로드 제한 시간 (초)을 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetMaxDownloadtime <Job> 
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

-   N\/A

## <a name="BKMK_examples"></a>예제
다음 예제에서는 명명 된 작업에 대 한 최대 다운로드 시간을 가져옵니다 *myDownloadJob* (초)에서입니다.

```
C:\>bitsadmin /GetMaxDownloadtime myDownloadJob
```

## <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)


