---
title: bitsadmin takeownership
description: '**Bitsadmin takeownership** 에 대 한 Windows 명령 항목-관리자 권한이 있는 사용자가 지정 된 작업의 소유권을 가져올 수 있습니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ea0ce7cb-440a-498f-a3ef-8368fa43e399
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1f0d0610b2ba6437f6fdd41bf1b875993cf11f2a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380361"
---
# <a name="bitsadmin-takeownership"></a>bitsadmin takeownership



관리자 권한으로는 사용자가 지정된 된 작업의 소유권을 가져올 수 있습니다.

## <a name="syntax"></a>구문

```
bitsadmin /TakeOwnership <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업의 소유권을 갖습니다 *myDownloadJob*합니다.
```
C:\>bitsadmin /TakeOwnership myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)