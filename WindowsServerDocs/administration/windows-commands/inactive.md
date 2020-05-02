---
title: 비활성
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f4fb4695-4e66-4166-b4ab-2c86a4605580
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4f1c0e0cd5ebbf92638a221852bc3133116f4911
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724829"
---
# <a name="inactive"></a>비활성



기본 MBR (마스터 부트 레코드) 디스크에서 포커스가 있는 시스템 파티션 또는 부팅 파티션을 비활성으로 표시 합니다.

## <a name="syntax"></a>구문

```
inactive
```

## <a name="remarks"></a>설명

> [!CAUTION]
> 활성 파티션이 없으면 컴퓨터 시작할 수 없습니다. 에 익숙한 사용자는 Windows 운영 체제 제품군에 잘 알고 있지 않은 경우에 시스템 또는 부팅 파티션을 비활성으로 표시 하지 마십시오.</br>> 시스템 또는 부팅 파티션을 비활성으로 표시 한 후 컴퓨터를 시작할 수 없는 경우 cd-rom 드라이브에 Windows 설치 프로그램 CD를 삽입 하 고 컴퓨터를 다시 시작한 다음 복구 콘솔에서 **fixmbr** 및 **fixboot** 명령을 사용 하 여 파티션을 복구 합니다.
> -   시스템 파티션 또는 부팅 파티션을 비활성으로 표시 한 후 컴퓨터는 BIOS에 지정 된 다음 옵션 (예: CD-ROM 드라이브 또는 PXE (사전 부팅 실행 환경))에서 시작 됩니다.
> -   이 작업을 완료 하려면 활성 시스템 또는 부팅 파티션을 선택 되어야 합니다. 사용 된 **파티션을 선택** 활성 파티션을 선택에서 포커스를 전환 하는 명령입니다.

## <a name="examples"></a>예

```
inactive
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

