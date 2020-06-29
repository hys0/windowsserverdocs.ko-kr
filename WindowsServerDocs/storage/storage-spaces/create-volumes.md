---
title: 스토리지 공간 다이렉트에서 볼륨 만들기
description: Windows 관리 센터 및 PowerShell을 사용 하 여 스토리지 공간 다이렉트에서 볼륨을 만드는 방법
ms.prod: windows-server
ms.reviewer: cosmosdarwin
author: cosmosdarwin
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.date: 02/25/2020
ms.openlocfilehash: 40750acb260335e858a7763c950dfc4ad2cd7979
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473830"
---
# <a name="creating-volumes-in-storage-spaces-direct"></a>스토리지 공간 다이렉트에서 볼륨 만들기

> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 Windows 관리 센터 및 PowerShell을 사용 하 여 스토리지 공간 다이렉트 클러스터에서 볼륨을 만드는 방법에 대해 설명 합니다.

> [!TIP]
> 아직 스토리지 공간 다이렉트 하지 않은 경우 먼저 [계획 볼륨](plan-volumes.md) 을 확인 하세요.

## <a name="create-a-three-way-mirror-volume"></a>3 방향 미러 볼륨 만들기

Windows 관리 센터에서 3 방향 미러 볼륨을 만들려면 다음을 수행 합니다.

1. Windows 관리 센터에서 스토리지 공간 다이렉트 클러스터에 연결한 다음 **도구** 창에서 **볼륨** 을 선택 합니다.
2. 볼륨 페이지에서 **인벤토리** 탭을 선택한 후 **볼륨 만들기**를 선택 합니다.
3. **볼륨 만들기** 창에서 볼륨의 이름을 입력 하 고 **복원 력을** **3 방향 미러**로 유지 합니다.
4. **HDD의 크기**에서 볼륨의 크기를 지정 합니다. 예: 5TB (테라바이트).
5. **만들기**를 선택합니다.

크기에 따라 볼륨을 만드는 데 몇 분 정도 걸릴 수 있습니다. 오른쪽 위에 있는 알림은 볼륨 생성 시기를 알려 주는 데 사용 됩니다. 새 볼륨이 인벤토리 목록에 표시 됩니다.

3 방향 미러 볼륨을 만드는 방법에 대 한 빠른 비디오를 시청 하세요.

> [!VIDEO https://www.youtube-nocookie.com/embed/o66etKq70N8]

## <a name="create-a-mirror-accelerated-parity-volume"></a>미러 가속 패리티 볼륨 만들기

미러 가속 패리티는 HDD의 볼륨 공간을 줄입니다. 예를 들어, 3 방향 미러 볼륨은 10tb의 크기 마다 30tb의 공간이 필요 하다는 것을 의미 합니다. 공간에서 오버 헤드를 줄이려면 미러 가속 패리티를 사용 하 여 볼륨을 만듭니다. 이렇게 하면 최대 20%의 데이터를 미러링 하 고 나머지를 저장 하는 데 더 많은 공간을 사용 하는 패리티를 사용 하 여 서버를 4 개만 사용 하더라도 30tb에서 22 tb 까지의 공간을 줄일 수 있습니다. 이러한 패리티와 미러 비율을 조정 하 여 워크 로드에 적합 한 성능 및 용량 균형을 유지할 수 있습니다. 예를 들어, 90% 패리티와 10%의 미러를 사용 하면 성능이 저하 되지만 더 많은 공간을 효율적으로 사용할 수도 있습니다.

Windows 관리 센터에서 미러 가속 패리티를 사용 하는 볼륨을 만들려면 다음을 수행 합니다.

1. Windows 관리 센터에서 스토리지 공간 다이렉트 클러스터에 연결한 다음 **도구** 창에서 **볼륨** 을 선택 합니다.
2. 볼륨 페이지에서 **인벤토리** 탭을 선택한 후 **볼륨 만들기**를 선택 합니다.
3. **볼륨 만들기** 창에서 볼륨의 이름을 입력 합니다.
4. **복원 력**에서 **미러 가속 패리티**를 선택 합니다.
5. 패리티 **백분율**에서 패리티의 백분율을 선택 합니다.
6. **만들기**를 선택합니다.

미러 가속 패리티 볼륨을 만드는 방법에 대 한 빠른 비디오를 시청 하세요.

> [!VIDEO https://www.youtube-nocookie.com/embed/R72QHudqWpE]

## <a name="open-volume-and-add-files"></a>볼륨을 열고 파일 추가

Windows 관리 센터에서 볼륨을 열고 볼륨에 파일을 추가 하려면 다음을 수행 합니다.

1. Windows 관리 센터에서 스토리지 공간 다이렉트 클러스터에 연결한 다음 **도구** 창에서 **볼륨** 을 선택 합니다.
2. 볼륨 페이지에서 **인벤토리** 탭을 선택 합니다.
2. 볼륨 목록에서 열려는 볼륨의 이름을 선택 합니다.

    볼륨 세부 정보 페이지에서 볼륨의 경로를 볼 수 있습니다.

4. 페이지 위쪽에서 **열기**를 선택 합니다. 그러면 Windows 관리 센터에서 파일 도구가 시작 됩니다.
5. 볼륨의 경로로 이동 합니다. 여기서 볼륨의 파일을 찾아볼 수 있습니다.
6. **업로드**를 선택한 다음 업로드할 파일을 선택 합니다.
7. 브라우저 **뒤로** 단추를 사용 하 여 Windows 관리 센터의 도구 창으로 돌아갑니다.

볼륨을 열고 파일을 추가 하는 방법에 대 한 빠른 비디오를 시청 하세요.

> [!VIDEO https://www.youtube-nocookie.com/embed/j59z7ulohs4]

## <a name="turn-on-deduplication-and-compression"></a>중복 제거 및 압축 설정

중복 제거 및 압축은 볼륨 별로 관리 됩니다. 중복 제거 및 압축은 사후 처리 모델을 사용 합니다. 즉, 실행이 완료 될 때까지 절감 효과가 표시 되지 않습니다. 이렇게 하면 이전에 있던 파일을 비롯 하 여 모든 파일에 대해 작동 합니다.

1. Windows 관리 센터에서 스토리지 공간 다이렉트 클러스터에 연결한 다음 **도구** 창에서 **볼륨** 을 선택 합니다.
2. 볼륨 페이지에서 **인벤토리** 탭을 선택 합니다.
3. 볼륨 목록에서 관리 하려는 볼륨의 이름을 선택 합니다.
4. 볼륨 세부 정보 페이지에서 **중복 제거 및 압축**이라는 레이블이 지정 된 스위치를 클릭 합니다.
5. 중복 제거 사용 창에서 중복 제거 모드를 선택 합니다.

    Windows 관리 센터에서는 복잡 한 설정 대신 다른 워크 로드에 대해 준비 된 프로필을 선택할 수 있습니다. 확실 하지 않은 경우 기본 설정을 사용 합니다.

6. **사용**을 선택합니다.

중복 제거 및 압축을 켜는 방법에 대 한 빠른 비디오를 시청 하세요.

> [!VIDEO https://www.youtube-nocookie.com/embed/PRibTacyKko]

## <a name="create-volumes-using-powershell"></a>PowerShell을 사용 하 여 볼륨 만들기

스토리지 공간 다이렉트에 대 한 볼륨을 만들려면 **새 볼륨** cmdlet을 사용 하는 것이 좋습니다. 가장 빠르고 간단한 환경을 제공 합니다. 이 단일 cmdlet은 가상 디스크를 자동으로 만들고, 파티션을 만들고 포맷 하며, 이름이 일치 하는 볼륨을 만들고 클러스터 공유 볼륨에 추가 합니다. 전체를 한 번의 단계로 수행할 수 있습니다.

**새 볼륨** cmdlet에는 항상 제공 해야 하는 4 개의 매개 변수가 있습니다.

- **FriendlyName:** 원하는 모든 문자열 (예: *"Volume1"* )
- **파일 시스템:** **CSVFS_ReFS** (권장) 또는 **CSVFS_NTFS**
- **Storagepoolfriendlyname:** 저장소 풀의 이름 (예: *"S2D On ClusterName")*
- **크기:** 볼륨의 크기 (예: *"10Tb")*

   > [!NOTE]
   > PowerShell을 포함 한 Windows는 이진 (밑 2) 숫자를 사용 하 여 계산 하는 반면 드라이브는 종종 10 진수 (밑수 10)를 사용 하 여 지정 됩니다. 이는 1조 바이트로 정의 된 "1 테라바이트" 드라이브가 Windows에 "909 GB"로 표시 되는 이유를 설명 합니다. 예상된 동작입니다. **새 볼륨**을 사용 하 여 볼륨을 만들 때는 **Size** 매개 변수를 이진 (밑수 2) 숫자에 지정 해야 합니다. 예를 들어 "909GB" 또는 "0.909495 TB"를 지정 하면 약 1조 바이트의 볼륨이 만들어집니다.

### <a name="example-with-2-or-3-servers"></a>예: 2 개 또는 3 대 서버

작업을 더 쉽게 수행 하기 위해 배포에 서버가 두 개만 있는 경우 스토리지 공간 다이렉트는 복원 력을 위해 양방향 미러링을 자동으로 사용 합니다. 배포에 서버가 3 개만 있으면 3 방향 미러링이 자동으로 사용 됩니다.

```PowerShell
New-Volume -FriendlyName "Volume1" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB
```

### <a name="example-with-4-servers"></a>예: 4 + 서버 사용

서버를 4 개 이상 사용 하는 경우 선택적 **ResiliencySettingName** 매개 변수를 사용 하 여 복원 력 유형을 선택할 수 있습니다.

-   **ResiliencySettingName:** **미러** 또는 **패리티**중 하나입니다.

다음 예제에서 *"Volume2"* 는 3 방향 미러링을 사용 하 고 *"Volume3"* 는 이중 패리티 (종종 "지우기 코딩" 이라고 함)를 사용 합니다.

```PowerShell
New-Volume -FriendlyName "Volume2" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Mirror
New-Volume -FriendlyName "Volume3" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Parity
```

### <a name="example-using-storage-tiers"></a>예: 저장소 계층 사용

3 가지 유형의 드라이브가 있는 배포에서는 한 볼륨이 SSD 및 HDD 계층에 부분적으로 걸쳐 배치 될 수 있습니다. 마찬가지로, 4 개 이상의 서버를 포함 하는 배포에서 한 볼륨이 미러링 및 이중 패리티를 혼합 하 여 각각에 부분적으로 배치할 수 있습니다.

이러한 볼륨을 만들 수 있도록 스토리지 공간 다이렉트는 *성능* 및 *용량*이라는 기본 계층 템플릿을 제공 합니다. 더 빠른 용량 드라이브 (해당 하는 경우)에 대 한 3 방향 미러링의 정의와 더 느린 용량 드라이브 (해당 하는 경우)에 대 한 이중 패리티를 캡슐화 합니다.

이러한 항목은 **Get StorageTier** cmdlet을 실행 하 여 확인할 수 있습니다.

```PowerShell
Get-StorageTier | Select FriendlyName, ResiliencySettingName, PhysicalDiskRedundancy
```

![저장소 계층 PowerShell 스크린샷](media/creating-volumes/storage-tiers-screenshot.png)

계층화 된 볼륨을 만들려면 **새 볼륨** Cmdlet의 **StorageTierFriendlyNames** 및 **StorageTierSizes** 매개 변수를 사용 하 여 이러한 계층 템플릿을 참조 합니다. 예를 들어 다음 cmdlet은 3 방향 미러링과 이중 패리티를 30:70 비율로 혼합 하는 볼륨 하나를 만듭니다.

```PowerShell
New-Volume -FriendlyName "Volume4" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -StorageTierFriendlyNames Performance, Capacity -StorageTierSizes 300GB, 700GB
```

작업을 완료했습니다. 필요에 따라 반복 하 여 둘 이상의 볼륨을 만듭니다.

## <a name="additional-references"></a>추가 참조

- [스토리지 공간 다이렉트 개요](storage-spaces-direct-overview.md)
- [스토리지 공간 다이렉트에서 볼륨 계획](plan-volumes.md)
- [스토리지 공간 다이렉트에서 볼륨 확장](resize-volumes.md)
- [스토리지 공간 다이렉트 볼륨 삭제](delete-volumes.md)
