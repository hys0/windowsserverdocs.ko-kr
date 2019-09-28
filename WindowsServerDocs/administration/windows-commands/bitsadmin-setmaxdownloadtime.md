---
title: bitsadmin setmaxdownloadtime
description: '**Bitsadmin setmaxdownloadtime** 에 대 한 Windows 명령 항목-다운로드 제한 시간 (초)을 설정 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16b96cf1-5738-415c-9b9d-c4ea8d5e4fec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 985453de5bd2f4a06b5635ae5b0a9794d30175b0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380562"
---
# <a name="bitsadmin-setmaxdownloadtime"></a>bitsadmin setmaxdownloadtime



다운로드 제한 시간을 초 단위로 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetMaxDownloadTime <Job> <Timeout>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|시간 제한|제한 시간 (초)|

## <a name="remarks"></a>설명

-   해당 사항 없음

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 제한 시간 설정 *myDownloadJob* 으로 10 초로 설정 합니다.
```
C:\>bitsadmin /SetMaxDownloadTime myDownloadJob 10
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)