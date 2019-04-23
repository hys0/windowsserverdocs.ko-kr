---
title: bitsadmin list
description: Windows 명령 항목에 대 한 **bitsadmin 목록** -현재 사용자가 소유 하 고 전송 작업을 나열 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1416965e-e0e6-49cf-b1d4-b286d3cf8716
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f0b88001b9c4ae01b57006ffeef66dec0348ca77
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873864"
---
# <a name="bitsadmin-list"></a>bitsadmin list



현재 사용자가 소유 하 고 전송 작업을 나열 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /List [/allusers][/verbose]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/ Allusers|선택적-모든 사용자에 대 한 작업을 나열 합니다.|
|/ 세부 정보 표시|선택적-각 작업에 대 한 자세한 정보를 제공 합니다.|

## <a name="remarks"></a>설명

/Allusers 매개 변수를 사용 하려면 관리자 권한이 있어야 합니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 현재 사용자가 소유한 작업에 대 한 정보를 검색 합니다.
```
C:\>bitsadmin /List 
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)