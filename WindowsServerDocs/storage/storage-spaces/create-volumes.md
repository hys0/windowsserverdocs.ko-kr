---
ms.assetid: a9f229eb-bef4-4231-97d0-0899e17cef32
title: 저장소 공간 다이렉트에서 볼륨 만들기
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 01/11/2017
ms.localizationpriority: medium
ms.openlocfilehash: 277a676d8e53a7847d54039aab6607be8e5a78c5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823614"
---
# <a name="creating-volumes-in-storage-spaces-direct"></a>저장소 공간 다이렉트에서 볼륨 만들기

>적용 대상: Windows Server 2016

이 항목에서는 PowerShell 또는 장애 조치(failover) 클러스터 관리자를 사용하여 저장소 공간 다이렉트에서 볼륨을 만드는 방법을 설명합니다.

   >[!TIP]
   >  아직 확인하지 않은 경우 [저장소 공간 다이렉트에서 볼륨 계획](plan-volumes.md)을 먼저 확인하세요.

## <a name="create-volumes-using-powershell"></a>PowerShell을 사용하여 볼륨 만들기

**New-Volume** cmdlet을 사용하여 저장소 공간 다이렉트용 볼륨을 만드는 것이 좋습니다. 가장 빠르고 간단한 환경을 제공합니다. 이 단일 cmdlet은 가상 디스크를 자동으로 만들어서 분할 및 포맷하고, 이와 일치하는 이름으로 볼륨을 만들어 클러스터 공유 볼륨에 추가합니다. 이 모든 과정이 하나의 간편한 단계만으로 진행됩니다.

**New-Volume** cmdlet에는 사용자가 항상 제공해야 할 네 가지 매개 변수가 있습니다.

- **FriendlyName:** 예를 들어 원하는 모든 문자열 *"Volume1"*
- **FileSystem:** 어느 **CSVFS_ReFS** (권장) 또는 **CSVFS_NTFS**
- **StoragePoolFriendlyName:** 예를 들어 사용자의 저장소 이름 풀 *"S2D에서 ClusterName"*
- **크기:** 예를 들어 볼륨의 크기 *"10TB"*

   >[!NOTE]
   >  PowerShell을 비롯한 Windows는 2진수(밑 2)를 사용하여 계산되지만 드라이브는 대개 10진수(밑 10)를 사용하여 레이블이 지정됩니다. 따라서 1,000,000,000,000바이트로 정의되는 "테라바이트" 드라이브는 Windows에서 약 "909GB"로 나타납니다. 이는 예정된 동작입니다. **New-Volume**을 사용하여 볼륨을 만들 때 **Size** 매개 변수를 이진수(밑2)로 지정해야 합니다. 예를 들어, "909GB" 또는 "0.909495TB"로 지정하면 약 1,000,000,000,000바이트의 볼륨이 생성됩니다.

### <a name="example-with-2-or-3-servers"></a>예: 2 또는 3 개의 서버를 사용 하 여

두 개의 서버에만 배포하는 경우 작업을 쉽게 하기 위해 저장소 공간 다이렉트는 복원력을 위해 양방향 미러링을 자동 사용합니다. 세 개의 서버에만 배포하는 경우에는 3방향 미러링을 자동 사용합니다.

```
New-Volume -FriendlyName "Volume1" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB
```

### <a name="example-with-4-servers"></a>예: 4 + 서버를 사용 하 여

4개 이상의 서버가 있는 경우 **ResiliencySettingName** 매개 변수를 복구 유형을 선택적으로 사용하여 복원력 유형을 선택합니다.

-   **ResiliencySettingName:** 어느 **미러** 하거나 **패리티**합니다.

다음 예제에서 *"Volume2"* 는 3방향 미러링을 사용하며 *"Volume3"* 는 이중 패리티("삭제 코딩"(erasure coding)이라고도 함)를 사용합니다.

```
New-Volume -FriendlyName "Volume2" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Mirror
New-Volume -FriendlyName "Volume3" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Parity
```

### <a name="example-using-storage-tiers"></a>예: 저장소 계층을 사용 하 여

세 가지 유형의 드라이브를 통한 배포에서 하나의 볼륨은 SSD 및 HDD 계층에 걸쳐 확장되어 각 부분에 부분적으로 상주할 수 있습니다. 마찬가지로, 4개 이상의 서버를 통한 배포에서 하나의 볼륨은 미러링과 이중 패리티를 혼합하여 각 부분에 부분적으로 상주할 수 있습니다.

이러한 볼륨을 쉽게 만들 수 있도록 저장소 공간 다이렉트는 *성능* 및 *용량*이라는 기본 계층 템플릿을 제공합니다. 이러한 템플릿에는 보다 빠른 용량 드라이브(해당하는 경우)에서의 3방향 미러링 및 느린 용량 드라이브에서의 이중 패리티(해당하는 경우)에 대한 정의가 캡슐화됩니다.

**Get-StorageTier** cmdlet을 실행하여 확인할 수 있습니다.

```
Get-StorageTier | Select FriendlyName, ResiliencySettingName, PhysicalDiskRedundancy
```

![저장소 계층 PowerShell 스크린샷](media/creating-volumes/storage-tiers-screenshot.png)

계층화된 볼륨을 만들려면 **New-Volume** cmdlet의 **StorageTierFriendlyNames** 및 **StorageTierSizes** 매개 변수를 사용하여 이러한 계층 템플릿을 참조하세요. 예를 들어 다음 cmdlet은 3방향 미러링과 30:70 비율의 이중 패리티를 혼합하는 하나의 볼륨을 만듭니다.

```
New-Volume -FriendlyName "Volume4" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -StorageTierFriendlyNames Performance, Capacity -StorageTierSizes 300GB, 700GB
```

## <a name="create-volumes-using-failover-cluster-manager"></a>장애 조치(failover) 클러스터 관리자를 사용하여 볼륨 만들기

장애 조치(failover) 클러스터 관리자의 *새 가상 디스크 마법사(저장소 공간 다이렉트)* 와 *새 볼륨 마법사*를 차례로 사용하여 볼륨을 만들 수도 있습니다. 이 워크플로에는 훨씬 많은 수동 단계가 있으며 권장되지 않습니다.

다음과 같은 세 가지 주요 단계가 있습니다.

### <a name="step-1-create-virtual-disk"></a>1단계: 가상 디스크 만들기

![새 가상 디스크](media/creating-volumes/GUI-Step-1.png)

1. 장애 조치(failover) 클러스터 관리자에서 **저장소** -> **풀**로 이동합니다.
2. 오른쪽 작업 창에서 **새 가상 디스크**를 선택하거나 풀을 마우스 오른쪽 단추로 클릭하고 **새 가상 디스크**를 선택합니다.
3. 저장소 풀을 선택하고 **확인**을 클릭합니다. *새 가상 디스크 마법사(저장소 공간 다이렉트)* 가 열립니다.
4. 마법사를 사용하여 가상 디스크 이름을 정하고 크기를 지정합니다.
5. 선택한 내용을 검토하고 **만들기**를 클릭합니다.
6. 닫기 전에 **이 마법사를 닫으면 볼륨 만들기** 확인란이 선택되어 있는지 확인합니다.

### <a name="step-2-create-volume"></a>2단계: 볼륨 만들기

*새 볼륨 마법사*가 열립니다.

7. 방금 만든 가상 디스크를 선택하고 **다음**을 클릭합니다.
8. 볼륨의 크기(기본값: 가상 디스크와 같은 크기)를 지정하고 **다음**을 클릭합니다. 
9. 볼륨에 드라이브 문자를 할당하거나 **드라이브 문자에 할당 안 함**을 선택하고 **다음**을 클릭합니다.
10. 사용할 파일 시스템을 지정하고 할당 단위 크기를 *기본값*으로 둔 다음 볼륨 이름을 정하고 **다음**을 클릭합니다.
11. 선택한 내용을 검토하고 **만들기**를 클릭한 다음 **닫기**를 클릭합니다.

### <a name="step-3-add-to-cluster-shared-volumes"></a>3단계: 클러스터 공유 볼륨에 추가

![클러스터 공유 볼륨에 추가](media/creating-volumes/GUI-Step-2.png)

12. 장애 조치(failover) 클러스터 관리자에서 **저장소** -> **디스크**로 이동합니다.
13. 방금 만든 가상 디스크를 선택하고 오른쪽 작업 창에서 **클러스터 공유 볼륨에 추가**를 선택하거나 가상 디스크를 마우스 오른쪽 단추로 클릭하고 **클러스터 공유 볼륨에 추가**를 선택합니다.

모든 작업이 끝났습니다. 필요에 따라 반복하여 두 개 이상의 볼륨을 만듭니다.

## <a name="see-also"></a>참조

- [저장소 공간 다이렉트 개요](storage-spaces-direct-overview.md)
- [저장소 공간 다이렉트 볼륨 계획](plan-volumes.md)
