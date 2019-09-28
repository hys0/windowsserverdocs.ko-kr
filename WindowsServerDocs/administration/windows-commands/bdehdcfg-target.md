---
title: bdehdcfg 대상
description: Bdehdcfg target에 대 한 Windows 명령 항목-BitLocker 및 Windows 복구를 통해 시스템 드라이브로 사용할 파티션을 준비 합니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f761d25d-8349-4ac7-ac46-6bb340a4348f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2fb0a1daa257ef2c9f1cd77b88e5ef14f84a0dfa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382184"
---
# <a name="bdehdcfg-target"></a>bdehdcfg: 대상



BitLocker와 Windows 복구 하 여 시스템 드라이브로 사용 하기 위해 파티션을 준비합니다. 기본적으로이 파티션에 드라이브 문자 없이 생성 됩니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge}
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|기본|명령줄 도구에서 BitLocker 설치 마법사와 동일한 프로세스를 따르는지를 나타냅니다.|
|할당 되지 않은|디스크에 시스템 파티션을 사용할 수 있는 할당 되지 않은 공간 부족을 만듭니다.|
|\<DriveLetter > 축소|활성 시스템 파티션을 만드는 데 필요한 양으로 지정 된 드라이브를 줄일 수 있습니다. 이 명령을 사용 하려면 지정 된 드라이브에서 최소 5%의 사용 가능한 공간 있어야 합니다.|
|\<DriveLetter > merge|현재 시스템 파티션으로 지정 된 드라이브를 사용 합니다. 운영 체제 드라이브 병합 대상이 될 수 없습니다.|

## <a name="BKMK_Examples"></a>예와

다음 예제를 사용 하 여 보여 주며는 **대상** 시스템 드라이브로 기존 드라이브 (P)를 지정 하는 명령입니다.
```
bdehdcfg -target P: merge
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)