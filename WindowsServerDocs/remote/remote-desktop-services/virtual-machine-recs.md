---
title: 가상 머신 크기 조정
description: 각 워크로드 유형에 대한 크기 추천 사항입니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 12/02/2019
ms.tgt_pltfrm: na
ms.topic: article
author: Heidilohr
manager: lizross
ms.openlocfilehash: 9564643e02a0b659914736c4047a8d723816976f
ms.sourcegitcommit: 76469d1b7465800315eaca3e0c7f0438fc3939ed
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/13/2020
ms.locfileid: "75919932"
---
# <a name="virtual-machine-sizing-guidance"></a>가상 머신 크기 조정 지침

원격 데스크톱 서비스 또는 Windows Virtual Desktop에서 VM(가상 머신)을 실행하는지 여부에 관계없이 워크로드 유형마다 서로 다른 세션 호스트 VM 구성이 필요합니다. 최상의 환경을 위해 사용자의 요구 사항에 따라 배포의 크기를 조정합니다.

## <a name="multi-session-recommendations"></a>다중 세션 추천 사항

다음 표에는 추천되는 vCPU(가상 중앙 처리 장치)당 최대 사용자 수와 각 워크로드에 대한 최소 VM 구성이 나와 있습니다. 이러한 추천 사항은 [원격 데스크톱 워크로드](remote-desktop-workloads.md)를 기반으로 합니다.

| 워크로드 유형 | vCPU당 최대 사용자 수 | 최소 vCPU/RAM/OS 스토리지 구성 | Azure 인스턴스 예제 | 최소 프로필 컨테이너 스토리지 크기 |
| --- | --- | --- | --- | --- |
| Light | 6 | 2개 vCPU, 8GB RAM, 16GB 스토리지 | D2s_v3, F2s_v2 | 30GB |
| 보통 | 4 | 4개 vCPU, 16GB RAM, 32GB 스토리지 | D4s_v3, F4s_v2 | 30GB |
| Heavy | 2 | 4개 vCPU, 16GB RAM, 32GB 스토리지 | D4s_v3, F4s_v2 | 30GB |
| 고급 | 1 | 6개 vCPU, 56GB RAM, 340GB 스토리지 | D4s_v3, F4s_v2, NV6 | 30GB |

## <a name="single-session-recommendations"></a>단일 세션 추천 사항

단일 세션 시나리오에 대한 VM 크기 조정 추천 사항의 경우 VM당 둘 이상의 물리적 CPU 코어(일반적으로 하이퍼스레딩을 사용하는 4개 vCPU)를 사용하는 것이 좋습니다. 단일 세션 시나리오에 대해 더 구체적인 VM 크기 조정 추천 사항이 필요한 경우 워크로드와 관련하여 소프트웨어 공급업체에 문의하세요. 단일 세션 VM에 대한 VM 크기 조정은 물리적 디바이스 지침에 따라 다를 수 있습니다.

## <a name="general-virtual-machine-recommendations"></a>일반 가상 머신 추천 사항

운영 체제를 실행하기 위한 VM 요구 사항은 [Windows 10 컴퓨터 사양 및 시스템 요구 사항](https://www.microsoft.com/windows/windows-10-specifications)을 참조하세요.

SLA(서비스 수준 계약)가 필요한 프로덕션 워크로드에는 OS 디스크의 프리미엄 SSD 스토리지를 사용하는 것이 좋습니다. 자세한 내용은 [Virtual Machines에 대한 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_8/)를 참조하세요.

GPU(그래픽 처리 장치)는 그래픽 집약적 프로그램을 비디오 렌더링, 3D 디자인 및 시뮬레이션에 정기적으로 사용하는 사용자에게 적합합니다. 그래픽 가속에 대한 자세한 내용은 [그래픽 렌더링 기술 선택](rds-graphics-virtualization.md)을 참조하세요. Azure에는 몇 가지 그래픽 가속 배포 옵션 및 여러 사용 가능한 GPU VM 크기가 있습니다. 자세한 내용은 [GPU 최적화 가상 머신 크기](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-gpu)를 참조하세요.

[B 시리즈 버스트 가능 VM](https://docs.microsoft.com/azure/virtual-machines/windows/b-series-burstable)은 최대 CPU 성능이 반드시 필요한 것이 아닌 사용자에게 적합합니다. VM 유형 및 크기에 대한 자세한 내용은 [Azure의 Windows 가상 머신 크기](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) 및 [Virtual Machine 시리즈 페이지](https://azure.microsoft.com/pricing/details/virtual-machines/series/)의 가격 정보를 참조하세요.

## <a name="test-your-workload"></a>워크로드 테스트

마지막으로, 시뮬레이션 도구를 사용하여 스트레스 테스트와 실제 사용량 시뮬레이션을 모두 사용하여 배포를 테스트하는 것이 좋습니다. 시스템에서 사용자의 요구 사항을 충족할 수 있을 만큼 응답성이 뛰어나고 탄력적인지 확인하고, 예기치 않은 상황을 방지할 수 있도록 로드 크기를 다양하게 변경해야 합니다.
