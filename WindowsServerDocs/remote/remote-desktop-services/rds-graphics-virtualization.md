---
title: RDS - 나에게 적합한 그래픽 가상화 기술은 무엇일까요?
description: 사용자의 RDS 배포에 적합한 그래픽 가상화 옵션을 선택하는 데 유용한 계획 정보입니다.
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
ms.openlocfilehash: af5d5ce89561c89d8468627e20dfdb6f35eca5ef
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "66447114"
---
# <a name="which-graphics-virtualization-technology-is-right-for-you"></a>나에게 적합한 그래픽 가상화 기술은 무엇일까요?

원격 데스크톱 서비스에서 그래픽 렌더링을 활성화하는 경우 다양한 옵션을 사용할 수 있습니다. 가상화 환경을 계획할 때 어떤 그래픽 렌더링 기술을 선택할지 결정하는 데 필요한 고려 사항은 다음과 같습니다.

![그래픽 렌더링 고려 사항 - 사용자 규모와 GPU 요구 사항을 비교하여 환경에 가장 적합한 GPU 기술을 결정](media/rds-gpu.png)

Windows Server 2016에서 GPU 하드웨어를 활용할 수 있도록 Hyper-V를 사용할 수 있는 두 개의 그래픽 가상화 기술이 있습니다.

- [개별 디바이스 할당(DDA)](#discrete-device-assignment) - VM 내에서 기본 GPU 드라이버 지원을 제공하는 VM 전용 GPU를 하나 이상 사용하여 최고의 성능을 제공합니다. 서버에서 사용할 수 있는 물리적 GPU 수에 의해 제한되기 때문에 밀도가 낮습니다. 
- [원격 FX vGPU](#remotefx-vgpu) - 병렬 가상화를 통해 여러 VM이 하나 이상의 GPU를 활용하는 지식 근로자 및 고가용성 GPU 시나리오를 위한 것입니다. 이 솔루션은 서버당 더 높은 사용자 밀도를 제공합니다.

다음 그림에서는 Windows Server 2016의 그래픽 가상화 옵션을 보여줍니다.

![RDS를 사용하는 Windows Server 2016의 그래픽 가상화 옵션 - 사용 가능한 세 가지 기술과 규모 및 성능에 따른 차이점을 보여줌](media/rds-graphics-virtualization.png)

## <a name="discrete-device-assignment"></a>개별 디바이스 할당
개별 디바이스 할당(DDA)은 VM이 네이티브 드라이버를 사용하여 GPU에 완전히 액세스할 수 있다는 점에서 최고의 성능을 제공하는 하드웨어 통과 솔루션입니다. VM 사용자는 디바이스의 네이티브 드라이버와 마찬가지로 디바이스의 전체 기능에 액세스할 수 있습니다. 즉, 베어 메탈에서 동일한 디바이스를 실행하는 VM 미러에서 디바이스를 실행하는 기능을 의미합니다.

DDA에 대한 자세한 내용은 [개별 디바이스 할당 배포를 위한 계획](../../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md)을 확인하세요.

## <a name="remotefx-vgpu"></a>RemoteFX vGPU 
RemoteFX vGPU는 GPU의 처리 능력을 다양한 게스트 운영 체제 간에 분할하여 지식 근로자 시나리오를 사용할 수 있도록 하는 그래픽 가상화 기술입니다(위의 첫 번째 그래픽 참조). Windows Server 2016의 발전으로 GPU 버스트 시나리오(예: 디자이너 애플리케이션 및 데이터 시각화)가 추가로 향상될 수 있습니다. 다음과 같은 기능이 추가로 향상됩니다.

- 2세대 게스트 VM, Windows Server 2016 게스트 VM 및 Windows 클라이언트 Hyper-V 호스트를 지원합니다.
  >[!NOTE] 
  > Windows Server 2016 게스트 VM에서는 원격 데스크톱 세션 호스트가 지원되지 않으므로 Windows Server 2016 게스트 VM당 하나의 세션만 호스팅할 수 있습니다.

- 애플리케이션 호환성 및 안정성이 향상됩니다.
- VM 연결 고급 세션 모드를 통해 RemoteFX vGPU를 사용하도록 설정된 VM에 VM Connect를 통한 USB 및 클립보드 리디렉션이 허용됩니다.

자세한 내용은 [원격 데스크톱 서비스에 대한 RemoteFX vGPU 설치 및 구성](rds-remotefx-vgpu.md)을 확인하세요.

## <a name="which-should-you-use"></a>어느 것을 사용하시겠습니까?

가상화 기술 선택에 대한 주요 고려 사항은 환경의 하드웨어 사양 또는 애플리케이션 요구 사항에 따라 달라질 수 있습니다. 다음에는 DDA 및 RemoteFX vGPU 기능에 대한 간략한 표가 나와 있습니다.

| 기능               | RemoteFX vGPU                                                                       | 개별 디바이스 할당                                             |
|-----------------------|-------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| 디바이스 GPU 할당 | 반가상화(많은 VM에서 하나 이상의 GPU로)                                     | 하나 이상의 GPU에서 하나의 VM으로                                                  |
| 배율                 | 최고 배율 / 1 GPU에서 여러 VM                                                      | 낮은 배율 / 하나 이상의 GPU에서 하나의 VM                                     |
| 앱 호환성     | DX 11.1, OpenGL 4.4, OpenCL 1.1                                                     | 공급 기업에서 제공하는 모든 GPU 기능(DX 12, OpenGL, CUDA)          |
| AVC444                | 기본적으로 사용하도록 설정(Windows 10 및 Windows Server 2016)                             | 그룹 정책을 통해 사용 가능(Windows 10 및 Windows Server 2016)    |
| GPU VRAM              | 최대 1GB 전용 VRAM                                                           | GPU에서 지원하는 최대 VRAM                                        |
| 프레임 속도            | 최대 30fps                                                                         | 최대 60fps                                                            |
| 게스트의 GPU 드라이버   | RemoteFX 3D 어댑터 디스플레이 드라이버(Microsoft)                                      | GPU 공급 기업 드라이버(Nvidia, AMD, Intel)                                 |
| 게스트 OS 지원      |  Windows Server 2012 R2  Windows Server 2016  Windows 7 SP1  Windows 8.1 Windows 10 |  Windows Server 2012 R2  Windows Server 2016  Windows 10 Linux         |
| 하이퍼바이저            | Microsoft Hyper-V                                                                   | Microsoft Hyper-V                                                      |
| 호스트 OS 가용성  |  Windows Server 2012 R2  Windows Server 2016 Windows 10                             | Windows Server 2016                                                    |
| GPU 하드웨어          | 엔터프라이즈 GPU(예: Nvidia Quadro/GRID 또는 AMD FirePro)                         | 엔터프라이즈 GPU(예: Nvidia Quadro/GRID 또는 AMD FirePro)            |
| 서버 하드웨어       | 특별한 요구 사항 없음                                                             | 최신 서버, OS에 IOMMU 노출(일반적으로 SR-IOV 호환 하드웨어) |

일반적으로 가상 머신이 GPU에 직접 액세스할 수 있으므로 최상의 애플리케이션 호환성을 위해 DDA를 사용하는 것이 일반적입니다. 애플리케이션이나 워크로드의 GPU 요구 사항이 엄격하지 않고 광범위한 사용자 기반을 관리하려는 경우 RemoteFX vGPU가 가장 적합할 수 있습니다.