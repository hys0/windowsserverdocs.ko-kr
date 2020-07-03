---
title: bdehdcfg driveinfo
description: Bdehdcfg driveinfo 명령에 대 한 참조 문서는 드라이브 문자, 총 크기, 최대 여유 공간 및 파티션 특징을 표시 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f2d065e7-eced-4509-a1a0-ee2521a7f02e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0063c73cd20aca8c8fe5cc21b245517475268c64
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923484"
---
# <a name="bdehdcfg-driveinfo"></a>bdehdcfg: driveinfo

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

드라이브 문자, 총 크기, 최대 여유 공간, 및 파티션 특성을 표시합니다. 유효한 파티션으로 나열 됩니다. 4 개의 주 또는 확장 된 파티션이 이미 존재 하는 경우에 할당 되지 않은 공간 나열 되지 않습니다.

>[!NOTE]
> 이 명령은 정보 제공 용 이므로 드라이브를 변경 하지 않습니다.

## <a name="syntax"></a>구문

```
bdehdcfg -driveinfo <drive_letter>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| <drive_letter> | 드라이브 문자 뒤에 콜론으로 지정 합니다. |

## <a name="example"></a>예제

C: 드라이브에 대 한 드라이브 정보를 표시 하려면:

```
bdehdcfg  driveinfo C:
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
