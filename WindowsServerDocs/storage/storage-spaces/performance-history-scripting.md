---
title: 스토리지 공간 다이렉트 성능 기록을 사용한 스크립팅
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 53a5f2aa403c83d24acde1fc57e793141175d9b6
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474720"
---
# <a name="scripting-with-powershell-and-storage-spaces-direct-performance-history"></a>PowerShell 및 스토리지 공간 다이렉트 성능 기록을 사용 하 여 스크립팅

> 적용 대상: 시작

Windows Server 2019에서는 가상 컴퓨터, 서버, 드라이브, 볼륨, 네트워크 어댑터 등에 대 한 광범위 한 [성능 기록을](performance-history.md) [스토리지 공간 다이렉트](storage-spaces-direct-overview.md) 기록 하 고 저장 합니다. 성능 기록은 PowerShell에서 쉽게 쿼리 및 처리할 수 있으므로 *원시 데이터* 에서 다음과 같은 질문에 대 한 *실제 답변* 으로 신속 하 게 이동할 수 있습니다.

1. 지난 주에 CPU 스파이크가 있나요?
2. 비정상적인 대기 시간이 발생 하는 실제 디스크가 있나요?
3. 지금은 가장 많은 저장소 IOPS를 사용 하는 Vm은 무엇 인가요?
4. 네트워크 대역폭이 포화 상태 인가요?
5. 이 볼륨의 사용 가능한 공간이 어디에서 사용 되나요?
6. 지난 달에는 가장 많은 메모리를 사용 하는 Vm은 무엇 인가요?

`Get-ClusterPerf`이 cmdlet은 스크립팅을 위해 작성 되었습니다. 또는 파이프라인과 같은 cmdlet의 입력을 허용 `Get-VM` `Get-PhysicalDisk` 하 여 연결을 처리 하 고,, 및와 같은 유틸리티 cmdlet으로 출력을 파이프 `Sort-Object` 하 여 `Where-Object` `Measure-Object` 강력한 쿼리를 신속 하 게 작성할 수 있습니다.

**이 항목에서는 위의 6 가지 질문에 대답 하는 6 개의 샘플 스크립트를 제공 하 고 설명 합니다.** 다양 한 데이터 및 기간 동안 최고 수를 찾고, 평균을 찾고, 추세 선을 플롯 하 고, 이상 값 검색을 실행 하는 데 적용할 수 있는 패턴을 제공 합니다. 이러한 기능은 복사, 확장 및 다시 사용할 수 있는 무료 시작 코드로 제공 됩니다.

   > [!NOTE]
   > 간단히 하기 위해 샘플 스크립트는 고화질 PowerShell 코드에서 발생할 수 있는 오류 처리와 같은 항목을 생략 합니다. 이러한 기능은 주로 프로덕션 사용이 아닌 사용자를 위한 것입니다.

## <a name="sample-1-cpu-i-see-you"></a>샘플 1: CPU, 표시

이 샘플에서는 기간에서 시리즈를 사용 하 여 `ClusterNode.Cpu.Usage` `LastWeek` 클러스터의 모든 서버에 대 한 최대 ("상위 워터 마크"), 최소 및 평균 CPU 사용량을 표시 합니다. 또한 지난 8 일 동안 CPU 사용량이 25%, 50% 및 75%를 초과 하는 시간을 표시 하는 간단한 사분 위 분석을 수행 합니다.

### <a name="screenshot"></a>스크린샷

아래 스크린샷에서 *Server 02* 에는 지난 주에 대 한 설명이 없는 스파이크가 있습니다.

![PowerShell의 스크린샷](media/performance-history/Show-CpuMinMaxAvg.png)

### <a name="how-it-works"></a>작동 방법

`Get-ClusterPerf`기본 제공 cmdlet에 적절 한 파이프의 출력으로 `Measure-Object` 속성을 지정 합니다 `Value` . , 및 플래그를 사용 하 여 `-Maximum` `-Minimum` `-Average` `Measure-Object` 처음 세 열을 거의 무료로 제공 합니다. 사분 위 분석을 수행 하기 위해 `Where-Object` `-Gt` (보다 큼) 25, 50 또는 75 값의 수를 계산 하 고 계산할 수 있습니다. 마지막 단계는 및 도우미 함수를 사용 하는 것입니다 `Format-Hours` `Format-Percent` (beautify).

### <a name="script"></a>스크립트

스크립트는 다음과 같습니다.

```
Function Format-Hours {
    Param (
        $RawValue
    )
    # Weekly timeframe has frequency 15 minutes = 4 points per hour
    [Math]::Round($RawValue/4)
}

Function Format-Percent {
    Param (
        $RawValue
    )
    [String][Math]::Round($RawValue) + " " + "%"
}

$Output = Get-ClusterNode | ForEach-Object {
    $Data = $_ | Get-ClusterPerf -ClusterNodeSeriesName "ClusterNode.Cpu.Usage" -TimeFrame "LastWeek"

    $Measure = $Data | Measure-Object -Property Value -Minimum -Maximum -Average
    $Min = $Measure.Minimum
    $Max = $Measure.Maximum
    $Avg = $Measure.Average

    [PsCustomObject]@{
        "ClusterNode"    = $_.Name
        "MinCpuObserved" = Format-Percent $Min
        "MaxCpuObserved" = Format-Percent $Max
        "AvgCpuObserved" = Format-Percent $Avg
        "HrsOver25%"     = Format-Hours ($Data | Where-Object Value -Gt 25).Length
        "HrsOver50%"     = Format-Hours ($Data | Where-Object Value -Gt 50).Length
        "HrsOver75%"     = Format-Hours ($Data | Where-Object Value -Gt 75).Length
    }
}

$Output | Sort-Object ClusterNode | Format-Table
```

## <a name="sample-2-fire-fire-latency-outlier"></a>샘플 2: 화재, 화재, 대기 시간 이상

이 샘플에서는 시간 범위에서 시리즈를 사용 하 여 `PhysicalDisk.Latency.Average` `LastHour` 모집단 평균을 초과 하는 +3 σ (표준 편차 3 개)를 초과 하는 평균 대기 시간이 포함 된 드라이브로 정의 된 통계적 이상 값을 찾습니다.

   > [!IMPORTANT]
   > 간단히 하기 위해이 스크립트는 낮은 변동에 대 한 보호 기능을 구현 하지 않으며 부분 누락 데이터를 처리 하지 않으며 모델 또는 펌웨어 등을 구분 하지 않습니다. 하드 디스크를 바꿀지 여부를 확인 하기 위해이 스크립트를 단독으로 사용 하지 말고 좋은 judgement을 사용 하십시오. 여기에는 교육용 으로만 제공 됩니다.

### <a name="screenshot"></a>스크린샷

아래 스크린샷에서는 이상 값이 없는 것을 볼 수 있습니다.

![PowerShell의 스크린샷](media/performance-history/Show-LatencyOutlierHDD.png)

### <a name="how-it-works"></a>작동 방법

먼저가 일관 되 게 작동 하는지 확인 하 여 유휴 또는 거의 유휴 드라이브를 제외 `PhysicalDisk.Iops.Total` `-Gt 1` 합니다. 모든 활성 HDD에 대해 `LastHour` 360 측정으로 구성 된 시간을 10 초 간격으로 파이프 하 여 `Measure-Object -Average` 지난 1 시간 동안 평균 대기 시간을 구합니다. 그러면 인구를 설정 합니다.

모집단의 평균과 표준 편차를 찾기 위해 [널리 알려진 수식을](http://www.mathsisfun.com/data/standard-deviation.html) 구현 합니다 `μ` `σ` . 모든 활성 HDD에 대해 평균 대기 시간을 모집단 평균과 비교 하 여 표준 편차로 나눕니다. 원시 값을 유지 하므로 결과를 볼 수 `Sort-Object` 있지만 `Format-Latency` 및 `Format-StandardDeviation` 도우미 함수를 사용 하 여 표시 되는 내용을 beautify 수 있습니다.

드라이브가 +3 σ 보다 많은 경우 `Write-Host` 빨간색이 고, 그렇지 않으면 녹색입니다.

### <a name="script"></a>스크립트

스크립트는 다음과 같습니다.

```
Function Format-Latency {
    Param (
        $RawValue
    )
    $i = 0 ; $Labels = ("s", "ms", "μs", "ns") # Petabits, just in case!
    Do { $RawValue *= 1000 ; $i++ } While ( $RawValue -Lt 1 )
    # Return
    [String][Math]::Round($RawValue, 2) + " " + $Labels[$i]
}

Function Format-StandardDeviation {
    Param (
        $RawValue
    )
    If ($RawValue -Gt 0) {
        $Sign = "+"
    }
    Else {
        $Sign = "-"
    }
    # Return
    $Sign + [String][Math]::Round([Math]::Abs($RawValue), 2) + "σ"
}

$HDD = Get-StorageSubSystem Cluster* | Get-PhysicalDisk | Where-Object MediaType -Eq HDD

$Output = $HDD | ForEach-Object {

    $Iops = $_ | Get-ClusterPerf -PhysicalDiskSeriesName "PhysicalDisk.Iops.Total" -TimeFrame "LastHour"
    $AvgIops = ($Iops | Measure-Object -Property Value -Average).Average

    If ($AvgIops -Gt 1) { # Exclude idle or nearly idle drives

        $Latency = $_ | Get-ClusterPerf -PhysicalDiskSeriesName "PhysicalDisk.Latency.Average" -TimeFrame "LastHour"
        $AvgLatency = ($Latency | Measure-Object -Property Value -Average).Average

        [PsCustomObject]@{
            "FriendlyName"  = $_.FriendlyName
            "SerialNumber"  = $_.SerialNumber
            "MediaType"     = $_.MediaType
            "AvgLatencyPopulation" = $null # Set below
            "AvgLatencyThisHDD"    = Format-Latency $AvgLatency
            "RawAvgLatencyThisHDD" = $AvgLatency
            "Deviation"            = $null # Set below
            "RawDeviation"         = $null # Set below
        }
    }
}

If ($Output.Length -Ge 3) { # Minimum population requirement

    # Find mean μ and standard deviation σ
    $μ = ($Output | Measure-Object -Property RawAvgLatencyThisHDD -Average).Average
    $d = $Output | ForEach-Object { ($_.RawAvgLatencyThisHDD - $μ) * ($_.RawAvgLatencyThisHDD - $μ) }
    $σ = [Math]::Sqrt(($d | Measure-Object -Sum).Sum / $Output.Length)

    $FoundOutlier = $False

    $Output | ForEach-Object {
        $Deviation = ($_.RawAvgLatencyThisHDD - $μ) / $σ
        $_.AvgLatencyPopulation = Format-Latency $μ
        $_.Deviation = Format-StandardDeviation $Deviation
        $_.RawDeviation = $Deviation
        # If distribution is Normal, expect >99% within 3σ
        If ($Deviation -Gt 3) {
            $FoundOutlier = $True
        }
    }

    If ($FoundOutlier) {
        Write-Host -BackgroundColor Black -ForegroundColor Red "Oh no! There's an HDD significantly slower than the others."
    }
    Else {
        Write-Host -BackgroundColor Black -ForegroundColor Green "Good news! No outlier found."
    }

    $Output | Sort-Object RawDeviation -Descending | Format-Table FriendlyName, SerialNumber, MediaType, AvgLatencyPopulation, AvgLatencyThisHDD, Deviation

}
Else {
    Write-Warning "There aren't enough active drives to look for outliers right now."
}
```

## <a name="sample-3-noisy-neighbor-thats-write"></a>샘플 3: 잡음이 있는 환경 작성 되었습니다.

성능 기록은 *현재*에 대 한 질문에 대답할 수 있습니다. 새 측정은 10 초 마다 실시간으로 사용할 수 있습니다. 이 샘플에서는 일정 기간의 시리즈를 사용 하 여 `VHD.Iops.Total` `MostRecent` 클러스터의 모든 호스트에서 가장 많은 저장소 IOPS를 사용 하는 가상 컴퓨터 ("noisiest")를 식별 하 고 해당 작업의 읽기/쓰기 분석을 표시 합니다.

### <a name="screenshot"></a>스크린샷

아래 스크린샷에는 저장소 활동 별로 상위 10 개의 가상 머신이 표시 됩니다.

![PowerShell의 스크린샷](media/performance-history/Show-TopIopsVMs.png)

### <a name="how-it-works"></a>작동 방법

와 달리 `Get-PhysicalDisk` `Get-VM` cmdlet은 클러스터를 인식 하지 않으며 로컬 서버에 있는 vm만 반환 합니다. 모든 서버에서 병렬로 쿼리하려면에서 호출을 래핑합니다 `Invoke-Command (Get-ClusterNode).Name { ... }` . 모든 VM에 대해 `VHD.Iops.Total` , `VHD.Iops.Read` 및 `VHD.Iops.Write` 측정이 제공 됩니다. 매개 변수를 지정 하지 않으면 `-TimeFrame` `MostRecent` 각각에 대해 단일 데이터 요소를 가져옵니다.

   > [!TIP]
   > 이러한 계열은 모든 VHD/VHDX 파일에 대 한이 VM의 작업 합계를 반영 합니다. 이 예에서는 성능 기록이 자동으로 집계 됩니다. VHD 당/VHDX 분석을 가져오려면 `Get-VHD` VM 대신 개별를로 파이프 할 수 있습니다 `Get-ClusterPerf` .

모든 서버의 결과는로 함께 제공 `$Output` 되며, 그 다음에는 가능 `Sort-Object` `Select-Object -First 10` 합니다. `Invoke-Command`에서 발생 한 위치를 나타내는 속성을 데코 레이트 하 고 `PsComputerName` , VM이 실행 되는 위치를 알 수 있도록 인쇄할 수 있습니다.

### <a name="script"></a>스크립트

스크립트는 다음과 같습니다.

```
$Output = Invoke-Command (Get-ClusterNode).Name {
    Function Format-Iops {
        Param (
            $RawValue
        )
        $i = 0 ; $Labels = (" ", "K", "M", "B", "T") # Thousands, millions, billions, trillions...
        Do { if($RawValue -Gt 1000){$RawValue /= 1000 ; $i++ } } While ( $RawValue -Gt 1000 )
        # Return
        [String][Math]::Round($RawValue) + " " + $Labels[$i]
    }

    Get-VM | ForEach-Object {
        $IopsTotal = $_ | Get-ClusterPerf -VMSeriesName "VHD.Iops.Total"
        $IopsRead  = $_ | Get-ClusterPerf -VMSeriesName "VHD.Iops.Read"
        $IopsWrite = $_ | Get-ClusterPerf -VMSeriesName "VHD.Iops.Write"
        [PsCustomObject]@{
            "VM" = $_.Name
            "IopsTotal" = Format-Iops $IopsTotal.Value
            "IopsRead"  = Format-Iops $IopsRead.Value
            "IopsWrite" = Format-Iops $IopsWrite.Value
            "RawIopsTotal" = $IopsTotal.Value # For sorting...
        }
    }
}

$Output | Sort-Object RawIopsTotal -Descending | Select-Object -First 10 | Format-Table PsComputerName, VM, IopsTotal, IopsRead, IopsWrite
```

## <a name="sample-4-as-they-say-25-gig-is-the-new-10-gig"></a>샘플 4: "25-4gb는 새로운 10-4gb"입니다.

이 샘플에서는 기간의 시리즈를 사용 하 여 `NetAdapter.Bandwidth.Total` `LastDay` 네트워크 포화의 부호를 찾습니다 .이는 이론적 최대 대역폭의 >90%로 정의 됩니다. 클러스터에 있는 모든 네트워크 어댑터에 대해 마지막 날에서 관찰 된 최고 대역폭 사용량을 해당 링크 속도와 비교 합니다.

### <a name="screenshot"></a>스크린샷

아래 스크린샷에서는 마지막 날에 한 *FABRIKAM NX-4 Pro #2* 뾰족한 것을 확인할 것입니다.

![PowerShell의 스크린샷](media/performance-history/Show-NetworkSaturation.png)

### <a name="how-it-works"></a>작동 방법

`Invoke-Command`위의 트릭을 `Get-NetAdapter` 모든 서버에서로 반복 하 고에 파이프 `Get-ClusterPerf` 합니다. 이 과정에서 두 개의 관련 속성인 `LinkSpeed` "10Gbps"와 같은 문자열 및 `Speed` 100억 같은 원시 정수를 가져옵니다. 를 사용 `Measure-Object` 하 여 마지막 날의 평균 및 최대 사용량을 가져옵니다 (미리 알림: 시간 범위에서 각 측정은 `LastDay` 5 분을 나타냄), 바이트 당 8 비트 단위로 곱하여 사과 대 사과 비교를 가져옵니다.

   > [!NOTE]
   > Chelsio와 같은 일부 공급 업체는 *네트워크 어댑터* 성능 카운터에 RDMA (원격 직접 메모리 액세스) 작업을 포함 하므로 시리즈에 포함 되어 `NetAdapter.Bandwidth.Total` 있습니다. Mellanox와 같은 다른 항목은 그렇지 않을 수도 있습니다. 공급 업체에서 제공 하지 않는 경우 `NetAdapter.Bandwidth.RDMA.Total` 이 스크립트의 버전에 시리즈를 추가 하기만 하면 됩니다.

### <a name="script"></a>스크립트

스크립트는 다음과 같습니다.

```
$Output = Invoke-Command (Get-ClusterNode).Name {

    Function Format-BitsPerSec {
        Param (
            $RawValue
        )
        $i = 0 ; $Labels = ("bps", "kbps", "Mbps", "Gbps", "Tbps", "Pbps") # Petabits, just in case!
        Do { $RawValue /= 1000 ; $i++ } While ( $RawValue -Gt 1000 )
        # Return
        [String][Math]::Round($RawValue) + " " + $Labels[$i]
    }

    Get-NetAdapter | ForEach-Object {

        $Inbound = $_ | Get-ClusterPerf -NetAdapterSeriesName "NetAdapter.Bandwidth.Inbound" -TimeFrame "LastDay"
        $Outbound = $_ | Get-ClusterPerf -NetAdapterSeriesName "NetAdapter.Bandwidth.Outbound" -TimeFrame "LastDay"

        If ($Inbound -Or $Outbound) {

            $InterfaceDescription = $_.InterfaceDescription
            $LinkSpeed = $_.LinkSpeed

            $MeasureInbound = $Inbound | Measure-Object -Property Value -Maximum
            $MaxInbound = $MeasureInbound.Maximum * 8 # Multiply to bits/sec

            $MeasureOutbound = $Outbound | Measure-Object -Property Value -Maximum
            $MaxOutbound = $MeasureOutbound.Maximum * 8 # Multiply to bits/sec

            $Saturated = $False

            # Speed property is Int, e.g. 10000000000
            If (($MaxInbound -Gt (0.90 * $_.Speed)) -Or ($MaxOutbound -Gt (0.90 * $_.Speed))) {
                $Saturated = $True
                Write-Warning "In the last day, adapter '$InterfaceDescription' on server '$Env:ComputerName' exceeded 90% of its '$LinkSpeed' theoretical maximum bandwidth. In general, network saturation leads to higher latency and diminished reliability. Not good!"
            }

            [PsCustomObject]@{
                "NetAdapter"  = $InterfaceDescription
                "LinkSpeed"   = $LinkSpeed
                "MaxInbound"  = Format-BitsPerSec $MaxInbound
                "MaxOutbound" = Format-BitsPerSec $MaxOutbound
                "Saturated"   = $Saturated
            }
        }
    }
}

$Output | Sort-Object PsComputerName, InterfaceDescription | Format-Table PsComputerName, NetAdapter, LinkSpeed, MaxInbound, MaxOutbound, Saturated
```

## <a name="sample-5-make-storage-trendy-again"></a>샘플 5: storage trendy을 다시 만듭니다.

매크로 추세를 보려면 최대 1 년 동안 성능 기록이 보존 됩니다. 이 샘플에서는 기간에서 시리즈를 사용 하 여 `Volume.Size.Available` `LastYear` 저장소를 채우는 속도와 저장소의 예상 시간을 결정 합니다.

### <a name="screenshot"></a>스크린샷

아래 스크린샷에서 *백업* 볼륨이 매일 약 15 g b를 추가 하는 것을 볼 수 있습니다.

![PowerShell의 스크린샷](media/performance-history/Show-StorageTrend.png)

이 속도는 다른 42 일 이내에 용량에 도달 합니다.

### <a name="how-it-works"></a>작동 방법

시간대에는 `LastYear` 하루에 하나의 데이터 요소가 있습니다. 추세선에 맞게 두 개의 지점만 엄격 하 게 필요 하지만 실제로는 14 일 등 더 많은 요구 사항을 충족 하는 것이 좋습니다. `Select-Object -Last 14` *(X, y) 점의 배열 (x, y)* 을 설정 하려면를 *x* 사용 합니다. 이러한 사항을 사용 하 여 가장 간단한 [선형 최소 제곱 알고리즘](http://mathworld.wolfram.com/LeastSquaresFitting.html) 을 구현 하 `$A` 고 `$B` 가장 적합 한 *y = ax + b*의 줄을 매개 변수화 합니다. 높은 school을 다시 시작 합니다.

볼륨의 속성을 `SizeRemaining` 추세 (슬로프)로 나누면 `$A` 볼륨이 가득 찼을 때까지 현재 저장소 성장 속도에서 일 수를 crudely 수 있습니다. `Format-Bytes`, `Format-Trend` 및 `Format-Days` 도우미 함수는 출력을 beautify 합니다.

   > [!IMPORTANT]
   > 이 예측은 선형 이며 가장 최근 14 일간의 측정만을 기준으로 합니다. 더 정교 하 고 정확한 기술이 있습니다. 저장소 확장에 투자할 지 여부를 결정 하기 위해이 스크립트를 단독으로 사용 하지 말고 좋은 judgement을 사용 하세요. 여기에는 교육용 으로만 제공 됩니다.

### <a name="script"></a>스크립트

스크립트는 다음과 같습니다.

```

Function Format-Bytes {
    Param (
        $RawValue
    )
    $i = 0 ; $Labels = ("B", "KB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB")
    Do { $RawValue /= 1024 ; $i++ } While ( $RawValue -Gt 1024 )
    # Return
    [String][Math]::Round($RawValue) + " " + $Labels[$i]
}

Function Format-Trend {
    Param (
        $RawValue
    )
    If ($RawValue -Eq 0) {
        "0"
    }
    Else {
        If ($RawValue -Gt 0) {
            $Sign = "+"
        }
        Else {
            $Sign = "-"
        }
        # Return
        $Sign + $(Format-Bytes [Math]::Abs($RawValue)) + "/day"
    }
}

Function Format-Days {
    Param (
        $RawValue
    )
    [Math]::Round($RawValue)
}

$CSV = Get-Volume | Where-Object FileSystem -Like "*CSV*"

$Output = $CSV | ForEach-Object {

    $N = 14 # Require 14 days of history

    $Data = $_ | Get-ClusterPerf -VolumeSeriesName "Volume.Size.Available" -TimeFrame "LastYear" | Sort-Object Time | Select-Object -Last $N

    If ($Data.Length -Ge $N) {

        # Last N days as (x, y) points
        $PointsXY = @()
        1..$N | ForEach-Object {
            $PointsXY += [PsCustomObject]@{ "X" = $_ ; "Y" = $Data[$_-1].Value }
        }

        # Linear (y = ax + b) least squares algorithm
        $MeanX = ($PointsXY | Measure-Object -Property X -Average).Average
        $MeanY = ($PointsXY | Measure-Object -Property Y -Average).Average
        $XX = $PointsXY | ForEach-Object { $_.X * $_.X }
        $XY = $PointsXY | ForEach-Object { $_.X * $_.Y }
        $SSXX = ($XX | Measure-Object -Sum).Sum - $N * $MeanX * $MeanX
        $SSXY = ($XY | Measure-Object -Sum).Sum - $N * $MeanX * $MeanY
        $A = ($SSXY / $SSXX)
        $B = ($MeanY - $A * $MeanX)
        $RawTrend = -$A # Flip to get daily increase in Used (vs decrease in Remaining)
        $Trend = Format-Trend $RawTrend

        If ($RawTrend -Gt 0) {
            $DaysToFull = Format-Days ($_.SizeRemaining / $RawTrend)
        }
        Else {
            $DaysToFull = "-"
        }
    }
    Else {
        $Trend = "InsufficientHistory"
        $DaysToFull = "-"
    }

    [PsCustomObject]@{
        "Volume"     = $_.FileSystemLabel
        "Size"       = Format-Bytes ($_.Size)
        "Used"       = Format-Bytes ($_.Size - $_.SizeRemaining)
        "Trend"      = $Trend
        "DaysToFull" = $DaysToFull
    }
}

$Output | Format-Table
```

## <a name="sample-6-memory-hog-you-can-run-but-you-cant-hide"></a>샘플 6: Memory hog (실행 가능 하지만 숨길 수 없음)

성능 기록은 전체 클러스터에 대해 중앙에서 수집 되 고 저장 되므로 Vm이 호스트 간에 이동 하는 횟수에 관계 없이 여러 컴퓨터의 데이터를 연결할 필요가 없습니다. 이 샘플에서는 기간에서 시리즈를 사용 하 여 `VM.Memory.Assigned` `LastMonth` 최근 35 일 동안 가장 많은 메모리를 사용 하는 가상 머신을 식별 합니다.

### <a name="screenshot"></a>스크린샷

아래 스크린샷에서는 지난 달의 메모리 사용량 별로 상위 10 개의 가상 머신이 표시 됩니다.

![PowerShell의 스크린샷](media/performance-history/Show-TopMemoryVMs.png)

### <a name="how-it-works"></a>작동 방법

`Invoke-Command`위에서 소개한 트릭을 `Get-VM` 모든 서버에서 반복 합니다. 를 사용 `Measure-Object -Average` 하 여 모든 VM에 대 한 월별 평균을 구한 다음를 사용 하 여 `Sort-Object` `Select-Object -First 10` 순위표을 가져옵니다. (또는 *가장 원하는* 목록 인가요?)

### <a name="script"></a>스크립트

스크립트는 다음과 같습니다.

```
$Output = Invoke-Command (Get-ClusterNode).Name {
    Function Format-Bytes {
        Param (
            $RawValue
        )
        $i = 0 ; $Labels = ("B", "KB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB")
        Do { if( $RawValue -Gt 1024 ){ $RawValue /= 1024 ; $i++ } } While ( $RawValue -Gt 1024 )
        # Return
        [String][Math]::Round($RawValue) + " " + $Labels[$i]
    }

    Get-VM | ForEach-Object {
        $Data = $_ | Get-ClusterPerf -VMSeriesName "VM.Memory.Assigned" -TimeFrame "LastMonth"
        If ($Data) {
            $AvgMemoryUsage = ($Data | Measure-Object -Property Value -Average).Average
            [PsCustomObject]@{
                "VM" = $_.Name
                "AvgMemoryUsage" = Format-Bytes $AvgMemoryUsage.Value
                "RawAvgMemoryUsage" = $AvgMemoryUsage.Value # For sorting...
            }
        }
    }
}

$Output | Sort-Object RawAvgMemoryUsage -Descending | Select-Object -First 10 | Format-Table PsComputerName, VM, AvgMemoryUsage
```

이것으로 끝입니다. 이러한 샘플을 영감 하 고 시작 하는 데 도움을 받으세요. 스토리지 공간 다이렉트 성능 기록과 강력 하 고 스크립팅이 편리한 cmdlet을 사용 하 여 `Get-ClusterPerf` 질문 하 고 답변할 수 있습니다. – Windows Server 2019 인프라를 관리 하 고 모니터링 하는 경우 복잡 한 질문입니다.

## <a name="additional-references"></a>추가 참조

- [Windows PowerShell 시작](https://docs.microsoft.com/powershell/scripting/getting-started/getting-started-with-windows-powershell)
- [스토리지 공간 다이렉트 개요](storage-spaces-direct-overview.md)
- [성능 기록](performance-history.md)
