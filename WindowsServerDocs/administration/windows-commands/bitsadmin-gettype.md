---
title: bitsadmin gettype
description: Windows 명령 항목에 대 한 **bitsadmin gettype** -지정된 된 된 작업의 작업 유형을 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ff0118f14acbf4e9f37c02e660bd9c7f6e8d0f70
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879434"
---
# <a name="bitsadmin-gettype"></a>bitsadmin gettype



지정된 된 작업의 작업 유형을 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetType <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

형식을 다운로드를 사용할 수 업로드-회신 또는 알 수 없는 업로드 합니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업에 대 한 작업 유형을 검색 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetType myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)