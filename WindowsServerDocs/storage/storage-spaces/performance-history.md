---
title: 저장소 공간 다이렉트에 대 한 성능 기록
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/07/2018
Keywords: 저장소 공간 다이렉트
ms.localizationpriority: medium
ms.openlocfilehash: 828a3265c9770bab0158067c4f856866d03e3d42
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870864"
---
# <a name="performance-history-for-storage-spaces-direct"></a>저장소 공간 다이렉트에 대 한 성능 기록

> 적용 대상: Windows Server 2019

성능 기록은 제공 하는 새로운 기능 [저장소 공간 다이렉트](storage-spaces-direct-overview.md) 관리자 호스트 서버, 드라이브, 볼륨, 가상 컴퓨터에서 기록 계산, 메모리, 네트워크 및 저장소 측정에 쉽게 액세스할 수 있습니다. 성능 기록은 자동으로 수집 이며 최대 1 년에 대 한 클러스터에 저장 됩니다.

   > [!IMPORTANT]
   > 이 기능은 Windows Server 2019에 새로운 기능입니다. Windows Server 2016에서 사용할 수 없는 합니다.

## <a name="get-started"></a>시작

성능 기록 Windows Server 2019에서 저장소 공간 다이렉트를 사용 하 여 기본적으로 수집 됩니다. 설치, 구성 또는 모든 요소 필요가 없습니다. 인터넷 연결이 필요 없음, System Center 필수가 아닙니다. 및 외부 데이터베이스 필요 하지 않습니다.

클러스터의 성능 기록을 그래픽으로 보려면 사용 하 여 [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md):

![Windows Admin Center 성능 기록](media/performance-history/perf-history-in-wac.png)

쿼리를 프로그래밍 방식으로 처리를 사용 하 여 새 `Get-ClusterPerf` cmdlet. 참조 [PowerShell에서 사용 현황](#usage-in-powershell)합니다.

## <a name="whats-collected"></a>수집 되는 내용

성능 기록 7 형식의 개체에 대해 수집 됩니다.

![개체의 형식](media/performance-history/types-of-object.png)

각 개체 형식에 여러 계열: 예를 들어 `ClusterNode.Cpu.Usage` 각 서버에 대해 수집 됩니다.

각 개체 유형에 대해 수집 되는 내용 및 해석 하는 방법의 자세한 내용은 다음 하위이 항목을 참조 하세요.

| Object             | 시리즈                                                                               |
|--------------------|--------------------------------------------------------------------------------------|
| 드라이브             | [드라이브에 대 한 수집 되는 내용](performance-history-for-drives.md)                     |
| 네트워크 어댑터   | [네트워크 어댑터에 대해 수집 되는 내용](performance-history-for-network-adapters.md) |
| 서버            | [서버에 대 한 수집 되는 내용](performance-history-for-servers.md)                   |
| 가상 하드 디스크 | [가상 하드 디스크에 대해 수집 되는 내용](performance-history-for-vhds.md)           |
| 가상 컴퓨터   | [가상 머신에 대 한 수집 되는 내용](performance-history-for-vms.md)              |
| 볼륨            | [볼륨에 대 한 수집 되는 내용](performance-history-for-volumes.md)                   |
| Clusters           | [클러스터에 대 한 수집 되는 내용](performance-history-for-clusters.md)                 |

계열은 해당 부모 피어 개체에 걸쳐 집계: 예를 들어 `NetAdapter.Bandwidth.Inbound` 개별적으로 각 네트워크 어댑터에 대해 수집 되 고 전체 서버에 대 한 집계 마찬가지로 `ClusterNode.Cpu.Usage` 전체 클러스터;으로 집계 등입니다.

## <a name="timeframes"></a>기간

성능 기록 줄어들 세분성을 사용 하 여 최대 1 년 동안 저장 됩니다. 가장 최근 시간을 측정을 사용할 수 10 초 마다. 지능적으로 병합 이후에 (평균 또는 합계를 계산 하 여 적절 하 게) 더 많은 시간에 걸쳐 있는 덜 세분화 된 계열로 합니다. 가장 최근의 하루 측정을 사용할 수 있습니다. 5 분 마다 가장 최근의 주, 15 분입니다. 등에입니다.

Windows Admin Center 차트 위의 오른쪽 상단에서에서 기간을 선택할 수 있습니다.

![Windows Admin Center 기간](media/performance-history/timeframes-in-honolulu.png)

PowerShell을 사용 하 여는 `-TimeFrame` 매개 변수입니다.

사용 가능한 시간 범위는 다음과 같습니다.

| 기간   | 측정 빈도 | 에 대 한 보존 |
|-------------|-----------------------|--------------|
| `LastHour`  | 10 초 마다         | 1시간       |
| `LastDay`   | 5 분 마다       | 25 시간     |
| `LastWeek`  | 15 분 마다      | 8일       |
| `LastMonth` | 1 시간 마다          | 35 일      |
| `LastYear`  | 1 일           | 400 일     |

## <a name="usage-in-powershell"></a>PowerShell에서 사용

사용 하 여는 `Get-ClusterPerformanceHistory` PowerShell에서 쿼리 및 처리 성능 기록에는 cmdlet입니다.

```PowerShell
Get-ClusterPerformanceHistory
```

   > [!TIP]
   > 사용 된 **Get ClusterPerf** 일부 키 입력을 저장 하는 별칭입니다.

### <a name="example"></a>예제

가상 컴퓨터의 CPU 사용량을 가져옵니다 *MyVM* 지난 1 시간 동안:

```PowerShell
Get-VM "MyVM" | Get-ClusterPerf -VMSeriesName "VM.Cpu.Usage" -TimeFrame LastHour
```

고급 예제를 보려면 게시 된 [하는 샘플 스크립트](performance-history-scripting.md) 최고 값을 찾을, 평균 계산, 추세 선 그리기, 검색 및 더 이상 실행 시작 코드를 제공 하는 합니다.

### <a name="specify-the-object"></a>개체를 지정 합니다.

파이프라인에서 원하는 개체를 지정할 수 있습니다. 이 7 가지 유형의 개체를 사용 하 여 작동합니다.

| 파이프라인에서 개체 | 예제     |
|----------------------|-------------|
| `Get-PhysicalDisk`   | <code>Get-PhysicalDisk -SerialNumber "XYZ456" &#124; Get-ClusterPerf</code>         |
| `Get-NetAdapter`     | <code>Get-NetAdapter "Ethernet" &#124; Get-ClusterPerf</code>                       |
| `Get-ClusterNode`    | <code>Get-ClusterNode "Server123" &#124; Get-ClusterPerf</code>                     |
| `Get-VHD`            | <code>Get-VHD "C:\ClusterStorage\MyVolume\MyVHD.vhdx" &#124; Get-ClusterPerf</code> |
| `Get-VM`             | <code>Get-VM "MyVM" &#124; Get-ClusterPerf</code>                                   |
| `Get-Volume`         | <code>Get-Volume -FriendlyName "MyVolume"  &#124; Get-ClusterPerf</code>            |
| `Get-Cluster`        | <code>Get-Cluster "MyCluster" &#124; Get-ClusterPerf</code>                         |

지정 하지 않으면 전체 클러스터에 대 한 성능 기록을 반환 됩니다.

### <a name="specify-the-series"></a>되풀이 지정 합니다.

이러한 매개 변수를 사용 하 여 원하는 계열을 지정할 수 있습니다.


| 매개 변수                 | 예제                       | 목록                                                                                 |
|---------------------------|-------------------------------|--------------------------------------------------------------------------------------|
| `-PhysicalDiskSeriesName` | `"PhysicalDisk.Iops.Read"`    | [드라이브에 대 한 수집 되는 내용](performance-history-for-drives.md)                     |
| `-NetAdapterSeriesName`   | `"NetAdapter.Bandwidth.Outbound"` | [네트워크 어댑터에 대해 수집 되는 내용](performance-history-for-network-adapters.md) |
| `-ClusterNodeSeriesName`  | `"ClusterNode.Cpu.Usage"`     | [서버에 대 한 수집 되는 내용](performance-history-for-servers.md)                   |
| `-VHDSeriesName`          | `"Vhd.Size.Current"`          | [가상 하드 디스크에 대해 수집 되는 내용](performance-history-for-vhds.md)           |
| `-VMSeriesName`           | `"Vm.Memory.Assigned"`        | [가상 머신에 대 한 수집 되는 내용](performance-history-for-vms.md)              |
| `-VolumeSeriesName`       | `"Volume.Latency.Write"`      | [볼륨에 대 한 수집 되는 내용](performance-history-for-volumes.md)                   |
| `-ClusterSeriesName`      | `"PhysicalDisk.Size.Total"`   | [클러스터에 대 한 수집 되는 내용](performance-history-for-clusters.md)                 |


   > [!TIP]
   > 사용 가능한 시계열에 검색할 탭 완성 기능을 사용 합니다.

지정 하지 않으면 지정된 된 개체에 대 한 사용 가능한 모든 계열 반환 됩니다.

### <a name="specify-the-timeframe"></a>기간을 지정 합니다.

와 함께 기록의 기간을 지정할 수는 `-TimeFrame` 매개 변수입니다.

   > [!TIP]
   > 탭 완성 기능을 사용 하 여 사용할 수 있는 기간을 검색 합니다.

를 지정 하지 않으면 경우는 `MostRecent` 측정 반환 됩니다.

## <a name="how-it-works"></a>작동 방법

### <a name="performance-history-storage"></a>성능 기록 저장소

약 10 GB 볼륨을 명명 된 저장소 공간 다이렉트가 사용 하도록 설정한 후에 곧 `ClusterPerformanceHistory` 만들어집니다 Extensible Storage Engine (Microsoft JET 라고도 함)의 인스턴스는 있는 프로 비전 됩니다. 이 간단한 데이터베이스 관리자의 개입 또는 관리 없이 성능 기록을 저장합니다.

![성능 기록 저장소에 대 한 볼륨](media/performance-history/perf-history-volume.png)

볼륨은 저장소 공간에서 지원 하 고 간단 하 고 양방향 미러 또는 클러스터의 노드 수에 따라 3 방향 미러 복원 력을 사용 합니다. 와 같이 저장소 공간 다이렉트의 다른 모든 볼륨 드라이브 또는 서버 오류 후 복구 하는 것.

볼륨은 ReFS를 사용 하 여 있지만 클러스터 그룹 소유자 노드에서 표시 되도록 클러스터 공유 볼륨 (CSV) 아닙니다. 자동으로 만들어지는 것 외에이 볼륨에 대 한 특별: 표시, 찾아봅니다, 크기를 변경 하거나 (권장 하지 않음) 삭제할 수 있습니다. 문제가 있는 경우, 참조 [문제 해결](#troubleshooting)합니다. 

### <a name="object-discovery-and-data-collection"></a>개체 검색 및 데이터 수집

성능 기록은 자동으로 클러스터의 아무 곳 이나 가상 머신과 같은 관련 개체를 검색 하 고 해당 성능 카운터를 스트리밍하기 시작 합니다. 카운터를 집계 하 고 동기화 하 고 데이터베이스에 삽입 됩니다. 스트리밍 지속적으로 실행 하 고 최소한의 시스템에 미치는 영향에 대해 최적화 됩니다.

컬렉션은 항상 사용할 수 있는 상태 서비스에서 처리 됩니다: 실행 되 고 있는 노드에 다운 되 면 다시 시작 됩니다 잠시 후 클러스터에서 나중에 다른 노드. 성능 기록 요약 하자면, 경과 될 수 있습니다 하지만 자동으로 다시 시작 됩니다. 실행 하 여 상태 관리 서비스 및 해당 소유자 노드를 볼 수 있습니다 `Get-ClusterResource Health` PowerShell에서.

### <a name="handling-measurement-gaps"></a>측정 차이 처리합니다.

측정에 설명 된 대로 더 많은 시간에 걸쳐 있는 덜 세분화 된 계열로 병합 되는 경우 [기간](#Timeframes), 누락 된 데이터의 마침표는 제외 됩니다. 예를 들어, 서버를 아래로 30 분에 대 한 경우 다음 실행 50 %CPU 다음 30 분간의 `ClusterNode.Cpu.Usage` 시간 50% (없습니다 25%)으로 올바르게 기록 됩니다에 대 한 평균입니다.

### <a name="extensibility-and-customization"></a>확장성 및 사용자 지정

성능 기록 스크립팅이 쉬운 경우 PowerShell을 사용 하 여 빌드 자동화 된 보고 또는 경고 내보내기 기록을 보관을 위해 데이터베이스에서 직접 사용할 수 있는 모든 기록 끌어오기를 사용자 고유의 시각화 등을 롤링 합니다. 게시 된 참조 [하는 샘플 스크립트](performance-history-scripting.md) 유용한 시작 코드에 대 한 합니다.

추가 개체, 기간 또는 계열에 대 한 기록을 수집 하는 것이 불가능 합니다.

측정 빈도 및 보존 기간은 현재 구성할 수 없습니다.

## <a name="start-or-stop-performance-history"></a>시작 또는 중지 성능 기록

### <a name="how-do-i-enable-this-feature"></a>이 기능을 어떻게 사용 하나요?

경우가 아니면 있습니다 `Stop-ClusterPerformanceHistory`, 성능 기록을 기본적으로 사용 됩니다.

다시 사용 하려면 관리자 권한으로 PowerShell cmdlet을 실행 합니다.

```PowerShell
Start-ClusterPerformanceHistory
```

### <a name="how-do-i-disable-this-feature"></a>이 기능을 비활성화 하려면 어떻게 하나요?

성능 기록을 수집을 중지 하려면 관리자 권한으로 PowerShell cmdlet을 실행 합니다.

```PowerShell
Stop-ClusterPerformanceHistory
```

기존 측정값을 삭제 하려면 사용 된 `-DeleteHistory` 플래그:

```PowerShell
Stop-ClusterPerformanceHistory -DeleteHistory
```

   > [!TIP]
   > 초기 배포 하는 동안 성능 기록을 설정 하 여 시작 방지할 수 있습니다 합니다 `-CollectPerformanceHistory` 의 매개 변수 `Enable-ClusterStorageSpacesDirect` 에 `$False`입니다.

## <a name="troubleshooting"></a>문제 해결

### <a name="the-cmdlet-doesnt-work"></a>Cmdlet이 작동 하지 않습니다.

오류 메시지와 같은 "*' Get-ClusterPerf' 용어는 cmdlet의 이름으로 인식 되지 않습니다*" 기능을 사용할 수 없거나 설치 된 것을 의미 합니다. Windows Server Insider Preview 빌드 17692 이상 있는지, 장애 조치 클러스터링 및 저장소 공간 다이렉트 실행 중인지를 설치 했는지 확인 합니다.

   > [!NOTE]
   > 이 기능은 Windows Server 2016에서 사용할 수 있거나 이전있지 않습니다.

### <a name="no-data-available"></a>사용 가능한 데이터 없음 

차트에 표시 되 면 "*사용 가능한 데이터 없음*" 같이, 문제 해결 방법 다음은:

![사용 가능한 데이터 없음](media/performance-history/no-data-available.png)

1. 개체를 새로 추가, 생성 하는 경우 되도록 대기 (최대 15 분)을 검색 합니다.

2. 페이지 새로 고침 또는 다음 백그라운드 새로 고침 (최대 30 초) 될 때까지 기다립니다.

3. 특정 특수 개체 성능 기록 – 예를 들어, 클러스터 아닌 가상 컴퓨터 및 클러스터 공유 볼륨 (CSV) 파일 시스템을 사용 하지 않는 볼륨에서에서 제외 됩니다. 같은 개체 형식에 대 한 하위 항목을 확인 [볼륨에 대 한 성능 기록을](performance-history-for-volumes.md)를 인쇄에 대 한 합니다.

4. 문제가 지속 되 면 실행 관리자 권한으로 PowerShell을 엽니다는 `Get-ClusterPerf` cmdlet. Cmdlet에서는 해결 하는 일반적인 문제를 식별 하는 논리 처럼 ClusterPerformanceHistory 볼륨 없으면 및 업데이트 관리 지침을 제공 합니다.

5. 이전 단계에서 명령을 nothing을 반환 하는 경우 다시 시작 상태 서비스 (성능 기록을 수집)를 실행 하 여 `Stop-ClusterResource Health ; Start-ClusterResource Health` PowerShell에서.

## <a name="see-also"></a>참조

- [저장소 공간 다이렉트 개요](storage-spaces-direct-overview.md)
