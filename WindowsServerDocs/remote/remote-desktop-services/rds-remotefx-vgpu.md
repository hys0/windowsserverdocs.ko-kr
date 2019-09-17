---
title: RDS - RemoteFX vGPU 설치 및 구성
description: RemoteFX vGPU 그래픽 가상화를 구성하기 위한 계획 정보입니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 03/23/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0263fa6b-2185-4cc3-99ef-3588e2f4ada5
author: lizap
manager: scottman
ms.openlocfilehash: 3e189d9ac059136b40d8ee5d93a4eea5b788cdd1
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70870854"
---
# <a name="set-up-and-configure-remotefx-vgpu-for-remote-desktop-services"></a>원격 데스크톱 서비스에 대한 RemoteFX vGPU 설치 및 구성


RemoteFX vGPU 기능은 여러 가상 머신이 하나의 실제 그래픽 어댑터를 공유할 수 있게 해줍니다. 가상 머신은 그래픽 정보의 렌더링을 프로세서에서 전용 그래픽 어댑터로 오프로드할 수 있습니다. 그러면 CPU 부하가 감소하고 VDI 가상 머신에서 실행되는 그래픽 집약적 워크로드의 확장성이 개선됩니다. 

## <a name="remotefx-vgpu-requirements"></a>RemoteFX vGPU 요구 사항

호스트 시스템 요구 사항: 

- Windows Sever 2016 또는 Windows 10
- WDDM 1.2 호환 가능 드라이버를 사용하는 DX 11.0 호환 가능 GPU 
- Windows Server RD 가상화 호스트 역할 활성화(Hyper-v 역할 사용) 
- SLAT(Second-Level Address Translation)를 지원하는 CPU가 탑재된 서버 

게스트 VM 요구 사항:

- Windows Enterprise 클라이언트(Windows 7 서비스 팩 1, Windows 8.1, Windows 10) 또는 Windows Server(Windows Server 2012 R2 또는 Windows Server 2016)에서 실행 중인 게스트 VM. 추가 OS 지원은 [원격 데스크톱 서비스에 지원되는 구성](rds-supported-config.md)을 참조하세요.

게스트 VM을 위한 추가 고려 사항:

- OpenGL 및 OpenCL 기능은 Windows 10 또는 Windows Server 2016에서만 사용할 수 있습니다.  
- DirectX 11.0은 Windows 8 이상의 게스트 VM에서만 사용할 수 있습니다. 
- 원격 데스크톱 세션 호스트는 [개인 세션 데스크톱](rds-personal-session-desktops.md)으로 실행 중인 경우에만 RemoteFX vGPU가 지원됩니다.

게스트 VMS의 경우 [VDI 배포 - 지원되는 게스트 OS](rds-supported-config.md#vdi-deployment--supported-guest-oss)를 살펴보세요.

## <a name="install-remotefx-vgpu"></a>RemoteFX vGPU 설치

Windows Server 2016 및 Windows 10용 호스트에서 RemoteFX를 설치하고 구성하려면 다음 단계를 수행하세요.

1. 운영 체제를 설치합니다.
2. 그래픽 카드 공급업체 사이트에서 제공되는 최신 Windows 10/Windows Server 2016 GPU 드라이버를 설치합니다.
3. Windows 10/Windows Server 2016 호스트에서 RemoteFX vGPU를 설치합니다.
   1. Windows 10 호스트의 제어판에서 Hyper-V 기능을 사용하도록 설정합니다(제어판/프로그램 및 기능으로 이동하여 Windows 기능 켜기 또는 끄기).

      ![Hyper-V 기능을 사용하도록 설정하는 Windows 기능 창](media/rds-hyperv-settings.png)

   2. Windows Server 2016 호스트에서 RDVH(원격 데스크톱 가상화 호스트) 역할을 설치합니다.
   

4. 이제 게스트 VM을 만들고 구성합니다.
   1. Windows 10 Enterprise 또는 Windows Server 2016이 탑재된 VM을 만듭니다.
   2. RemoteFX 3D 그래픽 어댑터를 추가합니다. Hyper-V 관리자 또는 PowerShell cmdlet을 사용하여 이 작업을 수행하는 방법에 대한 자세한 내용은 [RemoteFX vGPU 3D 어댑터 구성](#configure-the-remotefx-vgpu-3d-adapter)을 참조하세요. 

RemoteFX vGPU는 사용 가능한 GPU가 여러 개 있을 경우 모두 사용합니다. 그러나 특정한 경우에는 RemoteFX가 사용하는 GPU를 제한하는 것이 좋습니다. Hyper-V 환경에서 RemoteFX가 사용해서는 *안 되는* GPU를 구체적으로 선택하여 이를 제어하세요. 다음 단계를 따르십시오. 

   1. Hyper-V 관리자에서 Hyper-V 설정으로 이동합니다.
   2. Hyper-V 설정에서 **실제 GPU**를 클릭합니다.
   3. 사용하지 않으려는 GPU를 선택한 다음, **RemoteFX에서 이 GPU 사용**의 선택을 취소합니다.


### <a name="configure-the-remotefx-vgpu-3d-adapter"></a>RemoteFX vGPU 3D 어댑터 구성
Hyper-V 관리자 UI 또는 PowerShell cmdlet을 사용하여 RemoteFX vGPU 3D 그래픽 어댑터를 구성할 수 있습니다. 

#### <a name="through-hyper-v-manager"></a>Hyper-V 관리자를 통해 다음을 수행합니다.

1. 시스템이 Hyper-V를 사용하여 설정되었고, VM이 구성되어 있는지 확인합니다.  
2. 실행 중인 경우 VM을 중지합니다. 
3. Hyper-V 관리자에서 **VM 설정**으로 이동한 후 **하드웨어 추가**를 클릭합니다.
4. **RemoteFX 3D 그래픽 어댑터**를 선택하고 **추가**를 클릭합니다. 
5. 최대 모니터 수, 최대 모니터 해상도 및 전용 비디오 메모리를 설정하거나 기본값을 그대로 둡니다.

   > [!NOTE]
   > - 이러한 옵션에 높은 값을 설정하면 규모에 영향을 주므로 반드시 필요한 것만 설정해야 합니다.
   >
   > - 1GB의 전용 VRAM을 사용해야 하는 경우 32비트(x86) 대신 64비트 게스트 VM을 사용해야 최상의 결과를 얻을 수 있습니다.
6. **확인**을 클릭하여 구성을 완료합니다.

#### <a name="with-powershell-cmdlets"></a>PowerShell cmdlet을 사용하여 다음을 수행합니다.

어댑터를 추가, 검토, 구성하려면 다음 cmdlet을 실행합니다. 

```powershell
Add-VMRemoteFx3dVideoAdapter [-CimSession <CimSession[]>] [-ComputerName <String[]>] [-Credential <PSCredential[]>] [-VMName] <String[]> [-Passthru] [-WhatIf] [-Confirm] [<CommonParameters>]
```

자세한 내용은 [Add-VMRemoteFx3dVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/add-vmremotefx3dvideoadapter)를 참조하세요.

```powershell
Get-VMRemoteFx3dVideoAdapter [-CimSession <CimSession[]>] [-ComputerName <String[]>]  [-Credential <PSCredential[]>] [-VMName] <String[]> [<CommonParameters>]
```

자세한 내용은 [Get-VMRemoteFx3dVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmremotefx3dvideoadapter)를 참조하세요.

```powershell
Set-VMRemoteFx3dVideoAdapter [-CimSession <CimSession[]>] [-ComputerName <String[]>] [-Credential <PSCredential[]>] [-VMName] <String[]> [[-MonitorCount] <Byte>] [[-MaximumResolution] <String>] [[-VRAMSizeBytes] <UInt64>] [-Passthru] [-WhatIf] [-Confirm] [<CommonParameters>]
```

자세한 내용은 [Set-VMRemoteFx3dVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/set-vmremotefx3dvideoadapter)를 참조하세요.

실제 GPU를 검토하려면 다음 cmdlet을 실행합니다.

```powershell
Get-VMRemoteFXPhysicalVideoAdapter [-ComputerName <String[]>] [-Credential <PSCredential[]>] [[-Name] <String[]>] [<CommonParameters>]  
```

자세한 내용은 [Get-VMRemoteFXPhysicalVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmremotefxphysicalvideoadapter)를 참조하세요.

## <a name="monitor-performance"></a>성능 모니터링

VDI 시스템의 성능과 규모는 GPU의 총 메모리, 시스템 메모리의 양, 메모리 속도, CPU 코어 수 및 CPU 클럭 주파수, 스토리지 속도, NUMA 구현과 같은 다양한 요인에 따라 결정됩니다.

RDS의 원격 vGPU 지원에는 다음과 같은 성능 카운터가 포함되며, 성능 모니터(perfmon.exe)에서 이를 확인하여 프레임 속도 처리량에 대한 정보를 수집할 수 있습니다.

- RemoteFX 그래픽 - 원격 데스크톱 프로토콜 그래픽 압축용 카운터입니다. 예를 들어 RDP에 압축을 위해 제공되는 프레임 수를 보려면 **초당 입력 프레임 수** 카운터를 확인하세요.
- RemoteFX 네트워크 - 원격 데스크톱 프로토콜 네트워크 트래픽용 카운터입니다. 예를 들어 **왕복 시간(RTT)** 이 있습니다.
- RemoteFX 루트 GPU 관리 - 사용 가능하며 예약된 VRAM을 측정합니다.
- RemoteFX 소프트웨어 - 캡처 속도, GPU 응답 시간 등에 대한 카운터를 제공합니다.

더 낮은 수준의 성능 모니터링의 경우(특히 문제를 해결하는 경우) 다음과 같은 추가 성능 카운터를 사용할 수 있습니다.

- RemoteFX Synth3D VSC VM 디바이스 
- RemoteFX Synth3D VSC VM 전송 채널 
- RemoteFX Synth3D VSP 
- RemoteFX Synth3D VSP VM 디바이스 
- RemoteFX Synth3D VSP VM 채널
