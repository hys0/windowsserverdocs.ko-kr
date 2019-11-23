---
ms.assetid: 01988844-df02-4952-8535-c87aefd8a38a
title: Deploy Automatic File Classification (Demonstration Steps)
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 7b8d613653bc2effdae155d34a1a94a820bae3aa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357593"
---
# <a name="deploy-automatic-file-classification-demonstration-steps"></a>Deploy Automatic File Classification (Demonstration Steps)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 Active Directory에서 리소스 속성을 사용하도록 설정하고, 파일 서버에서 분류 규칙을 만든 다음, 파일 서버의 파일에 대한 리소스 속성에 값을 할당하는 방법에 대해 설명합니다. 이 예제에서는 다음 분류 규칙을 만듭니다.  
  
-   ' Contoso Confidential.' 문자열에 대 한 파일 집합을 검색 하는 콘텐츠 분류 규칙 문자열이 파일에서 발견되면 해당 파일의 영향 리소스 속성이 높음으로 설정됩니다.  
  
-   파일 집합에 대해 한 파일에서 10번 이상 주민 등록 번호와 일치하는 정규식을 검색하는 콘텐츠 분류 규칙. 패턴이 발견되면 파일은 개인 식별이 가능한 정보를 가진 것으로 되고 개인 식별이 가능한 정보 리소스 속성이 높음으로 설정됩니다.  
  
**이 문서의**  
  
-   [1 단계: 리소스 속성 정의 만들기](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step1)  
  
-   [2 단계: 문자열 콘텐츠 분류 규칙 만들기](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step2)  
  
-   [3 단계: 정규식 콘텐츠 분류 규칙 만들기](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step3)  
  
-   [4 단계: 파일이 분류 되었는지 확인](Deploy-Automatic-File-Classification--Demonstration-Steps-.md#BKMK_Step4)  
  
> [!NOTE]  
> 이 항목에는 설명한 절차의 일부를 자동화하는 데 사용할 수 있는 샘플 Windows PowerShell cmdlet이 포함되어 있습니다. 자세한 내용은 참조 [Cmdlet를 사용 하 여](https://go.microsoft.com/fwlink/p/?linkid=230693)합니다.  
  
## <a name="BKMK_Step1"></a>1 단계: 리소스 속성 정의 만들기  
파일 분류 인프라가 네트워크 공유 폴더에서 검사된 파일에 태그를 지정할 수 있도록 영향 및 개인 식별이 가능한 정보 리소스 속성을 설정합니다.  
  
[Windows PowerShell을 사용 하 여이 단계 수행](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)  
  
#### <a name="to-create-resource-property-definitions"></a>리소스 속성 정의를 만들려면  
  
1.  도메인 컨트롤러에서 Domain Admins 보안 그룹의 구성원으로 서버에 로그인합니다.  
  
2.  Active Directory 관리 센터를 엽니다. 서버 관리자에서 **도구**를 클릭한 다음 **Active Directory 관리 센터**를 클릭합니다.  
  
3.  **동적 Access Control**을 확장하고 **리소스 속성**을 클릭합니다.  
  
4.  **영향**을 마우스 오른쪽 단추로 클릭한 다음 **사용**을 클릭합니다.  
  
5.  **개인 식별이 가능한 정보**를 마우스 오른쪽 단추로 클릭한 다음 **사용**을 클릭합니다.  
  
![솔루션 가이드](media/Deploy-Automatic-File-Classification--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em>***  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
Set-ADResourceProperty '"Enabled:$true '"Identity:'CN=Impact_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'   
Set-ADResourceProperty '"Enabled:$true '"Identity:'CN=PII_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'  
```  
  
## <a name="BKMK_Step2"></a>2 단계: 문자열 콘텐츠 분류 규칙 만들기  
문자열 콘텐츠 분류 규칙은 파일에서 특정 문자열을 검사합니다. 문자열이 발견되면 리소스 속성 값을 구성할 수 있습니다. 이 예제에서는 검색 네트워크 공유 폴더에 있는 각 파일 하 고 ' Contoso Confidential.' 문자열을 찾습니다. 문자열이 발견되면 해당 파일은 높은 비즈니스 영향을 가진 것으로 분류됩니다.  
  
[Windows PowerShell을 사용 하 여이 단계 수행](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)  
  
#### <a name="to-create-a-string-content-classification-rule"></a>문자열 콘텐츠 분류 규칙을 만들려면  
  
1.  Administrators 보안 그룹의 구성원으로 파일 서버에 로그인합니다.  
  
2.  Windows PowerShell 명령 프롬프트에서 **Update-FsrmClassificationPropertyDefinition**을 입력하고 Enter 키를 누릅니다. 그러면 도메인 컨트롤러에서 만들어진 속성 정의가 파일 서버에 동기화됩니다.  
  
3.  파일 서버 리소스 관리자를 엽니다. 서버 관리자에서 **도구**를 클릭한 다음 **파일 서버 리소스 관리자**를 클릭합니다.  
  
4.  **분류 관리**를 확장하고 **분류 규칙**을 마우스 오른쪽 단추로 클릭한 다음 **분류 일정 구성**을 클릭합니다.  
  
5.  **고정된 일정 사용** 확인란과 **새 파일에 대해 분류 계속 허용** 확인란을 선택하고 분류를 실행할 요일을 선택한 다음 **확인**을 클릭합니다.  
  
6.  **분류 규칙**을 마우스 오른쪽 단추로 클릭하고 **분류 규칙 만들기**를 클릭합니다.  
  
7.  **일반** 탭의 **규칙 이름** 상자에 규칙 이름(예: **Contoso Confidential**)을 입력합니다.  
  
8.  **범위** 탭에서 **추가**를 클릭하고 이 규칙에 포함할 폴더(예: D:\Finance Documents)를 선택합니다.  
  
    > [!NOTE]  
    > 범위에 대한 동적 네임스페이스를 선택할 수도 있습니다. 분류 규칙에 대 한 동적 네임 스페이스에 대 한 자세한 내용은 참조 [파일 서버 리소스 관리자의 Windows Server 2012의 새로운 \[리디렉션\]](assetId:///d53c603e-6217-4b98-8508-e8e492d16083)합니다.  
  
9. **분류** 탭에서 다음을 구성합니다.  
  
    -   **파일에 속성 값을 할당할 방법 선택** 상자에서 **콘텐츠 분류자**가 선택되어 있는지 확인합니다.  
  
    -   **파일에 할당할 속성 선택** 상자에서 **가져오기**를 클릭합니다.  
  
    -   **값 지정** 상자에서 **높음**을 클릭합니다.  
  
10. **매개 변수** 머리글 아래에서 **구성**을 클릭합니다.  
  
11. **식 형식** 열에서 **문자열**을 선택합니다.  
  
12. **식** 열에 **Contoso Confidential**을 입력하고 **확인**을 클릭합니다.  
  
13. **평가 유형** 탭에서 **기존 속성 값 다시 평가** 확인란을 선택하고 **기존 값 덮어쓰기**를 클릭한 다음 **확인**을 클릭합니다.  
  
![솔루션 가이드](media/Deploy-Automatic-File-Classification--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em>***  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
$date = Get-Date  
$AutomaticClassificationScheduledTask = New-FsrmScheduledTask -Time $date -Weekly @(3, 2, 4, 5,1,6,0) -RunDuration 0;$AutomaticClassificationScheduledTask  
Set-FsrmClassification -Continuous -schedule $AutomaticClassificationScheduledTask  
New-FSRMClassificationRule -Name 'Contoso Confidential' -Property "Impact_MS" -PropertyValue "3000" -Namespace @('D:\Finance Documents') -ClassificationMechanism "Content Classifier" -Parameters @("StringEx=Min=1;Expr=Contoso Confidential") -ReevaluateProperty Overwrite  
```  
  
## <a name="BKMK_Step3"></a>3 단계: 정규식 콘텐츠 분류 규칙 만들기  
정규식 분류 규칙은 파일에서 정규식과 일치하는 패턴을 검사합니다. 정규식과 일치하는 문자열이 발견되면 리소스 속성 값을 구성할 수 있습니다. 이 예제에서는 네트워크 공유 폴더에 있는 각 파일을 검사하여 주민 등록 번호(XXX XX XXXX) 패턴과 일치하는 문자열을 찾습니다. 패턴이 발견되면 해당 파일은 개인 식별이 가능한 정보를 가진 것으로 분류됩니다.  
  
[Windows PowerShell을 사용 하 여이 단계 수행](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep3)  
  
#### <a name="to-create-a-regular-expression-content-classification-rule"></a>정규식 콘텐츠 분류 규칙을 만들려면  
  
1.  Administrators 보안 그룹의 구성원으로 파일 서버에 로그인합니다.  
  
2.  Windows PowerShell 명령 프롬프트에서 **Update-FsrmClassificationPropertyDefinition**을 입력하고 Enter 키를 누릅니다. 그러면 도메인 컨트롤러에서 만들어진 속성 정의가 파일 서버에 동기화됩니다.  
  
3.  파일 서버 리소스 관리자를 엽니다. 서버 관리자에서 **도구**를 클릭한 다음 **파일 서버 리소스 관리자**를 클릭합니다.  
  
4.  **분류 규칙**을 마우스 오른쪽 단추로 클릭하고 **분류 규칙 만들기**를 클릭합니다.  
  
5.  **일반** 탭의 **규칙 이름** 상자에 분류 규칙의 이름(예: PII Rule)을 입력합니다.  
  
6.  **범위** 탭에서 **추가**를 클릭하고 이 규칙에 포함할 폴더(예: D:\Finance Documents)를 선택합니다.  
  
7.  **분류** 탭에서 다음을 구성합니다.  
  
    -   **파일에 속성 값을 할당할 방법 선택** 상자에서 **콘텐츠 분류자**가 선택되어 있는지 확인합니다.  
  
    -   **파일에 할당할 속성 선택** 상자에서 **개인 식별이 가능한 정보**를 클릭합니다.  
  
    -   **값 지정** 상자에서 **높음**을 클릭합니다.  
  
8.  **매개 변수** 머리글 아래에서 **구성**을 클릭합니다.  
  
9. **식 형식** 열에서 **정규식**을 선택합니다.  
  
10. **식** 열에서 **^ (?! 000) ([0-7] \d{2}| 7 ([0-7] \d | 7 [012])) ([-]?) (?! 00) \d\d\3 (?! 0000) \d{4}$**  
  
11. **최소 발생 수** 열에 **10**을 입력하고 **확인**을 클릭합니다.  
  
12. **평가 유형** 탭에서 **기존 속성 값 다시 평가** 확인란을 선택하고 **기존 값 덮어쓰기**를 클릭한 다음 **확인**을 클릭합니다.  
  
![솔루션 가이드](media/Deploy-Automatic-File-Classification--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em>***  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
New-FSRMClassificationRule -Name "PII Rule" -Property "PII_MS" -PropertyValue "5000" -Namespace @('D:\Finance Documents') -ClassificationMechanism "Content Classifier" -Parameters @("RegularExpressionEx=Min=10;Expr=^(?!000)([0-7]\d{2}|7([0-7]\d|7[012]))([ -]?)(?!00)\d\d\3(?!0000)\d{4}$") -ReevaluateProperty Overwrite  
```  
  
## <a name="BKMK_Step4"></a>4 단계: 파일이 올바르게 분류 되었는지 확인  
분류 규칙에 지정된 폴더에 만들어진 파일의 속성을 보고 파일이 올바르게 분류되었는지 확인할 수 있습니다.  
  
#### <a name="to-verify-that-the-files-are-classified-correctly"></a>파일이 올바르게 분류되었는지 확인하려면  
  
1.  파일 서버에서 파일 서버 리소스 관리자를 사용하여 분류 규칙을 실행합니다.  
  
    1.  **분류 관리**를 클릭하고 **분류 규칙**을 마우스 오른쪽 단추로 클릭한 다음 **지금 모든 규칙을 사용한 분류 실행**을 클릭합니다.  
  
    2.  **완료할 때까지 분류 대기** 옵션을 클릭한 다음 **확인**을 클릭합니다.  
  
    3.  자동 분류 보고서를 닫습니다.  
  
    4.  다음 명령을 사용 하 여 Windows PowerShell을 사용 하 여 수행할 수 있습니다: **시작 FSRMClassification ' "RunDuration 0-확인: $false**  
  
2.  분류 규칙에 지정된 폴더(예: D:\Finance Documents)로 이동합니다.  
  
3.  해당 폴더의 파일을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **분류** 탭을 클릭하고 파일이 올바르게 분류되었는지 확인합니다.  
  
## <a name="BKMK_Links"></a>참고 항목  
  
-   [시나리오: 분류를 사용 하 여 데이터에 대 한 통찰력 얻기](Scenario--Get-Insight-into-Your-Data-by-Using-Classification.md)  
  
-   [자동 파일 분류 계획](https://docs.microsoft.com/previous-versions/orphan-topics/ws.11/jj574209(v%3dws.11))  

  
-   [동적 Access Control: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  
  

