---
title: 불연속 장치 할당을 사용 하 여 그래픽 장치 배포
description: DDA를 사용 하 여 Windows Server에서 그래픽 장치를 배포 하는 방법을 알아봅니다.
ms.prod: windows-server
ms.service: na
ms.technology: hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: chrishuybregts
ms.author: chrihu
ms.assetid: 67a01889-fa36-4bc6-841d-363d76df6a66
ms.openlocfilehash: 3b37abaf5a2341aff66ff0064ecc4f52faf47f06
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392999"
---
# <a name="deploy-graphics-devices-using-discrete-device-assignment"></a>불연속 장치 할당을 사용 하 여 그래픽 장치 배포

>적용 대상: Microsoft Hyper-V Server 2016, Windows Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019  

Windows Server 2016 부터는 불연속 장치 할당 또는 DDA를 사용 하 여 전체 PCIe 장치를 VM에 전달할 수 있습니다.  이렇게 하면 장치 기본 드라이버를 활용할 수 있는 동안 VM 내에서 [NVMe 저장소](./Deploying-storage-devices-using-dda.md) 또는 그래픽 카드와 같은 장치에 고성능 액세스할 수 있습니다.  작동 하는 장치에 대 한 자세한 내용은 [개별 장치 할당을 사용 하 여 장치 배포 계획](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) (영문)을 참조 하세요.

불연속 장치 할당을 사용 하는 장치를 사용 하는 세 가지 단계가 있습니다.
-   불연속 장치 할당을 위한 VM 구성
-   호스트 파티션에서 장치를 분리 합니다.
-   게스트 VM에 장치 할당

모든 명령은 Windows PowerShell 콘솔의 호스트에서 관리자 권한으로 실행할 수 있습니다.

## <a name="configure-the-vm-for-dda"></a>DDA에 대 한 VM 구성
불연속 장치 할당은 Vm에 몇 가지 제한을 적용 하며 다음 단계를 수행 해야 합니다.

1.  을 실행 하 여 TurnOff에 대 한 VM의 "자동 중지 작업"을 구성 합니다.

```
Set-VM -Name VMName -AutomaticStopAction TurnOff
```

### <a name="some-additional-vm-preparation-is-required-for-graphics-devices"></a>그래픽 장치에 몇 가지 추가 VM 준비가 필요 합니다.

일부 하드웨어는 특정 방식으로 구성 된의 경우 더 나은 성능을 발휘 합니다.  하드웨어에 대 한 다음 구성이 필요한 지 여부에 대 한 자세한 내용은 하드웨어 공급 업체에 문의 하세요. 추가 세부 정보는 [개별 장치 할당을 사용 하 여 장치를 배포 하기 위한 계획](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) 및이 [블로그 게시물](https://techcommunity.microsoft.com/t5/Virtualization/Discrete-Device-Assignment-GPUs/ba-p/382266) 에서 찾을 수 있습니다.

1. CPU에서 쓰기 결합 사용
   ```
   Set-VM -GuestControlledCacheTypes $true -VMName VMName
   ```
2. 32 비트 MMIO 공간 구성
   ```
   Set-VM -LowMemoryMappedIoSpace 3Gb -VMName VMName
   ```
3. 32 비트 이상 MMIO 공간 구성
   ```
   Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName VMName
   ```
   > [!TIP] 
   > 위의 MMIO 공간 값은 단일 GPU로 시험해 볼 수 있도록 설정 하기에 적합 한 값입니다.  VM을 시작한 후 장치에서 리소스가 부족 한 경우와 관련 된 오류를 보고 하는 경우 이러한 값을 수정 해야 합니다. MMIO 요구 사항을 정확 하 게 계산 하는 방법을 알아보려면 [불연속 장치 할당을 사용 하 여 장치 배포 계획](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) 을 참조 하세요.

## <a name="dismount-the-device-from-the-host-partition"></a>호스트 파티션에서 장치를 분리 합니다.
### <a name="optional---install-the-partitioning-driver"></a>선택 사항-분할 드라이버 설치
불연속 장치 할당은 하드웨어 venders 장치에 보안 완화 드라이버를 제공 하는 기능을 제공 합니다.  이 드라이버는 게스트 VM에 설치 되는 장치 드라이버와 동일 하지 않습니다.  이 드라이버를 제공 하는 것은 하드웨어 공급 업체의 재량에 따라 결정 됩니다. 그러나 장치를 제공 하는 경우 호스트 파티션에서 장치를 분리 하기 전에 설치 하세요.  하드웨어 공급 업체에 연락 하 여 완화 드라이버가 있는지에 대 한 자세한 내용을 확인 하세요.
> 분할 드라이버를 제공 하지 않으면 분리 하는 동안 `-force` 옵션을 사용 하 여 보안 경고를 무시 해야 합니다. [불연속 장치 할당을 사용 하 여 장치를 배포 하기 위한 계획](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md)에서이 작업을 수행 하는 보안 문제에 대해 자세히 알아보세요.

### <a name="locating-the-devices-location-path"></a>장치의 위치 경로 찾기
PCI 위치 경로는 호스트에서 장치를 분리 하 고 탑재 하는 데 필요 합니다.  예제 위치 경로 `"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"`는 다음과 같습니다.  위치 경로에 대 한 자세한 내용은 다음 위치에서 찾을 수 있습니다. [불연속 장치 할당을 사용 하 여 장치 배포를 계획](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md)합니다.

### <a name="disable-the-device"></a>장치 사용 안 함
Device Manager 또는 PowerShell을 사용 하 여 장치가 "사용 안 함" 인지 확인 합니다.  

### <a name="dismount-the-device"></a>장치 분리
공급 업체에서 완화 드라이버를 제공 했는지 여부에 따라 "-force" 옵션을 사용 해야 합니다.
- 완화 드라이버가 설치 된 경우
  ```
  Dismount-VMHostAssignableDevice -LocationPath $locationPath
  ```
- 완화 드라이버가 설치 되지 않은 경우
  ```
  Dismount-VMHostAssignableDevice -force -LocationPath $locationPath
  ```

## <a name="assigning-the-device-to-the-guest-vm"></a>게스트 VM에 장치 할당
마지막 단계는 VM이 장치에 액세스할 수 있어야 한다고 Hyper-v에 지시 하는 것입니다.  위에서 찾은 위치 경로 외에도 vm의 이름을 알아야 합니다.

```
Add-VMAssignableDevice -LocationPath $locationPath -VMName VMName
```

## <a name="whats-next"></a>다음 단계
장치가 VM에 성공적으로 탑재 되 면 이제 운영 체제 미 설치 시스템에서 실행 되는 경우와 마찬가지로 해당 VM을 시작 하 고 장치와 상호 작용할 수 있습니다.  즉, 이제 VM에 하드웨어 공급 업체의 드라이버를 설치할 수 있으며 응용 프로그램은 해당 하드웨어를 볼 수 있습니다.  게스트 VM에서 장치 관리자를 열고 하드웨어가 표시 되는 것을 확인 하 여이를 확인할 수 있습니다.

## <a name="removing-a-device-and-returning-it-to-the-host"></a>장치를 제거 하 고 호스트에 반환
장치를 원래 상태로 되돌리려면 VM을 중지 하 고 다음을 실행 해야 합니다.
```
#Remove the device from the VM
Remove-VMAssignableDevice -LocationPath $locationPath -VMName VMName
#Mount the device back in the host
Mount-VMHostAssignableDevice -LocationPath $locationPath
```
그런 다음 장치 관리자에서 장치를 다시 사용 하도록 설정 하면 호스트 운영 체제가 장치와 상호 작용할 수 있습니다.

## <a name="examples"></a>예

### <a name="mounting-a-gpu-to-a-vm"></a>VM에 GPU 탑재
이 예제에서는 PowerShell을 사용 하 여 "ddatest1" 라는 VM을 구성 하 고 제조업체 NVIDIA에서 사용 가능한 첫 번째 GPU를 가져와 VM에 할당 합니다.  
```
#Configure the VM for a Discrete Device Assignment
$vm =   "ddatest1"
#Set automatic stop action to TurnOff
Set-VM -Name $vm -AutomaticStopAction TurnOff
#Enable Write-Combining on the CPU
Set-VM -GuestControlledCacheTypes $true -VMName $vm
#Configure 32 bit MMIO space
Set-VM -LowMemoryMappedIoSpace 3Gb -VMName $vm
#Configure Greater than 32 bit MMIO space
Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName $vm

#Find the Location Path and disable the Device
#Enumerate all PNP Devices on the system
$pnpdevs = Get-PnpDevice -presentOnly
#Select only those devices that are Display devices manufactured by NVIDIA
$gpudevs = $pnpdevs |where-object {$_.Class -like "Display" -and $_.Manufacturer -like "NVIDIA"}
#Select the location path of the first device that's available to be dismounted by the host.
$locationPath = ($gpudevs | Get-PnpDeviceProperty DEVPKEY_Device_LocationPaths).data[0]
#Disable the PNP Device
Disable-PnpDevice  -InstanceId $gpudevs[0].InstanceId

#Dismount the Device from the Host
Dismount-VMHostAssignableDevice -force -LocationPath $locationPath

#Assign the device to the guest VM.
Add-VMAssignableDevice -LocationPath $locationPath -VMName $vm
```
