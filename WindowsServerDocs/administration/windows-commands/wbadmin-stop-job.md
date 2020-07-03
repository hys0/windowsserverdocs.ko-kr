---
title: wbadmin stop job
description: 현재 실행 중인 백업 또는 복구 작업을 취소 하는 wbadmin stop job에 대 한 참조 문서입니다. 취소 된 작업을 다시 시작할 수 없습니다-시작 부분에서 취소 된 백업 또는 복구 작업을 다시 실행 해야 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3b83b398-39c7-4410-bf17-5c1fb1a4f46d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2c6961b1fae425d06577fce3a93dca6262dd7127
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930886"
---
# <a name="wbadmin-stop-job"></a>wbadmin stop job



현재 실행 중인 백업 또는 복구 작업을 취소 합니다. 취소 된 작업을 다시 시작할 수 없습니다-시작 부분에서 취소 된 백업 또는 복구 작업을 다시 실행 해야 합니다.

이 하위 명령 사용 하 여 백업 또는 복구 작업을 중지 하려면의 구성원 이어야는 **백업 운영자** 그룹 또는 **관리자** 그룹 또는 사용자 받아야 적절 한 권한을 위임 합니다. 또한 실행 해야 **wbadmin** 상승된 된 명령 프롬프트에서. (관리자 권한 명령 프롬프트를 열려면 **명령 프롬프트** 를 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다.)

## <a name="syntax"></a>구문

```
wbadmin stop job
[-quiet]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-quiet|사용자에 게 하위 명령 프롬프트 없이 실행 됩니다.|

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)