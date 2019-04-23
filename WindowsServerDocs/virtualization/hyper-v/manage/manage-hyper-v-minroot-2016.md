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
ms.openlocfilehash: e1269c11df32c8ce95cc7455d47d7170e9d0b1c8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844334"
---
# <a name="hyper-v-host-cpu-resource-management"></a>Hyper-v 호스트 CPU 리소스 관리

Hyper-v 호스트 CPU 리소스 컨트롤 Windows Server 2016에 도입 된 또는 나중에 더 잘 관리 하 고 호스트 서버에 "root" 또는 관리 파티션 및 게스트 Vm 간에 CPU 리소스 할당 Hyper-v 관리자를 허용 합니다. 이러한 컨트롤을 사용 하 여 루트 파티션에 관리자는 호스트 시스템의 프로세서의 하위 집합 전념할 수 있습니다. 이 시스템 프로세서의 별도 하위 집합에서 실행 하 여 게스트 가상 컴퓨터에서 실행 중인 워크 로드의 Hyper-v 호스트에서 수행 된 작업을 분리할 수 있습니다.

Hyper-v 호스트에 대 한 하드웨어에 대 한 자세한 내용은 참조 하세요 [Windows 10 Hyper-v 시스템 요구 사항](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/hyper-v-requirements)합니다.

## <a name="background"></a>배경

CPU 리소스를 호스트 하는 Hyper-v에 대 한 설정을 제어 하려면 먼저 Hyper-v 아키텍처의 기본 사항을 검토에 유용 합니다.  
일반 요약에서 찾을 수 있습니다 합니다 [Hyper-v 아키텍처](https://docs.microsoft.com/windows-server/administration/performance-tuning/role/hyper-v-server/architecture) 섹션입니다.
다음은이 문서에 대 한 중요 한 개념입니다.

* Hyper-v가 만들고 파티션을 가상 컴퓨터 간에 계산 리소스 할당 되 고 공유, 하이퍼바이저의 제어를 관리 합니다.  파티션 및 게스트 Vm 및 루트 파티션에 모든 게스트 가상 컴퓨터 간의 강력한 격리 경계를 제공합니다.

* 루트 파티션에 파티션입니다 자체 가상 컴퓨터를 고유 속성 및 게스트 가상 머신 보다 훨씬 많은 권한이 있지만.  루트 파티션에 모든 게스트 가상 컴퓨터를 제어 하는 관리 서비스를 제공 하 고, 게스트 가상 장치 지, 게스트 가상 컴퓨터에 대 한 모든 장치 I/O를 관리 합니다.  모든 응용 프로그램 워크 로드를 호스트 파티션에에서 실행 하는 것이 좋습니다.

* 루트 파티션에의 각 가상 프로세서 (VP)은 기본 논리 프로세서 (LP)에 매핑된 1:1입니다.  VP 호스트는 동일한 기본 LP 항상 실행 됩니다.-루트 파티션의 VPs의 마이그레이션이 합니다.  

* 기본적으로 호스트 VPs 실행 LPs 게스트 VPs 실행할 수도 있습니다.

* 사용 가능한 모든 논리적 프로세서에서 실행 되도록 하이퍼바이저에서 게스트 VP은 예약할 수 있습니다.  게스트 VP를 예약할 때 임시 캐시 집약성, NUMA 토폴로지 및 기타 많은 요소를 고려해 야 할 하이퍼바이저 스케줄러 처리를 하는 동안는 VP LP 모든 호스트에 예약할 수 궁극적으로 합니다.

## <a name="the-minimum-root-or-minroot-configuration"></a>최소 루트 또는 "Minroot" 구성

이전 버전의 Hyper-v는 아키텍처 최대 제한인 64 VPs 파티션당 했습니다.  이 루트와 게스트 모두 파티션에 적용 합니다.  64 개 논리적 프로세서를 사용 하 여 시스템을 갖춘 고성능 서버에서 표시, Hyper-v 최대 320 개의 LPs 사용 하 여 호스트를 지 원하는 한 지점에서 더 큰 이러한 시스템을 지원 하도록 호스트 확장 한계를도 발전 했습니다.  그러나 64 주요 VP 당시 파티션 제한 당 몇 가지 과제가 나타나고 감당 하기 어려운 파티션당 64 개 VPs 지원 만든 복잡성을 도입 합니다.  이 해결 하기 위해 Hyper-v 기본 컴퓨터에는 사용할 수 있는 많은 더 많은 논리 프로세서는 경우에 VPs 64와 루트 파티션에 지정 된의 수를 제한 합니다.  하이퍼바이저는 계속 게스트 VPs 실행에 대 한 모든 사용 가능한 LPs를 사용 하지만 64에서 루트 파티션에 인위적으로 제한 합니다.  이 구성은 "최소 루트" 또는 "minroot" 구성 이라고 부르게 되었습니다.  도 LPs 64 개를 사용 하 여 대규모 시스템에서 루트 64 개 이상의 루트 VPs 지원을 제공 하기 위해 충분 한 수가 많은 게스트 Vm 및 게스트 VPs –를 실제로 필요 하지 않은, 64 보다 훨씬 작은 루트 VPs가 적절 한 자주 확인 성능 테스트 물론 등 특정 워크 로드를 실행 중인 게스트 Vm의 크기와 수에 따라 합니다.

이 "minroot" 개념을 지금 활용할 수 계속 합니다.  사실, Windows Server 2016 Hyper-v 512 LPs LPs 호스트에 대해 최대 아키텍처 지원 제한 증가 루트 파티션에 최대 320 LPs 제한 수 있습니다.

## <a name="using-minroot-to-constrain-and-isolate-host-compute-resources"></a>Minroot을 제한 하 고 호스트 계산 리소스 격리를 사용 하 여
Minroot 구성 320 LPs에서 Windows Server 2016 Hyper-v의 높은 기본 임계값을 사용 하 여 매우 큰 서버 시스템에 활용할 수만 됩니다.  그러나이 기능은 Hyper-v 호스트 관리자가 훨씬 더 낮은 임계값 하도록 고 크게 루트 파티션에 사용할 수 있는 호스트 CPU 리소스의 양을 제한 하는 데 사용 되므로 수 있습니다.  루트 LPs 활용 하는 특정 개수의 Vm 호스트에 할당 된 작업의 최대 요구 사항에 신중 하 게 물론 선택 해야 합니다.  그러나 호스트 LPs 수에 대 한 적절 한 값은 신중 하 게 평가 통해 결정 및 프로덕션 워크 로드를 모니터링 되 고 광범위 한 배포 하기 전에 비프로덕션 환경에서 검증 된 수 있습니다.

## <a name="enabling-and-configuring-minroot"></a>설정 및 Minroot 구성

Minroot 구성 하이퍼바이저 BCD 항목을 통해 제어 됩니다. 관리자 권한으로 명령 프롬프트에서 minroot 수 있도록 합니다.

```
    bcdedit /set hypervisorrootproc n
```
여기서 n은 루트 VPs의 개수입니다. 

시스템 다시 부팅 해야, 및 OS 부팅의 수명에 대 한 새 루트 프로세서 수가 유지 됩니다.  Minroot 구성은 런타임에 동적으로 변경할 수 없습니다.

각 노드에 표시 됩니다 여러 NUMA 노드가 없으면 `n/NumaNodeCount` 프로세서.

여러 NUMA 노드가 있는 되지 않도록 해야 VM의 토폴로지는 충분 한 여유 LPs (즉, 루트 VPs 없이 LPs)는 해당 VM의 NUMA 노드 VPs를 실행 하려면 각 NUMA 노드에서 note 합니다.

## <a name="verifying-the-minroot-configuration"></a>Minroot 구성 확인

아래와 같이 작업 관리자를 사용 하 여 호스트의 minroot 구성을 확인할 수 있습니다.

![](./media/minroot-taskman.png)

Minroot 활성 상태인 경우 작업 관리자는 시스템의 논리적 프로세서의 총 외에도 호스트에 현재 할당 된 논리 프로세서 수가 표시 됩니다.
 
