---
title: bitsadmin reset
description: Windows 명령 항목에 대 한 **bitsadmin 재설정** -현재 사용자가 소유 하는 전송 큐에 모든 작업을 취소 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e4f9d1d-072c-493f-8d7a-f6d713c3ef29
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b7c29aac55393cd87145583814b3ffa8f0a2c3b3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874254"
---
# <a name="bitsadmin-reset"></a>bitsadmin reset

현재 사용자가 소유 하는 전송 큐에 모든 작업을 취소 합니다.

**BITSAdmin 1.5 및 이전 버전**: 관리자 권한이 있는 경우 **재설정** 큐에 모든 작업을 취소 합니다. /AllUsers 옵션이 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /Reset [/AllUsers]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|AllUsers|선택적-큐에 있는 모든 작업을 취소합니다.|

## <a name="remarks"></a>설명

사용 하려면 관리자 권한이 있어야 합니다.는 **AllUsers** 매개 변수입니다.

> [!NOTE]
> 관리자는 로컬 시스템에 의해 생성 된 작업을 재설정할 수 없습니다. 이 명령은 로컬 시스템 자격 증명을 사용 하 여 작업으로 예약 작업 scheduler를 사용 합니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 현재 사용자에 대 한 전송 큐에 모든 작업을 취소합니다.
```
C:\>bitsadmin /Reset
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)