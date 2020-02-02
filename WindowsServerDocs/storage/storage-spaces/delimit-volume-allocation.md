---
title: 스토리지 공간 다이렉트 볼륨의 할당을 구분 합니다.
ms.author: cosmosdarwin
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 03/29/2018
ms.openlocfilehash: 19e5a38ca406878b7dbc5a187b0057e97e4fe2d1
ms.sourcegitcommit: 74107a32efe1e53b36c938166600739a79dd0f51
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76918299"
---
# <a name="delimit-the-allocation-of-volumes-in-storage-spaces-direct"></a>스토리지 공간 다이렉트 볼륨의 할당을 구분 합니다.
> 적용 대상: Windows Server 2019

Windows Server 2019에는 스토리지 공간 다이렉트 볼륨의 할당을 수동으로 구분 하는 옵션이 도입 되었습니다. 이렇게 하면 특정 조건에 따라 내결함성이 크게 향상 되지만 몇 가지 추가 관리 고려 사항과 복잡성이 적용 됩니다. 이 항목에서는 PowerShell의 작동 방식에 대해 설명 하 고 예제를 제공 합니다.

   > [!IMPORTANT]
   > 이 기능은 Windows Server 2019에 새로 있습니다. Windows Server 2016에서는 사용할 수 없습니다. 

## <a name="prerequisites"></a>전제 조건

### <a name="green-checkmark-iconmediadelimit-volume-allocationsupportedpng-consider-using-this-option-if"></a>![녹색 확인 표시 아이콘입니다.](media/delimit-volume-allocation/supported.png) 다음 경우에이 옵션을 사용 하는 것이 좋습니다.

- 클러스터에 6 개 이상의 서버가 있습니다. 하거나
- 클러스터에서 [3 방향 미러](storage-spaces-fault-tolerance.md#mirroring) 복원 력을 사용 합니다.

### <a name="red-x-iconmediadelimit-volume-allocationunsupportedpng-do-not-use-this-option-if"></a>![빨간색 X 아이콘.](media/delimit-volume-allocation/unsupported.png) 다음 경우에는이 옵션을 사용 하지 마십시오.

- 클러스터에 6 개 미만의 서버가 있습니다. 디스크나
- 클러스터에서 [패리티](storage-spaces-fault-tolerance.md#parity) 또는 [미러 가속 패리티](storage-spaces-fault-tolerance.md#mirror-accelerated-parity) 복원 력을 사용 합니다.

## <a name="understand"></a>이해

### <a name="review-regular-allocation"></a>검토: 일반 할당

정기적인 3 방향 미러링을 사용 하면 볼륨이 세 번 복사 되 고 클러스터의 모든 서버에 있는 모든 드라이브에 고르게 분산 되는 여러 개의 작은 "줄임"로 나뉩니다. 자세한 내용은 [심층 정보 블로그](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/)를 참조 하세요.

![3 개의 줄임 스택으로 나뉘어 모든 서버에 균일 하 게 분산 되는 볼륨을 보여 주는 다이어그램입니다.](media/delimit-volume-allocation/regular-allocation.png)

이 기본 할당은 병렬 읽기와 쓰기를 극대화 하 고 성능이 향상 되며, 모든 서버는 동일 하 게 사용 되 고 모든 드라이브가 동일 하 게 가득 차서 모든 볼륨이 온라인 상태가 되거나 함께 오프 라인으로 전환 됩니다. 모든 볼륨은 [다음 예제](storage-spaces-fault-tolerance.md#examples) 에서 설명 하는 것 처럼 최대 두 개의 동시 오류를 계속 유지 합니다.

그러나이 할당을 사용 하는 경우에는 볼륨에 세 개의 동시 오류가 남아 있을 수 없습니다. 3 개의 서버가 한 번에 실패 하는 경우 또는 3 개의 서버에 있는 드라이브가 한 번에 실패 하는 경우에는 최소 줄임 (매우 높은 확률)가 실패 한 정확히 3 개의 드라이브 또는 서버에 할당 되기 때문에 볼륨에 액세스할 수 없게 됩니다.

아래 예제에서는 서버 1, 3, 5가 동시에 실패 합니다. 많은 줄임 복사본을 보유 하 고 있지만 일부는 그렇지 않습니다.

![빨간색으로 강조 표시 된 6 개의 서버를 보여 주는 다이어그램 및 전체 볼륨이 빨간색입니다.](media/delimit-volume-allocation/regular-does-not-survive.png)

볼륨이 오프 라인 상태가 되 고 서버가 복구 될 때까지 액세스할 수 없게 됩니다.

### <a name="new-delimited-allocation"></a>새: 구분 된 할당

구분 된 할당을 사용 하 여 사용할 서버의 하위 집합을 지정 합니다 (최소 4 개). 이 볼륨은 이전과 같이 세 번 복사 된 줄임로 나뉩니다. 하지만 모든 서버에서 할당 하는 대신 **줄임는 지정한 서버의 하위 집합에만 할당 됩니다**.

예를 들어 8 개 노드 클러스터 (노드 1 ~ 8)가 있는 경우 노드 1, 2, 3, 4의 디스크에만 위치할 볼륨을 지정할 수 있습니다.
#### <a name="advantages"></a>이점

예제 할당을 사용 하는 경우 볼륨은 3 개의 동시 오류를 존속 시킬 가능성이 높습니다. 노드 1, 2, 6이 다운 되 면 볼륨의 데이터 복사본 3 개를 포함 하는 노드 2 개만 다운 되 고 볼륨이 온라인 상태로 유지 됩니다.

유지 확률은 서버 수 및 기타 요인에 따라 달라 집니다. 자세한 내용은 [분석](#analysis) 을 참조 하세요.

#### <a name="disadvantages"></a>단점

구분 된 할당은 몇 가지 추가 관리 고려 사항 및 복잡성을 적용 합니다.

1. 관리자는 [최선의 구현 방법](#best-practices) 섹션에 설명 된 대로 서버 전체에서 저장소 사용률의 균형을 유지 하 고 취했습니다 높은 생존 확률을 유지 하기 위해 각 볼륨의 할당을 구분 해야 합니다.

2. 분리 된 할당을 사용 하 여 **서버당 하나의 용량 드라이브 (최대값 없음)** 를 예약 합니다. 이는 일반 할당에 대해 [게시 된 권장 사항](plan-volumes.md#choosing-the-size-of-volumes) 보다 더 다양 합니다 .이는 총 4 개의 용량 드라이브에서 최대로 출력 합니다.

3. 서버 [와 해당 드라이브 제거](remove-servers.md#remove-a-server-and-its-drives)에 설명 된 대로 서버에 오류가 발생 하 여 교체 해야 하는 경우 관리자는 새 서버를 추가 하 고 실패 한 한 가지 예를 제거 하 여 영향을 받는 볼륨의 delimitation 업데이트 해야 합니다.

## <a name="usage-in-powershell"></a>PowerShell에서 사용

`New-Volume` cmdlet을 사용 하 여 스토리지 공간 다이렉트에서 볼륨을 만들 수 있습니다.

예를 들어 일반 3 방향 미러 볼륨을 만들려면 다음을 수행 합니다.

```PowerShell
New-Volume -FriendlyName "MyRegularVolume" -Size 100GB
```

### <a name="create-a-volume-and-delimit-its-allocation"></a>볼륨을 만들고 해당 할당을 구분 합니다.

3 방향 미러 볼륨을 만들고 해당 할당을 구분 하려면 다음을 수행 합니다.

1. 먼저 클러스터의 서버를 `$Servers`변수에 할당 합니다.

    ```PowerShell
    $Servers = Get-StorageFaultDomain -Type StorageScaleUnit | Sort FriendlyName
    ```

   > [!TIP]
   > 스토리지 공간 다이렉트에서 ' 저장소 배율 단위 ' 라는 용어는 직접 연결 된 드라이브 및 드라이브와 직접 연결 된 외부 인클로저를 포함 하 여 한 서버에 연결 된 모든 원시 저장소를 나타냅니다. 이 컨텍스트에서는 ' server '와 같습니다.

2. 새 `-StorageFaultDomainsToUse` 매개 변수와 함께 사용할 서버를 지정 하 고 `$Servers`에 인덱싱을 지정 합니다. 예를 들어 첫 번째, 두 번째, 세 번째 및 네 번째 서버 (인덱스 0, 1, 2, 3)에 대 한 할당을 구분 하려면 다음을 수행 합니다.

    ```PowerShell
    New-Volume -FriendlyName "MyVolume" -Size 100GB -StorageFaultDomainsToUse $Servers[0,1,2,3]
    ```

### <a name="see-a-delimited-allocation"></a>구분 된 할당 보기

*Myvolume* 을 할당 하는 방법을 확인 하려면 [부록](#appendix)에서 `Get-VirtualDiskFootprintBySSU.ps1` 스크립트를 사용 합니다.

```PowerShell
PS C:\> .\Get-VirtualDiskFootprintBySSU.ps1

VirtualDiskFriendlyName TotalFootprint Server1 Server2 Server3 Server4 Server5 Server6
----------------------- -------------- ------- ------- ------- ------- ------- -------
MyVolume                300 GB         100 GB  100 GB  100 GB  100 GB  0       0      
```

Server1, Server2, Server3 및 Server4만 *Myvolume*의 줄임를 포함 합니다.

### <a name="change-a-delimited-allocation"></a>구분 된 할당 변경

새 `Add-StorageFaultDomain` 및 `Remove-StorageFaultDomain` cmdlet을 사용 하 여 할당을 구분 하는 방법을 변경할 수 있습니다.

예를 들어 *Myvolume* 을 한 서버에서 이동 하려면 다음을 수행 합니다.

1. 다섯 번째 서버가 *Myvolume*의 줄임을 저장할 **수** 있도록 지정 합니다.

    ```PowerShell
    Get-VirtualDisk MyVolume | Add-StorageFaultDomain -StorageFaultDomains $Servers[4]
    ```

2. 첫 번째 서버가 *Myvolume*의 줄임을 저장할 **수** 없도록 지정 합니다.

    ```PowerShell
    Get-VirtualDisk MyVolume | Remove-StorageFaultDomain -StorageFaultDomains $Servers[0]
    ```

3. 변경 내용을 적용 하려면 저장소 풀의 균형을 다시 조정 합니다.

    ```PowerShell
    Get-StoragePool S2D* | Optimize-StoragePool
    ```

`Get-StorageJob`를 사용 하 여 리 밸런스의 진행률을 모니터링할 수 있습니다.

완료 되 면 `Get-VirtualDiskFootprintBySSU.ps1`를 다시 실행 하 여 *Myvolume* 이 이동 했는지 확인 합니다.

```PowerShell
PS C:\> .\Get-VirtualDiskFootprintBySSU.ps1

VirtualDiskFriendlyName TotalFootprint Server1 Server2 Server3 Server4 Server5 Server6
----------------------- -------------- ------- ------- ------- ------- ------- -------
MyVolume                300 GB         0       100 GB  100 GB  100 GB  100 GB  0      
```

S e r v e r 1에 *Myvolume* 의 줄임이 더 이상 포함 되지 않습니다. 대신 Server5이 수행 합니다.

## <a name="best-practices"></a>최선의 구현 방법

구분 된 볼륨 할당을 사용할 때 따라야 할 모범 사례는 다음과 같습니다.

### <a name="choose-four-servers"></a>4 대의 서버 선택

3 방향 미러 볼륨을 각각 4 개의 서버로 구분 합니다.

### <a name="balance-storage"></a>저장소 잔액

각 서버에 할당 된 저장소의 크기를 조정 하 여 볼륨 크기를 고려 합니다.

### <a name="stagger-delimited-allocation-volumes"></a>분리 된 할당 볼륨

내결함성을 최대화 하려면 각 볼륨의 할당을 고유 하 게 지정 합니다. 즉, *모든* 서버를 다른 볼륨과 공유 하지 않습니다. 즉, 일부 중복이 보장 됩니다. 

예를 들어 8 개 노드 시스템: 볼륨 1: 서버 1, 2, 3, 4 볼륨 2: 서버 5, 6, 7, 8 볼륨 3: 서버 3, 4, 5, 6 볼륨 4: 서버 1, 2, 7, 8

## <a name="analysis"></a>분석과

이 섹션에서는 오류가 발생 한 횟수와 클러스터 크기의 기능으로 볼륨이 온라인 상태가 되 고 온라인 상태를 유지 하 고 액세스할 수 있는 전체 저장소의 예상 비율에 액세스할 수 있는 수학적 확률을 파생 합니다.

   > [!NOTE]
   > 이 섹션은 선택적으로 읽을 수 있습니다. 수학을 keen 하는 경우에는를 읽어 보세요. 그러나 그렇지 않은 경우에는 걱정 하지 마세요. [PowerShell의 사용량과](#usage-in-powershell) [모범 사례](#best-practices) 는 모두 구분 된 할당을 성공적으로 구현 해야 한다는 것입니다.

### <a name="up-to-two-failures-is-always-okay"></a>최대 2 개의 실패는 항상 정상입니다.

3 방향 미러 볼륨은 할당에 관계 없이 동시에 최대 두 번의 오류를 발생 시킬 수 있습니다. 두 드라이브에 오류가 발생 하거나 두 개의 서버에서 오류가 발생 하거나, 두 서버 중 하나에서 오류가 발생 하는 경우 모든 3 방향 미러 볼륨은 온라인 상태를 유지 하 고 일반 할당을 통해 액세스할 수 있습니다

### <a name="more-than-half-the-cluster-failing-is-never-okay"></a>클러스터 실패의 절반 이상이 충분 하지 않음

반대로 클러스터에 있는 서버 또는 드라이브의 절반 이상이 한 번에 실패 하는 극단적인 경우에는 [쿼럼이 손실 되](understand-quorum.md) 고 모든 3 방향 미러 볼륨이 오프 라인 상태가 되 고 해당 할당에 관계 없이 액세스할 수 없게 됩니다.

### <a name="what-about-in-between"></a>어디에 있나요?

한 번에 세 개 이상의 오류가 발생 하지만 서버와 드라이브 중 절반 이상이 계속 작동 하는 경우 오류가 발생 한 서버에 따라 분리 된 할당이 있는 볼륨이 온라인 상태로 유지 되 고 액세스할 수 있습니다.

## <a name="frequently-asked-questions"></a>질문과 대답

### <a name="can-i-delimit-some-volumes-but-not-others"></a>일부 볼륨을 구분할 수 있나요?

그렇습니다. 할당을 구분할 지 여부에 따라 볼륨별를 선택할 수 있습니다.

### <a name="does-delimited-allocation-change-how-drive-replacement-works"></a>구분 된 할당을 통해 드라이브 교체가 어떻게 작동 하나요?

아니요, 일반 할당과 동일 합니다.

## <a name="see-also"></a>참고 항목

- [스토리지 공간 다이렉트 개요](storage-spaces-direct-overview.md)
- [스토리지 공간 다이렉트의 내결함성](storage-spaces-fault-tolerance.md)

## <a name="appendix"></a>부록

이 스크립트는 볼륨을 할당 하는 방법을 확인 하는 데 도움이 됩니다.

위에서 설명한 대로 사용 하려면 복사/붙여넣기 및 다른 이름으로 저장을 `Get-VirtualDiskFootprintBySSU.ps1`합니다.

```PowerShell
Function ConvertTo-PrettyCapacity {
    Param (
        [Parameter(
            Mandatory = $True,
            ValueFromPipeline = $True
            )
        ]
    [Int64]$Bytes,
    [Int64]$RoundTo = 0
    )
    If ($Bytes -Gt 0) {
        $Base = 1024
        $Labels = ("bytes", "KB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB")
        $Order = [Math]::Floor( [Math]::Log($Bytes, $Base) )
        $Rounded = [Math]::Round($Bytes/( [Math]::Pow($Base, $Order) ), $RoundTo)
        [String]($Rounded) + " " + $Labels[$Order]
    }
    Else {
        "0"
    }
    Return
}

Function Get-VirtualDiskFootprintByStorageFaultDomain {

    ################################################
    ### Step 1: Gather Configuration Information ###
    ################################################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Gathering configuration information..." -Status "Step 1/4" -PercentComplete 00

    $ErrorCannotGetCluster = "Cannot proceed because 'Get-Cluster' failed."
    $ErrorNotS2DEnabled = "Cannot proceed because the cluster is not running Storage Spaces Direct."
    $ErrorCannotGetClusterNode = "Cannot proceed because 'Get-ClusterNode' failed."
    $ErrorClusterNodeDown = "Cannot proceed because one or more cluster nodes is not Up."
    $ErrorCannotGetStoragePool = "Cannot proceed because 'Get-StoragePool' failed."
    $ErrorPhysicalDiskFaultDomainAwareness = "Cannot proceed because the storage pool is set to 'PhysicalDisk' fault domain awareness. This cmdlet only supports 'StorageScaleUnit', 'StorageChassis', or 'StorageRack' fault domain awareness."

    Try  {
        $GetCluster = Get-Cluster -ErrorAction Stop
    }
    Catch {
        throw $ErrorCannotGetCluster
    }

    If ($GetCluster.S2DEnabled -Ne 1) {
        throw $ErrorNotS2DEnabled
    }

    Try  {
        $GetClusterNode = Get-ClusterNode -ErrorAction Stop
    }
    Catch {
        throw $ErrorCannotGetClusterNode
    }

    If ($GetClusterNode | Where State -Ne Up) {
        throw $ErrorClusterNodeDown
    }

    Try {
        $GetStoragePool = Get-StoragePool -IsPrimordial $False -ErrorAction Stop
    }
    Catch {
        throw $ErrorCannotGetStoragePool
    }

    If ($GetStoragePool.FaultDomainAwarenessDefault -Eq "PhysicalDisk") {
        throw $ErrorPhysicalDiskFaultDomainAwareness
    }

    ###########################################################
    ### Step 2: Create SfdList[] and PhysicalDiskToSfdMap{} ###
    ###########################################################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Analyzing physical disk information..." -Status "Step 2/4" -PercentComplete 25

    $SfdList = Get-StorageFaultDomain -Type ($GetStoragePool.FaultDomainAwarenessDefault) | Sort FriendlyName # StorageScaleUnit, StorageChassis, or StorageRack

    $PhysicalDiskToSfdMap = @{} # Map of PhysicalDisk.UniqueId -> StorageFaultDomain.FriendlyName
    $SfdList | ForEach {
        $StorageFaultDomain = $_
        $_ | Get-StorageFaultDomain -Type PhysicalDisk | ForEach {
            $PhysicalDiskToSfdMap[$_.UniqueId] = $StorageFaultDomain.FriendlyName
        }
    }

    ##################################################################################################
    ### Step 3: Create VirtualDisk.FriendlyName -> { StorageFaultDomain.FriendlyName -> Size } Map ###
    ##################################################################################################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Analyzing virtual disk information..." -Status "Step 3/4" -PercentComplete 50

    $GetVirtualDisk = Get-VirtualDisk | Sort FriendlyName

    $VirtualDiskMap = @{}

    $GetVirtualDisk | ForEach {
        # Map of PhysicalDisk.UniqueId -> Size for THIS virtual disk
        $PhysicalDiskToSizeMap = @{}
        $_ | Get-PhysicalExtent | ForEach {
            $PhysicalDiskToSizeMap[$_.PhysicalDiskUniqueId] += $_.Size
        }
        # Map of StorageFaultDomain.FriendlyName -> Size for THIS virtual disk
        $SfdToSizeMap = @{}
        $PhysicalDiskToSizeMap.keys | ForEach {
            $SfdToSizeMap[$PhysicalDiskToSfdMap[$_]] += $PhysicalDiskToSizeMap[$_]
        }
        # Store
        $VirtualDiskMap[$_.FriendlyName] = $SfdToSizeMap
    }

    #########################
    ### Step 4: Write-Out ###
    #########################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Formatting output..." -Status "Step 4/4" -PercentComplete 75

    $Output = $GetVirtualDisk | ForEach {
        $Row = [PsCustomObject]@{}

        $VirtualDiskFriendlyName = $_.FriendlyName
        $Row | Add-Member -MemberType NoteProperty "VirtualDiskFriendlyName" $VirtualDiskFriendlyName

        $TotalFootprint = $_.FootprintOnPool | ConvertTo-PrettyCapacity
        $Row | Add-Member -MemberType NoteProperty "TotalFootprint" $TotalFootprint

        $SfdList | ForEach {
            $Size = $VirtualDiskMap[$VirtualDiskFriendlyName][$_.FriendlyName] | ConvertTo-PrettyCapacity
            $Row | Add-Member -MemberType NoteProperty $_.FriendlyName $Size
        }

        $Row
    }

    # Calculate width, in characters, required to Format-Table
    $RequiredWindowWidth = ("TotalFootprint").length + 1 + ("VirtualDiskFriendlyName").length + 1
    $SfdList | ForEach {
        $RequiredWindowWidth += $_.FriendlyName.Length + 1
    }

    $ActualWindowWidth = (Get-Host).UI.RawUI.WindowSize.Width

    If (!($ActualWindowWidth)) {
        # Cannot get window width, probably ISE, Format-List
        Write-Warning "Could not determine window width. For the best experience, use a Powershell window instead of ISE"
        $Output | Format-Table
    }
    ElseIf ($ActualWindowWidth -Lt $RequiredWindowWidth) {
        # Narrower window, Format-List
        Write-Warning "For the best experience, try making your PowerShell window at least $RequiredWindowWidth characters wide. Current width is $ActualWindowWidth characters."
        $Output | Format-List
    }
    Else {
        # Wider window, Format-Table
        $Output | Format-Table
    }
}

Get-VirtualDiskFootprintByStorageFaultDomain
```
