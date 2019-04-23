---
ms.assetid: 8a3cf2ae-2511-4eea-afd5-a43179a78613
title: 디렉터리 서비스 구성 요소 업데이트
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f3e0553b1919a7f9129d47616d0ffb66b6ff48f8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874444"
---
# <a name="directory-services-component-updates"></a>디렉터리 서비스 구성 요소 업데이트

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**작성자**: Windows 그룹과 Justin Turner, 수석 지원 에스컬레이션 엔지니어  
  
> [!NOTE]  
> 이 콘텐츠는 Microsoft 고객 지원 엔지니어에 의해 작성되었으며 Windows Server 2012 R2의 기능 및 솔루션에 대해 TechNet에서 일반적으로 제공하는 항목보다 더 자세한 기술적 설명을 찾고 있는 숙련된 관리자 및 시스템 설계자를 대상으로 합니다. 그러나 동일한 편집 과정을 수행하지 않았으므로 일부 언어는 일반적으로 TechNet에서 찾을 수 있는 것보다 완벽하지 않을 수 있습니다.  
  
이 단원에서는 Windows Server 2012 R2에서 디렉터리 서비스 구성 요소 업데이트를 설명합니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
다음 새 디렉터리 서비스 구성 요소 업데이트를 설명 합니다.  
  
-   다음 새 디렉터리 서비스 구성 요소 업데이트를 설명 합니다.  
  
    -   [도메인 및 포리스트 기능 수준](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_FL)  
  
    -   [NTFRS의 사용 중단](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_NTFRS)  
  
    -   [LDAP 쿼리 최적화 프로그램 변경 사항](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_LDAPQuery)  
  
    -   [1644 이벤트 개선 사항](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_1644)  
  
    -   [Active Directory 복제 처리량 개선 사항](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_ADRepl)  
  
## <a name="BKMK_FL"></a>도메인 및 포리스트 기능 수준  
  
### <a name="overview"></a>개요  
섹션에는 도메인 및 포리스트 기능 수준 변경에 대 한 간략 한 소개를 제공합니다.  
  
### <a name="new-dfl-and-ffl"></a>새 DFL 및 FFL  
릴리스에서 새 도메인 및 포리스트 기능 수준이 있습니다.  
  
-   포리스트 기능 수준: Windows Server 2012 R2  
  
-   도메인 기능 수준: Windows Server 2012 R2  
  
### <a name="the-windows-server-2012-r2-domain-functional-level-enables-support-for-the-following"></a>다음을 지원할 수 있도록 하는 Windows Server 2012 R2 도메인 기능 수준:  
  
1.  에 대 한 DC 쪽 보호 *보호 된 사용자*  
  
    *사용자를 보호* Windows Server 2012 R2 도메인에 인증할 수 없습니다 **이상**:  
  
    -   NTLM 인증을 사용 하 여 인증  
  
    -   Kerberos 사전 인증에서 DES 또는 RC4 암호 그룹 사용  
  
    -   무제한 또는 제한 된 위임을 사용한 위임  
  
    -   초기 4 시간 수명을 넘도록 사용자 티켓 (Tgt) 갱신  
  
2.  Authentication Policies  
  
    Windows Server 2012 R2 호스트를 제어 하는 도메인의 계정에 적용했습니다 수 있는 새 포리스트 기반 Active Directory 정책 수에서 sign-on 계정과 계정으로 실행 되는 서비스 인증에 대 한 액세스 제어 조건을 적용합니다  
  
3.  Authentication Policy Silos  
  
    새 포리스트 기반 Active Directory 개체 계정 인증 격리 또는 인증 정책에 대 한 분류 하는 데 사용할 사용자, 관리 되는 서비스 및 컴퓨터 계정 간의 관계를 만들 수 있습니다.  
  
참조 하는 방법에 대 한 자세한 내용은 보호 된 계정을 구성 합니다.  
  
위의 기능 외에도 Windows Server 2012 R2 도메인 기능 수준을 Windows Server 2012 R2 도메인의 모든 도메인 컨트롤러에 실행 되는지 확인 합니다.  
Windows Server 2012 R2 포리스트 기능 수준을 새로운 모든 기능을 제공 하지는 않지만 포리스트에서 만들어진 새 도메인이 Windows Server 2012 R2 도메인 기능 수준에서 자동으로 작동 되도록 합니다.  
  
### <a name="minimum-dfl-enforced-on-new-domain-creation"></a>새 도메인 만들기에 적용 되는 최소 DFL  
Windows Server 2008 DFL에는 새 도메인 만들기에서 지원 되는 최소 기능 수준입니다.  
  
> [!NOTE]  
> 사용 중단의 FRS 도메인 기능 수준이 Windows Server 2008 서버 관리자 또는 Windows PowerShell을 통해 보다 낮은 사용 하 여 새 도메인을 설치 하는 기능을 제거 하 여 수행 됩니다.  
  
### <a name="lowering-the-forest-and-domain-functional-levels"></a>포리스트 및 도메인 기능 수준을 낮추고  
포리스트 및 도메인 기능 수준은 새로운 도메인 및 새 포리스트 생성 시 기본적으로 Windows Server 2012 R2로 설정 되지만 Windows PowerShell을 사용 하 여 낮출 수 있습니다.  
  
Windows PowerShell을 사용 하 여 포리스트 기능 수준을 올리거나 설정, 사용 된 **Set-adforestmode** cmdlet.  
  
**Windows Server 2008 모드에 contoso.com FFL 설정:**  
  
```sql  
Set-ADForestMode -ForestMode Windows2008Forest -Identity contoso.com  
```  
  
Windows PowerShell을 사용 하 여 도메인 기능 수준을 올리거나 설정, Set-addomainmode cmdlet을 사용 합니다.  
  
**설정 하려면 contoso.com dfl로 Windows Server 2008 모드:**  
  
```powershell  
Set-ADDomainMode -DomainMode Windows2008Domain -Identity contoso.com  
```  
  
2003 DFL을 실행 하는 기존 도메인에 복제본을 추가할로 Windows Server 2012 R2를 실행 하는 DC의 수준 올리기 작동 합니다.  
  
기존 포리스트에 새 도메인 만들기  
  
![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_FFL.gif)  
  
### <a name="adprep"></a>ADPREP  
이 릴리스에서 도메인 작업 없거나 새 포리스트에 있습니다.  
  
이러한.ldf 파일에 대 한 스키마 변경 내용에 포함 된 **Device Registration Service**합니다.  
  
1.  Sch59  
  
2.  Sch61  
  
3.  Sch62  
  
4.  Sch63  
  
5.  Sch64  
  
6.  Sch65  
  
7.  Sch67  
  
**작업 폴더:**  
  
1.  Sch66  
  
**MSODS:**  
  
1.  Sch60  
  
**인증 정책 및 사일로**  
  
1.  Sch68  
  
2.  Sch69  
  
## <a name="BKMK_NTFRS"></a>NTFRS의 사용 중단  
  
### <a name="overview"></a>개요  
Windows Server 2012 R2의 FRS는 사용 하는 사용 되지 않습니다.  FRS 사용 중단은 Windows Server 2008의 최소 도메인 기능 수준 (DFL)를 적용 하 여 수행 됩니다.  이 적용은 서버 관리자 또는 Windows PowerShell을 사용 하 여 새 도메인은 생성 하는 경우에 제공 합니다.  
  
Install-addsforest 또는 Install-addsdomain cmdlet을 사용 하 여 도메인 기능 수준을 지정 하려면-DomainMode 매개 변수를 사용 합니다.  이 매개 변수에 대해 지원 되는 값은 해당 열거형된 문자열 값 또는 유효한 정수를 수 있습니다. 예를 들어, Windows Server 2008 R2 도메인 모드 수준 설정, "Win2008R2" 또는 4의 값을 지정할 수 있습니다.  값은 Windows Server 2008 (3, Win2008)에 대 한 유효한 Server 2012 R2에서 이러한 cmdlet을 실행 하는 경우 Windows Server 2008 R2 (4, Win2008R2) Windows Server 2012 (5, Win2012) 및 Windows Server 2012 R2 (Win2012R2 6). 도메인 기능 수준은 포리스트 기능 수준보다 낮은 값으로 설정할 수 없으며, 포리스트 기능 수준보다 높은 값으로 설정할 수는 있습니다.  이 릴리스에서 Windows Server 2003 (2, Win2003) FRS는 사용 되지 않습니다. 이후 Windows Server 2012 R2에서 실행 하는 경우 이러한 cmdlet 사용 하 여 인식할 수 있는 매개 변수가 아닙니다.  
  
![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_PS_Install2003DFL.gif)  
  
![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_PS_InstallDFL2.gif)  
  
## <a name="BKMK_LDAPQuery"></a>LDAP 쿼리 최적화 프로그램 변경 사항  
  
### <a name="overview"></a>개요  
LDAP 쿼리 최적화 프로그램은 알고리즘을 다시 평가 되어 더욱 최적화 합니다.  LDAP 검색 효율성 및 복잡 한 쿼리의 LDAP 검색 시간 성능이 향상 됩니다.  
  
> [!NOTE]  
> **개발자에서:** LDAP의 매핑의 향상 된 기능을 통해 검색의 성능이 향상 된 ESE 쿼리를 쿼리 합니다.  특정 수준의 복잡성을 넘어 LDAP 필터 선택을 최적화 된 인덱스 (1000 x 이상) 성능이 크게 저하 결과 방지 합니다. 이 문제를 방지 하려면 LDAP 쿼리에 대 한 인덱스를 선택 하는 방법을 변경 하는이 변경 합니다.  
  
> [!NOTE]  
> 결과적으로 LDAP 쿼리 최적화 프로그램은 알고리즘의 전체 정비:  
>   
> -   검색 시간 단축  
> -   많은 작업을 수행 하는 Dc를 허용 하는 효율성 향상  
> -   지원 호출 덜 AD 성능 관련 문제  
> -   Windows Server 2008 R2 (KB 2862304)로 가져올 백업  
  
### <a name="background"></a>배경  
Active Directory를 검색할 수는 도메인 컨트롤러에서 제공 하는 핵심 서비스입니다.  다른 서비스 및 기간 업무 응용 프로그램에는 Active Directory 검색에 사용합니다.  이 기능을 사용할 수 없는 경우 업무 중단 사라질 수 있습니다.  코어 및 많이 사용 되는 서비스로, 반드시 도메인 컨트롤러 LDAP 검색 트래픽을 효율적으로 처리 합니다.  LDAP 쿼리 최적화 프로그램은 알고리즘 이미 데이터베이스에 인덱스 레코드를 통해 충족 될 수 있는 결과 집합으로 LDAP 검색 필터를 매핑하여 LDAP 검색을 최대한 효율적으로 확인 하려고 합니다.  이 알고리즘 다시 평가 되어 더욱 최적화 합니다.  LDAP 검색 효율성 및 복잡 한 쿼리의 LDAP 검색 시간 성능이 향상 됩니다.  
  
### <a name="details-of-change"></a>변경의 세부 정보  
LDAP 검색에는 다음이 포함 됩니다.  
  
-   검색을 시작할 계층 구조 내의 위치 (NC 헤드에서 OU 개체)  
  
-   검색 필터  
  
-   반환할 특성의 목록  
  
검색 프로세스는 다음과 같이 요약할 수 있습니다.  
  
1.  가능한 경우 검색 필터를 간소화 합니다.  
  
2.  대상된 집합을 반환 하는 인덱스 키 집합을 선택 합니다.  
  
3.  대상된 집합을 줄이기 위해 인덱스 키의 하나 이상의 교차점을 수행 합니다.  
  
4.  대상된 집합의 각 레코드에 대 한 필터 식 뿐만 아니라 보안을 평가 합니다. 필터가 TRUE로 평가 될 액세스 권한을 부여 하 고 클라이언트에이 레코드를 반환 합니다.  
  
LDAP 쿼리 최적화 작업은 대상된 집합의 크기를 줄이기 위해 2-3 단계를 수정 합니다. 보다 구체적으로, 현재 구현에서는 중복 인덱스 키를 선택 하 고 중복 교차를 수행 합니다.  
  
### <a name="comparison-between-old-and-new-algorithm"></a>이전 및 새 알고리즘 비교  
이 예제에서 비효율적인 LDAP 검색 대상이 Windows Server 2012 도메인 컨트롤러입니다.  검색 결과로 더 효율적인 인덱스를 찾을 수 없게 약 44 초 이내에 완료 합니다.  
  
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
  
### <a name="sample-results-using-the-new-algorithm"></a>새 알고리즘을 사용 하 여 예제 결과  
이 예제에서는 위와 정확히 동일한 검색을 반복 하지만 Windows Server 2012 R2 도메인 컨트롤러를 대상으로 합니다.  동일한 검색 LDAP 쿼리 최적화 프로그램은 알고리즘의 향상 된 기능으로 인해 초 내에 완료 됩니다.  
  
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
  
-   트리를 최적화할 수 없는 경우:  
  
    -   예를 들어: 트리에서 식을 인덱싱되지 않은 열을 통해  
  
    -   목록을 최적화를 방지 하는 인덱스를 기록 합니다.  
  
    -   ETW 추적 및 이벤트 ID 1644를 통해 노출  
  
        ![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_Event1644.gif)  
  
### <a name="BKMK_EnableStats"></a>LDP에서 통계 컨트롤을 사용 하도록 설정 하려면  
  
1.  LDP.exe를 열고 및 연결 하 고 도메인 컨트롤러에 바인딩하십시오.  
  
2.  에 **옵션** 메뉴에서 클릭 **컨트롤**합니다.  
  
3.  컨트롤 대화 상자를 확장 합니다 **미리 정의 된 부하** 풀 다운 메뉴에서 클릭 **검색 통계** 클릭 하 고 **확인**합니다.  
  
    ![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_Controls.gif)  
  
4.  에 **찾아보기** 메뉴에서 클릭 **검색**  
  
5.  검색 대화 상자를 선택 합니다 **옵션** 단추입니다.  
  
6.  확인 합니다 **Extended** 선택한 검색 옵션 대화 상자에서 확인란을 선택 **확인**합니다.  
  
    ![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_SearchOptions.gif)  
  
### <a name="try-this-use-ldp-to-return-query-statistics"></a>다음과 같이 해보십시오. LDP를 사용 하 여 쿼리 통계를 반환 합니다.  
도메인 컨트롤러 또는 도메인에 가입 된 클라이언트 또는 AD DS 도구를 설치 하는 서버에서 다음을 수행 합니다.  다음 반복에 Windows Server 2012 DC 및 Windows Server 2012 R2 DC를 대상으로 합니다.  
  
1.  검토 합니다 ["보다 효율적인 Microsoft AD 사용 응용 프로그램 만들기"](https://msdn.microsoft.com/library/ms808539.aspx) 문서 및 필요에 따라를 다시 참조 하세요.  
  
2.  검색 통계를 활성화 LDP를 사용 합니다 (참조 [LDP 통계 컨트롤을 사용 하도록 설정 하려면](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_EnableStats))  
  
3.  여러 LDAP 검색을 수행 하 고 결과의 맨 위에 있는 통계 정보를 관찰 합니다.  다른에서 동일한 검색을 반복 하는 작업 이므로에 문서화 메모장 텍스트 파일입니다.  
  
4.  쿼리 최적화 프로그램이 인덱스 특성으로 인해 최적화 하기 위해 있어야 하는 LDAP 검색 수행  
  
5.  완료 하려면 시간이 오래 걸리는 검색을 구성 하려고 (늘려야 할 수도 합니다 **시간 제한** 검색 시간 초과 되지 않습니다 있도록 옵션).  
  
### <a name="additional-resources"></a>추가 리소스  
[Active Directory 검색은 무엇 인가요?](https://technet.microsoft.com/library/cc783845(v=ws.10).aspx)  
  
[Active Directory 작업을 검색 하는 방법](https://technet.microsoft.com/library/cc755809(v=WS.10).aspx)  
  
[보다 효율적인 Microsoft Active Directory 사용 응용 프로그램 만들기](https://msdn.microsoft.com/library/ms808539.aspx)  
  
[951581](https://support.microsoft.com/kb/951581) LDAP 쿼리 AD에 예상 보다 느리게 실행 되거나 LDS/ADAM 디렉터리 서비스 및 이벤트 ID 1644 기록 될 수 있습니다  
  
## <a name="BKMK_1644"></a>1644 이벤트 개선 사항  
  
### <a name="overview"></a>개요  
이 업데이트 문제 해결을 위해 지원 하기 위해 이벤트 ID 1644에 추가 LDAP 검색 결과 통계를 추가 합니다.  또한 시간 기반 임계값에 로깅을 사용 하도록 설정 하는 새 레지스트리 값을 있습니다.  이러한 향상 된이 기능은 Windows Server 2012 및 Windows Server 2008 R2 SP1 기술 자료를 통해 사용할 수 있는 내용이 [2800945](https://support.microsoft.com/kb/2800945) 사용 가능 하 게 Windows Server 2008 sp2 및 합니다.  
  
> [!NOTE]  
> -   이벤트 ID 1644 비효율적 이거나 비용이 많이 드는 LDAP 검색 문제 해결에 도움이 추가할 추가 LDAP 검색 통계  
> -   (예: 검색 시간 임계값을 지정할 수 있습니다. 로그의 이벤트 1644 100ms 보다 오래 된 검색을 위해)가 및 Inefficient 검색 결과 임계값 값을 지정 하는 대신  
  
### <a name="background"></a>배경  
Active Directory 성능 문제를 해결 하는 동안이 드러납니다 LDAP 검색 작업은 바로 문제를 일으킬 수 있습니다.  도메인 컨트롤러에서 처리 하는 비용이 많이 드는 혹은 LDAP 쿼리를 볼 수 있도록 로깅을 사용 하도록 설정 합니다.  로깅을 사용할 수 있도록, Field Engineering 진단 값을 설정 해야 하 고 비용이 많이 드는 / 비효율적인 검색 결과 임계값을 지정할 수 있습니다.  Field Engineering 로깅 수준을 5의 값을 사용 하도록 설정 하면, 이러한 기준을 충족 하는 모든 검색은 이벤트 ID 1644를 사용 하 여 디렉터리 서비스 이벤트 로그에 기록 됩니다.  
  
이벤트에는 다음이 포함 됩니다.  
  
-   클라이언트 IP 및 포트  
  
-   시작 노드  
  
-   Filter  
  
-   검색 범위  
  
-   특성 선택  
  
-   서버 컨트롤  
  
-   방문한 항목  
  
-   반환 된 항목  
  
그러나 키 데이터는 이벤트에서 누락 된 인덱스를 사용 하는 데 소요 된 시간에 검색 작업이 무엇 (있을 경우)와 같은 되었습니다.  
  
#### <a name="additional-search-statistics-added-to-event-1644"></a>이벤트 1644에 추가 하는 추가 검색 통계  
  
-   사용 되는 인덱스  
  
-   참조 페이지  
  
-   디스크에서 읽은 페이지  
  
-   디스크에서 preread 페이지  
  
-   클린 페이지 수정  
  
-   더티 페이지 수정  
  
-   검색 시간  
  
-   최적화를 방지 하는 특성  
  
#### <a name="new-time-based-threshold-registry-value-for-event-1644-logging"></a>1644 이벤트 로깅에 대 한 새 임계값 시간 기반 레지스트리 값  
가 및 Inefficient 검색 결과 임계값 값을 지정 하는 대신 검색 시간 임계값을 지정할 수 있습니다.  원하는 50 밀리초를 갖고 있는 모든 검색 결과 기록할 이상 지정 하면 됩니다 십진수 50 / 32 hex (외에도 Field Engineering 값을 설정).  
  
```  
Windows Registry Editor Version 5.00  
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters]  
"Search Time Threshold (msecs)"=dword:00000032  
```  
  
#### <a name="comparison-of-the-old-and-new-event-id-1644"></a>이전 및 새 이벤트 ID 1644의 비교  
이전  
  
![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_Event1644_2012.gif)  
  
새로 만들기  
  
![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_Event1644_2012R2.gif)  
  
#### <a name="try-this-use-the-event-log-to-return-query-statistics"></a>다음과 같이 해보십시오. 이벤트 로그를 사용 하 여 쿼리 통계를 반환 합니다.  
  
1.  다음 반복에 Windows Server 2012 DC 및 Windows Server 2012 R2 DC를 대상으로 합니다. 각 검색 후 두 개의 Dc에서 이벤트 ID 1644s를 관찰 합니다.  
  
2.  Regedit를 사용 하 여 로깅을 이벤트 ID 1644 시간 기반 임계값을 사용 하 여 Windows Server 2012 R2 DC에 Windows Server 2012 DC에 대 한 이전 메서드.  
  
3.  임계값을 초과 하 고 결과의 맨 위에 있는 통계 정보를 관찰 하는 여러 LDAP 검색을 수행 합니다.  앞에서 설명한 LDAP 쿼리를 사용 하 고 동일한 검색을 반복 합니다.  
  
4.  쿼리 최적화 프로그램은 수 없는 하나 이상의 특성은 인덱싱되지 때문에 최적화 하기 위해 LDAP 검색을 수행 합니다.  
  
## <a name="BKMK_ADRepl"></a>Active Directory 복제 처리량 개선 사항  
  
### <a name="overview"></a>개요  
AD 복제 복제 전송에 대 한 RPC를 사용합니다. 기본적으로 RPC는 8k 전송 버퍼와 5k 패킷 크기를 사용합니다. 이 효과가 net 보내는 인스턴스는 세 개의 패킷을 (약 15 K 만한 데이터)를 전송 하 고 자세한 보내기 전에 네트워크 왕복 대기 해야 합니다. 3 밀리초를 가정 하 고 왕복 시간 최대 처리량 1Gbps 또는 10 g b p s 네트워크 에서도 40Mbps 관련 됩니다.  
  
> [!NOTE]  
> -   이 업데이트는 최대 AD 복제 처리량이 40Mbps에서 약 600mbps 조정합니다.  
>   
>     -   네트워크의 수를 줄일 수 있는 RPC 송신 버퍼 크기를 증가 라운드트립  
> -   높은 속도에서 가장 눈에 띄는 수는 대기 시간이 긴 네트워크입니다.  
  
이 업데이트는 256KB로 8k에서 RPC 전송 버퍼 크기를 변경 하 여 약 600mbps 최대 처리량을 늘립니다.  이 변경은 8k를 초과 해 성장 하도록 TCP 창 크기를 왕복 네트워크의 수를 줄입니다.  
  
> [!NOTE]  
> 이 동작을 수정 하는 구성 가능한 설정이 없습니다.  
  
### <a name="additional-resources"></a>추가 리소스  
[Active Directory 복제 모델 작동 방식](https://technet.microsoft.com/library/cc772726(v=WS.10).aspx)  
  


