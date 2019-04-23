---
title: RDS-RemoteFX vGPU 설치 및 구성
description: RemoteFX vGPU 그래픽 가상화를 구성 하는 정보를 계획 합니다.
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
ms.openlocfilehash: 3e7da1a70826dc720a96ceb3fe5d04868943f163
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59876844"
---
# <a name="set-up-and-configure-remotefx-vgpu-for-remote-desktop-services"></a>원격 데스크톱 서비스에 사용할 RemoteFX vGPU 설치 및 구성


RemoteFX vGPU 기능의 실제 그래픽 어댑터를 공유 하도록 여러 가상 컴퓨터의 수 있습니다. 가상 컴퓨터 전용된 그래픽 어댑터 프로세서에서 그래픽 정보는 렌더링을 오프 로드할 수 있습니다. CPU 부하를 감소 되 고 VDI virtual machines에서 실행 되는 그래픽 강력한 워크 로드에 대 한 확장성이 개선 됩니다. 

## <a name="remotefx-vgpu-requirements"></a>RemoteFX vGPU 요구 사항

호스트 시스템 요구 사항: 

- Windows Server 2016 또는 Windows 10
- WDDM 1.2 호환 가능한 드라이버를 사용 하 여 호환 GPU DX 11.0 
- Windows Server RD 가상화 호스트 역할 활성화 (Hyper-v 역할 사용) 
- Cpu가 SLAT (Second Level Address Translation)를 지 원하는 서버 

게스트 VM 요구 사항:

- 게스트 VM을 Windows 엔터프라이즈 클라이언트 (Windows 7 서비스 팩 1, Windows 8.1, Windows 10) 또는 Windows Server (Windows Server 2012 R2 또는 Windows Server 2016)를 실행 합니다. 추가 OS에 대 한 참조를 지원 [원격 데스크톱 서비스에 대 한 지원 되는 구성을](rds-supported-config.md)합니다.

게스트 Vm에 대 한 추가 고려 사항:

- OpenGL 및 OpenCL 기능만 Windows 10 또는 Windows Server 2016에서 제공 됩니다.  
- DirectX 11.0은 Windows 8 또는 최신 게스트 Vm에 사용할 수만 있습니다. 
- 로 실행 중인 경우 RemoteFX vGPU를 사용한 원격 데스크톱 세션 호스트 에서만 지원 되는 [개인 세션 데스크톱](rds-personal-session-desktops.md)합니다.

VM 게스트에 대 한 검토 해야 [VDI 배포-지원 되는 게스트 Os](rds-supported-config.md#vdi-deployment--supported-guest-oss)합니다.

## <a name="install-remotefx-vgpu"></a>RemoteFX vGPU를 설치 합니다.

설치 및 Windows Server 2016 및 Windows 10에 대 한 호스트의 RemoteFX를 구성 하려면 다음 단계를 사용 합니다.

1. 운영 체제를 설치합니다.
2. 최신 Windows 10/windows Server 2016 GPU 드라이버를 사용할 수 있는 그래픽 카드 공급 업체 사이트에서 설치 합니다.
3. Windows 10 또는 Windows Server 2016 호스트에 RemoteFX vGPU를 설치 합니다.
   1. Windows 10 호스트에서 Control Panel (이동 컨트롤 패널/프로그램 및 기능/Turn Windows 기능을 켜거나)에서 Hyper-v 기능을 사용 하도록 설정:

      ![Windows 기능 Hyper-v 기능을 사용 하는 창](media/rds-hyperv-settings.png)

   2. Windows Server 2016 호스트에서 원격 데스크톱 가상화 호스트 (RDVH) 역할을 설치 합니다.
   

4. 이제 만들기 및 게스트 VM을 구성 합니다.
   1. Windows 10 Enterprise 또는 Windows Server 2016 사용 하 여 VM을 만듭니다.
   2. RemoteFX 3D 그래픽 어댑터를 추가 합니다. 참조 [RemoteFX vGPU 3D 어댑터를 구성](#configure-the-remotefx-vgpu-3d-adapter) Hyper-v 관리자 또는 PowerShell cmdlet을 사용 하 여 그렇게 하는 방법에 대 한 정보에 대 한 합니다. 

RemoteFX vGPU 둘 이상 사용할 수 있을 때 모든 Gpu를 사용 합니다. 그러나 특정 경우에 Gpu를 제한 하려는 경우 RemoteFX가 사용 됩니다. Hyper-v 환경에서 귀하가이 명시적으로 선택 해야 하는 gpu가 있는 *되지* RemoteFX가 사용 됩니다. 다음 단계를 따르십시오. 

   1. Hyper-v 관리자에서 Hyper-v 설정으로 이동 합니다.
   2. 클릭 **실제 Gpu** Hyper-v 설정에서 합니다.
   3. 선택 하 고 선택을 취소 한 후 원하지 않는 GPU **RemoteFX를 사용 하 여이 GPU를 사용 하 여**입니다.


### <a name="configure-the-remotefx-vgpu-3d-adapter"></a>RemoteFX vGPU 3D 어댑터를 구성 합니다.
RemoteFX vGPU 3D 그래픽 어댑터를 구성 하는 Hyper-v 관리자 UI 또는 PowerShell cmdlet을 사용할 수 있습니다. 

#### <a name="through-hyper-v-manager"></a>Hyper-v 관리자:

1. 시스템에서 Hyper-v를 사용 하 여 설정 된가 VM 구성 및 확인 합니다.  
2. 실행 중인 경우 VM을 중지 합니다. 
3. Hyper-v 관리자에서로 이동 합니다 **VM 설정**를 클릭 하 고 **하드웨어 추가**합니다.
4. 선택 **RemoteFX 3D 그래픽 어댑터**, 클릭 **추가**합니다. 
5. 모니터, 최대 모니터 해상도 및 전용된 비디오 메모리의 최대 수를 설정 하거나 기본값을 그대로 둡니다.

   > [!NOTE]
   > - 이러한 옵션 중 하나에 대 한 값이 높을수록 설정는 영향을 주지 크기를 조정 하려면 하므로 반드시 필요한 것만 설정 해야 합니다.
   >
   > - 전용된 VRAM 1GB를 사용 해야 할 때 최상의 결과 64 비트 게스트 VM 32 비트 (x86) 대신 사용 합니다.
6. 클릭 **확인** 구성을 완료 합니다.

#### <a name="with-powershell-cmdlets"></a>PowerShell cmdlet:

추가, 검토 및 어댑터를 구성 하려면 다음 cmdlet을 실행 합니다. 

```powershell
Add-VMRemoteFx3dVideoAdapter [-CimSession <CimSession[]>] [-ComputerName <String[]>] [-Credential <PSCredential[]>] [-VMName] <String[]> [-Passthru] [-WhatIf] [-Confirm] [<CommonParameters>]
```

자세한 내용은 참조 하십시오 [추가-VMRemoteFx3dVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/add-vmremotefx3dvideoadapter)합니다.

```powershell
Get-VMRemoteFx3dVideoAdapter [-CimSession <CimSession[]>] [-ComputerName <String[]>]  [-Credential <PSCredential[]>] [-VMName] <String[]> [<CommonParameters>]
```

자세한 내용은 참조 하십시오 [Get-VMRemoteFx3dVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmremotefx3dvideoadapter)

```powershell
Set-VMRemoteFx3dVideoAdapter [-CimSession <CimSession[]>] [-ComputerName <String[]>] [-Credential <PSCredential[]>] [-VMName] <String[]> [[-MonitorCount] <Byte>] [[-MaximumResolution] <String>] [[-VRAMSizeBytes] <UInt64>] [-Passthru] [-WhatIf] [-Confirm] [<CommonParameters>]
```

자세한 내용은 참조 하십시오 [Set-VMRemoteFx3dVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/set-vmremotefx3dvideoadapter)합니다.

실제 Gpu를 검토 하려면 다음 cmdlet을 실행 합니다.

```powershell
Get-VMRemoteFXPhysicalVideoAdapter [-ComputerName <String[]>] [-Credential <PSCredential[]>] [[-Name] <String[]>] [<CommonParameters>]  
```

자세한 내용은 참조 하십시오 [Get-vmremotefxphysicalvideoadapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmremotefxphysicalvideoadapter)합니다.

## <a name="monitor-performance"></a>성능 모니터링

성능 및 규모 VDI 시스템의 다양 한 GPU의 총 메모리, 메모리 속도, CPU 코어 수 및 CPU 클록 주파수, 저장소 속도, NUMA 구현 시스템 메모리의 양과 같은 요인으로 결정 됩니다.

RDS의 원격 vGPU 지원이 프레임 속도 처리량에 대 한 정보를 수집 하려면 성능 모니터 (perfmon.exe)에서 볼 수 있습니다 다음 성능 카운터를 포함 합니다.

- RemoteFX 그래픽-원격 데스크톱 프로토콜 그래픽 압축에 대 한 카운터입니다. 예를 들어 압축에 대 한 RDP에 게 표시 되는 프레임의 수를 확인 하려는 경우 확인 합니다 **입력 Frames/Second** 카운터입니다.
- RemoteFX 네트워크-원격 데스크톱 프로토콜 네트워크 트래픽에 대 한 카운터입니다. 예를 들어 **왕복 시간 (RTT)** 합니다.
- RemoteFX 루트 GPU 관리-측정값 VRAM 사용 가능 하 고 예약 합니다.
- RemoteFX 소프트웨어-캡처 속도, GPU 응답 시간 및 다른 사용자에 대 한 카운터를 제공 합니다.

더 낮은 수준의 성능 모니터링 용 문제 해결을 위해 특히 다음과 같은 추가 성능 카운터를 사용할 수 있습니다.

- RemoteFX Synth3D VSC VM 장치 
- RemoteFX Synth3D VSC VM 전송 채널 
- RemoteFX Synth3D VSP 
- RemoteFX Synth3D VSP VM 장치 
- RemoteFX Synth3D VSP VM 채널
