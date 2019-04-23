---
title: 빠른 응답 시간에 대 한 균형 조정된 전원 계획 매개 변수를이 좋습니다.
description: 빠른 응답 시간에 대 한 균형 조정된 전원 계획 매개 변수를이 좋습니다.
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Qizha;TristanB
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 134e868e1400729f754039fc8120cea0c73945bf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878794"
---
# <a name="recommended-balanced-power-plan-parameters-for-workloads-requiring-quick-response-times"></a>빠른 응답 시간이 필요한 워크 로드에 대 한 균형 조정된 전원 계획 매개 변수를 권장

기본값 **부하 분산** 계획 사용 하 여 power **처리량** 튜닝을 위한 성능 기준으로 합니다. 안정적인 상태에 있는 동안 **처리량** 시스템 오버 로드 된 완전히 (~ 100% 사용률) 될 때까지 다양 한 사용률에 따라 변경 되지 않습니다.  결과적으로 **부하 분산** 전원 프로세서 빈도 최소화 하 고 사용률 극대화를 많이 기능을 선호 합니다.

그러나 **응답 시간** 사용률 증가 사용 하 여 기하급수적으로 증가할 수 있습니다. 오늘날의 빠른 응답 시간 요구 사항이 크게 증가 했습니다. Microsoft 제안으로 전환 사용자도는 **고성능** 전원 계획 빠른 응답 시간을 필요할 때 일부 사용자에 게 하지 않으려는 보통 수준의 부하 수준으로 조명 하는 동안 전원 이점을 잃게 됩니다. 따라서 Microsoft는 빠른 응답 시간을 요구 하는 워크 로드에 대 한 다음 제안 된 매개 변수 변경 내용 집합을 제공 합니다.


| 매개 변수 | 설명 | 기본값 | 제안 된 값 |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| 프로세서 성능 증가 임계값 | 증가 하는 빈도 사용률 임계값 위의 | 90 | 60 |
| 프로세서 성능 저하 임계값 | 사용률 임계값 아래 빈도를 줄이려면 | 80 | 40 |
| 프로세서 성능 증가 시간 | 빈도 증가 되기 위해 먼저 PPM 확인 기간 수 | 3 | 1 |
| 프로세서 성능 증가 정책 | 높이 빈도 속도 | Single | 적합함 |

제안 된 값을 설정 하려면 사용자는 관리자를 사용 하 여 창에서 다음 명령을 실행할 수 있습니다.

``` syntax
Powercfg -setacvalueindex scheme_balanced sub_processor PERFINCTHRESHOLD 60
Powercfg -setacvalueindex scheme_balanced sub_processor PERFDECTHRESHOLD 40
Powercfg -setacvalueindex scheme_balanced sub_processor PERFINCTIME 1
Powercfg -setacvalueindex scheme_balanced sub_processor PERFINCPOL 0
Powercfg -setactive scheme_balanced
```

이 변경은 성능 및 다음 워크 로드를 사용 하 여 전원 균형 분석을 기반으로 합니다. 특정 SLA 요구 사항이 전력 효율성을 튜닝 하는 더욱 세밀 하 게 하려는 사용자에 대 한 참조 하세요 [서버 하드웨어에 대 한 성능 고려 사항](../power.md)합니다.

>[!Note]
> 추가 권장 사항 및 가상화 된 작업을 튜닝할 전원 계획을 활용 하 여에 대 한 정보를 읽기 [hyper-v 구성](../../role/hyper-v-server/configuration.md)

## <a name="specpower--java-workload"></a>SPECpower – JAVA 워크 로드

[SPECpower\_ssj2008](http://spec.org/power_ssj2008/)가장 서버 기능과 성능 특성에 대 한 인기 있는 업계 표준 사양 벤치 마크 power 영향 확인을 위해 사용 합니다. 만 사용 하므로 **처리량** 기본 성능 메트릭으로 **균형** 전원 계획 모범 전력 효율성을 제공 합니다.

제안 된 매개 변수에서 광원에서 전력과 약간 높습니다 (즉, < = 20%) 부하 수준입니다. 하지만 부하 사용 하 여 더 높은 수준에서 차이 증가 하 고으로 동일한 전력을 소비 하기 시작 합니다 **고성능** 60% 부하 수준이 후 전원 계획입니다. 제안 된 변경 매개 변수를 사용 하려면 해당 랙 용량 계획 중 사용자 수준 높은 부하를 중간에서 전원 비용 인식 이어야 합니다.

## <a name="geekbench-3"></a>GeekBench 3

[GeekBench 3](http://www.geekbench.com/geekbench3/) 은 단일 코어 및 다중 코어 성능에 대 한 점수를 구분 하는 플랫폼 간 프로세서 벤치 마크입니다. 정수 작업 (암호화, 압축, 이미지 처리, 등)를 포함 하 여 작업, 부동 지점 워크 로드 (모델링, 프랙탈, 이미지를 선명 하 게, 흐리게 표시 이미지 등) 및 (스트리밍) 메모리 작업 집합을 시뮬레이션 합니다.

**응답 시간** 점수 계산의 주요 측정값입니다. 테스트 시스템에서 기본값 **부하 분산** 전원 관리 옵션에 비해 다중 코어 테스트에서 단일 코어 테스트 및 ~ 40% 회귀에 대 한 ~ 18% 회귀 합니다 **고성능** 전원 계획입니다. 이러한 회귀를 제거 하는 제안된 된 변경 합니다.

## <a name="diskspd"></a>DiskSpd

[Diskspd](https://en.wikipedia.org/wiki/Diskspd) Microsoft에서 개발한 storage 벤치 마크에 대 한 명령줄 도구입니다. 광범위 하 게 다양 한 저장소 성능 분석에 대 한 저장소 시스템에 대 한 요청을 생성 하는 것이 됩니다.

[장애 조치 클러스터를]를 설정 하 고 임의 및 순차적 읽기를 생성 하 고 다른 IO 크기를 사용 하 여 로컬 및 원격 저장소 시스템에 쓰기 Io를 Diskspd를 사용 합니다. 테스트를 통해 서로 다른 전원 계획에서 IO 응답 시간을 프로세서 빈도에 매우 민감합니다 보여 줍니다. **부하 분산** 전원 계획에서의 응답 시간 double 수 합니다 **고성능** 특정 워크 로드에서 전원 계획입니다. 제안된 된 변경 재발의 대부분을 제거합니다.

>[!Important]
>Windows Server 2016을 실행 하는 [Broadwell] Intel 프로세서에서 시작 하며, 대부분의 프로세서 전원 관리 의사 결정에 대 한 OS 수준 대신 프로세서에서 워크 로드 변화에 빠르게 장구 달성. OS에서 사용 하는 레거시 PPM 매개 변수를 실제 빈도 결정 전원 또는 성능을 선호 하는 프로세서를 전달 하거나 최소 및 최대 빈도 제한 제외 하 고에 최소한의 영향을 미칠 합니다. 따라서 사전 Broadwell 시스템에만 제안된 된 PPM 매개 변수 변경 대상으로 합니다.

## <a name="see-also"></a>관련 항목
- [서버 하드웨어에 대 한 성능 고려 사항](../index.md)
- [서버 하드웨어에 대 한 전원 고려 사항](../power.md)
- [전원 및 성능 조정](power-performance-tuning.md)
- [프로세서 전원 관리 튜닝](processor-power-management-tuning.md)
- [장애 조치 클러스터](https://technet.microsoft.com/library/cc725923.aspx)
