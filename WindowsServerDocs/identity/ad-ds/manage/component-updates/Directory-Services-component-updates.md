---
ms.assetid: 8a3cf2ae-2511-4eea-afd5-a43179a78613
title: 디렉터리 서비스 구성 요소 업데이트
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: cde839feda47d55415b2b6cc1026a7a3e6515a44
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823096"
---
# <a name="directory-services-component-updates"></a>디렉터리 서비스 구성 요소 업데이트

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**작성자**: Justin Turner, Windows 그룹이 포함 된 선임 지원 에스컬레이션 엔지니어  
  
> [!NOTE]  
> 이 콘텐츠는 Microsoft 고객 지원 엔지니어에 의해 작성되었으며 Windows Server 2012 R2의 기능 및 솔루션에 대해 TechNet에서 일반적으로 제공하는 항목보다 더 자세한 기술적 설명을 찾고 있는 숙련된 관리자 및 시스템 설계자를 대상으로 합니다. 그러나 동일한 편집 과정을 수행하지 않았으므로 일부 언어는 일반적으로 TechNet에서 찾을 수 있는 것보다 완벽하지 않을 수 있습니다.  
  
이 단원에서는 Windows Server 2012 r 2의 디렉터리 서비스 구성 요소 업데이트에 대해 설명 합니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
다음과 같은 새로운 디렉터리 서비스 구성 요소 업데이트에 대해 설명 합니다.  
  
-   다음과 같은 새로운 디렉터리 서비스 구성 요소 업데이트에 대해 설명 합니다.  
  
    -   [도메인 및 포리스트 기능 수준](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_FL)  
  
    -   [NTFRS의 사용 중단](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_NTFRS)  
  
    -   [LDAP 쿼리 최적화 프로그램 변경 사항](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_LDAPQuery)  
  
    -   [1644 이벤트 개선 사항](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_1644)  
  
    -   [Active Directory 복제 처리량 개선 사항](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_ADRepl)  
  
## <a name="domain-and-forest-functional-levels"></a><a name="BKMK_FL"></a>도메인 및 포리스트 기능 수준  
  
### <a name="overview"></a>개요  
이 섹션에서는 도메인 및 포리스트 기능 수준 변경에 대해 간략하게 소개 합니다.  
  
### <a name="new-dfl-and-ffl"></a>새 DFL 및 FFL  
릴리스에는 새 도메인 및 포리스트 기능 수준이 있습니다.  
  
-   포리스트 기능 수준: Windows Server 2012 R2  
  
-   도메인 기능 수준: Windows Server 2012 R2  
  
### <a name="the-windows-server-2012-r2-domain-functional-level-enables-support-for-the-following"></a>Windows Server 2012 R2 도메인 기능 수준을 사용 하면 다음을 지원할 수 있습니다.  
  
1.  *보호 된 사용자* 에 대 한 DC 쪽 보호  
  
    Windows Server 2012 R2 도메인을 인증 하는 *보호 된 사용자* 는 **더 이상**다음을 수행할 수 없습니다.  
  
    -   NTLM 인증을 통한 인증  
  
    -   Kerberos 사전 인증에 DES 또는 RC4 암호 그룹 사용  
  
    -   제한 없는 위임 또는 제한된 위임을 사용한 위임  
  
    -   초기 4시간의 수명이 지난 후 사용자 티켓(TGT) 갱신  
  
2.  인증 정책  
  
    Windows Server 2012 R2 도메인의 계정에 적용 하 여 계정이 로그온 할 수 있는 호스트를 제어 하 고 계정으로 실행 되는 서비스에 대 한 인증 액세스 제어 조건을 적용할 수 있는 새로운 포리스트 기반 Active Directory 정책  
  
3.  Authentication Policy Silos  
  
    인증 정책 또는 인증 격리를 위해 계정을 분류 하는 데 사용할 사용자, 관리 서비스 및 컴퓨터 계정 간의 관계를 만들 수 있는 새 포리스트 기반 Active Directory 개체입니다.  
  
자세한 내용은 보호 된 계정을 구성 하는 방법을 참조 하세요.  
  
위의 기능 외에도 Windows Server 2012 R2 도메인 기능 수준을 사용 하면 도메인의 모든 도메인 컨트롤러가 Windows Server 2012 r 2를 실행 합니다.  
Windows Server 2012 R2 포리스트 기능 수준은 새로운 기능을 제공 하지 않지만 포리스트에서 생성 된 새 도메인은 Windows Server 2012 R2 도메인 기능 수준에서 자동으로 작동 되도록 합니다.  
  
### <a name="minimum-dfl-enforced-on-new-domain-creation"></a>새 도메인 만들기에 적용 된 최소 DFL  
Windows Server 2008 DFL은 새 도메인을 만들 때 지원 되는 최소 기능 수준입니다.  
  
> [!NOTE]  
> FRS의 사용 중단은 서버 관리자 또는 Windows PowerShell을 통해 Windows Server 2008 보다 낮은 도메인 기능 수준을 사용 하 여 새 도메인을 설치 하는 기능을 제거 하 여 수행 됩니다.  
  
### <a name="lowering-the-forest-and-domain-functional-levels"></a>포리스트 및 도메인 기능 수준 낮추기  
포리스트 및 도메인 기능 수준은 기본적으로 새 도메인 및 새 포리스트 만들기에서 Windows Server 2012 r 2로 설정 되지만 Windows PowerShell을 사용 하 여 낮출 수 있습니다.  
  
Windows PowerShell을 사용 하 여 포리스트 기능 수준을 높이 거 나 낮추려면 **set-adforestmode** cmdlet을 사용 합니다.  
  
**Contoso.com FFL을 Windows Server 2008 모드로 설정 하려면 다음을 수행 합니다.**  
  
```sql  
Set-ADForestMode -ForestMode Windows2008Forest -Identity contoso.com  
```  
  
Windows PowerShell을 사용 하 여 도메인 기능 수준을 높이 거 나 낮추려면 Set-ADDomainMode cmdlet을 사용 합니다.  
  
**Contoso.com DFL을 Windows Server 2008 모드로 설정 하려면 다음을 수행 합니다.**  
  
```powershell  
Set-ADDomainMode -DomainMode Windows2008Domain -Identity contoso.com  
```  
  
Windows Server 2012 r 2를 실행 하는 DC를 2003 DFL을 실행 하는 기존 도메인에 추가 복제본으로 프로 모션 합니다.  
  
기존 포리스트에 새 도메인 만들기  
  
![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_FFL.gif)  
  
### <a name="adprep"></a>ADPREP  
이 릴리스에는 새 포리스트 또는 도메인 작업이 없습니다.  
  
이러한 .ldf 파일에는 **장치 등록 서비스**에 대 한 스키마 변경 내용이 포함 되어 있습니다.  
  
1.  Sch59  
  
2.  Sch61  
  
3.  Sch62  
  
4.  Sch63  
  
5.  Sch64  
  
6.  Sch65  
  
7.  Sch67  
  
**작업 폴더:**  
  
1.  Sch66  
  
**MSODS**  
  
1.  Sch60  
  
**인증 정책 및 사일로**  
  
1.  Sch68  
  
2.  Sch69  
  
## <a name="deprecation-of-ntfrs"></a><a name="BKMK_NTFRS"></a>NTFRS 사용 중단  
  
### <a name="overview"></a>개요  
FRS는 Windows Server 2012 r 2에서 더 이상 사용 되지 않습니다.  FRS의 사용 중단은 Windows Server 2008의 최소 DFL (도메인 기능 수준)을 적용 하 여 수행 됩니다.  이 적용은 서버 관리자 또는 Windows PowerShell을 사용 하 여 새 도메인을 만든 경우에만 표시 됩니다.  
  
-DomainMode 매개 변수를 Install-ADDSForest 또는 Install-Addsforest cmdlet과 함께 사용 하 여 도메인 기능 수준을 지정 합니다.  이 매개 변수에 대해 지원 되는 값은 유효한 정수 또는 해당 하는 열거 문자열 값일 수 있습니다. 예를 들어 Windows Server 2008 r 2로 도메인 모드 수준을 설정 하려면 4 또는 "Win2008R2" 값 중 하나를 지정할 수 있습니다.  서버 2012 r 2에서 이러한 cmdlet을 실행할 때 유효한 값에는 Windows server 2008 (3, Win2008) windows server 2008 R2 (4, Win2008R2) windows Server 2012 (5, Win2012) 및 Windows Server 2012 R2 (6, Win2012R2)에 대 한 값이 포함 됩니다. 도메인 기능 수준은 포리스트 기능 수준보다 낮은 값으로 설정할 수 없으며, 포리스트 기능 수준보다 높은 값으로 설정할 수는 있습니다.  이 릴리스에서는 FRS가 더 이상 사용 되지 않으므로 windows server 2003 (2, Win2003)는 Windows Server 2012 r 2에서 실행 될 때 이러한 cmdlet에 대해 인식 되는 매개 변수가 아닙니다.  
  
![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_PS_Install2003DFL.gif)  
  
![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_PS_InstallDFL2.gif)  
  
## <a name="ldap-query-optimizer-changes"></a><a name="BKMK_LDAPQuery"></a>LDAP 쿼리 최적화 프로그램 변경 내용  
  
### <a name="overview"></a>개요  
LDAP 쿼리 최적화 프로그램 알고리즘이 다시 평가 되 고 추가 최적화 되었습니다.  그 결과 LDAP 검색 효율성 및 복잡 한 쿼리의 LDAP 검색 시간에 대 한 성능이 향상 됩니다.  
  
> [!NOTE]
> <strong>개발자:</strong>LDAP 쿼리에서 ESE 쿼리로의 향상 된 기능을 통해 검색 성능이 향상 되었습니다.  특정 수준의 복잡성을 초과 하는 LDAP 필터는 최적화 된 인덱스 선택을 방지 하므로 성능이 크게 저하 됩니다 (1000x 이상). 이렇게 변경 하면이 문제를 방지 하기 위해 LDAP 쿼리에 대 한 인덱스를 선택 하는 방법이 변경 됩니다.  
> 
> [!NOTE]
> LDAP 쿼리 최적화 프로그램 알고리즘의 전체 재정비 다음과 같은 결과가 발생 합니다.  
> 
> -   빠른 검색 시간  
> -   효율성 향상으로 Dc에서 더 많은 작업을 수행할 수 있습니다.  
> -   AD 성능 문제에 대 한 지원 감소  
> -   Windows Server 2008 r 2로 다시 이식 (KB 2862304)  
  
### <a name="background"></a>배경  
Active Directory 검색 기능은 도메인 컨트롤러에서 제공 하는 핵심 서비스입니다.  다른 서비스 및 lob (기간 업무) 응용 프로그램은 Active Directory 검색을 사용 합니다.  이 기능을 사용할 수 없는 경우 비즈니스 운영 중단을 중지할 수 있습니다.  핵심 이며 자주 사용 되는 서비스인 도메인 컨트롤러는 LDAP 검색 트래픽을 효율적으로 처리 해야 합니다.  Ldap 쿼리 최적화 프로그램 알고리즘은 LDAP 검색 필터를 데이터베이스에 이미 인덱싱되는 레코드를 통해 충족 될 수 있는 결과 집합에 매핑하여 ldap 검색을 최대한 효율적으로 수행 하려고 합니다.  이 알고리즘은 다시 평가 되 고 추가로 최적화 되었습니다.  그 결과 LDAP 검색 효율성 및 복잡 한 쿼리의 LDAP 검색 시간에 대 한 성능이 향상 됩니다.  
  
### <a name="details-of-change"></a>변경 내용에 대 한 세부 정보  
LDAP 검색에는 다음이 포함 됩니다.  
  
-   계층 내에서 검색을 시작할 위치 (NC 헤드, OU, 개체)  
  
-   검색 필터  
  
-   반환할 특성 목록입니다.  
  
검색 프로세스는 다음과 같이 요약할 수 있습니다.  
  
1.  가능 하면 검색 필터를 단순화 합니다.  
  
2.  가장 작은 집합을 반환 하는 인덱스 키 집합을 선택 합니다.  
  
3.  인덱스 키에 대해 하나 이상의 교차를 수행 하 여 검사 된 집합을 줄입니다.  
  
4.  대상 집합의 각 레코드에 대해 보안 뿐만 아니라 필터 식을 평가 합니다. 필터가 TRUE로 평가 되 고 액세스가 부여 된 경우이 레코드를 클라이언트에 반환 합니다.  
  
LDAP 쿼리 최적화 작업은 설명 된 집합의 크기를 줄이기 위해 2 단계와 3 단계를 수정 합니다. 구체적으로 말하자면, 현재 구현은 중복 된 인덱스 키를 선택 하 고 중복 교집합을 수행 합니다.  
  
### <a name="comparison-between-old-and-new-algorithm"></a>이전 알고리즘 및 새 알고리즘 비교  
이 예에서 비효율적인 LDAP 검색의 대상은 Windows Server 2012 도메인 컨트롤러입니다.  검색은 더 효율적인 인덱스를 찾지 못한 결과로 약 44 초 이내에 완료 됩니다.  
  
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
  
### <a name="sample-results-using-the-new-algorithm"></a>새 알고리즘을 사용 하는 샘플 결과  
이 예에서는 위와 똑같은 검색을 반복 하지만 Windows Server 2012 R2 도메인 컨트롤러를 대상으로 합니다.  LDAP 쿼리 최적화 프로그램 알고리즘의 향상 된 기능 때문에 동일한 검색은 1 초 이내에 완료 됩니다.  
  
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
  
-   에서 트리를 최적화할 수 없는 경우:  
  
    -   예: 트리의 식이 인덱싱되지 않은 열 위에 있습니다.  
  
    -   최적화를 방지 하는 인덱스 목록을 기록 합니다.  
  
    -   ETW 추적 및 이벤트 ID 1644을 통해 노출 됨  
  
        ![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_Event1644.gif)  
  
### <a name="to-enable-the-stats-control-in-ldp"></a><a name="BKMK_EnableStats"></a>LDP에서 통계 컨트롤을 사용 하도록 설정 하려면  
  
1.  LDP.EXE를 열고 도메인 컨트롤러에 연결 하 여 바인딩합니다.  
  
2.  **옵션** 메뉴에서 **컨트롤**을 클릭 합니다.  
  
3.  컨트롤 대화 상자에서 **미리 정의 된 로드** 풀 다운 메뉴를 확장 하 고 **검색 통계** 를 클릭 한 다음 **확인**을 클릭 합니다.  
  
    ![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_Controls.gif)  
  
4.  **찾아보기** 메뉴에서 **검색** 을 클릭 합니다.  
  
5.  검색 대화 상자에서 **옵션** 단추를 선택 합니다.  
  
6.  검색 옵션 대화 상자에서 **확장** 된 확인란을 선택 했는지 확인 하 고 **확인**을 선택 합니다.  
  
    ![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_SearchOptions.gif)  
  
### <a name="try-this-use-ldp-to-return-query-statistics"></a>이 작업을 수행해 보세요. LDP를 사용 하 여 쿼리 통계 반환  
도메인 컨트롤러에서 또는 AD DS 도구가 설치 된 도메인에 가입 된 클라이언트 또는 서버에서 다음을 수행 합니다.  Windows Server 2012 DC 및 Windows Server 2012 R2 DC를 대상으로 다음을 반복 합니다.  
  
1.  ["보다 효율적인 MICROSOFT AD 지원 응용 프로그램 만들기"](https://msdn.microsoft.com/library/ms808539.aspx) 문서를 검토 하 고 필요에 따라 다시 참조 하세요.  
  
2.  LDP를 사용 하 여 검색 통계를 사용 하도록 설정 합니다 ( [ldp에서 통계 컨트롤을 사용 하도록 설정 하려면](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_EnableStats)참조).  
  
3.  몇 가지 LDAP 검색을 수행 하 고 결과 위쪽의 통계 정보를 확인 합니다.  다른 작업에서 동일한 검색을 반복 하 여 메모장 텍스트 파일에 문서화 합니다.  
  
4.  특성 인덱스로 인해 쿼리 최적화 프로그램이 최적화할 수 있는 LDAP 검색을 수행 합니다.  
  
5.  완료 하는 데 시간이 오래 걸리는 검색을 생성 하려고 합니다. **시간 제한** 옵션을 늘려 검색 시간을 초과 하지 않도록 할 수도 있습니다.  
  
### <a name="additional-resources"></a>추가 리소스  
[Active Directory 검색 이란?](https://technet.microsoft.com/library/cc783845(v=ws.10).aspx)  
  
[Active Directory 검색 작동 방법](https://technet.microsoft.com/library/cc755809(v=WS.10).aspx)  
  
[보다 효율적인 Microsoft Active Directory 지원 응용 프로그램 만들기](https://msdn.microsoft.com/library/ms808539.aspx)  
  
[951581](https://support.microsoft.com/kb/951581) LDAP 쿼리가 AD 또는 LDS/ADAM 디렉터리 서비스에서 예상 보다 느리게 실행 되 고 이벤트 ID 1644이 기록 될 수 있습니다.  
  
## <a name="1644-event-improvements"></a><a name="BKMK_1644"></a>1644 이벤트 개선  
  
### <a name="overview"></a>개요  
이 업데이트는 문제 해결을 지원 하기 위해 이벤트 ID 1644에 추가 LDAP 검색 결과 통계를 추가 합니다.  또한 시간 기반 임계값에서 로깅을 사용 하도록 설정 하는 데 사용할 수 있는 새 레지스트리 값이 있습니다.  이러한 향상 된 기능은 KB [2800945](https://support.microsoft.com/kb/2800945) 를 통해 windows server 2012 및 windows Server 2008 R2 s p 1에서 사용할 수 있으며 windows server 2008 s p 2에서 사용할 수 있게 됩니다.  
  
> [!NOTE]  
> -   비효율적인 또는 비용이 많이 드는 LDAP 검색 문제를 해결 하는 데 도움이 되는 추가 LDAP 검색 통계가 이벤트 ID 1644에 추가 됩니다.  
> -   이제 검색 시간 임계값을 지정할 수 있습니다 (예: 비용이 많이 들고 비효율적인 검색 결과 임계값을 지정 하는 대신 100ms 보다 오래 걸리는 검색에 대해 이벤트 1644을 기록 합니다.  
  
### <a name="background"></a>배경  
Active Directory 성능 문제를 해결 하는 동안 LDAP 검색 작업이 문제에 영향을 미칠 수 있습니다.  도메인 컨트롤러에서 처리 하는 비용이 많이 들고 비효율적인 LDAP 쿼리를 볼 수 있도록 로깅을 사용 하도록 결정 합니다.  로깅을 사용 하도록 설정 하려면 필드 엔지니어링 진단 값을 설정 하 고 필요에 따라 비용이 많이 들고 비효율적인 검색 결과 임계값을 지정할 수 있습니다.  필드 엔지니어링 로깅 수준을 값 5로 설정 하면 이러한 조건을 충족 하는 모든 검색이 디렉터리 서비스 이벤트 로그에 이벤트 ID 1644으로 기록 됩니다.  
  
이벤트에는 다음이 포함 됩니다.  
  
-   클라이언트 IP 및 포트  
  
-   시작 노드  
  
-   필터  
  
-   검색 범위  
  
-   특성 선택  
  
-   서버 컨트롤  
  
-   방문한 항목  
  
-   반환 된 항목  
  
그러나 검색 작업에 소요 된 시간 및 사용 된 (있는 경우) 인덱스와 같은 키 데이터는 이벤트에서 누락 됩니다.  
  
#### <a name="additional-search-statistics-added-to-event-1644"></a>이벤트 1644에 추가 된 추가 검색 통계  
  
-   사용 되는 인덱스  
  
-   참조 된 페이지  
  
-   디스크에서 읽은 페이지  
  
-   디스크에서 페이지 preread  
  
-   수정 된 페이지 수정  
  
-   더티 페이지 수정 됨  
  
-   검색 시간  
  
-   최적화를 방지 하는 특성  
  
#### <a name="new-time-based-threshold-registry-value-for-event-1644-logging"></a>이벤트 1644 로깅에 대 한 새 시간 기반 임계값 레지스트리 값  
비용이 많이 들고 비효율적인 검색 결과 임계값을 지정 하는 대신 검색 시간 임계값을 지정할 수 있습니다.  50 밀리초 이상 걸린 모든 검색 결과를 기록 하려는 경우 50 decimal/32 hex를 지정 하 고 필드 엔지니어링 값을 설정 합니다.  
  
```  
Windows Registry Editor Version 5.00  
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters]  
"Search Time Threshold (msecs)"=dword:00000032  
```  
  
#### <a name="comparison-of-the-old-and-new-event-id-1644"></a>이전 이벤트와 새 이벤트 ID 1644 비교  
원래의  
  
![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_Event1644_2012.gif)  
  
새로 만들기  
  
![디렉터리 서비스 업데이트](media/Directory-Services-component-updates/GTR_ADDS_Event1644_2012R2.gif)  
  
#### <a name="try-this-use-the-event-log-to-return-query-statistics"></a>이 작업을 수행 합니다. 이벤트 로그를 사용 하 여 쿼리 통계 반환  
  
1.  Windows Server 2012 DC 및 Windows Server 2012 R2 DC를 대상으로 다음을 반복 합니다. 각 검색 후 두 Dc에서 이벤트 ID 1644s를 확인 합니다.  
  
2.  Regedit를 사용 하 여 windows server 2012 R2 DC에 시간 기반 임계값을 사용 하 고 Windows Server 2012 DC에서 이전 방법을 사용 하 여 이벤트 ID 1644 로깅을 사용 하도록 설정 합니다.  
  
3.  임계값을 초과 하는 여러 LDAP 검색을 수행 하 고 결과 위쪽의 통계 정보를 관찰 합니다.  앞에서 설명한 LDAP 쿼리를 사용 하 여 동일한 검색을 반복 합니다.  
  
4.  하나 이상의 특성이 인덱싱되지 않았기 때문에 쿼리 최적화 프로그램에서 최적화할 수 없는 LDAP 검색을 수행 합니다.  
  
## <a name="active-directory-replication-throughput-improvement"></a><a name="BKMK_ADRepl"></a>Active Directory 복제 처리량 향상  
  
### <a name="overview"></a>개요  
AD 복제는 해당 복제 전송에 RPC를 사용 합니다. 기본적으로 RPC는 8K 전송 버퍼와 5K 패킷 크기를 사용 합니다. 이는 전송 인스턴스가 3 개의 패킷 (약 15K 분량의 데이터)을 전송 하 고 네트워크 왕복을 기다린 후 더 많은 데이터를 전송 하도록 하는 순 효과가 있습니다. 3ms 왕복 시간을 가정할 때 최고 처리량은 1Gbps 또는 10gbps 네트워크에도 40Mbps를 기준으로 합니다.  
  
> [!NOTE]  
> -   이 업데이트는 최대 AD 복제 처리량을 40Mbps에서 600 Mbps로 조정 합니다.  
>   
>     -   네트워크 왕복 횟수를 줄이는 RPC 전송 버퍼 크기를 늘립니다.  
> -   고속 및 대기 시간이 긴 네트워크에서 효과가 가장 두드러지게 나타납니다.  
  
이 업데이트는 RPC 송신 버퍼 크기를 8K에서 256KB로 변경 하 여 최대 처리량을 600 Mbps로 늘립니다.  이러한 변경을 통해 TCP 창 크기를 8K 이상으로 늘릴 수 있으므로 네트워크 왕복 횟수가 줄어듭니다.  
  
> [!NOTE]  
> 이 동작을 수정 하는 구성 가능한 설정이 없습니다.  
  
### <a name="additional-resources"></a>추가 리소스  
[Active Directory 복제 모델의 작동 방식](https://technet.microsoft.com/library/cc772726(v=WS.10).aspx)  
  


