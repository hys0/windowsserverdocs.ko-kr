---
title: bitsadmin setcustomheaders
description: '**Bitsadmin setcustomheaders** 에 대 한 Windows 명령 항목-GET 요청에 사용자 지정 HTTP 헤더를 추가 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed926410-80d0-46ed-9a90-f752c164bb9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45e3a5178df69b84618966ca0fcd9cc1e6d0e449
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380644"
---
# <a name="bitsadmin-setcustomheaders"></a>bitsadmin setcustomheaders



GET 요청에 사용자 지정 HTTP 헤더를 추가 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetCustomHeaders <Job> <Header1> <Header2> <. . .>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|Header1 Header2 합니다. 을 선택합니다. 을 선택합니다.|작업에 대 한 사용자 지정 헤더|

## <a name="remarks"></a>설명

-   이 스위치는 HTTP 서버로 전송 된 GET 요청에 사용자 지정 HTTP 헤더를 추가 하는 데 사용 됩니다.

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 사용자 지정 HTTP 헤더 추가 *myDownloadJob*합니다.
```
C:\>bitsadmin / SetCustomHeaders myDownloadJob "Accept-encoding:deflate/gzip"
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)