---
title: 디스크 삭제
description: 디스크 삭제에 대 한 참조 항목으로, 디스크 목록에서 누락 된 동적 디스크를 삭제 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 44079900-e4ed-49d0-81e4-d652c38cd636
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad4888835c0bb1862344f104099b8b59027d1de9
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716761"
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

## <a name="examples"></a>예

디스크 목록에서 찾을 수 없는 동적 디스크를 삭제 하려면 다음을 입력 합니다.
```
delete disk
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

