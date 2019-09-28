---
title: bitsadmin geterrorcount
description: '**Bitsadmin geterrorcount** 에 대 한 Windows 명령 항목-지정 된 작업에서 일시적인 오류가 발생 한 횟수를 검색 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8840ae78-52b0-4c7e-b592-0547359a237e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2e5aa64c0e080e946e84c0bf804527bb00cad70a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381623"
---
# <a name="bitsadmin-geterrorcount"></a>bitsadmin geterrorcount



지정 된 작업에서 일시적인 오류가 발생 한 횟수를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetErrorCount <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 오류 개수 정보를 검색 *Mydownloadjob*합니다.
```
C:\>bitsadmin /GetErrorCount myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)