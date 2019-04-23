---
title: bitsadmin 캐시 및 setlimit
description: Windows 명령 항목에 대 한 **bitsadmin 캐시 및 setlimit** -캐시 크기 제한을 설정 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d0b72c5ec6c779fa4ce3fa038352836cd9456ac
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852594"
---
# <a name="bitsadmin-cache-and-setlimit"></a>bitsadmin 캐시 및 setlimit



캐시 크기 제한을 설정합니다.

## <a name="syntax"></a>구문

```
bitsadmin /Cache /SetLimit Percent
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|백분율|총 하드 디스크 공간의 백분율로 정의 된 캐시 제한...|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 캐시 크기 50%를 제한합니다.
```
C:\>bitsadmin /Cache /SetLimit 50 
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)