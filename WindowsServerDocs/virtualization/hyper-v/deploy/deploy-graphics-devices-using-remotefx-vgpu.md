---
title: RemoteFX vGPU를 사용 하 여 그래픽 장치 배포
description: Windows Server에서 RemoteFX vGPU를 배포 및 구성 하는 방법 알아보기
ms.prod: windows-server-threshold
ms.reviewer: rickman
author: rick-man
ms.author: rickman
manager: stevelee
ms.topic: article
ms.date: 08/21/2019
ms.openlocfilehash: 7111899557279d825191948e737d83d7467ce786
ms.sourcegitcommit: 81198fbf9e46830b7f77dcd345b02abb71ae0ac2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72923915"
---
# <a name="deploy-graphics-devices-using-remotefx-vgpu"></a>RemoteFX vGPU를 사용 하 여 그래픽 장치 배포

> 적용 대상: Windows Server 2016, Microsoft Hyper-V Server 2016

RemoteFX 용 vGPU 기능을 사용 하면 여러 가상 컴퓨터에서 실제 GPU를 공유할 수 있습니다. 렌더링 및 계산 리소스는 가상 컴퓨터 간에 동적으로 공유 되며, 전용 GPU 리소스가 필요 하지 않은 버스트 작업에 적합 한 RemoteFX vGPU를 만듭니다. 예를 들어 VDI 서비스에서 RemoteFX vGPU는 CPU 부하를 줄이고 서비스 확장성을 개선 하는 효과를 사용 하 여 앱 렌더링 비용을 GPU로 오프 로드 하는 데 사용할 수 있습니다.

## <a name="remotefx-vgpu-requirements"></a>RemoteFX vGPU 요구 사항

호스트 시스템 요구 사항:

- Windows Server 2016
- WDDM 1.2 호환 드라이버를 사용 하는 DirectX 11.0 호환 GPU
- SLAT (두 번째 수준 주소 변환)를 지 원하는 CPU

게스트 VM 요구 사항:

- 지원 되는 게스트 OS입니다. 자세한 내용은 [다음 항목을 참조 하세요.](../../../remote/remote-desktop-services/rds-supported-config.md#remotefx-3d-video-adapter-vgpu-support)

게스트 VM을 위한 추가 고려 사항:

- OpenGL 및 OpenCL 기능은 Windows 10 또는 Windows Server 2016를 실행 하는 게스트 에서만 사용할 수 있습니다.  
- DirectX 11.0은 Windows 8 이상을 실행 하는 게스트에만 사용할 수 있습니다.

## <a name="enable-remotefx-vgpu"></a>RemoteFX vGPU 사용

Windows Server 2016 호스트에서 RemoteFX vGPU를 구성 하려면:

1. Windows Server 2016에 대 한 GPU 공급 업체에서 권장 하는 그래픽 드라이버를 설치 합니다.
2. RemoteFX vGPU에서 지원 되는 게스트 OS를 실행 하는 VM을 만듭니다. 자세히 알아보려면 [RemoteFX 3D 비디오 어댑터 (vGPU) 지원](../../../remote/remote-desktop-services/rds-supported-config.md#remotefx-3d-video-adapter-vgpu-support)을 참조 하세요.
3. VM에 RemoteFX 3D 그래픽 어댑터를 추가 합니다. 자세히 알아보려면 [RemoteFX VGPU 3d 어댑터 구성](#configure-the-remotefx-vgpu-3d-adapter)을 참조 하세요.

기본적으로 RemoteFX vGPU는 사용 가능한 모든 Gpu와 지원 되는 Gpu를 사용 합니다. RemoteFX vGPU에서 사용 하는 Gpu를 제한 하려면 다음 단계를 수행 합니다.

1. Hyper-V 관리자에서 Hyper-V 설정으로 이동합니다.
2. Hyper-v 설정에서 **실제 gpu** 를 선택 합니다.
3. 사용하지 않으려는 GPU를 선택한 다음, **RemoteFX에서 이 GPU 사용**의 선택을 취소합니다.

### <a name="configure-the-remotefx-vgpu-3d-adapter"></a>RemoteFX vGPU 3D 어댑터 구성

Hyper-V 관리자 UI 또는 PowerShell cmdlet을 사용하여 RemoteFX vGPU 3D 그래픽 어댑터를 구성할 수 있습니다.

#### <a name="configure-remotefx-vgpu-with-hyper-v-manager"></a>Hyper-v 관리자를 사용 하 여 RemoteFX vGPU 구성

1. VM이 현재 실행 중인 경우 중지 합니다.
2. Hyper-v 관리자를 열고 **VM 설정**으로 이동한 다음 **하드웨어 추가**를 선택 합니다.
3. **RemoteFX 3D 그래픽 어댑터**를 선택 하 고 **추가**를 선택 합니다.
4. 최대 모니터 수, 최대 모니터 해상도 및 전용 비디오 메모리를 설정하거나 기본값을 그대로 둡니다.

   > [!NOTE]
   > - 이러한 옵션에 대 한 값을 높게 설정 하면 서비스 크기에 영향을 주므로 필요한 항목만 설정 하면 됩니다.
   > - 1gb의 전용 VRAM을 사용 해야 하는 경우 최상의 결과를 위해 32 비트 (x86) 대신 64 비트 게스트 VM을 사용 합니다.

5. **확인** 을 선택 하 여 구성을 완료 합니다.

#### <a name="configure-remotefx-vgpu-with-powershell-cmdlets"></a>PowerShell cmdlet을 사용 하 여 RemoteFX vGPU 구성

어댑터를 추가, 검토 및 구성 하려면 다음 PowerShell cmdlet을 사용 합니다.

- [VMRemoteFx3dVideoAdapter](https://docs.microsoft.com/powershell/module/hyper-v/add-vmremotefx3dvideoadapter?view=win10-ps)
- [VMRemoteFx3dVideoAdapter](https://docs.microsoft.com/powershell/module/hyper-v/get-vmremotefx3dvideoadapter?view=win10-ps)
- [VMRemoteFx3dVideoAdapter](https://docs.microsoft.com/powershell/module/hyper-v/set-vmremotefx3dvideoadapter?view=win10-ps)
- [Microsoft.hyperv.powershell.vmremotefxphysicalvideoadapter](https://docs.microsoft.com/powershell/module/hyper-v/get-vmremotefxphysicalvideoadapter?view=win10-ps)

## <a name="monitor-performance"></a>성능 모니터링

RemoteFX vGPU 지원 서비스의 성능 및 소수 자릿수는 시스템의 Gpu 수, 총 GPU 메모리, 시스템 메모리 양 및 메모리 속도, CPU 코어 수, CPU 클록 빈도, 저장소 속도, NUMA 등과 같은 다양 한 요소에 의해 결정 됩니다. 구현이.

### <a name="host-system-memory"></a>호스트 시스템 메모리

VGPU에서 사용 하도록 설정 된 모든 VM에 대해 RemoteFX는 게스트 운영 체제와 호스트 서버 모두에서 시스템 메모리를 사용 합니다. 하이퍼바이저는 게스트 운영 체제에 대 한 시스템 메모리의 가용성을 보장 합니다. 호스트에서 각 vGPU 지원 가상 데스크톱은 시스템 메모리 요구 사항을 하이퍼바이저에 보급 해야 합니다. VGPU 지원 가상 데스크톱이 시작 되 면 하이퍼바이저는 호스트에 추가 시스템 메모리를 예약 합니다.

Remotefx 사용 서버에서 사용 되는 메모리 양이 vGPU 지원 가상 데스크톱에 연결 된 모니터 수와에 대 한 최대 해상도에 따라 다르므로 RemoteFX 사용 서버에 대 한 메모리 요구 사항이 동적입니다. 이러한 모니터

### <a name="host-gpu-video-memory"></a>호스트 GPU 비디오 메모리

모든 vGPU 지원 가상 데스크톱은 호스트 서버에서 GPU 하드웨어 비디오 메모리를 사용 하 여 데스크톱을 렌더링 합니다. 또한 코덱은 비디오 메모리를 사용 하 여 렌더링 된 화면을 압축 합니다. 렌더링 및 압축에 필요한 메모리 양은 가상 컴퓨터에 프로 비전 된 모니터의 수를 기반으로 합니다. 예약 된 비디오 메모리의 양은 시스템 화면 해상도 및 모니터 수에 따라 달라 집니다. 일부 사용자는 특정 작업에 대해 더 높은 화면 해상도를 요구 하지만 다른 모든 설정이 일정 하 게 유지 되는 경우 더 낮은 해상도 설정을 사용 하 여 확장성이 높아집니다.

### <a name="host-cpu"></a>호스트 CPU

하이퍼바이저는 CPU에서 호스트 및 Vm을 예약 합니다. 시스템에서 vGPU 지원 가상 데스크톱 마다 추가 프로세스 (rdvgm)를 실행 하므로 RemoteFX 사용 호스트에서 오버 헤드가 증가 합니다. 이 프로세스는 그래픽 장치 드라이버를 사용 하 여 GPU에서 명령을 실행 합니다. 또한 코덱은 CPU를 사용 하 여 클라이언트로 다시 전송 되어야 하는 화면 데이터를 압축 합니다.

가상 프로세서를 많이 사용 하면 더 나은 사용자 환경을 의미 합니다. VGPU 지원 가상 데스크톱 당 두 개 이상의 가상 Cpu를 할당 하는 것이 좋습니다. 또한 x64 가상 컴퓨터의 성능은 x86 가상 컴퓨터와 비교 하 여 더 효율적 이므로 vGPU 지원 가상 데스크톱에 x64 아키텍처를 사용 하는 것이 좋습니다.

### <a name="gpu-processing-power"></a>GPU 처리 능력

모든 vGPU 지원 가상 데스크톱에는 호스트 서버에서 실행 되는 해당 DirectX 프로세스가 있습니다. 이 프로세스는 RemoteFX 가상 데스크톱에서 수신 하는 모든 그래픽 명령을 실제 GPU로 재생 합니다. 이는 동일한 실제 GPU에서 여러 DirectX 응용 프로그램을 동시에 실행 하는 것과 같습니다.

일반적으로 그래픽 장치 및 드라이버는 데스크톱에서 한 번에 몇 개의 응용 프로그램만 실행 하도록 조정 되지만 RemoteFX는 Gpu를 확장 하 여 훨씬 더 진행 합니다. vGPUs는 RemoteFX 요청에 대 한 GPU 응답을 측정 하는 성능 카운터와 함께 제공 되며 Gpu가 너무 멀리 확장 되지 않도록 하는 데 도움이 됩니다.

GPU의 리소스가 부족 하면 읽기 및 쓰기 작업을 완료 하는 데 시간이 오래 걸립니다. 관리자는 성능 카운터를 사용 하 여 리소스를 조정 하 고 사용자의 가동 중지 시간을 방지할 시기를 알 수 있습니다.

[원격 데스크톱의 그래픽 성능 문제 진단](https://docs.microsoft.com/azure/virtual-desktop/remotefx-graphics-performance-counters)에서 RemoteFX vGPU 동작 모니터링에 대 한 성능 카운터에 대해 자세히 알아보세요.
