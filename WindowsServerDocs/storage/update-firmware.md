---
ms.assetid: e5945bae-4a33-487c-a019-92a69db8cf6c
title: Windows Server 2016에서 드라이브 펌웨어 업데이트
ms.prod: windows-server-threshold
ms.author: toklima
ms.manager: dmoss
ms.technology: storage-spaces
ms.topic: article
author: toklima
ms.date: 10/04/2016
ms.openlocfilehash: 50291bd4da05d9c2736c84443b444b9a43f46344
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884784"
---
# <a name="updating-drive-firmware-in-windows-server-2016"></a>Windows Server 2016에서 드라이브 펌웨어 업데이트
>적용 대상: Windows 10, Windows Server (반기 채널), Windows Server 2016

드라이브의 펌웨어 업데이트는 지금까지 가동 중지 시간이 생길 수 있는 번거로운 작업이었습니다. 이런 이유로 Microsoft는 저장소 공간, Windows Server 및 Windows 10, 버전 1703 및 이후 버전을 개선하고 있습니다. Windows에 포함된 새로운 펌웨어 업데이트 메커니즘을 지원하는 드라이브가 있는 경우 가동 중지 시간 없이 프로덕션 드라이브의 펌웨어를 업데이트할 수 있습니다. 그러나 프로덕션 드라이브의 펌웨어를 업데이트하려는 경우 강력한 최신 펌웨어 업데이트 기능을 사용하는 동시에 위험을 최소화하는 방법에 대한 팁을 읽어야 합니다.

  > [!Warning]
  > 펌웨어 업데이트는 잠재적으로 위험한 유지 관리 작업이며, 새 펌웨어 이미지를 철저하게 테스트한 후에 적용해야 합니다. 지원되지 않는 하드웨어의 새 펌웨어는 신뢰성과 안정성에 부정적인 영향을 미칠 수 있으며, 데이터 손실을 일으킬 수도 있습니다. 관리자는 특정 업데이트와 함께 제공되는 릴리스 정보를 읽고 해당 영향 및 적용 가능성을 판단해야 합니다.

## <a name="drive-compatibility"></a>드라이브 호환성

Windows Server를 사용하여 드라이브 펌웨어를 업데이트하려면 지원되는 드라이브가 있어야 했습니다. 일반적인 장치 동작을 보장하기 위해 SAS, SATA 및 NVMe 장치에 대한 새롭고(Windows 10 및 Windows Server 2016의 경우) 선택적인 HLK(Hardware Lab Kit) 요구 사항을 정의하는 것으로 시작했습니다. 이러한 요구 사항은 Windows에 포함된 새로운 PowerShell cmdlet을 사용하여 펌웨어 업데이트가 가능하도록 SAS, SATA 또는 NVMe 장치에서 지원해야 하는 명령의 개요를 제공합니다. 공급업체 제품이 올바른 명령을 지원하며 향후 수정 버전에서 구현될지를 확인하기 위한 새로운 HLK 테스트가 있습니다. 

하드웨어가 드라이브 펌웨어를 업데이트하는 Windows를 지원하는지에 대한 정보는 솔루션 공급업체에 문의하세요.
다음은 다양한 요구 사항에 대한 링크입니다.

-   SATA: [Device.Storage.Hd.Sata](https://msdn.microsoft.com/windows/hardware/commercialize/design/compatibility/device-storage#devicestoragehdsata) -합니다 **[구현 된 경우\] 펌웨어 다운로드 및 활성화** 섹션
    
-   SAS: [Device.Storage.Hd.Sas](https://msdn.microsoft.com/windows/hardware/commercialize/design/compatibility/device-storage#devicestoragehdsas) -합니다 **[구현 된 경우\] 펌웨어 다운로드 및 활성화** 섹션

-   NVMe: [Device.Storage.ControllerDrive.NVMe](https://msdn.microsoft.com/windows/hardware/commercialize/design/compatibility/device-storage#devicestoragecontrollerdrivenvme) -단원의 **5.7** 하 고 **5.8**합니다.

## <a name="powershell-cmdlets"></a>PowerShell cmdlet

Windows에 추가된 두 개의 cmdlet은 다음과 같습니다.

-   Get-StorageFirmwareInformation
-   Update-StorageFirmware

첫 번째 cmdlet은 장치 기능, 펌웨어 이미지 및 수정 버전에 대한 자세한 정보를 제공합니다. 이 경우 컴퓨터에는 펌웨어 슬롯 1개와 단일 SATA SSD만 포함되어 있습니다. 예를 들면 다음과 같습니다.

   ```powershell
   Get-PhysicalDisk | Get-StorageFirmwareInformation

   SupportsUpdate        : True
   NumberOfSlots         : 1
   ActiveSlotNumber      : 0
   SlotNumber            : {0}
   IsSlotWritable        : {True}
   FirmwareVersionInSlot : {J3E16101}
   ```

이러한 명령의 지원 여부에 대해 장치에 명시적으로 쿼리할 방법이 없기 때문에 SAS 장치는 항상 "SupportsUpdate" 및 "True"를 보고합니다.

두 번째 cmdlet인 Update-StorageFirmware는 드라이브가 새 펌웨어 업데이트 메커니즘을 지원하는 경우 관리자가 이미지 파일로 드라이브 펌웨어를 업데이트할 수 있도록 해 줍니다. 이미지 파일은 OEM 또는 드라이브 공급업체에서 직접 받아야 합니다.

  > [!Note]
  > 프로덕션 하드웨어를 업데이트하기 전에 랩 설정에서 동일한 하드웨어에 대해 특정 펌웨어 이미지를 테스트하세요.

드라이브는 먼저 새 펌웨어 이미지를 내부 준비 영역에 로드합니다. 이렇게 하는 동안 I/O는 일반적으로 계속 진행됩니다. 이미지는 다운로드 후 활성화됩니다. 내부 다시 설정이 발생하므로 이 시간 동안 드라이브는 I/O 명령에 응답할 수 없습니다. 즉, 이 드라이브는 활성화 중에 데이터를 제공하지 않습니다. 이 드라이브의 데이터에 액세스하는 응용 프로그램은 펌웨어 활성화가 완료될 때까지 응답을 기다려야 합니다. 사용되는 cmdlet의 예는 다음과 같습니다.

   ```powershell 
   $pd | Update-StorageFirmware -ImagePath C:\Firmware\J3E160@3.enc -SlotNumber 0
   $pd | Get-StorageFirmwareInformation

   SupportsUpdate        : True
   NumberOfSlots         : 1
   ActiveSlotNumber      : 0
   SlotNumber            : {0}
   IsSlotWritable        : {True}
   FirmwareVersionInSlot : {J3E160@3}
   ```

일반적으로 드라이브는 새로운 펌웨어 이미지를 활성화할 때 I/O 요청을 완료하지 않습니다. 드라이브에서 활성화에 걸리는 시간은 업데이트하는 펌웨어의 설계 및 유형에 따라 다릅니다. 업데이트 시간은 5초 미만에서 30초 이상까지 걸리는 것으로 관찰되었습니다.

이 드라이브는 다음에 보이는 것처럼 5.8초 이내에 펌웨어 업데이트를 수행했습니다.

```powershell 
Measure-Command {$pd | Update-StorageFirmware -ImagePath C:\\Firmware\\J3E16101.enc -SlotNumber 0}

 Days : 0
 Hours : 0
 Minutes : 0
 Seconds : 5
 Milliseconds : 791
 Ticks : 57913910
 TotalDays : 6.70299884259259E-05
 TotalHours : 0.00160871972222222
 TotalMinutes : 0.0965231833333333
 TotalSeconds : 5.791391
 TotalMilliseconds : 5791.391
 ```

## <a name="updating-drives-in-production"></a>프로덕션에서 드라이브 업데이트

프로덕션 환경에 서버를 배치하기 전에 솔루션(저장소 엔클로저, 드라이브 및 서버)을 판매하고 지원하는 하드웨어 공급업체 또는 OEM에서 권장하는 펌웨어로 드라이브의 펌웨어를 업데이트하는 것이 좋습니다.

프로덕션 환경에 서버를 배치했으면 서버에 대한 변경을 최소화하는 것이 좋습니다. 그러나 솔루션 공급업체가 드라이브에 대한 매우 중요한 펌웨어 업데이트가 있다고 알려주는 경우도 있습니다. 이 경우 드라이브 펌웨어 업데이트를 적용하기 전에 다음과 같은 몇 가지를 수행하는 것이 바람직합니다.

1. 펌웨어 릴리스 정보를 검토하고 환경에 영향을 줄 수 있는 문제가 업데이트를 통해 해결되는지, 부정적인 영향을 줄 수 있는 알려진 문제가 펌웨어에 포함되어 있지 않은지를 확인합니다.

2. 동일한 드라이브(동일한 드라이브의 여러 수정 버전이 있는 경우 드라이브의 수정 버전 포함)가 있는 랩의 서버에 펌웨어를 설치하고 새 펌웨어가 로드된 상태에서 드라이브를 테스트합니다. 가상 부하 테스트를 수행하는 방법에 대한 자세한 내용은 [가상 워크로드를 사용하여 저장소 공간 성능 테스트](https://technet.microsoft.com/library/dn894707.aspx)를 참조하세요.

## <a name="automated-firmware-updates-with-storage-spaces-direct"></a>저장소 공간 다이렉트로 자동 펌웨어 업데이트

Windows Server 2016에는 저장소 공간 다이렉트 배포에 대한 상태 관리 서비스가 포함되어 있습니다(Microsoft Azure Stack 솔루션 포함). 상태 관리 서비스의 주요 목적은 하드웨어 배포의 모니터링 및 관리를 용이하게 하는 것입니다. 관리 기능의 일부로, 워크로드를 오프라인을 전환하거나 가동 중지 시간이 발생하는 일 없이 전체 클러스터에 드라이브 펌웨어를 롤아웃하는 기능이 포함되어 있습니다. 이 기능은 정책 기반이며 관리자가 직접 제어합니다.

상태 관리 서비스를 사용하여 클러스터 전체에 펌웨어를 롤아웃하는 것은 매우 간단하며 다음 단계가 포함됩니다.

-   저장소 공간 다이렉트 클러스터의 일부가 될 HDD 및 SSD 드라이브를 식별하고, 이러한 드라이브가 펌웨어 업데이트를 수행하는 Windows를 지원하는지 여부를 식별합니다.
-   지원되는 구성 요소 xml 파일에 해당 드라이브를 나열합니다.
-   지원되는 구성 요소 xml에 있어야 할 드라이브의 예상 펌웨어 버전을 식별합니다(펌웨어 이미지의 위치 경로 포함).
-   클러스터 DB에 xml 파일을 업로드합니다.

이 시점에서 상태 관리 서비스는 xml을 구문 분석하고 원하는 펌웨어 버전이 배포되지 않은 드라이브를 식별합니다. 그런 다음 영향받는 드라이브에서 I/O를 외부로 리디렉션하고(노드 단위로) 펌웨어를 업데이트합니다. 저장소 공간 다이렉트 클러스터는 여러 서버 노드에 데이터를 분산하여 복원력을 얻습니다. 상태 관리 서비스는 드라이브를 업데이트하기 위해 전체 노드를 격리할 수 있습니다. 노드는 업데이트되면 저장소 공간에서 복구를 시작하여, 다음 노드로 이동하기 전에 클러스터 전체에서 모든 데이터 복사본이 상호 동기화되도록 합니다. 펌웨어가 롤아웃되는 동안 저장소 공간이 "저하됨" 작동 모드로 전환되는 것은 정상적인 현상입니다.

새로운 펌웨어 이미지를 안정적으로 롤아웃하고 충분히 검증하기 위해 여러 서버의 업데이트 간에 상당한 지연이 존재합니다. 기본적으로 상태 관리 서비스는 두 번째 서버<sup>를</sup> 업데이트하기까지 7일 동안 대기합니다. 그 이후의 서버(<sup>세 번째</sup>, <sup>네 번째</sup>...)는 1일 지연으로 업데이트됩니다. 관리자는 펌웨어가 불안정하거나 문제가 있다고 생각하는 경우 언제든지 상태 관리 서비스에 의한 추가 롤아웃을 중지할 수 있습니다. 펌웨어를 미리 검증하여 롤아웃을 더 빠르게 진행하려는 경우 이러한 기본값을 며칠에서 몇 시간 또는 몇 분으로 수정할 수 있습니다.

일반 저장소 공간 다이렉트 클러스터에 대한 지원되는 구성 요소 xml의 예는 다음과 같습니다.

```xml
 <Components>
     <Disks>
        <Disk>
            <Manufacturer>Contoso</Manufacturer>
            <Model>XYZ9000</Model>
            <AllowedFirmware>
              <Version>2.0</Version>
              <Version>2.1>/Version>
              <Version>2.2</Version>
            </AllowedFirmware>
            <TargetFirmware>
              <Version>2.2</Version>
              <BinaryPath>\\path\to\image.bin</BinaryPath>
            </TargetFirmware>
        </Disk>
        ...
        ...
    </Disks>
 </Components>
```

새 펌웨어 롤아웃을 이 저장소 공간 다이렉트 클러스터에서 시작하려면 .xml 파일을 클러스터 DB에 업로드하면 됩니다.

```powershell
$SpacesDirect = Get-StorageSubSystem Clus*

$CurrentDoc = $SpacesDirect | Get-StorageHealthSetting -Name "System.Storage.SupportedComponents.Document"

$CurrentDoc.Value | Out-File <Path>
```

Visual Studio Code 또는 메모장 등 자주 사용하는 편집기에서 파일을 편집하고 저장합니다.

```powershell
$NewDoc = Get-Content <Path> | Out-String

$SpacesDirect | Set-StorageHealthSetting -Name "System.Storage.SupportedComponents.Document" -Value $NewDoc
```

작업의 상태 관리 서비스를 참조 하세요. 해당 롤아웃 메커니즘에 자세히 알아보기를 원하는 경우이 동영상: https://channel9.msdn.com/Blogs/windowsserver/Update-Drive-Firmware-Without-Downtime-in-Storage-Spaces-Direct

## <a name="frequently-asked-questions"></a>질문과 대답

[드라이브 펌웨어 업데이트 문제 해결](troubleshoot-firmware-update.md)도 참조하시기 바랍니다.

### <a name="will-this-work-on-any-storage-device"></a>업데이트는 모든 저장 장치에서 작동하나요?

펌웨어에서 올바른 명령을 구현한 저장 장치에서만 작동합니다. Get StorageFirmwareInformation cmdlet은 드라이브의 펌웨어가 올바른 명령(SATA/NVMe의 경우)을 지원하는지, 공급업체 및 OEM이 HLK 테스트에서 이 동작을 테스트할 수 있는지를 보여 줍니다.

### <a name="after-i-update-a-sata-drive-it-reports-to-no-longer-support-the-update-mechanism-is-something-wrong-with-the-drive"></a>SATA 드라이브를 업데이트한 후, 업데이트 메커니즘이 더 이상 지원되지 않는다고 보고합니다. 드라이브에 문제가 있나요?

아니요. 새 펌웨어에서 업데이트를 더 이상 허용하지 않는 경우가 아니면 드라이브는 문제가 없습니다. 드라이브 기능의 캐시된 버전이 올바르지 않은 알려진 문제가 있습니다. "Update-StorageProviderCache -DiscoveryLevel Full"을 실행하면 드라이브 기능이 다시 열거되고 캐시된 복사본이 업데이트됩니다. 공간 다이렉트 클러스터에서 펌웨어 업데이트 또는 완전한 롤아웃을 시작하기 전에 위 명령을 실행할 것을 권장합니다.

### <a name="can-i-update-firmware-on-my-san-through-this-mechanism"></a>이 메커니즘을 통해 SAN에서 펌웨어를 업데이트할 수 있나요?
아니요. SAN은 이러한 유지 관리 작업을 위한 자체 유틸리티와 인터페이스를 가지고 있습니다. 이 새로운 메커니즘은 SATA, SAS 또는 NVMe 장치 같이 직접 연결된 저장소를 위한 것입니다.

### <a name="from-where-do-i-get-the-firmware-image"></a>펌웨어 이미지를 어디에서 구할 수 있나요?

항상 OEM, 솔루션 공급업체 또는 드라이브 공급업체로부터 직접 펌웨어를 받아야 하며, 다른 곳에서 다운로드할 수 없습니다. Windows는 드라이브에 이미지를 가져오기 위한 메커니즘을 제공하지만 무결성을 확인할 수는 없습니다.

### <a name="will-this-work-on-clustered-drives"></a>클러스터된 드라이브에서 이 작업이 작동하나요?

클러스터된 드라이브에서도 cmdlet이 작동하지만, 상태 관리 서비스 오케스트레이션은 실행 중인 워크로드에 대한 I/O 영향을 완화합니다. 클러스터된 드라이브에서 cmdlet을 직접 사용하는 경우 I/O가 정지할 수 있습니다. 일반적으로 기본 드라이브에 워크로드가 없거나 최소 수준일 때 드라이브 펌웨어 업데이트를 수행하는 것이 가장 좋습니다.

### <a name="what-happens-when-i-update-firmware-on-storage-spaces"></a>저장소 공간에서 펌웨어를 업데이트하는 경우 어떤 일이 발생하나요?

저장소 공간 다이렉트에 상태 관리 서비스가 배포된 Windows Server 2016에서는 드라이브가 Windows Server의 펌웨어 업데이트를 지원한다고 가정하여, 워크로드를 오프라인 상태로 전환하지 않고도 이 작업을 수행할 수 있습니다.

### <a name="what-happens-if-the-update-fails"></a>업데이트가 실패하는 경우 어떤 일이 발생하나요?

업데이트는 다양 한 이유로 실패할 수 있습니다, 그리고 그 중 일부는: 1) 드라이브의 펌웨어를 업데이트 하는 Windows에 대 한 올바른 명령을 지원 하지 않습니다. 이 경우 새 펌웨어 이미지는 활성화되지 않으며 드라이브는 계속해서 이전 이미지로 작동합니다. 2) 이미지를 이 드라이브에 다운로드 또는 적용할 수 없습니다(버전 불일치, 손상된 이미지...). 이 경우 드라이브에서 활성화 명령이 실패합니다. 그러나 이전 펌웨어 이미지는 계속해서 작동합니다.

펌웨어 업데이트 후 드라이브에서 전혀 반응이 없으면 드라이브 펌웨어 자체의 버그일 수 있습니다. 프로덕션 환경에 배치하기 전에 랩 환경에서 모든 펌웨어 업데이트를 테스트하세요. 드라이브 교체가 유일한 해결책일 수 있습니다.

자세한 내용은 [드라이브 펌웨어 업데이트 문제 해결](troubleshoot-firmware-update.md)에서 확인하시기 바랍니다.

### <a name="how-do-i-stop-an-in-progress-firmware-roll-out"></a>진행 중인 펌웨어 롤아웃을 어떻게 중지하나요?

PowerShell에서 다음을 통해 롤아웃을 중지합니다.
```powershell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.Enabled" -Value false
```

### <a name="i-am-seeing-an-access-denied-or-path-not-found-error-during-roll-out-how-do-i-fix-this"></a>롤아웃 도중에 액세스 거부 또는 경로를 찾을 수 없음 오류가 표시됩니다. 어떻게 해결할 수 있나요?

업데이트에 사용할 펌웨어 이미지를 모든 클러스터 노드에서 액세스할 수 있는지 확인합니다. 이를 위한 가장 쉬운 방법은 해당 이미지를 클러스터 공유 볼륨에 두는 것입니다.
