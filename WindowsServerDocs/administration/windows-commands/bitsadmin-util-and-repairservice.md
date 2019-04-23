---
title: bitsadmin util 및 repairservice
description: Windows 명령 항목에 대 한 **bitsadmin util 및 repairservice** -명령은 BITS 서비스의 다양 한 버전의 알려진된 문제를 해결 하는 데 사용 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2ac7baeb-4340-4186-bfcb-66478195378d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc5101378a389c865f5753146b711be0d15c6785
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852094"
---
# <a name="bitsadmin-util-and-repairservice"></a>bitsadmin util 및 repairservice

BITS 시작 되지 않으면, 다양 한 버전의 BITS 사용 하 여 알려진된 문제를 해결 하려면이 스위치를 사용 합니다.

**BITSAdmin 1.5 및 이전 버전:** 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /Util /RepairService [/Force]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|Force|선택적-삭제 한 서비스를 다시 만듭니다.|

## <a name="remarks"></a>설명

이 스위치는 오류가 잘못 된 관련된 서비스 구성 및 Windows 서비스 (예: LANManworkstation)에 대 한 종속성 네트워크 디렉터리를 확인합니다. 이 스위치를 나타내는 출력을 생성 하는 경우 문제를 해결 했습니다.

> [!NOTE]
> BITS 서비스를 다시 만들어, 하는 경우 지역화 된 시스템에서 영어를 서비스 설명 문자열을 설정할 수 있습니다.

> [!IMPORTANT]
> 이 명령은 Windows Vista에서 지원 되지 않습니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 비트 서비스 구성을 수정합니다.
```
C:\>bitsadmin /Util /RepairService
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)