---
title: 독립 실행형 서버에서 저장소 공간 배포
description: Windows Server 2012 기반 독립 실행형 서버에서 저장소 공간 배포 하는 방법에 설명 합니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-spaces
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 40265e767ac9aca05386c0893def259aca3a5633
ms.sourcegitcommit: e73fbe1046a8bd2bf4f24ccffc11465ad8dfab1d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/07/2019
ms.locfileid: "8992536"
---
# 독립 실행형 서버에서 저장소 공간 배포

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 독립 실행형 서버에서 저장소 공간 배포 하는 방법을 설명 합니다. 클러스터 저장소 공간을 만드는 방법에 대 한 자세한 내용은 [Windows Server 2012 r 2에서 저장소 공간 클러스터 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/mt270997(v%3dws.11)>)를 참조 하십시오.

저장소 공간을 만들려면 먼저 하나 이상의 저장소 풀 만들어야 합니다. 저장소 풀은 실제 디스크의 컬렉션입니다. 저장소 풀을 통해 저장소 집계, 확대/축소 용량 확장 및 위임 된 관리 합니다.

저장소 풀에서 하나 이상의 가상 디스크를 만들 수 있습니다. 이러한 가상 디스크는 *저장소 공간*라고도 합니다. 저장소 공간을 만들 수 있는 일반 디스크 포맷 된 볼륨 Windows 운영 체제를 표시 합니다. 파일 및 저장소 서비스 사용자 인터페이스를 통해 가상 디스크를 만들 때 복원 력 유형을 구성할 수 있습니다 (간단한, 미러 또는 패리티), (씬 또는 고정)는 프로 비전 유형 및 크기입니다. Windows PowerShell을 통해 열, 인터리브 값 및 사용 하 여 풀에는 실제 디스크의 수와 같은 추가 매개 변수를 설정할 수 있습니다. 이러한 추가 매개 변수에 대 한 정보를 보려면 [새로 VirtualDisk](https://docs.microsoft.com/powershell/module/storage/new-virtualdisk?view=win10-ps) 및 [열이 무엇 인지와 저장소 공간 결정 하는 방법을 사용 하 여 얼마나 많은?](https://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx%23what_are_columns_and_how_does_storage_spaces_decide_how_many_to_use) 에서 저장소 공간 자주 질문과 대답 (FAQ).

>[!NOTE]
>Windows 운영 체제를 호스트 하는 저장소 공간을 사용할 수 없습니다.

가상 디스크에서 하나 이상의 볼륨을 만들 수 있습니다. 볼륨을 만들 때 크기, 드라이브 문자 또는 폴더, 파일 시스템 (NTFS 파일 시스템 또는 ReFS (복원 파일 시스템)), 할당 단위 크기 및 선택적 볼륨 레이블을 구성할 수 있습니다.

다음 그림은 저장소 공간 워크플로를 보여 줍니다.

![저장소 공간 워크플로](media/deploy-standalone-storage-spaces/storage-spaces-workflow.png)

**그림 1: 저장소 공간 워크플로**

>[!NOTE]
>이 항목에 설명 하는 절차 중 일부를 자동화 하는 데 사용할 수 있는 샘플 Windows PowerShell cmdlet을 포함 됩니다. 자세한 내용은 [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting?view=powershell-6)을 참조 하세요.

## 필수 조건

독립 실행형 Windows Server 2012−based 서버에서 저장소 공간을 사용 하는 실제 디스크를 사용 하려면 다음과 같은 필수 조건을 충족 하는지 확인 합니다.

> [!IMPORTANT]
> 장애 조치 클러스터에서 저장소 공간 배포 하는 방법은 하려는 경우 [Windows Server 2012 r 2에서 저장소 공간 클러스터 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/mt270997(v%3dws.11)>)를 참조 하십시오. 장애 조치 클러스터 배포에 지원 되는 디스크 버스 유형, 지원 되는 복원 력 유형 및 필요한 최소 디스크와 같은 다른 필수 조건이 있습니다.

|영역|요구 사항|메모|
|---|---|---|
|디스크 버스 유형|직렬 연결 SCSI (SAS)<br>직렬 고급 기술 첨부 파일 (SATA)<br>-iSCSI 및 파이버 채널 컨트롤러 합니다. |USB 드라이브를 사용할 수 있습니다. 그러나 서버 환경에서 USB 드라이브를 사용 하 여 최적 상태가 아닙니다.<br>저장소 공간 위에 만든 가상 디스크가 력이 (임의 개수의 열을 사용 하 여 단순)으로 iSCSI 및 파이버 채널 (FC) 컨트롤러에서 지원 됩니다.<br>|
|디스크 구성|-실제 디스크 4GB 이상 있어야 합니다.<br>-디스크는 비어 있는 포맷 되지 않았거나 이어야 합니다. 볼륨을 만들지 않습니다.||
|HBA 고려 사항|-RAID 기능을 지원 하지 않는 간단한 호스트 버스 어댑터 (Hba)는 것이 좋습니다.<br>-Hba RAID 지원 경우 모든 RAID 기능을 사용 하 여 비-RAID 모드로 이어야 함<br>-어댑터 실제 디스크, 데이터를 캐시 추상화 하거나 연결된 된 장치가 림 해서는 안 됩니다. 연결 된 바로-a-여러--디스크 (JBOD) 장치에서 제공 되는 엔클로저 서비스 포함 됩니다. |저장소 공간은 Hba 호환 RAID 기능을 모두를 완전히 비활성화할 수 있습니다.|
|JBOD 엔클로저|-JBOD 엔클로저는 선택 사항<br>인증 저장소 공간을 사용 하 여 권장 Windows Server 카탈로그에 나열 된 엔클로저<br>-JBOD 엔클로저를 사용 하는 경우 저장소 공급 업체 지원 하는지 확인 모양 전체 작동을 위해 저장소 공간<br>-JBOD 엔클로저 인클로저 및 슬롯 식별을 지원 하는지 여부를 확인 하려면 다음 Windows PowerShell cmdlet을 실행 합니다.<br><br>`Get-PhysicalDisk \| ? {$_.BusType –eq "SAS"} \| fc`<br><br>**EnclosureNumber** 및 **SlotNumber** 필드에 값이 없으면 모양 이러한 기능을 지원 합니다.||

독립 실행형 서버 배포에 대 한 원하는 복원 력 유형 및 실제 디스크 번호에 대 한 계획을 하려면 다음 지침을 사용 합니다.

|복원 력 유형|디스크 요구 사항|사용해야 하는 경우|
|---|---|---|
|**단순**<br><br>-실제 디스크에 걸쳐 띠 데이터<br>-디스크 용량 극대화 하 고 처리량이 증가<br>(디스크 오류에서 보호 하지 않습니다)-복원 력<br><br><br><br><br><br><br>|하나 이상의 실제 디스크에 필요합니다.|호스트 하거나 대체할 데이터를 사용 하지 마세요. 간단한 공간 디스크 오류에 대 한 보호 하지 않습니다.<br><br>저렴 한 가격 호스트 임시 또는 쉽게 다시 데이터를 사용 합니다.<br><br>여기서 복원 력 필요 하지 않거나 응용 프로그램에서 제공 된 고성능 워크 로드에 적합 합니다.|
|**미러**<br><br>-실제 디스크 집합 간에 데이터의 두 가지 또는 세 개의 복사본을 저장합니다.<br>-안정성 증가 하지만 용량을 줄입니다. 모든 쓰기 중복 발생합니다. 또한 미러 공간 스트라이프 데이터를 여러 개의 실제 드라이브 만드는 합니다.<br>-큰 데이터 처리량 및 패리티 보다 액세스 대기 시간 단축<br>-사용 하 여 변경 지역 (DRT) 풀의 디스크에 대 한 수정 추적을 추적 합니다. 시스템 종료에서 시작 하 고 공백을 온라인으로 다시 전환, DRT 이동 하면 디스크 풀의 서로 일치 합니다.|단일 디스크 오류를 보호 하기 위해 두 개 이상의 실제 디스크에 필요 합니다.<br><br>두 개의 동시 디스크 오류 으로부터 보호 하는 5 개 이상 실제 디스크에 필요 합니다.|대부분의 배포에 사용 됩니다. 예를 들어 미러 공간은 범용 파일 공유 나 가상 하드 디스크 (VHD) 라이브러리에 적합 합니다.|
|**패리티**<br><br>-실제 디스크에 걸쳐 띠 데이터 및 패리티 정보<br>-간단한 공간을 비교 않지만 용량 약간 감소 안정성 증가<br>-저널링 통해 복원 력을 증가합니다. 이렇게 하면 종료 발생 하는 경우 데이터 손상을 방지 됩니다.|단일 디스크 오류를 보호 하기 위해 최소 세 개의 실제 디스크에 필요 합니다.|보관 또는 백업 같은 고도로 순차적인 있는 워크 로드에 사용 됩니다.|

## 1 단계: 저장소 풀 만들기

하나 이상의 저장소 풀에 첫 번째 그룹의 사용 가능한 실제 디스크를 해야합니다.

1. 서버 관리자 탐색 창에서 **파일 및 저장소 서비스를**선택 합니다.

2. 탐색 창에서 **저장소 풀** 페이지를 선택 합니다.
    
    기본적으로 사용 가능한 디스크 *원시* 풀 라는 풀에 포함 됩니다. **저장소 풀**에서 원시 없는 풀 나열 되는 경우 저장소 저장소 공간에 대 한 요구를 충족 하지 못하면 나타냅니다. 디스크 사전 요구 사항 섹션에서 설명 하는 요구 사항을 충족 하는지 확인 합니다.
    
    >[!TIP]
    >**원시** 저장소 풀을 선택 하면 사용 가능한 실제 디스크 **실제 디스크**아래에 나열 됩니다.

3. **저장소 풀** **작업** 목록을 선택 하 고 **새 저장소 풀**을 선택 합니다. 새 저장소 풀 마법사가 열립니다.

4. **시작 하기 전에** 페이지에서 **다음**을 선택 합니다.

5. **하위 시스템 및 저장소 풀 이름 지정** 페이지에서 이름 및 저장소 풀에 대 한 선택적 설명을 입력, 사용 가능한 실제 디스크를 사용 하려는 그룹을 선택 하 고 **** 을 선택 합니다.

6. **저장소 풀에 대 한 실제 디스크 선택** 페이지를 차례로 선택 하 고 다음, **다음**을 수행 합니다.
    
    1. 저장소 풀에 포함 하려는 각 실제 디스크 옆에 있는 확인란을 선택 합니다.
    
    2. 드롭다운 화살표를 선택 하는 **할당**을 아래 핫 대체로 서 더 많은 디스크 하나를 지정 하려면, **핫 예비**를 선택 합니다.

7. **확인 선택** 페이지에서 설정을 올바른지를 선택한 다음 **만들기**를 확인 합니다.

8. **결과 보기** 페이지에서 모든 작업 완료를 선택한 후 **닫기**를 확인 합니다.
    
    >[!NOTE]
    >필요한 경우 다음 단계를 직접을 계속 해 서 **이 마법사를 닫으면 가상 디스크 만들기** 확인란을 선택할 수 있습니다.

9. **저장소 풀**새 저장소 풀 나열 되어 있는지 확인 합니다.

### 저장소 풀을 만들기 위한 Windows PowerShell 상응 하는 명령

다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행합니다. 하지만 서식 제약 조건으로 인해 여기에 여러 줄 바꿈 표시 될 수 있습니다 한 줄에 각 cmdlet을 입력 합니다.

다음 예제에서는 원시 풀에서 사용할 수 있는 실제 디스크를 보여 줍니다.

```PowerShell
Get-StoragePool -IsPrimordial $true | Get-PhysicalDisk | Where-Object CanPool -eq $True
```

다음 예제에서는 사용 가능한 모든 디스크를 사용 하는 *StoragePool1* 라는 새 저장소 풀을 만듭니다.

```PowerShell
New-StoragePool –FriendlyName StoragePool1 –StorageSubsystemFriendlyName “Storage Spaces*” –PhysicalDisks (Get-PhysicalDisk –CanPool $True)
```

다음 예제에서는 *StoragePool1*, 사용 가능한 디스크의 4 개를 사용 하는 새 저장소 풀을 만듭니다.

```PowerShell
New-StoragePool –FriendlyName StoragePool1 –StorageSubsystemFriendlyName “Storage Spaces*” –PhysicalDisks (Get-PhysicalDisk PhysicalDisk1, PhysicalDisk2, PhysicalDisk3, PhysicalDisk4)
```

다음 예제에서는 순서의 cmdlet *StoragePool1*저장소 풀에 사용 가능한 실제 디스크 *PhysicalDisk5* 핫 예비도 추가 하는 방법을 보여 줍니다.

```PowerShell
$PDToAdd = Get-PhysicalDisk –FriendlyName PhysicalDisk5
Add-PhysicalDisk –StoragePoolFriendlyName StoragePool1 –PhysicalDisks $PDToAdd –Usage HotSpare
```

## 2 단계: 가상 디스크 만들기

다음으로, 저장소 풀에서 하나 이상의 가상 디스크 만들어야 합니다. 가상 디스크를 만들 때 실제 디스크를 통해 데이터 배치 되는 방식을 선택할 수 있습니다. 모두 안정성 및 성능에 영향을 줍니다. 또한 씬 또는 고정-프로 비전 된 디스크를 만들지 여부를 선택할 수 있습니다.

1. 서버 관리자에서 **저장소 풀** 페이지에서 열려 있지 않으면 새 가상 디스크 마법사 경우 **저장소 풀**원하는 저장소 풀 선택 되었는지 확인을 확인 합니다.

2. **가상 디스크** **작업** 목록을 선택 하 고 **새 가상 디스크**를 선택 합니다. 새 가상 디스크 마법사가 열립니다.

3. **시작 하기 전에** 페이지에서 **다음**을 선택 합니다.

4. **저장소 풀을 선택** 페이지에서 원하는 저장소 풀을 선택 하 고 **** 을 선택 합니다.

5. **가상 디스크 이름 지정** 페이지에서 이름과 선택적 설명을 입력 하 고 **** 을 선택 합니다.

6. **저장소 레이아웃 선택** 페이지에서 원하는 레이아웃을 선택한 **다음**을 선택 합니다.
    
    >[!NOTE]
    >충분 한 실제 디스크가 없는 레이아웃을 선택 하면 선택 하면 **다음**오류 메시지를 받게 됩니다. 레이아웃을 사용 하 고 디스크 요구 사항에 대 한 정보에 대 한 [필수 구성 요소](#prerequisites)참조).

7. 저장소 레이아웃으로 **미러** 선택한 5 개 이상의 디스크 풀에 있는 경우 **복원 력 설정을 구성** 페이지가 나타납니다. 다음 옵션 중 하나를 선택 합니다.
    
      - **양방향 미러**
      - **3방향 미러**

8. **프로 비전 유형 지정** 페이지에서 다음 옵션 중 하나를 선택 하 고 **** 을 선택 합니다.
    
      - **씬**
        
        씬 프로 비전에 필요에 따라 공간이 할당 됩니다. 사용 가능한 저장소로 사용을 최적화합니다. 그러나를 과도 하 게 저장소를 할당 하면, 때문에 신중 하 게 모니터링 해야 디스크 공간을 사용할 수 있습니다.
    
      - **고정**
        
        고정 된 프로 비전 된 저장소 용량 가상 디스크를 만들 때에 즉시 할당 됩니다. 따라서 가상 디스크 크기와 같은 저장소 풀에서 프로 비전 사용 하 여 공간을 고정 합니다.
    
    >[!TIP]
    >저장소 공간을 사용 하 여 동일한 저장소 풀에 두 씬 및 고정-프로 비전 된 가상 디스크를 만들 수 있습니다. 예를 들어, 데이터베이스 및 관련된 로그 파일을 호스팅할 고정 프로 비전 된 가상 디스크를 호스트 하는 씬 프로 비전 된 가상 디스크를 사용할 수 있습니다.

9. **가상 디스크의 크기 지정** 페이지에서 다음을 수행 합니다.
    
    이전 단계에서 씬 프로 비전을 선택한 경우에 **가상 디스크 크기** 상자에 입력 된 가상 디스크 크기 (**MB**, **GB**또는 **테라바이트**) 단위 선택한 **다음**선택 합니다.
    
    이전 단계에서 고정 된 프로 비전을 선택한 경우 다음 중 하나를 선택 합니다.
    
      - **크기를 지정 합니다.**
        
        크기를 지정 하려면 **가상 디스크 크기** 상자에 값을 입력 한 다음 (**MB**, **GB**또는 **테라바이트**) 단위를 선택 합니다.
        
        단순 이외의 저장소 레이아웃을 사용 하는 경우 가상 디스크 지정 하는 크기 보다 더 많은 공간을 사용 합니다. 저장소 풀 여유 공간을 초과 하는 볼륨의 크기는 잠재적인 오류를 방지 하기 위해 **크기 제한 가능한 가장 큰 가상 디스크 만들기** 확인란을 선택할 수 있습니다.
    
      - **최대 크기**
        
        저장소 풀의 최대 용량을 사용 하는 가상 디스크를 만들려면이 옵션을 선택 합니다.

10. **확인 선택** 페이지에서 설정을 올바른지를 선택한 다음 **만들기**를 확인 합니다.

11. **결과 보기** 페이지에서 모든 작업 완료를 선택한 후 **닫기**를 확인 합니다.
    
    >[!TIP]
    >기본적으로 **이 마법사를 닫으면 볼륨 만들기** 확인란이 선택 되어 있습니다. 이 다음 단계로 이동합니다.

### 가상 디스크 만들기에 대 한 Windows PowerShell 해당 하는 명령

다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행합니다. 하지만 서식 제약 조건으로 인해 여기에 여러 줄 바꿈 표시 될 수 있습니다 한 줄에 각 cmdlet을 입력 합니다.

다음 예제에서는 *StoragePool1*라는 저장소 풀에 *VirtualDisk1* 라는 50GB 가상 디스크를 만듭니다.

```PowerShell
New-VirtualDisk –StoragePoolFriendlyName StoragePool1 –FriendlyName VirtualDisk1 –Size (50GB)
```

다음 예제에서는 *VirtualDisk1* *StoragePool1*라는 저장소 풀에서 미러링된 가상 디스크를 만듭니다. 디스크는 저장소 풀의 최대 저장소 용량을 사용합니다.

```PowerShell
New-VirtualDisk –StoragePoolFriendlyName StoragePool1 –FriendlyName VirtualDisk1 –ResiliencySettingName Mirror –UseMaximumSize
```

다음 예제에서는 *StoragePool1*라는 저장소 풀에 *VirtualDisk1* 라는 50GB 가상 디스크를 만듭니다. 씬 프로비저닝 형식을 사용 하는 디스크 합니다.

```PowerShell
New-VirtualDisk –StoragePoolFriendlyName StoragePool1 –FriendlyName VirtualDisk1 –Size (50GB) –ProvisioningType Thin
```

다음 예제에서는 *StoragePool1*라는 저장소 풀에 *VirtualDisk1* 라는 가상 디스크를 만듭니다. 가상 디스크 3 방향 미러링을 사용 하 여 되며 20GB의 고정된 크기입니다.

>[!NOTE]
>저장소 풀 작동 하려면이 cmdlet에 대 한 실제 디스크 5 개 이상 있어야 합니다. (이 핫 예비도 할당 되는 모든 디스크)

```PowerShell
New-VirtualDisk -StoragePoolFriendlyName StoragePool1 -FriendlyName VirtualDisk1 -ResiliencySettingName Mirror -NumberOfDataCopies 3 -Size 20GB -ProvisioningType Fixed
```

## 3 단계: 볼륨 만들기

다음으로 가상 디스크의 볼륨을 만들어야 합니다. 선택적 드라이브 문자 또는 폴더를 할당 다음 파일 시스템으로 볼륨을 포맷할 수 있습니다.

1. 서버 관리자에서 **가상 디스크** **저장소 풀** 페이지에서 열려 있지 않으면 새 볼륨 마법사 원하는 가상 디스크를 마우스 오른쪽 단추로 클릭 한 다음 **새 볼륨**을 선택 합니다.
    
    새 볼륨 마법사가 열립니다.

2. **시작 하기 전에** 페이지에서 **다음**을 선택 합니다.

3. **서버 및 디스크 선택** 페이지를 차례로 선택 하 고 다음, **다음**을 수행 합니다.
    
    1. **서버** 영역에서 볼륨을 프로 비전 하려는 서버를 선택 합니다.
    
    2. **디스크** 영역에서 볼륨 만들려는 가상 디스크를 선택 합니다.

4. **볼륨의 크기 지정** 페이지 (**MB**, **GB**또는 **테라바이트**) 단위를 지정 볼륨 크기를 입력 하 고 **** 을 선택 합니다.

5. **드라이브 문자 또는 폴더에 할당** 페이지에서 원하는 옵션을 구성 하 고 **** 을 선택 합니다.

6. **파일 시스템 설정 선택** 페이지를 차례로 선택 하 고 다음, **다음**을 수행 합니다.
    
    1. **파일 시스템** 은 **NTFS** 또는 **ReFS**를 선택 합니다.
    
    2. **할당 단위 크기** 목록에서 **기본** 설정을 유지 하거나 할당 단위 크기를 설정 합니다.
        
        >[!NOTE]
        >할당 단위 크기에 대 한 자세한 내용은 [기본 NTFS, FAT 및 exFAT 클러스터 크기를](https://support.microsoft.com/help/140365/default-cluster-size-for-ntfs-fat-and-exfat)참조 하세요.

    
    3. 필요에 따라 **볼륨 레이블** 상자에서 볼륨 레이블 이름, 예: **HR 데이터**를 입력 합니다.

7. **확인 선택** 페이지에서 설정을 올바른지를 선택한 다음 **만들기**를 확인 합니다.

8. **결과 보기** 페이지에서 모든 작업 완료를 선택한 후 **닫기**를 확인 합니다.

9. 볼륨 생성 되었는지 확인, 서버 관리자에서 **볼륨** 페이지를 선택 합니다. 볼륨 만들어진 서버 아래 표시 됩니다. Windows 탐색기에서 볼륨 인지 확인할 수 있습니다.

### 볼륨 만들기에 대 한 Windows PowerShell 해당 하는 명령

다음 Windows PowerShell cmdlet 이전 절차와 동일한 기능을 수행 합니다. 한 줄에 명령을 입력 합니다.

다음 예제에서는 *VirtualDisk1*가상 디스크의 디스크 초기화 되 고, 할당 된 드라이브 문자를 사용 하 여 파티션을 만듭니다 기본 NTFS 파일 시스템으로 볼륨 형식을 지정 합니다.

```PowerShell
Get-VirtualDisk –FriendlyName VirtualDisk1 | Get-Disk | Initialize-Disk –Passthru | New-Partition –AssignDriveLetter –UseMaximumSize | Format-Volume
```

## 추가 정보

- [저장소 공간](overview.md)
- [Windows PowerShell의 저장소 Cmdlet](https://docs.microsoft.com/powershell/module/storage/index?view=win10-ps)
- [클러스터 저장소 공간 배포](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11))
- [저장소 공간에 질문과 대답 (FAQ)](https://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx)
