---
title: bitsadmin getpriority
description: Windows 명령 항목에 대 한 **bitsadmin getpriority** -지정된 된 작업의 우선 순위를 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 6be2461ed87b75144367b1bd74376381e4674b66
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841444"
---
# <a name="bitsadmin-getpriority"></a>bitsadmin getpriority

지정된 된 작업의 우선 순위를 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetPriority <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

우선 순위입니다 **전경**, **높은**를 **보통**, **낮은**, 또는 **알 수 없는**합니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업에 대 한 우선 순위를 검색 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetPriority myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
