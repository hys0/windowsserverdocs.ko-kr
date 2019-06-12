---
title: 추가 성능 튜닝의 LDAP 고려 사항
description: Active Directory 워크 로드의 LDAP 고려 사항
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: TimWi; ChrisRob; HerbertM; KenBrumf;  MLeary; ShawnRab
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 7ac9453159fe97dc15ecbb2ab858214664a2a197
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811531"
---
# <a name="ldap-considerations-in-adds-performance-tuning"></a>추가 성능 튜닝의 LDAP 고려 사항

> [!IMPORTANT]
> 다음은 주요 권장 사항 및 고려 사항에서 더 자세히 설명 하는 Active Directory 워크 로드에 대 한 서버 하드웨어를 최적화 하기 위해 요약이 합니다 [Active Directory Domain Services에 대 한 용량 계획](https://go.microsoft.com/fwlink/?LinkId=324566) 문서. 판독기가 검토 하는 것이 좋습니다 [Active Directory Domain Services에 대 한 용량 계획](https://go.microsoft.com/fwlink/?LinkId=324566) 에 대 한 큰 기술 이해 및 이러한 권장 사항의 영향을 줍니다.

## <a name="verify-ldap-queries"></a>LDAP 쿼리를 확인 합니다.

LDAP 쿼리 만들기 효율적인 쿼리 권장 사항을 준수 하는지 확인 합니다.

제대로 구조를 작성 하 고 Active Directory 사용에 대 한 쿼리를 분석 하는 방법에 대 한 광범위 한 설명서 MSDN에 있습니다. 자세한 내용은 참조 하세요. [Creating More Efficient Microsoft Active Directory-Enabled 응용 프로그램](https://msdn.microsoft.com/library/ms808539.aspx)합니다.

## <a name="optimize-ldap-page-sizes"></a>LDAP 페이지 크기 최적화

클라이언트 요청에 따라에서 여러 개체를 사용 하 여 결과 반환 하는 경우 도메인 컨트롤러를 임시로 메모리에 결과 집합을 저장 해야 합니다. 페이지 크기를 증가 자세한 메모리 사용 하면 및 캐시에서 항목을 불필요 하 게 기간 수 있습니다. 이 경우 기본 설정에 가장 적합 합니다. 페이지 크기 설정은 향상 시킬 권장 사항을 만들 수 있는 몇 가지 시나리오가 있습니다. 특별히으로 부적절 한 경우가 아니면 기본값을 사용 하는 것이 좋습니다.

쿼리 결과가 많은 경우 비슷한 쿼리를 동시에 실행 한 제한이 발생할 수 있습니다.  LDAP 서버 쿠키 풀 이라고 하는 전역 메모리 영역 부족 해질 수 있습니다이 발생 합니다.  에 설명 된 대로 풀의 크기를 늘려야 할 수 있습니다 [LDAP 서버 쿠키 처리 방법을](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/manage/how-ldap-server-cookies-are-handled)합니다.

이러한 설정을 하나씩 조정해, 참조 [LDAP 응답에만 5000 값을 반환 하는 Windows Server 2008 이상 도메인 컨트롤러](https://support.microsoft.com/kb/2009267)합니다.

## <a name="determine-whether-to-add-indices"></a>인덱스를 추가할 것인지 결정

특성을 인덱싱하면 필터에서 특성 이름을 가진 개체를 검색할 때 유용 합니다. 인덱싱 필터를 평가할 때 방문 해야 하는 개체의 수를 줄일 수 있습니다. 그러나 해당 특성 수정 하거나 추가 하는 경우 인덱스를 업데이트 해야 하기 때문에 쓰기 작업의 성능을 감소이 합니다. 또한 종종 이점이 저장소 비용이 보다 중요 하지만 디렉터리 데이터베이스의 크기를 늘립니다. 로깅은 비용이 많이 들고 비효율적인 쿼리를 찾는 데 사용할 수 있습니다. 을 식별 한 후에 해당 쿼리에서 검색 성능을 개선 하기 위해 사용 되는 일부 특성을 인덱싱하면 하는 것이 좋습니다. Active Directory 검색의 작동 방식에 대 한 자세한 내용은 참조 하세요. [Active Directory 검색 방법](https://technet.microsoft.com/library/cc755809.aspx)합니다.

### <a name="scenarios-that-benefit-in-adding-indices"></a>인덱스 추가에 활용 하는 시나리오

-   중요 한 CPU 사용량을 생성 하는 데이터를 요청에서 클라이언트 로드 및 클라이언트 쿼리 동작을 변경 하거나 최적화 수입니다. 높은 부하에서 자체 Server Performance Advisor 또는 기본 제공 Active Directory 데이터 수집기 집합의 상위 10 개 문제가 있는 사용자만 목록에 표시 되 고 CPU의 1% 개를 사용 하는 것이 좋습니다.

-   인덱싱되지 않은 특성으로 인해 서버에서 중요 한 디스크 I/O를 생성 하는 클라이언트 로드 및 클라이언트 쿼리 동작을 변경 하거나 최적화 수입니다.

-   쿼리는 시간이 오래 걸리고 있으며 인덱스를 다루는 부족으로 인해 클라이언트에 적절 한 시간 내에 완료 되지 않습니다.

- 소비와 ATQ LDAP 스레드가 소진 된 많은 양의 높은 기간을 사용 하 여 쿼리 유발 합니다. 다음 성능 카운터를 모니터링 합니다.

    - **NTDS\\요청 대기 시간** – 기간에 따라 요청 하는 데 걸리는 프로세스입니다. 그러나 Active Directory 120 초 (기본값) 한 후 요청 시간이 대부분 훨씬 더 빠르게 실행 해야 하 고 매우 장기 실행 쿼리의 전체 숫자에서 숨겨진 가져오기 해야 합니다. 이 기준 보다는 절대 임계값의 변경 내용을 확인 합니다.

        > [!NOTE]
        > 여기에서 높은 값 표시기 다른 도메인과 CRL 검사에 대 한 "프록시" 요청에 지연 될 수도 있습니다.

    - **NTDS\\큐 지연 예상** –이 최적의 성능을 위해 0에 가까우면 가능 해야 합니다.이 요청 시간이 없는 서비스를 기다리는 것을 의미 하는 대로 합니다.

다음 방법 중 하나 이상을 사용 하 여 이러한 시나리오를 검색할 수 있습니다.

-   [통계 컨트롤을 사용 하 여 쿼리 시간 확인](https://msdn.microsoft.com/library/ms808539.aspx)

-   [추적 비용이 많이 들고 비효율적인 검색](https://msdn.microsoft.com/library/ms808539.aspx)

-   성능 모니터에서 active Directory 진단 데이터 수집기 집합 ([SPA 아들: AD 데이터 수집기 집합 Win2008 이상](http://blogs.technet.com/b/askds/archive/2010/06/08/son-of-spa-ad-data-collector-sets-in-win2008-and-beyond.aspx))

-   [Microsoft Server Performance Advisor](../../../server-performance-advisor/microsoft-server-performance-advisor.md) Active Directory Advisor 팩

-   외에도 모든 필터를 사용 하 여 검색 "(objectClass =\*)"를 사용 하는 상위 항목 인덱스입니다.

### <a name="other-index-considerations"></a>다른 인덱스 고려 사항

-   인덱스를 만들기는 문제에 적합 한 솔루션 옵션으로 쿼리를 튜닝을 소진 한 후 확인 합니다. 하드웨어를 올바르게 크기 조정 하는 것이 매우 중요 합니다. 이 인덱스 특성 및 하드웨어 문제를 난독 처리를 시도 하지를 오른쪽 수정 하는 경우에 인덱스를 추가 해야 합니다.

-   인덱스는 인덱싱되는 특성의 전체 크기는 최소 데이터베이스의 크기를 늘립니다. 데이터베이스 증가 예상 특성에는 데이터의 평균 크기를 가져오고 특성이 채워져야 갖게 되는 개체의 수를 곱하여 따라서 평가할 수 있습니다. 일반적으로이 데이터베이스 크기는 1% 증가 합니다. 자세한 내용은 참조 하세요. [데이터 저장소의 작동 방식](https://technet.microsoft.com/library/cc772829.aspx)합니다.

-   검색 동작은 주로 조직 구성 단위 수준에서 수행 됩니다, 경우에 컨테이너 화 된 검색에 대 한 인덱싱 하는 것이 좋습니다.

-   튜플 인덱스는 일반 인덱스 보다 큰 있지만 크기를 추정 하려면 훨씬 더 어렵습니다. 증가 경우 최대 20%를 사용 하 여 밑으로 크기를 추정 하는 일반 인덱스를 사용 합니다. 자세한 내용은 참조 하세요. [데이터 저장소의 작동 방식](https://technet.microsoft.com/library/cc772829.aspx)합니다.

-   검색 동작은 주로 조직 구성 단위 수준에서 수행 됩니다, 경우에 컨테이너 화 된 검색에 대 한 인덱싱 하는 것이 좋습니다.

-   튜플 인덱스 중성 검색 문자열과 최종 검색 문자열을 지 원하는 데 필요 합니다. 초기 검색 문자열에 대 한 튜플 인덱스가 필요 하지 않습니다.

    -   검색 문자열-초기 (samAccountName MYPC =\*)

    -   중성 검색 문자열 (samAccountName =\*MYPC\*)

    -   마지막 검색 문자열-(samAccountName =\*MYPC$)

-   인덱스를 만들면 인덱스를 작성 하는 동안 디스크 I/O를 생성 합니다. 낮은 우선 순위의 백그라운드 스레드에서 이렇게 및 인덱스 작성을 통해 들어오는 요청 우선 적용 됩니다. 환경을 위한 용량 계획 작업이 제대로 완료 되 면이 투명 해야 합니다. 그러나 쓰기 작업이 많은 시나리오 또는 있는 도메인 컨트롤러 저장소의 부하를 알 수 없는 환경 클라이언트 환경이 저하 될 수 있으며 해야 외를 수행 합니다.

-   로컬로 발생 하는 인덱스를 빌드 하므로 복제 트래픽에 영향 최소화 됩니다.

자세한 내용은 다음을 참조 하세요.

-   [보다 효율적인 Microsoft Active Directory 사용 응용 프로그램 만들기](https://msdn.microsoft.com/library/ms808539.aspx)

-   [Active Directory Domain Services에서 검색](https://msdn.microsoft.com/library/aa746427.aspx)

-   [인덱싱된 특성](https://msdn.microsoft.com/library/windows/desktop/ms677112.aspx)

## <a name="see-also"></a>참조

- [Active Directory 서버를 튜닝 하는 성능](index.md)
- [하드웨어 고려 사항](hardware-considerations.md)
- [적절한 도메인 컨트롤러 배치 및 사이트 고려 사항](site-definition-considerations.md)
- [ADDS 성능 문제 해결](troubleshoot.md) 
- [Active Directory 도메인 서비스의 용량 계획](https://go.microsoft.com/fwlink/?LinkId=324566)