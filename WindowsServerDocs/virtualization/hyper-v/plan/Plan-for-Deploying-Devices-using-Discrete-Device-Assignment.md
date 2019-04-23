---
title: 불연속 장치 할당을 사용 하 여 장치를 배포 하는 것에 대 한 계획
description: Windows Server에서 DDA 작동 하는 방식 알아보기
ms.prod: windows-server-threshold
ms.service: na
ms.technology: hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: chrishuybregts
ms.author: chrihu
ms.date: 02/06/2018
ms.openlocfilehash: c64c2b75c00f97622278c3e590db46995e108218
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840204"
---
# <a name="plan-for-deploying-devices-using-discrete-device-assignment"></a>불연속 장치 할당을 사용 하 여 배포 장치에 대 한 계획
>적용 대상: Microsoft Hyper-V Server 2016, Windows Server 2016, Microsoft Hyper-V Server 2019, Windows Server 2019

불연속 장치 할당 실제 PCIe 하드웨어를를 가상 머신 내에서 직접 액세스할 수 있습니다.  이 가이드에서는 제한 사항과 불연속 장치 할당의 보안 요구 사항 뿐만 아니라 가상 컴퓨터와 호스트 시스템 요구 사항, 불연속 장치 할당을 사용할 수 있는 장치 유형을 설명 합니다.

불연속 장치 할당의 초기 릴리스의 경우 Microsoft에서 공식적으로 지원 되는 데 두 장치 클래스에 집중 했습니다. 그래픽 어댑터 및 NVMe 저장소 장치입니다.  다른 장치를 작동할 가능성이 및 하드웨어 공급 업체는 해당 장치에 대 한 지원 설명을 제공할 수 있습니다.  이러한 다른 장치에 대 한 하세요 지원에 대 한 해당 하드웨어 공급 업체에 연락 합니다.

으로 이동 수를 불연속 장치 할당을 사용해 준비가 되었으면 [배포 그래픽 장치를 사용 하 여 불연속 장치 할당](../deploy/Deploying-graphics-devices-using-dda.md) 하거나 [불연속 장치 할당을 사용 하 여 저장소 장치 배포](../deploy/Deploying-storage-devices-using-dda.md) 시작 합니다!

## <a name="supported-virtual-machines-and-guest-operating-systems"></a>지원 되는 Virtual Machines 및 게스트 운영 체제
1 세대 또는 2 개의 Vm에 대 한 불연속 장치 할당은 지원 됩니다.  지원 되는 게스트에서 사용 하 여 Windows Server 2012r2, Windows Server 2016, Windows Server 2019, Windows 10을 포함 하는 또한 [KB 3133690](https://support.microsoft.com/kb/3133690) 적용 및의 다양 한 배포판을 [Linux OS입니다.](../supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md)

## <a name="system-requirements"></a>시스템 요구 사항
외에는 [Windows 서버에 대 한 시스템 요구 사항](../../../get-started/System-Requirements--and-Installation.md) 및 [Hyper-v에 대 한 시스템 요구 사항](../System-requirements-for-Hyper-V-on-Windows.md), 불연속 장치 할당 권한을 부여할 수 있는 서버 클래스 하드웨어가 필요 합니다 운영 체제에 대 한 제어 PCIe 패브릭 (네이티브 PCI Express 컨트롤) 구성 또한 PCIe 루트 복합에 "Access Control Services" (ACS)이를 통해 모든 PCIe 트래픽에 I/O MMU 통과 하도록 하기 위해 Hyper-v를 지원 합니다.

이러한 기능은 일반적으로 서버의 BIOS에 직접 노출 되지 않습니다 및 기타 설정을 뒤에 숨겨진 경우가 많습니다.  예를 들어, 동일한 기능은 SR-IOV 지원에 필요 하 고 BIOS에서 "SR-IOV를 사용 합니다."를 설정 해야  문의 하세요 시스템 공급 업체 BIOS의 올바른 설정을 확인할 수 없는 경우.

을 하드웨어는 하드웨어는 불연속 장치 할당을 보장 하기 위해 엔지니어 모아 놓은 [컴퓨터 프로필 스크립트](#machine-profile-script) 서버를 올바르게 설치 및 테스트 하는 사용 Hyper-v 호스트에서 실행할 수 있습니다 장치는 불연속 장치 할당 수입니다.

## <a name="device-requirements"></a>장치 요구 사항
불연속 장치 할당을 사용 하 여 일부 PCIe 장치를 사용할 수 있습니다.  예를 들어 레거시 (INTx) PCI 중단을 활용 하는 오래 된 장치는 지원 되지 않습니다. 그러나 Jake Oshin [블로그 게시물](https://blogs.technet.microsoft.com/virtualization/2015/11/20/discrete-device-assignment-machines-and-devices/) 실행 하는 소비자에 대 한 자세한 세부 정보-로 이동 합니다 [컴퓨터 프로필 스크립트](#machine-profile-script) 불연속 장치 할당에 사용할 수 있는 장치에 표시 됩니다.

장치 제조업체에서 대 한 자세한 내용은 해당 Microsoft 담당자에 게 연결할 수 있습니다.

## <a name="device-driver"></a>장치 드라이버
게스트 VM에 전체 PCIe 장치를 통과 하는 불연속 장치 할당, 호스트 드라이버를 설치한 다음, VM 내에서 탑재 되는 장치에 필요 하지 않습니다.  유일한 요구 사항은 호스트에는 장치의 [PCIe 위치 경로](#pcie-location-path) 확인할 수 있습니다.  장치 드라이버는 장치를 식별 하는 데 도움이 되는 경우에 필요에 따라 설치할 수 있습니다.  예를 들어 호스트에 설치 하는 장치 드라이버 없이 GPU 장치로 Microsoft 기본 렌더링 나타날 수 있습니다.  장치 드라이버 설치 되어 있으면 해당 제조업체 및 모델 가능성이 나타납니다.

게스트 내 장치가 탑재 된 후 제조업체의 장치 드라이버 게스트 가상 머신 내에서 일반적인 이제 설치할 수 있습니다.  

## <a name="virtual-machine-limitations"></a>가상 머신 제한 사항
불연속 장치 할당 구현 하는 방법에 대 한 특성상는 장치가 연결 되는 동안 가상 컴퓨터의 일부 기능이 제한 됩니다.  다음 기능은 사용할 수 없습니다.
- VM 저장/복원
- VM의 실시간 마이그레이션
- 동적 메모리 사용
- 고가용성 (HA) 클러스터에 VM 추가

## <a name="security"></a>보안
VM에 전체 장치를 전달 하는 불연속 장치 할당 합니다.  즉, 해당 장치의 모든 기능은 게스트 운영 체제에서 액세스할 수 있습니다. 펌웨어 업데이트 같은 일부 기능은 시스템의 안정성을 저하 될 수 있습니다. 따라서 호스트에서 장치를 분리 하는 경우 다양 한 경고는 관리자에 게 표시 됩니다. 불연속 장치 할당만는 Vm의 테 넌 트가 신뢰할 수 있는 것이 좋습니다.  

관리자는 신뢰할 수 없는 테 넌 트를 사용 하 여 장치를 사용 하려면 필요한, 하는 경우 호스트에 설치할 수 있는 완화 장치 드라이버를 만들 수 있는 기능을 사용 하 여 장치 제조업체에서 준비 했습니다.  장치 완화 드라이버 제공 여부에 대 한 내용은 장치 제조업체에 문의 하세요.

전달 해야 장치 완화 드라이버가 없는 장치에 대 한 보안 검사를 무시 하려는 경우는 `-Force` 매개 변수는 `Dismount-VMHostAssignableDevice` cmdlet.  이해는 작업을 수행 하면 해당 시스템의 보안 프로필을 변경 하 고이 프로토타입 중 권장 되었거나 신뢰할 수 있는 환경입니다.

## <a name="pcie-location-path"></a>PCIe 위치 경로
PCIe 위치 경로 호스트에서 장치를 탑재 및 분리 해야 합니다.  예를 들어 위치 경로 다음과 같습니다: `"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"`합니다.   합니다 [컴퓨터 프로필 스크립트](#machine-profile-script) 또한 PCIe 장치 위치 경로 반환 합니다.

### <a name="getting-the-location-path-by-using-device-manager"></a>장치 관리자를 사용 하 여 위치 경로 가져오기
![장치 관리자](../deploy/media/dda-devicemanager.png)
- 장치 관리자를 열고 장치를 찾습니다.  
- 장치를 마우스 오른쪽 단추로 클릭 하 고 "속성입니다."를 선택 합니다.
- 세부 정보 탭으로 이동한 다음 속성 드롭다운 목록에서 "위치 경로"를 선택 합니다.  
- "PCIROOT"로 시작 하는 항목을 마우스 오른쪽 단추로 클릭 하 고 "복사" 선택  이제 해당 장치에 대 한 위치 경로를 갖습니다.

## <a name="mmio-space"></a>MMIO 공간
일부 장치에서는 특히 Gpu에는 액세스할 수 있도록 해당 장치의 메모리에 대 한 VM에 할당할 추가 MMIO 공간이 필요 합니다. 기본적으로 낮은 MMIO 공간의 128MB 이며 각 VM 시작 및 512MB의 높은 MMIO 공간 할당 합니다. 그러나 장치 MMIO 공간이 필요할 수 있습니다 또는 이러한 값을 초과 하는 결합 된 요구 사항이 되도록 여러 장치를 통해 전달 될 수 있습니다.  MMIO 공간 변경은 간단 하며 다음 명령을 사용 하 여 PowerShell에서 수행할 수 있습니다.

```
Set-VM -LowMemoryMappedIoSpace 3Gb -VMName $vm
Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName $vm
```
할당할 MMIO 공간의 양을 사용 하는 것을 확인 하는 가장 쉬운 방법은 합니다 [컴퓨터 프로필 스크립트](#machine-profile-script)합니다.  또는 장치 관리자를 사용 하 여 계산할 수 있습니다. TechNet 블로그 게시물을 참조 하세요 [불연속 장치 할당-Gpu](https://blogs.technet.microsoft.com/virtualization/2015/11/23/discrete-device-assignment-gpus/) 대 한 자세한 내용은 합니다.

## <a name="machine-profile-script"></a>컴퓨터 프로필 스크립트
서버가 올바르게 구성 된 경우를 식별 하 고 어떤 장치는 불연속 장치 할당을 사용 하 여 전달할 수를 간단 하 게 하기 위해 엔지니어 중 하나를 모아 다음 PowerShell 스크립트: [SurveyDDA.ps1.](https://github.com/Microsoft/Virtualization-Documentation/blob/live/hyperv-tools/DiscreteDeviceAssignment/SurveyDDA.ps1)

스크립트를 사용 하기 전에 Hyper-v 역할이 설치 되어 있고 관리자 권한이 있는 PowerShell 명령 창에서 스크립트를 실행할를 확인 하세요.

시스템 불연속 장치 할당을 지원 하도록 올바르게 구성 되어, 경우 도구에는 무엇이 문제에 대 한 오류 메시지가 표시 됩니다. 도구를 올바르게 구성 시스템을 찾으면 PCIe 버스에 찾을 수 있는 모든 장치를 열거 합니다.

찾은 각 장치에 대 한 불연속 장치 할당을 사용 하 여 사용할 수 있는지 여부를 표시 됩니다. 장치는 불연속 장치 할당을 사용 하 여 호환 되는 것으로 식별 되 면 스크립트는 이유를 제공 합니다.  장치는 호환 되는 것으로 제대로 확인 되 면 장치의 위치 경로 표시 됩니다.  또한 해당 장치에 필요한 경우 [MMIO 공간](#mmio-space)에 표시 됩니다.

![SurveyDDA.ps1](./images/hyper-v-surveydda-ps1.png)

## <a name="frequently-asked-questions"></a>질문과 대답

### <a name="how-does-remote-desktops-remotefx-vgpu-technology-relate-to-discrete-device-assignment"></a>원격 데스크톱의 RemoteFX vGPU 기술 불연속 장치 할당 어떤 관계가 있습니까?
또는 완전히 별도 기술 됩니다. RemoteFX vGPU 불연속 장치 할당 작업에 대 한 설치할 필요가 없습니다. 또한 없습니다 추가 역할은 설치 해야 합니다. RemoteFX vGPU RDVH 역할 VM에 RemoteFX vGPU 드라이버를 설치 해야 합니다. 불연속 장치 할당에 대 한 하드웨어 공급 업체의 드라이버 가상 컴퓨터에 설치 되므로 추가 역할이 표시 되도록 해야 합니다.  

### <a name="ive-passed-a-gpu-into-a-vm-but-remote-desktop-or-an-application-isnt-recognizing-the-gpu"></a>VM에 GPU를 전달 했습니다 있습니까 되지만 원격 데스크톱 또는 응용 프로그램에는 GPU 인식 되지 않습니다.
다양 한 이유로 발생할 수 있습니다, 있지만 몇 가지 일반적인 문제는 다음과 같습니다.
- 최신 GPU 공급 업체의 드라이버를 설치 하 고 장치 관리자에서 장치 상태를 확인 하 여 오류를 보고 하지 않는 확인 합니다.
- 해당 장치에 충분 [MMIO 공간](#mmio-space) 내에 VM에 할당 합니다.
- Gpu가 장착 된 공급 업체에서는 사용 중인이 구성을 사용 해야 합니다. 예를 들어, 일부 공급 업체는 VM으로 전달 하는 경우 작업에서 해당 소비자 카드를 방지 합니다.
- VM 내에서 실행 되는 지원 및 GPU 및 해당 관련된 드라이버 응용 프로그램에서 지원 하는지 실행 중인 응용 프로그램을 확인 합니다. 일부 응용 프로그램 허용 목록 Gpu 및 환경의 경우
- 원격 데스크톱 세션 호스트 역할 또는 Windows Multipoint 서비스를 사용 하 여 게스트에는, 특정 그룹 정책 항목을 기본 GPU 사용을 허용 하도록 설정 되어 있는지 확인 해야 합니다. 게스트 (또는 게스트의 로컬 그룹 정책 편집기)에 적용 된 그룹 정책 개체를 사용 하 여, 다음 그룹 정책 항목으로 이동 합니다.
   - 컴퓨터 구성
   - 관리자 템플릿
   - Windows 구성 요소
   - 원격 데스크톱 서비스
   - 원격 데스크톱 세션 호스트
   - 원격 세션 환경
   - 모든 원격 데스크톱 서비스 세션에 대 한 하드웨어 기본 그래픽 어댑터를 사용 합니다.

    이 값 사용으로 설정한 다음 정책이 적용 되 면 VM을 다시 부팅 합니다.

### <a name="can-discrete-device-assignment-take-advantage-of-remote-desktops-avc444-codec"></a>불연속 장치 할당 원격 데스크톱 AVC444 코덱 활용을 걸릴 수 있습니다?
예, 자세한 내용은이 블로그 게시물을 참조 하세요: [Windows 10 및 Windows Server 2016 Technical Preview의 원격 데스크톱 프로토콜 (RDP) 10 AVC/H.264 향상 합니다.](https://blogs.technet.microsoft.com/enterprisemobility/2016/01/11/remote-desktop-protocol-rdp-10-avch-264-improvements-in-windows-10-and-windows-server-2016-technical-preview/)

### <a name="can-i-use-powershell-to-get-the-location-path"></a>위치 경로를 가져오는 PowerShell을 사용할 수 있나요?
예,이 작업을 수행 하는 다양 한 방법 이며 한 가지 예는 다음과 같습니다.
```
#Enumerate all PNP Devices on the system
$pnpdevs = Get-PnpDevice -presentOnly
#Select only those devices that are Display devices manufactured by NVIDIA
$gpudevs = $pnpdevs |where-object {$_.Class -like "Display" -and $_.Manufacturer -like "NVIDIA"}
#Select the location path of the first device that's available to be dismounted by the host.
$locationPath = ($gpudevs | Get-PnpDeviceProperty DEVPKEY_Device_LocationPaths).data[0]
```

### <a name="can-discrete-device-assignment-be-used-to-pass-a-usb-device-into-a-vm"></a>USB 장치를 VM에 전달할 불연속 장치 할당을 사용할 수 있습니까?
공식적으로 지원 되기는 하지만 고객에 게 전체 USB3 컨트롤러 VM에 전달 하 여이 작업을 수행할를 불연속 장치 할당을 사용 했습니다.  전체 컨트롤러에서 전달 되는 대로 해당 컨트롤러에 연결 된 USB 장치 각 VM에 액세스할 수도 있습니다.  불연속 장치 할당을 사용 하 여 일부 USB3 컨트롤러만 사용할 수도 및 USB2 컨트롤러를 사용할 수 없습니다.
