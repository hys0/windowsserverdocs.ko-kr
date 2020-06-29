---
title: 스토리지 공간 다이렉트에 대 한 성능 기록
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0c8adf5f5586bd9f86ed3c4cd42b6172ff3f91e7
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474700"
---
# <a name="performance-history-for-storage-spaces-direct"></a>스토리지 공간 다이렉트에 대 한 성능 기록

> 적용 대상: 시작

성능 기록은 관리자가 호스트 서버, 드라이브, 볼륨, 가상 컴퓨터 등에서 기록 된 계산, 메모리, 네트워크 및 저장소 측정에 쉽게 액세스할 수 있도록 하 [스토리지 공간 다이렉트](storage-spaces-direct-overview.md) 는 새로운 기능입니다. 최대 1 년 동안 성능 기록이 자동으로 수집 되 고 클러스터에 저장 됩니다.

   > [!IMPORTANT]
   > 이 기능은 Windows Server 2019에 새로 있습니다. Windows Server 2016에서는 사용할 수 없습니다.

## <a name="get-started"></a>시작하기

성능 기록은 Windows Server 2019의 스토리지 공간 다이렉트를 사용 하 여 기본적으로 수집 됩니다. 모든 항목을 설치, 구성 또는 시작할 필요는 없습니다. 인터넷 연결이 필요 하지 않으며, System Center가 필요 하지 않으며, 외부 데이터베이스가 필요 하지 않습니다.

클러스터의 성능 기록을 그래픽으로 보려면 [Windows 관리 센터](../../manage/windows-admin-center/understand/windows-admin-center.md)를 사용 합니다.

![Windows 관리 센터의 성능 기록](media/performance-history/perf-history-in-wac.png)

프로그래밍 방식으로 쿼리 및 처리 하려면 새 cmdlet을 사용 `Get-ClusterPerf` 합니다. [PowerShell에서 사용을](#usage-in-powershell)참조 하세요.

## <a name="whats-collected"></a>수집 되는 내용

성능 기록은 다음과 같은 7 가지 유형의 개체에 대해 수집 됩니다.

![개체의 유형](media/performance-history/types-of-object.png)

각 개체 유형에는 여러 계열이 있습니다. 예를 들어 `ClusterNode.Cpu.Usage` 는 각 서버에 대해 수집 됩니다.

각 개체 형식에 대해 수집 된 내용과이를 해석 하는 방법에 대 한 자세한 내용은 다음 하위 항목을 참조 하세요.

| Object             | 계열                                                                               |
|--------------------|--------------------------------------------------------------------------------------|
| 드라이브             | [드라이브에 대해 수집 되는 내용](performance-history-for-drives.md)                     |
| 네트워크 어댑터   | [네트워크 어댑터용으로 수집 되는 내용](performance-history-for-network-adapters.md) |
| 서버            | [서버에 대해 수집 되는 내용](performance-history-for-servers.md)                   |
| 가상 하드 디스크 | [가상 하드 디스크에 대해 수집 되는 내용](performance-history-for-vhds.md)           |
| 가상 머신   | [Virtual machines에 대해 수집 되는 내용](performance-history-for-vms.md)              |
| 볼륨            | [볼륨에 대해 수집 되는 내용](performance-history-for-volumes.md)                   |
| 클러스터           | [클러스터에 대해 수집 되는 내용](performance-history-for-clusters.md)                 |

많은 계열은 피어 개체에서 부모로 집계 됩니다. 예를 들어 `NetAdapter.Bandwidth.Inbound` 는 각 네트워크 어댑터에 대해 개별적으로 수집 되 고 전체 서버에 집계 됩니다. 마찬가지로는 `ClusterNode.Cpu.Usage` 전체 클러스터로 집계 됩니다.

## <a name="timeframes"></a>기간

성능 기록은 세분성을 포함 하 여 최대 1 년 동안 저장 됩니다. 가장 최근 시간에 대 한 측정은 10 초 마다 사용할 수 있습니다. 그 후에는 적절 하 게 평균 또는 합계를 계산 하 여 더 많은 시간을 포괄 하는 보다 세분화 된 계열로 지능적으로 병합 됩니다. 가장 최근 날짜의 경우 5 분 마다 측정을 사용할 수 있습니다. 최근 주에 대해 15 분 마다 합니다.

Windows 관리 센터에서 차트 위의 오른쪽 위에 있는 기간을 선택할 수 있습니다.

![Windows 관리 센터의 기간](media/performance-history/timeframes-in-honolulu.png)

PowerShell에서 `-TimeFrame` 매개 변수를 사용 합니다.

사용 가능한 기간은 다음과 같습니다.

| 시간 범위   | 측정 빈도 | 보존 기간 |
|-------------|-----------------------|--------------|
| `LastHour`  | 10 초 마다         | 1시간       |
| `LastDay`   | 5분마다       | 25 시간     |
| `LastWeek`  | 15분마다      | 8일       |
| `LastMonth` | 1 시간 마다          | 35일      |
| `LastYear`  | 1 일 마다           | 400 일     |

## <a name="usage-in-powershell"></a>PowerShell에서 사용

Cmdlet을 사용 `Get-ClusterPerformanceHistory` 하 여 PowerShell에서 성능 기록을 쿼리하고 처리 합니다.

```PowerShell
Get-ClusterPerformanceHistory
```

   > [!TIP]
   > **Get ClusterPerf** 별칭을 사용 하 여 일부 키 입력을 저장할 수 있습니다.

### <a name="example"></a>예제

지난 1 시간 동안 가상 머신 *Myvm* 의 CPU 사용량을 가져옵니다.

```PowerShell
Get-VM "MyVM" | Get-ClusterPerf -VMSeriesName "VM.Cpu.Usage" -TimeFrame LastHour
```

고급 예제를 보려면 시작 코드를 제공 하는 게시 된 [샘플 스크립트](performance-history-scripting.md) 를 사용 하 여 최대 값을 찾고, 평균을 계산 하 고, 추세 선을 플롯 하 고, 이상 값 검색을 실행 합니다.

### <a name="specify-the-object"></a>개체 지정

파이프라인에서 원하는 개체를 지정할 수 있습니다. 이는 7 가지 개체 형식으로 작동 합니다.

| 파이프라인의 개체 | 예제     |
|----------------------|-------------|
| `Get-PhysicalDisk`   | <code>Get-PhysicalDisk -SerialNumber "XYZ456" &#124; Get-ClusterPerf</code>         |
| `Get-NetAdapter`     | <code>Get-NetAdapter "Ethernet" &#124; Get-ClusterPerf</code>                       |
| `Get-ClusterNode`    | <code>Get-ClusterNode "Server123" &#124; Get-ClusterPerf</code>                     |
| `Get-VHD`            | <code>Get-VHD "C:\ClusterStorage\MyVolume\MyVHD.vhdx" &#124; Get-ClusterPerf</code> |
| `Get-VM`             | <code>Get-VM "MyVM" &#124; Get-ClusterPerf</code>                                   |
| `Get-Volume`         | <code>Get-Volume -FriendlyName "MyVolume"  &#124; Get-ClusterPerf</code>            |
| `Get-Cluster`        | <code>Get-Cluster "MyCluster" &#124; Get-ClusterPerf</code>                         |

을 지정 하지 않으면 전체 클러스터에 대 한 성능 기록이 반환 됩니다.

### <a name="specify-the-series"></a>계열 지정

다음 매개 변수를 사용 하 여 원하는 계열을 지정할 수 있습니다.


| 매개 변수                 | 예제                       | 목록                                                                                 |
|---------------------------|-------------------------------|--------------------------------------------------------------------------------------|
| `-PhysicalDiskSeriesName` | `"PhysicalDisk.Iops.Read"`    | [드라이브에 대해 수집 되는 내용](performance-history-for-drives.md)                     |
| `-NetAdapterSeriesName`   | `"NetAdapter.Bandwidth.Outbound"` | [네트워크 어댑터용으로 수집 되는 내용](performance-history-for-network-adapters.md) |
| `-ClusterNodeSeriesName`  | `"ClusterNode.Cpu.Usage"`     | [서버에 대해 수집 되는 내용](performance-history-for-servers.md)                   |
| `-VHDSeriesName`          | `"Vhd.Size.Current"`          | [가상 하드 디스크에 대해 수집 되는 내용](performance-history-for-vhds.md)           |
| `-VMSeriesName`           | `"Vm.Memory.Assigned"`        | [Virtual machines에 대해 수집 되는 내용](performance-history-for-vms.md)              |
| `-VolumeSeriesName`       | `"Volume.Latency.Write"`      | [볼륨에 대해 수집 되는 내용](performance-history-for-volumes.md)                   |
| `-ClusterSeriesName`      | `"PhysicalDisk.Size.Total"`   | [클러스터에 대해 수집 되는 내용](performance-history-for-clusters.md)                 |


   > [!TIP]
   > 탭 완성 기능을 사용 하 여 사용 가능한 계열을 검색 합니다.

을 지정 하지 않으면 지정 된 개체에 사용할 수 있는 모든 계열이 반환 됩니다.

### <a name="specify-the-timeframe"></a>기간 지정

매개 변수를 사용 하 여 원하는 기록 기간을 지정할 수 있습니다 `-TimeFrame` .

   > [!TIP]
   > 탭 완성 기능을 사용 하 여 사용 가능한 기간을 검색 합니다.

을 지정 하지 않으면 `MostRecent` 측정이 반환 됩니다.

## <a name="how-it-works"></a>작동 방법

### <a name="performance-history-storage"></a>성능 기록 저장소

스토리지 공간 다이렉트를 사용 하도록 설정 하 고 나면 이라는 약 10gb 볼륨이 `ClusterPerformanceHistory` 만들어지고, 확장 가능한 저장소 엔진 (MICROSOFT JET 라고도 함)의 인스턴스가 프로 비전 됩니다. 이 경량 데이터베이스는 관리자 개입 또는 관리 없이 성능 기록을 저장 합니다.

![성능 기록 저장소에 대 한 볼륨](media/performance-history/perf-history-volume.png)

볼륨은 저장소 공간으로 지원 되며 클러스터의 노드 수에 따라 단순, 양방향 미러 또는 3 방향 미러 복원 력을 사용 합니다. 스토리지 공간 다이렉트의 다른 볼륨과 마찬가지로 드라이브 또는 서버 오류가 발생 한 후에 복구 됩니다.

볼륨은 ReFS를 사용 하지만 CSV (클러스터 공유 볼륨는 아님) 이므로 클러스터 그룹 소유자 노드에만 표시 됩니다. 자동으로 생성 되는 것 외에도이 볼륨에 대 한 특별 한 사항은 없습니다. 즉,이 볼륨을 보거나, 탐색 하거나, 크기를 조정 하거나, 삭제할 수 있습니다 (권장 하지 않음). 문제가 발생 하는 경우 [문제 해결](#troubleshooting)을 참조 하세요.

### <a name="object-discovery-and-data-collection"></a>개체 검색 및 데이터 수집

성능 기록은 클러스터의 어디에서 나 가상 컴퓨터와 같은 관련 개체를 자동으로 검색 하 여 성능 카운터 스트리밍을 시작 합니다. 카운터는 데이터베이스에 집계, 동기화 및 삽입 됩니다. 스트리밍은 지속적으로 실행 되며 시스템에 미치는 영향을 최소화 하기 위해 최적화 됩니다.

컬렉션은 항상 사용 가능한 상태 관리 서비스에 의해 처리 됩니다. 실행 중인 노드가 중단 되 면 나중에 클러스터의 다른 노드에서 다시 시작 합니다. 성능 기록은 잠깐 경과할 수 있지만 자동으로 다시 시작 됩니다. PowerShell에서를 실행 하 여 상태 관리 서비스 및 해당 소유자 노드를 확인할 수 있습니다 `Get-ClusterResource Health` .

### <a name="handling-measurement-gaps"></a>측정 간격 처리

시간 범위에 설명 된 대로 [측정을 더](#timeframes)작은 계열로 병합 하면 누락 된 데이터 기간이 제외 됩니다. 예를 들어 서버가 30 분 동안 다운 된 후 다음 30 분 동안 50% CPU에서 실행 되는 경우 `ClusterNode.Cpu.Usage` 해당 시간의 평균은 50% (25% 아님)로 올바르게 기록 됩니다.

### <a name="extensibility-and-customization"></a>확장성 및 사용자 지정

성능 기록은 스크립팅이 간편 합니다. PowerShell을 사용 하 여 데이터베이스에서 직접 사용 가능한 모든 기록을 가져와서 자동화 된 보고 또는 경고를 작성 하 고, 보관을 위해 기록을 내보내고, 고유한 시각화를 롤아웃할 수 있습니다. 유용한 시작 코드는 게시 된 [샘플 스크립트](performance-history-scripting.md) 를 참조 하세요.

추가 개체, 기한 또는 계열에 대 한 기록을 수집할 수 없습니다.

측정 빈도와 보존 기간은 현재 구성할 수 없습니다.

## <a name="start-or-stop-performance-history"></a>성능 기록 시작 또는 중지

### <a name="how-do-i-enable-this-feature"></a>어떻게 할까요?이 기능을 사용 하도록 설정 하 시겠습니까?

사용자가 아닌 경우 `Stop-ClusterPerformanceHistory` 에는 기본적으로 성능 기록이 사용 됩니다.

다시 사용 하도록 설정 하려면 다음 PowerShell cmdlet을 관리자 권한으로 실행 합니다.

```PowerShell
Start-ClusterPerformanceHistory
```

### <a name="how-do-i-disable-this-feature"></a>어떻게 할까요?이 기능을 사용 하지 않도록 설정 하 시겠습니까?

성능 기록 수집을 중지 하려면 다음 PowerShell cmdlet을 관리자 권한으로 실행 합니다.

```PowerShell
Stop-ClusterPerformanceHistory
```

기존 측정값을 삭제 하려면 플래그를 사용 합니다 `-DeleteHistory` .

```PowerShell
Stop-ClusterPerformanceHistory -DeleteHistory
```

   > [!TIP]
   > 초기 배포 중에의 매개 변수를로 설정 하 여 성능 기록이 시작 되지 않도록 할 수 있습니다 `-CollectPerformanceHistory` `Enable-ClusterStorageSpacesDirect` `$False` .

## <a name="troubleshooting"></a>문제 해결

### <a name="the-cmdlet-doesnt-work"></a>Cmdlet이 작동 하지 않습니다.

"*' Get-ClusterPerf ' 라는 오류 메시지는 cmdlet의 이름으로 인식 되지*않습니다." 라는 오류 메시지는 해당 기능을 사용할 수 없거나 설치 되지 않았음을 의미 합니다. Windows Server Insider Preview 빌드 17692 이상, 장애 조치 (Failover) 클러스터링을 설치 했으며 스토리지 공간 다이렉트 실행 중인지 확인 합니다.

   > [!NOTE]
   > 이 기능은 Windows Server 2016 이전 버전에서는 사용할 수 없습니다.

### <a name="no-data-available"></a>데이터를 사용할 수 없습니다.

그림과 같이 "*사용할 수 있는 데이터 없음*"이 차트에 표시 되는 경우 문제를 해결 하는 방법은 다음과 같습니다.

![데이터를 사용할 수 없습니다.](media/performance-history/no-data-available.png)

1. 개체를 새로 추가 하거나 만든 경우 개체가 검색 될 때까지 기다립니다 (최대 15 분).

2. 페이지를 새로 고치거 나 다음 백그라운드 새로 고침 (최대 30 초) 동안 대기 합니다.

3. 특정 특수 개체는 성능 기록에서 제외 됩니다. 예를 들어 클러스터 되지 않은 가상 머신과 CSV (클러스터 공유 볼륨) 파일 시스템을 사용 하지 않는 볼륨이 있습니다. 자세한 인쇄를 위해 [볼륨의 성능 기록과](performance-history-for-volumes.md)같은 개체 유형에 대 한 하위 항목을 확인 합니다.

4. 문제가 지속 되 면 관리자 권한으로 PowerShell을 열고 cmdlet을 실행 `Get-ClusterPerf` 합니다. Cmdlet은 ClusterPerformanceHistory 볼륨이 없는 경우와 같은 일반적인 문제를 식별 하는 문제 해결 논리를 포함 하며 수정 지침을 제공 합니다.

5. 이전 단계에서 명령을 실행 해도 아무 것도 반환 되지 않으면 PowerShell에서를 실행 하 여 상태 관리 서비스 (성능 기록 수집)를 다시 시작 해 볼 수 있습니다 `Stop-ClusterResource Health ; Start-ClusterResource Health` .

## <a name="additional-references"></a>추가 참조

- [스토리지 공간 다이렉트 개요](storage-spaces-direct-overview.md)
