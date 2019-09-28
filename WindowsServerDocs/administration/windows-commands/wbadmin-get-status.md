---
title: wbadmin 가져오기 상태
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2911b944-7b95-46aa-8c1e-1d55a2fcc94c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0270a29e557ec135301753dd66c1f5f2404a8acc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362392"
---
# <a name="wbadmin-get-status"></a>wbadmin 가져오기 상태



현재 실행 중인 백업 또는 복구 작업의 상태를 보고 합니다.

이 하위 명령을 사용 하려면의 구성원 이어야는 **Backup Operators** 그룹 또는 **관리자** 그룹 또는 사용자 받아야 적절 한 권한을 위임 합니다. 또한 실행 해야 **wbadmin** 상승된 된 명령 프롬프트에서. (관리자 권한 명령 프롬프트 마우스를 열려면 **Command Prompt**, 를 클릭 하 고 **관리자 권한으로 실행**.)

## <a name="syntax"></a>구문

```
wbadmin get status
```

## <a name="parameters"></a>매개 변수

이 하위 명령에 매개 변수가 없습니다.

## <a name="remarks"></a>설명

-   현재 백업 또는 복구 작업이 완료 될 때까지이 하위 명령이 중지 되지 않습니다. 명령 창을 닫은 경우에도 하위 명령이 계속 실행 됩니다.
-   현재 백업 또는 복구 작업을 중지 하려면 **wbadmin stop job** 하위 명령을 사용 합니다.

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [WBJob](https://technet.microsoft.com/library/jj902426.aspx) cmdlet