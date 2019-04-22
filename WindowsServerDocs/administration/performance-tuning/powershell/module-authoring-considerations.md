---
title: PowerShell 모듈 작성 시 고려 사항
description: PowerShell 모듈 작성 시 고려 사항
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: JasonSh
author: lzybkr
ms.date: 10/16/2017
ms.openlocfilehash: 37dd860019b91daf70947dba93d20274048487a0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818724"
---
# <a name="powershell-module-authoring-considerations"></a>PowerShell 모듈 작성 시 고려 사항

이 문서는 최상의 성능을 위해 모듈은 작성 하는 방법에 관련 된 몇 가지 지침을 포함 합니다.

## <a name="module-manifest-authoring"></a>모듈 매니페스트 작성

다음 지침을 사용 하지 않는 모듈 매니페스트는 세션에서 모듈을 사용 하지 않는 하는 경우에 일반 PowerShell 성능에 눈에 띄는 영향이 있습니다.

명령을 자동 검색은 모듈이 내보내는 하 고이 분석은 비용이 많이 들 수 있는 명령을 확인 하려면 각 모듈을 분석 합니다.
모듈 분석 결과를 사용자별로 캐시 되지만 캐시는 컨테이너를 사용 하 여 일반적인 시나리오는 첫 번째 실행에서 사용할 수 없습니다.
모듈 분석 하는 동안 내보낸된 명령을 매니페스트에서 완벽 하 게 확인할 수 있습니다 하는 경우 비용이 많이 드는 분석 모듈을 방지할 수 있습니다.

### <a name="guidelines"></a>지침

* 모듈 매니페스트를 사용 하지 마세요에서 와일드 카드를 `AliasesToExport`, `CmdletsToExport`, 및 `FunctionsToExport` 항목입니다.

* 모듈 특정 형식의 명령을 내보내지 않습니다, 경우이 명시적으로 지정 매니페스트에서 지정 하 여 `@()`입니다.
누락 또는 `$null` 와일드 카드를 지정 하 항목 동일 `*`합니다.

가능한 경우 다음을 피해 야 합니다.

```PowerShell
@{
    FunctionsToExport = '*'

    # Also avoid omitting an entry, it is equivalent to using a wildcard
    # CmdletsToExport = '*'
    # AliasesToExport = '*'
}
```

대신 사용 하십시오.

```PowerShell
@{
    FunctionsToExport = 'Format-Hex', 'Format-Octal'
    CmdletsToExport = @()  # Specify an empty array, not $null
    AliasesToExport = @()  # Also ensure all three entries are present
}
```

## <a name="avoid-cdxml"></a>Avoid CDXML

모듈을 구현 하는 방법을 결정할 때 가지 세 가지 기본 방법이 있습니다.

* 이진 (일반적으로 C#)
* 스크립트 (PowerShell)
* CDXML (CIM 래핑 XML 파일)

모듈을 로드 하는 속도가 중요 한 경우 CDXML은 약 10 배 이진 모듈 보다 느립니다.

이진 모듈 미리 컴파일된 JIT 컴파일 컴퓨터당 한 번에 NGen을 사용할 수 있으므로 가장 빠르게 로드 합니다.

일반적으로 스크립트 모듈을 PowerShell 스크립트를 컴파일하고 실행 하기 전에 구문 분석 해야 하기 때문에 이진 모듈 보다 더 느리게 로드 합니다.

CDXML 모듈은 다음 매우 많은 구문 분석 되어 컴파일된 PowerShell 스크립트를 생성 하는 XML 파일을 먼저 구문 분석 해야 하기 때문에 일반적으로 스크립트 모듈 보다 훨씬 느립니다.

