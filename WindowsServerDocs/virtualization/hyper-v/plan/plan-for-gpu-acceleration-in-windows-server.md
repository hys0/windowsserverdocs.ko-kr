---
title: Windows Server의 GPU 가속 계획
description: DDA 및 RemoteFX vGPU를 포함 하 여 GPU 가속을 위한 다양 한 Hyper-v 기술에 대해 알아봅니다.
ms.prod: windows-server
ms.reviewer: rickman
author: rick-man
ms.author: rickman
manager: stevelee
ms.topic: article
ms.date: 07/14/2020
ms.openlocfilehash: c8e0e8798da9cb4a2b3ca317d9632450ade82504
ms.sourcegitcommit: f81aa22739d818382d314561dece59a9341dfb6f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2020
ms.locfileid: "86390100"
---
# <a name="plan-for-gpu-acceleration-in-windows-server"></a>Windows Server의 GPU 가속 계획

> 적용 대상: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

이 문서에서는 Windows Server에서 사용할 수 있는 그래픽 가상화 기능을 소개 합니다.

## <a name="when-to-use-gpu-acceleration"></a>GPU 가속을 사용 하는 경우

워크 로드에 따라 GPU 가속을 고려 하는 것이 좋습니다. GPU 가속을 선택 하기 전에 고려해 야 할 사항은 다음과 같습니다.

- **앱 및 데스크톱 원격 (VDI/DaaS) 워크 로드**: Windows Server를 사용 하 여 앱 또는 데스크톱 원격 서비스를 빌드하는 경우 사용자가 실행할 것으로 생각 되는 앱의 카탈로그를 고려 합니다. CAD/CAM 앱, 시뮬레이션 앱, 게임 및 렌더링/시각화 앱과 같은 일부 유형의 앱은 부드러운 대화형 대화형 작업을 제공 하기 위해 3D 렌더링에 크게 의존 합니다. 대부분의 고객은 이러한 종류의 앱을 통해 적절 한 사용자 환경을 위해 Gpu를 사용 하는 것을 고려 합니다.
- **원격 렌더링, 인코딩 및 시각화 워크 로드**: 이러한 그래픽 지향 워크 로드는 비용 효율성 및 처리량 목표를 달성 하기 위해 효율적인 3d 렌더링 및 프레임 인코딩/디코딩과 같은 GPU의 특수화 된 기능에 크게 의존 하는 경향이 있습니다. 이러한 종류의 워크 로드에서 단일 GPU 사용 VM은 많은 CPU 전용 vm의 처리량을 일치 시킬 수 있습니다.
- **HPC 및 ML 워크 로드**: 고성능 계산 및 기계 학습 모델 학습 또는 유추와 같은 매우 효율적인 데이터 병렬 계산 워크 로드의 경우 gpu는 결과, 유추 시간 및 학습 시간을 크게 단축할 수 있습니다. 또는 비교 가능한 성능 수준에서 CPU 전용 아키텍처 보다 더 나은 비용 효율성을 제공할 수 있습니다. 많은 HPC 및 기계 학습 프레임 워크에는 GPU 가속을 사용 하도록 설정 하는 옵션이 있습니다. 이로 인해 특정 작업에 도움이 될 수 있는지 여부를 고려 합니다.

## <a name="gpu-virtualization-in-windows-server"></a>Windows Server의 GPU 가상화

GPU 가상화 기술은 일반적으로 가상 컴퓨터 내에서 가상화 된 환경에서 GPU 가속을 사용 하도록 설정 합니다. Hyper-v를 사용 하 여 워크 로드를 가상화 하는 경우 실제 GPU에서 가상화 된 앱 또는 서비스에 대 한 GPU 가속을 제공 하기 위해 그래픽 가상화를 사용 해야 합니다. 그러나 실제 Windows Server 호스트에서 작업을 직접 실행 하는 경우에는 그래픽 가상화가 필요 하지 않습니다. 응용 프로그램 및 서비스에는 Windows Server에서 기본적으로 지원 되는 GPU 기능 및 Api에 대 한 액세스 권한이 이미 있습니다.

Windows Server의 Hyper-v Vm에서 사용할 수 있는 그래픽 가상화 기술은 다음과 같습니다.

- [불연속 장치 할당 (DDA)](#discrete-device-assignment-dda)
- [RemoteFX vGPU](#remotefx-vgpu)

Windows Server는 VM 워크 로드 외에도 Windows 컨테이너 내에서 컨테이너 화 된 워크 로드의 GPU 가속을 지원 합니다. 자세한 내용은 [Windows 컨테이너의 GPU 가속](https://docs.microsoft.com/virtualization/windowscontainers/deploy-containers/gpu-acceleration)을 참조 하세요.

## <a name="discrete-device-assignment-dda"></a>불연속 장치 할당 (DDA)

GPU 통과 라고도 하는 불연속 장치 할당 (DDA)을 사용 하면 하나 이상의 실제 Gpu를 가상 머신에 전용으로 사용할 수 있습니다. DDA 배포에서 가상화 된 워크 로드는 네이티브 드라이버에서 실행 되며 일반적으로 GPU의 기능에 대 한 모든 권한을 가집니다. DDA는 최고 수준의 앱 호환성과 잠재적 성능을 제공 합니다. DDA는 지원을 받을 수 있는 Linux Vm에 GPU 가속을 제공할 수도 있습니다.

각 실제 GPU는 최대 하나의 VM에 대 한 가속을 제공할 수 있으므로 DDA 배포는 제한 된 수의 가상 컴퓨터만 가속화할 수 있습니다. 아키텍처가 공유 가상 컴퓨터를 지 원하는 서비스를 개발 하는 경우 VM 당 여러 가속화 된 워크 로드를 호스트 하는 것이 좋습니다. 예를 들어 RDS를 사용 하 여 데스크톱 remoting 서비스를 구축 하는 경우 Windows Server의 다중 세션 기능을 활용 하 여 각 VM에서 여러 사용자 데스크톱을 호스트 함으로써 사용자 규모를 향상할 수 있습니다. 이러한 사용자는 GPU 가속의 이점을 공유 합니다.

자세한 내용은 다음 항목을 참조하세요.

- [불연속 장치 할당 배포 계획](plan-for-deploying-devices-using-discrete-device-assignment.md)
- [불연속 장치 할당을 사용 하 여 그래픽 장치 배포](../deploy/Deploying-graphics-devices-using-dda.md)

## <a name="remotefx-vgpu"></a>RemoteFX vGPU

> [!NOTE]
> 보안 문제로 인해 RemoteFX vGPU는 2020 년 7 월 14 일에 시작 되는 모든 Windows 버전에서 기본적으로 사용 되지 않습니다. 자세히 알아보려면 [KB 4570006](https://support.microsoft.com/help/4570006)을 참조 하세요.

RemoteFX vGPU는 단일 실제 GPU를 여러 가상 컴퓨터에서 공유할 수 있도록 하는 그래픽 가상화 기술입니다. RemoteFX vGPU 배포에서 가상화 된 작업은 Microsoft의 RemoteFX 3D 어댑터에서 실행 되며,이 어댑터는 호스트와 게스트 간의 GPU 처리 요청을 조정 합니다. RemoteFX vGPU는 전용 GPU 리소스가 필요 하지 않은 지식 근로자 및 버스트 작업에 가장 적합 합니다. RemoteFX vGPU는 Windows Vm에 대 한 GPU 가속만 제공할 수 있습니다.

자세한 내용은 다음 항목을 참조하세요.

- [RemoteFX vGPU를 사용하여 그래픽 디바이스 배포](../deploy/deploy-graphics-devices-using-remotefx-vgpu.md)
- [RemoteFX 3D 비디오 어댑터(vGPU) 지원](../../../remote/remote-desktop-services/rds-supported-config.md#remotefx-3d-video-adapter-vgpu-support)

## <a name="comparing-dda-and-remotefx-vgpu"></a>DDA 및 RemoteFX vGPU 비교

배포를 계획할 때 다음 기능을 고려 하 고 그래픽 가상화 기술 간의 차이점을 지원 합니다.

|                       | RemoteFX vGPU                                                                       | 개별 디바이스 할당                                                          |
|-----------------------|-------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| GPU 리소스 모델    | 전용 또는 공유                                                                 | 전용 전용                                                                      |
| VM 밀도            | 높음 (하나 이상의 Gpu에서 많은 Vm에)                                                 | 낮음 (한 VM에 하나 이상의 Gpu)                                                    |
| 앱 호환성     | DX 11.1, OpenGL 4.4, OpenCL 1.1                                                     | 공급 기업에서 제공하는 모든 GPU 기능(DX 12, OpenGL, CUDA)                       |
| AVC444                | 기본적으로 사용                                                                  | 그룹 정책 통해 사용 가능                                                      |
| GPU VRAM              | 최대 1GB 전용 VRAM                                                           | GPU에서 지원하는 최대 VRAM                                                     |
| 프레임 율            | 최대 30fps                                                                         | 최대 60fps                                                                         |
| 게스트의 GPU 드라이버   | RemoteFX 3D 어댑터 디스플레이 드라이버(Microsoft)                                      | GPU 공급 업체 드라이버 (NVIDIA, AMD, Intel)                                              |
| 호스트 OS 지원       | Windows Server 2016                                                                 | Windows Server 2016; Windows Server 2019                                            |
| 게스트 OS 지원      | Windows Server 2012 R2; Windows Server 2016; Windows 7 SP1 Windows 8.1; Windows 10 | Windows Server 2012 R2; Windows Server 2016; Windows Server 2019; Windows 10; 용 |
| 하이퍼바이저            | Microsoft Hyper-V                                                                   | Microsoft Hyper-V                                                                   |
| GPU 하드웨어          | 엔터프라이즈 GPU(예: Nvidia Quadro/GRID 또는 AMD FirePro)                         | 엔터프라이즈 GPU(예: Nvidia Quadro/GRID 또는 AMD FirePro)                         |
| 서버 하드웨어       | 특별한 요구 사항 없음                                                             | 최신 서버, OS에 IOMMU 노출(일반적으로 SR-IOV 호환 하드웨어)              |
