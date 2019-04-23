---
title: bitsadmin getdisplayname
description: Windows 명령 항목에 대 한 **bitsadmin getdisplayname** -지정된 된 된 작업의 표시 이름을 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5c0e76c-4cc6-42d8-ac30-30bf3dc11b9b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c1ef16f54b7b825e4293a3870d8181985b83843b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857604"
---
# <a name="bitsadmin-getdisplayname"></a>bitsadmin getdisplayname



지정된 된 작업의 표시 이름을 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetDisplayName <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 검색 이라는 작업에 대 한 표시 이름 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetDisplayName myDownloadJob
```
추가 참조

[명령줄 구문 키](command-line-syntax-key.md)