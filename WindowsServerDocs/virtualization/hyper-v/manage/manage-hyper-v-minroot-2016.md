---
title: Minroot
description: 호스트 CPU 리소스 컨트롤 구성
keywords: windows 10, Hyper-V
author: allenma
ms.date: 12/15/2017
ms.topic: article
ms.prod: windows-10-hyperv
ms.service: windows-10-hyperv
ms.assetid: ''
ms.openlocfilehash: 92de899a39aed05e2f598fcb3aae3fbae3f1cb67
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70872042"
---
# <a name="hyper-v-host-cpu-resource-management"></a>Hyper-v 호스트 CPU 리소스 관리

Windows Server 2016 이상 버전에 도입 된 hyper-v 호스트 CPU 리소스 제어를 통해 Hyper-v 관리자는 "루트", 관리 파티션 및 게스트 Vm 간에 호스트 서버 CPU 리소스를 보다 효율적으로 관리 하 고 할당할 수 있습니다. 관리자는 이러한 제어를 사용 하 여 호스트 시스템의 프로세서 하위 집합을 루트 파티션에 전용으로 사용할 수 있습니다. 이렇게 하면 시스템 프로세서의 개별 하위 집합에서 실행 하 여 게스트 가상 머신에서 실행 되는 워크 로드에서 Hyper-v 호스트의 작업을 수행할 수 있습니다.

Hyper-v 호스트의 하드웨어에 대 한 자세한 내용은 [Windows 10 Hyper-v 시스템 요구 사항](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/hyper-v-requirements)을 참조 하세요.

## <a name="background"></a>배경

Hyper-v 호스트 CPU 리소스에 대 한 컨트롤을 설정 하기 전에 Hyper-v 아키텍처의 기본 사항을 검토 하는 것이 좋습니다.  
일반 요약은 [Hyper-v 아키텍처](https://docs.microsoft.com/windows-server/administration/performance-tuning/role/hyper-v-server/architecture) 섹션에서 찾을 수 있습니다.
다음은이 문서에 대 한 중요 한 개념입니다.

* Hyper-v는 하이퍼바이저의 제어에서 계산 리소스를 할당 및 공유 하는 가상 컴퓨터 파티션을 만들고 관리 합니다.  파티션은 모든 게스트 가상 머신과 게스트 Vm과 루트 파티션 간에 강력한 격리 경계를 제공 합니다.

* 루트 파티션은 게스트 가상 컴퓨터 보다 고유한 속성과 훨씬 더 많은 권한을가지고 있지만 가상 컴퓨터 파티션입니다.  루트 파티션은 모든 게스트 가상 컴퓨터를 제어 하는 관리 서비스를 제공 하 고, 게스트에 대 한 가상 장치 지원을 제공 하 고, 게스트 가상 컴퓨터의 모든 장치 i/o를 관리 합니다.  호스트 파티션에서 응용 프로그램 워크 로드를 실행 하지 않는 것이 좋습니다.

* 루트 파티션의 각 가상 프로세서 (VP)는 1:1를 기본 논리적 프로세서 (LP)에 매핑합니다.  호스트 VP는 항상 동일한 기본 LP에서 실행 됩니다. 루트 파티션의 VPs는 마이그레이션하지 않습니다.  

* 기본적으로 호스트 VPs 실행 되는 LPs는 게스트 VPs 실행할 수도 있습니다.

* 하이퍼바이저는 사용 가능한 모든 논리 프로세서에서 실행 되도록 게스트 VP를 예약할 수 있습니다.  하이퍼바이저 스케줄러는 임시 캐시 집약성, NUMA 토폴로지 및 게스트 VP를 예약할 때 많은 다른 요인을 고려 하는 반면 궁극적으로 모든 호스트 LP에 대해 VP를 예약할 수 있습니다.

## <a name="the-minimum-root-or-minroot-configuration"></a>최소 루트 또는 "Minroot" 구성

Hyper-v의 초기 버전에는 파티션당 아키텍처 최대 제한인 64 VPs가 있습니다.  이는 루트 및 게스트 파티션에 적용 됩니다.  논리 프로세서가 64 개를 초과 하는 시스템은 고성능 서버에 표시 되기 때문에 Hyper-v는 최대 320 LPs를 사용 하는 호스트를 지 원하는 한 지점에서 이러한 대규모 시스템을 지원 하기 위해 호스트 규모 제한을 발전 했습니다.  그러나이 시간에 64 VP의 파티션 제한에 도달 하면 여러 가지 과제가 발생 하 고 파티션당 64 VPs 이상으로 지원 되는 복잡성이 도입 되었습니다.  이를 해결 하기 위해 Hyper-v는 기본 컴퓨터에 더 많은 논리 프로세서를 사용할 수 있는 경우에도 루트 파티션에 지정 된 VPs 수를 64로 제한 합니다.  하이퍼바이저는 게스트 VPs을 실행 하는 데 사용할 수 있는 모든 LPs를 계속 활용 하지만 64에서 루트 파티션을 인위적으로 사용 합니다.  이 구성을 "최소 루트" 또는 "minroot" 구성 이라고 합니다.  성능 테스트를 통해 64 LPs를 초과 하는 대규모 시스템 에서도, 많은 수의 게스트 Vm 및 게스트 64 VPs에 충분 한 지원을 제공 하기 위해 루트에 64 root VPs 이상 필요 하지 않은 것으로 확인 되었습니다. , 게스트 Vm의 수와 크기, 실행 중인 특정 워크 로드 등을 기준으로 합니다.

현재이 "minroot" 개념은 계속 활용 됩니다.  실제로 Windows Server 2016 Hyper-v는 호스트 LPs에서 512 LPs로의 최대 아키텍처 지원 제한을 증가 시켰습니다. 루트 파티션은 여전히 최대 320 LPs로 제한 됩니다.

## <a name="using-minroot-to-constrain-and-isolate-host-compute-resources"></a>Minroot를 사용 하 여 호스트 계산 리소스 제한 및 격리
Windows Server 2016 Hyper-v에서 기본 임계값이 320 LPs 이면 매우 큰 서버 시스템 에서만 minroot 구성이 활용 됩니다.  그러나이 기능은 Hyper-v 호스트 관리자가 훨씬 낮은 임계값으로 구성할 수 있으므로 루트 파티션에 사용할 수 있는 호스트 CPU 리소스의 양을 크게 제한 하는 데 활용 됩니다.  사용 해야 하는 특정 루트 LPs의 수를 신중 하 게 선택 하 여 호스트에 할당 된 Vm 및 워크 로드의 최대 요구 사항을 지원 해야 합니다.  그러나 호스트 LPs의 수에 대 한 적절 한 값은 프로덕션 워크 로드에 대 한 신중한 평가 및 모니터링을 통해 결정할 수 있으며 광범위 한 배포 전에 비프로덕션 환경에서 유효성을 검사할 수 있습니다.

## <a name="enabling-and-configuring-minroot"></a>Minroot 활성화 및 구성

Minroot 구성은 하이퍼바이저 BCD 항목을 통해 제어 됩니다. Minroot를 사용 하도록 설정 하려면 cmd 프롬프트에서 관리자 권한으로 다음을 수행 합니다.

```
    bcdedit /set hypervisorrootproc n
```
여기서 n은 root VPs의 수입니다. 

시스템을 다시 부팅 해야 하며, OS 부팅 수명 동안 새 루트 프로세서 수가 유지 됩니다.  Minroot 구성은 런타임에 동적으로 변경할 수 없습니다.

NUMA 노드가 여러 개 있는 경우 각 노드는 프로세서를 `n/NumaNodeCount` 가져옵니다.

여러 NUMA 노드를 사용 하는 경우 VM의 토폴로지가 각 NUMA 노드에 해당 VM의 NUMA 노드 VPs을 실행 하기에 충분 한 무료 LPs (즉, root VPs가 없는 LPs)가 있는지 확인 해야 합니다.

## <a name="verifying-the-minroot-configuration"></a>Minroot 구성 확인

아래와 같이 작업 관리자를 사용 하 여 호스트의 minroot 구성을 확인할 수 있습니다.

![](./media/minroot-taskman.png)

Minroot가 활성 상태인 경우 작업 관리자는 시스템에 있는 논리적 프로세서의 총 수와 함께 현재 호스트에 할당 된 논리 프로세서 수를 표시 합니다.
 
