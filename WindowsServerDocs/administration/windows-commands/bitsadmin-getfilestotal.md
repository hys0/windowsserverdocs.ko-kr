---
title: bitsadmin getfilestotal
description: Windows 명령 항목에 대 한 **bitsadmin getfilestotal** -지정 된 작업의 파일 수를 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5de113e-f29c-4cd3-9392-0e300018d516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 21240cfa1f0fa1f8e8fc3d2acf83f5df80812816
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857464"
---
# <a name="bitsadmin-getfilestotal"></a>bitsadmin getfilestotal



지정 된 작업의 파일을 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetFilesTotal <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업에 포함 된 파일의 수를 검색 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetFilesTotal myDownloadJob
```

##

[명령줄 구문 키](command-line-syntax-key.md) 참고