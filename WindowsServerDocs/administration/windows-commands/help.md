---
title: 도움말
description: 지정 된 명령에 대 한 자세한 도움말 정보 또는 사용 가능한 명령 목록을 표시 하는 도움말 항목에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c65b5ac3-711a-4368-95b8-ba82e2d00713
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b73ef32b49b834a91f24e943749eb21398c8588
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818663"
---
# <a name="help"></a>도움말

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정한 명령에 사용할 수 있는 명령 또는 자세한 도움말 정보 목록을 표시합니다. 매개 변수 없이 사용 하는 경우 **도움말** 을 나열 하 고 모든 시스템 명령을 간략하게 설명 합니다.

## <a name="syntax"></a>구문

```
help [<command>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<command>` | 자세한 도움말 정보를 표시 하는 명령을 지정 합니다. |

### <a name="examples"></a>예

**Robocopy** 명령에 대 한 정보를 보려면 다음을 입력 합니다.

```
help robocopy
```

DiskPart에서 사용할 수 있는 모든 명령 목록을 표시 하려면 다음을 입력 합니다.

```
help
```

사용 하는 방법에 대 한 자세한 도움말 정보를 표시 하는 **파티션을 주 만들** 형식 DiskPart 명령을:

```
help create partition primary
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
