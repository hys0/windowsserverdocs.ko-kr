---
title: bitsadmin 캐시 및 삭제
description: Windows 명령 항목에 대 한 **bitsadmin 캐시 및 삭제** -특정 캐시 엔트리를 삭제 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 22540273-55a5-46ea-869b-6df2aa6808a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 63b82cbbadebf2c4e36f2c76076b329787d7b1b5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852514"
---
# <a name="bitsadmin-cache-and-delete"></a>bitsadmin 캐시 및 삭제



특정 캐시 엔트리를 삭제합니다.

## <a name="syntax"></a>구문

```
bitsadmin /Cache /Delete RecordID 
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|RecordID|캐시 항목에 연결 된 GUID입니다.|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 {6511FB02-E195-40A2-B595-E8E2F8F47702}의 RecordID 캐시 항목을 삭제 합니다.
```
C:\>bitsadmin /Cache /Delete {6511FB02-E195-40A2-B595-E8E2F8F47702} 
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)