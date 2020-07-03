---
title: reset
description: '* * * *에 대 한 참조 문서'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: afbdab44-199c-4e11-884f-e96804965c21
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8a412eff7bdf432608a999edb4531074ed5e8f26
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933097"
---
# <a name="reset"></a>reset



DiskShadow.exe를 기본 상태로 다시 설정합니다. **재설정** 는 같은 복합 DiskShadow 작업을 분리 하는 데 특히 유용 **만들**, **가져올**, **백업**, 또는 **복원**합니다.

## <a name="syntax"></a>구문

```
reset
```

## <a name="remarks"></a>설명

-   사용 하는 경우는 **재설정** 잃게 상태 명령에서와 같은 명령을 **추가**, **설정**, **로드**, 또는 **기록기**합니다. 또한 **Reset** 은 IVssBackupComponent 인터페이스를 해제 하 고 비영구 섀도 복사본을 잃게 됩니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)