---
title: PowerShell 스크립팅 성능 고려 사항
description: PowerShell에서 성능에 대 한 스크립팅
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: JasonSh
author: lzybkr
ms.date: 10/16/2017
ms.openlocfilehash: df406c7e382907ca32006ec4dae6537a140a91cf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830374"
---
# <a name="powershell-scripting-performance-considerations"></a>PowerShell 스크립팅 성능 고려 사항

.NET을 직접 활용 하 고 파이프라인을 방지 하는 PowerShell 스크립트는 자연 스러운 PowerShell 보다 빠른 경향이 있습니다. 자연 스러운 PowerShell cmdlet을 일반적으로 사용 하 고 과도 하 게 종종 파이프라인을 활용 하 고 필요한 경우에.NET으로 끌어 놓은 PowerShell 함수입니다.

>[!Note] 
> 여기에 설명 된 기술의 여러 관용구 PowerShell 되지 않으며 PowerShell 스크립트의 가독성이 떨어질 수 있습니다. PowerShell 사용 하 여 자연 스러운 성능을 결정이 고, 그렇지 않으면 스크립트 작성자를 사용 하는 것이 좋습니다.

## <a name="suppressing-output"></a>출력 표시 안 함

여러 가지 방법으로 파이프라인에 개체를 작성 하지 않으려면:

```PowerShell
$null = $arrayList.Add($item)
[void]$arrayList.Add($item)
```

할당할 `$null` 에 캐스팅 또는 `[void]` 과 거의 동일 하며 일반적으로 성능이 중요 한 기본 설정 합니다.

```PowerShell
$arrayList.Add($item) > $null
```

파일에 리디렉션 `$null` 은 거의 우수한 이전 대안 가장 스크립트는 차이점을 확인 하지 않습니다.
시나리오에 따라 파일 리디렉션에 약간의 오버 헤드를 통해 소개 합니다.

```PowerShell
$arrayList.Add($item) | Out-Null
```

파이프에 `Out-Null` 대안에 비해 상당한 오버 헤드가 있습니다.
성능이 중요 한 코드에서 방지 수 해야 합니다.

```PowerShell
$null = . {
    $arrayList.Add($item)
    $arrayList.Add(42)
}
```

스크립트 블록을 소개 하 고 (도트 소싱 이거나 사용) 호출 결과를 할당 한 다음 `$null` 은 스크립트의 큰 블록의 출력을 표시 하지 않기 위한 편리한 기술 합니다.
이 기술은 파이핑 뿐만 아니라 거의 수행 `Out-Null` 성능이 중요 한 스크립트에서 피해 야 합니다.
이 예에서 추가 오버 헤드를 만드는 방법과 인라인 스크립트 이전에 있던 스크립트 블록을 호출에서 제공 됩니다.


## <a name="array-addition"></a>배열 추가

종종 이루어집니다 항목 목록을 생성 하 고 더하기 연산자를 사용 하 여 배열을 사용 하 여:

```PowerShell
$results = @()
$results += Do-Something
$results += Do-SomethingElse
$results
```

배열은 변경할 수 있으므로 매우 inefficent 수 있습니다.
각 추가 배열에 실제로 새 배열을 모두 왼쪽과 오른쪽 피연산자의 모든 요소를 보유할 만큼 충분히 크게 만듭니다 다음 두 피연산자의 요소를 새 배열에 복사 합니다.
작은 컬렉션에 대 한이 오버 헤드는 중요 하지 않을 수 있습니다.
큰 컬렉션의 경우이 문제가 분명 수 있습니다.

대체 방법 중 몇 가지 있습니다.
배열에 실제로 필요한 경우 ArrayList를 사용 하 여이 좋습니다.

```PowerShell
$results = [System.Collections.ArrayList]::new()
$results.AddRange((Do-Something))
$results.AddRange((Do-SomethingElse))
$results
```

배열을 해야 하는 경우 사용할 수 있습니다 고유한 `ArrayList` 만 호출 하면 `ArrayList.ToArray` 배열 하려는 경우.
또는 PowerShell을 만들 수는 `ArrayList` 및 `Array` 있습니다.

```PowerShell
$results = @(
    Do-Something
    Do-SomethingElse
)
```

이 예제에서는 PowerShell 만듭니다는 `ArrayList` 배열 식 내에서 파이프라인에 기록 하는 결과를 저장할 합니다.
에 할당 하기 직전 `$results`, PowerShell 변환 합니다 `ArrayList` 에 `object[]`합니다.

## <a name="processing-large-files"></a>큰 파일 처리

PowerShell에서 파일을 처리 하는 자연 스러운 방법은 같이 표시 될 수 있습니다.

```PowerShell
Get-Content $path | Where-Object { $_.Length -gt 10 }
```

거의 10 배.NET Api를 직접 사용 하 여 보다 속도가 느릴 수 있습니다.

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

## <a name="avoid-write-host"></a>Avoid Write-Host

콘솔에 직접 출력을 쓸 저하 사례는 일반적으로 간주 되지만 많은 스크립트를 사용 하는 적합 하면 `Write-Host`합니다.

콘솔에 메시지를 작성 해야 하는 경우 `Write-Host` 규모 보다 속도가 느릴 수 `[Console]::WriteLine()`입니다. 그러나는 `[Console]::WriteLine()` powershell.exe 또는 powershell_ise.exe와 같은 특정 호스트-모든 호스트에서 작동 하도록 보장 되지에 대 한 적절 한 대안만 됩니다.

사용 하는 대신 `Write-Host`를 사용 하는 것이 좋습니다 [Write-output](/powershell/module/Microsoft.PowerShell.Utility/Write-Output?view=powershell-5.1)합니다.

