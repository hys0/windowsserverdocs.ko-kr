---
title: bitsadmin resume
description: '**Bitsadmin 다시 시작** 에 대 한 Windows 명령 항목-전송 큐에서 새 작업 또는 일시 중단 된 작업을 활성화 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c7540a9-a11a-4910-923a-2a2a61cbf11d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1393e959980b72de09c546ced763a506d334b56c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380775"
---
# <a name="bitsadmin-resume"></a>bitsadmin resume



전송 큐에 새로운 또는 일시 중단 된 작업을 활성화합니다.

## <a name="syntax"></a>구문

```
bitsadmin /Resume <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예와

다음 예제에서는 라는 작업을 다시 시작 *myDownloadJob*합니다.
```
C:\>bitsadmin /Resume myDownloadJob
```
추가 참조

[명령줄 구문 키](command-line-syntax-key.md)