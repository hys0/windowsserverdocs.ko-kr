---
title: Hyper-v 가상 컴퓨터에서 Intel 성능 모니터링 하드웨어 사용
description: Hyper-v 컴퓨터에서 Intel의 성능 모니터링 하드웨어를 사용 하도록 설정 하는 방법 또한 성능 모니터링을 사용 하도록 설정 하는 방법에 대해서는 실시간 마이그레이션을 수행 합니다.
ms.prod: windows-server
ms.reviewer: ifufondu
author: ifeomaufondu-ms
ms.author: ifufondu
manager: chhuybre
ms.topic: article
ms.date: 09/20/2019
ms.openlocfilehash: 6938739d7c8efdf60c859d2d5ea5bc63246ae4fe
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364103"
---
# <a name="enable-intel-performance-monitoring-hardware-in-a-hyper-v-virtual-machine"></a>Hyper-v 가상 컴퓨터에서 Intel 성능 모니터링 하드웨어 사용

Intel 프로세서에는 성능 모니터링 하드웨어 (예: PMU, PEBS, LBR) 라고 하는 기능이 포함 되어 있습니다. 이러한 기능은 Intel VTune 증폭기와 같은 성능 튜닝 소프트웨어에서 소프트웨어 성능을 분석 하는 데 사용 됩니다.  Windows Server 2019 및 Windows 10 버전 1809 이전 버전에서는 Hyper-v를 사용 하도록 설정 했을 때 호스트 운영 체제와 Hyper-v 게스트 가상 컴퓨터 모두에서 성능 모니터링 하드웨어를 사용할 수 없습니다.  Windows Server 2019 및 Windows 10 버전 1809부터 호스트 운영 체제는 기본적으로 성능 모니터링 하드웨어에 액세스할 수 있습니다.  Hyper-v 게스트 가상 컴퓨터는 기본적으로 액세스 권한이 없지만 Hyper-v 관리자는 하나 이상의 게스트 가상 컴퓨터에 대 한 액세스 권한을 부여 하도록 선택할 수 있습니다.  이 문서에서는 게스트 가상 컴퓨터에 성능 모니터링 하드웨어를 노출 하는 데 필요한 단계에 대해 설명 합니다.

## <a name="requirements"></a>요구 사항

가상 컴퓨터에서 성능 모니터링 하드웨어를 사용 하도록 설정 하려면 다음이 필요 합니다.

- 성능 모니터링 하드웨어 (예: PMU, PEBS, IPT)를 포함 하는 Intel 프로세서
- Windows Server 2019 또는 Windows 10 버전 1809 (10 월 2018 업데이트) 이상
- [중첩 된 가상화](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization) 가 _없는_ hyper-v 가상 컴퓨터도 중지 된 상태입니다.
 
## <a name="enabling-performance-monitoring-components-in-a-virtual-machine"></a>가상 컴퓨터에서 성능 모니터링 구성 요소 사용

특정 게스트 가상 컴퓨터에 대해 다른 성능 모니터링 구성 요소를 사용 하도록 설정 `Set-VMProcessor` 하려면 PowerShell cmdlet을 사용 합니다.
 
``` Powershell
# Enable all components
Set-VMProcessor MyVMName -Perfmon @("pmu", "lbr", "pebs")
```
 
``` Powershell
# Enable a specific component
Set-VMProcessor MyVMName -Perfmon @("pmu")
```
 
``` Powershell
# Disable all components
Set-VMProcessor MyVMName -Perfmon @()
```
> [!NOTE]
> 성능 모니터링 구성 요소를 사용 하도록 설정 `"pebs"` 하는 경우을 `"pmu"` 지정한 경우을 지정 해야 합니다.  또한 호스트의 실제 프로세서에서 지원 하지 않는 구성 요소를 사용 하도록 설정 하면 가상 컴퓨터 시작 실패가 발생 합니다.
 
## <a name="effects-of-enabling-performance-monitoring-hardware-on-saverestore-export-and-live-migration"></a>저장/복원, 내보내기 및 실시간 마이그레이션에 대 한 성능 모니터링 하드웨어 사용의 효과
 
Microsoft는 다른 Intel 하드웨어를 사용 하는 시스템 간에 성능 모니터링 하드웨어를 사용 하 여 가상 컴퓨터를 실시간으로 마이그레이션하거나 저장/복원 하지 않는 것이 좋습니다. 성능 모니터링 하드웨어의 특정 동작은 종종 아키텍처와 Intel 하드웨어 시스템 간의 변경입니다.  서로 다른 시스템 간에 실행 중인 가상 컴퓨터를 이동 하면 아키텍처 카운터가 아닌 카운터의 예기치 않은 동작이 발생할 수 있습니다.