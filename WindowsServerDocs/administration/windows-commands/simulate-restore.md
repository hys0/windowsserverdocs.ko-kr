---
title: simulate restore
description: 작성자에 게 PreRestore 또는 PostRestore 이벤트를 발급 하지 않고 컴퓨터의 복원 세션에서 쓰기를 테스트 하는 복원 시뮬레이션에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d883d94c-3cb1-4848-9d74-1b4378044b31
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7cc247848ef4fac1e3a6537247f640f3533c2bcd
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936357"
---
# <a name="simulate-restore"></a>복원 시뮬레이션

실행 하지 않고 컴퓨터에 복원 세션에서 기록기 참여 테스트 **PreRestore** 또는 **PostRestore** 작성기에는 이벤트입니다.

## <a name="syntax"></a>구문

```
simulate restore
```

## <a name="remarks"></a>설명

-   **복원 시뮬레이션** 기록기를 사용 하 여 복원을 성공할 수 있는지 여부를 테스트 하는 데 사용 됩니다.
-   사용 하려면 먼저 **복원 시뮬레이션**, DiskShadow 메타 데이터 파일을 사용 하 여 로드 해야는 **메타 데이터를 로드** 명령입니다. 이 선택한 작성자 및 복원에 대 한 구성 요소를 로드합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)