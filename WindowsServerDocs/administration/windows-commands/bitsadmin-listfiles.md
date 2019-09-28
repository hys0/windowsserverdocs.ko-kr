---
title: bitsadmin listfiles
description: '**Bitsadmin listfiles** 에 대 한 Windows 명령 항목-지정 된 작업의 파일을 나열 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad0d1eaa-3bd8-45e5-8f72-4da7366f0d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 43823e4f5c8443396e21405f22ba8b3c5687da44
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381056"
---
# <a name="bitsadmin-listfiles"></a>bitsadmin listfiles



지정된 된 작업의 파일을 나열 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /ListFiles <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예와

다음 예제에서는 라는 작업에 대 한 파일의 목록을 검색 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetNotifyFlags myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)