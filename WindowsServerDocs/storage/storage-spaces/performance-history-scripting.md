---
title: 저장소 공간 다이렉트 성능 기록 된 스크립트
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 05/15/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: cc8ebcaaf7cc39cfadb0ebcec71ed573b436b466
ms.sourcegitcommit: 78ecb64cac789751abf9fd3f55b4a1fcbbe4dad2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/10/2018
ms.locfileid: "8843111"
---
# PowerShell 및 저장소 공간 다이렉트 성능 기록 된 스크립트

> 적용 대상: Windows Server Insider Preview 빌드 17692 이상

Windows Server 2019의 [저장소 공간 다이렉트](storage-spaces-direct-overview.md) 를 기록 하 고 가상 컴퓨터, 서버, 드라이브, 볼륨, 네트워크 어댑터 등에 대 한 광범위 한 [성능 기록이](performance-history.md) 저장 합니다. 성능 기록 쿼리 및 PowerShell의 프로세스를 쉽게 이므로 다음과 같은 질문에 *대답 실제* *원시 데이터* 에서 신속 하 게 이동할 수 있습니다.

1. 된 CPU 스파이크 지난 주?
2. 실제 디스크 비정상적인 대기 시간 현상이?
3. Vm 저장소 IOPS 가장 지금 바로 사용 하는?
4. 내 네트워크 대역폭 포화
5. 공간이 부족이 볼륨을 실행 하는 경우
6. 지난 달 Vm 가장 많은 메모리를 사용 합니까?

`Get-ClusterPerf` cmdlet은 스크립팅 위해 제작 되었습니다. Cmdlet 등의 입력을 받아들이는 `Get-VM` 또는 `Get-PhysicalDisk` 와 같은 유틸리티 cmdlet에 출력 파이프 수 파이프라인의 연결을 처리 하 여 `Sort-Object`, `Where-Object`, 및 `Measure-Object` 신속 하 게 강력한 쿼리를 작성 하 합니다.

**이 항목에서는 하 고 위의 6 질문에 대답 하는 6 샘플 스크립트에 설명 합니다.** 이러한 제공할 패턴 봉우리 찾기, 평균 찾기, 추세 선을 그릴, 탐지 및 다양 한 데이터 및 기간에서 더 outlier 실행을 적용할 수 있습니다. 복사, 확장 및 다시 사용할 수 있는 무료 시작 코드도 제공 됩니다.

   > [!NOTE]
   > 편의 위해 예제 스크립트 고품질 PowerShell 코드의 예상 대로 오류 처리 기능은 생략 합니다. 주로 영감 및 교육 위한 것은 프로덕션 대신 사용 합니다.

## 예제 1: CPU를 확인 하려면 있습니다!

이 샘플에서는 사용 합니다 `ClusterNode.Cpu.Usage` 에서 일련의 `LastWeek` 클러스터에서 최대 ("상위 워터 마크"), 모든 서버에 대 한 최소 및 평균 CPU 사용량을 표시 하는 기간입니다. 간단한 사분 위 분석을 몇 시간 동안 CPU 사용량 25%를 넘는 표시도 수행 50% 및 75 %8 일 이내입니다.

### 스크린샷

아래 스크린샷에서 *서버 02* 가 지난 주 설명할 수 없는 스파이크를 확인 합니다.

![PowerShell의 스크린샷](media/performance-history/Show-CpuMinMaxAvg.png)

### 작동 방식

출력을 `Get-ClusterPerf` 기본 제공에 깔끔하게 파이프 `Measure-Object` cmdlet을 방금 지정는 `Value` 속성. 사용 하 여 해당 `-Maximum`, `-Minimum`, 및 `-Average` 플래그를 `Measure-Object` 구할 처음 세 개의 열 거의 대 한 무료입니다. 사분 위 분석을 수행 하기에 파이프 수에서는 `Where-Object` 하 고 계산 된 값의 개수 `-Gt` (보다 큼) 25, 50 또는 75 합니다. 마지막 단계는 사용 하 여 beautify 하는 `Format-Hours` 및 `Format-Percent` 도우미 함수 – 확실히 선택 사항입니다.

### 스크립트

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

## 예제 2: 실행, 실행, 대기 시간 outlier

이 샘플에서는 사용 합니다 `PhysicalDisk.Latency.Average` 에서 일련의 `LastHour` 평균 대기 시간 초과 + 3σ 드라이브로 통계 이루어진 검색할 시간 범위 정의 (세 가지 표준 편차) 인구 평균 합니다.

   > [!IMPORTANT]
   > 편의 위해에 대 한이 스크립트 부분 누락 된 데이터를 처리 하지 않는, 모델 또는 펌웨어 등으로 구분 하지 않으며 낮은 차이 대 한 보호 기능을 구현 하지 않습니다. 하드 디스크를 교체 것인지 결정에이 스크립트에 의존 하지 않는 한 하십시오 좋은 관행을 실행 합니다. 아래 교육 목적 으로만 제공 됩니다.

### 스크린샷

아래 스크린샷에서 없는 이루어진 참조.

![PowerShell의 스크린샷](media/performance-history/Show-LatencyOutlierHDD.png)

### 작동 방식

확인 하 여 유휴 상태 이거나 거의 유휴 드라이브를 제외 하는 먼저 `PhysicalDisk.Iops.Total` 계속 `-Gt 1`. 파이프 하는 모든 활성 HDD에 대 한 해당 `LastHour` 시간 범위에서 이루어진 360 측정 10 초 간격으로 `Measure-Object -Average` 평균 대기 시간이 지난 시간에서 얻을 수 있습니다. 이 사용자를 설정합니다.

평균 찾으려고 [널리 알려진 수식](http://www.mathsisfun.com/data/standard-deviation.html) 구현 `μ` 고 표준 편차가 `σ` 인구입니다. 모든 활성 HDD에 대 한 인구 평균 평균 대기 시간은 비교 하 고 표준 편차가 나누어 합니다. 원시 값을 유지할 수 있도록 `Sort-Object` 결과 사용 하지만 `Format-Latency` 및 `Format-StandardDeviation` 도우미 함수를 어떻게 하겠습니다 – 확실히 선택적 beautify 합니다.

드라이브가 경우 이상 + 3σ,에서는 `Write-Host` 빨간색입니다. 녹색으로 그렇지 않은 경우.

### 스크립트

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

## 예제 3: 소음? 쓰기입니다!

성능 기록 *지금 바로*대 한 질문을 너무 응답할 수 있습니다. 실시간에서 사용할 수 있는 새로운 측정, 10 초 마다 합니다. 이 샘플에서는 사용은 `VHD.Iops.Total` 에서 일련의 `MostRecent` 최대 사용률이 (일부 말할 수 "noisiest")를 식별 하는 기간 클러스터 및 해당 활동의 읽기/쓰기 세분화 되어 표시의 모든 호스트 IOPS을 저장소 가장 많이 사용 되는 가상 컴퓨터.

### 스크린샷

아래 스크린샷에서 저장소 작업 Top 10 가상 컴퓨터의 참조.

![PowerShell의 스크린샷](media/performance-history/Show-TopIopsVMs.png)

### 작동 방식

달리 `Get-PhysicalDisk`, `Get-VM` cmdlet 클러스터 인식 되지 – 로컬 서버에서 Vm만 반환 합니다. 이 호출의 동시에 모든 서버에서 쿼리를 래핑할 `Invoke-Command (Get-ClusterNode).Name { ... }`. 얻은 모든 VM에는 `VHD.Iops.Total`, `VHD.Iops.Read`, 및 `VHD.Iops.Write` 측정 합니다. 지정 하지는 `-TimeFrame` 매개 변수를 가져오도록 합니다 `MostRecent` 각각에 대 한 데이터 요소를 단일 합니다.

   > [!TIP]
   > 이러한 일련의 모든 VHD/VHDX 파일에이 VM 작업의 합계를 반영합니다. 여기서 성능 기록 되 고 자동으로 집계 한 예입니다. VHD/VHDX 분석 결과 얻으려면 개인 파이프 수 `Get-VHD` 에 `Get-ClusterPerf` VM 대신 합니다.

와 함께 제공 되는 모든 서버에서 결과 `$Output`, 수 있는 `Sort-Object` 및 `Select-Object -First 10`합니다. 태그 `Invoke-Command` 사용 하 여 결과 데코 레이트는 `PsComputerName` 나타내는 원본 위치에서 우리 VM이 실행 되는 위치를 인쇄할 수 있는 속성.

### 스크립트

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

## 예제 4:으로 "25 기가 새 10 기가"

이 샘플에서는 사용 합니다 `NetAdapter.Bandwidth.Total` 에서 일련의 `LastDay` 으로 정의 된 네트워크 채도 공격의 징후를 검색할 시간 범위 > 이론적 최대 대역폭의 90% 합니다. 클러스터의 모든 네트워크 어댑터에 명시 된 연결 속도를 마지막 날 가장 높은 관찰 된 대역폭 사용을 비교합니다.

### 스크린샷

아래 스크린샷에서 하나의 *Pro #2-4 Fabrikam NX* 피크 마지막 날에는 참조.

![PowerShell의 스크린샷](media/performance-history/Show-NetworkSaturation.png)

### 작동 방식

반복 하는 `Invoke-Command` 를 위에서 트릭 `Get-NetAdapter` 모든 서버와에 파이프 `Get-ClusterPerf`합니다. 두 개의 관련 속성을 가져옵니다에서는 프로세스를 진행: 해당 `LinkSpeed` "10 g b p s"를 지정 하 고 해당 원시와 같은 문자열 `Speed` 10000000000 같은 정수입니다. 사용 하 여 `Measure-Object` 마지막 날부터 평균 및 최고를 얻을 수 (미리 알림: 각 측정에는 `LastDay` 기간을 5 분 나타냅니다) 사과-사과 비교를 가져오려면 바이트 당 8 비트를 곱해 합니다.

   > [!NOTE]
   > Chelsio, 등의 일부 공급 업체에 포함 되어 있으므로 해당 *네트워크 어댑터* 성능 카운터에 원격 직접 메모리 액세스 (RDMA) 작업을 포함 합니다 `NetAdapter.Bandwidth.Total` 시리즈입니다. 기타 Mellanox, 같은 하지 않을 수 있습니다. 공급 업체 없는 추가 하기만 하는 경우는 `NetAdapter.Bandwidth.RDMA.Total` 이 스크립트의 버전에서 시리즈 합니다.

### 스크립트

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

## 예제 5: 저장소 최신 유행을 따르고 있는 다시 사이트로!

매크로 추세를 살펴보는 성능 기록 최대 1 년 동안 유지 됩니다. 이 샘플에서는 사용 합니다 `Volume.Size.Available` 에서 일련의 `LastYear` 전체 되는 저장소 채우는 속도 예상 수치를 결정 하는 기간입니다.

### 스크린샷

아래 스크린샷에서 15GB 하루를 추가 하는 *백업* 볼륨을 참조 합니다.

![PowerShell의 스크린샷](media/performance-history/Show-StorageTrend.png)

이 속도로 다른 42 일 후에는 용량을 도달지 것입니다.

### 작동 방식

`LastYear` 시간 범위는 하루 한 데이터 요소입니다. 된 라인에 맞게 두 지점만 엄격 하 게 해야 하지만 실제로 것이 좋습니다 14 일 같은 더 필요 합니다. 사용 하 여 `Select-Object -Last 14` [1, 14] 범위에 대 한 *x* *(x, y)* 점 배열을 설정 합니다. 이러한 요소를 사용 하 여 찾을 수 간단한 [선형 예상값 알고리즘](http://mathworld.wolfram.com/LeastSquaresFitting.html) 을 구현 `$A` 및 `$B` 하는 가장 적합 한 줄을 매개 변수화 *y = ax + b*합니다. 시작 학생부터 다시 합니다.

볼륨의 분할 `SizeRemaining` 추세 속성 (기울기 `$A`) 끝났음을 crudely 볼륨 가득 찰 때까지 저장소 증가의 현재 속도로 일 수를 예측 합니다. `Format-Bytes`, `Format-Trend`, 및 `Format-Days` 도우미 함수 beautify 출력 합니다.

   > [!IMPORTANT]
   > 이 추정 선형 및 최근 14 일일 측정 기준입니다. 더 정교 하 고 정확 하 게 기술 존재합니다. 저장소 확장에 대 한 투자를 사용할지 결정에이 스크립트에 의존 하지 않는 한 하십시오 좋은 관행을 실행 합니다. 아래 교육 목적 으로만 제공 됩니다.

### 스크립트

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

## 예제 6: 실행할 수 메모리 소비량이 있지만 숨길 수 없습니다.

성능 기록 이므로 수집 하 고를 하는 방법에 관계 없이 서로 다른 컴퓨터의 데이터를 여러 번 필요 하지 않는 사용자 전체 클러스터에 대 한 중앙에서 저장 된 Vm 간에 이동 호스트 합니다. 이 샘플에서는 사용 합니다 `VM.Memory.Assigned` 에서 일련의 `LastMonth` 마지막 35 일 동안 가장 많은 메모리를 사용 하 여 가상 컴퓨터를 식별 하는 기간입니다.

### 스크린샷

아래 스크린샷에서 지난 달의 메모리 사용 하 여 Top 10 가상 컴퓨터의 참조.

![PowerShell의 스크린샷](media/performance-history/Show-TopMemoryVMs.png)

### 작동 방식

반복 우리의 `Invoke-Command` 트릭을으로, 위에서 소개 `Get-VM` 모든 서버에 있습니다. 사용 하 여 `Measure-Object -Average` 다음 모든 VM에 대 한 월별 평균을 얻으려면 `Sort-Object` 뒤에 `Select-Object -First 10` 우리의 순위표 얻을 수 있습니다. (또는 *가장 원하는* list? 이기 해야 할 수도)

### 스크립트

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

이제 되었습니다. 다행히 이러한 샘플 영감 하 여 시작 합니다. 저장소 공간 다이렉트 성능 기록 및에서 강력한 스크립팅 친화적인 `Get-ClusterPerf` cmdlet을 – 하며 응답 임 파워 됩니다! -복잡 한 질문을 관리 하 고 Windows Server 2019 인프라를 모니터링 합니다.

## 참고 항목

- [Windows PowerShell을 시작 하기](https://docs.microsoft.com/powershell/scripting/getting-started/getting-started-with-windows-powershell)
- [저장소 공간 다이렉트 개요](storage-spaces-direct-overview.md)
- [성능 기록](performance-history.md)
