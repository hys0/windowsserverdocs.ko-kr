---
title: wbadmin 가져오기 상태
description: Wbadmin get status에 대 한 Windows 명령 항목은 현재 실행 중인 백업 또는 복구 작업의 상태를 보고 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2911b944-7b95-46aa-8c1e-1d55a2fcc94c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8ebf1a078632f78dc8d58c232550345f0de78f2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829746"
---
# <a name="wbadmin-get-status"></a>wbadmin 가져오기 상태



현재 실행 중인 백업 또는 복구 작업의 상태를 보고 합니다.

이 하위 명령을 사용 하려면의 구성원 이어야는 **Backup Operators** 그룹 또는 **관리자** 그룹 또는 사용자 받아야 적절 한 권한을 위임 합니다. 또한 실행 해야 **wbadmin** 상승된 된 명령 프롬프트에서. (관리자 권한 명령 프롬프트 마우스를 열려면 **Command Prompt**, 를 클릭 하 고 **관리자 권한으로 실행**.)

## <a name="syntax"></a>구문

```
wbadmin get status
```

### <a name="parameters"></a>매개 변수

이 하위 명령에 매개 변수가 없습니다.

## <a name="remarks"></a>주의

-   현재 백업 또는 복구 작업이 완료 될 때까지이 하위 명령이 중지 되지 않습니다. 명령 창을 닫은 경우에도 하위 명령이 계속 실행 됩니다.
-   현재 백업 또는 복구 작업을 중지 하려면 **wbadmin stop job** 하위 명령을 사용 합니다.

## <a name="additional-references"></a>추가 참조

-   - [명령줄 구문 키](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [WBJob](https://technet.microsoft.com/library/jj902426.aspx) cmdlet