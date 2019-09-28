---
ms.assetid: f15c02d7-1cbd-4eba-a571-0ea34ab93ef4
title: 데이터 중복 제거 실행
ms.technology: storage-deduplication
ms.prod: windows-server
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 09/15/2016
ms.openlocfilehash: 86aff55b4c548ccf4fcbb04cc477dd63a889bebd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403206"
---
# <a name="running-data-deduplication"></a>데이터 중복 제거 실행

> 적용 대상: Windows Server(반기 채널), Windows Server 2016

## <a id="running-dedup-jobs-manually"></a>수동으로 데이터 중복 제거 작업 실행

다음 PowerShell cmdlet을 사용하면 예약된 모든 데이터 중복 제거 작업을 수동으로 실행할 수 있습니다.
* [`Start-DedupJob`](https://technet.microsoft.com/library/hh848442.aspx): 새 데이터 중복 제거 작업을 시작 합니다.
* [`Stop-DedupJob`](https://technet.microsoft.com/library/hh848439.aspx): 이미 진행 중인 데이터 중복 제거 작업을 중지 (또는 큐에서 제거) 합니다.
* [`Get-DedupJob`](https://technet.microsoft.com/library/hh848452.aspx): 모든 활성 및 대기 중인 데이터 중복 제거 작업을 표시 합니다.

[데이터 중복 제거 작업을 예약할 때 사용할 수 있는 설정](advanced-settings.md#modifying-job-schedules-available-settings)은 예약별 설정을 제외한 작업을 수동으로 시작할 때도 모두 사용할 수 있습니다. 예를 들어 높은 우선 순위, 최대 CPU 사용량 및 최대 메모리 사용량으로 [최적화](understand.md#job-info-optimization) 작업을 수동으로 시작하려면 관리자 권한으로 다음 PowerShell 명령을 실행합니다.

```PowerShell
Start-DedupJob -Type Optimization -Volume <Your-Volume-Here> -Memory 100 -Cores 100 -Priority High
```

## <a id="monitoring-dedup"></a>데이터 중복 제거 모니터링

### <a id="monitoring-dedup-job-successes"></a>작업 성공

데이터 중복 제거는 사후 처리 모델을 사용하므로 [데이터 중복 제거 작업](understand.md#job-info)에 성공하는 것이 중요합니다. 가장 최근 작업의 상태를 확인하는 간편한 방법은 [`Get-DedupStatus`](https://technet.microsoft.com/library/hh848437.aspx) PowerShell cmdlet을 사용하는 것입니다. 주기적으로 다음 필드를 확인합니다.

* [최적화 작업](understand.md#job-info-optimization)의 경우 `LastOptimizationResult`(0 = 성공), `LastOptimizationResultMessage` 및 `LastOptimizationTime`(최근이어야 함)
* [가비지 수집 작업](understand.md#job-info-gc)의 경우 `LastGarbageCollectionResult`(0 = 성공), `LastGarbageCollectionResultMessage` 및 `LastGarbageCollectionTime`(최근이어야 함)
* [무결성 스크러빙 작업](understand.md#job-info-scrubbing)의 경우 `LastScrubbingResult`(0 = 성공), `LastScrubbingResultMessage` 및 `LastScrubbingTime`(최근이어야 함)

> [!Note]  
> 작업 성공 및 실패에 대한 세부 정보는 Windows 이벤트 뷰어의 `\Applications and Services Logs\Windows\Deduplication\Operational`에서 확인할 수 있습니다.

### <a id="monitoring-dedup-optimization-rates"></a>최적화 속도

[최적화 작업](understand.md#job-info-optimization) 실패의 한 가지 지표는 최적화 속도의 하향 추세입니다. 하향 추세의 최적화 속도는 최적화 작업이 변경률 또는 변동률에 뒤처지고 있다는 것을 의미할 수 있습니다. [`Get-DedupStatus`  ](https://technet.microsoft.com/library/hh848437.aspx) PowerShell cmdlet을 사용하여 최적화 속도를 확인할 수 있습니다.

> [!Important]
> `Get-DedupStatus`에는 최적화 비율과 관련 된 두 개의 필드인 `OptimizedFilesSavingsRate`과 `SavingsRate`가 있습니다. 두 필드는 모두 추적에 중요한 값이지만 각각에는 고유한 의미가 있습니다.
> - `OptimizedFilesSavingsRate`은 최적화를 위해 ' 정책 내 ' 인 파일에만 적용 됩니다 (`space used by optimized files after optimization / logical size of optimized files`).
> - `SavingsRate`은 전체 볼륨 (`space used by optimized files after optimization / total logical size of the optimization`)에 적용 됩니다.

## <a id="disabling-dedup"></a>데이터 중복 제거 사용 안 함
데이터 중복 제거를 사용하지 않으려면 [최적화 해제 작업](understand.md#job-info-unoptimization)을 실행합니다. 볼륨 최적화를 실행 취소하려면 다음 명령을 실행합니다.

```PowerShell
Start-DedupJob -Type Unoptimization -Volume <Desired-Volume>
```

> [!Important]  
> 볼륨에 공간이 부족하여 최적화 해제된 데이터를 유지할 수 없는 경우 최적화 해제 작업에 실패합니다.

## <a id="faq"></a>질문과 대답
**데이터 중복 제거를 모니터링 하는 데 사용할 수 있는 System Center Operations Manager 관리 팩이 있나요?**  
예. 파일 서버용 System Center 관리 팩을 통해 데이터 중복 제거를 모니터링할 수 있습니다. 자세한 내용은 [File Server 2012 R2용 System Center 관리 팩 가이드](https://download.microsoft.com/download/6/F/7/6F7A33B9-9383-48ED-9252-23C2C8AD1BDA/MPGuide_FileServer2012R2.doc)를 참조하세요.
