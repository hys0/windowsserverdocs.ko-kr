---
title: 의 LDAP 고려 사항은 성능 튜닝을 추가 합니다.
description: Active Directory 워크 로드의 LDAP 고려 사항
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: TimWi; ChrisRob; HerbertM; KenBrumf;  MLeary; ShawnRab
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 5e407f9f32339e3f9c75e3722ad218228b608b9d
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75947106"
---
# <a name="ldap-considerations-in-adds-performance-tuning"></a>의 LDAP 고려 사항은 성능 튜닝을 추가 합니다.

> [!IMPORTANT]
> 다음은 [Active Directory Domain Services의 용량 계획](https://go.microsoft.com/fwlink/?LinkId=324566) 문서에 자세히 설명 된 Active Directory 워크 로드에 대 한 서버 하드웨어 최적화에 대 한 주요 권장 사항 및 고려 사항에 대 한 요약입니다. 독자 들은 이러한 권장 사항에 대 한 보다 기술적 이해와 의미를 위해 [Active Directory Domain Services에 대 한 용량 계획](https://go.microsoft.com/fwlink/?LinkId=324566) 을 검토 하는 것이 좋습니다.

## <a name="verify-ldap-queries"></a>LDAP 쿼리 확인

LDAP 쿼리가 효율적인 쿼리 만들기 권장 사항을 준수 하는지 확인 합니다.

Active Directory에 사용 하기 위해 쿼리를 올바르게 작성, 구조화 및 분석 하는 방법에 대 한 자세한 설명서는 MSDN에 있습니다. 자세한 내용은 [보다 효율적인 Microsoft Active Directory 지원 응용 프로그램 만들기](https://msdn.microsoft.com/library/ms808539.aspx)를 참조 하세요.

## <a name="optimize-ldap-page-sizes"></a>LDAP 페이지 크기 최적화

클라이언트 요청에 대 한 응답으로 여러 개체가 포함 된 결과를 반환 하는 경우 도메인 컨트롤러는 임시로 결과 집합을 메모리에 저장 해야 합니다. 페이지 크기를 높이면 메모리가 더 많이 사용 되 고 불필요 하 게 캐시에서 항목이 손실 될 수 있습니다. 이 경우 기본 설정은 최적입니다. 페이지 크기 설정을 늘리기 위해 권장 사항이 적용 되는 몇 가지 시나리오가 있습니다. 특별히 부적절 한 것으로 식별 되지 않은 경우 기본값을 사용 하는 것이 좋습니다.

쿼리에 결과가 많은 경우 비슷한 쿼리를 동시에 실행할 수 있는 한도를 발견할 수 있습니다.  이는 LDAP 서버에서 쿠키 풀 이라고 하는 전역 메모리 영역을 고갈 시킬 수 있기 때문에 발생 합니다.  [LDAP 서버 쿠키를 처리 하는 방법](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/manage/how-ldap-server-cookies-are-handled)에 설명 된 대로 풀의 크기를 늘려야 할 수도 있습니다.

이러한 설정을 조정 하려면 [Windows Server 2008 이상 도메인 컨트롤러는 LDAP 응답에서 5000 값만 반환](https://support.microsoft.com/kb/2009267)합니다 .를 참조 하세요.

## <a name="determine-whether-to-add-indices"></a>인덱스 추가 여부 결정

인덱싱 특성은 필터에서 특성 이름을 가진 개체를 검색할 때 유용 합니다. 인덱스를 만들면 필터를 평가할 때 방문 해야 하는 개체 수를 줄일 수 있습니다. 그러나 이렇게 하면 해당 특성이 수정 되거나 추가 될 때 인덱스를 업데이트 해야 하기 때문에 쓰기 작업의 성능이 저하 됩니다. 또한 저장소 비용에 비해 이점이 많지만 디렉터리 데이터베이스의 크기도 늘어납니다. 로깅을 사용 하 여 비용이 많이 들고 비효율적인 쿼리를 찾을 수 있습니다. 검색 된 후 검색 성능을 향상 시키기 위해 해당 쿼리에 사용 되는 일부 특성을 인덱싱하는 것이 좋습니다. Active Directory 검색의 작동 방식에 대 한 자세한 내용은 [Active Directory 검색의 작동 방식](https://technet.microsoft.com/library/cc755809.aspx)을 참조 하세요.

### <a name="scenarios-that-benefit-in-adding-indices"></a>인덱스 추가의 이점을 활용 하는 시나리오

-   데이터를 요청 하는 클라이언트 로드가 상당한 CPU 사용량을 생성 하 고 있으며 클라이언트 쿼리 동작을 변경 하거나 최적화할 수 없습니다. 상당한 부하를 사용 하 여 서버 성능 Advisor 또는 기본 제공 Active Directory 데이터 수집기 집합에서 상위 10 개가 아닌 목록에 자신을 표시 하 고 있고 CPU의 1% 이상을 사용 하 고 있다고 가정 합니다.

-   인덱싱되지 않은 특성으로 인해 클라이언트 로드가 서버에서 상당한 디스크 i/o를 생성 하 고 있으며 클라이언트 쿼리 동작을 변경 하거나 최적화할 수 없습니다.

-   쿼리가 시간이 오래 걸리고 포함 인덱스가 부족 하 여 클라이언트에 허용 되는 기간 내에 완료 되지 않습니다.

- 대용량 쿼리를 사용 하면 ATQ LDAP 스레드의 사용량과 소비를 초래 하 게 됩니다. 다음 성능 카운터를 모니터링 합니다.

    - **NTDS\\요청 대기 시간** -요청을 처리 하는 데 걸리는 시간에 따라 결정 됩니다. 120 초 (기본값) 후에 요청 시간이 초과 되는 경우 대부분의 시간이 훨씬 더 빨리 실행 되 고 장기 실행 쿼리는 전체 숫자에서 숨겨집니다. Active Directory 절대 임계값이 아닌이 기준에서 변경 내용을 확인 합니다.

        > [!NOTE]
        > 여기에서 높은 값은 다른 도메인 및 CRL 확인에 대 한 "프록시" 요청의 지연을 확인할 수도 있습니다.

    - **NTDS\\예상 큐 지연** -이는 최적의 성능을 위해 0에 가까운 것이 좋습니다. 즉, 요청이 서비스 대기 시간을 소비 하지 않습니다.

이러한 시나리오는 다음 방법 중 하나 이상을 사용 하 여 검색할 수 있습니다.

-   [통계 컨트롤을 사용 하 여 쿼리 타이밍 결정](https://msdn.microsoft.com/library/ms808539.aspx)

-   [비용이 많이 들고 비효율적인 검색 추적](https://msdn.microsoft.com/library/ms808539.aspx)

-   성능 모니터의 Active Directory 진단 데이터 수집기 집합 ([SPA: AD 데이터 수집기 집합 Win2008 이상](https://blogs.technet.com/b/askds/archive/2010/06/08/son-of-spa-ad-data-collector-sets-in-win2008-and-beyond.aspx))

-   [Microsoft Server Performance Advisor](../../../server-performance-advisor/microsoft-server-performance-advisor.md) Active Directory Advisor 팩

-   상위 인덱스를 사용 하는 "(objectClass =\*)" 외의 필터를 사용 하 여 검색 합니다.

### <a name="other-index-considerations"></a>기타 인덱스 고려 사항

-   쿼리를 튜닝 한 후에는 옵션으로 사용 된 것과 같은 방법으로 인덱스를 만들어야 합니다. 하드웨어를 적절히 크기 조정 하는 것이 매우 중요 합니다. 인덱스는 특성의 인덱스를 지정 하는 것이 적절 한 수정 인 경우에만 추가 해야 하며 하드웨어 문제를 난독 처리 하지는 않습니다.

-   인덱스는 인덱싱된 특성의 최소 총 크기를 기준으로 데이터베이스의 크기를 늘립니다. 따라서 특성에서 데이터의 평균 크기를 계산 하 고 특성을 채울 개체의 수를 곱하여 예상 데이터베이스 증가를 평가할 수 있습니다. 일반적으로 데이터베이스 크기가 1% 증가 합니다. 자세한 내용은 [데이터 저장소의 작동 방식](https://technet.microsoft.com/library/cc772829.aspx)을 참조 하세요.

-   검색 동작이 조직 단위 수준에서 주로 수행 되는 경우 컨테이너 화 된 검색에 대 한 인덱싱을 고려 합니다.

-   튜플 인덱스는 일반 인덱스 보다 크므로 크기를 예측 하는 것이 훨씬 어렵습니다. 최대 20%를 사용 하 여 증가에 대 한 층으로 일반 인덱스 크기를 예상 합니다. 자세한 내용은 [데이터 저장소의 작동 방식](https://technet.microsoft.com/library/cc772829.aspx)을 참조 하세요.

-   검색 동작이 조직 단위 수준에서 주로 수행 되는 경우 컨테이너 화 된 검색에 대 한 인덱싱을 고려 합니다.

-   튜플 인덱스는 중성 검색 문자열과 최종 검색 문자열을 지 원하는 데 필요 합니다. 초기 검색 문자열에는 튜플 인덱스가 필요 하지 않습니다.

    -   초기 검색 문자열 – (samAccountName = MYPC\*)

    -   중성 검색 문자열-(samAccountName =\*MYPC\*)

    -   최종 검색 문자열 – (samAccountName =\*MYPC $)

-   인덱스를 만들면 인덱스를 작성 하는 동안 디스크 i/o가 생성 됩니다. 이 작업은 우선 순위가 낮은 백그라운드 스레드에서 수행 되며, 들어오는 요청은 인덱스 빌드 보다 우선 순위가 지정 됩니다. 환경에 대 한 용량 계획을 올바르게 수행한 경우에는 투명 해야 합니다. 그러나 도메인 컨트롤러 저장소에 대 한 부하를 알 수 없는 쓰기 작업이 많은 시나리오 또는 환경에서는 클라이언트 환경이 저하 될 수 있으므로 시간이 지난 후에 야 합니다.

-   빌드 인덱스는 로컬로 발생 하므로 복제 트래픽에 영향을 최소화 합니다.

자세한 내용은 다음을 참조 하세요.

-   [보다 효율적인 Microsoft Active Directory 지원 응용 프로그램 만들기](https://msdn.microsoft.com/library/ms808539.aspx)

-   [Active Directory Domain Services 검색](https://msdn.microsoft.com/library/aa746427.aspx)

-   [인덱싱된 특성](https://msdn.microsoft.com/library/windows/desktop/ms677112.aspx)

## <a name="see-also"></a>참고 항목

- [성능 튜닝 Active Directory 서버](index.md)
- [하드웨어 고려 사항](hardware-considerations.md)
- [적절한 도메인 컨트롤러 배치 및 사이트 고려 사항](site-definition-considerations.md)
- [ADDS 성능 문제 해결](troubleshoot.md) 
- [Active Directory 도메인 서비스의 용량 계획](https://go.microsoft.com/fwlink/?LinkId=324566)