---
title: bitsadmin getmodificationtime
description: '**Bitsadmin getmodificationtime** 에 대 한 Windows 명령 항목-작업이 마지막으로 수정 되었거나 데이터가 성공적으로 전송 된 시간을 검색 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e543945e-92c4-491e-8c2d-344f8a3e342d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 48b4d252ce6161b288726190f41f08c64efdbcf2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381532"
---
# <a name="bitsadmin-getmodificationtime"></a>bitsadmin getmodificationtime



작업이 마지막으로 수정 되었거나 데이터가 성공적으로 전송 된 시간을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetModificationTime <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예와

다음 예제에서는 이름이 *Mydownloadjob*인 작업에 대해 마지막으로 수정한 시간을 검색 합니다.
```
C:\>bitsadmin /GetModificationTime myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)