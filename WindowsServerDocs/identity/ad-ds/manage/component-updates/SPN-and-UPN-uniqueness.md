---
ms.assetid: 40bc24b1-2e7d-4e77-bd0f-794743250888
title: SPN 및 UPN 고유성
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c9a769fdd9fb7d13c47da465b25bc59e7f55237f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856744"
---
# <a name="spn-and-upn-uniqueness"></a>SPN 및 UPN 고유성

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**작성자**: Windows 그룹과 Justin Turner, 수석 지원 에스컬레이션 엔지니어  
  
> [!NOTE]  
> 이 콘텐츠는 Microsoft 고객 지원 엔지니어에 의해 작성되었으며 Windows Server 2012 R2의 기능 및 솔루션에 대해 TechNet에서 일반적으로 제공하는 항목보다 더 자세한 기술적 설명을 찾고 있는 숙련된 관리자 및 시스템 설계자를 대상으로 합니다. 그러나 동일한 편집 과정을 수행하지 않았으므로 일부 언어는 일반적으로 TechNet에서 찾을 수 있는 것보다 완벽하지 않을 수 있습니다.  
  
## <a name="overview"></a>개요  
Windows Server 2012 R2 블록 만들기를 실행 하는 도메인 컨트롤러에 서비스 사용자 이름 (SPN) 및 사용자 이름 (UPN) 중복 되었습니다. 복원 또는 개체의 이름 바꾸기 또는 삭제 된 개체의 애니메이션 결과적으로 복제 하는 경우이 포함 됩니다.  
  
### <a name="background"></a>배경  
중복 이름 SPN (서비스 사용자) 일반적으로 발생 하 고 인증 오류가 발생 하 고 LSASS CPU 사용률이 과도 한 발생할 수 있습니다. 추가 중복 된 SPN 또는 UPN을 차단 하도록 기본 메서드가 없습니다. *  
  
중복 된 UPN 값 온-프레미스 간 동기화를 중단 AD 및 Office 365입니다.  
  
*Setspn.exe는 일반적으로 새 Spn을 만드는 데 사용 되 고 기능이 중복 검사를 추가 하는 Windows Server 2008과 함께 출시 된 버전으로 빌드된 합니다.  
  
**테이블 SEQ 테이블 \\ \* 아랍어 1: SPN 및 UPN 고유성**  
  
|기능|설명|  
|-----------|-----------|  
|UPN 고유성|중복 된 Upn 나누기 동기화 온-프레미스 AD 계정 Office 365와 같은 Windows Azure AD 기반 서비스.|  
|SPN 고유성|Kerberos 상호 인증에 대 한 Spn을 필요합니다.  중복 된 Spn 인증 오류가 발생 합니다.|  
  
Upn 및 Spn에 대 한 고유성 요구 사항에 대 한 자세한 내용은 참조 [고유성 제약 조건을](https://msdn.microsoft.com/library/dn392337.aspx)합니다.  
  
## <a name="symptoms"></a>증상  
오류 코드 8467 또는 8468 또는 16 진수, 기호 또는 해당 문자열 로그인 다양 한 화면에 나타나는 대화 상자 및 디렉터리 서비스 이벤트 로그에서 이벤트 ID 2974 합니다. 다음과 같은 경우에만 중복 된 UPN 또는 SPN를 만들려는 시도가 차단 됩니다.  
  
-   Windows Server 2012 R2 DC에 의해 처리 쓰기  
  
**테이블 SEQ 테이블 \\ \* 아랍어 2: SPN 및 UPN 고유성 오류 코드**  
  
|Decimal|Hex|바로 가기|문자열|  
|-----------|-------|------------|----------|  
|8467|21C 7|ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST|추가/수정에 제공 되는 SPN 값은 포리스트 전체에서 고유 하지는 작업이 실패 했습니다.|  
|8648|21C 8|ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST|추가/수정에 제공 되는 UPN 값은 포리스트 전체에서 고유 하지는 작업이 실패 했습니다.|  
  
## <a name="new-user-creation-fails-if-upn-is-not-unique"></a>UPN 고유 하지 않은 경우 새 사용자 만들기 실패  
  
### <a name="dsamsc"></a>DSA.msc  
선택한 사용자 로그온 이름이 이미이 엔터프라이즈에서 사용 중입니다. 다른 로그온 이름을 선택한 다음 다시 시도 하십시오.  
  
![SPN 및 UPN 고유성](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig01_DupUPN.gif)  
  
기존 계정을 수정 합니다.  
  
엔터프라이즈에서 지정 된 사용자 로그온 이름이 이미 있습니다. 접두사를 변경 하거나 다른 접미사 목록에서 선택 하 여 새 암호를 지정 합니다.  
  
![SPN 및 UPN 고유성](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig02_DupUPNMod.gif)  
  
### <a name="active-directory-administrative-center-dsacexe"></a>Active Directory 관리 센터 (DSAC.exe)  
이미 존재 하는 UPN 가진 Active Directory 관리 센터에 새 사용자를 만들면 다음과 같은 오류가 반환 됩니다.  
  
![SPN 및 UPN 고유성](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig03_DupUPNADAC.gif)  
  
**그림 SEQ 그림 \\ \* 중복 된 UPN으로 인해 새 사용자 만들기가 실패 하면 AD 관리 센터에 표시 되는 아랍어 1 오류**  
  
### <a name="event-2974-source-activedirectorydomainservice"></a>이벤트 2974 소스: ActiveDirectory_DomainService  
![SPN 및 UPN 고유성](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig04_Event2974.gif)  
  
**그림 SEQ 그림 \\ \* 8648 오류로 아랍어 2 이벤트 ID 2974**  
  
이벤트 2974 차단 된 값과 이미 해당 값을 포함 하는 10) (최대 하나 이상의 개체의 목록이 나열 합니다.  다음 그림에서는 해당 UPN 특성 값을 볼 수 있습니다 ***dhunt@blue.contoso.com*** 다른 4 개의 개체에 이미 있습니다.  Windows Server 2012 r 2의 새로운 기능 이므로, 혼합된 환경에서 중복 된 UPN 및 Spn 실수로 생성 하위 Dc 쓰기 시도 처리 하는 경우 계속 발생 합니다.  
  
![SPN 및 UPN 고유성](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig05_Event2974ShowAllDups.gif)  
  
**그림 SEQ 그림 \\ \* 중복 된 UPN을 포함 하는 모든 개체를 표시 하는 아랍어 3 이벤트 2974**  
  
> [!TIP]  
> 이벤트 ID 2974s에 정기적으로 검토 합니다.  
>   
> -   중복 된 UPN 또는 Spn을 만들려고 시도 식별  
> -   이미 중복 항목을 포함 하는 개체를 식별 합니다.  
  
8648 = "작업이 추가/수정에 제공 되는 UPN 값 포리스트 전체에서 고유 없기 때문에 실패 했습니다."  
  
### <a name="setspn"></a>SetSPN:  
Setspn.exe 사용 하는 경우 Windows Server 2008 출시 후에 기본 제공 중복 SPN 검색에는 **"-S"** 옵션입니다.  그러나 사용 하 여 중복 SPN 검색을 무시할 수는 **"-A"** 옵션입니다.  SetSPN-A 옵션으로 사용 하 여 Windows Server 2012 R2 DC를 대상으로 할 때 중복 된 SPN 만들기 차단 됩니다.  표시 되는 오류 메시지-S 옵션을 사용 하는 경우 표시 된 것 같습니다. "중복 작업을 중단 발견 SPN!"  
  
### <a name="adsiedit"></a>ADSIEDIT:  
  
```  
Operation failed. Error code: 0x21c8  
The operation failed because UPN value provided for addition/modification is not unique forest-wide.  
000021C8: AtrErr: DSID-03200BBA, #1: 0: 000021C8: DSID-03200BBA, problem 1005 (CONSTRAINT_ATT_TYPE), data 0, Att 90290 (userPrincipalName)  
```  
  
![SPN 및 UPN 고유성](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig06_ADSI21c8.gif)  
  
**그림 SEQ 그림 \\ \* 추가 중복 된 UPN이 차단 될 때 ADSIEdit에 표시 되는 아랍어 4 오류 메시지**  
  
### <a name="windows-powershell"></a>Windows PowerShell  
Windows Server 2012 R2:  
  
![SPN 및 UPN 고유성](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig07_SetADUser2012.gif)  
  
Windows Server 2012 R2 DC를 대상으로 하는 Server 2012에서 실행 PS:  
  
![SPN 및 UPN 고유성](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig08_SetADUser2012R2.gif)  
  
Windows Server 2012 R2 DC를 대상으로 하는 Windows Server 2012에서 실행 되 고 DSAC.exe:  
  
![SPN 및 UPN 고유성](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig09_UserCreateError.gif)  
  
**그림 SEQ 그림 \\ \* 아랍어 5 DSAC 사용자 만들기 오류에서 비-Windows Server 2012 R2 Windows Server 2012 R2 DC를 대상으로 하는 동안**  
  
![SPN 및 UPN 고유성](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig10_UserModError.gif)  
  
**그림 SEQ 그림 \\ \* 아랍어 6 DSAC 사용자 수정 오류에서 비-Windows Server 2012 R2 Windows Server 2012 R2 DC를 대상으로 하는 동안**  
  
### <a name="restore-of-an-object-that-would-result-in-a-duplicate-upn-fails"></a>중복 된 UPN을 초래 하는 개체의 복원에 실패 합니다.  
![SPN 및 UPN 고유성](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig11_RestoreDupUPN.gif)  
  
![SPN 및 UPN 고유성](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig12_RestoreDupUPNError.gif)  
  
이벤트가 기록 되지 않음 개체 중복 된 UPN으로 인해 복원 하지 못할 때 / SPN입니다.  
  
개체의 UPN 복원 하기 위해에서 고유 해야 합니다.  
  
1.  휴지통에 있는 개체에 존재 하는 UPN을 식별 합니다.  
  
2.  동일한 값을 가진 모든 개체를 식별 합니다.  
  
3.  중복 UPN(s) 제거  
  
### <a name="identify-the-conflicting-upn-on-the-deleted-objectusing-repadminexe"></a>삭제 된 objectUsing repadmin.exe에서 충돌 하는 UPN을 식별 합니다.  
  
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
  
### <a name="to-identify-all-objects-with-the-same-upnusing-repadminexe"></a>동일한 UPN을 가진 모든 개체를 식별 하려면: Repadmin.exe를 사용 하 여  
  
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
> 이전에 문서화 되지 않은 **삭제 /** repadmin.exe에 매개 변수는 결과 집합에서 삭제 된 개체를 포함 하는 데  
  
### <a name="using-global-search"></a>전체 검색을 사용 하 여  
  
-   Active Directory 관리 센터 열기로 이동 하 고 **전체 검색**  
  
-   선택 된 **LDAP로 변환** 라디오 단추  
  
-   형식 **(userPrincipalName =*ConflictingUPN*)**  
  
    -   대체 ***ConflictingUPN*** 충돌 하는 실제 UPN을 가진  
  
-   선택 **적용**  
  
![SPN 및 UPN 고유성](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig13_GlobalSearch.gif)  
  
### <a name="using-windows-powershell"></a>Windows PowerShell 사용  
  
```  
Get-ADObject -LdapFilter "(userPrincipalName=dhunt@blue.contoso.com)" -IncludeDeletedObjects -SearchBase "DC=blue,DC=Contoso,DC=com" -SearchScope Subtree -Server winbluedc1.blue.contoso.com  
```  
  
![SPN 및 UPN 고유성](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig13_GlobalSearchPS.gif)  
  
개체를 복원 해야 하는 경우 하면 다른 개체에서 중복 된 Upn을 제거 하 고 필요한 됩니다.  하나의 개체에 대 한 간단 충분히를 사용 하 여 ADSIEdit에 중복을 제거 합니다.  중복 항목을 여러 개체가 있는 경우 Windows PowerShell 사용 하 여 더 나은 도구를 수 있습니다.  
  
Windows PowerShell을 사용 하 여 UserPrincipalName 특성 null로 설정 합니다.  
  
![SPN 및 UPN 고유성](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig15_NullUPN.gif)  
  
> [!NOTE]  
> UserPrincipalName 특성 단일 값 특성 이므로이 절차에는 중복 된 UPN만 제거 됩니다.  
  
### <a name="duplicate-spn"></a>중복 된 SPN  
![SPN 및 UPN 고유성](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig16_DupSPN.gif)  
  
**그림 SEQ 그림 \\ \* 중복 된 SPN 추가 차단 되었을 때 ADSIEdit에 표시 되는 아랍어 8 오류 메시지**  
  
디렉터리 서비스 이벤트 로그는 로그는 **ActiveDirectory_DomainService** 이벤트 ID **2974**합니다.  
  
```  
Operation failed. Error code: 0x21c7  
The operation failed   
The attribute value provided is not unique in the forest or partition. Attribute:  
servicePrincipalName Value=<SPN>  
<Object DN> Winerror: 8467  
```  
  
![SPN 및 UPN 고유성](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig17_DupSPN2974.gif)  
  
**그림 SEQ 그림 \\ \* 아랍어 9 오류 중복 된 SPN 만들기 차단 되었을 때를 기록 합니다.**  
  
### <a name="workflow"></a>워크플로  
  
-   **If DC == GC**  
  
    -   Offbox 호출 되지 않고 필요한 쿼리는 로컬로 충족 시킬 수 있습니다.  
  
    -   ***UPN의 경우***  
  
        -   제공 된 UPN에 대 한 쿼리 로컬 포리스트 UPN 인덱스 (*userPrincipalName; 전역 인덱스*)  
  
            -   항목을 반환 하는 경우 = = 0-쓰기 진행 >  
  
            -   항목을 반환 하는 경우! = 0에 쓰기 실패->  
  
                -   이벤트 기록  
  
                -   또한 확장 된 오류를 반환합니다.  
  
                    -   **8648:**  
  
                        *ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST*  
  
    -   ***SPN 사례***  
  
        -   제공 된 SPN에 대 한 쿼리 로컬 포리스트 SPN 인덱스 (*servicePrincipalName; 전역 인덱스*)  
  
            -   항목을 반환 하는 경우 = = 0-쓰기 진행 >  
  
            -   항목을 반환 하는 경우! = 0에 쓰기 실패->  
  
                -   이벤트 기록  
  
                -   또한 확장 된 오류를 반환합니다.  
  
                    -   **8647:**  
  
                        **ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST**  
  
-   **If DC != GC**  
  
    -   Offbox 호출 **바람직한** 있지만 중요 하지, 즉,이 최상의 고유성 검사  
  
        -   GC를 찾을 수 없는 경우에 로컬 DIT에 대 한 진행 되는 확인  
  
        -   이벤트를 나타내는 등 기록  
  
    -   ***UPN의 경우***  
  
        -   가장 가까운 GC에 대 한 LDAP 쿼리를 제출? 제공 된 UPN에 대 한 쿼리 GC의 포리스트 전체 UPN 인덱스 (*userPrincipalName; 전역 인덱스*)  
  
            -   항목을 반환 하는 경우 = = 0-쓰기 진행 >  
  
            -   항목을 반환 하는 경우! = 0에 쓰기 실패->  
  
                -   이벤트 기록  
  
                -   또한 확장 된 오류를 반환합니다.  
  
                    -   **8648:**  
  
                        *ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST*  
  
    -   ***SPN 사례***  
  
        -   가장 가까운 GC에 대 한 LDAP 쿼리를 제출? 제공 된 SPN에 대 한 쿼리 GC의 포리스트 전체 SPN 인덱스 (*servicePrincipalName; 전역 인덱스*)  
  
            -   항목을 반환 하는 경우 = = 0-쓰기 진행 >  
  
            -   항목을 반환 하는 경우! = 0에 쓰기 실패->  
  
                -   이벤트 기록  
  
                -   또한 확장 된 오류를 반환합니다.  
  
                    -   **8647:**  
  
                        *ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST*  
  
삭제 된 개체 다시 애니메이션을 SPN 또는 UPN 값이 나타나는 고유성 확인 됩니다. 중복이 발견 되 면 요청이 실패 합니다.  
  
-   DNS 호스트 이름, SAM 계정 이름 등과 같은 특정 특성 변경에 대 한 수정 될 때 Spn 적절히 업데이트 됩니다. 프로세스에서 사용 되지 않는 Spn 삭제 되 고 새 Spn 생성 하 고 데이터베이스에 추가 됩니다. 이 경로 트리거됩니다 기준이 필수 특성 수정 됩니다.  
  
    -   ATT_DNS_HOST_NAME  
  
    -   ATT_MS_DS_ADDITIONAL_DNS_HOST_NAME  
  
    -   ATT_SAM_ACCOUNT_NAME  
  
    -   ATT_MS_DS_ADDITIONAL_SAM_ACCOUNT_NAME  
  
    -   ATT_SERVER_REFERENCE_BL  
  
    -   ATT_USER_ACCOUNT_CONTROL  
  
새 SPN 값 중 하나는 중복 하면 수정을 실패 합니다. 위의 목록에서의 중요 한 특성은 ATT_DNS_HOST_NAME (컴퓨터 이름) 및 ATT_SAM_ACCOUNT_NAME (SAM 계정 이름)입니다.  
  
### <a name="try-this-exploring-spn-and-upn-uniqueness"></a>다음과 같이 해보십시오. SPN 및 UPN 고유성을 탐색  
이 여러 가지 방법 중 첫 번째 "**이 작업을 수행할**" 모듈에는 활동입니다.  이 모듈에 대 한 별도 랩 가이드가 않습니다.  **이** 활동은 랩 환경에서 학습 자료를 탐색할 수 있는 자유 형식의 활동 기본적으로 합니다.  다음 프롬프트 또는 스크립트의 옵션 있고 고유한 활동을 제공 합니다.  
  
> [!NOTE]  
> -   이 여러 가지 방법 중 첫 번째 "**이**" 활동입니다.  
> -   이 모듈에 대 한 별도 랩 가이드가 않습니다.  
> -   **이** 활동은 랩 환경에서 학습 자료를 탐색할 수 있는 자유 형식의 활동 기본적으로 합니다.  
> -   다음 프롬프트 또는 스크립트의 옵션 있고 고유한 활동을 제공 합니다.  
> -   반면 일부 섹션은 **이 작업을 수행할** 프롬프트 있습니다는 여전히 적절 한 랩에서 단원 내용을 탐색 하는 것이 좋습니다.  
  
SPN 및 UPN 고유성 시험해 보십시오.  다음 화면의이 지시에 따라 또는 사용자 고유의 완료 합니다.  
  
1.  UPN을 가진 새 사용자 만들기  
  
2.  Spn으로 계정을 만들으십시오  
  
3.  이전에 이미 정의 된 UPN을 가진 새 사용자 만들기 또는 기존 계정의 UPN을 변경 합니다.  다른 계정에 SPN에 대해 동일한 작업을 수행합니다  
  
    1.  이미 사용 중인 UPN 가진 기존 사용자 계정을 채웁니다.  
  
        1.  PowerShell, ADSIEDIT, 또는 Active Directory 관리 센터 (DSAC.exe)를 사용 하 여  
  
    2.  이미 사용 중인 SPN과 기존 계정을 채웁니다.  
  
        1.  Windows를 사용 하 여 PowerShell, ADSIEDIT, 또는 SetSPN  
  
4.  오류를 확인 합니다.  
  
**필요에 따라**  
  
1.  있다는 사용 하도록 설정 하는 강사로 확인은 *[AD 휴지통](https://technet.microsoft.com/library/jj574144.aspx#BKMK_EnableRecycleBin)* Active Directory 관리 센터에 있습니다.  그럴 경우 다음 단계로 이동 합니다.  
  
2.  사용자 계정에 UPN을 채웁니다  
  
3.  계정 삭제  
  
4.  삭제 된 계정으로 동일한 UPN 가진 다른 계정을 채웁니다.  
  
5.  사용 하는 재활용 Bin GUI 계정을 복원 하십시오.  
  
6.  이전 단계에서 참조 하는 오류와 함께 표시 방금 있습니다 가정해 보겠습니다.  (및 방금 수행한 단계에 대 한 기록이 없는) 목표는 계정의 복원을 완료 하는 것입니다.  예를 들어 단계를 통합 문서를 참조 하십시오.  
  


