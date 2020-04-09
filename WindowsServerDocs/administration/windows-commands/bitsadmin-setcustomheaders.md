---
title: bitsadmin setcustomheaders
description: GET 요청에 사용자 지정 HTTP 헤더를 추가 하는 bitsadmin setcustomheaders에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ed926410-80d0-46ed-9a90-f752c164bb9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e5d97fae5f84637c80c3d1ef00aa36f09049bb17
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849616"
---
# <a name="bitsadmin-setcustomheaders"></a>bitsadmin setcustomheaders

GET 요청에 사용자 지정 HTTP 헤더를 추가 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetCustomHeaders <Job> <Header1> <Header2> <. . .>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|Header1 Header2 합니다. . .|작업에 대 한 사용자 지정 헤더|

## <a name="remarks"></a>주의

-   이 스위치는 HTTP 서버로 전송 된 GET 요청에 사용자 지정 HTTP 헤더를 추가 하는 데 사용 됩니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 사용자 지정 HTTP 헤더 추가 *myDownloadJob*합니다.
```
C:\>bitsadmin / SetCustomHeaders myDownloadJob Accept-encoding:deflate/gzip
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)