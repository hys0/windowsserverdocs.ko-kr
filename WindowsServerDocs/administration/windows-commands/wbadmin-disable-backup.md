---
title: wbadmin 백업 사용 안 함
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5176cbd9-0696-4b3f-9c35-272dd84f7898
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 405bbb3c07206032f1a9e3039c563e7c842e362e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362486"
---
# <a name="wbadmin-disable-backup"></a>wbadmin 백업 사용 안 함



기존 예약 된 매일 백업의 실행을 중지 합니다.

예약된 된 매일 백업을 사용 하지 않으려면,의 구성원 이어야는 **관리자** 그룹 또는 사용자 받아야 적절 한 권한을 위임 합니다. 또한 실행 해야 **wbadmin** 상승된 된 명령 프롬프트에서. (관리자 권한 명령 프롬프트 마우스를 열려면 **Command Prompt** 클릭 하 고 **관리자 권한으로 실행**.)

## <a name="syntax"></a>구문

```
wbadmin disable backup
[-quiet]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-quiet|사용자에 게 하위 명령 프롬프트 없이 실행 됩니다.|

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)