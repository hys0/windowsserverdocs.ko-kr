---
title: bitsadmin setnoprogresstimeout
description: '**Bitsadmin setnoprogresstimeout** 에 대 한 Windows 명령 항목-일시적 오류가 발생 한 후 서비스가 파일을 전송 하려고 시도 하는 시간 (초)을 설정 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7fac50d9-cc6b-46a4-a96f-fab751ee1756
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 761d0d76a2c70af9d4ad68aa564c1a9816691d0d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380504"
---
# <a name="bitsadmin-setnoprogresstimeout"></a>bitsadmin setnoprogresstimeout

첫 번째 일시적인 오류가 발생 한 후 BITS가 파일을 전송 하려고 시도 하는 시간 (초)을 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetNoProgressTimeout <Job> <TimeOutvalue>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|TimeOutvalue|시간 (초)로 표현 된 숫자입니다.|

## <a name="remarks"></a>설명

-   작업에 일시적인 오류가 발생 하면 없는 진행률 시간 제한 간격을 시작 합니다.
-   시간 제한 간격 중지 하거나 데이터의 바이트 성공적으로 전송 될 때 다시 설정 합니다.
-   없는 진행률 시간 제한 간격을 초과 하는 경우는 *TimeOutvalue*, 작업이 심각한 오류 상태에 오게 됩니다.

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 없음 진행률 제한 시간 값을 설정 *myDownloadJob* 20 초
```
C:\>bitsadmin /SetNoProgressTimeout myDownloadJob 20
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)