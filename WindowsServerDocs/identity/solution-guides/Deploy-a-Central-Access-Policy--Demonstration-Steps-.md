---
ms.assetid: 8738c03d-6ae8-49a7-8b0c-bef7eab81057
title: "중앙 액세스 정책을 (데모 단계) 배포"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 16973b32407985ffc3f66bf5ac579384a756b5d0
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="deploy-a-central-access-policy-demonstration-steps"></a>중앙 액세스 정책을 (데모 단계) 배포

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 경우 금융 부서 보안 작업 파일 서버에 저장 된 보관된 금융 정보를 보호할 수 있도록 중앙 액세스 정책에 대 한 필요성을 지정할 수 중앙 정보 보안 노력 중입니다. 동일한 국가에서 금융 직원이 읽기 전용으로 각 국가에서 보관된 금융 정보에 액세스할 수 있습니다. 중앙 금융 관리자 그룹 일부 국가에서 금융 정보에 액세스할 수 있습니다.  
  
중앙 액세스 정책 배포 다음 단계에 포함 됩니다.  
  
|단계|설명  
|---------|---------------  
|[정책 및 배포 하는 데 필요한 구성에 대 한 필요성을 식별 계획:](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md#BKMK_1.2)|정책 및 배포 하는 데 필요한 구성에 대 한 필요성을 확인 합니다. 
|[정책 및 구성 요소 구현: 구성](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md#BKMK_1.3)|정책 및 구성 요소를 구성 합니다.  
|[배포 중앙 액세스 정책](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md#BKMK_1.4)|정책의 배포 합니다.  
|[준비 정책 및 유지 관리: 변경](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md#BKMK_1.5)|정책 변경 내용 및 준비 합니다. 
  
## <a name="BKMK_1.1"></a>테스트 환경을 설정합니다  
시작 하기 전에이 시나리오를 테스트 랩을 설정 해야 합니다. 랩을 설정 하는 단계에 자세히 설명 된 [부록 b: the 테스트 환경 설정을](Appendix-B--Setting-Up-the-Test-Environment.md)합니다.  
  
## <a name="BKMK_1.2"></a>정책 및 배포 하는 데 필요한 구성에 대 한 필요성을 식별 계획:  
이 섹션의 배포 계획 단계에 도움이 되는 단계 고급 시리즈를 제공 합니다.  
  
||단계|예제|  
|-|--------|-----------|  
|1.1|비즈니스 중앙 액세스 정책 필요는 확인|파일 서버에 저장 된 금융 정보를 보호 하기 금융 부서 보안 작업 중앙 정보 보안 지정 중앙 액세스 정책에 대 한 필요성을 사용 합니다.|  
|1.2|기본 액세스 정책|금융 문서 금융 부서의 회원만 읽을 해야 합니다. 금융 부서의 회원 문서 자체 국가에 액세스 해야 합니다. 금융 관리자만 쓰기 권한이 있어야 합니다. FinanceException 그룹의 회원에 대해 예외로 허용 됩니다. 이 그룹 읽기 액세스할 수 있습니다.|  
|1.3|기본 Windows Server 2012 구문에 액세스 정책|대상으로 합니다.<br /><br />-Resource.Department 금융 포함<br /><br />액세스 규칙 다음과 같습니다.<br /><br />-User.Country=Resource.Country 읽고 User.department 허용 Resource.Department =<br />에서 모든 권한 User.MemberOf(FinanceAdmin) 허용<br /><br />예외:<br /><br />읽기 memberOf(FinanceException) 허용|  
|1.4|정책 하는 데 필요한 파일 속성을 결정|태그와 파일을:<br /><br />-성<br />국내|  
|1.5|클레임은 유형 및 그룹 정책에 필요한 확인|클레임은 유형:<br /><br />국내<br />-성<br /><br />사용자 그룹 다음과 같습니다.<br /><br />-FinanceAdmin<br />-FinanceException|  
|1.6|이 정책이 적용 하는에서 서버를 확인|모든 금융 파일 서버에 정책이 적용 됩니다.|  
  
## <a name="BKMK_1.3"></a>정책 및 구성 요소 구현: 구성  
이 섹션에서 금융 문서에 대 한 중앙 액세스 정책을 배포 하는 예를 제공 합니다.  
  
|아니요|단계|예제|  
|------|--------|-----------|  
|2.1|클레임 유형에 만들기|다음 청구 종류를 만듭니다.<br /><br />-성<br />국내|  
|2.2|리소스 속성 만들기|만들고 사용 리소스는 다음과 같습니다.<br /><br />-성<br />국내|  
|2.3|중앙 액세스 규칙을 구성 합니다.|이전 섹션에 결정 정책에 포함 된 문서 금융 규칙을 만듭니다.|  
|2.4|구성 중앙 액세스 정책 (뚜껑)|금융 정책 뚜껑 만들고 금융 문서 규칙 해당 뚜껑을 추가 합니다.|  
|2.5|파일 서버에 대상 중앙 액세스 정책|금융 정책 뚜껑 파일 서버에 게시 합니다.|  
|2.6|클레임, 복합 인증과 armoring Kerberos KDC 지원 사용 합니다.|클레임, 복합 인증 및 Kerberos contoso.com에 대 한 armoring KDC 지원 사용 합니다.|  
  
두 가지 클레임 종류 다음 절차에 만들: 국가 및 부서 합니다.  
  
#### <a name="to-create-claim-types"></a>클레임 종류를 만들려면  
  
1.  암호로 contoso\administrator로에 Hyper-v 관리자 및 로그 d 서버 c 1를 열고 **pass@word1**합니다.  
  
2.  관리 센터를 Active Directory를 엽니다.  
  
3.  클릭는 **밤나무 보기 아이콘**, 확장 **동적 액세스 제어**를 선택한 다음 **클레임 유형**합니다.  
  
    마우스 오른쪽 단추로 클릭 **클레임 유형**, 클릭 **새로**을 차례로 클릭 하 고 **클레임 유형**합니다.  
  
    > [!TIP]  
    > 열 수도 있습니다는 **만들기 클레임 유형:** 창에서는 **작업** 창 합니다. 에 **작업** 창 클릭 **새로**을 차례로 클릭 하 고 **클레임 유형**합니다.  
  
4.  에 **원본 특성** 목록의 특성을 목록을 아래로 스크롤하세요 및 클릭 **부서**합니다. 이 채울 해야는 **표시 이름** 필드 **부서**합니다. 클릭 **확인**합니다.  
  
5.  **작업** 창 클릭 **새로**을 차례로 클릭 하 고 **클레임 유형**합니다.  
  
6.  에 **원본 특성** 목록의 특성을 목록을 아래로 스크롤하세요 및 클릭 한 다음는 **c** 특성 (국가 이름). 에 **표시 이름** 필드를 입력 **국가**합니다.  
  
7.  에 **제안 값** 섹션을 **다음 값 추천 하시:**, 클릭 한 다음 **추가**합니다.  
  
8.  에 **값** 및 **표시 이름** 필드를 입력 **미국**을 차례로 클릭 하 고 **확인**합니다.  
  
9. 위의 단계를 반복 합니다. **추천 가치** 대화 상자, 입력 **JP** 에 **값** 및 **표시 이름** 필드 및 클릭 **확인**합니다.  
  
![해결 방법 가이드](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.  
  
 
    New-ADClaimType country -SourceAttribute c -SuggestedValues:@((New-Object Microsoft.ActiveDirectory.Management.ADSuggestedValueEntry("US","US","")), (New-Object Microsoft.ActiveDirectory.Management.ADSuggestedValueEntry("JP","JP","")))  
    New-ADClaimType department -SourceAttribute department  
      
 
  
> [!TIP]  
> Windows PowerShell cmdlet에 대 한 Active Directory 관리 센터에서 수행 하면 각 절차 찾으려면 Active Directory 관리 센터에서 Windows PowerShell 기록 뷰어를 사용할 수 있습니다. 자세한 내용은 참조 [Windows PowerShell 기록 뷰어](https://technet.microsoft.com/library/hh831702)  
  
다음 단계를 리소스 속성 만드는 것입니다. 다음 절차 파일 서버를 사용할 수 있는 리소스 속성을 도메인 컨트롤러의 글로벌 리소스 속성 목록에 추가 자동으로 만듭니다.  
  
#### <a name="to-create-and-enable-pre-created-resource-properties"></a>만들고 미리 작성된 된 리소스 속성을 설정 하려면  
  
1.  Active Directory 관리 센터의 왼쪽된 창에서 클릭 **트리 보기**합니다. 확장 **동적 액세스 제어**를 선택한 다음 **리소스 속성**합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **리소스 속성**, 클릭 **새로**을 차례로 클릭 하 고 **참조 리소스 속성**합니다.  
  
    > [!TIP]  
    > 리소스 속성 선택할 수도 있는 **작업** 창 합니다. 클릭 **새로** 차례로 클릭 하 고 **참조 리소스 속성**합니다.  
  
3.  **클레임 유형 공유 하는 추천 선택 값 목록**, 클릭 **국가**합니다.  
  
4.  에 **표시 이름** 필드를 입력 **국가**을 차례로 클릭 하 고 **확인**합니다.  
  
5.  두 번 클릭 하 고 **리소스 속성** 목록에서 때까지 아래로 스크롤하여는 **부서** 리소스 속성 합니다. 마우스 클릭 한 다음 **활성화**합니다. 이렇게 하면 기본 제공 **부서** 리소스 속성 합니다.  
  
6.  에 **리소스 속성** 목록 Active Directory 관리 센터의 탐색 창에서 하면 이제는 두 활성화 된 리소스 속성:  
  
    -   국가  
  
    -   성  
  
![해결 방법 가이드](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.  
  
```  
New-ADResourceProperty Country -IsSecured $true -ResourcePropertyValueType MS-DS-MultivaluedChoice -SharesValuesWith country  
Set-ADResourceProperty Department_MS -Enabled $true  
Add-ADResourcePropertyListMember "Global Resource Property List" -Members Country  
Add-ADResourcePropertyListMember "Global Resource Property List" -Members Department_MS  
  
```  
  
다음 단계 리소스에 액세스할 수 있는 사용자 정의 하는 중앙 액세스 규칙 만드는 것입니다. 여기서에서 비즈니스 규칙은 다음과 같습니다.  
  
-   금융 부서의 회원 해야만 금융 문서를 읽을 수 있습니다.  
  
-   금융 부서의 회원 자체 국가에서 문서에만 액세스할 수 있습니다.  
  
-   금융 관리자만 쓰기 액세스할 수 있습니다.  
  
-   FinanceException 그룹의 회원에 대 한 예외를 하면 했습니다. 이 그룹 읽기 액세스할 수 있습니다.  
  
-   관리자 및 문서 소유자는 계속 전체 액세스 합니다.  
  
또는 Windows Server 2012 구문 사용 규칙 표현 하기:  
  
금융 포함 되어 Resource.Department 대상:  
  
액세스 규칙 다음과 같습니다.  
  
-   읽기 User.Country=Resource.Country 및 User.department 허용 Resource.Department =  
  
-   모든 권한을 User.MemberOf(FinanceAdmin) 허용  
  
-   읽기 User.MemberOf(FinanceException) 허용  
  
#### <a name="to-create-a-central-access-rule"></a>중앙 액세스 규칙을 만들려면  
  
1.  Active Directory 관리 센터의 왼쪽된 창에서 클릭 **밤나무 보기**선택 **동적 액세스 제어**을 차례로 클릭 하 고 **중앙 액세스 규칙**합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **중앙 액세스 규칙**, 클릭 **새로**을 차례로 클릭 하 고 **중앙 액세스 규칙**합니다.  
  
3.  에 **이름** 필드를 입력 **금융 문서 규칙**합니다.  
  
4.  에 **대상 리소스** 섹션에서 클릭 **편집**의 **중앙 액세스 규칙** 대화 상자에서 클릭 **조건을 추가**합니다. 다음 조건을 추가:   
    [**리소스**] [**부서**] [**같음**] [**Value**] [**금융**]을 차례로 클릭 하 고 **확인**합니다.  
  
5.  에 **권한을** 섹션을 **현재 사용 권한으로 다음 권한을 사용 하 여**, 클릭 **편집**의 **권한에 대 한 고급 보안 설정을** 대화 상자를 클릭 **추가**합니다.  
  
    > [!NOTE]  
    > **제안 된 권한으로 다음 권한을 사용** 옵션 정책을 준비를 만들 수 있습니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 하 고 유지: 변경 하 고 단계가이 항목의 정책 섹션.  
  
6.  에 **권한에 대 한 권한 항목** 대화 상자에서 클릭 **주체 선택**, 입력 **인증 된 사용자**, 클릭 한 다음 **확인**합니다.  
  
7.  에 **권한에 대 한 권한 항목** 대화 상자를 클릭 **조건을 추가**, 다음과 같은 추가:   
    [**User**] [**국가**] [**Any of**] [**리소스**] [**국가**]   
     클릭 **조건을 추가**합니다.   
     [**And**]   
    클릭 [**사용자**] [**부서**] [**중 하나로**] [**리소스**] [**부서**] 합니다. 설정에서 **권한을** 에 **읽기**합니다.  
  
8.  클릭 **확인**을 차례로 클릭 하 고 **추가**합니다. 클릭 **주체 선택**, 입력 **FinanceAdmin**을 차례로 클릭 하 고 **확인**합니다.  
  
9. 선택는 **수정, 읽기 하 고 실행 읽고, 쓰기** 권한과 클릭 **확인**합니다.  
  
10. 클릭 **추가**, 클릭 **주체 선택**, 입력 **FinanceException**을 차례로 클릭 하 고 **확인**합니다. 선택 될 수 있는 권한이 **읽기** 및 **읽기 및 실행**합니다.  
  
11. 클릭 **확인** 세 번 완료 한 Active Directory 관리 센터도 돌아갑니다.  
  
    ![해결 방법 가이드](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
    다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.  
  
 
    $countryClaimType Get-ADClaimType 국가 =  
    $departmentClaimType Get-ADClaimType 부서 =  
    $countryResourceProperty Get-ADResourceProperty 국가 =  
    $departmentResourceProperty Get-ADResourceProperty 부서 =  
    $currentAcl = "O:SYG:SYD:AR(A;; FA;; O W) (한; FA; 됩니다. 모음) (.. 0 x1200a9; 됩니다. S-1-5-21-1787166779-1215870801-2157059049-1113) (.. 0 x1301bf; 됩니다. S-1-5-21-1787166779-1215870801-2157059049-1112) (한; FA; 됩니다. SY) (XA; 0 x1200a9; 됩니다. AU;((@USER." + $countryClaimType.Name + "Any_of @RESOURCE." + $countryResourceProperty.Name + ") & & (@USER." + $departmentClaimType.Name + "Any_of @RESOURCE." + $departmentResourceProperty.Name + ")))"  
    $resourceCondition = "(@RESOURCE." + $departmentResourceProperty.Name + "포함 {`"Finance`"}) "  
    New-ADCentralAccessRule "문서 규칙 재무" CurrentAcl $currentAcl-ResourceCondition $resourceCondition  

  
> [!IMPORTANT]  
> 위의 cmdlet 예제 FinanceAdmin 그룹에 대 한 보안 식별자 (Sid)와 사용자를 만들 때 결정 하 고 예에서 다른 됩니다. 예를 들어, 제공된 SID 값 (S-1-5-21-1787166779-1215870801-2157059049-1113) 배포에서 만드는 해야 FinanceAdmin 그룹 실제 sid 교체 FinanceAdmins 요구 사항에 대 한입니다. 이 그룹에 SID 값을 우러러 보세요, 값을 변수를 할당 및 사용 하 여 변수 여기 Windows PowerShell 사용할 수 있습니다. 자세한 내용은 참조 [Windows PowerShell 팁: Sid와 협력](https://go.microsoft.com/fwlink/?LinkId=253545)합니다.  
  
이제 국가 동일한 부서에서 문서에 액세스할 수 있게 하는 중앙 액세스 규칙이 있어야 합니다. 규칙 FinanceAdmin 그룹 문서, 편집할 수 있으며 FinanceException 그룹이 문서를 읽을 수 있습니다. 이 규칙 금융으로 분류 문서만 대상으로 합니다.  
  
#### <a name="to-add-a-central-access-rule-to-a-central-access-policy"></a>중앙 액세스 정책에 대 한 중앙 액세스 규칙을 추가 하려면  
  
1.  Active Directory 관리 센터의 왼쪽된 창에서 클릭 **동적 액세스 제어**을 차례로 클릭 하 고 **중앙 액세스 정책을**합니다.  
  
2.  에 **작업** 창 클릭 **새로**을 차례로 클릭 하 고 **중앙 액세스 정책**합니다.  
  
3.  **중앙 액세스 정책 만들기:**, 입력 **금융 정책** 에 **이름** 상자 합니다.  
  
4.  **액세스 중앙 멤버 규칙**, 클릭 **추가**합니다.  
  
5.  두 번 클릭는 **금융 문서 규칙** 추가 하는 **중앙 액세스 규칙 다음과 같은 추가** 목록을 클릭 한 다음 선택 하 고 **확인**합니다.  
  
6.  클릭 **확인** 완료 합니다. 이제 금융 정책 라는 중앙 액세스 정책이 있어야 합니다.  
  
    ![해결 방법 가이드](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
    다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.  
  
    ```  
    New-ADCentralAccessPolicy "Finance Policy" Add-ADCentralAccessPolicyMember   
    -Identity "Finance Policy"   
    -Member "Finance Documents Rule"  
  
    ```  
  
#### <a name="to-apply-the-central-access-policy-across-file-servers-by-using-group-policy"></a>그룹 정책을 사용 하 여 중앙 액세스 정책 파일 서버에서 적용 하기 위해  
  
1.  에 **시작** 화면에 **검색** 상자에 입력 **그룹 정책 관리**합니다. 두 번 클릭 **그룹 정책 관리**합니다.  
  
    > [!TIP]  
    > 하는 경우는 **표시 관리 도구** 설정은 사용자가 **관리 도구** 폴더 및 해당 콘텐츠는에 표시 되지는 **설정** 결과 합니다.  
  
    > [!TIP]  
    > 프로덕션 환경의 파일 서버 조직 장치 (OU)을 만들려면 고이 정책이 적용 하려는 모든 파일 서버가이 OU에 추가 해야 합니다. 다음 그룹 정책을 만들 하 고이 OU 해당 정책에 추가할 수 있습니다.  
  
2.  만든 그룹 정책 개체가이 단계에서 편집 [빌드 도메인 컨트롤러](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_Build) 만든 중앙 액세스 정책 포함 테스트 환경에서 섹션. 그룹 정책 관리 편집기에서을 찾아서 (여기서에서 contoso.com) 도메인에 있는 조직이 선택: **그룹 정책 관리**, **숲: contoso.com**, **도메인**, **contoso.com**, **Contoso**, **FileServerOU**합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **FlexibleAccessGPO**을 차례로 클릭 하 고 **편집**합니다.  
  
4.  그룹 정책 편집기 관리 창에서 이동 **컴퓨터 구성**, 확장 **정책**, 확장 **Windows 설정**를 클릭 하 고 **보안 설정**합니다.  
  
5.  확장 **파일 시스템**를 마우스 오른쪽 단추로 클릭 **중앙 액세스 정책**을 차례로 클릭 하 고 **중앙 관리 액세스 정책**합니다.  
  
6.  에 **중앙 액세스 정책에서 구성** 대화 상자에 추가 **금융 정책**을 차례로 클릭 하 고 **확인**합니다.  
  
7.  아래로 스크롤하여 **감사 정책 구성 고급**를 확장 합니다.  
  
8.  확장 **감사 정책**를 선택 하 고 **개체 액세스**합니다.  
  
9. 두 번 클릭 **중앙 액세스 정책 준비 감사**합니다. 모든 세 확인란을 선택한 다음 **확인**합니다. 이 단계의 시스템을 이벤트 중앙 액세스 준비 정책 관련 감사를 받을 수 있습니다.  
  
10. 두 번 클릭 **파일 시스템 속성 감사**합니다. 세 가지 확인란을 모두 선택 하 고 클릭 **확인**합니다.  
  
11. 그룹 정책 관리 편집기 닫습니다. 이제는 중앙 액세스 정책을 그룹 정책에 포함 했습니다.  
  
클레임 또는 인증 데이터 장치를 제공 하는 도메인 도메인 컨트롤러에 대 한 도메인 컨트롤러 동적 액세스 제어를 지원 하도록 구성 해야 합니다.  
  
#### <a name="to-enable-support-for-claims-and-compound-authentication-for-contosocom"></a>청구에 대 한 지원 및 복합 인증 contoso.com를 사용 하도록 설정 하려면  
  
1.  그룹 정책 관리 열을 클릭 **contoso.com**을 차례로 클릭 하 고 **도메인 컨트롤러**합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **기본 도메인 컨트롤러 정책**을 차례로 클릭 하 고 **편집**합니다.  
  
3.  그룹 정책 편집기 관리 창에서 두 번 클릭 **컴퓨터 구성**를 두 번 클릭 **정책**, 두 번 클릭 **관리 템플릿**, 두 번 클릭 **시스템**, 다음 두 번 클릭 하 고 **KDC**합니다.  
  
4.  두 번 클릭 **인증 Kerberos armoring 및 청구에 대 한 지원을 KDC 복합**합니다. 에 **인증 Kerberos armoring 및 청구에 대 한 지원을 KDC 복합** 대화 상자를 클릭 **사용** 선택 **지원 되는** 에서 **옵션** 드롭다운 목록에서 합니다. (사용자 클레임 중앙 액세스 정책에서 사용 하 여이 설정을 사용 해야 합니다.)  
  
5.  닫기 **그룹 정책 관리**합니다.  
  
6.  명령 프롬프트를 열고 유형 `gpupdate /force`합니다.  
  
## <a name="BKMK_1.4"></a>배포 중앙 액세스 정책  
  
||단계|예제|  
|-|--------|-----------|  
|3.1|뚜껑 파일 서버에 적절 한 공유 폴더를 할당 합니다.|중앙 액세스 정책을 파일 서버에 적절 한 공유 폴더를 할당 합니다.|  
|3.2|액세스 적절 하 게 구성 되어 있는지 확인 합니다.|사용자는 여러 국가 및 부서에 대 한 액세스를 확인 합니다.|  
  
이 단계에서 파일 서버에 중앙 액세스 정책을 할당 합니다. 이전 단계를 만든 중앙 액세스 정책 수신 되는 파일 서버에 로그온 한 정책을 공유 폴더를 할당 합니다.  
  
#### <a name="to-assign-a-central-access-policy-to-a-file-server"></a>파일 서버에 중앙 액세스 정책 지정 하려면  
  
1.  Hyper-v 관리자에서 파일 1 서버에 연결 합니다. Contoso\administrator 암호를 사용 하 여 서버에 로그온: **pass@word1**합니다.  
  
2.  관리자 권한 명령 프롬프트 및 유형 엽니다: **gpupdate /force**합니다. 이렇게 하면 그룹 정책을 변경 내용을 적용 서버에는 합니다.  
  
3.  글로벌 리소스 속성 Active Directory에서 복구 해야 할 수도 있습니다. 관리자 권한 Windows PowerShell 창 및 유형 엽니다 `Update-FSRMClassificationpropertyDefinition`합니다. ENTER를 클릭 한 다음 Windows PowerShell를 닫습니다.  
  
    > [!TIP]  
    > 또한 파일 서버에 로그인 하 여 전 세계 리소스 속성을 복구할 수 있습니다. 파일 서버에서 전 세계 리소스 속성 복구 하려면 다음을 수행합니다  
    >   
    > 1.  암호를 사용 하 여으로 contoso\administrator, 파일 서버 파일을 1에 로그온 **pass@word1**합니다.  
    > 2.  파일 서버 리소스 관리자를 엽니다. 파일 서버 리소스 관리자를 열을 클릭 **시작**, 입력 **파일 서버 리소스 관리자**을 차례로 클릭 하 고 **파일 서버 리소스 관리자**합니다.  
    > 3.  파일 서버 리소스 관리자에서 클릭 **파일 분류 관리** 를 마우스 오른쪽 단추로 클릭 **분류 속성** 차례로 클릭 하 고 **새로 고침**합니다.  
  
4.  Windows 탐색기를 열고 왼쪽된 창에서 드라이브 D. 마우스 오른쪽 단추로 클릭 하 고 **금융 문서** 폴더를 클릭 하 고 **속성**합니다.  
  
5.  클릭는 **분류** 탭을 클릭 **국가**를 선택한 다음 **미국** 에 **값** 필드 합니다.  
  
6.  클릭 **부서**를 선택한 다음 **금융** 에 **값** 필드와 클릭 한 다음 **적용**합니다.  
  
    > [!NOTE]  
    > 중앙 액세스 정책 금융 부서 대상 파일 하도록 구성 된 기억 합니다. 이전 단계 국가 및 부서 특성으로 폴더에 있는 모든 문서를 표시합니다.  
  
7.  클릭 하 고 **보안** 탭을 클릭 한 다음 **고급**합니다. 클릭 하 고 **중앙 정책** 탭 합니다.  
  
8.  클릭 **변경**선택 **금융 정책** 드롭다운 메뉴에서 **적용**합니다. 볼 수 있는 **금융 문서 규칙** 정책에 표시 합니다. Active Directory 규칙을 만들 때를 설정 하는 사용 권한을 모두 볼 수 있는 항목을 확장 합니다.  
  
9. 클릭 **확인** Windows 탐색기도 돌아갑니다.  
  
다음 단계를 적절 하 게 액세스 구성 되어 있는지 확인 합니다.  사용자 계정이 있어야 적절 한 부서 특성 집합 합니다 (이 사용 하 여 설정 Active Directory 관리 센터). 새로운 정책의 효과적인 결과를 확인 하는 가장 간단한 방법은 사용 하는 것은 **유효한 액세스** Windows 탐색기에서 탭 합니다. **유효한 액세스** 특정된 사용자 계정에 대 한 액세스 권한을 탭에 표시 됩니다.  
  
#### <a name="to-examine-the-access-for-various-users"></a>다양 한 사용자에 대 한 액세스를 검사 하려면  
  
1.  Hyper-v 관리자에서 파일 1 서버에 연결 합니다. 서버에 contoso\administrator 사용 하 여 로그온 합니다. D:\ Windows 탐색기에서로 이동 합니다. 마우스 오른쪽 단추로 클릭는 **금융 문서** 폴더를 클릭 하 고 **속성**합니다.  
  
2.  클릭는 **보안** 탭을 클릭 **고급**을 차례로 클릭 하 고 있는 **유효한 액세스** 탭 합니다.  
  
3.  사용자에 대 한 권한을 검사를 클릭 **사용자 선택**, 사용자의 이름을 입력 한 다음 **유효한 액세스 보기** 유효한 액세스 권한이 볼 수 있습니다. 예를 들어:  
  
    -   Myriam Delesalle (MDelesalle) 금융 부서에 이며 폴더에 읽기 액세스 있어야 합니다.  
  
    -   남궁익선 (MReid) FinanceAdmin 그룹의 회원 이며 폴더 수정 액세스할 수 있어야 합니다.  
  
    -   Esther Valle (EValle) 금융 부서;에 있지 않습니다. 그러나 FinanceException 그룹의 회원은 많이 하며 읽기 액세스 있어야 합니다.  
  
    -   Maira Wenzel (MWenzel) 금융 부서에서 아니며 FinanceAdmin 또는 FinanceException 그룹의 속해 있지 않습니다. 폴더에 대 한 액세스 없을 해야 언제.  
  
    마지막 열 라는 공지 **액세스 하 여 제한 된** 유효한 액세스 창에 있습니다. 이 열 어떤 게이트 사용자의 권한을 영향는 알 수 있습니다. 이 경우 NTFS 및 사용 권한을 모든 권한을 모든 사용자를 허용 합니다. 그러나 중앙 액세스 정책 규칙 이전 구성에 따라 액세스를 제한 합니다.  
  
## <a name="BKMK_1.5"></a>준비 정책 및 유지 관리: 변경  
  
||||  
|-|-|-|  
|번호|단계|예제|  
|4.1|클라이언트에 대 한 주장 디바이스를 구성 합니다.|클레임 디바이스를 사용 하도록 설정 하려면 그룹 정책 설정을 설정합니다|  
|4.2|디바이스에 대 한 청구 사용 하도록 설정 합니다.|디바이스에 대 한 국가 클레임 유형을 사용 하도록 설정 합니다.|  
|4.3|준비 정책 기존 중앙 액세스 규칙을 수정할 수에 추가 합니다.|금융 문서 규칙을 준비 정책 추가 수정 합니다.|  
|4.4|결과 준비 정책 봅니다.|Ester Velle 권한이 있는지 확인 합니다.|  
  
#### <a name="to-set-up-group-policy-setting-to-enable-claims-for-devices"></a>디바이스에 대 한 주장 설정을 사용 하도록 설정 하려면 그룹 정책 설정 하려면  
  
1.  D c 1, 그룹 정책 관리 열기를 클릭 로그온 **contoso.com**, 클릭 **기본 도메인 정책**마우스 오른쪽 단추로 클릭 하 고 선택 **편집**합니다.  
  
2.  그룹 정책 편집기 관리 창에서 이동 **컴퓨터 구성**, **정책**, **관리 템플릿**, **시스템**, **Kerberos**합니다.  
  
3.  선택 **Kerberos 클라이언트 클레임, 지원 복합 인증 Kerberos armoring** 클릭 **활성화**합니다.  
  
#### <a name="to-enable-a-claim-for-devices"></a>디바이스에 대 한 청구 사용 하도록 설정 하려면  
  
1.  암호로 contoso\Administrator로에 Hyper-v 관리자 및 로그 d 서버 c 1를 열고 **pass@word1**합니다.  
  
2.  **도구** 메뉴, Active Directory 관리 센터를 엽니다.  
  
3.  클릭 **밤나무 보기**, 확장 **동적 액세스 제어**를 두 번 클릭 **주장 유형**, 두 번 클릭 하 고는 **국가** 주장.  
  
4.  **청구 이러한 종류의 다음 클래스 실행할 수**는 **컴퓨터** 확인란을 선택 합니다. 클릭 **확인**합니다.   
    모두 **사용자** 및 **컴퓨터** 이제 확인란을 선택 해야 합니다. 국가 클레임 이제 뿐만 아니라 사용자가 디바이스 에서도 사용할 수 있습니다.  
  
다음 단계를 준비 정책 규칙 만드는 것입니다. 사용 하기 전에 새 정책 항목의 효과 모니터링 하 준비 정책 사용할 수 있습니다. 다음 단계를 준비 정책 항목을 만들고 공유 폴더에 미치는 영향을 모니터링 합니다.  
  
#### <a name="to-create-a-staging-policy-rule-and-add-it-to-the-central-access-policy"></a>준비 정책 규칙 만들고 중앙 액세스 정책에 추가 하려면  
  
1.  암호로 contoso\Administrator로에 Hyper-v 관리자 및 로그 d 서버 c 1를 열고 **pass@word1**합니다.  
  
2.  관리 센터를 Active Directory를 엽니다.  
  
3.  클릭 **트리 보기**, 확장 **동적 액세스 제어**를 선택 하 고 **중앙 액세스 규칙**합니다.  
  
4.  마우스 오른쪽 단추로 클릭 **금융 문서 규칙**을 차례로 클릭 하 고 **속성**합니다.  
  
5.  에 **제안 권한을** 섹션을는 **준비 구성 사용 권한을** 확인란을 클릭 **편집**, 클릭 한 다음 **추가**합니다. **권한을 제안에 대 한 사용 권한을 항목** 창 클릭는 **주체 선택** 링크, 입력 **인증 된 사용자**, 차례로 클릭 하 고 **확인**합니다.  
  
6.  클릭 하 고 **조건을 추가** 에 연결 하 고 다음 조건을 추가:   
     [**User**] [**국가**] [**Any of**] [**리소스**] [**국가**] 합니다.  
  
7.  클릭 **조건을 추가** 다시은 다음 조건을 추가:  
    [**And**]   
     [**장치**] [**국가**] [**Any of**] [**리소스**] [**국가**]  
  
8.  클릭 **조건을 추가** 다시은 다음 조건을 추가 합니다.  
    [및]   
     [**User**] [**Group**] [**의 모든 구성원이**] [**값**] \ (**FinanceException**)  
  
9. FinanceException를 설정 하려면 그룹에서 **항목 추가** 의 **사용자, 컴퓨터, 계정 서비스, 또는 그룹 선택** 창, 입력 **FinanceException**합니다.  
  
10. 클릭 **사용 권한을**선택 **모든 권한**를 클릭 하 고 **확인**합니다.  
  
11. 사용 권한 제안 창에 대 한 고급 보안 설정을 선택 **FinanceException** 클릭 **제거**합니다.  
  
12. 클릭 **확인** 두 번 완료 합니다.  
  
![해결 방법 가이드](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.  
  
```  
Set-ADCentralAccessRule  
-Identity: "CN=FinanceDocumentsRule,CN=CentralAccessRules,CN=ClaimsConfiguration,CN=Configuration,DC=Contoso.com"  
-ProposedAcl: "O:SYG:SYD:AR(A;;FA;;;BA)(A;;FA;;;SY)(A;;0x1301bf;;;S-1-21=1426421603-1057776020-1604)"  
-Server: "WIN-2R92NN8VKFP.Contoso.com"  
  
```  
  
> [!NOTE]  
> 위의 cmdlet 예제 서버 값 테스트 랩 환경에서 서버를 반영합니다. Windows PowerShell 기록 뷰어를 사용 하 여 Windows PowerShell cmdlet에 대 한 Active Directory 관리 센터에서 수행 하면 각 절차를 확인할 수 있습니다. 자세한 내용은 참조 [Windows PowerShell 기록 뷰어](https://technet.microsoft.com/library/hh831702)  
  
이 제안된 권한 집합에 FinanceException 그룹의 회원은 전체 액세스할 파일에 자체 국가에서 문서와 같은 국가에서 장치를 통해 액세스할 때마다 합니다. 감사 항목 파일 액세스 하려고 할 때 금융 부서에서 다른 사람이 보안 로그 파일 서버에 사용할 수 있습니다. 그러나 정책을 준비에서 확장지 않습니다 될 때까지 보안 설정은 적용 되지 않습니다.  
  
다음 절차에서는 준비 정책 결과 확인합니다. 현재 규칙에 따라 사용 권한이 있는 사용자 이름으로 공유 폴더에 액세스 하면 됩니다. Esther Valle (EValle) FinanceException의 회원 이며 권한 읽기 현재 사용자. 준비 정책에 따라 EValle 모든 권한이 없이 됩니다.  
  
#### <a name="to-verify-the-results-of-the-staging-policy"></a>준비 정책 결과 확인 하려면  
  
1.  암호를 사용 contoso\administrator로 Hyper-v 관리자 및 로그 파일 서버 파일 1에 연결 **pass@word1**합니다.  
  
2.  명령 프롬프트 창을 열고 유형 **gpupdate /force**합니다. 이렇게 하면 그룹 정책 변경 사항을 적용 서버에 있습니다.  
  
3.  Hyper-v 관리자 CLIENT1 서버에 연결 됩니다. 로그 오프 사용자의 현재 로그온 합니다. CLIENT1 가상 컴퓨터를 다시 시작 합니다. 다음 컴퓨터에 로그온 contoso\EValle를 사용 하 여 pass@word1합니다.  
  
4.  바탕 화면 바로 가기를 \\\FILE1\Finance 문서를 두 번 클릭 합니다. EValle 파일에 액세스할 여전히 해야 합니다. 파일 1 다시 전환 합니다.  
  
5.  열기 **이벤트 뷰어** 에서 바탕 화면에서 바로 가기 키입니다. 확장 **Windows 로그**를 선택한 다음 **보안**합니다. 와 항목을 열고 **이벤트 ID 4818**아래에서 **중앙 액세스 정책 준비** 작업 범주입니다. EValle; 액세스를 허용 된 나타나면 그러나 준비 정책에 따라 사용자가 있는 된 액세스할 수 없습니다.  
  
## <a name="next-steps"></a>다음 단계  
System Center Operations Manager 같은 중앙 서버 관리 시스템을 사용 하는 경우 이벤트에 대 한 모니터링 구성 수 있습니다. 이 관리자를 적용 되기 전에 중앙 액세스 정책을 영향을 확인할 수 있습니다.  
  

