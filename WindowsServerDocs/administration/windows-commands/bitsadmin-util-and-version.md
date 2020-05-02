---
title: bitsadmin util and version
description: BITS 서비스의 버전을 표시 하는 bitsadmin util 및 version 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 98f17328-dfbd-4cbb-93c1-b8d424bc3f0a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 20c3db6e6fcd5ef3d00287f36c9f9624ab5224dd
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707589"
---
# <a name="bitsadmin-util-and-version"></a>bitsadmin util and version

BITS 서비스의 버전을 표시 합니다 (예: 2.0).

> [!NOTE]
> 이 명령은 BITS 1.5 이전 버전에서는 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /util /version [/verbose]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| /verbose | 이 스위치를 사용 하 여 각 비트 관련 DLL의 파일 버전을 표시 하 고 BITS 서비스를 시작할 수 있는지 여부를 확인할 수 있습니다.|

## <a name="examples"></a>예

BITS 서비스의 버전을 표시 합니다.

```
bitsadmin /util /version
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin util 명령](bitsadmin-util.md)

- [bitsadmin 명령](bitsadmin.md)
