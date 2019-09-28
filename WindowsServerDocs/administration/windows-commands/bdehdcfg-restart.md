---
title: bdehdcfg 다시 시작
description: Bdehdcfg 다시 시작에 대 한 Windows 명령 항목-드라이브 준비가 완료 된 후 컴퓨터를 다시 시작 해야 함을 bdehdcfg에 게 알립니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a98b76bb-36f1-4790-b337-7dc35f606bc6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e6c4e48b051f567c98ea679feaa22f995982a899
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382207"
---
# <a name="bdehdcfg-restart"></a>bdehdcfg: 다시 시작



컴퓨터 다시 시작 해야 드라이브 준비 되어도 Bdehdcfg 명령줄 도구에 알립니다. 이 명령을 사용할 수 있는 방법을의 예제를 참조 하십시오. [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -restart
```

### <a name="parameters"></a>매개 변수

이 명령은 추가 매개 변수를 사용 합니다.

## <a name="remarks"></a>설명

다른 사용자가 컴퓨터에 로그온 하는 경우와 **quiet** 명령을 지정 하지 않으면, 컴퓨터를 다시 시작 해야 있는지 확인 하는 메시지가 표시 됩니다.

## <a name="BKMK_Examples"></a>예와

다음 예제를 사용 하는 **다시 시작** 명령입니다.
```
bdehdcfg -target default -restart
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)