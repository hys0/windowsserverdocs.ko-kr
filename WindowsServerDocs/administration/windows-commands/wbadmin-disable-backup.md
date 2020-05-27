---
title: wbadmin 백업 사용 안 함
description: 기존 예약 된 매일 백업 실행을 중지 하는 wbadmin disable backup에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5176cbd9-0696-4b3f-9c35-272dd84f7898
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6bc211946c908b44b196995a9e5000d6ff3b7f82
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821423"
---
# <a name="wbadmin-disable-backup"></a>wbadmin 백업 사용 안 함



기존 예약 된 매일 백업의 실행을 중지 합니다.

예약된 된 매일 백업을 사용 하지 않으려면,의 구성원 이어야는 **관리자** 그룹 또는 사용자 받아야 적절 한 권한을 위임 합니다. 또한 실행 해야 **wbadmin** 상승된 된 명령 프롬프트에서. (관리자 권한 명령 프롬프트를 열려면 **명령 프롬프트** 를 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다.)

## <a name="syntax"></a>구문

```
wbadmin disable backup
[-quiet]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-quiet|사용자에 게 하위 명령 프롬프트 없이 실행 됩니다.|

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)