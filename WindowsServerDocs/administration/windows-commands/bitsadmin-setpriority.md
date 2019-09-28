---
title: bitsadmin setpriority
description: '**Bitsadmin setpriority** 의 Windows 명령 항목-지정 된 작업의 우선 순위를 설정 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90788363-01a2-4d7c-a560-a3eba45b5e9e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 60564350928f917ca1861684e042304d5d380426
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380441"
---
# <a name="bitsadmin-setpriority"></a>bitsadmin setpriority



지정된 된 작업의 우선 순위를 설정합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetPriority <Job> <Priority>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|우선 순위|다음 값 중 하나입니다.</br>-전경</br>-높음</br>-표준</br>-낮음|

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 우선 순위 설정 *myDownloadJob* 정상입니다.
```
C:\>bitsadmin /SetPriority myDownloadJob NORMAL
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)