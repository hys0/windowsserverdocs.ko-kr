---
title: bitsadmin setnoprogresstimeout
description: 서비스에서 일시적인 오류가 발생 한 후 파일을 전송 하려고 시도 하는 시간 (초)을 설정 하는 bitsadmin setnoprogresstimeout에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7fac50d9-cc6b-46a4-a96f-fab751ee1756
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 544a6c73f29684bc4091ec05fa28016fbc718bb2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849356"
---
# <a name="bitsadmin-setnoprogresstimeout"></a>bitsadmin setnoprogresstimeout

첫 번째 일시적인 오류가 발생 한 후 BITS가 파일을 전송 하려고 시도 하는 시간 (초)을 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetNoProgressTimeout <Job> <TimeOutvalue>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|TimeOutvalue|시간 (초)로 표현 된 숫자입니다.|

## <a name="remarks"></a>주의

-   작업에 일시적인 오류가 발생 하면 없는 진행률 시간 제한 간격을 시작 합니다.
-   시간 제한 간격 중지 하거나 데이터의 바이트 성공적으로 전송 될 때 다시 설정 합니다.
-   없는 진행률 시간 제한 간격을 초과 하는 경우는 *TimeOutvalue*, 작업이 심각한 오류 상태에 오게 됩니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 없음 진행률 제한 시간 값을 설정 *myDownloadJob* 20 초
```
C:\>bitsadmin /SetNoProgressTimeout myDownloadJob 20
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)