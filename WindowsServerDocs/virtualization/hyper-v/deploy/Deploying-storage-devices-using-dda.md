---
title: 불연속 장치 할당을 사용 하 여 NVMe 저장소 장치를 배포 합니다.
description: DDA를 사용 하 여 저장소 장치를 배포 하는 방법 알아보기
ms.prod: windows-server-threshold
ms.service: na
ms.technology: hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: chrishuybregts
ms.author: chrihu
ms.assetid: 1c36107e-78c9-4ec0-a313-6ed557ac0ffc
ms.openlocfilehash: d6fe54789d37386d5dc782ef8a2ca26b47adc69e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841364"
---
# <a name="deploy-nvme-storage-devices-using-discrete-device-assignment"></a>불연속 장치 할당을 사용 하 여 NVMe 저장소 장치를 배포 합니다.

>적용 대상: Microsoft Hyper-V Server 2016, Windows Server 2016

Windows Server 2016부터 전체 PCIe 장치를 VM에 전달할 불연속 장치 할당 또는 DDA를 사용할 수 있습니다.  장치 기본 드라이버를 활용 하는 동안 NVMe storage 또는 VM 내에서 그래픽 카드와 같은 장치에 대 한 고성능 액세스를 하면이 있습니다.  방문 하십시오 합니다 [불연속 장치 할당을 사용 하 여 배포 장치에 대 한 계획](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) 등 가능한 보안 이란 어떤 장치 작업에 대 한 자세한 내용은 합니다. DDA를 사용 하 여 장치를 사용 하는 방법은 세 가지 단계가 있습니다.
-   DDA에 대 한 VM 구성
-   호스트 파티션에에서 장치를 분리 합니다.
-   게스트 VM에 장치 할당

모든 명령은 관리자 권한으로 Windows PowerShell 콘솔에서 호스트에서 실행할 수 있습니다.

## <a name="configure-the-vm-for-dda"></a>DDA에 대 한 VM 구성
불연속 장치 할당 Vm에 몇 가지 제한을 적용 하 고 다음 단계를 수행 해야 합니다.

1.  "자동 중지 작업을" vm TurnOff 실행 하 여 구성

```
Set-VM -Name VMName -AutomaticStopAction TurnOff
```

## <a name="dismount-the-device-from-the-host-partition"></a>호스트 파티션에에서 장치를 분리 합니다.

### <a name="locating-the-devices-location-path"></a>장치의 위치 경로 찾기
PCI 위치 경로 호스트에서 장치를 탑재 및 분리 해야 합니다.  예를 들어 위치 경로 다음과 같습니다: `"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"`합니다.   배치에 대 한 자세한 내용은 위치 경로 여기: [불연속 장치 할당을 사용 하 여 배포 장치에 대 한 계획](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md)합니다.

### <a name="disable-the-device"></a>장치를 사용 하지 않도록 설정
장치 관리자 또는 PowerShell를 사용 하 여, 장치는 "사용할 수 없습니다." 확인  

### <a name="dismount-the-device"></a>장치를 분리 합니다.
```
Dismount-VMHostAssignableDevice -LocationPath $locationPath
```

## <a name="assigning-the-device-to-the-guest-vm"></a>게스트 VM에 장치 할당
마지막 단계 하기가 Hyper-v VM을 장치에 액세스할 수 있어야 한다는 것입니다.  위에서 찾은 위치 경로 외에도 vm의 이름을 확인 해야 합니다.

```
Add-VMAssignableDevice -LocationPath $locationPath -VMName VMName
```

## <a name="whats-next"></a>다음 단계
VM에서 장치를 성공적으로 탑재 되 면 해당 VM을 시작 하 고 평소와 같이 운영 체제 미 설치 시스템에서 실행 했던 경우 장치와 상호 작용 하는 일을 할 이제 합니다.  게스트 VM의 장치 관리자를 열고 하드웨어 이제 표시 되는지 확인 하 여이 확인할 수 있습니다.

## <a name="removing-a-device-and-returning-it-to-the-host"></a>장치를 제거 하 고 호스트에 반환
그 장치를 원래 상태로 다시 반환 하려는 경우 VM을 중지 하 고 다음을 실행 해야 합니다.
```
#Remove the device from the VM
Remove-VMAssignableDevice -LocationPath $locationPath -VMName VMName
#Mount the device back in the host
Mount-VMHostAssignableDevice -LocationPath $locationPath
```
다음 다시 설정 하는 장치 관리자에서 장치 및 호스트 운영 체제를 다시 장치와 상호 작용할 수 있습니다.
