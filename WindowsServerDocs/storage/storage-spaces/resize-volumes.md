---
title: 스토리지 공간 다이렉트에서 볼륨 확장
description: Windows 관리 센터 및 PowerShell을 사용 하 여 스토리지 공간 다이렉트 볼륨의 크기를 조정 하는 방법입니다.
ms.prod: windows-server
ms.reviewer: cosmosdarwin
author: cosmosdarwin
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.date: 03/10/2020
ms.openlocfilehash: 4526bdc87bfbb8cdaf6cc3b0e8f3cd1cd80f4a9d
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474610"
---
# <a name="extending-volumes-in-storage-spaces-direct"></a>스토리지 공간 다이렉트에서 볼륨 확장
> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 Windows 관리 센터를 사용 하 여 [스토리지 공간 다이렉트](storage-spaces-direct-overview.md) 클러스터의 볼륨 크기를 조정 하는 지침을 제공 합니다.

> [!WARNING]
> **지원 되지 않음: 스토리지 공간 다이렉트에서 사용 하는 기본 저장소의 크기를 조정 합니다.** Azure에서를 포함 하 여 가상화 된 저장소 환경에서 스토리지 공간 다이렉트를 실행 하는 경우 가상 컴퓨터에 사용 되는 저장 장치의 특성 크기 조정 또는 변경이 지원 되지 않으며 데이터에 액세스할 수 없게 됩니다. 대신, [서버 또는 드라이브 추가](add-nodes.md) 섹션의 지침에 따라 볼륨을 확장 하기 전에 용량을 더 추가 합니다.

볼륨 크기를 조정 하는 방법에 대 한 빠른 비디오를 시청 하세요.

> [!VIDEO https://www.youtube-nocookie.com/embed/hqyBzipBoTI]

## <a name="extending-volumes-using-windows-admin-center"></a>Windows 관리 센터를 사용 하 여 볼륨 확장

1. Windows 관리 센터에서 스토리지 공간 다이렉트 클러스터에 연결한 다음 **도구** 창에서 **볼륨** 을 선택 합니다.
2. 볼륨 페이지에서 **인벤토리** 탭을 선택한 후 크기를 조정 하려는 볼륨을 선택 합니다.

    볼륨 세부 정보 페이지에서 볼륨의 저장소 용량이 표시 됩니다. 대시보드에서 직접 볼륨 세부 정보 페이지를 열 수도 있습니다. 대시보드의 경고 창에서 볼륨의 저장소 용량이 부족 한 경우이를 알리는 경고를 선택 하 고 **볼륨으로 이동**을 선택 합니다.

4. 볼륨 세부 정보 페이지의 위쪽에서 **크기 조정**을 선택 합니다.
5. 더 큰 크기를 새로 입력 하 고 크기 **조정**을 선택 합니다.

    볼륨 세부 정보 페이지에는 볼륨에 대 한 더 큰 저장소 용량이 표시 되 고 대시보드의 경고는 지워집니다.

## <a name="extending-volumes-using-powershell"></a>PowerShell을 사용 하 여 볼륨 확장

### <a name="capacity-in-the-storage-pool"></a>저장소 풀의 용량

볼륨의 크기를 조정 하기 전에 저장소 풀에 용량이 충분 한지 확인 해야 합니다. 예를 들어, 3 방향 미러 볼륨의 크기를 1tb에서 2tb로 조정 하는 경우 해당 사용 공간은 3TB에서 6tb까지 증가 합니다. 크기 조정에 성공 하려면 저장소 풀에서 최소 (6-3) = 3TB의 사용 가능한 용량이 필요 합니다.

### <a name="familiarity-with-volumes-in-storage-spaces"></a>저장소 공간에서 볼륨에 대해 잘 알고 있어야 합니다.

스토리지 공간 다이렉트에서 모든 볼륨은 볼륨 인 CSV (클러스터 공유 볼륨)와 같은 누적 개체로 구성 됩니다. 파티션 디스크는 가상 디스크입니다. 하나 이상의 저장소 계층 (해당 하는 경우). 볼륨의 크기를 조정 하려면 이러한 개체의 크기를 조정 해야 합니다.

![smapi 볼륨](media/resize-volumes/volumes-in-smapi.png)

해당 명사를 숙지 하려면 PowerShell에서 해당 명사를 사용 하 여 **Get** 을 실행 해 보세요.

예를 들면 다음과 같습니다.

```PowerShell
Get-VirtualDisk
```

스택의 개체 간 연결을 따르려면 하나의 **Get** cmdlet을 다음으로 파이프 합니다.

예를 들어 가상 디스크에서 볼륨으로 가져오는 방법은 다음과 같습니다.

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-Disk | Get-Partition | Get-Volume
```

### <a name="step-1--resize-the-virtual-disk"></a>1 단계-가상 디스크 크기 조정

가상 디스크는 생성 된 방법에 따라 저장소 계층을 사용할 수 있습니다.

확인 하려면 다음 cmdlet을 실행 합니다.

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-StorageTier
```

Cmdlet에서 아무 것도 반환 하지 않으면 가상 디스크에서 저장소 계층을 사용 하지 않습니다.

#### <a name="no-storage-tiers"></a>저장소 계층 없음

가상 디스크에 저장소 계층이 없으면 **VirtualDisk** cmdlet을 사용 하 여 직접 크기를 조정할 수 있습니다.

**-Size** 매개 변수에 새 크기를 제공 합니다.

```PowerShell
Get-VirtualDisk <FriendlyName> | Resize-VirtualDisk -Size <Size>
```

**VirtualDisk**크기를 조정 하면 **디스크가** 자동으로 따르며 크기가 조정 됩니다.

![크기 조정-VirtualDisk](media/resize-volumes/Resize-VirtualDisk.gif)

#### <a name="with-storage-tiers"></a>저장소 계층 사용

가상 디스크에서 저장소 계층을 사용 하는 경우 **크기 조정-StorageTier** cmdlet을 사용 하 여 각 계층의 크기를 별도로 조정할 수 있습니다.

가상 디스크의 연결을 따라 저장소 계층의 이름을 가져옵니다.

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-StorageTier | Select FriendlyName
```

그런 다음 각 계층에 대해 **-size** 매개 변수에 새 크기를 제공 합니다.

```PowerShell
Get-StorageTier <FriendlyName> | Resize-StorageTier -Size <Size>
```

> [!TIP]
> 계층이 다른 물리적 미디어 유형 (예: **mediatype = SSD** 및 **mediatype = HDD**) 인 경우 각 계층의 더 큰 새로운 공간을 수용할 수 있도록 저장소 풀에 각 미디어 유형의 용량이 충분 한지 확인 해야 합니다.

**Storagetier**크기를 조정 하면 **VirtualDisk** 및 **디스크가** 자동으로 이동 하 여 크기가 조정 됩니다.

![Resize-StorageTier](media/resize-volumes/Resize-StorageTier.gif)

### <a name="step-2--resize-the-partition"></a>2 단계 – 파티션 크기 조정

그런 다음, 파티션 **크기 조정** cmdlet을 사용 하 여 파티션 크기를 조정 합니다. 가상 디스크에는 두 개의 파티션이 있어야 합니다. 첫 번째는 예약 되어 있으므로 수정 하면 안 됩니다. 크기를 조정 하는 데 필요한 항목 **번호는 2** 이며 **유형 = Basic**입니다.

**-Size** 매개 변수에 새 크기를 제공 합니다. 아래와 같이 지원 되는 최대 크기를 사용 하는 것이 좋습니다.

```PowerShell
# Choose virtual disk
$VirtualDisk = Get-VirtualDisk <FriendlyName>

# Get its partition
$Partition = $VirtualDisk | Get-Disk | Get-Partition | Where PartitionNumber -Eq 2

# Resize to its maximum supported size
$Partition | Resize-Partition -Size ($Partition | Get-PartitionSupportedSize).SizeMax
```

**파티션**크기를 조정 하면 **볼륨** 및 **clustersharedvolume** 이 자동으로 이동 하 여 크기가 조정 됩니다.

![파티션 크기 조정](media/resize-volumes/Resize-Partition.gif)

이것으로 끝입니다.

> [!TIP]
> 볼륨이 **Get 볼륨**을 실행 하 여 새 크기 인지 확인할 수 있습니다.

## <a name="additional-references"></a>추가 참조

- [Windows Server 2016의 스토리지 공간 다이렉트](storage-spaces-direct-overview.md)
- [스토리지 공간 다이렉트에서 볼륨 계획](plan-volumes.md)
- [스토리지 공간 다이렉트에서 볼륨 만들기](create-volumes.md)
- [스토리지 공간 다이렉트 볼륨 삭제](delete-volumes.md)
