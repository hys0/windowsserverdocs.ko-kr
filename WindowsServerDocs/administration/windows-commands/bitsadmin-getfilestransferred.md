---
title: bitsadmin getfilestransferred
description: '**Bitsadmin getfilestransferred** 에 대 한 Windows 명령 항목-지정 된 작업에 대해 전송 된 파일 수를 검색 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e282815c-938b-4ac0-a09d-9baafb656dcb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d02d9d7bc216a5ad7ca922e716c368f64c4b9a44
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381605"
---
# <a name="bitsadmin-getfilestransferred"></a>bitsadmin getfilestransferred



지정 된 작업에 대해 전송 된 파일 수를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetFilesTransferred <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예와

다음 예제에서는 이름이 *Mydownloadjob*인 작업에서 전송 된 파일 수를 검색 합니다.
```
C:\>bitsadmin /GetFilesTransferred myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)