---
title: retain
description: '* * * *에 대 한 참조 문서'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eeab0aef-2ba5-441a-a10d-bbef6f0d7e3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 958ee0de7bd69c9391407ec6f4a832e1262746a2
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933069"
---
# <a name="retain"></a>retain



시스템 볼륨 나 기존의 동적 단순 볼륨으로 부팅을 사용 하도록 준비 합니다.

## <a name="syntax"></a>구문

```
retain
```

## <a name="remarks"></a>설명

-   이 명령은 마스터 부트 레코드 (MBR) 동적 디스크의 마스터 부트 레코드에 파티션 항목을 만듭니다.
-   GUID 파티션 테이블 (GPT) 동적 디스크에서이 명령은 GUID 파티션 테이블의 파티션 항목을 만듭니다.

## <a name="additional-references"></a>추가 참조

