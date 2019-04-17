---
ms.assetid: 3acaa977-ed63-4e38-ac81-229908c47208
title: "LDAP 서버 쿠키를 처리 하는 방법"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 89369cb1e52a315520062ca5ecc96b66ac3e2bfc
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="how-ldap-server-cookies-are-handled"></a>LDAP 서버 쿠키를 처리 하는 방법

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

LDAP, 일부 쿼리 결과 큰 결과에 설정합니다. 이러한 쿼리 Windows Server에 몇 가지 문제가 발생할 합니다.  
  
수집 하 고 큰 결과 집합 이러한 빌드는 많은 작업입니다. 대부분의 특성 내부 표시 LDAP 와이어 표현 변환할 수 해야 합니다. 많은 특성 LDAP 응답 프레임에는 텍스트 기반 F-8 형식으로 발생 하는 내부, 자주 이진 형식으로 변환 해야 합니다.  
  
다른 문제 결과 개체 크게 될 쉽게 여러 백 메가 바이트 수십만으로 설정 하는 것입니다. 가상 이러한 다음 필요 많은 주소 공간을도 전송 네트워크를 통해 몇 가지 문제가으로 전송 되에서는 TCP 세션 세분화 전체 노력 손실 됩니다.  
  
이러한 용량과 물류 문제 있는 "페이지 쿼리"로 알려진 LDAP 확장 만들기 Microsoft LDAP 개발자 일으키는 합니다. LDAP 컨트롤 개의 거 대 한 쿼리가 조각 작은 결과 집합으로 분리 하 구현 하는 것입니다. 로 RFC 표준 되었기 때문에 [RFC 2696](http://www.ietf.org/rfc/rfc2696)합니다.  
  
## <a name="cookie-handling-on-client"></a>쿠키 클라이언트에서 처리  
페이지 쿼리 방법은 사용 페이지 크기 클라이언트가 또는 설정 중 하나는 [LDAP 정책](https://support.microsoft.com/kb/315071/en-us) ("MaxPageSize"). 페이징 LDAP 컨트롤을 전송 하 여 사용 하는 클라이언트 항상 필요 합니다.  

  
많은 결과를 쿼리에서 작업 하는 경우을 준비해 줍니다 허용 개체 최대에 도달 하면 됩니다. LDAP 서버가 응답 메시지를 패키지를 나중에 검색을 계속 하는 데 필요한 정보를 포함 하는 쿠키를 추가 합니다.  
  
클라이언트 응용 프로그램 불투명 물방울으로 쿠키를 처리 해야 합니다. 응답에 개체 수를 검색할 수 하 고 쿠키 있는지 여부에 따라 검색 계속할 수 있습니다. 클라이언트 쿼리 기본 개체, 필터를 등 동일한 매개 변수를 사용 하 여 다시 LDAP 서버에 전송 하 여 검색을 계속 하 고 이전 응답에서 반환 된 쿠키 값이 포함 됩니다.  
  
개체 수가 페이지 채우기 하지 않는 경우 LDAP 쿼리 완료 되 고 응답 하지 페이지 쿠키를 포함 합니다. 쿠키가 없는 서버에서 반환 되 면 클라이언트 성공적으로 완료 되기를 페이지 된 검색을 고려해 야 합니다.  
  
오류가 발생 서버에서 반환 되 면 클라이언트 성공 하려면 페이지 된 검색을 고려해 야 합니다. 검색 다시 시도 하는 첫 번째 페이지에서 검색을 다시 시작 발생 합니다.  
  
## <a name="server-side-cookie-handling"></a>서버 쪽 쿠키 처리  
Windows Server 쿠키 클라이언트 돌아와 때때로 서버에서 쿠키와 관련 된 정보를 저장 합니다. 이 정보 캐시에서 서버에 저장 하 고 특정 제한 될 수 있습니다.  
  
이 경우 클라이언트는 서버 전송 하는 쿠키는 또한 서버에서 서버의 캐시의 정보를 찾을 합니다. 클라이언트 계속 페이지 된 검색을 하는 경우 Windows Server 사용 합니다 클라이언트 쿠키 뿐만 아니라 모든 관련된 정보 server 쿠키 캐시에서 검색을 계속 하. 서버 어떤 이유로 인해 서버 캐시의 쿠키 관련된 정보를 찾을 수 없으면 검색 중단 되 고 오류 클라이언트를 반환 됩니다.  
  
## <a name="how-the-cookie-pool-is-managed"></a>쿠키 풀의 관리 되는 방법  
물론,을 LDAP 서버는 한 번에 여러 개 클라이언트를 제공 하 고 한 번에 여러 명의 클라이언트는 서버 쿠키 캐시를 사용 해야 하는 쿼리 시작할 수 있습니다. 따라서 Windows Server 구현 있는 쿠키 풀 사용량을 추적 이며 쿠키 풀이 너무 많이 리소스를 받지 않고 하도록 제한을 제자리에 저장 합니다. 제한은 LDAP 정책의 다음 설정을 사용 하 여 관리자가 설정할 수 있습니다. 기본 설정 및 설명을 다음과 같습니다.  
  
**MinResultSets: 4**  
  
LDAP 서버 서버 쿠키 캐시의 MinResultSets 항목이 보다 작은 경우 하지 아래에 대해 수시로 이야기 최대 풀 크기로 보입니다.  
  
**262144 바이트 MaxResultSetSize:**  
  
총 쿠키 캐시 크기 서버에 바이트에서 MaxResultSetSize 최대를 넘지 해야 합니다. 그렇지 않으면 풀 MaxResultSetSize 바이트 보다 작은 풀 있는 MinResultSets 쿠키 보다 작음 때까지에서 가장 오래 된 시작 쿠키 삭제 됩니다. 이 되었음을 의미 하며 기본 설정을 사용 하 고 LDAP 서버 풀을 확인 하는 3 쿠키를 저장 하는 경우 450 KB 합니다.  
  
**MaxResultSetsPerConn: 10**  
  
풀에서 LDAP 연결 당 MaxResultSetsPerConn 쿠키 뿐인 LDAP 서버 수 있게합니다.  
  
## <a name="handling-deleted-cookies"></a>처리 쿠키를 삭제  
LDAP Server 캐시에서 쿠키 정보 제거 항상에서 응용 프로그램에 대 한 즉각적인 오류가 발생 하지 않습니다. 응용 프로그램 페이징된 검색 처음부터 다시 시작 및 다른 시도에 완료 될 수 있습니다. 일부 응용 프로그램 이러한 종류의 안정성을 추가 하려면 재시도 메커니즘 했습니다.  
  
일부 응용 프로그램 페이지 검색을 통해 이동한 완료 하지 못하는 될 수 있습니다. 이 유지 LDAP 서버에서 항목 섹션 4 메커니즘을 통해 처리 하는 쿠키 캐시 합니다. 메모리 활성 LDAP 검색에 대 한 서버에서 확보 필수입니다.  
  
서버에서 쿠키를 삭제 되 고 클라이언트 계속이 쿠키 핸들을 사용 하 여 검색 하면 어떻게 되나요? LDAP 서버는 하지 쿠키 캐시 서버에서 쿠키를 찾을 쿼리에 대 한 오류를 반환, 오류 응답 유사한 됩니다.  
  
```  
00000057: LdapErr: DSID-xxxxxxxx, comment: Error processing control, data 0, v1db1  
```  
  
> [!NOTE]  
> "DSID" 뒤 16 진 값 LDAP 서버 바이너리의 빌드 버전에 따라 달라 집니다.  
  
## <a name="reporting-on-the-cookie-pool"></a>쿠키 풀에서 보고  
LDAP 서버 "16 Ldap 인터페이스" 범주를 통해 이벤트를 기록 하는 기능에는 [NTDS 진단 키](https://support.microsoft.com/kb/314980/en-us)합니다. 이 범주 "2"를 설정한 경우 다음과 같은 이벤트를 볼 수 있습니다.  
  
```  
Log Name:      Directory Service  
Source:        Microsoft-Windows-ActiveDirectory_DomainService  
Event ID:      2898  
Task Category: LDAP Interface  
Level:         Information  
Description:  
Internal event: The LDAP server has reached the limit of the number of Result Sets it will maintain for a single connection.  A stored Result Set will be discarded.  This will result in a client being unable to continue a paged LDAP search.  
Maximum number of Result Sets allowed per LDAP connection:  
10  
Current number of Result Sets for this LDAP connection:  
11  
  
User Action  
The client should consider a more efficient search filter.  The limit for Maximum Result Sets per Connection may also be increased.  
  
```  
  
```  
Log Name:      Directory Service  
Source:        Microsoft-Windows-ActiveDirectory_DomainService  
Event ID:      2899  
Task Category: LDAP Interface  
Level:         Information  
Description:  
Internal event: The LDAP server has exceeded the limit of the LDAP Maximum Result Set Size. A stored Result Set will be discarded.  This will result in a client being unable to continue a paged LDAP search.   
  
Number of result sets currently stored:   
4   
Current Result Set Size:   
263504   
Maximum Result Set Size:   
262144   
Size of single Result Set being discarded:   
40876   
User Action   
The client should consider a more efficient search filter.  The limit for Maximum Result Set Size may also be increased.  
  
```  
  
이벤트 신호 저장 된 쿠키를 삭제 되었습니다. 클라이언트가 본 LDAP 오류만 LDAP 서버에 대 한 캐시 관리 제한에 도달 했습니다 의미 하지 않습니다.  경우에 따라 LDAP 클라이언트 페이징된 검색 버려진 있을 수 있습니다 및 오류를 표시 하지 될 수 있습니다.  
  
## <a name="monitoring-the-cookie-pool"></a>쿠키 풀을 모니터링합니다.  
절대 LDAP 검색 오류가 도메인에 발생 하면 수 LDAP 서버 페이지 검색 쿠키 풀 모니터링 필요가 없습니다. 귀하의 환경에 관련된 오류 검색 LDAP 페이지가 표시 되 면 경우 쿠키 풀 관리자가 첨자 문제가 있을 수 있습니다.  
  
이벤트 2898 및 2899 LDAP 서버 관리자 제한에 도달 했습니다 알만 가지가 있습니다. 아웃 LDAP 쿼리 오류를 제어 위의 오류 처리으로 인해 발생 하면 증가 제한 되는 이벤트에 따라 4 섹션에 언급 LDAP 정책 설정 중 하나 이상을 확인 해야 합니다.  
  
DC/LDAP 서버에 2898 이벤트를 표시 하는 경우 MaxResultSetsPerConn 25로 설정 하는 것이 좋습니다. 하나의 LDAP 연결에 대 한 25 개 이상의 병렬 페이징된 검색 별로있지 않습니다. 2898 이벤트를 계속 조사 하 고 오류가 발생 하는 LDAP 클라이언트 응용 프로그램 하는 것이 좋습니다. 더욱 커졌습니다 추가 페이지 된 결과 가져오는 멈추는, 보류 중인 쿠키 잎를 새 쿼리를 다시 시작 되는 생각 것입니다. 지금 확인 여부 응용 프로그램은을 준비해 줍니다 충분 한 쿠키는 목적을 위해 이벤트 2899 도메인 컨트롤러에 기록에 표시 되 면 MaxResultSetsPerConn 25. 초과 값 늘릴 수도 있습니다, 요금제는 다를 수 있습니다. DC/LDAP 서버 충분 한 메모리 (사용 가능한 메모리가 여러 기가바이트) 사용 하는 컴퓨터에서 실행 하는 경우는 MaxResultsetSize LDAP 서버를 설정 하는 것이 좋습니다 > 250MB = 합니다. 이 제한은 LDAP 페이지 검색 매우 큰 디렉터리에 더 많은 양의 맞게입니다.  
  
풀 250MB 이상의 사용 2899 이벤트 되는 많은 클라이언트 반환 개체 매우 높음 수 있는 표시 여전히 인 경우 매우 빈번한 방식으로 묻습니다. 데이터를 수집할 수 있는 [Active Directory 데이터 수집기 설정](http://blogs.technet.com/b/askds/archive/2010/06/08/son-of-spa-ad-data-collector-sets-in-win2008-and-beyond.aspx) 도움말 LDAP 서버를 유지 하는 반복 페이징된 쿼리를 찾을 수 없음 합니다. 이러한 쿼리 모두 사용 하는 페이지의 크기와 일치 하는 여러 가지 "항목 반환"으로 표시 됩니다.  
  
가능 하면 응용 프로그램 디자인을 검토 하 고 낮은 주파수, 데이터 볼륨 및/또는 적은 클라이언트 인스턴스가이 데이터를 쿼리 다른 접근 방식을 구현 해야 합니다. 이 가이드로 시작 소스 코드 액세스 열어야 응용 프로그램의 경우 [효율적인 AD-Enabled 응용 프로그램을 만드는](https://msdn.microsoft.com/en-us/library/ms808539.aspx) 최적의 액세스 광고에 응용 프로그램에 대 한 방법으로 이해 하는 데 도움이 될 수 있습니다.  
  
쿼리 동작을 변경할 수 없는 경우 방법 중 하나는 더 복제 인스턴스 필요한 명명 컨텍스트를 클라이언트 재배포할 및 결국 개별 LDAP 서버의 로드 줄이기 추가 합니다.  
  


