---
title: PowerShell 스크립팅 성능 고려 사항
description: PowerShell의 성능에 대 한 스크립팅
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: JasonSh
author: lzybkr
ms.date: 10/16/2017
ms.openlocfilehash: 2898cf5ee965da77c9f6a3473e55c1cee6b53f2b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71354981"
---
# <a name="powershell-scripting-performance-considerations"></a>PowerShell 스크립팅 성능 고려 사항

.NET을 직접 활용 하 고 파이프라인을 방지 하는 PowerShell 스크립트는 자연 스러운 PowerShell 보다 속도가 더 빠릅니다. 자연 스러운 PowerShell은 일반적으로 cmdlet 및 PowerShell 함수를 자주 사용 하 고, 파이프라인을 활용 하 고, 필요한 경우에만 .NET으로 삭제 합니다.

>[!Note] 
> 여기서 설명 하는 대부분의 기술은 PowerShell이 자연 스러운 powershell 스크립트의 가독성을 저하 시킬 수 있습니다. 다른 방법으로는 성능이 결정 되지 않는 한 자연 스러운 PowerShell을 사용 하는 것이 좋습니다.

## <a name="suppressing-output"></a>출력 표시 안 함

파이프라인에 개체를 작성 하지 않도록 방지 하는 방법에는 여러 가지가 있습니다.

```PowerShell
$null = $arrayList.Add($item)
[void]$arrayList.Add($item)
```

@No__t-0에 대 한 할당 또는 `[void]`로의 캐스팅은 거의 동일 하며, 일반적으로 성능이 중요 한 경우에는 우선적으로 사용할 수 있어야 합니다.

```PowerShell
$arrayList.Add($item) > $null
```

@No__t-0에 대 한 파일 리디렉션은 이전 대체와 거의 동일 하지만 대부분의 스크립트는 차이점을 알 수 없습니다.
시나리오에 따라 파일 리디렉션은 약간 약간의 오버 헤드를 발생 시키지만

```PowerShell
$arrayList.Add($item) | Out-Null
```

파이프에 `Out-Null`은 대체 항목에 비해 상당한 오버 헤드가 발생 합니다.
성능에 중요 한 코드는 피해 야 합니다.

```PowerShell
$null = . {
    $arrayList.Add($item)
    $arrayList.Add(42)
}
```

스크립트 블록을 소개 하 고이를 호출 하 고 (점 소싱을 사용 하 여), `$null`에 결과를 할당 하면 많은 스크립트 블록의 출력을 표시 하지 않는 편리한 기술입니다.
이 기법은 `Out-Null`에 대 한 파이프 및 파이프를 수행 하므로 성능이 중요 한 스크립트에서 피해 야 합니다.
이 예의 추가 오버 헤드는 이전에 인라인 스크립트인 스크립트 블록을 만들고 호출 하는 것에서 나옵니다.


## <a name="array-addition"></a>배열 더하기

항목 목록을 생성 하는 경우에는 더하기 연산자가 포함 된 배열을 사용 하는 경우가 많습니다.

```PowerShell
$results = @()
$results += Do-Something
$results += Do-SomethingElse
$results
```

배열은 변경할 수 없기 때문에 매우 inefficent 수 있습니다.
배열에 대 한 각 추가는 실제로 왼쪽 피연산자와 오른쪽 피연산자의 모든 요소를 보유할 만큼 큰 새 배열을 만든 다음 두 피연산자의 요소를 새 배열에 복사 합니다.
소규모 컬렉션의 경우 이러한 오버 헤드가 중요 하지 않을 수 있습니다.
컬렉션이 클 경우에는 문제가 발생할 수 있습니다.

몇 가지 대안이 있습니다.
실제로 배열이 필요 하지 않은 경우에는 ArrayList를 사용 하는 것이 좋습니다.

```PowerShell
$results = [System.Collections.ArrayList]::new()
$results.AddRange((Do-Something))
$results.AddRange((Do-SomethingElse))
$results
```

배열이 필요 하면 고유한 `ArrayList`을 사용 하 고 배열을 원할 때 `ArrayList.ToArray`을 호출 하기만 하면 됩니다.
또는 PowerShell에서 `ArrayList` 및 `Array`을 만들도록 할 수 있습니다.

```PowerShell
$results = @(
    Do-Something
    Do-SomethingElse
)
```

이 예에서 PowerShell은 배열 식 내의 파이프라인에 기록 된 결과를 저장 하는 `ArrayList`을 만듭니다.
@No__t-0에 할당 하기 직전에 PowerShell은 `ArrayList`을 `object[]`로 변환 합니다.

## <a name="processing-large-files"></a>큰 파일 보고서 처리

PowerShell에서 파일을 처리 하는 자연 스러운 방법은 다음과 같습니다.

```PowerShell
Get-Content $path | Where-Object { $_.Length -gt 10 }
```

이는 .NET Api를 직접 사용 하는 것 보다 훨씬 더 느릴 수 있습니다.

```PowerShell
try
{
    $stream = [System.IO.StreamReader]::new($path)
    while ($line = $stream.ReadLine())
    {
        if ($line.Length -gt 10)
        {
            $line
        }
    }
}
finally
{
    $stream.Dispose()
}
```

## <a name="avoid-write-host"></a>쓰기 방지-호스트

일반적으로 출력을 콘솔에 직접 작성 하는 것이 좋지 않은 경우는 거의 없습니다. 그러나 많은 스크립트에서 `Write-Host`을 사용 합니다.

콘솔에 많은 메시지를 작성 해야 하는 경우 `Write-Host`은 `[Console]::WriteLine()` 보다 속도가 느릴 수 있습니다. 그러나 `[Console]::WriteLine()`은 powershell .exe 또는 powershell_ise와 같은 특정 호스트에 대 한 적절 한 대안이 며 모든 호스트에서 작동 하지 않을 수 있습니다.

@No__t-0을 사용 하는 대신 [쓰기 출력](/powershell/module/Microsoft.PowerShell.Utility/Write-Output?view=powershell-5.1)을 사용 하는 것이 좋습니다.

