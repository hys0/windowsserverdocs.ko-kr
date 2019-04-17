---
ms.assetid: 8a3cf2ae-2511-4eea-afd5-a43179a78613
title: "디렉터리 서비스 컴포넌트 업데이트"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ac42591450038240ced273555fb01e66b1ff5546
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="directory-services-component-updates"></a>디렉터리 서비스 컴포넌트 업데이트

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**작성자**: Windows 그룹과 조자룡 Turner, 선임 지원 엔지니어로  
  
> [!NOTE]  
> 이 콘텐츠는 Microsoft 고객 지원 담당자가 작성 하며 경험이 관리자와 technet 항목 일반적으로 제공 하는 것 보다에 대 한 보다 긴밀 기술 설명은 기능 및 Windows Server 2012 r 2에 대 한 해결 방법을 찾는 누가 시스템 개발자를 위한 것입니다. 그러나 받지 않았습니다 동일한 편집 가공 일부 언어 일반적으로 technet 찾을 수 보다 세련 된 적게 보일 수 있도록 합니다.  
  
이 Windows Server 2012 r 2의 디렉터리 서비스 구성 요소 업데이트에 설명 합니다.  
  
## <a name="what-you-will-learn"></a>내용  
다음과 같은 새로운 디렉터리 서비스 구성 요소 업데이트에 설명 합니다.  
  
-   다음과 같은 새로운 디렉터리 서비스 구성 요소 업데이트에 설명 합니다.  
  
    -   [도메인 및 숲 기능 수준](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_FL)  
  
    -   [NTFRS의 사용 중단](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_NTFRS)  
  
    -   [LDAP 쿼리 최적화 변경](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_LDAPQuery)  
  
    -   [1644 이벤트 개선 사항](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_1644)  
  
    -   [Active Directory 복제 처리량 개선](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_ADRepl)  
  
## <a name="BKMK_FL"></a>도메인 및 숲 기능 수준  
  
### <a name="overview"></a>개요  
섹션은 도메인 및 숲 기능 수준 변경에 대 한 간략 한 소개를 제공합니다.  
  
### <a name="new-dfl-and-ffl"></a>새 DFL 및 FFL  
릴리스를 통해 새로운 도메인 및 숲 기능 수준은 다음과 같습니다.  
  
-   숲 기능 수준: Windows Server 2012 r 2  
  
-   Windows Server 2012 R2 도메인 기능 수준:  
  
### <a name="the-windows-server-2012-r2-domain-functional-level-enables-support-for-the-following"></a>Windows Server 2012 R2 도메인 기능 수준을 다음에 대 한 지원을 수 있습니다.  
  
1.  DC 측 보호에 대 한 *사용자 보호*  
  
    *사용자를 보호* 수 Windows Server 2012 R2 도메인에 인증 **더 이상**:  
  
    -   인증 된 NTLM 인증  
  
    -   Kerberos 미리 인증에서 DES 또는 r c 4 암호 그룹을 사용 하 여  
  
    -   무제한 또는 제한 된 위임와 위임  
  
    -   초기 4 시간 수명 이상의 사용자 티켓 (Tgt) 갱신  
  
2.  인증 정책  
  
    어떤 호스트 제어 하기 위해 Windows Server 2012 R2 도메인에 있는 계정에 적용할 수 있는 새 숲 기반 Active Directory 정책을 계정을 수 sign-on에서 및 인증에 대 한 액세스를 제어 조건 계정으로 실행 되는 서비스에 적용  
  
3.  인증 정책 사일로  
  
    새 숲 기반 Active Directory 개체 사용자, 관리 되는 서비스와 계정 인증 격리 또는 인증 정책에 대 한 분류 하는 데 사용할 컴퓨터 계정 간의 관계를 만들 수는 있습니다.  
  
확인에 대 한 자세한 내용은 계정 보호를 구성 하는 방법입니다.  
  
위의 기능 뿐만 아니라 Windows Server 2012 R2 도메인 기능 수준을 도메인에 있는 도메인 컨트롤러 Windows Server 2012 r 2 실행 되도록 보장 합니다.  
Windows Server 2012 r 2 숲 기능 수준 새로운 기능을 제공 하지는 않지만 확인 하 고 숲 속의 만든 새 도메인 Windows Server 2012 R2 도메인 기능 수준에서 자동으로 작동 합니다.  
  
### <a name="minimum-dfl-enforced-on-new-domain-creation"></a>새로운 도메인 만들기에 적용 최소 DFL  
Windows Server 2008 DFL 새로운 도메인 만들기에서 지원 되는 최소 기능 수준입니다.  
  
> [!NOTE]  
> FRS의 사용 중단 서버 관리자와 또는 Windows PowerShell를 통해 Windows Server 2008 보다 낮은 도메인 기능 수준으로 새 도메인을 설치 하는 기능을 제거 하면 됩니다.  
  
### <a name="lowering-the-forest-and-domain-functional-levels"></a>숲 및 도메인 기능 수준 내려  
숲 및 도메인 기능 수준 Windows Server 2012 R2 도메인 및 숲 새로 만들기 새에서 기본적으로 설정 하지만 Windows PowerShell 사용 중일 수 있습니다.  
  
높이 거 나 Windows PowerShell를 사용 하 여 숲 기능 수준 낮추기를 사용 하는 **설정 ADForestMode** cmdlet 합니다.  
  
**Windows Server 2008 모드로 FFL contoso.com 설정 방법:**  
  
```sql  
Set-ADForestMode -ForestMode Windows2008Forest -Identity contoso.com  
```  
  
높이 거 나 Windows PowerShell를 사용 하 여 도메인 기능 수준 낮추기, Set-ADDomainMode cmdlet 사용.  
  
**Windows Server 2008 모드로 contoso.com DFL 설정 방법:**  
  
```powershell  
Set-ADDomainMode -DomainMode Windows2008Domain -Identity contoso.com  
```  
  
Windows Server 2012 r 2 추가 복제본 2003 DFL 실행 기존 도메인 실행 dc 프로 모션 작동 합니다.  
  
기존 숲 속의 새로운 도메인 만들기  
  
![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_FFL.gif)  
  
### <a name="adprep"></a>ADPREP  
이 릴리스에 도메인 작업 없거나 새로 숲 가지가 있습니다.  
  
이러한.ldf 파일에 대 한 스키마 변경 포함 되어 있는 **디바이스 등록 서비스**합니다.  
  
1.  Sch59  
  
2.  Sch61  
  
3.  Sch62  
  
4.  Sch63  
  
5.  Sch64  
  
6.  Sch65  
  
7.  Sch67  
  
**클라우드 폴더 다음과 같습니다.**  
  
1.  Sch66  
  
**MSODS:**  
  
1.  Sch60  
  
**인증 정책과 사일로**  
  
1.  Sch68  
  
2.  Sch69  
  
## <a name="BKMK_NTFRS"></a>NTFRS의 사용 중단  
  
### <a name="overview"></a>개요  
Windows Server 2012 r 2에서 FRS 사용 되지 않습니다.  Windows Server 2008의 최소 도메인 기능 수준을 (DFL)을 적용 하 여 FRS의 사용 중단 수행 됩니다.  이 적용 서버 관리자 또는 Windows PowerShell 사용 하 여 새 도메인을 만든 경우에 표시 됩니다.  
  
사용 하 여-DomainMode 매개 Install-ADDSForest 또는 Install-ADDSDomain cmdlet 도메인 기능 수준을 지정 합니다.  에 오류가 또는 해당 열거형된 문자열 값이이 매개에 대 한 지원 되는 값 될 수 있습니다. 예를 들어, Windows Server 2008 R2을 도메인 모드 수준으로 설정 하려면 4 또는 "Win2008R2" 지정할 수 있습니다.  Windows Server 2008 (3 Win2008)에 대 한 값은 이러한 cmdlet Server 2012 r 2 유효한에서 실행 하는 경우 Windows Server 2008 R2 (Win2008R2 4) (Win2012 5) Windows Server 2012와 Windows Server 2012 r 2 (Win2012R2 6) 합니다. 도메인 기능 수준을 숲 기능 수준 미만 될 수 없지만 높은 될 수 있습니다.  이후 Windows Server 2003 (w i n 2003 2)이 릴리스에서 FRS는 사용 되지 않습니다. Windows Server 2012 r 2에서 실행 될 때 이러한 cmdlet으로 인식 된 매개는 아닙니다.  
  
![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_PS_Install2003DFL.gif)  
  
![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_PS_InstallDFL2.gif)  
  
## <a name="BKMK_LDAPQuery"></a>LDAP 쿼리 최적화 변경  
  
### <a name="overview"></a>개요  
LDAP 쿼리 최적화 알고리즘 다시 평가 것 이며 더 최적화 되었습니다.  LDAP 검색 효율성 및 LDAP 검색 쿼리 복잡 한 시간에 성능 향상 됩니다.  
  
> [!NOTE]  
> **개발자에 게:**ESE 쿼리를 쿼리 검색 LDAP에서 매핑의 향상 된 기능을 통해의 성능 개선 합니다.  LDAP 필터 복잡성 어느 정도 이상 방지 1000 x 이상과 성능이 저하 크게에 최적화 된 인덱스 선택 합니다. 이 변경에이 문제를 피하려면 LDAP 쿼리 인덱스 알게 선택 하는 방법을 변경 합니다.  
  
> [!NOTE]  
> 결과적으로 LDAP 쿼리 최적화 알고리즘의 전체 정비:  
>   
> -   시간을 더 빠르게 검색  
> -   효율성 Dc 더 많은 작업을 허용합니다  
> -   관련 항목 광고 성능 문제 덜 지원 요청  
> -   Windows Server 2008 R2 (KB 2862304) 가져옵니다 돌아가기  
  
### <a name="background"></a>배경  
Active Directory를 검색 하는 기능은 도메인 컨트롤러에서 제공 되는 핵심 서비스입니다.  다른 서비스와 비즈니스 응용 프로그램의 Active Directory 검색 사용합니다.  이 기능을 사용할 수 없는 경우 중단 비즈니스 운영 중단할 수 있습니다.  핵심 및 많이 사용 되는 서비스는 도메인 컨트롤러 LDAP 검색 교통 효율적으로 처리 합니다.  LDAP 쿼리 최적화 알고리즘도 이미 데이터베이스에서 색인 레코드를 통해 충족 될 수 있는 결과 집합으로 LDAP 검색 필터 매핑하여 LDAP 검색 가능한 효율적으로 만들 하려고 합니다.  이 알고리즘 다시 확인 하 고 더 최적화 되었습니다.  LDAP 검색 효율성 및 LDAP 검색 쿼리 복잡 한 시간에 성능 향상 됩니다.  
  
### <a name="details-of-change"></a>변경 세부 정보  
LDAP 검색 포함 되어 있습니다.  
  
-   검색 시작 계층 내 위치 (NC 머리 OU 개체)  
  
-   검색 필터  
  
-   반환 특성의 목록  
  
검색 다음과 같은 요약 될 수 있습니다.  
  
1.  가능 하면 검색 필터 간단 하 게 됩니다.  
  
2.  덮여 집합을 반환 하 인덱스 키 집합을 선택 합니다.  
  
3.  덮여 간단해 인덱스 키 하나 또는 여러 개의 교차로 수행 합니다.  
  
4.  각 레코드 덮여 설정에 대해 보안 뿐만 아니라 필터 식 평가 합니다. 필터가 진정한 액세스 권한을 부여 하는 경우이 레코드 클라이언트를 반환 합니다.  
  
LDAP 쿼리 최적화 작업 2-3 덮여 설정의 크기를 줄이기 위해 단계를 수정 합니다. 특히, 현재 구현 중복 색인 키를 선택 하 고 중복 교차로 수행 합니다.  
  
### <a name="comparison-between-old-and-new-algorithm"></a>이전 버전과 새 알고리즘을 비교  
이 이때에 비효율적 LDAP 검색 대상이 Windows Server 2012 도메인 컨트롤러 합니다.  검색 결과 더 효율적 인덱스를 찾을 수 없게 44 초 정도에 완료 합니다.  
  
```  
adfind -b dc=blue,dc=contoso,dc=com -f "(| (& (|(cn=justintu) (postalcode=80304) (userprincipalname=justintu@blue.contoso.com)) (|(objectclass=person) (cn=justintu)) ) (&(cn=justintu)(objectclass=person)))" -stats >>adfind.txt  
  
Using server: WINSRV-DC1.blue.contoso.com:389  
  
<removed search results>  
  
Statistics  
=====  
Elapsed Time: 44640 (ms)  
Returned 324 entries of 553896 visited - (0.06%)  
  
Used Filter:  
 ( |  ( &  ( |  (cn=justintu)  (postalCode=80304)  (userPrincipalName=justintu@blue.contoso.com) )  ( |  (objectClass=person)  (cn=justintu) ) )  ( &  (cn=justintu)  (objectClass=person) ) )   
  
Used Indices:  
 DNT_index:516615:N  
  
Pages Referenced          : 4619650  
Pages Read From Disk      : 973  
Pages Pre-read From Disk  : 180898  
Pages Dirtied             : 0  
Pages Re-Dirtied          : 0  
Log Records Generated     : 0  
Log Record Bytes Generated: 0  
```  
  
### <a name="sample-results-using-the-new-algorithm"></a>새로운 알고리즘을 사용 하 여 샘플 결과  
이 이때 위의 정확한 동일한 검색 반복 하지만 Windows Server 2012 R2 도메인 컨트롤러를 대상으로 합니다.  동일한 검색 쿼리 LDAP 최적화 알고리즘의 향상 된 기능으로 인해 초 미만이에 완료합니다.  
  
```  
adfind -b dc=blue,dc=contoso,dc=com -f "(| (& (|(cn=justintu) (postalcode=80304) (userprincipalname=dhunt@blue.contoso.com)) (|(objectclass=person) (cn=justintu)) ) (&(cn=justintu)(objectclass=person)))" -stats >>adfindBLUE.txt  
  
Using server: winblueDC1.blue.contoso.com:389  
  
.<removed search results>  
  
Statistics  
=====  
Elapsed Time: 672 (ms)  
Returned 324 entries of 648 visited - (50.00%)  
  
Used Filter:  
 ( |  ( &  ( |  (cn=justintu)  (postalCode=80304)  (userPrincipalName=justintu@blue.contoso.com) )  ( |  (objectClass=person)  (cn=justintu) ) )  ( &  (cn=justintu)  (objectClass=person) ) )   
  
Used Indices:  
 idx_userPrincipalName:648:N  
 idx_postalCode:323:N  
 idx_cn:1:N  
  
Pages Referenced          : 15350  
Pages Read From Disk      : 176  
Pages Pre-read From Disk  : 2  
Pages Dirtied             : 0  
Pages Re-Dirtied          : 0  
Log Records Generated     : 0  
Log Record Bytes Generated: 0  
```  
  
-   트리 최적화 수 없는 경우:  
  
    -   예를 들어: 트리에서 식 인덱싱되지 열을 통해 된  
  
    -   녹화 하 않도록 최적화 인덱스 목록  
  
    -   이벤트 ID 1644 및 ETW 추적을 통해 표시  
  
        ![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_Event1644.gif)  
  
### <a name="BKMK_EnableStats"></a>LDP에 통계 컨트롤을 설정 하려면  
  
1.  LDP.exe 및 열고 연결 도메인 컨트롤러에 연결 합니다.  
  
2.  에 **옵션** 메뉴를 클릭 **컨트롤**합니다.  
  
3.  컨트롤 대화 상자에서의 확장는 **미리 로드** 드롭다운 메뉴를 클릭 **검색 통계** 차례로 클릭 하 고 **확인**합니다.  
  
    ![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_Controls.gif)  
  
4.  에 **찾아보기** 메뉴를 클릭 **검색**  
  
5.  검색 대화 상자에서 선택는 **옵션** 단추.  
  
6.  확인는 **추가** 확인란을 선택한 검색 옵션 대화 상자에서 선택 **확인**합니다.  
  
    ![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_SearchOptions.gif)  
  
### <a name="try-this-use-ldp-to-return-query-statistics"></a>시도해 보기: 사용 쿼리 통계 돌아가려면 LDP  
도메인 가입 클라이언트 또는 AD DS 도구가 설치 되어 있는 서버에서 도메인 컨트롤러 또는 하려면 다음을 수행 합니다.  다음 반복 Windows Server 2012 DC 사용자 및 Windows Server 2012 r 2 DC 사용자를 대상으로 합니다.  
  
1.  리뷰는 ["만들기 더 효율적으로 Microsoft 광고 사용 응용 프로그램"](https://msdn.microsoft.com/library/ms808539.aspx) 문서 하 고 필요에 따라으로 다시 참조 합니다.  
  
2.  검색 통계 LDP을 사용 하 여 사용 (참조 [LDP에 통계 컨트롤을 설정 하려면](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_EnableStats))  
  
3.  여러 LDAP으로 검색 하 고 결과의 맨 통계 정보를 확인 합니다.  또 다른 동일한 검색 반복 하는 활동 때문에 문서화 메모장 텍스트 파일.  
  
4.  LDAP 검색 쿼리 최적화 인덱스 특성으로 인해 최적화 수 있는 수행  
  
5.  완료 하는 데 오랜 시간이 걸리는 검색 구성 하려고 (증가 하 않도록 할 수 있는 **시간 제한** 검색 시간 초과 하지 않는 하므로 옵션).  
  
### <a name="additional-resources"></a>추가 리소스  
[검색 Active Directory 이란 무엇 인가요?](https://technet.microsoft.com/library/cc783845(v=ws.10).aspx)  
  
[Active Directory 작업을 검색 하는 방법](https://technet.microsoft.com/library/cc755809(v=WS.10).aspx)  
  
[보다 효율적 Microsoft Active Directory 사용 응용 프로그램을 만들기](https://msdn.microsoft.com/library/ms808539.aspx)  
  
[951581](https://support.microsoft.com/kb/951581) LDAP 쿼리를 광고에 예상 보다 느리게 실행 또는 LDS/ADAM 디렉터리 서비스 및 이벤트 ID 1644 기록 될 수 있습니다  
  
## <a name="BKMK_1644"></a>1644 이벤트 개선 사항  
  
### <a name="overview"></a>개요  
이 업데이트 문제 해결을 위해 지원 하기 위해 ID 1644 이벤트를 추가 LDAP 검색 결과 통계를 추가 합니다.  또한 시간을 기준으로 임계값 로그온 사용 하도록 설정 하려면 사용할 수 있는 새로운 레지스트리 값이입니다.  이러한 개선 사항을 통해 KB Windows Server 2008 R2 SP1 및 Windows Server 2012에서 사용할 수 있게 되었습니다 [2800945](https://support.microsoft.com/kb/2800945) 는 사용할 수 있게 하려면 Windows Server 2008 SP2 및 합니다.  
  
> [!NOTE]  
> -   이벤트 ID 1644 지원 비효율적 또는 비싼 LDAP 검색 문제를 해결 하기 위해에 추가 LDAP 검색 통계 추가  
> -   (예: 검색 시간 임계값 지정할 수 있습니다. 100ms 보다 더 길게 만들면 촬영 검색에 대 한 로그 이벤트 1644)가 및 Inefficient 검색 결과 임계값 지정 하는 대신  
  
### <a name="background"></a>배경  
Active Directory 성능 문제를 해결 하는 동안 하 게 드러납니다 LDAP 검색 활동 문제를 일으킬 수 있습니다.  도메인 컨트롤러에서 처리 비싼 또는 비효율적 LDAP 쿼리를 볼 수 있도록 로깅 사용 하려는 경우 됩니다.  기록을 활성화를 위해 필드 엔지니어링 진단 값으로 설정 해야 및 비싼 / 비효율적 검색 결과 임계값을 필요에 따라 지정할 수 있습니다.  들판 엔지니어링 로깅 수준 5 값을 활성화 하면,이 조건을 충족 하는 검색 된 이벤트 ID 1644 디렉터리 서비스 이벤트 로그에 기록 됩니다.  
  
이벤트 포함 되어 있습니다.  
  
-   클라이언트 IP와 포트  
  
-   노드 시작  
  
-   필터  
  
-   검색 범위  
  
-   속성 선택  
  
-   서버 컨트롤  
  
-   방문한 항목  
  
-   반환 된 항목  
  
그러나 주요 데이터는 이벤트에서 누락 된 인덱스를 사용한 시간을 사용한 검색 작업 한 내용을 (있는 경우)와 같은 합니다.  
  
#### <a name="additional-search-statistics-added-to-event-1644"></a>추가 검색 통계 1644 이벤트에 추가  
  
-   인덱스를 사용 하는  
  
-   페이지를 참조  
  
-   디스크에서 페이지 읽기  
  
-   디스크에서 preread 페이지  
  
-   수정 새로 페이지  
  
-   수정 부적절 페이지  
  
-   검색 시간  
  
-   최적화 방지 특성  
  
#### <a name="new-time-based-threshold-registry-value-for-event-1644-logging"></a>새 시간 기반 레지스트리 임계값 1644 이벤트 로깅에서 대 한  
여가 고 Inefficient 검색 결과 임계값을 지정 하는 대신 검색 시간 임계값 지정할 수 있습니다.  50 ms 촬영 하는 모든 검색 결과 기록 원하는 나 큰를 사용자 지정 50 소수점 (근거리 엔지니어링 값으로 설정) 이외의 32 hex / 합니다.  
  
```  
Windows Registry Editor Version 5.00  
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters]  
"Search Time Threshold (msecs)"=dword:00000032  
```  
  
#### <a name="comparison-of-the-old-and-new-event-id-1644"></a>이전 버전과 새 이벤트 ID 1644 비교  
이전  
  
![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_Event1644_2012.gif)  
  
새로운  
  
![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_Event1644_2012R2.gif)  
  
#### <a name="try-this-use-the-event-log-to-return-query-statistics"></a>이벤트 로그를 사용 하 여 쿼리 통계 돌아갑니다 시도해 보기:  
  
1.  다음 반복 Windows Server 2012 DC 사용자 및 Windows Server 2012 r 2 DC 사용자를 대상으로 합니다. 각 검색 한 후에 두 개의 Dc 이벤트 ID 1644s 준수 합니다.  
  
2.  시간 기반의 임계값을 사용 하 여 Windows Server 2012 r 2 DC 및 Windows Server 2012 DC에서 이전 방법을 ID 1644 이벤트 로깅에서 regedit 사용.  
  
3.  임계값을 초과 하 고 검색 결과의 맨 통계 정보를 확인 하는 몇 가지 LDAP 검색을 수행 합니다.  이전에 설명 된 LDAP 쿼리를 사용 하 고 같은 검색을 반복 합니다.  
  
4.  LDAP 검색 쿼리 최적화 되지 않을 수 있는 하나 이상의 특성 인덱싱되지은 때문에 최적화 하기 위해을 수행 합니다.  
  
## <a name="BKMK_ADRepl"></a>Active Directory 복제 처리량 개선  
  
### <a name="overview"></a>개요  
광고 복제 RPC 복제 전송에 대 한 사용합니다. 기본적으로 RPC 8k 전송 버퍼가 및 5 K 패킷 크기를 사용합니다. 이렇게 할 경우 보내는 인스턴스는 세 개의 패킷을 (약 15 K 가치 데이터)를 전송 하 고 더 많은 보내기 전에 왕복 이동 네트워크에 대 한 기다려야 다음 합니다. 가정는 3ms 왕복 시간, 가장 높은 처리량 40Mbps 1Gbps 나 10 g b p s 네트워크에도 전 것입니다.  
  
> [!NOTE]  
> -   이 업데이트에 m b 정도 600 p s 40Mbps에서 최대 AD 복제 처리량을 조정합니다.  
>   
>     -   네트워크의 수를 줄일 수 있는 RPC 보내기 버퍼가 크기를 늘리는 왕복  
> -   효과 가장 빠른 속도의 눈에 띄는 됩니다 지연이 네트워크입니다.  
  
이 업데이트 8k에서 256KB RPC 보내기 버퍼가 크기를 변경 하 여 최대 처리량 m b 정도 600 p s 늘립니다.  이 변경을 통해 8k, 이상 증가 하는 TCP 창 크기 왕복 네트워크의 수를 줄일 수 있습니다.  
  
> [!NOTE]  
> 이 문제를 수정 하려면 구성할 수 있는 설정이 있습니다.  
  
### <a name="additional-resources"></a>추가 리소스  
[Active Directory 복제 모델의 작동 방식](https://technet.microsoft.com/library/cc772726(v=WS.10).aspx)  
  


