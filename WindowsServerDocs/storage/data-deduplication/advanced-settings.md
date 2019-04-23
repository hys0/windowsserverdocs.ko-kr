---
ms.assetid: 01c8cece-66ce-4a83-a81e-aa6cc98e51fc
title: 고급 데이터 중복 제거 설정
ms.prod: windows-server-threshold
ms.technology: storage-deduplication
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 09/15/2016
ms.openlocfilehash: 15cfc054810a2cab85aae9a04d6195c3ae6fe0b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861214"
---
# <a name="advanced-data-deduplication-settings"></a>고급 데이터 중복 제거 설정

> 적용 대상: Windows Server(반기 채널), Windows Server 2016

이 문서에서는 고급 [데이터 중복 제거](overview.md) 설정을 수정하는 방법을 설명합니다. [권장 워크로드](install-enable.md#enable-dedup-candidate-workloads)의 경우 기본 설정으로 충분합니다. 이러한 설정을 수정하는 주된 이유는 다른 종류의 워크로드에서 데이터 중복 제거의 성능을 개선하기 위한 것입니다.

## <a id="modifying-job-schedules"></a>데이터 중복 제거 작업 일정 수정
[기본 데이터 중복 제거 작업 일정](understand.md#job-info)은 권장 워크로드에 적합하고 가능한 비주입식으로 설계되었습니다([**백업** 사용 유형](understand.md#usage-type-backup)에 사용되는 *우선 순위 최적화* 작업 제외). 워크로드에 대규모 리소스가 필요한 경우 유휴 시간 중에만 작업을 실행하거나 데이터 중복 제거 작업에서 사용할 수 있는 시스템 리소스의 양을 감소 또는 증가시킬 수 있습니다.

### <a id="modifying-job-schedules-change-schedule"></a>데이터 중복 제거 일정 변경
데이터 중복 제거 작업은 Windows 작업 스케줄러를 통해 예약되며 Microsoft\Windows\Deduplication 경로 아래에서 보고 편집할 수 있습니다. 데이터 중복 제거에는 예약을 도와주는 여러 cmdlet이 포함되어 있습니다.
* [`Get-DedupSchedule`](https://technet.microsoft.com/library/hh848446.aspx) 현재 예약 된 작업을 보여 줍니다.
* [`New-DedupSchedule`](https://technet.microsoft.com/library/hh848445.aspx) 새 예약 된 작업을 만듭니다.
* [`Set-DedupSchedule`](https://technet.microsoft.com/library/hh848447.aspx) 기존 예약 된 작업을 수정합니다.
* [`Remove-DedupSchedule`](https://technet.microsoft.com/library/hh848451.aspx) 예약된 된 작업을 제거합니다.

데이터 중복 제거 작업을 실행하는 시점을 변경하는 가장 주된 이유는 유휴 시간에 실행하기 위한 것입니다. 다음 단계별 예에서는 *주간* 시나리오(하이퍼 수렴형 Hyper-V 호스트가 평일 오후 7시 이후와 주말에는 유휴 상태임)에 대한 데이터 중복 제거 일정을 수정하는 방법을 보여 줍니다. 일정을 변경하려면 관리자 컨텍스트에서 다음 PowerShell cmdlet을 실행합니다.

1. 예약된 매시간 [최적화](understand.md#job-info-optimization) 작업을 사용하지 않도록 설정합니다.  
    ```PowerShell
    Set-DedupSchedule -Name BackgroundOptimization -Enabled $false
    Set-DedupSchedule -Name PriorityOptimization -Enabled $false
    ```

2. 현재 예약된 [가비지 수집](understand.md#job-info-gc) 및 [무결성 스크러빙](understand.md#job-info-scrubbing) 작업을 제거합니다.
    ```PowerShell
    Get-DedupSchedule -Type GarbageCollection | ForEach-Object { Remove-DedupSchedule -InputObject $_ }
    Get-DedupSchedule -Type Scrubbing | ForEach-Object { Remove-DedupSchedule -InputObject $_ }
    ```

3. 시스템에서 사용 가능한 우선 순위가 높은 모든 CPU 및 메모리에 대해 오후 7시에 실행되는 야간 최적화 작업을 만듭니다.
    ```PowerShell
    New-DedupSchedule -Name "NightlyOptimization" -Type Optimization -DurationHours 11 -Memory 100 -Cores 100 -Priority High -Days @(1,2,3,4,5) -Start (Get-Date "2016-08-08 19:00:00")
    ```

    >[!NOTE]  
    > `-Start`에 제공된 `System.Datetime`의 *date* 부분은 과거인 경우 상관없지만 *time* 부분은 작업이 시작되는 시점을 지정합니다.
4. 시스템에서 사용 가능한 우선 순위가 높은 모든 CPU 및 메모리에 대해 토요일 오전 7시부터 실행되는 주간 가비지 수집 작업을 만듭니다.
    ```PowerShell
    New-DedupSchedule -Name "WeeklyGarbageCollection" -Type GarbageCollection -DurationHours 23 -Memory 100 -Cores 100 -Priority High -Days @(6) -Start (Get-Date "2016-08-13 07:00:00")
    ```

5. 시스템에서 사용 가능한 우선 순위가 높은 모든 CPU 및 메모리에 대해 일요일 오전 7시부터 실행되는 주간 무결성 스크러빙 작업을 만듭니다.
    ```PowerShell
    New-DedupSchedule -Name "WeeklyIntegrityScrubbing" -Type Scrubbing -DurationHours 23 -Memory 100 -Cores 100 -Priority High -Days @(0) -Start (Get-Date "2016-08-14 07:00:00")
    ```

### <a id="modifying-job-schedules-available-settings"></a>사용 가능한 작업 수준 설정
신규 또는 예약된 데이터 중복 제거 작업에 대해 다음 설정을 전환할 수 있습니다.

<table>
    <thead>
        <tr>
            <th style="min-width:125px">매개 변수 이름</th>
            <th>정의</th>
            <th>사용 가능한 값</th>
            <th>이 값을 설정하는 이유</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>형식</td>
            <td>예약해야 하는 작업 유형</td>
            <td>
                <ul>
                    <li>Optimization</li>
                    <li>GarbageCollection</li>
                    <li>스크러빙</li>
                </ul>
            </td>
            <td>이 값은 예약해야 하는 작업 유형이기 때문에 필요합니다. 작업을 예약한 후에는 이 값을 변경할 수 없습니다.</td>
        </tr>
        <tr>
            <td>우선 순위</td>
            <td>예약된 작업의 시스템 우선 순위</td>
            <td>
                <ul>
                    <li>높음</li>
                    <li>중간</li>
                    <li>낮음</li>
                </ul>
            </td>
            <td>이 값은 시스템에서 CPU 시간을 할당하는 방법을 결정하도록 도와줍니다. *High*는 사용하는 CPU 시간이 많고 *low*는 적습니다.</td>
        </tr>
        <tr>
            <td>요일</td>
            <td>작업이 예약된 요일</td>
            <td>요일을 나타내는 정수 0~6의 배열:<ul>
                <li>0 = 일요일</li>
                <li>1 = 월요일</li>
                <li>2 = 화요일</li>
                <li>3 = 수요일</li>
                <li>4 = 목요일</li>
                <li>5 = 금요일</li>
                <li>6 = 토요일</li>
            </ul></td>
            <td>하루에 한 번 이상 실행해야 하는 예약된 작업</td>
        </tr>
        <tr>
            <td>Cores</td>
            <td>작업에서 사용해야 하는 시스템의 코어 비율</td>
            <td>정수 0~100(백분율을 나타냄)</td>
            <td>작업이 시스템의 계산 리소스에 미치는 영향력 제어</td>
        </tr>
        <tr>
            <td>DurationHours</td>
            <td>작업을 실행해야 하는 최대 시간</td>
            <td>양의 정수</td>
            <td>워크로드의 비유휴 시간에 작업이 실행되는 것을 방지</td>
        </tr>
        <tr>
            <td>Enabled</td>
            <td>작업의 실행 여부</td>
            <td>True/false</td>
            <td>작업을 제거하지 않고 사용하지 않도록 설정</td>
        </tr>
        <tr>
            <td>전체</td>
            <td>전체 가비지 수집 작업 예약</td>
            <td>스위치(true/false)</td>
            <td>기본적으로 모든 네 번째 작업이 전체 가비지 수집 작업입니다. 이 스위치를 사용하여 더 자주 실행되도록 전체 가비지 수집을 예약할 수 있습니다.</td>
        </tr>
        <tr>
            <td>InputOutputThrottle</td>
            <td>작업에 적용된 입/출력 스로틀 양 지정</td>
            <td>정수 0~100(백분율을 나타냄)</td>
            <td>스로틀은 작업이 다른 I/O 집약적 프로세스를 간섭하지 않도록 합니다.</td>
        </tr>
        <tr>
            <td>메모리</td>
            <td>작업에서 사용해야 하는 시스템의 메모리 비율</td>
            <td>정수 0~100(백분율을 나타냄)</td>
            <td>작업이 시스템의 메모리 리소스에 미치는 영향력 제어</td>
        </tr>
        <tr>
            <td>이름</td>
            <td>예약된 작업의 이름</td>
            <td>문자열</td>
            <td>작업에는 고유하게 식별 가능한 이름이 있어야 합니다.</td>
        </tr>
        <tr>
            <td>읽기 전용</td>
            <td>스크러빙 작업이 진행 중임을 나타내고 발견된 손상을 보고하지만 복구 작업을 실행하지는 않습니다.</td>
            <td>스위치(true/false)</td>
            <td>디스크의 불량 섹션에 있는 파일을 수동으로 복원할 수 있습니다.</td>
        </tr>
        <tr>
            <td>시작</td>
            <td>작업을 시작해야 하는 시간을 지정합니다.</td>
            <td>`System.DateTime`</td>
            <td>*Start*에 제공된 `System.Datetime`의 *date* 부분은 과거인 경우 상관없지만 *time* 부분은 작업이 시작되는 시점을 지정합니다.</td>
        </tr>
        <tr>
            <td>StopWhenSystemBusy</td>
            <td>시스템이 사용 중인 경우 데이터 중복 제거를 중지할지 여부를 지정합니다.</td>
            <td>스위치(True/False)</td>
            <td>이 스위치를 사용하여 데이터 중복 제거 동작을 제어할 수 있습니다. 이는 워크로드가 유휴 상태가 아닌 동안 데이터 중복 제거를 실행하려는 경우에 특히 중요합니다.</td>
        </tr>
    </tbody>
</table>

## <a id="modifying-volume-settings"></a>데이터 중복 제거 볼륨 수준 설정 수정
### <a id="modifying-volume-settings-how-to-toggle"></a>볼륨 설정 전환
볼륨에 대한 중복 제거를 사용하도록 설정할 때 선택하는 [사용 유형](understand.md#usage-type)을 통해 데이터 중복 제거에 대한 볼륨 수준의 기본 설정을 지정할 수 있습니다. 데이터 중복 제거에는 볼륨 수준 설정을 쉽게 편집할 수 있는 cmdlet이 포함되어 있습니다.

* [`Get-DedupVolume`](https://technet.microsoft.com/library/hh848448.aspx)
* [`Set-DedupVolume`](https://technet.microsoft.com/library/hh848438.aspx)

선택한 사용 유형에서 볼륨 설정을 수정하는 주된 이유는 특정 파일(예: 멀티미디어 또는 이미 압축된 다른 파일 형식)에 대한 읽기 성능을 개선하거나 특정 워크로드의 최적화 향상을 위해 데이터 중복 제거를 미세 조정하기 위한 것입니다. 다음 예에서는 일반용 파일 서버 워크로드와 매우 유사하지만 자주 변경되는 대용량 파일을 사용하는 워크로드에 대한 데이터 중복 제거 볼륨 설정을 수정하는 방법을 보여 줍니다.

1. 클러스터 공유 볼륨 1에 대한 현재 볼륨 설정을 확인합니다.
    ```PowerShell
    Get-DedupVolume -Volume C:\ClusterStorage\Volume1 | Select *
    ```

2. MinimumFileAge 정책이 전체 파일 대신 파일의 섹션에 적용되도록 클러스터 공유 볼륨 1에서 OptimizePartialFiles를 사용하도록 설정합니다. 이렇게 하면 파일의 섹션이 정기적으로 변경되는 경우에도 파일의 대부분이 최적화됩니다.
    ```PowerShell
    Set-DedupVolume -Volume C:\ClusterStorage\Volume1 -OptimizePartialFiles
    ```

### <a id="modifying-volume-settings-available-settings"></a>사용 가능한 볼륨 수준 설정
<table>
    <thead>
        <tr>
            <th style="min-width:125px">설정 이름</th>
            <th>정의</th>
            <th>사용 가능한 값</th>
            <th>이 값을 수정하는 이유</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>ChunkRedundancyThreshold</td>
            <td>청크가 청크 저장소의 핫스폿 섹션으로 복제되기 전에 청크가 참조되는 횟수입니다. 핫스폿 섹션의 값은 액세스 시간을 개선하기 위해 여러 액세스 경로가 있는 "핫" 청크입니다.</td>
            <td>양의 정수</td>
            <td>이 수치를 수정하는 주된 이유는 중복도가 높은 볼륨의 공간 절약률을 늘리기 위한 것입니다. 일반적으로 기본값(100)이 권장되는 설정이며 이 값을 수정할 필요가 없습니다.</td>
        </tr>
        <tr>
            <td>ExcludeFileType</td>
            <td>최적화에서 제외되는 파일 형식</td>
            <td>파일 확장명의 배열</td>
            <td>일부 파일 형식, 특히 멀티미디어 또는 이미 압축된 파일은 최적화 효과가 거의 없습니다. 이 설정을 사용하여 제외되는 형식을 구성할 수 있습니다.</td>
        </tr>
        <tr>
            <td>ExcludeFolder</td>
            <td>최적화 대상으로 간주되지 않는 폴더 경로를 지정합니다.</td>
            <td>폴더 경로의 배열</td>
            <td>성능을 개선하거나 특정 경로의 콘텐츠를 최적화에서 제외하려는 경우 볼륨의 특정 경로를 최적화 고려 대상에서 제외할 수 있습니다.</td>
        </tr>
        <tr>
            <td>InputOutputScale</td>
            <td>사후 처리 작업 중 볼륨에서 사용할 데이터 중복 제거에 대한 IO 병렬화(IO 큐) 수준을 지정합니다.</td>
            <td>1~36의 양의 정수</td>
            <td>이 값을 수정하는 주된 이유는 볼륨에서 데이터 중복 제거에 사용할 수 있는 IO 큐 수를 제한하여 높은 IO 워크로드의 성능에 미치는 영향을 줄이기 위한 것입니다. 이 설정을 기본값에서 수정하면 데이터 중복 제거의 사후 처리 작업이 느리게 실행될 수 있습니다.</td>
        </tr>
        <tr>
            <td>MinimumFileAgeDays</td>
            <td>파일이 만들어진 후 최적화에 대한 정책 내에 속하는 것으로 간주되기 전까지의 날짜 수입니다.</td>
            <td>양의 정수(0 포함)</td>
            <td>**기본** 및 **HyperV** 사용 유형은 자주 사용되거나 최근에 만들어진 파일의 성능을 극대화하기 위해 이 값을 3으로 설정합니다. 데이터 중복 제거를 보다 적극적으로 실행하려는 경우 또는 중복 제거와 관련된 추가 대기 시간이 중요하지 않은 경우 이 설정을 수정할 수 있습니다.</td>
        </tr>
        <tr>
            <td>MinimumFileSize</td>
            <td>파일을 최적화에 대한 정책 내에 속하는 것으로 간주해야 하는 최소 파일 크기</td>
            <td>32KB보다 큰 양의 정수(바이트)</td>
            <td>이 값을 변경하는 주된 이유는 계산 시간을 절약하기 위해 최적화 값을 제한할 수 있는 작은 파일을 제외하기 위한 것입니다.</td>
        </tr>
        <tr>
            <td>NoCompress</td>
            <td>청크 저장소에 두기 전에 청크를 압축할지 여부</td>
            <td>True/False</td>
            <td>일부 파일 형식, 특히 멀티미디어 파일 및 이미 압축된 파일 형식은 효율적으로 압축되지 않을 수 있습니다. 이 설정을 통해 볼륨의 모든 파일에 대한 압축을 해제할 수 있습니다. 이는 많은 파일이 이미 압축된 데이터 집합을 최적화하는 경우에 가장 적합합니다.</td>
        </tr>
        <tr>
            <td>NoCompressionFileType</td>
            <td>청크 저장소로 이동하기 전에 해당 청크를 압축하지 않을 파일 형식</td>
            <td>파일 확장명의 배열</td>
            <td>일부 파일 형식, 특히 멀티미디어 파일 및 이미 압축된 파일 형식은 효율적으로 압축되지 않을 수 있습니다. 이 설정을 통해 이러한 파일에 대한 압축을 해제하여 CPU 리소스를 절약할 수 있습니다.</td>
        </tr>
        <tr>
            <td>OptimizeInUseFiles</td>
            <td>사용하도록 설정된 경우 활성 핸들이 있는 파일이 최적화에 대한 정책 내에 속하는 것으로 간주됩니다.</td>
            <td>True/false</td>
            <td>워크로드가 연장된 기간 동안 열린 상태로 유지되는 경우 이 설정을 사용하도록 설정합니다. 이 설정을 사용하도록 설정하지 않으면 워크로드에 열린 핸들이 있는 경우 파일이 최적화되지 않으며, 이는 끝에 데이터가 아주 드물게 추가되는 경우에도 마찬가지입니다.</td>
        </tr>
        <tr>
            <td>OptimizePartialFiles</td>
            <td>사용하도록 설정된 경우 MinimumFileAge 값은 전체 파일이 아니라 파일의 세그먼트에 적용됩니다.</td>
            <td>True/false</td>
            <td>자주 편집되는 대용량 파일에서 대부분의 파일 내용이 그대로 유지되는 경우 이 설정을 사용하도록 설정합니다. 이러한 파일은 변경된 상태로 유지되기 때문에 이 설정을 사용하도록 설정하지 않으면 대부분의 파일 내용이 최적화 준비가 완료된 경우에도 파일이 최적화되지 않습니다.</td>
        </tr>
        <tr>
            <td>확인</td>
            <td>사용하도록 설정된 경우 청크 해시가 청크 저장소에 이미 있는 청크와 일치하면 바이트 단위로 청크를 비교하여 동일한지 확인합니다.</td>
            <td>True/false</td>
            <td>이는 실제로 다르지만 해시가 동일한 두 개의 데이터 청크를 비교함으로써 청크를 비교하는 해시 알고리즘이 실수를 저지르지 않도록 하는 무결성 기능입니다. 실제로 이러한 문제는 거의 발생하지 않습니다. 확인 기능을 사용하도록 설정하면 최적화 작업에 상당한 오버헤드가 추가됩니다.</td>
        </tr>
    </tbody>
</table>

## <a id="modifying-dedup-system-settings"></a>데이터 중복 제거 시스템 수준 설정 수정
데이터 중복 제거에는 [레지스트리](https://technet.microsoft.com/library/cc755256(v=ws.11).aspx)를 통해 구성할 수 있는 추가 시스템 수준 설정이 있습니다. 이러한 설정은 시스템에서 실행되는 모든 작업 및 볼륨에 적용됩니다. 레지스트리를 편집할 때마다 각별히 주의해야 합니다.

예를 들어 전체 가비지 수집을 사용하지 않도록 설정할 수 있습니다. 이것이 사용자의 시나리오에 유용한 이유에 대한 자세한 내용은 [질문과 대답](#faq-why-disable-full-gc)에서 확인할 수 있습니다. PowerShell을 사용하여 레지스트리를 편집하려면 다음을 수행합니다.

* 데이터 중복 제거가 클러스터에서 실행되는 경우
    ```PowerShell
    Set-ItemProperty -Path HKLM:\System\CurrentControlSet\Services\ddpsvc\Settings -Name DeepGCInterval -Type DWord -Value 0xFFFFFFFF
    Set-ItemProperty -Path HKLM:\CLUSTER\Dedup -Name DeepGCInterval -Type DWord -Value 0xFFFFFFFF
    ```

* 데이터 중복 제거가 클러스터에서 실행되지 않는 경우
    ```PowerShell
    Set-ItemProperty -Path HKLM:\System\CurrentControlSet\Services\ddpsvc\Settings -Name DeepGCInterval -Type DWord -Value 0xFFFFFFFF
    ```

### <a id="modifying-dedup-system-settings-available-settings"></a>사용 가능한 시스템 수준 설정
<table>
    <thead>
        <tr>
            <th style="min-width:125px">설정 이름</th>
            <th>정의</th>
            <th>사용 가능한 값</th>
            <th>이 값을 변경하는 이유</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>WlmMemoryOverPercentThreshold</td>
            <td>이 설정을 통해 데이터 중복 제거가 실제로 사용 가능하다고 판단하는 것보다 많은 메모리를 작업에서 사용할 수 있습니다. 예를 들어 300으로 설정하면 작업에서 할당된 메모리의 3배를 사용하여 취소해야 합니다.</td>
            <td>양의 정수(값 300은 300% 또는 3배를 의미함)</td>
            <td>데이터 중복 제거에서 더 많은 메모리를 사용하면 중지되는 다른 작업이 있는 경우</td>
        </tr>
        <tr>
            <td>DeepGCInterval</td>
            <td>이 설정은 일반 가비지 수집 작업이 [전체 가비지 수집 작업](advanced-settings.md#faq-full-v-regular-gc)이 되는 간격을 구성합니다. 설정 n은 매 n<sup></sup>번째 작업이 전체 가비지 수집 작업임을 의미합니다. [백업 사용 유형](understand.md#usage-type-backup)을 사용하는 볼륨의 경우 전체 가비지 컬렉션은 항상 사용할 수 없습니다(레지스트리 값과 관계없음). `Start-DedupJob -Type GarbageCollection -Full` 백업 볼륨에 전체 가비지 수집을 원하는 경우 사용할 수 있습니다.</td>
            <td>정수(-1은 사용할 수 없음을 의미함)</td>
            <td>[이 질문과 대답](advanced-settings.md#faq-why-disable-full-gc)을 참조하세요.</td>
        </tr>
    </tbody>
</table>

## <a id="faq"></a>질문과 대답
<a id="faq-use-responsibly"></a>**데이터 중복 제거 설정을 변경 하 고 이제 작업 느린가 완료 되지 않고 또는 내 워크 로드 성능이 저하. 이유**  
이러한 설정은 데이터 중복 제거 실행 방법에 대한 제어 권한을 강화합니다. 책임감 있게 사용하고 [성능을 모니터링](run.md#monitoring-dedup)하세요.

<a id="faq-running-dedup-jobs-manually"></a>**지금 바로 데이터 중복 제거 작업을 실행 하려고 하지만 새 일정을 만들려면 하지 않으려는 경우 그럴 수 있습니까?**  
예, [모든 작업을 수동으로 실행할 수 있습니다](run.md#running-dedup-jobs-manually).

<a id="faq-full-v-regular-gc"></a>**전체 수집과 일반 가비지 수집 간의 차이 무엇입니까?**  
두 가지 유형의 [가비지 수집](understand.md#job-info-gc)이 있습니다.

- *일반 가비지 수집*은 통계 알고리즘을 사용하여 특정 조건(낮은 메모리 및 IOPs)을 충족하는 참조되지 않은 대용량 청크를 찾습니다. 일반 가비지 수집은 최소 비율의 청크가 참조되지 않은 경우에만 청크 저장소 컨테이너를 압축합니다. 이 유형의 가비지 수집은 전체 가비지 수집보다 훨씬 빠르게 실행되며 더 적은 리소스를 사용합니다. 일반 가비지 수집 작업의 기본 일정은 일주일에 한 번 실행되는 것입니다.
- *전체 가비지 수집*은 훨씬 철저한 작업을 수행하여 참조되지 않은 청크를 찾고 더 많은 디스크 공간을 확보합니다. 전체 가비지 수집은 컨테이너의 단일 청크만 참조되지 않은 경우에도 모든 컨테이너를 압축합니다. 또한 전체 가비지 수집은 최적화 작업 중에 작동 중단이나 정전이 발생하는 경우에도 사용 중일 수 있는 공간을 확보합니다. 전체 가비지 수집 작업은 일반 가비지 수집 작업에 비해 더 많은 시간과 시스템 리소스가 필요하지만 중복 제거된 볼륨에서 복구할 수 있는 사용 가능한 공간을 100% 복구합니다. 전체 가비지 수집 작업은 일반적으로 일반 가비지 수집 작업보다 참조되지 않은 데이터를 5% 더 찾아서 확보합니다. 전체 가비지 수집 작업의 기본 일정은 네 번째 때마다 예약된 가비지 수집을 실행하는 것입니다.

<a id="faq-why-disable-full-gc"></a>**전체 가비지 수집을 사용 하지 않도록 설정 하려고 하는 이유**  
- 가비지 수집은 볼륨의 수명, 섀도 복사본 및 증분 백업의 크기에 부정적인 영향을 줄 수 있습니다. 변동이 많거나 I/O 집약적인 워크로드는 전체 가비지 수집 작업으로 인해 성능이 저하될 수 있습니다.           
- 시스템이 작동 중단되었음을 알고 있는 경우 PowerShell에서 전체 가비지 수집 작업을 수동으로 실행하여 누수를 정리할 수 있습니다.
