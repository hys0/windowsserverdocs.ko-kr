---
title: bitsadmin getcompletiontime
description: Windows 명령 항목에 대 한 **bitsadmin getcompletiontime** -작업 데이터 전송을 완료 했습니다.는 시간을 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a4b3c1c-9832-4724-86b2-cce3c01bfa28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3790a91c4b347b982c0f0a023d5977a8d6cd1f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857384"
---
# <a name="bitsadmin-getcompletiontime"></a>bitsadmin getcompletiontime



작업 데이터 전송을 완료 했습니다.는 시간을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetCompletionTime <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 검색 이라는 작업 시간 *myDownloadJob* 데이터 전송을 완료 했습니다.
```
C:\>bitsadmin /GetCompletionTime myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)