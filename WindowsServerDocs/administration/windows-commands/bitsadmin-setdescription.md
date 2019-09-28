---
title: bitsadmin setdescription
description: '**Bitsadmin setdescription** 에 대 한 Windows 명령 항목-지정 된 작업에 대 한 설명을 설정 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e46a5dd-4637-4a2e-b88f-d3f85b177db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d140ee9d575828a1a4d536073e468c9b4e56799f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380933"
---
# <a name="bitsadmin-setdescription"></a>bitsadmin setdescription



지정된 된 작업의 설명을 설정합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetDescription <Job> <Description>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|설명|작업에 설명 하는 데 사용 하는 텍스트입니다.|

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 설명을 검색 *Mydownloadjob*합니다.
```
C:\>bitsadmin /SetDescription myDownloadJob "Music Downloads"
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)