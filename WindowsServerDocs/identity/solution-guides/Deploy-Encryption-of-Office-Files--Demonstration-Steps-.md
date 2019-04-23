---
ms.assetid: 2c76e81a-c2eb-439f-a89f-7d3d70790244
title: Deploy Encryption of Office Files (Demonstration Steps)
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 529000c60a80ee33fc2aa7d09370d8ac1e06311c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850234"
---
# <a name="deploy-encryption-of-office-files-demonstration-steps"></a>Deploy Encryption of Office Files (Demonstration Steps)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Contoso 재무 부서는 여러 문서를 저장 하는 파일 서버에 있습니다. 이러한 문서는 일반 문서일 수도 있고 HBI(높은 비즈니스 영향) 문서일 수도 있습니다. 예를 들어 기밀 정보가 포함된 문서는 Contoso에서 HBI 문서로 간주됩니다. Contoso에서는 모든 문서에 최소한의 보호가 적용되는지, HBI 문서가 적합한 사람으로 제한되어 있는지 확인하고 싶어 합니다. 이를 위해 Contoso는 FCI 파일 분류 인프라 () 및 Windows Server 2012에서 사용할 수 있는 AD RMS를 사용 하 여 탐색 합니다. Contoso는 FCI를 사용하여 파일 서버에 있는 모든 문서를 콘텐츠에 따라 분류한 다음 AD RMS를 사용하여 적절한 권한 정책을 적용할 예정입니다.  
  
이 시나리오에서는 다음 단계를 수행 합니다.  
  
|태스크|설명|  
|--------|---------------|  
|[리소스 속성을 사용 하도록 설정](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_1.1)|**영향** 및 **개인 식별이 가능한 정보** 리소스 속성을 사용합니다.|  
|[분류 규칙 만들기](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_2)|이 시나리오에서는 **HBI 분류 규칙** 및 **PII 분류 규칙**을 만듭니다.|  
|[파일 관리 작업을 사용 하 여 자동으로 AD RMS 사용 하 여 문서를 보호 하려면](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_3)|자동으로 AD RMS를 사용하여 높은 PII(개인 식별이 가능한 정보)가 포함된 문서를 보호하는 파일 관리 작업을 만듭니다. FinanceAdmin 그룹의 구성원만 높은 PII가 포함된 문서에 액세스할 수 있습니다.|  
|[결과 보기](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_4)|문서 분류를 검토하고 문서의 콘텐츠를 변경할 때 문서 분류가 어떻게 변경되는지 확인합니다. 또한 문서가 AD RMS로 보호되는 방식을 확인합니다.|  
|[AD RMS 보호 확인](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_5)|문서가 AD RMS로 보호되는지 확인합니다.|  
|||  
  
## <a name="BKMK_1.1"></a>1 단계: 리소스 속성 사용  
  
#### <a name="to-enable-resource-properties"></a>리소스 속성을 사용하려면  
  
1.  Hyper-V 관리자에서 ID_AD_DC1 서버에 연결합니다. Contoso\Administrator 암호로 사용 하 여 서버에 로그인 **pass@word1**합니다.  
  
2.  Active Directory 관리 센터를 열고 **트리 보기**를 클릭합니다.  
  
3.  **동적 액세스 제어**를 확장하고 **리소스 속성**을 선택합니다.  
  
4.  **표시 이름** 열에서 아래의 **영향** 속성으로 스크롤합니다. **영향**을 마우스 오른쪽 단추로 클릭한 다음 **사용**을 클릭합니다.  
  
5.  **표시 이름** 열에서 아래의 **개인 식별이 가능한 정보** 속성으로 스크롤합니다. **개인 식별이 가능한 정보**를 마우스 오른쪽 단추로 클릭한 다음 **사용**을 클릭합니다.  
  
6.  리소스 속성을 **전역 리소스 목록**에 게시하려면 왼쪽 창에서 **리소스 속성 목록**을 클릭한 다음 **전역 리소스 속성 목록**을 두 번 클릭합니다.  
  
7.  **추가**를 클릭하고 아래로 스크롤한 다음 **영향**을 클릭하여 목록에 추가합니다. **개인 식별이 가능한 정보**에 대해서도 동일한 단계를 수행합니다. **확인** 을 두 번 클릭하여 작업을 마칩니다.  
  
![솔루션 가이드](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
Set-ADResourceProperty -Enabled:$true -Identity:"CN=Impact_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com"  
Set-ADResourceProperty -Enabled:$true -Identity:"CN=PII_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com" 
```  
  
## <a name="BKMK_2"></a>2 단계: 분류 규칙 만들기  
이 단계에서는 **높은 영향** 분류 규칙을 만드는 방법을 설명합니다. 이 규칙은 문서의 콘텐츠를 검색 하 고 "Contoso Confidential" 문자열이 발견 되는 경우이 문서를 높은 비즈니스 영향이 있는 것으로 분류 합니다. 이전에 할당된 낮은 비즈니스 영향 분류는 이 규칙으로 재정의됩니다.  
  
또한 **높은 PII** 규칙도 만듭니다. 이 규칙은 문서의 콘텐츠를 검색하여 주민 등록 번호가 발견되면 이 문서를 높은 PII가 있는 것으로 분류합니다.  
  
#### <a name="to-create-the-high-impact-classification-rule"></a>높은 영향 분류 규칙을 만들려면  
  
1.  Hyper-V 관리자에서 ID_AD_FILE1에 연결합니다. Contoso\Administrator 암호로 사용 하 여 서버에 로그인 **pass@word1**합니다.  
  
2.  Active Directory에서 전역 리소스 속성을 새로 고쳐야 합니다. Windows PowerShell을 엽니다. `Update-FSRMClassificationPropertyDefinition`을 입력한 다음 Enter 키를 누릅니다. Windows PowerShell을 닫습니다.  
  
3.  파일 서버 리소스 관리자를 엽니다. 파일 서버 리소스 관리자를 열려면 **시작**을 클릭하고 **파일 서버 리소스 관리자**를 입력한 다음 **파일 서버 리소스 관리자**를 클릭합니다.  
  
4.  파일 서버 리소스 관리자의 왼쪽 창에서 **분류 관리**를 확장하고 **분류 규칙**을 선택합니다.  
  
5.  **작업** 창에서 **분류 일정 구성**을 클릭합니다. **자동 분류** 탭에서 **고정된 일정 사용**과 **요일**을 차례로 선택한 다음 **새 파일에 대해 분류 계속 허용** 확인란을 선택합니다. **확인**을 클릭합니다.  
  
6.  **작업** 창에서 **분류 규칙 만들기**를 클릭합니다. 이렇게 하면 **분류 규칙 만들기** 대화 상자가 열립니다.  
  
7.  **규칙 이름** 상자에 **High Business Impact**를 입력합니다.  
  
8.  에 **설명** 상자에 입력 합니다 **문서 "Contoso Confidential" 문자열의 유무에 따라 높은 비즈니스 영향을 인지 여부를 결정**  
  
9. **범위** 탭에서 **폴더 관리 속성 설정**을 클릭하고 **폴더 사용량**을 선택한 다음 **추가**를 클릭합니다. 그런 다음 **찾아보기**를 클릭하고 D:\Finance Documents 경로로 이동하여 **확인**을 클릭한 다음 **그룹 파일** 이라는 속성 값을 선택하고 **닫기**를 클릭합니다. 관리 속성이 설정되면 **규칙 범위** 탭에서 **그룹 파일**을 선택합니다.  
  
10. **분류** 탭을 클릭합니다.  파일에 속성 값을 할당할 방법 선택아래의 드롭다운 목록에서 **콘텐츠 분류자** 를 선택합니다.  
  
11. **파일에 할당할 속성 선택** 아래의 드롭다운 목록에서 **영향**을 선택합니다.  
  
12. **값 지정**아래의 드롭다운 목록에서 **높음** 을 선택합니다.  
  
13. **매개 변수** 아래에서 **구성**을 클릭합니다.  **분류 매개 변수** 대화 상자의 **식 형식** 목록에서 **문자열**을 선택합니다. **식** 상자에 Contoso Confidential을 입력하고 **확인**을 클릭합니다.  
  
14. **평가 유형** 탭을 클릭합니다.  기존 속성 값 다시 평가, **기존 값 덮어쓰기**, **확인** 을 차례로 클릭하여 작업을 마칩니다.  
  
![솔루션 가이드](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
Update-FSRMClassificationPropertyDefinition  
$date = Get-Date  
$AutomaticClassificationScheduledTask = New-FsrmScheduledTask -Time $date -Weekly @(3, 2, 4, 5,1,6,0) -RunDuration 0;  
Set-FsrmClassification -Continuous -schedule $AutomaticClassificationScheduledTask  
New-FSRMClassificationRule -Name "High Business Impact" -Property "Impact_MS" -Description "Determines if the document has a high business impact based on the presence of the string 'Contoso Confidential'" -PropertyValue "3000" -Namespace @("D:\Finance Documents") -ClassificationMechanism "Content Classifier" -Parameters @("StringEx=Min=1;Expr=Contoso Confidential") -ReevaluateProperty Overwrite  
```  
  
#### <a name="to-create-the-high-pii-classification-rule"></a>높은 PII 분류 규칙을 만들려면  
  
1.  Hyper-V 관리자에서 ID_AD_FILE1에 연결합니다. Contoso\Administrator 암호로 사용 하 여 서버에 로그인 **pass@word1**합니다.  
  
2.  바탕 화면에서 **Regular Expressions**라는 폴더를 열고 **RegEx-SSN**이라는 문서를 엽니다. 강조 표시 하 고 다음 정규식 문자열 복사: **^ (?! 000) ([0-7] \d{2}| 7([0-7]\d|7[012 ([-]?) (?! 00) \d\d\3 (?! 0000) \d{4}$** 합니다. 이 문자열은 이 단계의 뒷부분에서 사용되므로 클립보드에 그대로 두어야 합니다.  
  
3.  파일 서버 리소스 관리자를 엽니다. 파일 서버 리소스 관리자를 열려면 **시작**을 클릭하고 **파일 서버 리소스 관리자**를 입력한 다음 **파일 서버 리소스 관리자**를 클릭합니다.  
  
4.  파일 서버 리소스 관리자의 왼쪽 창에서 **분류 관리**를 확장하고 **분류 규칙**을 선택합니다.  
  
5.  **작업** 창에서 **분류 일정 구성**을 클릭합니다. **자동 분류** 탭에서 **고정된 일정 사용**과 **요일**을 차례로 선택한 다음 **새 파일에 대해 분류 계속 허용** 확인란을 선택합니다. 확인을 클릭합니다.  
  
6.  **규칙 이름** 상자에 **High PII**를 입력합니다. **설명** 상자에 **Determines if the document has a high PII based on the presence of a Social Security Number**을 입력합니다.  
  
7.  **범위** 탭을 클릭하고 **그룹 파일** 확인란을 선택합니다.  
  
8.  **분류** 탭을 클릭합니다.  파일에 속성 값을 할당할 방법 선택아래의 드롭다운 목록에서 **콘텐츠 분류자** 를 선택합니다.  
  
9. **파일에 할당할 속성 선택** 아래의 드롭다운 목록에서 **개인 식별이 가능한 정보**를 선택합니다.  
  
10. **값 지정**아래의 드롭다운 목록에서 **높음** 을 선택합니다.  
  
11. **매개 변수** 아래에서 **구성**을 클릭합니다.   
    에 **분류 매개 변수**창에는 **식 형식을** 목록에서 **정규식**합니다. 에 **식** 상자에 클립보드의 텍스트를 붙여 넣습니다: **^ (?! 000) ([0-7] \d{2}| 7([0-7]\d|7[012 ([-]?) (?! 00) \d\d\3 (?! 0000) \d{4}$** 를 클릭 하 고 **확인**합니다.  
  
    > [!NOTE]  
    > 이 식은 유효하지 않은 주민 등록 번호를 허용합니다. 따라서 데모에서 가상의 주민 등록 번호를 사용할 수 있습니다.  
  
12. **평가 유형** 탭을 클릭합니다.  기존 속성 값 다시 평가, **기존 값 덮어쓰기**를 차례로 선택하고 **확인** 을 클릭하여 작업을 마칩니다.  
  
![솔루션 가이드](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
New-FSRMClassificationRule -Name "High PII" -Description "Determines if the document has a high PII based on the presence of a Social Security Number." -Property "PII_MS" -PropertyValue "5000" -Namespace @("D:\Finance Documents") -ClassificationMechanism "Content Classifier" -Parameters @("RegularExpressionEx=Min=1;Expr=^(?!000)([0-7]\d{2}|7([0-7]\d|7[012]))([ -]?)(?!00)\d\d\3(?!0000)\d{4}$") -ReevaluateProperty Overwrite  
```  
  
다음 두 개의 분류 규칙을 만들었습니다.  
  
-   High Business Impact  
  
-   높은 PII  
  
## <a name="BKMK_3"></a>3 단계: 파일 관리 작업을 사용 하 여 자동으로 AD RMS 사용 하 여 문서를 보호  
내용을 기반으로 하는 문서를 자동으로 분류 하는 규칙을 만들었으므로 이제 다음 단계는 AD RMS를 사용 하 여 자동으로 분류에 따라 특정 문서를 보호 하는 파일 관리 작업을 만드는 것입니다. 이 단계에서는 높은 PII가 포함된 문서를 자동으로 보호하는 파일 관리 작업을 만듭니다. FinanceAdmin 그룹의 구성원만 높은 PII가 포함된 문서에 액세스할 수 있습니다.  
  
#### <a name="to-protect-documents-with-ad-rms"></a>AD RMS로 문서를 보호하려면  
  
1.  Hyper-V 관리자에서 ID_AD_FILE1에 연결합니다. Contoso\Administrator 암호로 사용 하 여 서버에 로그인 **pass@word1**합니다.  
  
2.  파일 서버 리소스 관리자를 엽니다. 파일 서버 리소스 관리자를 열려면 **시작**을 클릭하고 **파일 서버 리소스 관리자**를 입력한 다음 **파일 서버 리소스 관리자**를 클릭합니다.  
  
3.  왼쪽 창에서 **파일 관리 작업**을 선택합니다. **작업** 창에서 **파일 관리 작업 만들기**를 선택합니다.  
  
4.  **작업 이름:** 필드에 **High PII**를 입력합니다. **설명** 필드에 **Automatic RMS protection for high PII documents**를 입력합니다.  
  
5.  **범위** 탭을 클릭하고 **그룹 파일** 확인란을 선택합니다.  
  
6.  **동작** 탭을 클릭합니다. 유형에서 **RMS 암호화**를 선택합니다. **찾아보기**를 클릭하여 템플릿을 선택한 다음 **Contoso Finance Admin Only**를 선택합니다.  
  
7.  **조건** 탭을 클릭한 다음 **추가**를 클릭합니다. **속성** 아래에서 **개인 식별이 가능한 정보**를 선택합니다. **연산자** 아래에서 **같음**을 선택합니다. **값** 아래에서 **높음**을 선택합니다. **확인**을 클릭합니다.  
  
8.  **일정** 탭을 클릭합니다. 일정 섹션에서 **매주**를 클릭한 다음 **일요일**을 선택합니다. 매주 한 번 작업을 실행하면 서비스 중단 또는 기타 중단 이벤트로 인해 누락되었을 수 있는 문서를 발견할 수 있습니다.  
  
9. **연속 작업** 섹션에서 **새 파일에서 계속 실행**을 선택하고 **확인**을 클릭합니다. 이제 High PII라는 파일 관리 작업이 만들어졌습니다.  
  
![솔루션 가이드](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
$fmjRmsEncryption = New-FSRMFmjAction -Type 'Rms' -RmsTemplate 'Contoso Finance Admin Only'  
$fmjCondition1 = New-FSRMFmjCondition -Property 'PII_MS' -Condition 'Equal' -Value '5000'  
$date = get-date  
$schedule = New-FsrmScheduledTask -Time $date -Weekly @('Sunday')    
$fmj1=New-FSRMFileManagementJob -Name "High PII" -Description "Automatic RMS protection for high PII documents" -Namespace @('D:\Finance Documents') -Action $fmjRmsEncryption -Schedule $schedule -Continuous -Condition @($fmjCondition1)  
```  
  
## <a name="BKMK_4"></a>4 단계: 결과 보기  
작업에서 새 자동 분류 및 AD RMS 보호 규칙을 확인 하는 차례입니다. 이 단계에서는 문서 분류를 검토하고 문서의 콘텐츠를 변경할 때 문서 분류가 어떻게 변경되는지 확인합니다.  
  
#### <a name="to-view-the-results"></a>결과를 보려면  
  
1.  Hyper-V 관리자에서 ID_AD_FILE1에 연결합니다. Contoso\Administrator 암호로 사용 하 여 서버에 로그인 **pass@word1**합니다.  
  
2.  Windows 탐색기에서 D:\Finance Documents로 이동합니다.  
  
3.  Finance Memo 문서를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭한 다음 **분류** 탭을 클릭하여 현재 영향 속성에 값이 없는지 확인합니다. 클릭 **취소**합니다.  
  
4.  **Request for Approval to Hire**문서를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
5.  **분류** 탭을 클릭하고 현재 **개인 식별이 가능한 정보** 속성에 값이 없는지 확인합니다. 클릭 **취소**합니다.  
  
6.  CLIENT1로 전환합니다. 사용자가 로그인 및 다음 암호를 사용 하 여 Contoso\MReid로 로그인 **pass@word1**합니다.  
  
7.  바탕 화면에서 **Finance Documents** 공유 폴더를 엽니다.  
  
8.  **Finance Memo** 문서를 엽니다. 문서 아래쪽에 **Confidential**이 표시되어 있습니다. 이 문자열을 **Contoso Confidential**로 수정합니다. 문서를 저장하고 닫습니다.  
  
9. **Request for Approval to Hire** 문서를 엽니다. **Social Security#:** 섹션에 777-77-7777을 입력합니다. 문서를 저장하고 닫습니다.  
  
    > [!NOTE]  
    > 분류가 완료될 때까지 30초 정도 기다려야 할 수 있습니다.  
  
10. ID_AD_FILE1로 다시 전환합니다. Windows 탐색기에서 D:\Finance Documents로 이동합니다.  
  
11. Finance Memo 문서를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. **분류** 탭을 클릭합니다. 이제 영향 속성이 **높음**으로 설정된 것을 알 수 있습니다. 클릭 **취소**합니다.  
  
12. Request for Approval to Hire 문서를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
13. . **분류** 탭을 클릭합니다. 이제 개인 식별이 가능한 정보 속성이 **높음**으로 설정된 것을 알 수 있습니다. 클릭 **취소**합니다.  
  
## <a name="BKMK_5"></a>5 단계: AD RMS로 보호 확인  
  
#### <a name="to-verify-that-the-document-is-protected"></a>문서가 보호되는지 확인하려면  
  
1.  ID_AD_CLIENT1로 다시 전환합니다.  
  
2.  **Request for approval to Hire** 문서를 엽니다.  
  
3.  **확인** 을 클릭하여 문서에서 AD RMS 서버에 연결하도록 허용합니다.  
  
4.  문서에 주민 등록 번호가 포함되어 있으므로 이제 문서가 AD RMS로 보호된 것을 알 수 있습니다.  
  

