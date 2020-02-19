---
ms.assetid: 898d72f1-01e7-4b87-8eb3-a8e0e2e6e6da
title: 저장소 공간 다이렉트에 서버 또는 드라이브 추가
ms.prod: windows-server
ms.author: cosdar
ms.manager: dongill
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 11/06/2017
description: 스토리지 공간 다이렉트 클러스터에 서버 또는 드라이브를 추가 하는 방법
ms.localizationpriority: medium
ms.openlocfilehash: f5fb9da903bb76de3a075fa7feeeaba468d802c2
ms.sourcegitcommit: 2a15de216edde8b8e240a4aa679dc6d470e4159e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77465627"
---
# <a name="adding-servers-or-drives-to-storage-spaces-direct"></a>저장소 공간 다이렉트에 서버 또는 드라이브 추가

>적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 저장소 공간 다이렉트에 서버 또는 드라이브를 추가하는 방법에 대해 설명합니다.

## <a name="adding-servers"></a>서버 추가

규모 확장이라고도 하는 서버 추가는 스토리지 용량을 추가하고, 스토리지 성능을 개선하고, 스토리지 효율성을 더욱 높입니다. 하이퍼 수렴형 배포인 경우 서버를 추가하면 워크로드에 더 많은 컴퓨팅 리소스가 제공됩니다.

![4 개 노드 클러스터에 서버를 추가 하는 애니메이션](media/add-nodes/Scaling-Out.gif)

일반적인 배포는 서버를 추가하여 간단하게 확장하는 것입니다. 두 단계만 수행하면 됩니다.

1. 장애 조치(Failover) 클러스터 스냅인을 사용하거나 PowerShell에서 [Test-Cluster](https://technet.microsoft.com/library/cc732035(v=ws.10).aspx) cmdlet을 사용하여(관리자 권한으로 실행) **클러스터 유효성 검사 마법사**를 실행합니다. 추가하려는 새 서버 *\<NewNode>* 를 포함합니다.

   ```PowerShell
   Test-Cluster -Node <Node>, <Node>, <Node>, <NewNode> -Include "Storage Spaces Direct", Inventory, Network, "System Configuration"
   ```

   이를 통해 새 서버가 Windows Server 2016 Datacenter Edition을 실행 중이고, 기존 서버와 동일한 Active Directory Domain Services 도메인에 추가되었으며, 필요한 모든 역할과 기능을 가지고 있고, 네트워킹이 적절히 구성되어 있음을 확인하게 됩니다.

   >[!IMPORTANT]
   > 더 이상 필요하지 않은 오래된 데이터나 메타데이터가 포함된 드라이브를 다시 사용하려면 **Disk Management** 또는 **Reset-PhysicalDisk** cmdlet을 사용하여 이들을 지웁니다. 오래된 데이터나 메타데이터가 검색되면 드라이브가 풀링되지 않습니다.

2. 서버 추가를 완료하려면 클러스터에서 다음 cmdlet을 실행합니다.

```
Add-ClusterNode -Name NewNode 
```

   >[!NOTE]
   > 자동 풀링은 풀이 하나만 있는 경우 이용할 수 있습니다. 표준 구성을 피해 여러 풀을 만든 경우 **Add-physicaldisk**를 사용하여 기본 설정 풀에 새 드라이브를 직접 추가해야 합니다.

### <a name="from-2-to-3-servers-unlocking-three-way-mirroring"></a>서버 2개에서 3개로: 3방향 미러링 잠금 해제

![2 개 노드 클러스터에 세 번째 서버 추가](media/add-nodes/Scaling-2-to-3.png)

서버가 두 개인 경우 양방향 미러 볼륨만 만들 수 있습니다(분산형 RAID-1과 비교). 서버가 세 개이면 더 높은 내결함성을 위해 3방향 미러 볼륨을 만들 수 있습니다. 가능하면 3방향 미러링을 사용하는 것이 좋습니다.

양방향 미러 볼륨은 현재 위치에서 3방향 미러링으로 업그레이드할 수 없습니다. 대신 새 볼륨을 만들어 데이터를 마이그레이션([Storage Replica](../storage-replica/server-to-server-storage-replication.md) 등을 사용하여 복사)한 다음 오래된 볼륨을 제거합니다.

3방향 미러 볼륨을 만들기 시작할 때 몇 가지 유용한 옵션이 있습니다. 원하는 옵션을 사용하면 됩니다. 

#### <a name="option-1"></a>옵션 1

새 볼륨을 만들 때 각 볼륨에서 **PhysicalDiskRedundancy = 2**를 지정합니다.

```PowerShell
New-Volume -FriendlyName <Name> -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size <Size> -PhysicalDiskRedundancy 2
```

#### <a name="option-2"></a>옵션 2

대신 풀의 **Mirror**라는 **ResiliencySetting** 개체에 **PhysicalDiskRedundancyDefault = 2**를 설정할 수 있습니다. 그러면 별도로 지정하지 않아도 새 미러 볼륨이 자동으로 *3방향* 미러링을 사용하게 됩니다.

```PowerShell
Get-StoragePool S2D* | Get-ResiliencySetting -Name Mirror | Set-ResiliencySetting -PhysicalDiskRedundancyDefault 2

New-Volume -FriendlyName <Name> -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size <Size>
```

#### <a name="option-3"></a>옵션 3

**Capacity**라는 **StorageTier** 템플릿에서 *PhysicalDiskRedundancy = 2*를 설정한 다음 계층을 참조하여 볼륨을 만듭니다.

```PowerShell
Set-StorageTier -FriendlyName Capacity -PhysicalDiskRedundancy 2 

New-Volume -FriendlyName <Name> -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -StorageTierFriendlyNames Capacity -StorageTierSizes <Size>
```

### <a name="from-3-to-4-servers-unlocking-dual-parity"></a>서버 3개에서 4개로: 이중 패리티 잠금 해제

![3 개 노드 클러스터에 네 번째 서버 추가](media/add-nodes/Scaling-3-to-4.png)

서버가 네 개인 경우 삭제 코딩(erasure coding)이라고도 하는 이중 패리티를 사용할 수 있습니다(분산형 RAID-6과 비교). 이 경우 3방향 미러링과 동일한 내결함성이 제공되지만 스토리지 효율성은 더 높습니다. 자세한 내용은 [내결함성 및 저장소 효율성](storage-spaces-fault-tolerance.md)을 참조하세요.

더 작은 배포를 살펴보면 이중 패리티 볼륨을 만들기 시작할 때 사용할 수 있는 몇 가지 유용한 옵션이 있습니다. 원하는 옵션을 사용하면 됩니다.

#### <a name="option-1"></a>옵션 1

새 볼륨을 만들 때 각 볼륨에서 **PhysicalDiskRedundancy = 2** 및 **ResiliencySettingName = Parity**를 지정합니다.

```PowerShell
New-Volume -FriendlyName <Name> -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size <Size> -PhysicalDiskRedundancy 2 -ResiliencySettingName Parity
```

#### <a name="option-2"></a>옵션 2

풀의 **Parity**라는 **ResiliencySetting** 개체에 **PhysicalDiskRedundancy = 2**를 설정합니다. 그러면 별도로 지정하지 않아도 새 패리티 볼륨이 자동으로 *이중* 패리티를 사용하게 됩니다.

```PowerShell
Get-StoragePool S2D* | Get-ResiliencySetting -Name Parity | Set-ResiliencySetting -PhysicalDiskRedundancyDefault 2

New-Volume -FriendlyName <Name> -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size <Size> -ResiliencySettingName Parity
```

서버가 네 개인 경우 미러-가속 패리티를 사용할 수 있습니다. 여기서 개별 볼륨은 부분 미러 및 부분 패리티입니다.

이 경우 **Performance** 계층과 *Capacity* 계층을 모두 포함하도록 *StorageTier* 템플릿을 업데이트해야 합니다. 이 두 계층은 네 개의 서버에서 **Enable-ClusterS2D**를 처음 실행한 경우에만 생성되기 때문입니다. 구체적으로, 두 계층에는 용량 장치(예: SSD 또는 HDD)의 **MediaType** 및 **PhysicalDiskRedundancy = 2**가 있어야 합니다. *Performance* 계층은 **ResiliencySettingName = Mirror**, *Capacity* 계층은 **ResiliencySettingName = Parity**여야 합니다.

#### <a name="option-3"></a>옵션 3

기존 계층 템플릿을 제거하고 두 계층 템플릿을 새로 만드는 것이 가장 쉬울 수 있습니다. 계층 템플릿을 참조 하 여 만든 기존 볼륨에는 영향을 주지 않습니다. 단지 템플릿입니다.

```PowerShell
Remove-StorageTier -FriendlyName Capacity

New-StorageTier -StoragePoolFriendlyName S2D* -MediaType HDD -PhysicalDiskRedundancy 2 -ResiliencySettingName Mirror -FriendlyName Performance
New-StorageTier -StoragePoolFriendlyName S2D* -MediaType HDD -PhysicalDiskRedundancy 2 -ResiliencySettingName Parity -FriendlyName Capacity
```

정말 간단하죠. 이제 이 계층 템플릿을 참조하여 미러-가속 패리티 볼륨을 만들 준비가 되었습니다.

#### <a name="example"></a>예제

```PowerShell
New-Volume -FriendlyName "Sir-Mix-A-Lot" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -StorageTierFriendlyNames Performance, Capacity -StorageTierSizes <Size, Size> 
```

### <a name="beyond-4-servers-greater-parity-efficiency"></a>서버가 5개 이상일 경우: 패리티 효율성 향상

서버를 5개 이상으로 확장할 경우 새 볼륨은 훨씬 큰 패리티 인코딩 효율성의 혜택을 누릴 수 있습니다. 예를 들어 6~7개 서버의 경우 Reed-Solomon 4+2(2+2가 아닌)를 사용할 수 있으므로 효율성이 50.0%에서 66.7%로 향상됩니다. 이 새로운 효율성을 누리기 위해 수행해야 할 추가 단계는 없습니다. 볼륨을 만들 때마다 가능한 최적의 인코딩이 자동으로 결정됩니다.

그러나 기존의 볼륨이 더 폭넓은 새 인코딩으로 "변환"되지는 *않습니다*. 한 가지 좋은 점은, 그렇게 할 경우 전체 배포의 *모든 단일 비트*에 영향을 미치는 대량 계산이 필요할 수 있다는 사실입니다. 기존 데이터를 더 높은 효율성으로 인코딩하려는 경우 새 볼륨으로 마이그레이션할 수 있습니다.

자세한 내용은 [내결함성 및 저장소 효율성](storage-spaces-fault-tolerance.md)을 참조하세요.

### <a name="adding-servers-when-using-chassis-or-rack-fault-tolerance"></a>섀시 또는 랙 내결함성을 사용하는 경우 서버 추가

배포에 섀시 또는 랙 내결함성을 사용하는 경우 클러스터에 추가하기 전에 새 서버의 섀시 또는 랙을 지정해야 합니다. 그러면 저장소 공간 다이렉트는 내결함성을 최대화하도록 데이터를 배포하는 방법을 알게 됩니다.

1. 승격된 PowerShell 세션을 열고 다음 명령을 사용하여 노드에 대한 임시 장애 도메인을 만듭니다. 여기서 *\<NewNode>* 는 새 클러스터 노드의 이름입니다.

   ```PowerShell
   New-ClusterFaultDomain -Type Node -Name <NewNode> 
   ```

2. 이 임시 장애 도메인을 섀시 또는 랙으로 이동합니다. 새 서버는 *\<ParentName>* 에 지정된 실제 장소에 있습니다.

   ```PowerShell
   Set-ClusterFaultDomain -Name <NewNode> -Parent <ParentName> 
   ```

   자세한 내용은 [Windows Server 2016에서 장애 도메인 인식](../../failover-clustering/fault-domains.md)을 참조하세요.

3. [서버 추가](#adding-servers)에 설명된 대로 클러스터에 서버를 추가합니다. 새 서버를 클러스터에 추가하면 자동으로 자리 표시자 장애 도메인과 연결됩니다(자체 이름 사용).

## <a name="adding-drives"></a>드라이브 추가

드라이브 추가(강화라고도 함)는 스토리지 용량을 추가하고 성능도 향상할 수 있습니다. 사용 가능한 슬롯이 있는 경우 서버를 추가하지 않고 각 서버에 드라이브를 추가하여 스토리지 용량을 확장할 수 있습니다. 캐시 드라이브 또는 용량 드라이브를 언제든지 독립적으로 추가할 수 있습니다.

   >[!IMPORTANT]
   > 모든 서버를 동일한 스토리지 구성으로 구성하는 것이 좋습니다.

![디스크를 시스템과 함께 추가 하는 애니메이션](media/add-nodes/Scale-Up.gif)

확장하려면 드라이브를 연결하고 Windows에서 이를 검색하는지 확인합니다. 드라이버가 PowerShell의 **Get-PhysicalDisk** cmdlet의 출력에 표시되어야 하고 **CanPool** 속성이 **True**로 설정되어야 합니다. 속성이 **CanPool = False**로 표시되면 **CannotPoolReason** 속성을 확인하여 그 이유를 알아볼 수 있습니다.

```PowerShell
Get-PhysicalDisk | Select SerialNumber, CanPool, CannotPoolReason
```

짧은 시간 내에 적격 드라이브가 저장소 공간 다이렉트에 의해 자동으로 클레임되고, 저장소 풀에 추가되며, 볼륨이 자동으로 [모든 드라이브에 균일하게 재배포됩니다](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/). 이 시점에서 작업을 마치고 [볼륨을 확장](resize-volumes.md)하거나 [새 볼륨을 만들](create-volumes.md) 준비가 완료됩니다.

드라이브가 나타나지 않으면 하드웨어 변경 사항을 수동으로 검색합니다. **작업** 메뉴의 **장치 관리자**를 사용하면 됩니다. 오래된 데이터 또는 메타데이터가 포함된 경우 다시 포맷하는 것이 좋습니다. 이 작업은 **디스크 관리** 또는 **Reset-PhysicalDisk** cmdlet을 사용하여 수행할 수 있습니다.

   >[!NOTE]
   > 자동 풀링은 풀이 하나만 있는 경우 이용할 수 있습니다. 표준 구성을 피해 여러 풀을 만든 경우 **Add-physicaldisk**를 사용하여 기본 설정 풀에 새 드라이브를 직접 추가해야 합니다.

## <a name="optimizing-drive-usage-after-adding-drives-or-servers"></a>드라이브 또는 서버를 추가한 후 드라이브 사용 최적화

시간이 지남에 따라 드라이브를 추가 하거나 제거 하면 풀의 드라이브 간에 데이터를 분산 하는 것은 불균형 해질 수 있습니다. 일부 경우에는 특정 드라이브가 가득 차서 풀의 다른 드라이브가 훨씬 낮은 사용량을 초래할 수 있습니다.

풀에 대 한 드라이브 할당을 유지 하기 위해 스토리지 공간 다이렉트는 풀에 드라이브나 서버를 추가한 후 드라이브 사용을 자동으로 최적화 합니다 (공유 SAS 인클로저를 사용 하는 저장소 공간 시스템의 수동 프로세스). 최적화는 풀에 새 드라이브를 추가한 후 15 분이 지나면 시작 됩니다. 풀 최적화는 우선 순위가 낮은 백그라운드 작업으로 실행 되므로 특히 용량이 많은 하드 드라이브를 사용 하는 경우 완료 하는 데 몇 시간이 나 며칠 정도 걸릴 수 있습니다.

최적화는 두 개의 작업 ( *최적화* 라고 함)과 *리 밸런스* 하나를 사용 합니다. 즉, 다음 명령을 사용 하 여 진행률을 모니터링할 수 있습니다.

```powershell
Get-StorageJob
```

[최적화-storagepool](https://docs.microsoft.com/powershell/module/storage/optimize-storagepool?view=win10-ps) cmdlet을 사용 하 여 저장소 풀을 수동으로 최적화할 수 있습니다. 예를 들면 다음과 같습니다.

```powershell
Get-StoragePool <PoolName> | Optimize-StoragePool
```
