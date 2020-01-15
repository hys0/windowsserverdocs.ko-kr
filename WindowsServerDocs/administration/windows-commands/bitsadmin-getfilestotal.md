---
title: bitsadmin getfilestotal
description: '**Bitsadmin getfilestotal** 에 대 한 Windows 명령 항목-지정 된 작업의 파일 수를 검색 합니다.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: e5c28d8e970bd7db896073bf8cddb168ffe9deff
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75946841"
---
# <a name="bitsadmin-getfilestotal"></a>bitsadmin getfilestotal



지정 된 작업의 파일 수를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetFilesTotal <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업에 포함 된 파일의 수를 검색 *Mydownloadjob*합니다.
```
C:\>bitsadmin /GetFilesTotal myDownloadJob
```

## <a name="see-also"></a>참고 항목

[명령줄 구문 키](command-line-syntax-key.md)
