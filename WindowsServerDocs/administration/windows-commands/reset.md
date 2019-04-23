---
title: 다시 설정
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: afbdab44-199c-4e11-884f-e96804965c21
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0bd9b6735697cbcefdcf68dc3d4a53a6870a7a76
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850964"
---
# <a name="reset"></a>다시 설정



DiskShadow.exe를 기본 상태로 다시 설정합니다. **재설정** 는 같은 복합 DiskShadow 작업을 분리 하는 데 특히 유용 **만들**, **가져올**, **백업**, 또는 **복원**합니다.

## <a name="syntax"></a>구문

```
reset
```

## <a name="remarks"></a>설명

-   사용 하는 경우는 **재설정** 잃게 상태 명령에서와 같은 명령을 **추가**, **설정**, **로드**, 또는 **기록기**합니다. **재설정** 도 IVssBackupComponent 인터페이스를 해제 하 고 비 영구적인 섀도 복사본을 상실 합니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)