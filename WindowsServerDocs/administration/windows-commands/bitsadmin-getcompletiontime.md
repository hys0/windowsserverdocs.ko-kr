---
title: bitsadmin getcompletiontime
description: '**Bitsadmin getcompletiontime** 에 대 한 Windows 명령 항목-작업에서 데이터 전송을 완료 한 시간을 검색 합니다.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 190467d5f3a7b7244ed0d7ab3b75d4cbbf56c8d5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381741"
---
# <a name="bitsadmin-getcompletiontime"></a>bitsadmin getcompletiontime



작업에서 데이터 전송을 완료 한 시간을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetCompletionTime <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예와

다음 예제에서는 *Mydownloadjob* 이라는 작업에서 데이터 전송을 완료 한 시간을 검색 합니다.
```
C:\>bitsadmin /GetCompletionTime myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)