---
ms.assetid: 3acaa977-ed63-4e38-ac81-229908c47208
title: LDAP 서버 쿠키를 처리하는 방법
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 873953155d22bafef5b042887b22e953ff580b5c
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280575"
---
# <a name="how-ldap-server-cookies-are-handled"></a>LDAP 서버 쿠키를 처리하는 방법

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

LDAP에서는 일부 쿼리가 큰 결과 집합을 생성합니다. 이러한 쿼리는 Windows Server에서 몇 가지 문제를 발생시킵니다.  
  
이러한 큰 결과 집합을 수집하고 빌드하는 작업은 매우 중요합니다. 내부 표현에서 LDAP 연결 표현으로 많은 특성을 변환해야 합니다. 많은 특성에 대해 내부 이진 형식에서 LDAP 응답 프레임의 텍스트 기반 UTF-8 형식으로 변환해야 합니다.  
  
또 다른 문제는 수만 개의 개체가 포함된 결과 집합이 커져서 쉽게 수백 메가바이트가 될 수 있다는 점입니다. 따라서 많은 가상 주소 공간이 필요하게 되고 네트워크를 통해 전송하는 동안 TCP 세션이 중단되면 전체 노력이 손실되는 문제도 발생할 수 있습니다.  
  
이러한 용량 및 로지스틱 문제로 있었는지 Microsoft LDAP 개발자는 "페이징된 쿼리" 라는 LDAP 확장 만들기. 이 확장은 LDAP 컨트롤을 구현하여 매우 큰 쿼리를 더 작은 결과 집합 더 작은 결과 집합의 청크로 구분합니다. 그리고 [RFC 2696](http://www.ietf.org/rfc/rfc2696)과 같은 RFC 표준이 되었습니다.  
  
## <a name="cookie-handling-on-client"></a>클라이언트의 쿠키 처리  
페이징 쿼리 방법 페이지 크기를 통해 또는 클라이언트에서 설정 중 하나를 사용 하는 [LDAP 정책](https://support.microsoft.com/kb/315071/en-us) ("MaxPageSize"). 클라이언트는 항상 LDAP 컨트롤을 보내 페이징을 사용하도록 설정해야 합니다.  

  
결과가 많은 쿼리를 사용하는 경우 특정 지점에서 허용되는 최대 개체 수에 도달합니다. LDAP 서버는 응답 메시지를 패키지하고 나중에 검색을 계속하는 데 필요한 정보를 포함하는 쿠키를 추가합니다.  
  
클라이언트 응용 프로그램은 쿠키를 불투명 blob으로 처리해야 합니다. 응용 프로그램은 응답에서 개체 수를 검색하고 쿠키의 유무에 따라 검색을 계속할 수 있습니다. 클라이언트는 기준 개체 및 필터와 같은 동일한 매개 변수를 사용하여 다시 LDAP 서버로 쿼리를 전송하여 검색을 계속하고 이전 응답에서 반환된 쿠키 값을 포함합니다.  
  
개체 수가 페이지를 채우지 않습니다 LDAP 쿼리가 완료 되 고 응답 없음 페이지 쿠키를 포함 합니다. 서버에서 쿠키가 반환되지 않으면 클라이언트는 페이지된 검색이 완료된 것으로 간주해야 합니다.  
  
서버에서 오류가 반환되면 클라이언트는 페이지된 검색이 실패한 것으로 간주해야 합니다. 검색을 다시 시도하면 검색이 첫 페이지부터 다시 시작됩니다.  
  
## <a name="server-side-cookie-handling"></a>서버 쪽 쿠키 처리  
Windows Server는 클라이언트에 쿠키를 반환하고 경우에 따라 쿠키와 관련된 정보를 서버에 저장합니다. 이 정보는 서버의 캐시에 저장되고 특정 제한이 적용됩니다.  
  
이 경우 서버에서 클라이언트로 보낸 쿠키는 서버가 캐시에서 정보를 조회하는 데도 사용됩니다. 클라이언트에서 페이지된 검색을 계속할 경우 Windows Server는 클라이언트 쿠키는 물론 서버 쿠키 캐시의 관련 정보도 사용하여 검색을 계속합니다. 서버가 어떠한 이유로 인해 서버 캐시에서 관련된 쿠키 정보를 찾을 수 없는 경우 검색이 중단되고 클라이언트로 오류가 반환됩니다.  
  
## <a name="how-the-cookie-pool-is-managed"></a>쿠키 풀의 관리 방법  
LDAP 서버는 한 번에 둘 이상의 클라이언트를 처리하고 한 번에 둘 이상의 클라이언트에서 서버 쿠키 캐시를 사용해야 하는 쿼리를 시작할 수도 있습니다. 따라서 Windows Server 구현에서는 쿠키 풀 사용 추적 및 제한을 적용하여 쿠키 풀에서 너무 많은 리소스를 사용하지 않도록 해야 합니다. 이 제한은 LDAP 정책에서 다음 설정을 사용하여 관리자가 설정할 수 있습니다. 기본값 및 설명은 다음과 같습니다.  
  
**MinResultSets: 4**  
  
서버 쿠키 캐시에 MinResultSets보다 적은 항목이 있을 경우 LDAP 서버에서 아래에 설명된 최대 풀 크기를 확인하지 않습니다.  
  
**MaxResultSetSize: 262,144 바이트**  
  
서버의 총 쿠키 캐시 크기는 MaxResultSetSize(바이트)의 최대값을 초과할 수 없습니다. 초과할 경우 쿠키가 가장 오래된 것부터 시작하여 풀이 MaxResultSetSize 바이트보다 작아지거나 MinResultSets보다 적은 쿠키가 풀에 남을 때까지 삭제됩니다. 즉, 저장된 쿠키가 3개만 있을 경우 LDAP 서버는 기본 설정을 사용하여 450KB의 풀이 정상인 것으로 간주합니다.  
  
**MaxResultSetsPerConn: 10**  
  
LDAP 서버는 풀에서 LDAP 연결당 MaxResultSetsPerConn보다 많은 쿠키를 허용하지 않습니다.  
  
## <a name="handling-deleted-cookies"></a>삭제된 쿠키 처리  
LDAP 서버 캐시에서 쿠키 정보를 제거해도 모든 경우에 응용 프로그램에서 바로 오류가 발생하는 것은 아닙니다. 응용 프로그램이 처음부터 페이지된 검색을 다시 시작하여 다른 시도에서 완료할 수 있습니다. 일부 응용 프로그램은 이러한 종류의 다시 시도 메커니즘을 사용하여 견고성을 추가합니다.  
  
일부 응용 프로그램에서는 페이지 검색을 수행하고 완료하지 못할 수 있습니다. 이런 경우 LDAP 서버 쿠키 캐시에 항목이 남아 섹션 4의 메커니즘을 통해 처리될 수 있습니다. 이 작업은 활성 LDAP 검색을 위해 서버에서 메모리를 확보하는 데 반드시 필요합니다.  
  
서버에서는 이러한 쿠키가 삭제되고 클라이언트에서는 이 쿠키 핸들을 사용하여 검색을 계속하면 어떻게 될까요? LDAP 서버가 서버 쿠키 캐시에서 쿠키를 찾을 수 없으므로 쿼리에 대해 오류를 반환합니다. 오류 응답은 다음과 유사합니다.  
  
```  
00000057: LdapErr: DSID-xxxxxxxx, comment: Error processing control, data 0, v1db1  
```  
  
> [!NOTE]  
> "DSID" 뒤의 16 진수 값은 LDAP 서버 이진 파일의 빌드 버전에 따라 달라 집니다.  
  
## <a name="reporting-on-the-cookie-pool"></a>쿠키 풀에 대한 보고  
LDAP 서버 "16 Ldap 인터페이스" 범주를 통해 이벤트를 로깅할 수에 합니다 [NTDS 진단 키](https://support.microsoft.com/kb/314980/en-us)합니다. 이 범주를 "2"로 설정한 경우에 다음 이벤트를 가져올 수 있습니다.  
  
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
  
이 이벤트는 저장된 쿠키가 제거되었음을 나타냅니다. 클라이언트에 LDAP 오류가 표시되었다는 의미가 아니라 LDAP 서버가 캐시에 대한 관리 제한에 도달했음을 의미합니다.  경우에 따라 LDAP 클라이언트가 페이지된 검색을 중단해도 오류가 표시되지 않을 수 있습니다.  
  
## <a name="monitoring-the-cookie-pool"></a>쿠키 풀 모니터링  
도메인에서 LDAP 검색 오류가 발생하지 않은 경우 LDAP 서버 페이지 검색 쿠키 풀을 모니터링할 필요가 없습니다. 사용자 환경에 LDAP 페이지 검색 관련 오류가 표시되면 쿠키 풀 관리자 제한에 문제가 있을 수 있습니다.  
  
이벤트 2898 및 2899는 LDAP 서버가 관리자 제한에 도달했음을 알 수 있는 유일한 방법입니다. 위의 오류 처리 제어로 인해 LDAP 쿼리 오류가 발생하는 경우 이벤트에 따라 섹션 4에서 설명한 LDAP 정책 설정 중 하나 이상에서 제한을 늘려야 합니다.  
  
DC/LDAP 서버에 2898 이벤트가 표시되는 경우 MaxResultSetsPerConn을 25로 설정하는 것이 좋습니다. 단일 LDAP 연결에서 25개 이상의 병렬 페이지된 검색은 일반적이지 않습니다. 2898 이벤트가 계속 표시되는 경우 오류가 발생하는 LDAP 클라이언트 응용 프로그램을 조사하는 것이 좋습니다. 어떻게 하든 추가 페이지된 결과를 검색하려고 한다고 의심되면 쿠키를 보류 중 상태로 유지하고 새 쿼리를 다시 시작합니다. 따라서 특정 지점에서 해당 용도에 충분한 쿠키가 응용 프로그램에 있는지 확인하려면 MaxResultSetsPerConn 값을 25 이상으로 늘릴 수도 있습니다. 도메인 컨트롤러에 이벤트 2899가 기록된 것을 확인하면 계획은 달라집니다. 메모리가 충분한(몇 GB의 사용 가능한 메모리) 컴퓨터에서 DC/LDAP 서버가 실행되는 경우에는 LDAP 서버에서 MaxResultsetSize를 >=250MB로 설정하는 것이 좋습니다. 이 제한은 매우 큰 디렉터리에 많은 양의 LDAP 페이지 검색을 수용할 만큼 충분히 큽니다.  
  
250MB 이상의 풀에서도 이벤트 2899가 계속 표시되면 많은 클라이언트에서 매우 자주 쿼리되어 매우 많은 개체가 반환되는 것일 수 있습니다. [Active Directory 데이터 수집기 집합](http://blogs.technet.com/b/askds/archive/2010/06/08/son-of-spa-ad-data-collector-sets-in-win2008-and-beyond.aspx) 을 사용하여 수집할 수 있는 데이터를 사용하면 LDAP 서버를 사용 중 상태로 유지하는 반복적인 페이징된 쿼리를 찾을 수 있습니다. 이러한 쿼리 모두 사용 하는 페이지의 크기와 일치 하는 "항목이 반환" 수로 표시 됩니다.  
  
가능한 경우 응용 프로그램 디자인을 검토 하 고 더 낮은 빈도, 데이터 볼륨 및/또는 더 적은 클라이언트 인스턴스로이 데이터를 쿼리 하는 다른 방법을 구현 해야 합니다. 이 가이드를 소스 코드 액세스 권한이 있는 응용 프로그램의 경우 [효율적인 AD-Enabled 응용 프로그램을 만드는](https://msdn.microsoft.com/library/ms808539.aspx) 액세스 AD 응용 프로그램에 대 한 최적의 방법을 이해할 수 있습니다.  
  
쿼리 동작을 변경할 수 없는 경우 한 가지 방법은 필요한 명명 컨텍스트의 및 클라이언트를 재배포 하 고 최종적으로 개별 LDAP 서버에 부하를 줄이거나에 복제 된 인스턴스를 더 추가 됩니다.  
  


