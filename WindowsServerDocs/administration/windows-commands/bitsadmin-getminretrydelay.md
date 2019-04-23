---
title: bitsadmin getminretrydelay
description: Windows 명령 항목에 대 한 **bitsadmin getminretrydelay** -서비스에 일시적인 오류가 발생 하는 파일을 전송 하기 전에 대기 하는 초 단위로 시간 길이 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 54f0abab-c129-40ed-a603-50f464d26011
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2a6df9faab8340994ad9219a863ad8e50186ccd1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832204"
---
# <a name="bitsadmin-getminretrydelay"></a>bitsadmin getminretrydelay



시간 (초) 서비스는 일시적인 오류가 발생 하는 파일을 전송 하기 전에 대기 하는 기간을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetMinRetryDelay <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 검색 이라는 작업에 대 한 최소 재시도 지연 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetMinRetryDelay myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)