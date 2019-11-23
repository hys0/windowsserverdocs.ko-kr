---
ms.assetid: 8738c03d-6ae8-49a7-8b0c-bef7eab81057
title: 중앙 액세스 정책 배포(시연 단계)
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 09b7edcd843dfe65d7e2391612f029cf18b633ec
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357502"
---
# <a name="deploy-a-central-access-policy-demonstration-steps"></a>중앙 액세스 정책 배포(시연 단계)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 시나리오에서는 재무 부서 보안 운영 팀이 중앙 정보 보안 팀과 함께 파일 서버에 저장되어 있는 보관된 재무 정보를 보호하기 위해 중앙 액세스 정책의 필요성을 지정하는 단계에 대해 설명합니다. 각 국가의 보관된 재무 정보에는 해당 국가의 재무 직원이 읽기 전용으로 액세스할 수 있습니다. 중앙 재무 관리자 그룹은 모든 국가의 재무 정보에 액세스할 수 있습니다.  

중앙 액세스 정책 배포는 다음 단계로 구성됩니다.  

|단계|설명  
|---------|---------------  
|[계획: 정책에 대 한 필요성 및 배포에 필요한 구성을 확인 합니다.](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md#BKMK_1.2)|정책의 필요성 및 배포에 필요한 구성 확인 
|[구현: 구성 요소 및 정책 구성](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md#BKMK_1.3)|구성 요소 및 정책 구성  
|[중앙 액세스 정책 배포](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md#BKMK_1.4)|정책을 배포합니다.  
|[유지 관리: 정책 변경 및 준비](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md#BKMK_1.5)|정책 변경 및 준비 합니다. 

## <a name="BKMK_1.1"></a>테스트 환경 설정  
시작하기 전에 이 시나리오를 테스트할 랩을 설정해야 합니다. 랩 설정에 대 한 단계에서 자세히 설명 되어 [부록 b: the 테스트 환경 설정을](Appendix-B--Setting-Up-the-Test-Environment.md)합니다.  

## <a name="BKMK_1.2"></a>계획: 정책에 대 한 필요성 및 배포에 필요한 구성을 확인 합니다.  
이 섹션에서는 배포의 계획 단계에 도움이 되는 개략적인 단계를 제공합니다.  

||단계|예|  
|-|--------|-----------|  
|1.1|회사에서 중앙 액세스 정책이 필요한 것으로 결정|파일 서버에 저장된 재무 정보를 보호하기 위해 재무 부서 보안 운영 팀은 중앙 정보 보안 팀과 함께 중앙 액세스 정책의 필요성을 지정합니다.|  
|1.2|액세스 정책 표현|재무 문서는 재무 부서의 구성원만 볼 수 있어야 합니다. 재무 부서의 구성원은 해당 국가의 문서에만 액세스해야 합니다. 재무 관리자만 쓰기 권한이 있어야 합니다. FinanceException 그룹의 구성원에게는 예외가 허용됩니다. 이 그룹에는 읽기 권한이 부여됩니다.|  
|1.3|Windows Server 2012 구문으로 액세스 정책 표현|대상:<br /><br />-Resource.Department 재무를 포함합니다.<br /><br />액세스 규칙:<br /><br />-허용 읽기 User.Country=Resource.Country AND User.department = Resource.Department<br />--모든 권한 User.MemberOf(FinanceAdmin)를 허용 하는 중<br /><br />예외:<br /><br />Allow read memberOf(FinanceException)|  
|1.4|정책에 필요한 파일 속성 결정|파일에 지정할 태그:<br /><br />-부서<br />-국가|  
|1.5|정책에 필요한 클레임 유형 및 그룹 결정|클레임 유형:<br /><br />-국가<br />-부서<br /><br />사용자 그룹:<br /><br />-FinanceAdmin<br />-FinanceException|  
|1.6|이 정책을 적용할 서버 결정|모든 재무 파일 서버에 정책을 적용합니다.|  

## <a name="BKMK_1.3"></a>구현: 구성 요소 및 정책 구성  
이 섹션에서는 재무 문서에 대한 중앙 액세스 정책을 배포하는 예제를 제공합니다.  

|아니요|단계|예|  
|------|--------|-----------|  
|2.1|클레임 유형 만들기|다음 클레임 유형을 만듭니다.<br /><br />-부서<br />-국가|  
|2.2|리소스 속성 만들기|다음 리소스 속성을 만들고 사용하도록 설정합니다.<br /><br />-부서<br />-국가|  
|2.3|중앙 액세스 규칙 구성|이전 섹션에서 결정한 정책이 포함된 Finance Documents 규칙을 만듭니다.|  
|2.4|CAP(중앙 액세스 규칙) 구성|재무 정책이라는 CAP를 만들고 이 CAP에 Finance Documents 규칙을 추가합니다.|  
|2.5|중앙 액세스 정책의 대상으로 파일 서버로 지정|파일 서버에 재무 정책 CAP를 게시합니다.|  
|2.6|클레임, 복합 인증 및 Kerberos 아머링(armoring)에 대한 KDC 지원 설정|contoso.com에 대해 클레임, 복합 인증 및 Kerberos 아머링(armoring)에 대한 KDC 지원을 설정합니다.|  

다음 절차에서는 두 개의 클레임 형식 만들게: 국가 및 부서입니다.  

#### <a name="to-create-claim-types"></a>클레임 유형을 만들려면  

1. Hyper-v 관리자에서 DC1 서버를 열고 <strong>pass@word1</strong>암호를 사용 하 여 contoso\administrator로 로그온 합니다.  

2. Active Directory 관리 센터를 엽니다.  

3. 클릭는 **트리 뷰 아이콘**, 확장 **동적 액세스 제어**, 를 선택한 다음 **클레임 유형은**합니다.  

   마우스 오른쪽 단추로 클릭 **클레임 유형**, 클릭 **새로**, 를 클릭 하 고 **클레임 유형**합니다.  

   > [!TIP]  
   > 열 수도 있습니다는 **클레임 유형 만들기:** 에서 창 고 **작업** 창. **작업** 창에서 **새로 만들기**를 클릭한 다음 **클레임 유형**을 클릭합니다.  

4. 에 **원본 특성** 목록 특성 목록의 아래로 스크롤하여을 클릭 하 여 **부서**합니다. 그러면 **표시 이름** 필드가 **부서**로 채워집니다. **확인**을 클릭합니다.  

5. **작업** 창에서 **새로 만들기**를 클릭한 다음 **클레임 유형**을 클릭합니다.  

6. **원본 특성** 목록에서 특성 목록의 아래로 스크롤하여 **c** 특성(국가-이름)을 클릭합니다. 에 **표시 이름** 필드를 입력 **국가**합니다.  

7. 에 **제안 값** 섹션에서 **다음 값이 제안 됨:** , 를 클릭 하 고 **추가**.  

8. 에 **값** 및 **표시 이름** 필드, 형식 **미국**, 를 클릭 하 고 **확인**합니다.  

9. 위 단계를 반복합니다. **제안 값 추가** 대화 상자에서 **값** 및 **표시 이름** 필드에 **JP**를 입력하고 **확인**을 클릭합니다.  

![솔루션 가이드](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em>***  

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  


    New-ADClaimType country -SourceAttribute c -SuggestedValues:@((New-Object Microsoft.ActiveDirectory.Management.ADSuggestedValueEntry("US","US","")), (New-Object Microsoft.ActiveDirectory.Management.ADSuggestedValueEntry("JP","JP","")))  
    New-ADClaimType department -SourceAttribute department  



> [!TIP]  
> Active Directory 관리 센터의 Windows PowerShell 기록 뷰어를 사용하여 Active Directory 관리 센터에서 수행하는 각 작업에 대한 Windows PowerShell cmdlet을 조회할 수 있습니다. 자세한 내용은 참조 [Windows PowerShell 기록 뷰어](https://technet.microsoft.com/library/hh831702)  

다음 단계에서는 리소스 속성을 만듭니다. 아래 절차에 따라 파일 서버에서 사용할 수 있도록 도메인 컨트롤러의 전역 리소스 속성 목록에 자동으로 추가되는 리소스 속성을 만들 수 있습니다.  

#### <a name="to-create-and-enable-pre-created-resource-properties"></a>리소스 속성을 만들고 미리 만든 리소스 속성을 사용하려면  

1.  Active Directory 관리 센터의 왼쪽 창에서 **트리 보기**를 클릭합니다. 확장 **동적 액세스 제어**, 를 선택한 다음 **리소스 속성**합니다.  

2.  **리소스 속성**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **참조 리소스 속성**을 클릭합니다.  

    > [!TIP]  
    > 리소스 속성을 선택할 수도 있습니다는 **작업** 창입니다. 클릭 **새로** 클릭 하 고 **참조 리소스 속성**합니다.  

3.  **제안 값을 공유하려면 클레임 유형을 선택합니다.** 목록에서 **국가**를 클릭합니다.  

4.  **표시 이름** 필드에 **국가**를 입력하고 **확인**을 클릭합니다.  

5.  **리소스 속성** 목록을 두 번 클릭하고 아래의 **부서** 리소스 속성으로 이동합니다. 마우스 오른쪽 단추를 클릭 한 다음 **사용**합니다. 이렇게 하면 기본 제공 **부서** 리소스 속성입니다.  

6.  에 **리소스 속성** 목록 Active Directory 관리 센터 탐색 창에서 지금 할 두 가지 사용 가능한 리소스 속성:  

    -   Country  

    -   부서  

![솔루션 가이드](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em>***  

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  

```  
New-ADResourceProperty Country -IsSecured $true -ResourcePropertyValueType MS-DS-MultivaluedChoice -SharesValuesWith country  
Set-ADResourceProperty Department_MS -Enabled $true  
Add-ADResourcePropertyListMember "Global Resource Property List" -Members Country  
Add-ADResourcePropertyListMember "Global Resource Property List" -Members Department_MS  

```  

다음 단계에서는 리소스에 액세스할 수 있는 사람을 정의하는 중앙 액세스 규칙을 만듭니다. 이 시나리오의 비즈니스 규칙은 다음과 같습니다.  

-   재무 문서는 재무 부서의 구성원만 볼 수 있습니다.  

-   재무 부서의 구성원은 해당 국가의 문서에만 액세스할 수 있습니다.  

-   재무 관리자만 쓰기 권한을 가질 수 있습니다.  

-   FinanceException 그룹의 구성원에게는 예외가 허용됩니다. 이 그룹에는 읽기 권한이 부여됩니다.  

-   관리자와 문서 소유자는 여전히 모든 권한을 가집니다.  

또는 Windows Server 2012 구문으로 규칙을 표현 합니다.  

재무 포함 되어 Resource.Department 목표 설정:  

액세스 규칙:  

-   Allow read User.Country=Resource.Country AND User.department = Resource.Department  

-   Allow Full control User.MemberOf(FinanceAdmin)  

-   Allow Read User.MemberOf(FinanceException)  

#### <a name="to-create-a-central-access-rule"></a>중앙 액세스 규칙을 만들려면  

1. Active Directory 관리 센터의 왼쪽 창에서 **트리 보기**를 클릭하고 **동적 Access Control**을 선택한 다음 **중앙 액세스 규칙**을 클릭합니다.  

2. 마우스 오른쪽 단추로 클릭 **중앙 액세스 규칙**, 클릭 **새로**, 를 클릭 하 고 **중앙 액세스 규칙**합니다.  

3. **이름** 필드에 **Finance Documents 규칙**을 입력합니다.  

4. **대상 리소스** 섹션에서 **편집**을 클릭하고 **중앙 액세스 규칙** 대화 상자에서 **조건 추가**를 클릭합니다. 그런 다음   
   [**리소스**] [**부서**] [**Equals**] [**값**] [**재무**]를 클릭 하 고 **확인**합니다.  

5. **사용 권한** 섹션에서 **다음 권한을 현재 권한으로 사용**을 선택하고 **편집**을 클릭한 다음 **사용 권한 고급 보안 설정** 대화 상자에서 **추가**를 클릭합니다.  

   > [!NOTE]  
   > **다음 권한을 임시 권한으로 사용 하 여** 옵션 준비에는 정책을 만들 수 있습니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 유지 관리를 참조 하십시오: 변경 및 스테이지 정책 섹션을이 참조 합니다.  

6. 에 **사용 권한 권한 항목** 대화 상자, 클릭 **보안 주체 선택**, 형식 **Authenticated Users**, 클릭 하 고 **확인**합니다.  

7. **사용 권한 권한 항목** 대화 상자에서 **조건 추가**를 클릭하고   
   [**사용자**] [**국가**] [**의**] [**리소스**] [**국가**]   
    클릭 **조건 추가**합니다.   
    [**And**]   
   클릭 하 여 [**사용자**] [**부서**] [**의**] [**리소스**] [**부서**]. 설정의 **권한을** 에 **읽기**합니다.  

8. 클릭 **확인**, 를 클릭 하 고 **추가**합니다. 클릭 **보안 주체 선택**, 형식 **FinanceAdmin**, 를 클릭 하 고 **확인**합니다.  

9. **수정, 읽기 및 실행, 읽기, 쓰기** 권한을 선택하고 **확인**을 클릭합니다.  

10. **추가**를 클릭하고 **보안 주체 선택**을 클릭한 다음 **FinanceException**을 입력하고 **확인**을 클릭합니다. 되도록 사용 권한을 선택 **읽기** 및 **읽기 및 실행**합니다.  

11. **확인** 을 세 번 클릭하여 작업을 마치고 Active Directory 관리 센터로 돌아갑니다.  

    ![솔루션 가이드](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em>***  

    다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  


~~~
$countryClaimType = Get-ADClaimType country  
$departmentClaimType = Get-ADClaimType department  
$countryResourceProperty = Get-ADResourceProperty Country  
$departmentResourceProperty = Get-ADResourceProperty Department  
$currentAcl = "O:SYG:SYD:AR(A;;FA;;;OW)(A;;FA;;;BA)(A;;0x1200a9;;;S-1-5-21-1787166779-1215870801-2157059049-1113)(A;;0x1301bf;;;S-1-5-21-1787166779-1215870801-2157059049-1112)(A;;FA;;;SY)(XA;;0x1200a9;;;AU;((@USER." + $countryClaimType.Name + " Any_of @RESOURCE." + $countryResourceProperty.Name + ") && (@USER." + $departmentClaimType.Name + " Any_of @RESOURCE." + $departmentResourceProperty.Name + ")))"  
$resourceCondition = "(@RESOURCE." + $departmentResourceProperty.Name + " Contains {`"Finance`"})"  
New-ADCentralAccessRule "Finance Documents Rule" -CurrentAcl $currentAcl -ResourceCondition $resourceCondition  
~~~


> [!IMPORTANT]  
> 위 예제 cmdlet에서 FinanceAdmin 그룹과 사용자의 SID(보안 식별자)는 만들 당시에 정해지므로 실제 예에서는 이와 다릅니다. 예를 들어 FinanceAdmins에 제공된 SID 값 (S-1-5-21-1787166779-1215870801-2157059049-1113)을 실제 배포에서 만들어야 하는 FinanceAdmin 그룹의 실제 SID로 바꿔야 합니다. 이 그룹의 SID 값을 조회를 해당 값을 변수에 할당 한 다음 변수를 여기서 사용 하려면 Windows PowerShell을 사용할 수 있습니다. 자세한 내용은 참조 [Windows PowerShell 팁: Sid](https://go.microsoft.com/fwlink/?LinkId=253545)합니다.  

이제 사용자가 동일한 국가와 동일한 부서의 문서에 액세스할 수 있는 중앙 액세스 규칙이 만들어졌습니다. 이 규칙은 FinanceAdmin 그룹에서 문서를 편집할 수 있도록 허용하고, FinanceException 그룹에서 문서를 읽을 수 있도록 허용합니다. 이 규칙은 재무로 분류된 문서에만 적용됩니다.  

#### <a name="to-add-a-central-access-rule-to-a-central-access-policy"></a>중앙 액세스 정책에 중앙 액세스 규칙을 추가하려면  

1. Active Directory 관리 센터의 왼쪽 창에서 **동적 Access Control**을 클릭한 다음 **중앙 액세스 정책**을 클릭합니다.  

2. **작업** 창에서 **새로 만들기**를 클릭한 다음 **중앙 액세스 정책**을 클릭합니다.  

3. **중앙 액세스 정책 만들기:** , 형식 **재무 정책** 에 **이름** 상자입니다.  

4. **구성원 중앙 액세스 규칙**에서 **추가**를 클릭합니다.  

5. 두 번 클릭 하는 **Finance Documents 규칙** 추가 하는 **다음 중앙 액세스 규칙을 추가** 목록을 연 다음 클릭 **확인**.  

6. **확인**을 클릭하여 작업을 마칩니다. 이제 재무 정책이라는 중앙 액세스 정책이 만들어졌습니다.  

   ![솔루션 가이드](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em>***  

   다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  

   ```  
   New-ADCentralAccessPolicy "Finance Policy" Add-ADCentralAccessPolicyMember   
   -Identity "Finance Policy"   
   -Member "Finance Documents Rule"  

   ```  

#### <a name="to-apply-the-central-access-policy-across-file-servers-by-using-group-policy"></a>그룹 정책을 사용하여 파일 서버에서 중앙 액세스 정책을 적용하려면  

1.  **시작** 화면의 **검색** 상자에 **그룹 정책 관리**를 입력합니다. **그룹 정책 관리**를 두 번 클릭합니다.  

    > [!TIP]  
    > **PC 관리 도구 표시** 설정이 사용되지 않도록 설정된 경우 **관리 도구** 폴더 및 해당 콘텐츠가 **설정** 결과에 표시되지 않습니다.  

    > [!TIP]  
    > 프로덕션 환경에서는 파일 서버 OU(조직 단위)를 만들고 이 OU에 이 정책을 적용할 모든 파일 서버를 추가해야 합니다. 그런 다음 그룹 정책을 만들고 해당 정책에 이 OU를 추가할 수 있습니다.  

2.  이 단계에서는 방금 만든 중앙 액세스 정책을 포함하기 위해 테스트 환경의 [도메인 컨트롤러 빌드](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_Build) 섹션에서 만든 그룹 정책 개체를 편집합니다. 그룹 정책 관리 편집기에서 탐색 하 고 (이 예에서는 contoso.com) 도메인에 조직 구성 단위를 선택 합니다.: **그룹 정책 관리**, **포리스트: contoso.com**, **도메인**, **contoso.com**, **Contoso**, **FileServerOU**합니다.  

3.  마우스 오른쪽 단추로 클릭 **FlexibleAccessGPO**, 를 클릭 하 고 **편집**합니다.  

4.  그룹 정책 관리 편집기 창에서 **컴퓨터 구성**으로 이동하여 **정책**, **Windows 설정**을 차례로 확장한 다음 **보안 설정**을 클릭합니다.  

5.  **파일 시스템**을 확장하고 **중앙 액세스 정책**을 마우스 오른쪽 단추로 클릭한 다음 **중앙 액세스 정책 관리**를 클릭합니다.  

6.  **중앙 액세스 정책 구성** 대화 상자에서 **재무 정책**을 추가하고 **확인**을 클릭합니다.  

7.  아래로 스크롤하여 **고급 감사 정책 구성**, 를 확장 합니다.  

8.  확장 **감사 정책을**, 를 선택 하 고 **개체 액세스**합니다.  

9. 두 번 클릭 **중앙 액세스 정책 준비 감사**합니다. 세 개의 모든 확인란을 선택한 다음 클릭 **확인**합니다. 이 단계를 수행하면 시스템에서 중앙 액세스 준비 정책과 관련된 감사 이벤트를 받을 수 있습니다.  

10. **파일 시스템 속성 감사**를 두 번 클릭합니다. 세 개의 모든 확인란을 선택한 다음 클릭 **확인**합니다.  

11. 그룹 정책 관리 편집기를 닫습니다. 이제 그룹 정책에 중앙 액세스 정책이 포함되었습니다.  

클레임 또는 장치 권한 부여 데이터를 제공 하는 도메인의 도메인 컨트롤러에 대 한 도메인 컨트롤러가 동적 액세스 제어를 지원 하도록 구성 해야 합니다.  

#### <a name="to-enable-support-for-claims-and-compound-authentication-for-contosocom"></a>contoso.com에 대해 클레임 및 복합 인증을 지원하려면  

1.  그룹 정책 관리를 열고 **contoso.com**을 클릭한 다음 **도메인 컨트롤러**를 클릭합니다.  

2.  **기본 도메인 컨트롤러 정책**을 마우스 오른쪽 단추로 클릭한 후 **편집**을 클릭합니다.  

3.  그룹 정책 관리 편집기 창에서 **컴퓨터 구성**, **정책**, **관리 템플릿**, **시스템**, **KDC**를 차례로 두 번 클릭합니다.  

4.  두 번 클릭 **클레임에 대 한 KDC 지원 복합 인증 및 Kerberos 아머 링**합니다. **클레임, 복합 인증 및 Kerberos 아머링(armoring)에 대한 KDC 지원 설정** 대화 상자에서 **사용**을 클릭하고 **옵션** 드롭다운 목록에서 **지원됨**을 선택합니다. 중앙 액세스 정책에서 사용자 클레임을 사용하려면 이 설정을 지정해야 합니다.  

5.  **그룹 정책 관리**를 닫습니다.  

6.  명령 프롬프트를 열고 `gpupdate /force`를 입력합니다.  

## <a name="BKMK_1.4"></a>중앙 액세스 정책 배포  

||단계|예|  
|-|--------|-----------|  
|3.1|파일 서버의 적절한 공유 폴더에 CAP 할당|파일 서버의 적절한 공유 폴더에 중앙 액세스 정책을 할당합니다.|  
|3.2|액세스가 적절하게 구성되었는지 확인|다른 국가 및 부서의 사용자에 대한 액세스를 확인합니다.|  

이 단계에서는 파일 서버에 중앙 액세스 정책을 할당합니다. 이전 단계에서 만든 중앙 액세스 정책을 수신하는 파일 서버에 로그온하여 정책을 공유 폴더에 할당합니다.  

#### <a name="to-assign-a-central-access-policy-to-a-file-server"></a>파일 서버에 중앙 액세스 정책을 할당하려면  

1. Hyper-V 관리자에서 FILE1 서버에 연결합니다. Contoso\administrator <strong>pass@word1</strong>암호와 함께를 사용 하 여 서버에 로그온 합니다.  

2. 관리자 권한 명령 프롬프트를 열고 **gpupdate /force**를 입력합니다. 그러면 그룹 정책 변경 내용이 서버에 적용됩니다.  

3. 또한 Active Directory에서 전역 리소스 속성을 새로 고쳐야 합니다. 관리자 권한 Windows PowerShell 창을 열고 `Update-FSRMClassificationpropertyDefinition`을 입력합니다. Enter 키를 클릭하고 Windows PowerShell을 닫습니다.  

   > [!TIP]
   > 파일 서버에 로그온하여 전역 리소스 속성을 새로 고칠 수도 있습니다. 파일 서버에서 전역 리소스 속성을 새로 고치려면 다음을 수행합니다  
   > 
   > 1. 암호 <strong>pass@word1</strong>를 사용 하 여 Contoso\administrator로 파일 서버 FILE1에 로그온 합니다.  
   > 2. 파일 서버 리소스 관리자를 엽니다. 파일 서버 리소스 관리자를 열려면 **시작**을 클릭하고 **파일 서버 리소스 관리자**를 입력한 다음 **파일 서버 리소스 관리자**를 클릭합니다.  
   > 3. 파일 서버 리소스 관리자에서 클릭 **파일 분류 관리** , 를 마우스 오른쪽 단추로 클릭 **분류 속성** 클릭 하 고 **새로 고침**합니다.  

4. Windows 탐색기를 열고 왼쪽된 창에서 4. 마우스 오른쪽 단추로 클릭 하는 드라이브는 **재무 문서** 클릭 **속성**합니다.  

5. **분류** 탭을 클릭한 다음 **국가**를 클릭하고 **값** 필드에서 **US**를 선택합니다.  

6. 클릭 **부서**, 을 선택한 다음 **재무** 에 **값** 필드를 클릭 한 다음 **적용**합니다.  

   > [!NOTE]  
   > 중앙 액세스 정책은 재무 부서의 파일에 적용되도록 구성되었음을 기억해야 합니다. 위 단계를 수행하면 폴더의 모든 문서에 국가 및 부서 특성이 표시됩니다.  

7. 클릭 하 고 **보안** 탭을 클릭 한 후 **고급**합니다. **중앙 정책** 탭을 클릭합니다.  

8. **변경**을 클릭하고 드롭다운 메뉴에서 **재무 정책**을 선택한 다음 **적용**을 클릭합니다. 볼 수는 **Finance Documents 규칙** 는 정책에 나열 합니다. 항목을 확장하여 Active Directory에서 규칙을 만들 때 설정한 모든 사용 권한을 확인합니다.  

9. **확인**을 클릭하여 Windows 탐색기로 돌아갑니다.  

다음 단계에서는 액세스가 적절하게 구성되었는지 확인합니다.  사용자 계정에 적절한 부서 특성이 설정되어 있어야 합니다(Active Directory 관리 센터를 사용하여 설정). 새 정책의 적용 결과를 보려면 Windows 탐색기에서 **유효한 액세스** 탭을 사용하는 것이 가장 간단합니다. **유효한 액세스** 탭에 지정 된 사용자 계정에 대 한 액세스 권한을 표시 합니다.  

#### <a name="to-examine-the-access-for-various-users"></a>여러 사용자에 대한 액세스 권한을 확인하려면  

1.  Hyper-V 관리자에서 FILE1 서버에 연결합니다. contoso\administrator로 서버에 로그온합니다. Windows 탐색기에서 D:\로 이동합니다. 마우스 오른쪽 단추로 클릭는 **재무 문서** 폴더를 마우스 클릭 한 다음 **속성**합니다.  

2.  **보안** 탭, **고급**, **유효한 액세스** 탭을 차례로 클릭합니다.  

3.  사용자에 대 한 권한의 검사 하려면 클릭 **사용자 선택**, 사용자의 이름을 입력 하 고 클릭 한 다음  **유효한 액세스 보기** 유효한 액세스 권한을 볼 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  

    -   Myriam Delesalle(MDelesalle)은 재무 부서에 속해 있으므로 폴더에 대한 읽기 권한이 있어야 합니다.  

    -   Miles Reid(MReid)는 FinanceAdmin 그룹의 구성원이므로 폴더에 대한 수정 권한이 있어야 합니다.  

    -   Esther Valle(EValle)는 재무 부서에 속해 있지 않지만 FinanceException 그룹의 구성원이므로 읽기 권한이 있어야 합니다.  

    -   Maira Wenzel(MWenzel)은 재무 부서에 속해 있지 않고 FinanceAdmin 또는 FinanceException 그룹의 구성원도 아니므로 폴더에 대한 액세스 권한이 없어야 합니다.  

    유효한 액세스 창에 **액세스 제한 기준**이라는 마지막 열이 있습니다. 이 열은 주는 게이트 사용자의 권한에 영향을 알려 줍니다. 이 예제에서는 공유 및 NTFS 권한이 모든 사용자에게 모든 권한을 허용합니다. 그러나 중앙 액세스 정책이 이전에 구성한 규칙에 따라 액세스를 제한합니다.  

## <a name="BKMK_1.5"></a>유지 관리: 정책 변경 및 준비  

||||  
|-|-|-|  
|Number|단계|예|  
|4.1|클라이언트에 대한 장치 클레임 구성|장치 클레임을 사용하도록 그룹 정책 설정을 지정합니다.|  
|4.2|장치에 클레임 사용|장치에 국가 클레임 유형을 사용합니다.|  
|4.3|수정하려는 기존 중앙 액세스 규칙에 준비 정책 추가|Finance Documents 규칙을 수정하여 준비 정책을 추가합니다.|  
|4.4|준비 정책의 결과 보기|Ester Velle의 사용 권한을 확인 합니다.|  

#### <a name="to-set-up-group-policy-setting-to-enable-claims-for-devices"></a>장치에 클레임을 사용하도록 그룹 정책 설정을 지정하려면  

1.  DC1에 로그인하여 그룹 정책 관리를 열고 **contoso.com**, **기본 도메인 정책**을 차례로 클릭한 다음 마우스 오른쪽 단추를 클릭하고 **편집**을 선택합니다.  

2.  그룹 정책 관리 편집기 창에서 이동 **컴퓨터 구성**, **정책**, **관리 템플릿**, **시스템**, **Kerberos**합니다.  

3.  **클레임, 복합 인증 및 Kerberos 아머링(armoring)에 대한 Kerberos 클라이언트 지원**을 선택하고 **사용**을 클릭합니다.  

#### <a name="to-enable-a-claim-for-devices"></a>장치에 클레임을 사용하려면  

1. Hyper-v 관리자에서 DC1 서버를 열고 <strong>pass@word1</strong>암호를 사용 하 여 contoso\Administrator로 로그온 합니다.  

2. **도구** 메뉴에서 Active Directory 관리 센터를 엽니다.  

3. 클릭 **트리 뷰**, 확장 **동적 액세스 제어**, 를 두 번 클릭 **클레임 유형**, 두 번 클릭 하 고는 **국가** 클레임입니다.  

4. **이 유형의 클레임은 다음 클래스에 대해 발급할 수 있습니다.** 에서 **컴퓨터** 확인란을 선택합니다. **확인**을 클릭합니다.   
   모두는 **사용자** 및 **컴퓨터** 확인란 선택 됩니다. 이제 사용자 외에 장치에서도 국가 클레임을 사용할 수 있습니다.  

다음 단계에서는 준비 정책 규칙을 만듭니다. 준비 정책은 새 정책 항목을 사용하기 전에 그 효과를 모니터링하는 데 사용될 수 있습니다. 다음 단계에서는 준비 정책 항목을 만들고 공유 폴더에 대한 효과를 모니터링합니다.  

#### <a name="to-create-a-staging-policy-rule-and-add-it-to-the-central-access-policy"></a>준비 정책 규칙을 만들고 중앙 액세스 정책에 추가하려면  

1. Hyper-v 관리자에서 DC1 서버를 열고 <strong>pass@word1</strong>암호를 사용 하 여 contoso\Administrator로 로그온 합니다.  

2. Active Directory 관리 센터를 엽니다.  

3. 클릭 **트리 뷰**, 를 확장 하 고 **동적 액세스 제어**, 선택한 **중앙 액세스 규칙**합니다.  

4. **Finance Documents** 폴더를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  

5. **임시 권한** 섹션에서 **권한 준비 구성 사용** 확인란을 선택하고 **편집**을 클릭한 다음 **추가**를 클릭합니다. **임시 권한 권한 항목** 창에서 **보안 주체 선택** 링크를 클릭하고 **Authenticated Users**를 입력한 다음 **확인**을 클릭합니다.  

6. **조건 추가** 링크를 클릭하고   
    [**사용자**] [**국가**] [**의**] [**리소스**] [**국가**].  

7. **조건 추가** 링크를 다시 클릭하고  
   [**And**]   
    [**장치**] [**국가**] [**의**] [**리소스**] [**국가**]  

8. **조건 추가**를 다시 클릭하고  
   [및]   
    [**사용자**] [**그룹**] [**중 구성원**] [**값**]\(**FinanceException**)  

9. FinanceException을 설정 하려면 그룹에서 **항목 추가** 및는 **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 창, 형식 **FinanceException**합니다.  

10. **사용 권한**을 클릭하고 **모든 권한**을 선택한 다음 **확인**을 클릭합니다.  

11. 제안 된 사용 권한 창에 대 한 고급 보안 설정에서 선택 **FinanceException** 클릭 **제거**합니다.  

12. 클릭 **확인** 완료를 두 번입니다.  

![솔루션 가이드](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em>***  

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  

```  
Set-ADCentralAccessRule  
-Identity: "CN=FinanceDocumentsRule,CN=CentralAccessRules,CN=ClaimsConfiguration,CN=Configuration,DC=Contoso.com"  
-ProposedAcl: "O:SYG:SYD:AR(A;;FA;;;BA)(A;;FA;;;SY)(A;;0x1301bf;;;S-1-21=1426421603-1057776020-1604)"  
-Server: "WIN-2R92NN8VKFP.Contoso.com"  

```  

> [!NOTE]  
> 위 예제 cmdlet에서 Server 값은 테스트 랩 환경의 서버를 나타냅니다. Windows PowerShell 기록 뷰어를 사용하여 Active Directory 관리 센터에서 수행하는 각 작업에 대한 Windows PowerShell cmdlet을 조회할 수 있습니다. 자세한 내용은 참조 [Windows PowerShell 기록 뷰어](https://technet.microsoft.com/library/hh831702)  

이 임시 권한 집합에서 FinanceException 그룹의 구성원은 문서와 동일한 국가에서 장치를 통해 액세스한 경우 해당 국가의 파일에 대한 모든 권한을 가집니다. 재무 부서의 다른 구성원이 파일에 액세스하려고 한 경우 파일 서버 보안 로그에서 감사 항목을 확인할 수 있습니다. 그러나 정책이 준비 단계에서 승격될 때까지 보안 설정은 적용되지 않습니다.  

다음 절차에서는 준비 정책의 결과를 확인합니다. 현재 규칙에 따라 권한이 있는 사용자 이름으로 공유 폴더에 액세스합니다. Esther Valle(EValle)은 FinanceException의 구성원이므로 현재 읽기 권한이 있습니다. 준비 정책에 따르면 EValle은 어떤 권한도 가질 수 없습니다.  

#### <a name="to-verify-the-results-of-the-staging-policy"></a>준비 정책의 결과를 확인하려면  

1. Hyper-v 관리자에서 파일 서버 FILE1에 연결 하 고 <strong>pass@word1</strong>암호를 사용 하 여 contoso\administrator로 로그온 합니다.  

2. 명령 프롬프트 창을 열고 유형 **gpupdate /force**합니다. 그러면 그룹 정책 변경 내용이 서버에 적용됩니다.  

3. Hyper-V 관리자에서 CLIENT1에 연결합니다. 현재 로그온된 사용자를 로그오프합니다. 가상 컴퓨터 CLIENT1을 다시 시작합니다. 그런 다음 contoso\EValle pass@word1를 사용 하 여 컴퓨터에 로그온 합니다.  

4. 바탕 화면 바로 가기를 두 번 클릭 \\\FILE1\Finance 문서입니다. EValle이 여전히 파일에 액세스할 수 있습니다. FILE1로 다시 전환합니다.  

5. 바탕 화면의 바로 가기에서 **이벤트 뷰어**를 엽니다. **Windows 로그**를 확장하고 **보안**을 선택합니다. 항목을 엽니다 **Event ID 4818**아래는 **중앙 액세스 정책 준비** 작업 범주입니다. EValle에 액세스가 허용된 것으로 표시되어 있습니다. 그러나 준비 정책에 따르면 이 사용자는 액세스가 거부되어야 합니다.  

## <a name="next-steps"></a>다음 단계  
System Center Operations Manager와 같은 중앙 서버 관리 시스템을 사용하는 경우 이벤트에 대한 모니터링을 구성할 수도 있습니다. 이를 통해 관리자는 중앙 액세스 정책을 적용하기 전에 그 효과를 모니터링할 수 있습니다.  


