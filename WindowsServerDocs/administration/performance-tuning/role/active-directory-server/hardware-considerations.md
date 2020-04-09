---
title: AD 성능 조정의 하드웨어 고려 사항
description: AD 성능 조정의 하드웨어 고려 사항
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: timwi; chrisrob; herbertm; kenbrumf;  mleary; shawnrab
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: c40faca06668adf6fd29a5e4e753e5790b8104b7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851916"
---
# <a name="hardware-considerations-in-adds-performance-tuning"></a>성능 튜닝 추가의 하드웨어 고려 사항 

>[!Important]
> 다음은 [Active Directory Domain Services의 용량 계획](https://go.microsoft.com/fwlink/?LinkId=324566) 문서에 자세히 설명 된 Active Directory 워크 로드에 대 한 서버 하드웨어 최적화에 대 한 주요 권장 사항 및 고려 사항에 대 한 요약입니다. 독자 들은 이러한 권장 사항에 대 한 보다 기술적 이해와 의미를 위해 [Active Directory Domain Services에 대 한 용량 계획](https://go.microsoft.com/fwlink/?LinkId=324566) 을 검토 하는 것이 좋습니다.

## <a name="avoid-going-to-disk"></a>디스크로 이동 하지 않습니다.

Active Directory는 메모리를 허용 하는 만큼의 데이터베이스를 캐시 합니다. 메모리에서 페이지를 인출 하는 것은 미디어가 헤드 또는 SSD 기반 인지 여부에 관계 없이 실제 미디어로 이동 하는 것 보다 더 빠른 크기의 주문입니다. 디스크 i/o를 최소화 하기 위해 메모리를 추가 합니다.

-   Active Directory 모범 사례는 전체 DIT를 메모리로 로드 하 고 바이러스 백신, 백업 소프트웨어, 모니터링 등의 기타 설치 된 응용 프로그램을 수용 하는 데 충분 한 RAM을 설정 하는 것이 좋습니다.

    -   레거시 플랫폼의 제한 사항은 [Windows Server 2003 또는 windows 2000 server를 실행 하는 도메인 컨트롤러의 lsass.exe 프로세스에서 메모리 사용량](https://support.microsoft.com/kb/308356)을 참조 하세요.

    -   메모리\\장기 평균 대기 캐시 수명 &gt; 30 분 성능 카운터를 사용 합니다.

-   운영 체제, 로그 및 데이터베이스를 별도의 볼륨에 배치 합니다. DIT의 모든 또는 과반수를 캐시할 수 있는 경우 캐시가 준비 안정 된 상태에 있으면이는 관련성이 낮고 저장소 레이아웃의 유연성이 약간 향상 됩니다. 전체 DIT를 캐시할 수 없는 시나리오에서는 운영 체제, 로그 및 데이터베이스를 별도의 볼륨에 분할 하는 것이 더 중요 합니다.

-   일반적으로 DIT에 대 한 i/o 비율은 90% 읽기 및 10% 쓰기에 해당 합니다. 쓰기 i/o 볼륨이 10%-20%를 초과 하는 시나리오는 쓰기가 많은 것으로 간주 됩니다. 쓰기 작업이 많은 시나리오는 Active Directory 캐시의 이점을 크게 활용 하지 않습니다. 디렉터리에 기록 되는 데이터의 트랜잭션 내 구성을 보장 하기 위해 Active Directory는 디스크 쓰기 캐싱을 수행 하지 않습니다. 대신이 작업을 수행 하지 않는 명시적 요청이 있는 경우를 제외 하 고 작업에 대 한 성공적인 완료 상태를 반환 하기 전에 디스크에 대 한 모든 쓰기 작업을 커밋합니다. 따라서 고속 디스크 i/o는 Active Directory에 대 한 쓰기 작업의 성능에 중요 합니다. 다음은 이러한 시나리오에 대 한 성능을 향상 시킬 수 있는 하드웨어 권장 사항입니다.

    -   하드웨어 RAID 컨트롤러

    -   DIT 및 로그 파일을 호스팅하는 짧은 대기 시간/RPM 디스크 수 늘리기

    -   컨트롤러에 대 한 쓰기 캐싱

-   각 볼륨에 대 한 디스크 하위 시스템 성능을 개별적으로 검토 합니다. 대부분의 Active Directory 시나리오는 주로 읽기 기반 이므로 DIT를 호스트 하는 볼륨에 대 한 통계를 검사 하는 것이 가장 중요 합니다. 그러나 운영 체제 및 로그 파일 드라이브를 비롯 한 나머지 드라이브 모니터링은 간과 하지 마십시오. 저장소 성능에 대 한 병목 현상이 발생 하지 않도록 도메인 컨트롤러가 올바르게 구성 되었는지 확인 하려면 표준 저장소 권장 사항에 대 한 저장소 하위 시스템 섹션을 참조 하세요. 많은 환경에서 원리는 부하 급증 또는 급증을 수용할 수 있는 충분 한 헤드 공간이 있는지 확인 하는 것입니다. 이러한 임계값은 부하의 급증 또는 급증을 수용 하는 헤드 공간이 제한 되 고 클라이언트 응답성이 저하 되는 경고 임계값입니다. 간단히 말해서 이러한 임계값을 초과 하는 것은 단기 (5 ~ 15 분의 하루에 몇 번)에서 잘못 된 것 이지만 이러한 종류의 통계를 사용 하 여 지속적으로 실행 되는 시스템은 데이터베이스를 완전히 캐싱하지 않으며 taxed 될 수 있으므로 조사 해야 합니다.

    -   Database = =&gt; Instances (lsass/NTDSA)\\i/o 데이터베이스 읽기 평균 대기 시간 &lt; 15ms

    -   Database = =&gt; 인스턴스 (lsass/NTDSA)\\i/o Database Reads/sec &lt; 10

    -   Database = =&gt; 인스턴스 (lsass/NTDSA)\\i/o 로그 쓰기 평균 대기 시간 &lt; 10ms

    -   Database = =&gt; 인스턴스 (lsass/NTDSA)\\i/o 로그 쓰기/초 – 정보 제공 용입니다.

        데이터의 일관성을 유지 하려면 모든 변경 내용을 로그에 써야 합니다. 여기에는 올바른 또는 잘못 된 숫자가 없으며, 저장소에서 지 원하는 정도를 측정 한 것입니다.

-   사용량이 많지 않은 로드 기간에 대해 백업 및 바이러스 백신 검색과 같은 비 코어 디스크 i/o 로드를 계획 합니다. 또한 Windows Server 2008에 도입 된 낮은 우선 순위의 i/o 기능을 지 원하는 백업 및 바이러스 백신 솔루션을 사용 하 여 Active Directory의 i/o 요구에 대 한 경쟁을 줄일 수 있습니다.

## <a name="dont-over-tax-the-processors"></a>프로세서의 세금을 초과 하지 않음

사용 가능한 주기가 충분 하지 않은 프로세서는 실행을 위해 프로세서에 스레드를 가져오는 데 긴 대기 시간이 발생할 수 있습니다. 대부분의 환경에서 이러한 시나리오에서 클라이언트 응답성에 미치는 영향을 최소화 하기 위해 부하의 급증 또는 급증을 수용 하기에 충분 한 헤드 공간이 있는지 확인 하는 것이 좋습니다. 즉, 아래 임계값을 초과 하는 것은 단기 (5 ~ 15 분 a 일)에서 잘못 된 것 이지만 이러한 종류의 통계를 사용 하 여 지속적으로 실행 되는 시스템은 비정상적인 부하를 수용할 수 있는 충분 한 공간을 제공 하지 않으며 taxed 시나리오에 쉽게 적용할 수 있습니다. 임계값을 초과 하는 기간 동안 지속 되는 기간을 초과 하는 시스템은 프로세서 부하를 줄이는 방법으로 조사 해야 합니다.

-   프로세서를 선택 하는 방법에 대 한 자세한 내용은 [서버 하드웨어 성능 조정](../../hardware/index.md)을 참조 하세요.

-   CPU 부하를 줄이기 위해 하드웨어를 추가 하거나, 부하를 최적화 하 고, 다른 곳에서 클라이언트를 추가 하거나, 환경에서 로드를 제거 합니다.

-   프로세서 정보 (총\_)\\% 프로세서 사용률 &lt; 60% 성능 카운터를 사용 합니다.

## <a name="avoid-overloading-the-network-adapter"></a>네트워크 어댑터 오버 로드 방지

프로세서의 경우와 마찬가지로 과도 한 네트워크 어댑터를 사용 하면 아웃 바운드 트래픽이 네트워크에 전송 될 때까지 대기 시간이 길어질 수 있습니다. Active Directory은 작은 인바운드 요청을 포함 하 고 있으며 클라이언트 시스템에 반환 되는 데이터의 양이 매우 많은 경향이 있습니다. 보낸 데이터는 받은 데이터를 초과 합니다. 많은 환경에서 원리는 부하 급증 또는 급증을 수용할 수 있는 충분 한 헤드 공간이 있는지 확인 하는 것입니다. 이 임계값은 부하의 급증 또는 급증을 수용 하는 헤드 공간이 제한 되 고 클라이언트 응답성이 저하 되는 경고 임계값입니다. 간단히 말해서 이러한 임계값을 초과 하는 것은 단기 (5 ~ 15 분의 하루에 몇 번)에서 잘못 된 것 이지만 이러한 종류의 통계를 사용 하 여 지속적으로 실행 되는 시스템은 taxed를 초과 하 여 조사 해야 합니다.

-   네트워크 하위 시스템을 튜닝 하는 방법에 대 한 자세한 내용은 [네트워크 하위 시스템에 대 한 성능 조정](../../../../networking/technologies/network-subsystem/net-sub-performance-top.md)을 참조 하세요.

-   Compare NetworkInterface (\*)\\Bytes Sent/Sec with NetworkInterface (\*)\\Current 대역폭 성능 카운터를 사용 합니다. 비율은 60% 미만 이어야 합니다.

## <a name="see-also"></a>참고 항목
- [성능 튜닝 Active Directory 서버](index.md)
- [LDAP 고려 사항](ldap-considerations.md)
- [적절한 도메인 컨트롤러 배치 및 사이트 고려 사항](site-definition-considerations.md)
- [ADDS 성능 문제 해결](troubleshoot.md) 
- [Active Directory 도메인 서비스의 용량 계획](https://go.microsoft.com/fwlink/?LinkId=324566)