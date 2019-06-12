---
title: 독립 실행형 서버에서 저장소 공간 배포
description: 독립 실행형 Windows Server 2012 기반 서버에서 저장소 공간을 배포 하는 방법에 설명 합니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-spaces
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: f9b5d2b0d5acfcbde52131c29704e38d835d048e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447555"
---
# <a name="deploy-storage-spaces-on-a-stand-alone-server"></a>독립 실행형 서버에서 저장소 공간 배포

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 독립 실행형 서버에서 저장소 공간을 배포 하는 방법을 설명 합니다. 클러스터 된 저장소 공간을 만드는 방법에 대 한 자세한 내용은 [Windows Server 2012 R2에서 저장소 공간 클러스터를 배포할](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/mt270997(v%3dws.11)>)합니다.

저장소 공간을 만들려면 먼저 하나 이상의 저장소 풀을 만들어야 합니다. 저장소 풀은 실제 디스크의 모음입니다. 저장소 풀은 저장소 집계, 탄력적 용량 확장 및 위임된 관리를 지원합니다.

저장소 풀에서 하나 이상의 가상 디스크를 만들 수 있습니다. 이러한 가상 디스크를 *저장소 공간*이라고도 합니다. 저장소 공간은 Windows 운영 체제에 포맷된 볼륨을 만들 수 있는 일반 디스크로 표시됩니다. 파일 및 저장소 서비스 사용자 인터페이스를 통해 가상 디스크를 만드는 경우 복원 유형(단순, 미러 또는 패리티), 프로비저닝 유형(씬 또는 고정) 및 크기를 구성할 수 있습니다. Windows PowerShell을 통해서는 열 수, 인터리빙 값 및 사용할 풀의 실제 디스크와 같은 추가 매개 변수를 설정할 수 있습니다. 이러한 추가 매개 변수에 대한 자세한 내용은 저장소 공간 FAQ(질문과 대답)에서 [New-VirtualDisk](https://docs.microsoft.com/powershell/module/storage/new-virtualdisk?view=win10-ps) 및 [열 정의 및 저장소 공간에서 사용할 개수를 결정하는 방법](https://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx%23what_are_columns_and_how_does_storage_spaces_decide_how_many_to_use)을 참조하세요.

>[!NOTE]
>Windows 운영 체제를 호스트 하는 저장소 공간을 사용할 수 없습니다.

가상 디스크에서 하나 이상의 볼륨을 만들 수 있습니다. 볼륨을 만들면 크기, 드라이브 문자 또는 폴더, 파일 시스템 (NTFS 파일 시스템 또는 ReFS (복원 파일 시스템)), 할당 단위 크기 및 선택적 볼륨 레이블을 구성할 수 있습니다.

다음 그림에서는 저장소 공간 워크플로를 보여 줍니다.

![저장소 공간 워크플로](media/deploy-standalone-storage-spaces/storage-spaces-workflow.png)

**그림 1: 저장소 공간 워크플로**

>[!NOTE]
>이 항목에는 설명한 절차의 일부를 자동화하는 데 사용할 수 있는 샘플 Windows PowerShell cmdlet이 포함되어 있습니다. 자세한 내용은 [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting?view=powershell-6)합니다.

## <a name="prerequisites"></a>사전 요구 사항

저장소 공간에서 독립 실행형 Windows Server 2012−based 서버를 사용 하는 데 사용할 실제 디스크가 다음 필수 조건을 충족 하는지 확인 합니다.

> [!IMPORTANT]
> 내용은 장애 조치 클러스터에서 저장소 공간을 배포 하는 방법을 알아보려면 싶다면 [Windows Server 2012 R2에서 저장소 공간 클러스터를 배포할](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/mt270997(v%3dws.11)>)합니다. 장애 조치 클러스터 배포에 필요한 최소 디스크 수가 지원 되는 디스크 버스 유형, 지원 되는 복원 력 유형을 등 다양 한 필수 조건

|영역|요구 사항|참고|
|---|---|---|
|디스크 버스 유형|-Serial Attached SCSI (SAS)<br>직렬 Advanced Technology Attachment SATA)<br>-iSCSI 및 파이버 채널 컨트롤러입니다. |USB 드라이브를 사용할 수도 있습니다. 그러나 서버 환경에서 USB 드라이브를 사용 하는 데 가장 적합 한 아닙니다.<br>저장소 공간을 기반으로 만든 가상 디스크는 복원 되지 않은 (임의 개수의 열을 사용 하 여 단순)으로 iSCSI 및 FC (파이버 채널) 컨트롤러에서 지원 됩니다.<br>|
|디스크 구성|실제 디스크가 4GB 이상 있어야 합니다.<br>비어 있고 포맷 되지 않은 디스크 여야 합니다. 볼륨을 만들지 마세요.||
|HBA 고려 사항|-간단한 Hba (호스트 버스 어댑터) RAID 기능을 지원 하지 않는 것이 좋습니다.<br>-Hba을 사용 하지 않도록 설정 하는 모든 RAID 기능을 사용 하 여 비 RAID 모드에 있어야 RAID를 사용할 수 있으면<br>-어댑터 캐시 데이터를 실제 디스크를 추상화 하거나 모든 연결 된 장치를가 려 서 안 합니다. 여기에는 연결된 JBOD(Just-a-Bunch-Of-Disks) 장치를 통해 제공되는 엔클로저 서비스가 포함됩니다. |저장소 공간은 모든 RAID 기능을 완전히 사용하지 않도록 설정할 수 있는 HBA와만 호환됩니다.|
|JBOD 엔클로저|-JBOD 엔클로저는 선택 사항<br>권장 저장소 공간을 사용 하도록 인증 된 Windows Server 카탈로그에 나열 된 엔클로저<br>-JBOD 엔클로저를 사용 하는 경우 저장소 공급 업체와 함께 지원 하는지 확인 인클로저 전체 기능을 사용 하기 위해 저장소 공간<br>-를 JBOD 엔클로저가 엔클로저와 슬롯 식별을 지원 하는지 확인 하려면 다음 Windows PowerShell cmdlet을 실행 합니다.<br><br>`Get-PhysicalDisk \| ? {$_.BusType –eq "SAS"} \| fc`<br><br>경우는 **EnclosureNumber** 하 고 **SlotNumber** 는 엔클로저가 이러한 기능을 지원함을 필드 값을 포함 합니다.||

독립 실행형 서버 배포를 위한 실제 디스크 수 및 원하는 복원 유형을 계획하려면 다음 지침을 사용하세요.

|복원 유형|디스크 요구 사항|사용 시기|
|---|---|---|
|**간단**<br><br>-실제 디스크에 걸쳐 데이터를 스트라이프합니다.<br>-처리량을 높이고 디스크 용량을 극대화 합니다.<br>-(디스크 오류 로부터 보호 하지 않습니다) 하는 복원 력 없음<br><br><br><br><br><br><br>|하나 이상의 실제 디스크가 필요합니다.|호스트 대체할 수 없는 데이터를 사용 하지 마세요. 단순한 공간 디스크 오류 로부터 보호 하지 않습니다.<br><br>저렴한 비용으로 일시적이거나 간편하게 다시 만들 수 있는 데이터를 호스트하는 데 사용합니다.<br><br>복원 력 필요 하지 않습니다 또는 응용 프로그램에서 이미 제공 되는 고성능 워크 로드에 적합 합니다.|
|**미러**<br><br>-실제 디스크 집합 간에 두 또는 세 개의 데이터 복사본을 저장합니다.<br>-안정성이 증가 하지만 용량이 줄어듭니다. 쓸 때마다 중복이 발생합니다. 미러 공간도 여러 실제 드라이브에 데이터를 스트라이프합니다.<br>뛰어난 데이터 처리량 및 패리티 보다 더 낮은 액세스 대기 시간<br>-사용 하 여 더티 영역 (DRT) 풀의 디스크에 대 한 수정 작업을 추적할 수를 추적 합니다. 계획되지 않은 종료에서 시스템이 다시 시작되고 공간이 다시 온라인 상태로 전환된 경우 DRT는 풀의 디스크를 서로 일치하도록 만듭니다.|단일 디스크 오류로부터 보호하는 데 2개 이상의 실제 디스크가 필요합니다.<br><br>디스크 두 개의 동시 오류로부터 보호하는 데 5개 이상의 실제 디스크가 필요합니다.|대부분의 배포에 사용합니다. 예를 들어 미러 공간은 일반적인 용도의 파일 공유 또는 VHD(가상 하드 디스크) 라이브러리에 적합합니다.|
|**패리티**<br><br>-실제 디스크에 걸쳐 데이터와 패리티 정보가 스트라이프합니다.<br>-단순 공간 비교할 하지만 용량이 다소 줄어듭니다 때 안정성 향상<br>-저널링을 통해 복원 력을 높입니다. 이는 계획되지 않은 종료가 발생한 경우 데이터 손상을 방지하는 데 도움이 됩니다.|단일 디스크 오류로부터 보호하는 데 3개 이상의 실제 디스크가 필요합니다.|보관이나 백업과 같은 매우 순차적인 작업에 사용합니다.|

## <a name="step-1-create-a-storage-pool"></a>1단계: 저장소 풀 만들기

먼저 사용 가능한 실제 디스크를 하나 이상의 저장소 풀에 그룹화해야 합니다.

1. 서버 관리자 탐색 창에서 선택 **File and Storage Services**합니다.

2. 탐색 창에서 선택 합니다 **저장소 풀** 페이지입니다.
    
    기본적으로 사용 가능한 디스크는 *원시* 풀이라는 풀에 포함됩니다. **저장소 풀** 아래에 나열된 원시 풀이 없는 경우 이는 저장소가 저장소 공간 요구 사항을 충족하지 않음을 나타냅니다. 디스크가 사전 요구 사항 섹션에 설명된 요구 사항을 충족하는지 확인합니다.
    
    >[!TIP]
    >**원시** 저장소 풀을 선택하면 사용 가능한 실제 디스크가 **실제 디스크** 아래에 나열됩니다.

3. 아래 **저장소 풀**를 선택 합니다 **작업** 목록 및 선택한 **새 저장소 풀**합니다. 새 저장소 풀 마법사가 열립니다.

4. 에 **시작 하기 전에** 페이지에서 **다음**합니다.

5. 에 **저장소 풀 이름 및 하위 시스템 지정** 페이지, 이름 및 저장소 풀에 대 한 선택적 설명을 입력 하 고 클릭 하려는 사용 가능한 실제 디스크의 그룹 선택 **다음**합니다.

6. 에 **저장소 풀 용 실제 디스크 선택** 페이지에서 다음을 수행 하 고 선택한 **다음**:
    
    1. 저장소 풀에 포함할 각 실제 디스크 옆의 확인란을 선택합니다.
    
    2. 아래에 있는 하나 이상의 디스크 핫 스패어로 지정 하려는 경우 **할당**, 드롭 다운 화살표를 선택한 다음 선택 **핫 스패어**합니다.

7. 에 **선택 확인** 페이지에서 설정이 올바른지 하 고 선택한 것 **만들기**합니다.

8. 에 **결과 볼** 페이지에서 확인 하는 모든 작업이 완료 되 면 선택한 후 **닫기**합니다.
    
    >[!NOTE]
    >필요에 따라 다음 단계를 바로 진행하려면 **이 마법사를 닫으면 가상 디스크 만들기** 확인란을 선택하면 됩니다.

9. **저장소 풀**에서 새 저장소 풀이 나열되어 있는지 확인합니다.

### <a name="windows-powershell-equivalent-commands-for-creating-storage-pools"></a>저장소 풀을 만들기 위한 Windows PowerShell 해당 명령

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

다음 예제에서는 원시 풀에서 사용할 수 있는 실제 디스크를 보여 줍니다.

```PowerShell
Get-StoragePool -IsPrimordial $true | Get-PhysicalDisk | Where-Object CanPool -eq $True
```

다음 예제에서는 명명 된 새 저장소 풀을 만듭니다 *StoragePool1* 사용 가능한 모든 디스크를 사용 하는 합니다.

```PowerShell
New-StoragePool –FriendlyName StoragePool1 –StorageSubsystemFriendlyName “Storage Spaces*” –PhysicalDisks (Get-PhysicalDisk –CanPool $True)
```

다음 예제에서는 새 저장소 풀을 만듭니다 *StoragePool1*, 사용 가능한 디스크 4 개를 사용 하 합니다.

```PowerShell
New-StoragePool –FriendlyName StoragePool1 –StorageSubsystemFriendlyName “Storage Spaces*” –PhysicalDisks (Get-PhysicalDisk PhysicalDisk1, PhysicalDisk2, PhysicalDisk3, PhysicalDisk4)
```

다음 예제 cmdlet 시퀀스에서는 사용 가능한 실제 디스크 *PhysicalDisk5*를 저장소 풀 *StoragePool1*에 핫 스패어로 추가하는 방법을 보여 줍니다.

```PowerShell
$PDToAdd = Get-PhysicalDisk –FriendlyName PhysicalDisk5
Add-PhysicalDisk –StoragePoolFriendlyName StoragePool1 –PhysicalDisks $PDToAdd –Usage HotSpare
```

## <a name="step-2-create-a-virtual-disk"></a>2단계: 가상 디스크 만들기

이제 저장소 풀에서 하나 이상의 가상 디스크를 만들어야 합니다. 가상 디스크를 만들 때 실제 디스크에 데이터가 배치되는 방식을 선택할 수 있습니다. 이는 안정성과 성능 모두에 영향을 줍니다. 또한 씬 프로비저닝된 디스크를 만들지 또는 고정 프로비저닝된 디스크를 만들지 선택할 수 있습니다.

1. 새 가상 디스크 마법사가 이미 열려 있지 않은 경우 서버 관리자의 **저장소 풀** 페이지에서 **저장소 풀** 아래에 원하는 저장소 풀이 선택되어 있는지 확인합니다.

2. 아래 **가상 디스크**를 선택 합니다 **작업** 목록 및 선택한 **새 가상 디스크**합니다. 새 가상 디스크 마법사가 열립니다.

3. 에 **시작 하기 전에** 페이지에서 **다음**합니다.

4. 에 **저장소 풀 선택** 페이지에서 원하는 저장소 풀을 선택한 다음 선택 **다음**합니다.

5. 에 **가상 디스크 이름 지정** 페이지에서 이름과 선택적 설명을 입력 하 고 다음 선택 **다음**합니다.

6. 에 **저장소 레이아웃 선택** 페이지에서 원하는 레이아웃을 선택한 다음 선택 **다음**합니다.
    
    >[!NOTE]
    >선택 하면 오류 메시지가 나타날는 위치 없는 충분 한 실제 디스크 레이아웃을 선택 하면 **다음**합니다. 레이아웃을 사용 하 여 디스크 요구 사항에 대 한 정보를 참조 하세요 [필수 구성 요소](#prerequisites)).

7. 선택한 경우 **미러** 동일 저장소 레이아웃을 5 개 이상의 디스크 풀에는 **복원 력 설정 구성** 페이지가 나타납니다. 다음 옵션 중 하나를 선택합니다.
    
      - **양방향 미러**
      - **3방향 미러**

8. 에 **프로비저닝 유형 지정** 페이지에서 다음 옵션 중 하나를 선택 하 고 다음 선택 **다음**합니다.
    
   - **씬**
        
     씬 프로비저닝을 사용하면 필요할 때 공간이 할당됩니다. 이는 사용 가능한 저장소의 사용을 최적화합니다. 그러나 저장소를 과도하게 할당할 수 있으므로 사용 가능한 디스크 공간을 신중하게 모니터링해야 합니다.
    
   - **고정**
        
     고정 프로비저닝을 사용하면 가상 디스크가 만들어지는 즉시 저장소 용량이 할당됩니다. 따라서 고정 프로비저닝에서는 저장소 풀에서 가상 디스크 크기와 동일한 공간을 사용합니다.
    
     >[!TIP]
     >저장소 공간을 사용하는 경우 동일한 저장소 풀에서 씬 프로비저닝된 가상 디스크와 고정 프로비저닝된 가상 디스크를 모두 만들 수 있습니다. 예를 들어 씬 프로비저닝된 가상 디스크를 사용하여 데이터베이스를 호스트하고, 고정 프로비저닝된 가상 디스크를 사용하여 연관된 로그 파일을 호스트할 수 있습니다.

9. **가상 디스크의 크기를 지정하세요.** 페이지에서 다음을 수행합니다.
    
    이전 단계에서 씬 프로비저닝을 선택한 경우 합니다 **가상 디스크 크기** 상자에서 가상 디스크 크기를 입력를 단위 (**MB**를 **GB**, 또는 **TB** )을 선택한 후 **다음**합니다.
    
    이전 단계에서 고정 프로비저닝을 선택한 경우 다음 중 하나를 선택 합니다.
    
      - **크기 지정**
        
        크기를 지정 하려면 값을 입력 합니다 **가상 디스크 크기** 상자를 선택한 다음 단위를 선택 (**MB**에 **GB**, 또는 **TB**).
        
        단순 이외의 저장소 레이아웃을 사용할 경우 가상 디스크에서 지정한 크기보다 더 많은 여유 공간을 사용합니다. 볼륨 크기가 저장소 풀 여유 공간을 초과하는 잠재적 오류를 방지하려면 **최대 지정한 크기까지 가능한 가장 큰 가상 디스크 만들기** 확인란을 선택하면 됩니다.
    
      - **최대 크기**
        
        저장소 풀의 최대 용량을 사용하는 가상 디스크를 만들려면 이 옵션을 선택합니다.

10. 에 **선택 확인** 페이지에서 설정이 올바른지 하 고 선택한 것 **만들기**합니다.

11. 에 **결과 볼** 페이지에서 확인 하는 모든 작업이 완료 되 면 선택한 후 **닫기**합니다.
    
    >[!TIP]
    >기본적으로 **이 마법사를 닫으면 볼륨 만들기** 확인란이 선택되며, 이 경우 다음 단계로 바로 이동합니다.

### <a name="windows-powershell-equivalent-commands-for-creating-virtual-disks"></a>가상 디스크를 만드는 데 Windows PowerShell 해당 명령

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

다음 예에서는 이라는 50GB 가상 디스크를 만듭니다 *VirtualDisk1* 저장소 풀에서 라는 *StoragePool1*합니다.

```PowerShell
New-VirtualDisk –StoragePoolFriendlyName StoragePool1 –FriendlyName VirtualDisk1 –Size (50GB)
```

다음 예에서는 이라는 미러링된 가상 디스크를 만듭니다 *VirtualDisk1* 저장소 풀에서 라는 *StoragePool1*합니다. 디스크는 저장소 풀의 최대 저장소 용량을 사용합니다.

```PowerShell
New-VirtualDisk –StoragePoolFriendlyName StoragePool1 –FriendlyName VirtualDisk1 –ResiliencySettingName Mirror –UseMaximumSize
```

다음 예에서는 이라는 50GB 가상 디스크를 만듭니다 *VirtualDisk1* 이라고 하는 저장소 풀에 *StoragePool1*합니다. 이 디스크는 씬 프로비저닝 유형을 사용합니다.

```PowerShell
New-VirtualDisk –StoragePoolFriendlyName StoragePool1 –FriendlyName VirtualDisk1 –Size (50GB) –ProvisioningType Thin
```

다음 예제에서는 명명 된 가상 디스크를 만듭니다 *VirtualDisk1* 저장소 풀에서 라는 *StoragePool1*합니다. 이 가상 디스크는 3방향 미러링을 사용하며 고정 크기가 20GB입니다.

>[!NOTE]
>이 cmdlet이 작동하려면 저장소 풀에 5개 이상의 실제 디스크가 있어야 합니다. 핫 스패어로 할당된 디스크는 여기에 포함되지 않습니다.

```PowerShell
New-VirtualDisk -StoragePoolFriendlyName StoragePool1 -FriendlyName VirtualDisk1 -ResiliencySettingName Mirror -NumberOfDataCopies 3 -Size 20GB -ProvisioningType Fixed
```

## <a name="step-3-create-a-volume"></a>3단계: 볼륨 만들기

이제 가상 디스크에서 볼륨을 만들어야 합니다. 선택적 드라이브 문자 또는 폴더를 할당 다음 파일 시스템으로 볼륨을 포맷할 수 있습니다.

1. 새 볼륨 마법사가 이미 열려 있으면 합니다 **저장소 풀** 아래에 있는 서버 관리자에서 페이지 **가상 디스크**원하는 가상 디스크를 마우스 오른쪽 단추로 클릭 한 다음 선택 **새볼륨**.
    
    새 볼륨 마법사가 열립니다.

2. 에 **시작 하기 전에** 페이지에서 **다음**합니다.

3. 에 **서버 및 디스크 선택** 페이지에서 다음을 수행 하 고 선택한 **다음**합니다.
    
    1. 에 **Server** 영역에서 볼륨을 프로 비전 하려는 서버를 선택 합니다.
    
    2. 에 **디스크** 영역에서 볼륨을 만드는 데 사용할 가상 디스크를 선택 합니다.

4. 에 **볼륨의 크기를 지정** 페이지에서 단위를 지정 합니다. 볼륨 크기를 입력 (**MB**합니다 **GB**, 또는 **TB**)를 선택한 다음 **다음**합니다.

5. 에 **드라이브 문자 또는 폴더에 할당할** 페이지에서 원하는 옵션을 구성 하 고 선택한 **다음**합니다.

6. 에 **파일 시스템 설정 선택** 페이지에서 다음을 수행 하 고 선택한 **다음**합니다.
    
    1. 에 **파일 시스템** 목록에서 선택 하거나 **NTFS** 또는 **ReFS**합니다.
    
    2. **할당 단위 크기** 목록에서 **기본값** 설정을 그대로 두거나 할당 단위 크기를 설정합니다.
        
        >[!NOTE]
        >할당 단위 크기에 대한 자세한 내용은 [NTFS, FAT 및 exFAT의 기본 클러스터 크기](https://support.microsoft.com/help/140365/default-cluster-size-for-ntfs-fat-and-exfat)를 참조하세요.

    
    3. 필요한 경우 **볼륨 레이블** 상자에 볼륨 레이블 이름을 입력합니다(예: **HR 데이터**).

7. 에 **선택 확인** 페이지에서 설정이 올바른지 하 고 선택한 것 **만들기**합니다.

8. 에 **결과 볼** 페이지에서 확인 하는 모든 작업이 완료 되 면 선택한 후 **닫기**합니다.

9. 볼륨 생성 되었는지 확인 하려면, 서버 관리자에서 선택 합니다 **볼륨** 페이지입니다. 볼륨이 만들어진 서버 아래에 볼륨이 나열됩니다. 볼륨이 Windows 탐색기에 있는지도 확인할 수 있습니다.

### <a name="windows-powershell-equivalent-commands-for-creating-volumes"></a>볼륨 만들기에 대 한 Windows PowerShell 해당 명령

다음 Windows PowerShell cmdlet은 이전 절차와 동일한 기능을 수행합니다. 한 줄에 명령을 입력합니다.

다음 예제에서는 *VirtualDisk1* 가상 디스크의 디스크를 초기화하고, 할당된 드라이브 문자로 파티션을 만든 다음, 기본 NTFS 파일 시스템으로 볼륨을 포맷합니다.

```PowerShell
Get-VirtualDisk –FriendlyName VirtualDisk1 | Get-Disk | Initialize-Disk –Passthru | New-Partition –AssignDriveLetter –UseMaximumSize | Format-Volume
```

## <a name="additional-information"></a>추가 정보

- [스토리지 공간](overview.md)
- [Windows PowerShell의 저장소 Cmdlet](https://docs.microsoft.com/powershell/module/storage/index?view=win10-ps)
- [클러스터 된 저장소 공간 배포](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11))
- [저장소 공간 질문과 대답 (FAQ)](https://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx)
