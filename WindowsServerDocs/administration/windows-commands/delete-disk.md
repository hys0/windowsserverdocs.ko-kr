---
title: 디스크 삭제
description: 디스크 삭제에 대 한 Windows 명령 항목. 디스크 목록에서 누락 된 동적 디스크를 삭제 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 44079900-e4ed-49d0-81e4-d652c38cd636
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1a767e0689d5fbabb193df37528a0909ab63a1ab
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846656"
---
# <a name="delete-disk"></a>디스크 삭제

디스크 목록에서 찾을 수 없는 동적 디스크를 삭제합니다.

이 명령을 사용 하는 방법에 대 한 지침은 [누락 된 동적 디스크 제거](https://go.microsoft.com/fwlink/?LinkId=207055) (https://go.microsoft.com/fwlink/?LinkId=207055)를 참조 하세요.

## <a name="syntax"></a>구문

```
delete disk [noerr] [override]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|noerr|스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|
|override|Diskpart 명령을으로 디스크에서 단순 볼륨을 모두 삭제할 수 있습니다. 디스크에 미러 볼륨의 절반을 디스크에 미러의 절반 삭제 됩니다. 디스크가 RAID-5 볼륨의 구성원 인 경우 delete disk override 명령이 실패 합니다.|

## <a name="examples"></a><a name=BKMK_examples></a>예와

디스크 목록에서 찾을 수 없는 동적 디스크를 삭제 하려면 다음을 입력 합니다.
```
delete disk
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

