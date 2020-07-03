---
title: bdehdcfg target
description: BitLocker 및 Windows 복구를 통해 시스템 드라이브로 사용할 파티션을 준비 하는 bdehdcfg target 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f761d25d-8349-4ac7-ac46-6bb340a4348f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 509c659907878f7b0ddc0b0c601715fa996c5fe7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923365"
---
# <a name="bdehdcfg-target"></a>bdehdcfg: 대상

BitLocker와 Windows 복구 하 여 시스템 드라이브로 사용 하기 위해 파티션을 준비합니다. 기본적으로이 파티션에 드라이브 문자 없이 생성 됩니다.

## <a name="syntax"></a>구문

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink|<drive_letter> merge}
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| default | 명령줄 도구에서 BitLocker 설치 마법사와 동일한 프로세스를 따르는지를 나타냅니다. |
| 할당 되지 않은 | 디스크에 시스템 파티션을 사용할 수 있는 할당 되지 않은 공간 부족을 만듭니다. |
| `<drive_letter>`축소할 | 활성 시스템 파티션을 만드는 데 필요한 양으로 지정 된 드라이브를 줄일 수 있습니다. 이 명령을 사용 하려면 지정 된 드라이브에서 최소 5%의 사용 가능한 공간 있어야 합니다. |
| `<drive_letter>`결합 | 현재 시스템 파티션으로 지정 된 드라이브를 사용 합니다. 운영 체제 드라이브 병합 대상이 될 수 없습니다. |

## <a name="examples"></a>예

기존 드라이브 (P)를 시스템 드라이브로 지정 하려면 다음을 수행 합니다.

```
bdehdcfg -target P: merge
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
