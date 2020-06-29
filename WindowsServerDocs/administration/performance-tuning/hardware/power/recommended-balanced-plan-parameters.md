---
title: 빠른 응답 시간에 대 한 권장 분산 전원 계획 매개 변수
description: 빠른 응답 시간에 대 한 권장 분산 전원 계획 매개 변수
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: conceptual
ms.author: qizha;tristanb
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 62dc6168e76bf3951443df0f06c47a8684d2df26
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471588"
---
# <a name="recommended-balanced-power-plan-parameters-for-workloads-requiring-quick-response-times"></a>빠른 응답 시간이 필요한 워크 로드에 대해 권장 되는 분산 전원 계획 매개 변수

**분산** 된 기본 전원 계획은 튜닝을 위한 성능 메트릭으로 **처리량** 을 사용 합니다. 안정적인 상태에서는 시스템이 완전히 오버 로드 (~ 100% 사용률) 될 때까지 다양 한 사용률으로 **처리량** 이 변경 되지 않습니다.  따라서 **균형 조정** 된 전원 계획은 프로세서 빈도를 최소화 하 고 사용률을 최대화 하 여 전력에 크게 우위를 적용 합니다.

그러나 사용률이 증가 함에 **따라 응답 시간이** 급격히 늘어날 수 있습니다. 오늘날 빠른 응답 시간에 대 한 요구 사항이 크게 증가 했습니다. Microsoft에서 사용자에 게 빠른 응답 시간이 필요한 경우 **고성능** 전원 계획으로 전환 하는 것을 제안 했지만, 일부 사용자는 보통 부하 수준에 대 한 전력 혜택을 잃지 않으려고 합니다. 따라서 Microsoft는 빠른 응답 시간이 필요한 워크 로드에 대해 다음과 같은 권장 매개 변수 변경 집합을 제공 합니다.


| 매개 변수 | Description | 기본값 | 제안 된 값 |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| 프로세서 성능 증가 임계값 | 빈도가 증가 하는 임계값을 초과 하는 사용률 임계값 | 90 | 60 |
| 프로세서 성능 감소 임계값 | 빈도가 감소 되는 사용률 임계값 | 80 | 40 |
| 프로세서 성능 증가 시간 | 빈도를 늘리기 전까지 최대 PPM 확인 창 수 | 3 | 1 |
| 프로세서 성능 증가 정책 | 빈도가 증가 하는 속도 | Single | 이상적 |

사용자는 제안 된 값을 설정 하기 위해 관리자 권한으로 창에서 다음 명령을 실행할 수 있습니다.

``` syntax
Powercfg -setacvalueindex scheme_balanced sub_processor PERFINCTHRESHOLD 60
Powercfg -setacvalueindex scheme_balanced sub_processor PERFDECTHRESHOLD 40
Powercfg -setacvalueindex scheme_balanced sub_processor PERFINCTIME 1
Powercfg -setacvalueindex scheme_balanced sub_processor PERFINCPOL 0
Powercfg -setactive scheme_balanced
```

이러한 변경은 다음 작업을 사용 하 여 성능 및 전원 균형 분석을 기반으로 합니다. 특정 SLA 요구 사항에 따라 전원 효율성을 더 세밀 하 게 조정 하려는 사용자의 경우 [서버 하드웨어 성능 고려 사항](../power.md)을 참조 하세요.

>[!Note]
> 전원 계획을 활용 하 여 가상화 된 워크 로드를 조정 하는 방법에 대 한 추가 권장 사항 및 정보는 [Hyper-v 구성](../../role/hyper-v-server/configuration.md)

## <a name="specpower--java-workload"></a>SPECpower – JAVA 워크 로드

서버 전원 및 성능 특성에 대 한 가장 인기 있는 업계 표준 사양 벤치 [SPECpower \_ ssj2008](http://spec.org/power_ssj2008/)는 전원 영향을 확인 하는 데 사용 됩니다. **처리량** 은 성능 메트릭 으로만 사용 되므로 **분산** 된 기본 전원 계획은 최상의 전원 효율성을 제공 합니다.

제안 된 매개 변수 변경 내용이 빛에서 약간 더 높습니다 (예: <= 20%). 로드 수준. 그러나 더 높은 부하 수준을 사용 하면 차이가 늘어나고 60% 로드 수준 후에 **고성능** 전원 계획과 동일한 기능을 사용 하기 시작 합니다. 제안 된 변경 매개 변수를 사용 하려면 사용자가 랙 용량 계획 중에 보통에서 높은 부하 수준으로 전력 비용을 인식 해야 합니다.

## <a name="geekbench-3"></a>GeekBench 3

[GeekBench 3](http://www.geekbench.com/geekbench3/) 은 단일 코어 및 다중 코어 성능의 점수를 구분 하는 플랫폼 간 프로세서 벤치 마크입니다. 이는 정수 작업 (암호화, 압축, 이미지 처리 등), 부동 소수점 작업 (모델링, 프랙탈, 이미지 선명 효과, 이미지 흐림 등) 및 메모리 워크 로드 (스트리밍)를 비롯 한 워크 로드 집합을 시뮬레이션 합니다.

**응답 시간은** 점수 계산에서 중요 한 측정값입니다. 테스트 된 시스템에서 기본 **균형이 조정** 된 전원 계획은 단일 코어 테스트에서 ~ 18%의 회귀를 포함 하 고, 다중 코어 테스트에서 40% 회귀를 수행 하는 **고성능** 전원 계획과 비교 합니다. 제안 된 변경 내용으로 이러한 재발이 제거 됩니다.

## <a name="diskspd"></a>DiskSpd

[Diskspd](https://en.wikipedia.org/wiki/Diskspd) 는 Microsoft에서 개발한 저장소 벤치마킹을 위한 명령줄 도구입니다. 저장소 성능 분석을 위해 저장소 시스템에 대해 다양 한 요청을 생성 하는 데 널리 사용 됩니다.

[장애 조치 (Failover) 클러스터]를 설정 하 고 Diskspd를 사용 하 여 임의 및 순차를 생성 하 고 다른 IO 크기를 사용 하 여 로컬 및 원격 저장소 시스템에 대 한 IOs를 읽고 씁니다. 테스트 결과 IO 응답 시간이 다른 전원 계획에서 프로세서 주파수와 매우 중요 하다는 것을 알 수 있습니다. **분산** 된 전원 계획은 특정 워크 로드에서 **고성능** 전원 계획의 응답 시간을 두 배로 증가 시킬 수 있습니다. 제안 된 변경 내용으로 인해 대부분의 재발이 제거 됩니다.

>[!Important]
>Windows Server 2016를 실행 하는 Intel [Broadwell] 프로세서에서 시작 하 여 대부분의 프로세서 전원 관리 결정은 OS 수준 대신 프로세서에서 수행 되어 워크 로드 변경에 대 한 더 빠른 장구을 구현 합니다. OS에서 사용 하는 레거시 PPM 매개 변수는 실제 빈도 결정에 거의 영향을 주지 않습니다. 단, 전원 또는 성능을 선호 해야 하는 경우 프로세서를 지정 하거나 최소 및 최대 빈도를 50, 합니다. 따라서 제안 된 PPM 매개 변수 변경 내용은 사전 Broadwell 시스템을 대상으로 합니다.

## <a name="see-also"></a>참고 항목
- [서버 하드웨어에 대한 성능 고려 사항](../index.md)
- [서버 하드웨어에 대한 전원 고려 사항](../power.md)
- [전원 및 성능 튜닝](power-performance-tuning.md)
- [프로세서 전원 관리 튜닝](processor-power-management-tuning.md)
- [장애 조치(failover) 클러스터](https://technet.microsoft.com/library/cc725923.aspx)
