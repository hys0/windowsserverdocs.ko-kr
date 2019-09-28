---
title: bitsadmin cancel
description: '**Bitsadmin cancel** 의 Windows 명령 항목-전송 큐에서 작업을 제거 하 고 작업과 연결 된 모든 임시 파일을 삭제 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7374b544-6a16-4d3e-872c-dcf4c02ad89d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 77e46d787359af43a37faba5d844bfec09730454
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381800"
---
# <a name="bitsadmin-cancel"></a>bitsadmin cancel

작업 전송 큐에서 제거 하 고 작업과 연결 된 모든 임시 파일을 삭제 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /cancel <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예와

다음 예제에서는 제거 된 *myDownloadJob* 전송 큐에서 작업 합니다.
```
C:\>bitsadmin /cancel myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)