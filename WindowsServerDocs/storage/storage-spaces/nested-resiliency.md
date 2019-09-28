---
title: 스토리지 공간 다이렉트에 대 한 중첩 복원 력
ms.prod: windows-server
ms.author: jgerend
ms.manager: dansimp
ms.technology: storagespaces
ms.topic: article
author: cosmosdarwin
ms.date: 03/15/2019
ms.openlocfilehash: ea1c4b2c249759634e00f6a1ac2caa34f8085ae1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402862"
---
# <a name="nested-resiliency-for-storage-spaces-direct"></a>스토리지 공간 다이렉트에 대 한 중첩 복원 력

> 적용 대상: Windows Server 2019

중첩 된 복원 력은 Windows Server 2019에 [스토리지 공간 다이렉트](storage-spaces-direct-overview.md) 의 새로운 기능으로,이 기능을 통해 두 서버 클러스터에서 저장소 가용성의 손실 없이 여러 하드웨어 오류를 동시에 견딜 수 있습니다. 즉, 사용자, 앱 및 가상 컴퓨터를 사용할 수 있습니다. 중단 없이 계속 실행 합니다. 이 항목에서는 작동 방식에 대해 설명 하 고, 시작 하는 단계별 지침을 제공 하 고, 가장 자주 묻는 질문에 대 한 답을 제공 합니다.

## <a name="prerequisites"></a>사전 요구 사항

### <a name="green-checkmark-iconmedianested-resiliencysupportedpng-consider-nested-resiliency-if"></a>![녹색 확인 표시 아이콘입니다.](media/nested-resiliency/supported.png) 다음과 같은 경우 중첩 된 복원 력을 고려 합니다.

- 클러스터가 Windows Server 2019를 실행 합니다. 하거나
- 클러스터에 서버 노드가 정확히 2 개 있습니다.

### <a name="red-x-iconmedianested-resiliencyunsupportedpng-you-cant-use-nested-resiliency-if"></a>![빨간색 X 아이콘.](media/nested-resiliency/unsupported.png) 다음과 같은 경우에는 중첩 된 복원 력을 사용할 수 없습니다.

- 클러스터가 Windows Server 2016를 실행 합니다. 디스크나
- 클러스터에 서버 노드가 3 개 이상 있습니다.

## <a name="why-nested-resiliency"></a>복원 력이 중첩 된 이유

중첩 된 복원 력을 사용 하는 볼륨은 클래식 [양방향 미러링](storage-spaces-fault-tolerance.md) 복원 력과 달리 **여러 하드웨어 오류가 동시에 발생 하는 경우에도 온라인 상태를 유지 하 고 액세스할**수 있습니다. 예를 들어 두 드라이브가 동시에 실패 하거나 서버 작동이 중단 되 고 드라이브에 오류가 발생 하는 경우 중첩 된 복원 력을 사용 하는 볼륨은 온라인 상태를 유지 하 고 액세스할 수 있습니다. 하이퍼 수렴 형 인프라의 경우 앱 및 가상 컴퓨터의 작동 시간이 늘어납니다. 파일 서버 작업의 경우 사용자가 중단 없이 파일에 액세스할 수 있음을 의미 합니다.

![저장소 가용성](media/nested-resiliency/storage-availability.png)

이는 중첩 된 복원 력이 **클래식 양방향 미러링 보다 용량 효율성이 낮으므로**사용 가능한 공간을 조금 단축 한다는 것입니다. 자세한 내용은 아래의 [용량 효율성](#capacity-efficiency) 단원을 참조 하세요.

## <a name="how-it-works"></a>작동 방법

### <a name="inspiration-raid-51"></a>영감 RAID 5 + 1

RAID 5 + 1은 중첩 된 복원 력을 이해 하는 데 도움이 되는 일종의 분산 저장소 복원 력입니다. RAID 5 + 1의 각 서버 내에서 단일 드라이브의 손실을 방지 하기 위해 RAID 5 또는 *단일 패리티*에서 로컬 복원 력을 제공 합니다. 그런 다음 두 서버 간에 두 서버를 모두 손실 하지 않도록 보호 하기 위해 RAID 1 또는 *양방향 미러링의*추가 복원 력을 제공 합니다.

![RAID 5 + 1](media/nested-resiliency/raid-51.png)

### <a name="two-new-resiliency-options"></a>두 가지 새로운 복원 력 옵션

Windows Server 2019의 스토리지 공간 다이렉트에서는 특수 RAID 하드웨어 없이 소프트웨어에서 구현 된 두 가지 새로운 복원 력 옵션을 제공 합니다.

- **중첩 된 양방향 미러입니다.** 각 서버 내에서 로컬 복원 력을 양방향 미러링에 의해 제공 된 다음 두 서버 간에 양방향 미러링이 제공 됩니다. 기본적으로 각 서버에 두 개의 복사본이 있는 4 방향 미러 서버입니다. 중첩 된 양방향 미러링은 uncompromising 성능을 제공 합니다. 쓰기는 모든 복사본으로 이동 하 고 읽기는 모든 복사본에서 제공 됩니다.

  ![중첩 된 양방향 미러](media/nested-resiliency/nested-two-way-mirror.png)

- **중첩 된 미러 가속 패리티입니다.** 위에서 중첩 된 두 방향 미러링을 중첩 된 패리티와 결합 합니다. 각 서버 내에서 대부분의 데이터에 대 한 로컬 복원 력을 양방향 미러링을 사용 하는 새로운 최근 쓰기를 제외 하 고 단일 [비트 패리티 산술 연산](storage-spaces-fault-tolerance.md#parity)으로 제공 됩니다. 그런 다음 모든 데이터에 대 한 추가 복원 력을 서버 간 양방향 미러링에 의해 제공 됩니다. 미러 가속 패리티의 작동 방식에 대 한 자세한 내용은 [미러 가속 패리티](https://docs.microsoft.com/windows-server/storage/refs/mirror-accelerated-parity)를 참조 하세요.

  ![중첩 된 미러 가속 패리티](media/nested-resiliency/nested-mirror-accelerated-parity.png)

### <a name="capacity-efficiency"></a>용량 효율성

용량 효율성은 [볼륨](plan-volumes.md#choosing-the-size-of-volumes)공간에 사용 가능한 공간의 비율입니다. 복원 력으로 인 한 용량 오버 헤드를 설명 하 고 선택한 복원 력 옵션에 따라 달라 집니다. 간단한 예로, 복원 력 없이 데이터를 저장 하는 것은 100% 용량 효율적이 고 (1tb의 데이터는 1tb의 실제 저장소 용량을 차지 함), 양방향 미러링은 50% 효율적입니다 (1tb의 데이터는 1tb의 실제 저장소 용량을 차지 함).

- **중첩 양방향 미러** 는 1tb의 데이터를 저장 하는 4 tb의 복사본을 작성 합니다. 즉, 1tb의 물리적 저장소 용량이 필요 합니다. 단순성은 매우 간단 하지만 25%의 중첩 된 양방향 미러의 용량 효율성은 스토리지 공간 다이렉트의 복원 력 옵션 중 가장 낮습니다.

- **중첩 된 미러 가속 패리티** 는 약 35%-40%의 용량 효율성을 달성 합니다 .이는 각 서버의 용량 드라이브 수와 볼륨에 대해 지정 하는 미러 및 패리티의 조합에 따라 달라 집니다. 다음 표에서는 일반적인 구성에 대 한 조회를 제공 합니다.

  | 서버당 용량 드라이브 | 10% 미러 | 20% 미러 | 30% 미러 |
  |----------------------------|------------|------------|------------|
  | 4                          | 35.7%      | 34.1%      | 32.6%      |
  | 5                          | 37.7%      | 35.7%      | 33.9%      |
  | 6                          | 39.1%      | 36.8%      | 34.7%      |
  | 7 이상                         | 40.0%      | 37.5%      | 35.3%      |

  > [!NOTE]
  > **자세한 내용은 다음을 참조 하세요.** 두 서버 각각에 6 개의 용량 드라이브가 있고 10gb의 미러 및 90 GB의 패리티로 구성 된 1 100 GB 볼륨을 만들려고 한다고 가정 합니다. 서버 로컬 양방향 미러는 50.0% 효율적입니다. 즉, 10gb의 미러 데이터는 각 서버에 저장 하는 데 20gb를 사용 합니다. 두 서버에 모두 미러된 전체 공간은 40 GB입니다. 이 경우 서버 로컬 단일 패리티는 5/6 = 83.3% 효율적입니다. 즉, 90 GB의 패리티 데이터는 각 서버에 저장 하는 데 108 GB를 사용 합니다. 두 서버에 모두 미러된 전체 공간은 216 GB입니다. 전체 공간은 39.1% 전체 용량 효율성을 위해 [(10 GB/50.0% + (90 GB/83.3%] × 2 = 256 GB입니다.

클래식 양방향 미러링의 용량 효율성이 (약 50%) 확인 합니다. 및 중첩 된 미러 가속 패리티 (최대 40%) 는 크게 다르지 않습니다. 요구 사항에 따라 약간 낮은 용량의 효율성은 저장소 가용성이 크게 증가 하는 것이 좋습니다. 볼륨 당 복원 력을 선택 하므로 동일한 클러스터 내에서 중첩 된 복원 력 볼륨과 클래식 양방향 미러 볼륨을 혼합할 수 있습니다.

![균형](media/nested-resiliency/tradeoff.png)

## <a name="usage-in-powershell"></a>PowerShell에서 사용

PowerShell에서 친숙 한 저장소 cmdlet을 사용 하 여 중첩 된 복원 력이 있는 볼륨을 만들 수 있습니다.

### <a name="step-1-create-storage-tier-templates"></a>1단계: 저장소 계층 템플릿 만들기

먼저 `New-StorageTier` cmdlet을 사용 하 여 새 저장소 계층 템플릿을 만듭니다. 이 작업은 한 번만 수행 하면 되며, 새로 만드는 모든 볼륨은 이러한 템플릿을 참조할 수 있습니다. 용량 드라이브의 `-MediaType`을 지정 하 고 필요에 따라 원하는 @no__t 1을 지정 합니다. 다른 매개 변수를 수정 하지 마십시오.

용량 드라이브가 HDD (하드 디스크 드라이브) 인 경우 관리자 권한으로 PowerShell을 시작 하 고 다음을 실행 합니다.

```PowerShell 
# For mirror
New-StorageTier -StoragePoolFriendlyName S2D* -FriendlyName NestedMirror -ResiliencySettingName Mirror -MediaType HDD -NumberOfDataCopies 4

# For parity
New-StorageTier -StoragePoolFriendlyName S2D* -FriendlyName NestedParity -ResiliencySettingName Parity -MediaType HDD -NumberOfDataCopies 2 -PhysicalDiskRedundancy 1 -NumberOfGroups 1 -FaultDomainAwareness StorageScaleUnit -ColumnIsolation PhysicalDisk 
``` 

용량 드라이브가 SSD (반도체 드라이브) 인 경우 `-MediaType`을 대신 `SSD`로 설정 합니다. 다른 매개 변수를 수정 하지 마십시오.

> [!TIP]
> @No__t-0을 사용 하 여 성공적으로 만든 계층이 있는지 확인 합니다.

### <a name="step-2-create-volumes"></a>2단계: 볼륨 만들기

그런 다음 `New-Volume` cmdlet을 사용 하 여 새 볼륨을 만듭니다.

#### <a name="nested-two-way-mirror"></a>중첩 된 양방향 미러

중첩 된 양방향 미러를 사용 하려면 `NestedMirror` 계층 템플릿을 참조 하 고 크기를 지정 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

```PowerShell
New-Volume -StoragePoolFriendlyName S2D* -FriendlyName Volume01 -StorageTierFriendlyNames NestedMirror -StorageTierSizes 500GB
```

#### <a name="nested-mirror-accelerated-parity"></a>중첩 된 미러 가속 패리티

중첩 된 미러 가속 패리티를 사용 하려면 `NestedMirror` 및 `NestedParity` 계층 템플릿을 모두 참조 하 고 볼륨의 각 부분에 대해 하나씩 두 개의 크기 (미러를 먼저, 패리티 초)를 지정 합니다. 예를 들어 20% 중첩 된 양방향 미러 및 80% 중첩 된 패리티의 1 500 GB 볼륨을 만들려면 다음을 실행 합니다.

```PowerShell
New-Volume -StoragePoolFriendlyName S2D* -FriendlyName Volume02 -StorageTierFriendlyNames NestedMirror, NestedParity -StorageTierSizes 100GB, 400GB
```

### <a name="step-3-continue-in-windows-admin-center"></a>3단계: Windows 관리 센터에서 계속

중첩 된 복원 력을 사용 하는 볼륨은 아래 스크린샷에 나와 있는 것 처럼 명확 하 게 레이블 지정 된 [Windows 관리 센터](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center) 에 표시 됩니다. 만든 후에는 스토리지 공간 다이렉트의 다른 볼륨과 마찬가지로 Windows 관리 센터를 사용 하 여 관리 하 고 모니터링할 수 있습니다.

![](media/nested-resiliency/windows-admin-center.png)

### <a name="optional-extend-to-cache-drives"></a>선택 사항: 캐시 드라이브로 확장

중첩 복원 력은 기본 설정을 사용 하 여 동시에 여러 용량 드라이브의 손실을 방지 하거나 한 서버와 하나의 용량 드라이브를 동시에 보호 합니다. [캐시](understand-the-cache.md) 드라이브에 대해이 보호를 확장 하기 위해 추가 고려 사항이 있습니다. 캐시 드라이브가 *여러* 용량 드라이브에 대 한 읽기 *및 쓰기* 캐싱을 종종 제공 하기 때문에 캐시 드라이브의 손실을 허용할 수 있는 유일한 방법은 다른 서버 다운은 단순히 쓰기를 캐시 하지 않고 성능에 영향을 주는 것입니다.

이 시나리오를 해결 하기 위해 스토리지 공간 다이렉트는 두 서버 클러스터의 한 서버가 다운 된 경우 자동으로 쓰기 캐싱을 사용 하지 않도록 설정 하는 옵션을 제공 하 고 서버가 백업 된 후 쓰기 캐싱을 다시 사용 하도록 설정 합니다. 성능에 영향을 주지 않고 루틴 다시 시작을 허용 하려면 30 분 동안 서버가 중단 될 때까지 쓰기 캐싱을 사용 하지 않도록 설정 되지 않습니다. 쓰기 캐싱을 사용 하지 않도록 설정 하면 쓰기 캐시의 콘텐츠가 용량 장치에 기록 됩니다. 그런 다음 서버는 온라인 서버에서 실패 한 캐시 장치를 허용할 수 있습니다. 그러나 캐시 장치에 오류가 발생 하면 캐시에서 읽기가 지연 되거나 실패할 수 있습니다.

이 동작을 설정 하려면 (선택 사항) PowerShell을 관리자 권한으로 시작 하 고 다음을 실행 합니다.

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.NestedResiliency.DisableWriteCacheOnNodeDown.Enabled" -Value "True"
```

**True**로 설정 되 면 캐시 동작은 다음과 같습니다.

| 적합                       | 캐시 동작                           | 캐시 드라이브 손실을 허용할 수 있나요? |
|---------------------------------|------------------------------------------|--------------------------------|
| 두 서버 모두                 | 캐시 읽기 및 쓰기, 전체 성능 | 예                            |
| 서버 작동 중단, 처음 30 분   | 캐시 읽기 및 쓰기, 전체 성능 | 아니요 (일시적)               |
| 처음 30 분 후          | 캐시 읽기 전용, 성능 영향을 받음   | 예 (용량 드라이브에 캐시를 기록한 후)                           |

## <a name="frequently-asked-questions"></a>질문과 대답

### <a name="can-i-convert-an-existing-volume-between-two-way-mirror-and-nested-resiliency"></a>기존 볼륨을 양방향 미러와 중첩 된 복원 력 간에 변환할 수 있나요?

아니요, 복원 력 유형 간에는 볼륨을 변환할 수 없습니다. Windows Server 2019에 새로 배포 하는 경우 요구 사항에 가장 적합 한 복원 력 유형을 미리 결정 합니다. Windows Server 2016에서 업그레이드 하는 경우에는 중첩 된 복원 력을 사용 하 여 새 볼륨을 만들고, 데이터를 마이그레이션한 후 이전 볼륨을 삭제할 수 있습니다.

### <a name="can-i-use-nested-resiliency-with-multiple-types-of-capacity-drives"></a>여러 유형의 용량 드라이브로 중첩 된 복원 력을 사용할 수 있나요?

예, 위의 [1 단계](#step-1-create-storage-tier-templates) 에서 각 계층의 `-MediaType`을 적절 하 게 지정 하면 됩니다. 예를 들어 동일한 클러스터에서 NVMe, SSD 및 HDD를 사용 하는 경우 NVMe는 캐시를 제공 하 고, 두 번째는 용량을 제공 하는 반면, `NestedMirror` 계층을 `-MediaType SSD`로 설정 하 고 `NestedParity` 계층을 `-MediaType HDD`으로 설정 합니다. 이 경우 패리티 용량 효율성은 HDD 드라이브의 수에만 의존 하므로 서버당 4 개 이상이 필요 합니다.

### <a name="can-i-use-nested-resiliency-with-3-or-more-servers"></a>3 개 이상의 서버에서 중첩 된 복원 력을 사용할 수 있나요?

아니요, 클러스터에 정확히 2 개의 서버가 있는 경우에만 중첩 된 복원 력을 사용 합니다.

### <a name="how-many-drives-do-i-need-to-use-nested-resiliency"></a>중첩 된 복원 력을 사용 해야 하는 드라이브는 몇 개입니까?

스토리지 공간 다이렉트 하는 데 필요한 최소 드라이브 수는 서버 노드당 4 개의 용량 드라이브, 서버 노드당 2 개의 캐시 드라이브 (있는 경우)입니다. 이는 Windows Server 2016에서 변경 되지 않았습니다. 중첩 된 복원 력을 위한 추가 요구 사항은 없으며, 예약 용량의 권장 사항도 변경 되지 않습니다.

### <a name="does-nested-resiliency-change-how-drive-replacement-works"></a>중첩 된 복원 력이 드라이브 교체의 작동 방식을 변경 하나요?

아니요.

### <a name="does-nested-resiliency-change-how-server-node-replacement-works"></a>중첩 된 복원 력이 서버 노드 교체의 작동 방식을 변경 하나요?

아니요. 서버 노드와 해당 드라이브를 교체 하려면 다음 순서를 따르세요.

1. 보내는 서버에서 드라이브 사용 중지
2. 새 서버와 해당 드라이브를 클러스터에 추가 합니다.
3. 저장소 풀의 균형을 다시 조정 합니다.
4. 보내는 서버 및 해당 드라이브 제거

자세한 내용은 [서버 제거](remove-servers.md) 항목을 참조 하세요.

## <a name="see-also"></a>참조

- [스토리지 공간 다이렉트 개요](storage-spaces-direct-overview.md)
- [스토리지 공간 다이렉트의 내결함성을 이해 합니다.](storage-spaces-fault-tolerance.md)
- [스토리지 공간 다이렉트에서 볼륨 계획](plan-volumes.md)
- [스토리지 공간 다이렉트에서 볼륨 만들기](create-volumes.md)
