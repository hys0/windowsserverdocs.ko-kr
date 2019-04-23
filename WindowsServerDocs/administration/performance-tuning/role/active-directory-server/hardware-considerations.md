---
title: AD 성능 튜닝의 하드웨어 고려 사항
description: AD 성능 튜닝의 하드웨어 고려 사항
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: TimWi; ChrisRob; HerbertM; KenBrumf;  MLeary; ShawnRab
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 0f1aa1e3c07c5cb9238a332156abfec248e74176
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866094"
---
# <a name="hardware-considerations-in-adds-performance-tuning"></a>추가 성능 튜닝의 하드웨어 고려 사항 

>[!Important]
> 다음은 주요 권장 사항 및 고려 사항에서 더 자세히 설명 하는 Active Directory 워크 로드에 대 한 서버 하드웨어를 최적화 하기 위해 요약이 합니다 [Active Directory Domain Services에 대 한 용량 계획](https://go.microsoft.com/fwlink/?LinkId=324566) 문서. 판독기가 검토 하는 것이 좋습니다 [Active Directory Domain Services에 대 한 용량 계획](https://go.microsoft.com/fwlink/?LinkId=324566) 에 대 한 큰 기술 이해 및 이러한 권장 사항의 영향을 줍니다.

## <a name="avoid-going-to-disk"></a>디스크에 방지

메모리 수 만큼 데이터베이스의 active Directory 캐시 합니다. 메모리에서 페이지를 페치하는 중 이며 배나 미디어가 스핀 들 또는 SSD 기반 실제 미디어 하는 것 보다 더 빠르게 디스크 I/O를 최소화 하기 위해 더 많은 메모리를 추가 합니다.

-   Active Directory 모범 사례 권장 전체 DIT 메모리로 로드 하는 운영 체제 및 바이러스 백신, 백업 소프트웨어와 같은 기타 설치 된 응용 프로그램을 수용할 수 있도록 RAM을 충분히 배치 모니터링 등에입니다.

    -   기존 플랫폼의 제한 사항에 대해서 [Windows Server 2003 또는 Windows 2000 Server를 실행 하는 도메인 컨트롤러에서 Lsass.exe 프로세스의 메모리 사용량이](https://support.microsoft.com/kb/308356)합니다.

    -   메모리를 사용 하 여\\장기 평균 대기 캐시 수명 (초) &gt; 30 분 동안 성능 카운터입니다.

-   별도 볼륨에 운영 체제, 로그 및 데이터베이스를 배치 합니다. 모든 또는 대부분의 DIT 캐시할 수 있는지는 캐시가 준비 될 하 고 안정 된 상태에서이 작은 관련 되며 저장소 레이아웃에 약간 더 많은 유연성을 제공 합니다. 전체 DIT을 캐싱할 수 없는 시나리오에서는 운영 체제, 로그 및 별도 볼륨에 대 한 데이터베이스 분할의 중요도 더욱 커지고 있습니다.

-   일반적으로 DIT에 I/O 비율은 약 90% 읽기 및 쓰기 10%입니다. 10%-20%에 쓰기 I/O 볼륨 크게 초과 시나리오 쓰기 작업이 많은 것으로 간주 됩니다. 쓰기 작업이 많은 시나리오에서 Active Directory 캐시 크게 유용 하지 않습니다. 디렉터리에 기록 되는 데이터의 트랜잭션 영속성을 보장 하기 위해 Active Directory 수행 하지 않습니다 디스크 쓰기 캐싱. 를 커밋합니다 디스크에 모든 쓰기 작업을 작업에 대 한 완료 상태를 반환 하기 전에 명시적으로 요청할이 작업을 수행할 필요가 없는 합니다. 따라서 빠른 디스크 I/O가 Active Directory에 쓰기 작업의 성능에 중요 합니다. 다음은 이러한 시나리오의 성능을 향상 시킬 수 있는 하드웨어 권장 사항입니다.

    -   하드웨어 RAID 컨트롤러

    -   DIT 및 로그 파일을 호스트 하는 낮은 대기 시간/높은 RPM 디스크의 수를 늘리려면

    -   컨트롤러에 쓰기 캐시

-   각 볼륨에 대해 개별적으로 디스크 하위 시스템 성능을 검토 합니다. 대부분의 Active Directory 시나리오는 주로 읽기 기반, DIT를 호스트 하는 볼륨에 대 한 통계를 검사 하는 가장 중요 한 되므로 합니다. 그러나 수행 하지 간과 운영 체제를 비롯 한 드라이브의 나머지 부분을 모니터링 하 고 로그 파일 드라이브입니다. 도메인 컨트롤러 성능 병목 현상이 되는 저장소를 방지 하려면 올바르게 구성 되어 있는지 확인, 표준 저장소 권장 사항에 대 한 저장소 하위 시스템에 대 한 섹션을 참조 합니다. 다양 한 환경에서 개념 급증 이나 로드의 급증을 수용 하기 위해 헤드 충분 한 공간이 있는지 확인 하는 것입니다. 이러한 임계값은 경고 여기서는 공간 급증 이나 로드의 급증을 수용 하기 위해 임계값 제한 됩니다 및 클라이언트 응답성이 저하 됩니다. 그러나 즉, 이러한 임계값을 초과 아니며 단기 (5 ~ 15 분 하루에 몇 번)에 잘못 된, 이러한 종류의 통계를 사용 하 여 지속적으로 실행 하는 시스템 데이터베이스를 완전히 캐시 되지가 될 수 세금이 부과 됩니다 하 고 조사 해야 합니다.

    -   Database ==&gt; Instances(lsass/NTDSA)\\I/O Database Reads Averaged Latency &lt; 15ms

    -   Database ==&gt; Instances(lsass/NTDSA)\\I/O Database Reads/sec &lt; 10

    -   Database ==&gt; Instances(lsass/NTDSA)\\I/O Log Writes Averaged Latency &lt; 10ms

    -   Database ==&gt; Instances(lsass/NTDSA)\\I/O Log Writes/sec – informational only.

        데이터의 일관성을 유지 하려면 모든 변경 내용이 로그에 작성 되어야 합니다. 좋은 또는 잘못 된 번호가 없으면 여기, 얼마나 많은 저장소를 지 원하는의 측정값만 있습니다.

-   사용량 감소 시 로드 기간에 대 한 백업 및 바이러스 검색과 같은 비핵심 디스크 I/O 로드를 계획 합니다. 또한 Active Directory의 I/O 요구를 사용 하 여 경합을 줄이기 위해 Windows Server 2008에서 도입 된 우선 순위가 낮은 I/O 기능을 지 원하는 백업 및 바이러스 백신 솔루션을 사용 합니다.

## <a name="dont-over-tax-the-processors"></a>프로세서를 세 개 안 함

충분 한 여유 주기 없는 프로세서는 실행에 대 한 프로세서에는 스레드를 가져오는 방법에 긴 대기 시간이 발생할 수 있습니다. 다양 한 환경에서 개념 급증을 수용 하기 위해 헤드 충분 한 공간이 있는지 확인 하는 것 또는 이러한 시나리오에서 클라이언트 응답성에 미치는 영향을 최소화 하기 위해 부하가 급증 합니다. 하지만 즉, 초과 임계값 아닙니다 단기 (5 ~ 15 분 하루에 몇 번)에 잘못 된 모든 헤드 비정상적인 로드를 수용 하기 위해 공간 및 초과 쉽게 전환할 수 있습니다 이러한 종류의 통계를 사용 하 여 지속적으로 실행 하는 시스템 제공 하지 않습니다 세금이 부과 s 시나리오입니다. 지출 임계값 오랫동안 지속 되 면된 시스템 프로세서 로드를 줄이는 방법에 조사 해야 합니다.

-   프로세서를 선택 하는 방법에 대 한 자세한 내용은 참조 하세요. [서버 하드웨어에 대 한 성능 튜닝](../../hardware/index.md)합니다.

-   하드웨어를 추가, 부하 최적화, 클라이언트를 다른 곳에서 직접 또는 CPU 부하를 줄이기 위해 환경에서 부하를 제거 합니다.

-   프로세서 정보를 사용 하 여 (\_총)\\% Processor Utilization &lt; 성능 카운터를 60%입니다.

## <a name="avoid-overloading-the-network-adapter"></a>네트워크 어댑터를 오버 로드 방지

마찬가지로 프로세서를 사용 하 여 과도 한 네트워크 어댑터 사용률 하면 네트워크에 로그온 하는 아웃 바운드 트래픽에 대 한 긴 대기 시간. Active Directory가 인바운드 요청을 작은 경향이 및 상대적으로 훨씬 더 많은 양의 데이터 클라이언트 시스템에 반환 합니다. 전송된 데이터 수신된 된 데이터를 훨씬 초과합니다. 다양 한 환경에서 개념 급증 이나 로드의 급증을 수용 하기 위해 헤드 충분 한 공간이 있는지 확인 하는 것입니다. 이 임계값 여기서는 공간 급증 이나 로드의 급증을 수용 하기 위해 경고 임계값은 제한 되어 클라이언트 응답성이 저하 됩니다. 하지만 즉, 이러한 임계값을 초과 아닙니다. 단기 (5 ~ 15 분 하루에 몇 번)에 잘못 된 이러한 종류의 통계를 사용 하 여 지속적으로 실행 하는 시스템을 통해 세금이 부과 이며 조사 해야 합니다.

-   네트워크 하위 시스템을 튜닝 하는 방법에 대 한 자세한 내용은 참조 하세요. [네트워크 하위 시스템에 대 한 성능 튜닝](../../../../networking/technologies/network-subsystem/net-sub-performance-top.md)합니다.

-   비교 NetworkInterface를 사용 하 여 (\*)\\NetworkInterface 사용 하 여 Bytes Sent/Sec (\*)\\현재 대역폭 성능 카운터입니다. 비율이 60% 미만 사용 해야 합니다.

## <a name="see-also"></a>참조
- [Active Directory 서버를 튜닝 하는 성능](index.md)
- [LDAP 고려 사항](ldap-considerations.md)
- [적절 한 배치의 도메인 컨트롤러와 사이트 고려 사항](site-definition-considerations.md)
- [추가 성능 문제 해결](troubleshoot.md) 
- [Active Directory Domain Services를 위한 용량 계획](https://go.microsoft.com/fwlink/?LinkId=324566)