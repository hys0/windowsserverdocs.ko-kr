---
title: bitsadmin getreplydata
description: Windows 명령 항목에 대 한 **bitsadmin getreplydata** -16 진수 형식으로 서버 응답 데이터를 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 819f97d5-b255-4b2d-9f63-0daa73915434
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 78d70a44d6881568c8d92db145fdf22a260ee8af
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883824"
---
# <a name="bitsadmin-getreplydata"></a>bitsadmin getreplydata

16 진수 형식에는 서버 응답 데이터를 검색합니다.

**1.2 및 이전 비트**: 지원되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetReplyData <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

업로드-회신 작업에 대해서만 유효 합니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업에 대 한 회신 데이터를 검색 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetReplyData myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)