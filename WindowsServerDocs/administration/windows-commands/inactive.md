---
title: 비활성
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4fb4695-4e66-4166-b4ab-2c86a4605580
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6642288385571b00c3fd0094dcd6cc4237aa492e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812924"
---
# <a name="inactive"></a>비활성



마스터 부트 레코드 (MBR) 디스크에 시스템 파티션 또는 비활성으로 포커스가 있는 부팅 파티션을 표시합니다.

## <a name="syntax"></a>구문

```
inactive
```

## <a name="remarks"></a>설명

> [!CAUTION]
> 활성 파티션이 없으면 컴퓨터 시작할 수 없습니다. 에 익숙한 사용자는 Windows 운영 체제 제품군에 잘 알고 있지 않은 경우에 시스템 또는 부팅 파티션을 비활성으로 표시 하지 마십시오.</br>> 시스템 또는 부팅 파티션을 비활성으로 표시 한 후 컴퓨터를 시작할 수 없는 경우 CD-ROM 드라이브에 Windows 설치 CD를 삽입, 컴퓨터를 다시 시작 하 고 사용 하 여 파티션 복구는 **fixmbr** 고**fixboot** 복구 콘솔에서 명령을 합니다.
-   시스템 파티션 또는 부팅 파티션을 비활성으로 표시 하면 컴퓨터를 BIOS에서 CD-ROM 드라이브는 사전 부팅 환경 PXE (eXecution) 등에서 다음 옵션에서 시작 합니다.
-   이 작업을 완료 하려면 활성 시스템 또는 부팅 파티션을 선택 되어야 합니다. 사용 된 **파티션을 선택** 활성 파티션을 선택에서 포커스를 전환 하는 명령입니다.

## <a name="BKMK_examples"></a>예제

```
inactive
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

