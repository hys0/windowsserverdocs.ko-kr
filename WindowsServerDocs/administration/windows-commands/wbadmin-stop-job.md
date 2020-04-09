---
title: wbadmin 중지 작업
description: Wbadmin stop job에 대 한 Windows 명령 항목-현재 실행 중인 백업 또는 복구 작업을 취소 합니다. 취소 된 작업을 다시 시작할 수 없습니다-시작 부분에서 취소 된 백업 또는 복구 작업을 다시 실행 해야 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3b83b398-39c7-4410-bf17-5c1fb1a4f46d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a00b4a93e0aaa954f8f07adae825a4f582c5581
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829486"
---
# <a name="wbadmin-stop-job"></a>wbadmin 중지 작업



현재 실행 중인 백업 또는 복구 작업을 취소 합니다. 취소 된 작업을 다시 시작할 수 없습니다-시작 부분에서 취소 된 백업 또는 복구 작업을 다시 실행 해야 합니다.

이 하위 명령 사용 하 여 백업 또는 복구 작업을 중지 하려면의 구성원 이어야는 **백업 운영자** 그룹 또는 **관리자** 그룹 또는 사용자 받아야 적절 한 권한을 위임 합니다. 또한 실행 해야 **wbadmin** 상승된 된 명령 프롬프트에서. (관리자 권한 명령 프롬프트 마우스를 열려면 **Command Prompt** 클릭 하 고 **관리자 권한으로 실행**.)

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

-   - [명령줄 구문 키](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)