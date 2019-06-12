---
title: 불연속 장치 할당을 사용 하 여 그래픽 장치를 배포 합니다.
description: DDA를 사용 하 여 Windows Server의 그래픽 장치를 배포 하는 방법 알아보기
ms.prod: windows-server-threshold
ms.service: na
ms.technology: hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: chrishuybregts
ms.author: chrihu
ms.assetid: 67a01889-fa36-4bc6-841d-363d76df6a66
ms.openlocfilehash: 6c528535fd34f57957a37992843933d4cd9f8824
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447874"
---
# <a name="deploy-graphics-devices-using-discrete-device-assignment"></a>불연속 장치 할당을 사용 하 여 그래픽 장치를 배포 합니다.

>적용 대상: Microsoft Hyper-V Server 2016, Windows Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019  

Windows Server 2016부터 전체 PCIe 장치를 VM에 전달할 불연속 장치 할당 또는 DDA를 사용할 수 있습니다.  이렇게 하면 같은 장치에 대 한 고성능 액세스 [NVMe 저장소](./Deploying-storage-devices-using-dda.md) 또는 장치 기본 드라이버를 활용 하는 동안 VM 내에서 그래픽 카드.  방문 하십시오 합니다 [불연속 장치 할당을 사용 하 여 배포 장치에 대 한 계획](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) 등 가능한 보안 이란 어떤 장치 작업에 대 한 자세한 내용은 합니다.

불연속 장치 할당을 사용 하 여 장치를 사용 하는 방법은 세 가지 단계가 있습니다.
-   불연속 장치 할당에 대 한 VM 구성
-   호스트 파티션에에서 장치를 분리 합니다.
-   게스트 VM에 장치 할당

모든 명령은 관리자 권한으로 Windows PowerShell 콘솔에서 호스트에서 실행할 수 있습니다.

## <a name="configure-the-vm-for-dda"></a>DDA에 대 한 VM 구성
불연속 장치 할당 Vm에 몇 가지 제한을 적용 하 고 다음 단계를 수행 해야 합니다.

1.  "자동 중지 작업을" vm TurnOff 실행 하 여 구성

```
Set-VM -Name VMName -AutomaticStopAction TurnOff
```

### <a name="some-additional-vm-preparation-is-required-for-graphics-devices"></a>그래픽 장치에 대 한 몇 가지 추가 VM 준비 필수임

일부 하드웨어에서 VM을 특정 방식으로 구성 된 경우 성능은 향상.  하드웨어에 대 한 다음과 같은 구성이 필요 여부에 대 한 내용은 하세요 하드웨어 공급 업체에 연락 합니다. 추가 세부 정보에서 확인할 수 있습니다 [불연속 장치 할당을 사용 하 여 배포 장치에 대 한 계획](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) 이 고 [블로그 게시물.](https://blogs.technet.microsoft.com/virtualization/2015/11/23/discrete-device-assignment-gpus/)

1. CPU에서 쓰기 조합 사용
   ```
   Set-VM -GuestControlledCacheTypes $true -VMName VMName
   ```
2. 32 비트 MMIO 공간 구성
   ```
   Set-VM -LowMemoryMappedIoSpace 3Gb -VMName VMName
   ```
3. 32 비트 MMIO 공간 보다 큰 구성
   ```
   Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName VMName
   ```
   Note 위의 MMIO 공간 값은 단일 GPU를 사용 하 여 실험에 대해 설정할 적절 한 값입니다.  VM을 시작한 후 장치는 리소스가 부족와 관련 된 오류를 보고, 이러한 값을 수정 해야 가능성이 높습니다.  또한 여러 Gpu를 할당 하는 경우에 이러한 값을 증가 해야 합니다.

## <a name="dismount-the-device-from-the-host-partition"></a>호스트 파티션에에서 장치를 분리 합니다.
### <a name="optional---install-the-partitioning-driver"></a>선택 사항-분할 드라이버 설치
불연속 장치 할당 하드웨어 공급 업체 자신의 장치를 사용 하 여 보안 완화 드라이버를 제공 하는 기능을 제공 합니다.  참고가이 드라이버는 게스트 VM에에서 설치 되는 장치 드라이버와 동일 합니다.  그러나 것에 하드웨어 공급 업체의 제공이 드라이버를 재량에 따라 최대를 제공 하는 경우 하세요 이전에 설치는 호스트 파티션에에서 장치를 분리 합니다.  연락 하 대 한 자세한 내용은 하드웨어 공급 업체는 완화 드라이버가 있는 경우
> 분할 드라이버가 제공 하는 경우 분리 하는 동안 사용 해야 합니다는 `-force` 보안 경고를 무시 하는 옵션입니다. 자세히 읽어보세요에서이 작업의 보안 의미 하는 방법에 대 한 [불연속 장치 할당을 사용 하 여 배포 장치에 대 한 계획](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md)합니다.

### <a name="locating-the-devices-location-path"></a>장치의 위치 경로 찾기
PCI 위치 경로 호스트에서 장치를 탑재 및 분리 해야 합니다.  예를 들어 위치 경로 다음과 같습니다: `"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"`합니다.  배치에 대 한 자세한 내용은 위치 경로 여기: [불연속 장치 할당을 사용 하 여 배포 장치에 대 한 계획](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md)합니다.

### <a name="disable-the-device"></a>장치를 사용 하지 않도록 설정
장치 관리자 또는 PowerShell를 사용 하 여, 장치는 "사용할 수 없습니다." 확인  

### <a name="dismount-the-device"></a>장치를 분리 합니다.
에 따라 경우 공급 업체 완화 드라이버를 제공 하거나 해야 사용 하는 "-강제로" 여부 옵션입니다.
- 완화 드라이버가 설치 된 경우
  ```
  Dismount-VMHostAssignableDevice -LocationPath $locationPath
  ```
- 완화 드라이버가 설치 되지 않은 경우
  ```
  Dismount-VMHostAssignableDevice -force -LocationPath $locationPath
  ```

## <a name="assigning-the-device-to-the-guest-vm"></a>게스트 VM에 장치 할당
마지막 단계 하기가 Hyper-v VM을 장치에 액세스할 수 있어야 한다는 것입니다.  위에서 찾은 위치 경로 외에도 vm의 이름을 확인 해야 합니다.

```
Add-VMAssignableDevice -LocationPath $locationPath -VMName VMName
```

## <a name="whats-next"></a>다음 단계
VM에서 장치를 성공적으로 탑재 되 면 해당 VM을 시작 하 고 평소와 같이 운영 체제 미 설치 시스템에서 실행 했던 경우 장치와 상호 작용 하는 일을 할 이제 합니다.  즉, VM의 하드웨어 공급 업체의 드라이버를 설치할 수 이제 응용 프로그램을 볼 수 있는 하드웨어 됩니다.  게스트 VM의 장치 관리자를 열고 하드웨어 이제 표시 되는지 확인 하 여이 확인할 수 있습니다.

## <a name="removing-a-device-and-returning-it-to-the-host"></a>장치를 제거 하 고 호스트에 반환
그 장치를 원래 상태로 다시 반환 하려는 경우 VM을 중지 하 고 다음을 실행 해야 합니다.
```
#Remove the device from the VM
Remove-VMAssignableDevice -LocationPath $locationPath -VMName VMName
#Mount the device back in the host
Mount-VMHostAssignableDevice -LocationPath $locationPath
```
다음 다시 설정 하는 장치 관리자에서 장치 및 호스트 운영 체제를 다시 장치와 상호 작용할 수 있습니다.

## <a name="examples"></a>예

### <a name="mounting-a-gpu-to-a-vm"></a>GPU VM에 탑재
이 예제에서는 PowerShell NVIDIA 제조업체에서 사용 가능한 첫 번째 GPU를 사용 하 여 VM에 할당 "ddatest1" 이라는 VM을 구성 하려면 사용 합니다.  
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
