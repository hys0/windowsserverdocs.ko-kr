---
title: 저장소 공간 다이렉트에 대 한 성능 기록
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/07/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: 828a3265c9770bab0158067c4f856866d03e3d42
ms.sourcegitcommit: d31e266130b3b082372f7af4024e6089cb347d74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2018
ms.locfileid: "4239260"
---
# 저장소 공간 다이렉트에 대 한 성능 기록

> 적용 대상: Windows Server 2019

성능 기록에 권한을 부여 하는 [저장소 공간 다이렉트](storage-spaces-direct-overview.md) 관리자가 쉽게 액세스할 수 있도록 기록 컴퓨팅, 메모리, 네트워크 및 저장소 측정 호스트 서버, 드라이브, 볼륨, 가상 컴퓨터 등 걸쳐 새로운 기능입니다. 성능 기록 자동으로 수집 되 고 최대 1 년 동안 클러스터에 저장 됩니다.

   > [!IMPORTANT]
   > 이 기능은 Windows Server 2019의 새로운 기능입니다. Windows Server 2016에서 사용할 수는 없습니다.

## 시작

Windows Server 2019의 저장소 공간 다이렉트를 사용 하 여 기본적으로 성능 기록을 수집 됩니다. 설치, 구성 또는 마음껏 필요가 없습니다. 인터넷 연결이 필요 하지 않습니다., System Center 필요 하지 않습니다. 및 외부 데이터베이스 필요 하지 않습니다.

클러스터의 성과 보려면 기록 그래픽으로 [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md)를 사용 합니다.

![Windows Admin Center에서 성능 기록](media/performance-history/perf-history-in-wac.png)

쿼리하고 프로그래밍 방식으로 처리를 사용 하 여 새 `Get-ClusterPerf` cmdlet입니다. [PowerShell에서 사용량](#usage-in-powershell)을 참조 하세요.

## 수집 된 기능

7 유형의 개체에 대 한 성능 기록을 수집 됩니다.

![유형의 개체](media/performance-history/types-of-object.png)

각 개체 형식에 많은 시리즈: 예를 들어 `ClusterNode.Cpu.Usage` 는 각 서버에 대해 수집 합니다.

각 개체 유형에 대해 수집 되는 기능 및 해석 하는 방법의 세부 정보, 다음 하위이 항목을 참조 하세요.

| 개체             | 시리즈                                                                               |
|--------------------|--------------------------------------------------------------------------------------|
| 드라이브             | [드라이브 수집 하는 기능](performance-history-for-drives.md)                     |
| 네트워크 어댑터   | [네트워크 어댑터에 대해 수집 된 기능](performance-history-for-network-adapters.md) |
| 서버            | [서버에 대 한 수집 되는 기능](performance-history-for-servers.md)                   |
| 가상 하드 디스크 | [가상 하드 디스크 수집 하는 기능](performance-history-for-vhds.md)           |
| 가상 컴퓨터   | [가상 컴퓨터에 수집 된 기능](performance-history-for-vms.md)              |
| 볼륨            | [볼륨에 대 한 수집 되는 기능](performance-history-for-volumes.md)                   |
| 클러스터           | [클러스터를 위한 수집 되는 기능](performance-history-for-clusters.md)                 |

많은 시리즈 피어 개체를 해당 부모에서 집계 됩니다: 예를 들어 `NetAdapter.Bandwidth.Inbound` 개별적으로 각 네트워크 어댑터에 대 한 수집 되어 전체 서버로 집계 된 마찬가지로 `ClusterNode.Cpu.Usage` 전체 클러스터; 집계 합니다.

## 기간

성능 기록 최대 1 년 동안 줄어들 세분성으로 저장 됩니다. 가장 최근 시간에 대 한 측정값은 사용할 수 있는 10 초 마다입니다. 지능적으로 병합 부터는 (평균 또는 가산, 필요에 따라) 더 많은 시간에 걸쳐 있는 덜 세분화 된 시리즈입니다. 가장 최근 날짜에 대 한 측정값은 사용할 수 있는 5 분 마다; 최근 주의; 15 분 마다 합니다.

Windows Admin Center에서 차트 위 오른쪽 위에서에서 기간을 선택할 수 있습니다.

![Windows Admin Center의 기간](media/performance-history/timeframes-in-honolulu.png)

PowerShell을 사용 하는 `-TimeFrame` 매개 변수입니다.

다음은 사용 가능한 기간이입니다.

| 기간   | 측정 빈도 | 에 대 한 유지 됩니다. |
|-------------|-----------------------|--------------|
| `LastHour`  | 10 초 마다         | 1시간       |
| `LastDay`   | 5 분 마다       | 25 시간     |
| `LastWeek`  | 15 분 마다      | 8 일       |
| `LastMonth` | 1 시간 마다          | 35 일      |
| `LastYear`  | 1 일 마다           | 400 일     |

## Powershell 사용

사용 하는 `Get-ClusterPerformanceHistory` PowerShell의 성능 기록 쿼리 및 프로세스에 cmdlet입니다.

```PowerShell
Get-ClusterPerformanceHistory
```

   > [!TIP]
   > 일부 키 입력을 저장 하려면 **Get ClusterPerf** 별칭을 사용 합니다.

### 예

마지막 시간에 대 한 *MyVM* 가상 컴퓨터의 CPU 사용량을 가져옵니다.

```PowerShell
Get-VM "MyVM" | Get-ClusterPerf -VMSeriesName "VM.Cpu.Usage" -TimeFrame LastHour
```

고급 예제 최대 값을 찾으려면, 평균을 계산 추세 선을 그릴, 검색 등에 outlier 실행 시작 코드를 제공 하는 게시 된 [샘플 스크립트](performance-history-scripting.md) 를 참조 하세요.

### 개체를 지정 합니다.

파이프라인에 의해 개체를 지정할 수 있습니다. 이 7 유형의 개체에서 작동합니다.

| 파이프라인에서 개체 | 예     |
|----------------------|-------------|
| `Get-PhysicalDisk`   | <code>Get-PhysicalDisk -SerialNumber "XYZ456" &#124; Get-ClusterPerf</code>         |
| `Get-NetAdapter`     | <code>Get-NetAdapter "Ethernet" &#124; Get-ClusterPerf</code>                       |
| `Get-ClusterNode`    | <code>Get-ClusterNode "Server123" &#124; Get-ClusterPerf</code>                     |
| `Get-VHD`            | <code>Get-VHD "C:\ClusterStorage\MyVolume\MyVHD.vhdx" &#124; Get-ClusterPerf</code> |
| `Get-VM`             | <code>Get-VM "MyVM" &#124; Get-ClusterPerf</code>                                   |
| `Get-Volume`         | <code>Get-Volume -FriendlyName "MyVolume"  &#124; Get-ClusterPerf</code>            |
| `Get-Cluster`        | <code>Get-Cluster "MyCluster" &#124; Get-ClusterPerf</code>                         |

지정 하지 않으면 전체 클러스터에 대 한 성능 기록을 반환 됩니다.

### 시리즈를 지정 합니다.

이러한 매개 변수를 사용 하 여 원하는 시리즈를 지정할 수 있습니다.


| 매개 변수                 | 예                       | List                                                                                 |
|---------------------------|-------------------------------|--------------------------------------------------------------------------------------|
| `-PhysicalDiskSeriesName` | `"PhysicalDisk.Iops.Read"`    | [드라이브 수집 하는 기능](performance-history-for-drives.md)                     |
| `-NetAdapterSeriesName`   | `"NetAdapter.Bandwidth.Outbound"` | [네트워크 어댑터에 대해 수집 된 기능](performance-history-for-network-adapters.md) |
| `-ClusterNodeSeriesName`  | `"ClusterNode.Cpu.Usage"`     | [서버에 대 한 수집 되는 기능](performance-history-for-servers.md)                   |
| `-VHDSeriesName`          | `"Vhd.Size.Current"`          | [가상 하드 디스크 수집 하는 기능](performance-history-for-vhds.md)           |
| `-VMSeriesName`           | `"Vm.Memory.Assigned"`        | [가상 컴퓨터에 수집 된 기능](performance-history-for-vms.md)              |
| `-VolumeSeriesName`       | `"Volume.Latency.Write"`      | [볼륨에 대 한 수집 되는 기능](performance-history-for-volumes.md)                   |
| `-ClusterSeriesName`      | `"PhysicalDisk.Size.Total"`   | [클러스터를 위한 수집 되는 기능](performance-history-for-clusters.md)                 |


   > [!TIP]
   > 탭 완성 사용 가능한 시리즈를 검색 하는 데 사용 합니다.

지정 하지 않으면 지정된 된 개체에 사용할 수 있는 모든 시리즈 반환 됩니다.

### 시간대를 지정 합니다.

사용 하 여 원하는 기록 시간 범위를 지정할 수는 `-TimeFrame` 매개 변수입니다.

   > [!TIP]
   > 탭 완성 사용 가능한 기간을 검색 하는 데 사용 합니다.

지정 하지 않으면는 `MostRecent` 측정 반환 됩니다.

## 작동 방식

### 기록 저장소 성능

약 10 GB 볼륨 라는 저장소 공간 다이렉트를 사용 하면 직후 `ClusterPerformanceHistory` 생성 되 고 확장 가능한 저장소 엔진 (Microsoft JET 라고도 함)의 인스턴스는 프로 비전 있습니다. 이 경량 데이터베이스 관리 나 관리자 개입 없이 성능 기록이 저장합니다.

![기록 저장소 성능에 대 한 볼륨](media/performance-history/perf-history-volume.png)

저장소 공간에 의해 지원 받지는 간단 하 고 양방향 미러 또는 클러스터에서 노드의 수에 따라 3 방향 미러 복원은 중 하나를 사용 하는 볼륨 합니다. 드라이브 또는 서버 오류와 마찬가지로 저장소 공간 다이렉트에서 다른 볼륨 후를 복구 하는 것입니다.

볼륨은 ReFS를 사용 하지만 되지 않으므로 클러스터 공유 볼륨 (CSV) 클러스터 그룹 소유자 노드에서 표시 됩니다. 외에도 자동으로 생성 되는 특별이 볼륨에 대 한: 표시에서 찾아볼, 크기를 변경 하거나 (권장 하지 않음) 삭제할 수 있습니다. 문제가 발생할 경우 [문제 해결](#troubleshooting)을 참조 합니다. 

### 개체 검색 및 데이터 수집

자동으로 성능 기록 클러스터의 아무 곳 이나 가상 컴퓨터와 같은 관련 개체를 검색 하 고 성능 카운터가 스트리밍 시작 됩니다. 카운터 집계, 동기화 및 데이터베이스에 삽입 합니다. 스트리밍 지속적으로 실행 되며 최소한의 시스템에 미치는 영향에 대 한 최적화 되어 있습니다.

높은 사용할 수 있는 상태 관리 서비스에서 처리 하는 컬렉션: 실행 되 고 있는 노드를 이동 하면 다시 시작할 순간 클러스터에서 나중에 다른 노드로 합니다. 성능 기록을 간략하게, 경과할 수 있지만 자동으로 다시 시작 됩니다. 상태 관리 서비스 및 해당 소유자 노드에서 실행 하 여 볼 수 있습니다 `Get-ClusterResource Health` PowerShell에서.

### 측정 간격이 처리

측정 [기간](#Timeframes)에 설명 된 대로 더 많은 시간에 걸쳐 있는 덜 세밀 하 게 시리즈 병합 되어, 손실 된 데이터 기간 제외 됩니다. 예를 들어 서버가 30 분 동안 눌렀는지 하는 경우 다음 50 %CPU 위해 실행 다음 30 분의 `ClusterNode.Cpu.Usage` 시간 50% (하지 25%)로 올바르게 기록 될에 대 한 평균 합니다.

### 확장성 및 사용자 지정

성능 기록 스크립팅 친화적인입니다. PowerShell을 사용 하 여 고유한 시각화 등 롤, 데이터베이스 보고 자동화 된 빌드를 안전 하 게 보관 기록 내보내기 경고에서 직접 사용할 수 있는 모든 기록 가져오기. 유용한 시작 코드에 대 한 게시 된 [샘플 스크립트](performance-history-scripting.md) 를 참조 하세요.

추가 개체, 기간, 또는 시리즈에 대 한 기록을 수집 하는 것이 불가능 합니다.

측정 빈도 및 보존 기간은 현재 구성할 수 있습니다.

## 시작 또는 성능 기록 중지

### 이 기능을 사용 하는 방법

하지 않는 한 하면 `Stop-ClusterPerformanceHistory`, 성능 기록 기본적으로 사용 됩니다.

것을 다시 활성화 하려면 관리자 권한으로이 PowerShell cmdlet을 실행 합니다.

```PowerShell
Start-ClusterPerformanceHistory
```

### 이 기능을 비활성화 하려면 어떻게 하나요?

성능 기록을 수집을 중지 하려면 관리자 권한으로이 PowerShell cmdlet을 실행 합니다.

```PowerShell
Stop-ClusterPerformanceHistory
```

기존 측정 값을 삭제 하려면 사용은 `-DeleteHistory` 플래그:

```PowerShell
Stop-ClusterPerformanceHistory -DeleteHistory
```

   > [!TIP]
   > 초기 배포 중 설정 하 여 시작 성능을 기록 방지할 수는 `-CollectPerformanceHistory` 매개 변수 `Enable-ClusterStorageSpacesDirect` 를 `$False`합니다.

## 문제 해결

### Cmdlet은 작동 하지 않는 경우

오류 메시지 "*라는 용어는 cmdlet의 이름으로 ' Get-ClusterPerf' 인식 되지 않습니다*" 의미 기능 처럼 사용할 수 없거나 설치 합니다. Windows Server Insider Preview 빌드 17692 이상 있다고, 장애 조치 클러스터링 및는 저장소 공간 다이렉트 실행 중인 설치 했는지 확인 합니다.

   > [!NOTE]
   > 이 기능은 Windows Server 2016에서 사용할 수 있거나 이전있지 않습니다.

### 데이터를 사용할 수 없음 

그림과 같이 "*데이터를 사용할 수 없음*"를 표시 하는 차트를 하는 경우 문제를 해결 하는 방법은 다음과 같습니다.

![데이터를 사용할 수 없음](media/performance-history/no-data-available.png)

1. 개체가 새로 추가 되거나 생성 된, 대기 상태가 되도록 (최대 15 분)을 검색 합니다.

2. 페이지 새로 고침 또는 다음 백그라운드 새로 고침 (최대 30 초) 기다립니다.

3. 일부 특수 개체 성능 기록-예: 클러스터 되지 않는 경우 가상 컴퓨터 및 클러스터 공유 볼륨 (CSV) 파일 시스템을 사용 하지 않는 볼륨에서에서 제외 됩니다. 세부 항목에 대 한 [볼륨에 대 한 성능 기록](performance-history-for-volumes.md), 같은 개체 유형으로 하위 항목을 확인 합니다.

4. 문제가 계속 되 면 관리자 권한으로 실행 PowerShell을 열고 합니다 `Get-ClusterPerf` cmdlet입니다. Cmdlet을 해결 하는 일반적인 문제를 식별 하는 논리를 제공 여부 등 ClusterPerformanceHistory 볼륨 없으면 및 문제 해결 지침을 제공 합니다.

5. 이전 단계에서 명령이 아무것도 반환 하는 경우 다시 시작 (수집 하는 성능 기록) 상태 관리 서비스를 실행 하 여 `Stop-ClusterResource Health ; Start-ClusterResource Health` PowerShell에서.

## 참고 항목

- [저장소 공간 다이렉트 개요](storage-spaces-direct-overview.md)
