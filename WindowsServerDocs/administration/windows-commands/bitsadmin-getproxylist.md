---
title: bitsadmin getproxylist-지정된 된 된 작업에 대 한 프록시 목록을 검색 합니다.
description: Windows 명령 항목에 대 한 **bitsadmin getproxylist** -지정된 된 된 작업에 대 한 프록시 목록을 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eebfa727-d8f1-4ae3-9382-6d8ffe8c3df3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e8c3ffb1e425552cda5b14a00287817ace77a90f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840514"
---
# <a name="bitsadmin-getproxylist"></a>bitsadmin getproxylist

지정된 된 작업에 대 한 프록시 목록을 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetProxyList <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

프록시 목록에는 사용할 프록시 서버의 목록이입니다. 목록은은 쉼표로 구분 됩니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업에 대 한 프록시 목록을 검색 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetProxyList myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)