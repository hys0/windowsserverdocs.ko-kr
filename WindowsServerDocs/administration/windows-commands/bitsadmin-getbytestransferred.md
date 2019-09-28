---
title: bitsadmin getbytestransferred
description: '**Bitsadmin getbytestransferred** 에 대 한 Windows 명령 항목-지정 된 작업에 대해 전송 된 바이트 수를 검색 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47bbf184-e06f-4be0-b2ba-d32b10d82002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f690fa55a4ac5ae31223794c5e7eabc0c982c2ce
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381728"
---
# <a name="bitsadmin-getbytestransferred"></a>bitsadmin getbytestransferred



지정 된 작업에 대해 전송 된 바이트 수를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetBytesTransferred <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예와

다음 예에서는 이름이 *Mydownloadjob*인 작업에 대해 전송 된 바이트 수를 검색 합니다.
```
C:\>bitsadmin /GetBytesTransferred myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)