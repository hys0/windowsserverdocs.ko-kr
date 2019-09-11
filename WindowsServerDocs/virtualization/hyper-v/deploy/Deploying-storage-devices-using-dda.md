---
title: 불연속 장치 할당을 사용 하 여 NVMe 저장소 장치 배포
description: DDA를 사용 하 여 저장소 장치를 배포 하는 방법을 알아봅니다.
ms.prod: windows-server-threshold
ms.service: na
ms.technology: hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: chrishuybregts
ms.author: chrihu
ms.assetid: 1c36107e-78c9-4ec0-a313-6ed557ac0ffc
ms.openlocfilehash: 001d8addba2cdb8cbbd5d72ffa224d16f62d1245
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70872118"
---
# <a name="deploy-nvme-storage-devices-using-discrete-device-assignment"></a>불연속 장치 할당을 사용 하 여 NVMe 저장소 장치 배포

>적용 대상: Microsoft Hyper-V Server 2016, Windows Server 2016

Windows Server 2016 부터는 불연속 장치 할당 또는 DDA를 사용 하 여 전체 PCIe 장치를 VM에 전달할 수 있습니다.  이렇게 하면 장치 기본 드라이버를 활용할 수 있는 동안 VM 내에서 NVMe 저장소 또는 그래픽 카드와 같은 장치에 고성능 액세스할 수 있습니다.  작동 하는 장치에 대 한 자세한 내용은 [개별 장치 할당을 사용 하 여 장치 배포 계획](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) (영문)을 참조 하세요. DDA에서 장치를 사용 하는 세 가지 단계가 있습니다.
-   DDA에 대 한 VM 구성
-   호스트 파티션에서 장치를 분리 합니다.
-   게스트 VM에 장치 할당

모든 명령은 Windows PowerShell 콘솔의 호스트에서 관리자 권한으로 실행할 수 있습니다.

## <a name="configure-the-vm-for-dda"></a>DDA에 대 한 VM 구성
불연속 장치 할당은 Vm에 몇 가지 제한을 적용 하며 다음 단계를 수행 해야 합니다.

1.  을 실행 하 여 TurnOff에 대 한 VM의 "자동 중지 작업"을 구성 합니다.

```
Set-VM -Name VMName -AutomaticStopAction TurnOff
```

## <a name="dismount-the-device-from-the-host-partition"></a>호스트 파티션에서 장치를 분리 합니다.

### <a name="locating-the-devices-location-path"></a>장치의 위치 경로 찾기
PCI 위치 경로는 호스트에서 장치를 분리 하 고 탑재 하는 데 필요 합니다.  예제 위치 경로 `"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"`는 다음과 같습니다.   위치 경로에 대 한 자세한 내용은 다음 위치에서 찾을 수 있습니다. [불연속 장치 할당을 사용 하 여 장치 배포를 계획](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md)합니다.

### <a name="disable-the-device"></a>장치 사용 안 함
Device Manager 또는 PowerShell을 사용 하 여 장치가 "사용 안 함" 인지 확인 합니다.  

### <a name="dismount-the-device"></a>장치 분리
```
Dismount-VMHostAssignableDevice -LocationPath $locationPath
```

## <a name="assigning-the-device-to-the-guest-vm"></a>게스트 VM에 장치 할당
마지막 단계는 VM이 장치에 액세스할 수 있어야 한다고 Hyper-v에 지시 하는 것입니다.  위에서 찾은 위치 경로 외에도 vm의 이름을 알아야 합니다.

```
Add-VMAssignableDevice -LocationPath $locationPath -VMName VMName
```

## <a name="whats-next"></a>새로운 기능
장치가 VM에 성공적으로 탑재 되 면 이제 운영 체제 미 설치 시스템에서 실행 되는 경우와 마찬가지로 해당 VM을 시작 하 고 장치와 상호 작용할 수 있습니다.  게스트 VM에서 장치 관리자를 열고 하드웨어가 표시 되는 것을 확인 하 여이를 확인할 수 있습니다.

## <a name="removing-a-device-and-returning-it-to-the-host"></a>장치를 제거 하 고 호스트에 반환
장치를 원래 상태로 되돌리려면 VM을 중지 하 고 다음을 실행 해야 합니다.
```
#Remove the device from the VM
Remove-VMAssignableDevice -LocationPath $locationPath -VMName VMName
#Mount the device back in the host
Mount-VMHostAssignableDevice -LocationPath $locationPath
```
그런 다음 장치 관리자에서 장치를 다시 사용 하도록 설정 하면 호스트 운영 체제가 장치와 상호 작용할 수 있습니다.
