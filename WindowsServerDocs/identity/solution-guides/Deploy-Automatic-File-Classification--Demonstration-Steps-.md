---
ms.assetid: 01988844-df02-4952-8535-c87aefd8a38a
title: "자동으로 파일 분류 (데모 단계)를 배포 합니다."
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1c5c0fa221e0d7375216426f838ba37bee852984
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="deploy-automatic-file-classification-demonstration-steps"></a>자동으로 파일 분류 (데모 단계)를 배포 합니다.

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 Active Directory에 속성 리소스를 사용 하도록 설정, 파일 서버에 분류 규칙을 만들 다음 리소스 속성 파일 서버에서 파일에 대 한 값을 지정 하는 방법을 설명 합니다. 이 예는 다음과 같은 분류 규칙 만들어집니다.  
  
-   여러 문자열 ' Contoso 기밀.'에 대 한 파일을 검색 하는 콘텐츠 분류 규칙 파일에는 문자열 발견 되 면 영향 리소스 속성 파일 높음으로 설정 되어 있습니다.  
  
-   여러 한 파일에 10 시간 이상 사회 보장 번호와 일치 하는 일반적인 식에 대 한 파일을 검색 하는 콘텐츠 분류 규칙 합니다. 패턴 발견 되 면 개인 식별 정보를 편리 파일로 분류 되는 및 개인 식별 정보 리소스 속성 높음으로 설정 되어 있습니다.  
  
**이 문서에서**  
  
-   [1 단계: 속성 정의 리소스 만들기](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step1)  
  
-   [2 단계: 문자열 콘텐츠 분류 규칙 만들기](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step2)  
  
-   [3 단계: 일반 식 콘텐츠 분류 규칙 만들기](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step3)  
  
-   [4 단계: 파일은 분류 확인](Deploy-Automatic-File-Classification--Demonstration-Steps-.md#BKMK_Step4)  
  
> [!NOTE]  
> 이 항목에 설명 된 절차 일부 자동화 데 사용할 수 있는 샘플 Windows PowerShell cmdlet 포함 되어 있습니다. 자세한 내용은 참조 [사용 하 여 Cmdlet](https://go.microsoft.com/fwlink/p/?linkid=230693)합니다.  
  
## <a name="BKMK_Step1"></a>1 단계: 속성 정의 리소스 만들기  
영향 및 개인 식별 가능 정보 리소스 속성 파일 분류 인프라 이러한 리소스 속성 태그 네트워크 공유 폴더에서 검색 된 파일을 사용할 수 있도록 활성화 됩니다.  
  
[Windows PowerShell를 사용 하 여이 단계를 수행 합니다.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)  
  
#### <a name="to-create-resource-property-definitions"></a>속성 정의 리소스를 만들려면  
  
1.  도메인 컨트롤러 서버에로 로그인 도메인 관리자 보안 그룹의 회원 합니다.  
  
2.  관리 센터를 Active Directory를 엽니다. 서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **Active Directory 관리 센터**합니다.  
  
3.  확장 **동적 액세스 제어**을 차례로 클릭 하 고 **리소스 속성**합니다.  
  
4.  마우스 오른쪽 단추로 클릭 **영향**을 차례로 클릭 하 고 **활성화**합니다.  
  
5.  마우스 오른쪽 단추로 클릭 **개인 식별 정보**을 차례로 클릭 하 고 **활성화**합니다.  
  
![해결 방법 가이드](media/Deploy-Automatic-File-Classification--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.  
  
```  
Set-ADResourceProperty '"Enabled:$true '"Identity:'CN=Impact_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'   
Set-ADResourceProperty '"Enabled:$true '"Identity:'CN=PII_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'  
```  
  
## <a name="BKMK_Step2"></a>2 단계: 문자열 콘텐츠 분류 규칙 만들기  
문자열 콘텐츠 분류 규칙 특정 문자열로 대 한 파일을 검색합니다. 문자열 발견 되 면 리소스 속성 값 구성할 수 있습니다. 여기에서 했습니다 검색 네트워크 공유 폴더에서 각 파일 하 고 ' Contoso 기밀.' 문자열에 대 한 확인 문자열 발견 되 면 업무에 큰 영향을 하는 것으로 관련된 된 파일 분류 됩니다.  
  
[Windows PowerShell를 사용 하 여이 단계를 수행 합니다.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)  
  
#### <a name="to-create-a-string-content-classification-rule"></a>문자열 콘텐츠 분류 규칙을 만들려면  
  
1.  파일 서버에 관리자 보안 그룹의 회원으로 로그온 합니다.  
  
2.  Windows PowerShell 명령 프롬프트에 입력 **업데이트 FsrmClassificationPropertyDefinition** ENTER 키를 누릅니다. 이 파일 서버에 도메인 컨트롤러에서 만든 속성 정의 동기화 됩니다.  
  
3.  파일 서버 리소스 관리자를 엽니다. 서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **파일 서버 리소스 관리자**합니다.  
  
4.  확장 **분류 관리**를 마우스 오른쪽 단추로 클릭 **분류 규칙**을 차례로 클릭 하 고 **구성 분류 일정**합니다.  
  
5.  선택는 **고정된 일정을 사용 하도록 설정** 확인란을 선택 하 고는 **새 파일에 대 한 지속적인 분류 허용** 확인란을 실행 하는 분류 고 클릭 한 다음 요일 선택 **확인**합니다.  
  
6.  마우스 오른쪽 단추로 클릭 **분류 규칙**을 차례로 클릭 하 고 **분류 규칙 만들기**합니다.  
  
7.  에 **일반** 탭에 **규칙 이름** 상자에 같은 규칙 이름을 입력 **Contoso 기밀**합니다.  
  
8.  에 **범위** 탭을 클릭 **추가**, D:\Finance 문서 등이 규칙에 포함 되는 폴더를 선택 합니다.  
  
    > [!NOTE]  
    > 범위에 대 한 동적 네임 스페이스를 선택할 수 있습니다. 분류 규칙에 대 한 동적 이름 공간에 대 한 자세한 내용은 참조 [새로운 파일 서버 리소스 관리자 \[redirected\ Windows Server 2012에서에서 소식]](assetId:///d53c603e-6217-4b98-8508-e8e492d16083)합니다.  
  
9. 에 **분류** 탭에서 다음을 구성 합니다.  
  
    -   에 **속성 파일을 지정 하는 방법을 선택** 상자에 되도록 **콘텐츠 분류자** 을 선택 합니다.  
  
    -   에 **속성 파일에 지정을 선택** 상자를 클릭 **영향**합니다.  
  
    -   에 **값 지정** 상자를 클릭 **높은**합니다.  
  
10. 아래에서 **매개** 클릭 제목, **구성**합니다.  
  
11. 에 **식 형식을** 열을 **문자열**합니다.  
  
12. **식** 열, 형식 **Contoso 기밀**을 차례로 클릭 하 고 **확인**합니다.  
  
13. 에 **평가 유형** 탭을 선택 하 고는 **다시 기존 속성 값을 확인** 확인란을 클릭 **기존 값은 덮어쓰기를**, 클릭 한 다음 **확인**합니다.  
  
![해결 방법 가이드](media/Deploy-Automatic-File-Classification--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.  
  
```  
$date = Get-Date  
$AutomaticClassificationScheduledTask = New-FsrmScheduledTask -Time $date -Weekly @(3, 2, 4, 5,1,6,0) -RunDuration 0;$AutomaticClassificationScheduledTask  
Set-FsrmClassification -Continuous -schedule $AutomaticClassificationScheduledTask  
New-FSRMClassificationRule -Name 'Contoso Confidential' -Property "Impact_MS" -PropertyValue "3000" -Namespace @('D:\Finance Documents') -ClassificationMechanism "Content Classifier" -Parameters @("StringEx=Min=1;Expr=Contoso Confidential") -ReevaluateProperty Overwrite  
```  
  
## <a name="BKMK_Step3"></a>3 단계: 일반 식 콘텐츠 분류 규칙 만들기  
일반 식 분류 규칙 패턴 일반 식와 일치 하는 파일을 검색 합니다. 정규 식와 일치 하는 문자열 발견 되 면 리소스 속성 값 구성할 수 있습니다. 여기에서 우리 검색 네트워크 공유 폴더에서 각 파일 하 고 패턴을 사회 보장 번호 (XXX-XX-XXXX)와 일치 하는 문자열을 찾으세요. 패턴 발견 되 면 개인 식별 정보를 편리로 연결된 된 파일 분류 됩니다.  
  
[Windows PowerShell를 사용 하 여이 단계를 수행 합니다.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep3)  
  
#### <a name="to-create-a-regular-expression-content-classification-rule"></a>일반 식 콘텐츠 분류 규칙을 만들려면  
  
1.  관리자 보안 그룹의 회원으로 파일 서버에 로그인 합니다.  
  
2.  Windows PowerShell 명령 프롬프트에 입력 **업데이트 FsrmClassificationPropertyDefinition**, ENTER 키를 누릅니다. 이 파일 서버에 도메인 컨트롤러에서 생성 된 속성 정의 동기화 됩니다.  
  
3.  파일 서버 리소스 관리자를 엽니다. 서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **파일 서버 리소스 관리자**합니다.  
  
4.  마우스 오른쪽 단추로 클릭 **분류 규칙**을 차례로 클릭 하 고 **분류 규칙 만들기**합니다.  
  
5.  에 **일반** 탭에 있는 **규칙 이름** 상자 분류 규칙 PII 규칙 등의 이름을 입력 합니다.  
  
6.  에 **범위** 탭을 클릭 **추가**, 다음 D:\Finance 문서 등이 규칙에 포함 되는 폴더를 선택 하 고 있습니다.  
  
7.  에 **분류** 탭에서 다음을 구성 합니다.  
  
    -   에 **속성 파일을 지정 하는 방법을 선택** 상자에 되도록 **콘텐츠 분류자** 을 선택 합니다.  
  
    -   에 **속성 파일에 지정을 선택** 상자를 클릭 **개인 식별 정보**합니다.  
  
    -   에 **값 지정** 상자를 클릭 **높은**합니다.  
  
8.  아래에서 **매개** 클릭 제목, **구성**합니다.  
  
9. 에 **식 형식을** 열을 **일반 식**합니다.  
  
10. 에 **식** 유형, 열 **^ (건가요? 000)([0-7]\d{2}|7([0-7]\d|7[012])) ([-]?) (?! 00) \d\d\3 (건가요? \d {4} $ 0000)**  
  
11. 에 **최소 발생** 유형, 열 **10**, 클릭 한 다음 **확인**합니다.  
  
12. 에 **평가 유형** 탭을 선택 하 고는 **다시 기존 속성 값을 확인** 확인란을 클릭 **기존 값은 덮어쓰기를**, 클릭 한 다음 **확인**합니다.  
  
![해결 방법 가이드](media/Deploy-Automatic-File-Classification--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.  
  
```  
New-FSRMClassificationRule -Name "PII Rule" -Property "PII_MS" -PropertyValue "5000" -Namespace @('D:\Finance Documents') -ClassificationMechanism "Content Classifier" -Parameters @("RegularExpressionEx=Min=10;Expr=^(?!000)([0-7]\d{2}|7([0-7]\d|7[012]))([ -]?)(?!00)\d\d\3(?!0000)\d{4}$") -ReevaluateProperty Overwrite  
```  
  
## <a name="BKMK_Step4"></a>4 단계: 파일 잘못 분류 됩니다 확인  
파일 속성 만든 분류 규칙에 지정 된 폴더에서 파일을 확인 하 여 제대로 분류 됩니다 확인할 수 있습니다.  
  
#### <a name="to-verify-that-the-files-are-classified-correctly"></a>파일이 제대로 분류 됩니다 확인 하려면  
  
1.  파일 서버에서 파일 서버 리소스 관리자를 사용 하 여 분류 규칙을 실행 합니다.  
  
    1.  클릭 **분류 관리**를 마우스 오른쪽 단추로 클릭 **분류 규칙**을 차례로 클릭 하 고 **실행 분류 된 모든 지금 규칙**합니다.  
  
    2.  클릭 하 고 **분류 완료 될 때까지 기다리는** 옵션을 클릭 한 다음 **확인**합니다.  
  
    3.  자동 분류 보고서를 닫습니다.  
  
    4.  다음 명령을 사용 하 여 Windows PowerShell를 사용 하 여이 수행할 수 있습니다: **시작 FSRMClassification ' "RunDuration 0-확인: $false**  
  
2.  분류 규칙 D:\Finance 문서 등에 지정 된 폴더로 이동 합니다.  
  
3.  해당 폴더의 파일을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **속성**합니다.  
  
4.  클릭 하 고 **분류** 탭 하 고 파일 잘못 분류 되 확인 합니다.  
  
## <a name="BKMK_Links"></a>참조 하십시오  
  
-   [시나리오: 분류를 사용 하 여 사용자의 데이터에 대 한 정보 가져오기](Scenario--Get-Insight-into-Your-Data-by-Using-Classification.md)  
  
-   [자동으로 파일 분류 계획](assetId:///e3c3bb4b-3034-42b7-b391-8ef5f5851955)  
  
-   [동적 액세스 제어: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  
  

