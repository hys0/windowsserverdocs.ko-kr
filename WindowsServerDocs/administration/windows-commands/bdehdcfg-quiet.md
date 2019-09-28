---
title: bdehdcfg quiet
description: Bdehdcfg quiet에 대 한 Windows 명령 항목-bdehdcfg에 게 모든 작업 및 오류를 표시 하지 않도록 지시 합니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f75b702-890b-4ff9-805c-edf5cadd8822
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d59a14e34200e3fa8e18e36e166ef62ceca1afe7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382224"
---
# <a name="bdehdcfg-quiet"></a>bdehdcfg: quiet



모든 동작 및 오류 되지 않는 명령줄 인터페이스에서 표시 하는 Bdehdcfg 명령줄 도구를 알립니다. 이 명령을 사용할 수 있는 방법을의 예제를 참조 하십시오. [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -quiet
```

### <a name="parameters"></a>매개 변수

이 명령은 추가 매개 변수를 사용 합니다.

## <a name="remarks"></a>설명

하는 경우 모든 Yes / (Y/N) 프롬프트 없이 드라이브를 준비 하는 동안 표시 된 것을 "예" 답을 가정 합니다. 드라이브 준비 중에 발생 한 오류를 보려면 아래에서 시스템 이벤트 로그를 검토는 **Windows BitLocker DrivePreparationTool Microsoft** 이벤트 공급자.

## <a name="BKMK_Examples"></a>예와

다음 예제를 사용 하는 **quiet** 명령입니다.
```
bdehdcfg -target default -quiet
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)