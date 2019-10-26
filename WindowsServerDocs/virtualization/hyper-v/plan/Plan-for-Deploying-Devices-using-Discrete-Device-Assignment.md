---
title: 불연속 장치 할당을 사용 하 여 장치 배포 계획
description: Windows Server에서 DDA가 작동 하는 방식에 대해 알아봅니다.
ms.prod: windows-server
ms.service: na
ms.technology: hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: chrishuybregts
ms.author: chrihu
ms.date: 08/21/2019
ms.openlocfilehash: 114dd87b86bfffd1070229af57ae65deea2c2db0
ms.sourcegitcommit: 81198fbf9e46830b7f77dcd345b02abb71ae0ac2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72923870"
---
# <a name="plan-for-deploying-devices-using-discrete-device-assignment"></a>불연속 장치 할당을 사용 하 여 장치 배포 계획
>적용 대상: Microsoft Hyper-V Server 2016, Windows Server 2016, Microsoft Hyper-V Server 2019, Windows Server 2019

불연속 장치 할당을 통해 가상 머신 내에서 물리적 PCIe 하드웨어를 직접 액세스할 수 있습니다.  이 가이드에서는 불연속 장치 할당을 사용할 수 있는 장치 유형, 호스트 시스템 요구 사항, 가상 머신에 적용 되는 제한 사항 및 불연속 장치 할당의 보안 영향에 대해 설명 합니다.

불연속 장치 할당의 초기 릴리스에서는 Microsoft에서 공식적으로 지원 되는 두 가지 장치 클래스 (그래픽 어댑터 및 NVMe 저장소 장치)에 중점을 두었습니다.  다른 장치는 작동 하 고 하드웨어 공급 업체에서 해당 장치에 대 한 지원 문을 제공할 수 있습니다.  이러한 기타 장치의 경우 지원에 대 한 해당 하드웨어 공급 업체에 문의 하세요.

GPU 가상화의 다른 방법에 대 한 자세한 내용은 [Windows Server에서 gpu 가속 계획](plan-for-gpu-acceleration-in-windows-server.md)을 참조 하세요. 개별 장치 할당을 사용해 볼 준비가 되 면 불연속 장치 [할당을 사용 하 여 그래픽 장치 배포](../deploy/Deploying-graphics-devices-using-dda.md) 또는 [불연속 장치 할당을 사용 하 여 저장 장치 배포](../deploy/Deploying-storage-devices-using-dda.md) 로 이동 하 여 시작할 수 있습니다.

## <a name="supported-virtual-machines-and-guest-operating-systems"></a>지원 되는 Virtual Machines 및 게스트 운영 체제
불연속 장치 할당은 1 세대 또는 2 세대 Vm에 대해 지원 됩니다.  또한 지원 되는 게스트에는 Windows 10, Windows Server 2019, Windows Server 2016, Windows Server 2012r2 [KB 3133690](https://support.microsoft.com/kb/3133690) 이 적용 되 고 다양 한 [Linux OS](../supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md) 배포가 포함 됩니다.

## <a name="system-requirements"></a>시스템 요구 사항
[Windows server에 대 한 시스템 요구 사항](../../../get-started/System-Requirements--and-Installation.md) 및 [hyper-v에 대 한 시스템 요구 사항](../System-requirements-for-Hyper-V-on-Windows.md)외에도 불연속 장치 할당에는 PCIe 구성에 대해 운영 체제 제어를 부여할 수 있는 서버 클래스 하드웨어가 필요 합니다. 패브릭 (네이티브 PCI Express 컨트롤) 또한 PCIe 루트 복소수는 ACS ("Access Control Services")를 지원 해야 합니다 .이를 통해 Hyper-v에서 i/o MMU을 통해 모든 PCIe 트래픽을 강제로 적용할 수 있습니다.

이러한 기능은 일반적으로 서버의 BIOS에서 직접 노출 되지 않으며 다른 설정 뒤에 숨겨진 경우가 많습니다.  예를 들어, SR-IOV 지원과 BIOS에서 동일한 기능이 필요 합니다. "SR-IOV 사용"을 설정 해야 할 수 있습니다.  BIOS에서 올바른 설정을 확인할 수 없는 경우 시스템 공급 업체에 문의 하세요.

하드웨어에서 개별 장치 할당을 할 수 있는 하드웨어를 보장 하기 위해 엔지니어는 Hyper-v 사용 가능 호스트에서 실행 하 여 서버가 올바르게 설정 되어 있는지 여부를 테스트 하는 데 사용할 수 있는 [컴퓨터 프로필 스크립트](#machine-profile-script) 와 불연속 장치 할당.

## <a name="device-requirements"></a>장치 요구 사항
모든 PCIe 장치를 불연속 장치 할당과 함께 사용할 수 있는 것은 아닙니다.  예를 들어 레거시 (INTx) PCI 인터럽트를 활용 하는 이전 장치는 지원 되지 않습니다. Jake Oshin의 [블로그 게시물](https://blogs.technet.microsoft.com/virtualization/2015/11/20/discrete-device-assignment-machines-and-devices/) 에 대 한 세부 정보가 표시 됩니다. 그러나 소비자의 경우 [컴퓨터 프로필 스크립트](#machine-profile-script) 를 실행 하면 불연속 장치 할당에 사용할 수 있는 장치가 표시 됩니다.

장치 제조업체는 Microsoft 담당자에 게 연락 하 여 자세한 내용을 확인할 수 있습니다.

## <a name="device-driver"></a>장치 드라이버
불연속 장치 할당은 전체 PCIe 장치를 게스트 VM으로 전달 하므로 VM 내에서 장치를 탑재 하기 전에 호스트 드라이버를 설치할 필요가 없습니다.  호스트의 유일한 요구 사항은 장치의 [PCIe 위치 경로](#pcie-location-path) 를 확인할 수 있다는 것입니다.  장치를 식별 하는 데 도움이 되는 경우 장치 드라이버를 선택적으로 설치할 수 있습니다.  예를 들어 장치 드라이버가 호스트에 설치 되어 있지 않은 GPU가 Microsoft 기본 렌더링 장치로 표시 될 수 있습니다.  장치 드라이버가 설치 되어 있으면 제조업체와 모델이 표시 될 가능성이 높습니다.

장치가 게스트 내부에 탑재 되 면 이제 게스트 가상 컴퓨터 내에서 제조업체의 장치 드라이버를 정상적으로 설치할 수 있습니다.  

## <a name="virtual-machine-limitations"></a>가상 컴퓨터 제한 사항
불연속 장치 할당의 구현 방식 때문에, 장치가 연결 된 동안에는 가상 머신의 일부 기능이 제한 됩니다.  다음 기능은 사용할 수 없습니다.
- VM 저장/복원
- VM의 실시간 마이그레이션
- 동적 메모리 사용
- 고가용성 (HA) 클러스터에 VM 추가

## <a name="security"></a>보안
불연속 장치 할당은 전체 장치를 VM에 전달 합니다.  즉, 게스트 운영 체제에서 해당 장치의 모든 기능에 액세스할 수 있습니다. 펌웨어 업데이트와 같은 일부 기능은 시스템의 안정성에 악영향을 줄 수 있습니다. 따라서 호스트에서 장치를 분리 하는 경우 관리자에 게 많은 경고가 표시 됩니다. 불연속 장치 할당은 Vm의 테 넌 트를 신뢰할 수 있는 경우에만 사용 하는 것이 좋습니다.  

관리자가 신뢰할 수 없는 테 넌 트가 있는 장치를 사용 하려는 경우 호스트에 설치할 수 있는 장치 완화 드라이버를 만들 수 있는 기능이 장치 제조업체에 제공 되었습니다.  장치 완화 드라이버를 제공 하는지 여부에 대 한 자세한 내용은 장치 제조업체에 문의 하세요.

장치 완화 드라이버가 없는 장치에 대 한 보안 검사를 무시 하려는 경우에는 `-Force` 매개 변수를 `Dismount-VMHostAssignableDevice` cmdlet에 전달 해야 합니다.  이렇게 하면 해당 시스템의 보안 프로필을 변경 했으며 프로토타입 또는 신뢰할 수 있는 환경 에서만 권장 됩니다.

## <a name="pcie-location-path"></a>PCIe 위치 경로
호스트에서 장치를 분리 하 고 탑재 하려면 PCIe 위치 경로가 필요 합니다.  위치 경로 예제는 다음과 같습니다. `"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"`.   또한 [컴퓨터 프로필 스크립트](#machine-profile-script) 는 PCIe 장치의 위치 경로도 반환 합니다.

### <a name="getting-the-location-path-by-using-device-manager"></a>Device Manager를 사용 하 여 위치 경로 가져오기
![장치 관리자를 입력하고](../deploy/media/dda-devicemanager.png)
- Device Manager를 열고 장치를 찾습니다.  
- 장치를 마우스 오른쪽 단추로 클릭 하 고 "속성"을 선택 합니다.
- 세부 정보 탭으로 이동 하 여 속성 드롭다운에서 "위치 경로"를 선택 합니다.  
- "PCIROOT"로 시작 하는 항목을 마우스 오른쪽 단추로 클릭 하 고 "복사"를 선택 합니다.  이제 해당 장치에 대 한 위치 경로가 있습니다.

## <a name="mmio-space"></a>MMIO 공간
일부 장치, 특히 Gpu의 경우 해당 장치의 메모리를 액세스할 수 있도록 VM에 추가 MMIO 공간을 할당 해야 합니다. 기본적으로 각 VM은 낮은 MMIO 공간의 128MB 및 512MB에 할당 된 최대 512MB의 512MB로 시작 합니다. 그러나 장치에 더 많은 MMIO 공간이 필요할 수도 있고, 결합 된 요구 사항이 이러한 값을 초과 하도록 여러 장치를 전달할 수도 있습니다.  다음 명령을 사용 하 여 MMIO 공간을 변경 하는 작업은 바로 진행 되며 PowerShell에서 수행할 수 있습니다.

```PowerShell
Set-VM -LowMemoryMappedIoSpace 3Gb -VMName $vm
Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName $vm
```

할당할 MMIO 공간의 크기를 결정 하는 가장 쉬운 방법은 [컴퓨터 프로필 스크립트](#machine-profile-script)를 사용 하는 것입니다. 컴퓨터 프로필 스크립트를 다운로드 하 여 실행 하려면 PowerShell 콘솔에서 다음 명령을 실행 합니다.

```PowerShell
curl -o SurveyDDA.ps1 https://raw.githubusercontent.com/MicrosoftDocs/Virtualization-Documentation/live/hyperv-tools/DiscreteDeviceAssignment/SurveyDDA.ps1
.\SurveyDDA.ps1
```

할당 될 수 있는 장치의 경우 스크립트는 아래 예제와 같이 지정 된 장치에 대 한 MMIO 요구 사항을 표시 합니다.

```PowerShell
NVIDIA GRID K520
Express Endpoint -- more secure.
    ...
    And it requires at least: 176 MB of MMIO gap space
...
```

낮은 MMIO 공간은 32 비트 주소를 사용 하는 32 비트 운영 체제 및 장치 에서만 사용 됩니다. 대부분의 경우 32 비트 구성이 매우 일반적이 아니기 때문에 VM의 최대 MMIO 공간을 설정 하는 데 충분 합니다.

> [!IMPORTANT]
> VM에 MMIO 공간을 할당 하는 경우 사용자는 원하는 할당 된 모든 장치에 대 한 요청 된 MMIO 공간의 합계와 몇 MB의 MMIO 공간이 필요한 다른 가상 장치가 있는 경우 추가 버퍼에 대 한 MMIO 공간을 설정 해야 합니다. 위에서 설명한 기본 MMIO 값을 낮은 및 높은 MMIO의 버퍼 (각각 128, 512 MB)로 사용 합니다.

사용자가 위의 예제에서와 같이 단일 K520 GPU를 할당 하는 경우 VM의 MMIO 공간을 컴퓨터 프로필 스크립트 및 버퍼 (512 176)에 의해 출력 된 값으로 설정 해야 합니다. 사용자가 3 개의 K520 Gpu를 할당 하는 경우에는 MMIO 공간을 176 3 배 이상, 버퍼 또는 528 MB + 512 MB로 설정 해야 합니다.

MMIO 공간에 대 한 자세한 내용은 TechCommunity 블로그의 [개별 장치 할당-gpu](https://techcommunity.microsoft.com/t5/Virtualization/Discrete-Device-Assignment-GPUs/ba-p/382266) 를 참조 하세요.

## <a name="machine-profile-script"></a>컴퓨터 프로필 스크립트
서버가 올바르게 구성 되었는지와 불연속 장치 할당을 사용 하 여 전달할 수 있는 장치를 식별 하는 과정을 간소화 하기 위해 엔지니어 중 한 [SurveyDDA](https://github.com/Microsoft/Virtualization-Documentation/blob/live/hyperv-tools/DiscreteDeviceAssignment/SurveyDDA.ps1) 는 다음과 같은 PowerShell 스크립트를 포함 합니다.

스크립트를 사용 하기 전에 Hyper-v 역할이 설치 되어 있는지 확인 하 고 관리자 권한이 있는 PowerShell 명령 창에서 스크립트를 실행 하십시오.

불연속 장치 할당을 지원 하도록 시스템이 잘못 구성 된 경우이 도구는 오류 메시지를 표시 합니다. 도구가 올바르게 구성 된 시스템을 찾으면 PCIe 버스에서 찾을 수 있는 모든 장치를 열거 합니다.

검색 된 각 장치에 대해이 도구는 불연속 장치 할당과 함께 사용할 수 있는지 여부를 표시 합니다. 장치가 불연속 장치 할당과 호환 되는 것으로 식별 되는 경우 스크립트에서 이유를 제공 합니다.  장치가 호환 되는 것으로 식별 되 면 장치의 위치 경로가 표시 됩니다.  또한 해당 장치에는 [MMIO 공간이](#mmio-space)필요한 경우에도 표시 됩니다.

![SurveyDDA](./images/hyper-v-surveydda-ps1.png)
