---
title: PowerShell 모듈 제작 고려 사항
description: PowerShell 모듈 제작 고려 사항
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: JasonSh
author: lzybkr
ms.date: 10/16/2017
ms.openlocfilehash: 8945339e7a7950d3cd722ab2af629b45e7f6dd5d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370363"
---
# <a name="powershell-module-authoring-considerations"></a>PowerShell 모듈 제작 고려 사항

이 문서에는 최상의 성능을 위해 모듈을 작성 하는 방법과 관련 된 몇 가지 지침이 포함 되어 있습니다.

## <a name="module-manifest-authoring"></a>모듈 매니페스트 제작

다음 지침을 사용 하지 않는 모듈 매니페스트는 모듈이 세션에서 사용 되지 않은 경우에도 일반적인 PowerShell 성능에 눈에 띄는 영향을 줄 수 있습니다.

명령 자동 검색은 각 모듈을 분석 하 여 모듈에서 내보내는 명령을 확인 하 고이 분석에 비용이 많이 들 수 있습니다.
모듈 분석의 결과는 사용자별로 캐시 되지만 컨테이너를 사용 하는 일반적인 시나리오로는 처음 실행할 때 캐시를 사용할 수 없습니다.
모듈 분석 중에 내보낸 명령이 매니페스트에서 완전히 결정 될 수 있는 경우 모듈에 대 한 더 비싼 분석을 피할 수 있습니다.

### <a name="guidelines"></a>지침

* 모듈 매니페스트에서 `AliasesToExport`, `CmdletsToExport` 및 `FunctionsToExport` 항목에서 와일드 카드를 사용 하지 않습니다.

* 모듈이 특정 형식의 명령을 내보내지 않는 경우 `@()`을 지정 하 여 매니페스트에 명시적으로 지정 합니다.
누락 또는 @no__t 0 항목은 와일드 카드 `*`을 지정 하는 것과 같습니다.

가능한 경우 다음을 피해 야 합니다.

```PowerShell
@{
    FunctionsToExport = '*'

    # Also avoid omitting an entry, it is equivalent to using a wildcard
    # CmdletsToExport = '*'
    # AliasesToExport = '*'
}
```

대신 다음을 사용 합니다.

```PowerShell
@{
    FunctionsToExport = 'Format-Hex', 'Format-Octal'
    CmdletsToExport = @()  # Specify an empty array, not $null
    AliasesToExport = @()  # Also ensure all three entries are present
}
```

## <a name="avoid-cdxml"></a>CDXML 방지

모듈을 구현 하는 방법을 결정할 때 세 가지 기본 옵션을 선택할 수 있습니다.

* Binary (일반적 C#으로)
* 스크립트 (PowerShell)
* CDXML (XML 파일 래핑 CIM)

모듈을 로드 하는 속도가 중요 한 경우 CDXML는 이진 모듈 보다 더 느린 크기의 순서입니다.

이진 모듈은 미리 컴파일되고 NGen을 사용 하 여 컴퓨터당 한 번씩 JIT 컴파일을 수행할 수 있으므로 가장 빠르게 로드 됩니다.

PowerShell은 스크립트를 컴파일하고 실행 하기 전에 스크립트를 구문 분석 해야 하기 때문에 일반적으로 스크립트 모듈은 이진 모듈 보다 약간 더 느리게 로드 됩니다.

일반적으로는 XML 파일을 구문 분석 한 다음 구문 분석 되 고 컴파일되는 매우 많은 PowerShell 스크립트를 생성 하는 XML 파일을 구문 분석 해야 하기 때문에 일반적으로는 스크립트 모듈 보다 더 느립니다.

