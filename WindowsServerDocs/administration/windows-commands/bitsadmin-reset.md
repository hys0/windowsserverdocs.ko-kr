---
title: bitsadmin reset
description: '**Bitsadmin reset** 에 대 한 Windows 명령 항목-현재 사용자가 소유 하는 전송 큐의 모든 작업을 취소 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e4f9d1d-072c-493f-8d7a-f6d713c3ef29
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: adc6b07a7b5d1414c733fe6a3ac05eba7cb3029e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380813"
---
# <a name="bitsadmin-reset"></a>bitsadmin reset

현재 사용자가 소유 하는 전송 큐에 모든 작업을 취소 합니다.

**Bitsadmin 1.5 및 이전 버전**: 관리자 권한이 있는 경우  을 **다시 설정**하면 큐에 있는 모든 작업이 취소 됩니다. /Sd 옵션은 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /Reset [/AllUsers]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|AllUsers|선택적-큐에 있는 모든 작업을 취소합니다.|

## <a name="remarks"></a>설명

사용 하려면 관리자 권한이 있어야 합니다.는 **AllUsers** 매개 변수입니다.

> [!NOTE]
> 관리자는 로컬 시스템에 의해 생성 된 작업을 재설정할 수 없습니다. 작업 스케줄러를 사용 하 여 로컬 시스템 자격 증명을 사용 하 여이 명령을 작업으로 예약 합니다.

## <a name="BKMK_examples"></a>예와

다음 예제에서는 현재 사용자에 대 한 전송 큐에 모든 작업을 취소합니다.
```
C:\>bitsadmin /Reset
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)