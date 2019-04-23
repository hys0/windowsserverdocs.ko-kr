---
title: RDS-그래픽 가상화 기술을 적합 한?
description: 적합 한 그래픽 RDS 배포에 대 한 가상화 옵션을 선택할 수 있도록 계획 정보입니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 03/16/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d6ff5b22-7695-4fee-b1bd-6c9dce5bd0e8
author: lizap
manager: scottman
ms.openlocfilehash: 7cf7fdf3510fcaaa955bd0031fb3564fe4372472
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875804"
---
# <a name="which-graphics-virtualization-technology-is-right-for-you"></a>그래픽 가상화 기술을 적합 한?

원격 데스크톱 서비스의 그래픽 렌더링을 사용 하도록 설정 하는 데 있어 다양 한 옵션 해야 합니다. 가상화 환경을 계획할 때 다음 사항을 선택할 기술이 렌더링 하는 그래픽 드라이브:

![그래픽 렌더링 고려 사항-비교 하 여 사용자 확장 및 사용자 환경에 가장 적합 한 GPU 기술과 결정할 GPU 요구 사항](media/rds-gpu.png)

Windows Server 2016에서 GPU 하드웨어를 활용할 수 있도록 Hyper-v를 사용 하 여 사용할 수 있는 두 개의 그래픽 가상화 기술 해야 합니다.

- [불연속 장치 할당 (DDA)](#discrete-device-assignment) -VM 내에서 기본 GPU 드라이버 지원을 제공 하는 VM에 하나 이상의 Gpu를 사용 하 여 가장 높은 성능을 전용입니다. 서버에서 사용할 수 있는 실제 Gpu의 개수로 제한 되어 있으므로 밀도 부족 합니다. 
- [원격 FX vGPU](#remotefx-vgpu) -지식 근로자 및 여러 Vm 반 가상화를 통해 하나 이상의 Gpu를 활용 하는 위치는 높은 버스트 GPU 시나리오에 대 한 합니다. 이 솔루션은 서버당 더 높은 사용자 밀집도 제공 합니다.

다음 그림에서는 Windows Server 2016에서 사용 되는 그래픽 가상화 옵션 보여 줍니다.

![그래픽 가상화 옵션-RDS 사용 하 여 Windows Server 2016에서 사용할 수 있는 세 가지 기술 및 확장성 및 성능 서로 어떻게 보여 줍니다.](media/rds-graphics-virtualization.png)

## <a name="discrete-device-assignment"></a>개별 장치 할당
불연속 장치 할당 (DDA) 하는 최상의 성능을 제공 하는 하드웨어 통과 솔루션 VM에 기본 드라이버를 사용 하 여 GPU에 대 한 전체 액세스 합니다. VM 사용자 장치의 네이티브 드라이버로 장치의 전체 기능을 액세스할 수 있습니다. 즉, 기능 및 운영 체제 미 설치 컴퓨터에서 동일한 장치를 실행 중인 VM 미러의 장치를 실행 하는 기능.

DDA에 대 한 자세한 내용은 체크 아웃 [불연속 장치 할당을 배포 하기 위한 계획](../../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md)합니다.

## <a name="remotefx-vgpu"></a>RemoteFX vGPU 
RemoteFX vGPU는 지식 근로자 시나리오 (위 첫 번째 그림 참조)를 사용 하도록 설정 하려면 게스트 운영 체제를 다양 한 분할 되어야 GPU의 처리 능력을 허용 하는 그래픽 가상화 기술입니다. Windows Server 2016의 향상 된 기능 디자이너 응용 프로그램 및 데이터 시각화에 대 한 예를 들어 GPU 버스트 시나리오에 대 한 향상 된 추가 기능을 허용합니다. 기타 기능 향상은 다음과 같습니다.

-   2 세대 게스트 Vm, Windows Server 2016 게스트 Vm 및 Windows 클라이언트 Hyper-v 호스트를 지원 합니다.
   >[!NOTE] 
   > Windows Server 2016 게스트 VM;에서 원격 데스크톱 세션 호스트를 사용할 수 없습니다. Windows Server 2016 게스트 VM 당 1 개의 세션을 호스트할 수 있습니다.

-   향상 된 응용 프로그램 호환성 및 안정성입니다.
-   VM 연결 고급 세션 모드, RemoteFX vGPU에 사용 되는 VM에 VM 연결을 통해 USB 및 클립보드 리디렉션을 허용 합니다.

자세한 내용은 체크 아웃 [설정 및 원격 데스크톱 서비스에 대 한 RemoteFX vGPU 구성](rds-remotefx-vgpu.md)합니다.

## <a name="which-should-you-use"></a>언제 사용 하나요?

주요 고려 사항이 가상화 기술 하드웨어 사양 또는 사용자 환경에서 응용 프로그램 요구 사항에 따라 달라질 수 있습니다. DDA 및 RemoteFX vGPU 기능에 대 한 간략 한 표는 다음과 같습니다.

| 기능               | RemoteFX vGPU                                                                       | 개별 장치 할당                                             |
|-----------------------|-------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| GPU 장치 할당 | 반 가상화 된 (많은 Vm을 하나 이상의 Gpu)                                     | 1 VM에 하나 이상의 GPU                                                  |
| 소수 자릿수                 | 크기 조정 모범 / 1 GPU Vm 수를                                                      | 확장을 낮은 / 1 VM에 하나 이상의 Gpu                                     |
| 응용 프로그램 호환성     | DX 11.1, OpenGL 4.4, OpenCL 1.1                                                     | (DX 12, OpenGL, CUDA) 공급 업체에서 제공 하는 모든 GPU 기능          |
| AVC444                | (Windows 10 및 Windows Server 2016) 기본적으로 사용 하도록 설정                             | 그룹 정책 (Windows 10 및 Windows Server 2016)를 통해 사용할 수 있습니다.    |
| GPU VRAM              | 최대 1GB VRAM 전용                                                           | VRAM GPU에서 지 원하는 최대                                        |
| 프레임 속도            | 최대 30fps                                                                         | 최대 60 fps                                                            |
| 게스트에 GPU 드라이버   | RemoteFX 3D 어댑터 디스플레이 드라이버 (Microsoft)                                      | GPU 공급 업체 드라이버 (Nvidia, AMD, Intel)                                 |
| 게스트 OS 지원      |  Windows Server 2012 R2  Windows Server 2016  Windows 7 SP1  Windows 8.1 Windows 10 |  Windows Server 2012 R2  Windows Server 2016  Windows 10 Linux         |
| 하이퍼바이저            | Microsoft Hyper-V                                                                   | Microsoft Hyper-V                                                      |
| 호스트 OS 가용성  |  Windows Server 2012 R2  Windows Server 2016 Windows 10                             | Windows Server 2016                                                    |
| GPU 하드웨어          | 엔터프라이즈 Gpu (예: Nvidia Quadro/표 또는 AMD FirePro)                         | 엔터프라이즈 Gpu (예: Nvidia Quadro/표 또는 AMD FirePro)            |
| 서버 하드웨어       | 특별 한 요구 사항 없음                                                             | 최신 서버 os (일반적으로 SR-IOV를 지 원하는 하드웨어) IOMMU를 노출 합니다. |

일반적인 경험상 가상 컴퓨터 GPU에 직접 액세스할 수 있으므로 최상의 응용 프로그램 호환성을 위해 DDA를 사용 하는 것입니다. 응용 프로그램 또는 워크 로드와 GPU의 엄격한 요구 사항이 없는 경우 원하는 서버에 사용자에 대 한 광범위 한 자료 RemoteFX vGPU 수를 가장 효과적입니다.