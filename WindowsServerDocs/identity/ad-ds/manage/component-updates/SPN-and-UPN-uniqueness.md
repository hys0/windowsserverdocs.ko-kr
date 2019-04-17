---
ms.assetid: 40bc24b1-2e7d-4e77-bd0f-794743250888
title: "SPN 및 UPN 고유"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 81d686c81082ad29384585d541c1304d654e1924
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="spn-and-upn-uniqueness"></a>SPN 및 UPN 고유

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**작성자**: Windows 그룹과 조자룡 Turner, 선임 지원 엔지니어로  
  
> [!NOTE]  
> 이 콘텐츠는 Microsoft 고객 지원 담당자가 작성 하며 경험이 관리자와 technet 항목 일반적으로 제공 하는 것 보다에 대 한 보다 긴밀 기술 설명은 기능 및 Windows Server 2012 r 2에 대 한 해결 방법을 찾는 누가 시스템 개발자를 위한 것입니다. 그러나 받지 않았습니다 동일한 편집 가공 일부 언어 일반적으로 technet 찾을 수 보다 세련 된 적게 보일 수 있도록 합니다.  
  
## <a name="overview"></a>개요  
Windows Server 2012 r 2 차단 생성 실행 하는 도메인 컨트롤러 중복 서비스 사용자 이름 (SPN) 및 사용자 이름 (UPN). 이것 복원 하거나 개체의 이름 바꾸기 또는 삭제 개체의 애니메이션 전화를 받으면 중복 포함 됩니다.  
  
### <a name="background"></a>배경  
중복 서비스 SPN 사용자 이름 () 일반적으로 발생 인증 오류가 발생할 수 있으며 과도 하 게 LSASS cpu 될 수 있습니다. 차단 중복 SPN 또는 UPN를 추가 하려면 상자에서 방법은 없습니다. *  
  
중복 UPN 값 중단 온-프레미스 간 동기화 광고 및 Office 365 합니다.  
  
*Setspn.exe는 일반적으로 새 Spn 만드는 데 사용 하 고 기능이 추가 중복 확인 하는 Windows Server 2008과 함께 출시 된 버전으로 빌드 되었습니다.  
  
**테이블 SEQ 테이블 \\\ * 아랍어 1: UPN 및 SPN 고유**  
  
|기능|메모|  
|-----------|-----------|  
|UPN 고유|중복 Upn 휴식 동기화의 온-프레미스 Office 365 같은 Windows Azure AD 기반 서비스의 계정과 광고 합니다.|  
|SPN 고유|Kerberos Spn 상호 인증을 위한 필요합니다.  중복 Spn 인증 오류가 발생합니다.|  
  
Upn와 Spn 고유 요구 사항에 대 한 자세한 내용은 참조 [고유 제한](https://msdn.microsoft.com/library/dn392337.aspx)합니다.  
  
## <a name="symptoms"></a>증상이  
오류 코드 8467 또는 8468 또는 hex 기호 또는 문자열 해당 하는 화면의 다양 한에 기록 됩니다 대화 상자 및 이벤트 ID 2974 디렉터리 서비스 이벤트 로그에 기록 됩니다. 다음과 같은 경우에만 중복 UPN 또는 SPN을 차단 됩니다.  
  
-   Windows Server 2012 r 2 DC로 처리 쓰기  
  
**테이블 SEQ 테이블 \\\ * 아랍어 2: UPN 및 SPN 고유 오류 코드**  
  
|소수점|Hex|기호|문자열|  
|-----------|-------|------------|----------|  
|8467|21C 7|ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST|또한/수정 하기 위해 제공한 SPN 값이 독특한 숲 전체는 작업이 실패 했습니다.|  
|8648|21C 8|ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST|또한/수정 하기 위해 제공한 UPN 값이 독특한 숲 전체는 작업이 실패 했습니다.|  
  
## <a name="new-user-creation-fails-if-upn-is-not-unique"></a>새 사용자 작성 실패 UPN 고유 하지 않은 경우  
  
### <a name="dsamsc"></a>DSA.msc  
사용자 로그온 이름을 선택한 이미이 기업에서 사용 중입니다. 다른 로그온 이름을 선택한 후 다시 시도 합니다.  
  
![SPN 및 UPN 고유](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig01_DupUPN.gif)  
  
기존 계정을 수정 합니다.  
  
기업에서 이미 사용자 지정 된 로그온 이름입니다. 접두사 변경 하거나 다른 접미사 목록에서 선택 하 여 새 암호를 지정 합니다.  
  
![SPN 및 UPN 고유](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig02_DupUPNMod.gif)  
  
### <a name="active-directory-administrative-center-dsacexe"></a>관리 active Directory (DSAC.exe) 센터  
이미 있는 UPN 된 Active Directory 관리 센터에서 새로운 사용자를 시도 다음과 같은 오류를 생성 됩니다.  
  
![SPN 및 UPN 고유](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig03_DupUPNADAC.gif)  
  
**SEQ 골격을 그린 그림 \\\ * 중복 UPN 되기 때문에 새로운 사용자 만들기 실패 하는 경우 광고 관리 센터에 표시 된 아랍어 1 오류**  
  
### <a name="event-2974-source-activedirectorydomainservice"></a>이벤트 2974 소스: ActiveDirectory_DomainService  
![SPN 및 UPN 고유](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig04_Event2974.gif)  
  
**SEQ 골격을 그린 그림 \\\ * 8648 오류로 아랍어 이벤트 ID 2974 2**  
  
차단 된 값 및 이미 값을 포함 하는 (최대 10) 하나 또는 여러 개의 개체 목록이 2974 이벤트 보여 줍니다.  다음 그림에서는 UPN 특성 값을 볼 수 있습니다 *** dhunt@blue.contoso.com *** 이미에 네 가지 다른 개체 합니다.  Windows Server 2012 r 2의 새로운 기능 이므로 하위 수준 Dc 처리 쓰기 시도 혼합된 환경에서 중복 UPN 및 Spn 실수로 생성 여전히 수행 됩니다.  
  
![SPN 및 UPN 고유](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig05_Event2974ShowAllDups.gif)  
  
**SEQ 골격을 그린 그림 \\\ * 아랍어 3 이벤트 2974 모든 개체 중복 UPN 포함 된 표시**  
  
> [!TIP]  
> 이벤트 ID 2974s에 정기적으로 검토 합니다.  
>   
> -   식별 중복 UPN 또는 Spn 만들기 시도  
> -   이미 중복 포함 되어 있는 개체 식별  
  
8648 = "작업 UPN 값을 추가/수정 하기 위해 제공 고유한 숲 전체 되지 않아 하지 못했습니다."  
  
### <a name="setspn"></a>SetSPN:  
Setspn.exe 사용 하는 경우 Windows Server 2008 출시 된 후에 기본 제공 중복 SPN 검색을 초래 했습니다는 **"-S"** 옵션이 있습니다.  그러나 사용 하 여 중복 SPN 검색 무시할 수는 **"-A"** 옵션 합니다.  중복 SPN 만들기 SetSPN-옵션과 함께 사용 하 여 Windows Server 2012 r 2 DC 대상으로 차단 되어 있습니다.  -S 옵션을 사용할 때 표시 되는 것과 같은 오류 메시지가 표시 됩니다. "복제 작업 중단 발견 SPN!"  
  
### <a name="adsiedit"></a>ADSIEDIT:  
  
```  
Operation failed. Error code: 0x21c8  
The operation failed because UPN value provided for addition/modification is not unique forest-wide.  
000021C8: AtrErr: DSID-03200BBA, #1: 0: 000021C8: DSID-03200BBA, problem 1005 (CONSTRAINT_ATT_TYPE), data 0, Att 90290 (userPrincipalName)  
```  
  
![SPN 및 UPN 고유](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig06_ADSI21c8.gif)  
  
**SEQ 골격을 그린 그림 \\\ * 중복 UPN 추가 차단 되어 있을 때 ADSIEdit에 표시 되는 아랍어 4 오류 메시지**  
  
### <a name="windows-powershell"></a>Windows PowerShell  
Windows Server 2012 r 2:  
  
![SPN 및 UPN 고유](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig07_SetADUser2012.gif)  
  
Windows Server 2012 r 2 DC 표적화 Server 2012에서 실행 PS:  
  
![SPN 및 UPN 고유](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig08_SetADUser2012R2.gif)  
  
DSAC.exe Windows Server 2012 r 2 DC 대상으로 Windows Server 2012에서 실행 합니다.  
  
![SPN 및 UPN 고유](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig09_UserCreateError.gif)  
  
**SEQ 골격을 그린 그림 \\\ * 아랍어 5 DSAC 사용자 작성 오류에 아닌-Windows Server 2012 r 2 Windows Server 2012 r 2 DC 대상으로 하는 동안**  
  
![SPN 및 UPN 고유](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig10_UserModError.gif)  
  
**SEQ 골격을 그린 그림 \\\ * 아랍어 6 DSAC 사용자 수정에서 아닌-Windows Server 2012 r 2 Windows Server 2012 r 2 DC 대상으로 하는 동안 오류**  
  
### <a name="restore-of-an-object-that-would-result-in-a-duplicate-upn-fails"></a>복원 중복 UPN 전화를 받으면 개체의 실패 합니다.  
![SPN 및 UPN 고유](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig11_RestoreDupUPN.gif)  
  
![SPN 및 UPN 고유](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig12_RestoreDupUPNError.gif)  
  
없음 이벤트가 개체 중복 UPN 때문 복원을 받지 못한 경우 / SPN 합니다.  
  
개체 UPN 복원 하기 위해에서 고유한 해야 합니다.  
  
1.  휴지통의 개체에 있는 UPN 식별  
  
2.  동일한 값을 가진 모든 사용자의 신원을 확인합니다  
  
3.  중복 UPN(s) 제거  
  
### <a name="identify-the-conflicting-upn-on-the-deleted-objectusing-repadminexe"></a>삭제 된 objectUsing repadmin.exe에 충돌 하는 UPN 식별  
  
```  
Repadmin /showattr DCName "DN of deleted objects container" /subtree /filter:"(msDS-LastKnownRDN=<NAME>)" /deleted /atts:userprincipalname  
```  
  
```  
repadmin /showattr DCName "CN=Deleted Objects,DC=blue,DC=contoso,DC=com" /subtree /filter:"(msDS-LastKnownRDN=Dianne Hunt2)" /deleted /atts:userprincipalname  
  
C:\>repadmin /showattr winbluedc1 "cn=deleted objects,dc=blue,dc=contoso,dc=com" /subtree /filter:"(msds-lastknownrdn=Dianne Hunt2)" /deleted /atts:userprincipalname  
DN: CN=Dianne Hunt2\0ADEL:dd3ab8a4-3005-4f2f-814f-d6fc54a1a1c0,CN=Deleted Object  
s,DC=blue,DC=contoso,DC=com  
    1> userPrincipalName: dhunt@blue.contoso.com  
```  
  
### <a name="to-identify-all-objects-with-the-same-upnusing-repadminexe"></a>모든 개체와 같은 UPN 식별: Repadmin.exe 사용  
  
```  
repadmin /showattr WinBlueDC1 "DC=blue,DC=contoso,DC=com" /subtree /filter:"(userPrincipalName=dhunt@blue.contoso.com)" /deleted /atts:DN  
  
C:\>repadmin /showattr winbluedc1 "dc=blue,dc=contoso,dc=com" /subtree /filter:"(userPrincipalName=dhunt@blue.contoso.com)" /deleted /atts:DN  
DN: CN=Administrator,CN=Users,DC=blue,DC=contoso,DC=com  
DN: CN=xouser1,CN=Users,DC=blue,DC=contoso,DC=com  
DN: CN=xouser10,CN=Users,DC=blue,DC=contoso,DC=com  
DN: CN=xouser100,CN=Users,DC=blue,DC=contoso,DC=com  
DN: CN=Dianne Hunt,OU=Marketing,DC=blue,DC=contoso,DC=com  
DN: CN=Dianne Hunt2\0ADEL:dd3ab8a4-3005-4f2f-814f-d6fc54a1a1c0,CN=Deleted Objects,DC=blue,DC=contoso,DC=com  
```  
  
> [!TIP]  
> 이전에 문서화 **삭제 /** repadmin.exe 매개 삭제 개체 결과 집합에 포함 하는 데 사용 되  
  
### <a name="using-global-search"></a>전 세계 검색을 사용 하 여  
  
-   Active Directory 관리 센터를 열고 탐색 하 고 **글로벌 검색**  
  
-   선택는 **LDAP 변환** 라디오 단추  
  
-   입력 * *(파티션에서 =*ConflictingUPN*) * *  
  
    -   교체 ***ConflictingUPN*** 충돌 하는 실제 UPN 함께  
  
-   선택 **적용**  
  
![SPN 및 UPN 고유](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig13_GlobalSearch.gif)  
  
### <a name="using-windows-powershell"></a>Windows PowerShell를 사용 하 여  
  
```  
Get-ADObject -LdapFilter "(userPrincipalName=dhunt@blue.contoso.com)" -IncludeDeletedObjects -SearchBase "DC=blue,DC=Contoso,DC=com" -SearchScope Subtree -Server winbluedc1.blue.contoso.com  
```  
  
![SPN 및 UPN 고유](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig13_GlobalSearchPS.gif)  
  
개체를 복원 하는 경우 사용자 다른 개체에서 중복 Upn을 제거 하 고 필요한 됩니다.  하나의 개체 ADSIEdit 중복을 제거 하는 데 충분 한 간단 합니다.  여러 개체 중복 된 경우 Windows PowerShell 더 나은 도구를 사용할 수 있습니다.  
  
수 파티션에서 특성 Windows PowerShell를 사용 하 여 다음과 같습니다.  
  
![SPN 및 UPN 고유](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig15_NullUPN.gif)  
  
> [!NOTE]  
> 파티션에서 특성 단일 값 특성 이므로이 절차 중복 UPN 제거 됩니다.  
  
### <a name="duplicate-spn"></a>SPN 복제  
![SPN 및 UPN 고유](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig16_DupSPN.gif)  
  
**SEQ 골격을 그린 그림 \\\ * 중복 SPN 추가 차단 되어 있을 때 ADSIEdit에 표시 되는 아랍어 8 오류 메시지**  
  
디렉터리 서비스는 이벤트 로그에 기록 된 **ActiveDirectory_DomainService** 이벤트 ID **2974**합니다.  
  
```  
Operation failed. Error code: 0x21c7  
The operation failed   
The attribute value provided is not unique in the forest or partition. Attribute:  
servicePrincipalName Value=<SPN>  
<Object DN> Winerror: 8467  
```  
  
![SPN 및 UPN 고유](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig17_DupSPN2974.gif)  
  
**SEQ 골격을 그린 그림 \\\ * 아랍어 9 오류 중복 SPN 만들기 차단 되어 있을 때 기록**  
  
### <a name="workflow"></a>워크플로  
  
-   **하는 경우 DC GC = =**  
  
    -   쿼리 로컬 만족 수 없음 offbox 통화 필요  
  
    -   ***UPN의 경우***  
  
        -   제공된 UPN에 대 한 쿼리가 로컬 숲 전체의 UPN 인덱스 (*파티션에서; 전체 색인*)  
  
            -   항목을 반환 하는 경우 = = 0 쓰기 진행->  
  
            -   항목을 반환 하는 경우! = 0 쓰기 실패->  
  
                -   이벤트 기록  
  
                -   또한 확장된 오류를 반환합니다.  
  
                    -   **8648:**  
  
                        *ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST*  
  
    -   ***SPN 경우***  
  
        -   제공된 SPN에 대 한 쿼리가 로컬 숲 전체 SPN 인덱스 (*쓰기; 전체 색인*)  
  
            -   항목을 반환 하는 경우 = = 0 쓰기 진행->  
  
            -   항목을 반환 하는 경우! = 0 쓰기 실패->  
  
                -   이벤트 기록  
  
                -   또한 확장된 오류를 반환합니다.  
  
                    -   **8647:**  
  
                        **ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST**  
  
-   **하는 경우 DC! GC =**  
  
    -   Offbox 통화 **바람직한** 하지만 중요 하지 즉,이 최대한 고유 확인  
  
        -   GC 찾을 수 없는 경우에 확인 로컬 DIT에 대해 진행  
  
        -   이벤트를 나타내는 등 기록  
  
    -   ***UPN의 경우***  
  
        -   LDAP 쿼리 가까운 GC에 대해 전송 되나요? 제공된 UPN에 대 한 쿼리가 GC의 전체 숲 UPN 인덱스 (*파티션에서; 전체 색인*)  
  
            -   항목을 반환 하는 경우 = = 0 쓰기 진행->  
  
            -   항목을 반환 하는 경우! = 0 쓰기 실패->  
  
                -   이벤트 기록  
  
                -   또한 확장된 오류를 반환합니다.  
  
                    -   **8648:**  
  
                        *ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST*  
  
    -   ***SPN 경우***  
  
        -   LDAP 쿼리 가까운 GC에 대해 전송 되나요? 제공 된 SPN에 대 한 쿼리가 GC의 숲 전체 SPN 인덱스 (*쓰기; 전체 색인*)  
  
            -   항목을 반환 하는 경우 = = 0 쓰기 진행->  
  
            -   항목을 반환 하는 경우! = 0 쓰기 실패->  
  
                -   이벤트 기록  
  
                -   또한 확장된 오류를 반환합니다.  
  
                    -   **8647:**  
  
                        *ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST*  
  
삭제 된 개체 인 다시 애니메이션 있는 SPN 또는 UPN 값 고유한 검사 합니다. 중복 발견 되 면 요청이 실패 합니다.  
  
-   DNS 호스트 이름, 삼로 계정 이름 등과 같은 특정 특성 변경에 대 한 수정 될 때 Spn 적절히 업데이트 됩니다. 이 과정에서 오래 된 Spn 삭제 되 고 새로운 Spn 생성 하 고 데이터베이스에 추가 됩니다. 필수 특성 수정 하는이 경로 트리거될는 다음과 같습니다.  
  
    -   ATT_DNS_HOST_NAME  
  
    -   ATT_MS_DS_ADDITIONAL_DNS_HOST_NAME  
  
    -   ATT_SAM_ACCOUNT_NAME  
  
    -   ATT_MS_DS_ADDITIONAL_SAM_ACCOUNT_NAME  
  
    -   ATT_SERVER_REFERENCE_BL  
  
    -   ATT_USER_ACCOUNT_CONTROL  
  
새 SPN 값 중은 중복을 수정을 실패 했습니다. 위의 목록의 중요 한 특성 ATT_DNS_HOST_NAME (디바이스 이름) 및 ATT_SAM_ACCOUNT_NAME (삼로 계정 이름)은 합니다.  
  
### <a name="try-this-exploring-spn-and-upn-uniqueness"></a>시도해 보기: 탐험 SPN 및 UPN 고유  
이 몇 가지 첫 번째 "**해보세요**" 모듈에서 활동 합니다.  이 모듈에 대 한 별도 환경 가이드가 않습니다.  **해보세요** 활동 랩 환경에서과 자료를 탐색할 수 있는 자유형 활동 기본적으로입니다.  다음 메시지 또는 스크립트 꺼졌는지 옵션을 직접 활동 들이 내놓는 아이디어입니다.  
  
> [!NOTE]  
> -   이 몇 가지 첫 번째 "**해보세요**" 활동 합니다.  
> -   이 모듈에 대 한 별도 환경 가이드가 않습니다.  
> -   **해보세요** 활동 랩 환경에서과 자료를 탐색할 수 있는 자유형 활동 기본적으로입니다.  
> -   다음 메시지 또는 스크립트 꺼졌는지 옵션을 직접 활동 들이 내놓는 아이디어입니다.  
> -   하지만 일부 섹션에 **해보세요** 프롬프트 사용자는 여전히 적절 한 위치 랩에서 콘텐츠를 탐색 하는 것이 좋습니다.  
  
SPN 및 UPN 고유 사용해 봅니다.  이러한 지시에 따라 하거나 원하는 수행 합니다.  
  
1.  새 사용자 UPN 함께 만들기  
  
2.  Spn와 계정 만들기  
  
3.  새 사용자 이미 이전에 정의 된 UPN 만들고 하거나 기존 계정 UPN 변경 합니다.  다른 계정에 SPN에 대해 동일한 작업을 수행합니다  
  
    1.  기존 사용자 계정에 이미 사용 UPN으로 채우려면  
  
        1.  관리 센터 (DSAC.exe) ADSIEDIT, PowerShell, Active Directory를 사용 하 여  
  
    2.  기존 계정에 이미 사용 SPN으로 채우려면  
  
        1.  Windows PowerShell, ADSIEDIT, 또는 SetSPN 사용  
  
4.  오류 확인  
  
**(선택 사항)**  
  
1.  있다는 수 있도록 강의 강의 확인는 * [광고 휴지통](https://technet.microsoft.com/library/jj574144.aspx#BKMK_EnableRecycleBin) * Active Directory 관리 센터에서 합니다.  경우에 다음 단계로 이동 합니다.  
  
2.  사용자 계정에서 UPN 채우려면  
  
3.  계정 삭제  
  
4.  다른 계정을 삭제 된 계정으로 동일한 UPN으로 채우려면  
  
5.  계정을 복구 하는 Recycle Bin GUI 사용 하려고  
  
6.  이전 단계에서 표시 오류와 함께 제공 하기만 하면 가정 합니다.  (와 방금 수행한 단계의 역사 없는) 계정 복원이 완료이 목표가입니다.  통합 예를 들어 단계를 참조 하십시오.  
  


