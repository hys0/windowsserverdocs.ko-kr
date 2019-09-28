---
title: bitsadmin monitor
description: '**Bitsadmin monitor** 에 대 한 Windows 명령 항목-현재 사용자가 소유 하는 전송 큐의 작업을 모니터링 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2c424d27-e011-49c2-b579-a2c235467c39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fe4963349c7e17fc77500b5adfceafc48a20ac5f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381223"
---
# <a name="bitsadmin-monitor"></a>bitsadmin monitor



현재 사용자가 소유 하는 전송 큐에서 작업을 모니터링 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /Monitor [/allusers] [/refresh <Seconds>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|Allusers|선택 사항-모든 사용자에 대 한 작업을 모니터링 합니다.|
|새로 고침|선택적-지정 된 간격으로 데이터를 새로 고칩니다 *초*합니다. 기본 새로 고침 간격은 5 초입니다.|

## <a name="remarks"></a>설명

사용 하려면 관리자 권한이 있어야 합니다.는 **Allusers** 매개 변수입니다.

새로 고침을 중지 하려면 CTRL + C를 사용 합니다.

## <a name="BKMK_examples"></a>예와

다음 예제에서는 현재 사용자가 소유한 작업에 대 한 전송 큐를 모니터링 하 고 60 초 마다 정보를 새로 고칩니다.
```
C:\>bitsadmin /Monitor /refesh 60
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)