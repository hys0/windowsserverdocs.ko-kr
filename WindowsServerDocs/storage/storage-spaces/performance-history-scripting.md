---
title: 성능 기록 저장소 공간 다이렉트를 사용 하 여 스크립팅
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 05/15/2018
Keywords: 저장소 공간 다이렉트
ms.localizationpriority: medium
ms.openlocfilehash: cc8ebcaaf7cc39cfadb0ebcec71ed573b436b466
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816324"
---
# <a name="scripting-with-powershell-and-storage-spaces-direct-performance-history"></a>성능 기록 PowerShell 및 저장소 공간 다이렉트를 사용 하 여 스크립팅

> 적용 대상: Windows Server Insider Preview 빌드 17692 이상

Windows Server 2019 [저장소 공간 다이렉트](storage-spaces-direct-overview.md) 레코드 및 광범위 한 저장소 [성능 기록](performance-history.md) 가상 컴퓨터, 서버, 드라이브, 볼륨, 네트워크 어댑터, 등에 대 한 합니다. 성능 기록 이므로 쿼리 및 프로세스를 PowerShell에서에서 쉽게에서 신속 하 게 이동할 수 있습니다 *원시 데이터* 하 *실제 답변* 다음과 같은 질문에:

1. 있었습니까 모든 CPU 스파이크 지난주?
2. 모든 실제 디스크는 비정상적 대기 시간을 나타내는?
3. Vm이 사용 하는 저장소 IOPS 가장 지금?
4. 내 네트워크 대역폭을 포화?
5. 이 볼륨 사용 가능한 공간이 부족 하면 실행 됩니까?
6. 지난 달에 가장 많은 메모리를 사용 하는 Vm이?

`Get-ClusterPerf` cmdlet 스크립팅에 빌드됩니다. 와 같은 cmdlet의 입력을 받아들이는지 `Get-VM` 또는 `Get-PhysicalDisk` 와 같은 유틸리티 cmdlet에 해당 출력을 파이프할 수을 연결 하 고 처리 하는 파이프라인에 의해 `Sort-Object`를 `Where-Object`, 및 `Measure-Object` 신속 하 게 강력한 쿼리를 작성 하 합니다.

**이 항목에서는 고 위의 6 질문에 대답 하는 6 샘플 스크립트에 설명 합니다.** 이러한 표시 패턴 최대치를 찾을, 평균을 찾으려면, 추세 선 그리기, 감지 및 다양 한 데이터 및 기간에서 더 이상 실행에 적용할 수 있습니다. 무료 시작 코드를 복사, 확장 및 재사용할 수로 제공 됩니다.

   > [!NOTE]
   > 간단히 하기 위해 샘플 스크립트는 고품질 PowerShell 코드의 예상 오류 처리 등을 생략 합니다. 이러한 용도로 주로 영감 및 education 프로덕션 하는 대신 사용 합니다.

## <a name="sample-1-cpu-i-see-you"></a>샘플 1: CPU, 볼!

이 샘플에서는 합니다 `ClusterNode.Cpu.Usage` 시리즈를 `LastWeek` 클러스터의 모든 서버에 대 한 최소 및 평균 CPU 사용량을 최대값 ("상위 워터 마크")를 표시 하는 기간. 이 메서드에서 얼마나 많은 CPU 시간 사용 25%가 넘는 표시할 분석 간단한 사분 위 수는 50%에 만들어지고 지난 8 일 동안에서 75%입니다.

### <a name="screenshot"></a>스크린샷

아래 스크린샷에서 했습니다 보면 *서버-02* 지난주를 설명할 수 없는 급증 했습니다.

![PowerShell 스크린샷](media/performance-history/Show-CpuMinMaxAvg.png)

### <a name="how-it-works"></a>작동 방법

출력 `Get-ClusterPerf` 기본 제공에 원활 하 게 파이프 `Measure-Object` cmdlet만 지정 합니다 `Value` 속성입니다. 사용 하 여 해당 `-Maximum`, `-Minimum`, 및 `-Average` 플래그 `Measure-Object` 제공 처음 세 열 거의 대 한 무료입니다. 사분 위 수 분석을 수행 하기에 파이프할 수 있습니다 `Where-Object` 계산 된 값의 개수 및 `-Gt` (보다 큼) 25, 50, 75입니다. 마지막 단계는 사용 하 여 beautify `Format-Hours` 고 `Format-Percent` 도우미 함수 – 확실히 선택 사항입니다.

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

## <a name="sample-2-fire-fire-latency-outlier"></a>샘플 2: 실행, 실행, 대기 시간 이상 값

이 샘플에서는 합니다 `PhysicalDisk.Latency.Average` 시리즈는 `LastHour` 시간당 평균 대기 시간 초과 + 3σ 드라이브로 통계 이상 값을 검색할 기간 정의 (3 개의 표준 편차) 채우기 평균 초과 합니다.

   > [!IMPORTANT]
   > 간단히 하기 위해이 스크립트 부분 누락 된 데이터를 처리 하지 않습니다, 그리고 모델 또는 펌웨어 등을 구분 하지 않습니다 낮은 차이 대 한 보호를 구현 하지 않습니다. 하세요 좋은 관행을 연습 하 고 하드 디스크를 교체 여부를 결정 하는 단독으로이 스크립트에 의존 하지 마십시오. 아래 교육용 으로만 제공 됩니다.

### <a name="screenshot"></a>스크린샷

아래 스크린샷에서 알 수 없는 이상 값을 가지:

![PowerShell 스크린샷](media/performance-history/Show-LatencyOutlierHDD.png)

### <a name="how-it-works"></a>작동 방법

첫째, 유휴 또는 거의 유휴 상태 드라이브를 확인 하 여 제외 `PhysicalDisk.Iops.Total` 지속적으로 `-Gt 1`입니다. 파이프에서는 모든 활성 HDD에 대 한 해당 `LastHour` 이루어져 360 측정 10 초 간격으로 시간 `Measure-Object -Average` 지난 시간 동안에서 해당 평균 대기 시간을 가져오려고 합니다. 이 인구를 설정합니다.

구현 된 [널리 알려진 수식](http://www.mathsisfun.com/data/standard-deviation.html) 평균을 찾으려면 `μ` 및 표준 편차 `σ` 모집단의 합니다. 모든 활성 HDD에 대 한 채우기 평균 해당 평균 대기 시간을 비교 하 고 표준 편차로 나눕니다. 수 있도록 원시 값을 유지 `Sort-Object` 사용 하 여 결과 `Format-Latency` 고 `Format-StandardDeviation` 어떤 살펴보겠습니다 – 확실히 선택적 beautify에 도우미 함수입니다.

드라이브가 경우 개 + 3σ,에서는 `Write-Host` 빨간색; 그렇지 않으면 녹색에서입니다.

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

## <a name="sample-3-noisy-neighbor-thats-write"></a>샘플 3: 시끄러운 이웃? 쓰기입니다.

성능 기록에 대 한 질문에 대답할 수 *지금*도 합니다. 새 측정값을 실시간으로 사용할 수 있는, 10 초 마다. 이 샘플에서는 합니다 `VHD.Iops.Total` 시리즈는 `MostRecent` (일부 한다고 여 긴 "noisiest") 사용자를 식별 하는 기간 클러스터의 모든 호스트 저장소 IOPS, 가장을 사용 하는 가상 컴퓨터에 대 한 읽기/쓰기 분석을 표시 하 고 해당 작업입니다.

### <a name="screenshot"></a>스크린샷

아래 스크린샷에 저장소 활동에서 상위 10 개 가상 컴퓨터가 표시 됩니다.

![PowerShell 스크린샷](media/performance-history/Show-TopIopsVMs.png)

### <a name="how-it-works"></a>작동 방법

와 달리 `Get-PhysicalDisk`, `Get-VM` cmdlet는 클러스터를 인식 하지 않습니다 – 로컬 서버에서 Vm만 반환 합니다. 래핑할 호출에서 동시에 모든 서버를 쿼리하려면 `Invoke-Command (Get-ClusterNode).Name { ... }`합니다. 얻게 모든 VM에 대 한 합니다 `VHD.Iops.Total`, `VHD.Iops.Read`, 및 `VHD.Iops.Write` 측정 합니다. 지정 하지는 `-TimeFrame` 얻게 매개 변수는 `MostRecent` 각각에 대 한 단일 지점에서 데이터.

   > [!TIP]
   > 이 시리즈의 모든 VHD/VHDX 파일에이 VM의이 작업의 합계를 반영합니다. 여기서 성능 기록을 자동으로 집계 중인 한 예입니다. VHD/VHDX 파일에 대 한 분석을 가져오려면 개별을 파이프할 수 있습니다 `Get-VHD` 에 `Get-ClusterPerf` VM 대신 합니다.

와 함께 제공 되는 모든 서버에서 결과 `$Output`, 수 있는 `Sort-Object` 차례로 `Select-Object -First 10`합니다. 있음을 `Invoke-Command` 사용 하 여 결과 데코레이팅하는 `PsComputerName` 출처에서 VM이 실행 되는 위치를 알고에서는 인쇄할 수는 나타내는 속성입니다.

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

## <a name="sample-4-as-they-say-25-gig-is-the-new-10-gig"></a>샘플 4: 이러한 예를 들어 "25 기가 새 10 기가"

이 샘플에서는 합니다 `NetAdapter.Bandwidth.Total` 시리즈는 `LastDay` 네트워크 채도를 검색할 기간으로 정의 > 이론적 최대 대역폭의 90%입니다. 클러스터의 모든 네트워크 어댑터에 대해 언급 된 링크 속도에 마지막 날에 관찰 된 대역폭 사용량이 가장 높은 비교합니다.

### <a name="screenshot"></a>스크린샷

아래 스크린샷에서 것을 볼 하나 *Fabrikam NX 4 Pro #2* 마지막 날에 최고점에 도달 했습니다.

![PowerShell 스크린샷](media/performance-history/Show-NetworkSaturation.png)

### <a name="how-it-works"></a>작동 방법

반복 우리의 `Invoke-Command` 을 위에서 트릭은 `Get-NetAdapter` 모든 서버 및 파이프에 `Get-ClusterPerf`입니다. 그 과정에서 두 개의 관련 속성을 잡고 했습니다: 해당 `LinkSpeed` 등 "10gbps"는 원시 문자열 `Speed` 10000000000과 같은 정수입니다. 사용 하 여 `Measure-Object` 어제 평균 및 최대 사용을 가져오려고 (미리 알림: 각 측정을 `LastDay` 기간 5 분을 나타냅니다)를 사과-사과 비교를 가져오려면 바이트 당 8 비트를 곱합니다.

   > [!NOTE]
   > Chelsio와 같은 일부 공급 업체에서 원격 직접 메모리 액세스 (RDMA) 활동을 포함 자신의 *네트워크 어댑터* 성능 카운터에 포함 되어 있으므로 `NetAdapter.Bandwidth.Total` 시리즈입니다. 다른 Mellanox, 같은 행위입니다. 공급 업체에 추가 하지 않는 경우는 `NetAdapter.Bandwidth.RDMA.Total` 계열에이 스크립트의 버전입니다.

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

## <a name="sample-5-make-storage-trendy-again"></a>샘플 5: 저장소 최신 유행을 따르고 있는 작업을 다시 수행.

매크로 추세를 살펴보려면 성능 기록 최대 1 년 동안 보존 됩니다. 이 샘플에서는 합니다 `Volume.Size.Available` 시리즈는 `LastYear` 가득 차게 됩니다 때 저장소 가득 속도 및 예측을 확인 하는 기간.

### <a name="screenshot"></a>스크린샷

아래 스크린샷에 표시 된 *백업* 15GB 하루를 추가 하는 볼륨:

![PowerShell 스크린샷](media/performance-history/Show-StorageTrend.png)

이 속도 다른 42 일 후에 해당 용량에 도달 하 합니다.

### <a name="how-it-works"></a>작동 방법

`LastYear` 기간에 매일 하나의 데이터 요소입니다. 추세 선을 맞게 두 지점에만 엄격 하 게 필요는 없지만 실제로 것이 좋습니다에 14 일 같은 많은 메모리가 필요 합니다. 사용 하 여 `Select-Object -Last 14` 배열을 설정 하려면 *(x, y)* 지점에 대 한 *x* 범위는 [1, 14]. 이러한 지점과 간단 하 게 구현 [최소 자승 선형 알고리즘](http://mathworld.wolfram.com/LeastSquaresFitting.html) 찾으려고 `$A` 하 고 `$B` 줄 맞춤을 매개 변수화 하는 *y = ax + b*합니다. 시작 고등학교 도처 다시 합니다.

볼륨의 분할 `SizeRemaining` 추세 속성 (기울기 `$A`) 투박한 볼륨이 꽉 찰 때까지 기간 (일) 저장소 증가의 현재 요금으로 예측할 수 있습니다. 합니다 `Format-Bytes`, `Format-Trend`, 및 `Format-Days` 도우미 함수 beautify 출력 합니다.

   > [!IMPORTANT]
   > 이 예상 선형 이며 가장 최근의 14 일일 측정값에 대해서만 기반 합니다. 더 정교 하 고 정확한 기법이 있습니다. 하세요 좋은 관행을 연습 하 고 저장소를 확장 하는 데 투자 여부를 결정 하는 단독으로이 스크립트에 의존 하지 마십시오. 아래 교육용 으로만 제공 됩니다.

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

## <a name="sample-6-memory-hog-you-can-run-but-you-cant-hide"></a>샘플 6: 메모리 소비량이 있습니다를 실행할 수 있지만 숨길 수 없습니다.

성능 기록 되므로 수집 되 고 함께 붙이기 위한 관계 없이 다른 컴퓨터의에서 데이터를 여러 번 필요 하지 않는 사용자 전체 클러스터에 대 한 중앙 집중식으로 저장 Vm 호스트 간에 이동 합니다. 이 샘플에서는 합니다 `VM.Memory.Assigned` 시리즈는 `LastMonth` 지난 35 일 동안 가장 많은 메모리를 사용 하 여 가상 머신을 식별 하는 기간.

### <a name="screenshot"></a>스크린샷

아래 스크린샷에 지난달 메모리 사용량에 따른 상위 10 개 가상 컴퓨터가 표시 됩니다.

![PowerShell 스크린샷](media/performance-history/Show-TopMemoryVMs.png)

### <a name="how-it-works"></a>작동 방법

반복 우리의 `Invoke-Command` 기법으로, 위에서 도입 된 `Get-VM` 모든 서버. 사용 하 여 `Measure-Object -Average` 다음 모든 VM에 대 한 월별 평균을 얻으려면 `Sort-Object` 뒤에 `Select-Object -First 10` 우리의 순위표를 가져오려고 합니다. (또는 보는 것이 우리의 *가장 원하는* 목록?)

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

정말 간단하죠. 다행히 이러한 샘플 영감 하 고 시작할 수 있도록 지원 합니다. 저장소 공간 다이렉트 성능 기록 및 강력한 스크립팅이 쉬운 `Get-ClusterPerf` cmdlet을 – 요청 및 응답에 제공 됩니다! – 복잡 한 질문을 관리 하 고 Windows Server 2019 인프라를 모니터링 합니다.

## <a name="see-also"></a>참조

- [Windows PowerShell 시작](https://docs.microsoft.com/powershell/scripting/getting-started/getting-started-with-windows-powershell)
- [저장소 공간 다이렉트 개요](storage-spaces-direct-overview.md)
- [성능 기록](performance-history.md)
