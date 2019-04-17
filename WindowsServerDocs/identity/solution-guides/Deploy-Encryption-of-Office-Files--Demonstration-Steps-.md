---
ms.assetid: 2c76e81a-c2eb-439f-a89f-7d3d70790244
title: "Office 파일 (데모 단계) 암호화를 배포 합니다."
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 529000c60a80ee33fc2aa7d09370d8ac1e06311c
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="deploy-encryption-of-office-files-demonstration-steps"></a>Office 파일 (데모 단계) 암호화를 배포 합니다.

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Contoso 금융 부서에 문서를 저장 하는 파일 서버 수 있습니다. 이 문서 일반 설명서 또는 높은 비즈니스 효과 (HBI) 있을 수 있습니다. 예를 들어 높은 비즈니스 영향을 미치지 Contoso 하 여 기밀 정보가 포함 된 모든 문서 간주 됩니다. Contoso의 모든 설명서에서 보호 최소한 있고 HBI 설명서 자녀가 적절 한 사람에 게 제한 인지 확인 하고자 합니다. 이렇게 하기 위해 파일 분류 Infrastructure (FCI) 및 Windows Server 2012에서 사용할 수 있는 AD RMS 사용 하 여 Contoso 탐험입니다. FCI를 사용 하 여 Contoso 모든 콘텐츠를 기반으로 파일 서버에 문서를 분류 되며 다음 AD RMS 적절 한 권한이 정책을 적용을 사용 합니다.  
  
이 경우 다음 단계를 수행 합니다.  
  
|작업|설명|  
|--------|---------------|  
|[속성 리소스를 사용 하도록 설정](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_1.1)|설정에서 **영향** 및 **개인 식별 정보** 리소스 속성 합니다.|  
|[분류 규칙 만들기](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_2)|다음 분류 규칙 만들기: **HBI 분류 규칙** 및 **PII 분류 규칙**합니다.|  
|[AD RMS 문서를 자동으로 보호를 사용 하는 파일 관리 작업](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_3)|자동으로 AD RMS 문서 (PII) 높은 개인 식별 정보를 보호 하는 데 사용 하는 파일 관리 작업을 만듭니다. FinanceAdmin 그룹의 회원만 높은 PII 포함 된 문서에 액세스할을 수 됩니다.|  
|[검색 결과 보기](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_4)|문서 분류를 검사 하 고에서 문서에 있는 콘텐츠를 변경 하면 변경 어떻게 확인 합니다. 또한 문서 AD RMS에 의해 보호 되는 방법을 확인 합니다.|  
|[AD RMS 보호를 확인 합니다.](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_5)|문서 AD RMS 보호를 확인 합니다.|  
|||  
  
## <a name="BKMK_1.1"></a>1 단계: 사용 리소스 속성  
  
#### <a name="to-enable-resource-properties"></a>속성 리소스를 사용 하도록 설정 하려면  
  
1.  Hyper-v 관리자 ID_AD_DC1 서버에 연결 됩니다. Contoso\Administrator 암호를 사용 하 여 서버에 로그인 **pass@word1**합니다.  
  
2.  클릭 하 고 열기 Active Directory 관리 센터 **트리 보기**합니다.  
  
3.  확장 **동적 액세스 제어**를 선택 하 고 **리소스 속성**합니다.  
  
4.  아래로 스크롤하여는 **영향** 속성의 **표시 이름** 열 합니다. 마우스 오른쪽 단추로 클릭 **영향**을 차례로 클릭 하 고 **활성화**합니다.  
  
5.  아래로 스크롤하여는 **개인 식별 정보** 속성의 **표시 이름** 열 합니다. 마우스 오른쪽 단추로 클릭 **개인 식별 정보**을 차례로 클릭 하 고 **활성화**합니다.  
  
6.  리소스 속성 게시 하는 **전체 리소스 목록**, 왼쪽된 창에서 클릭 **리소스 속성 나열**, 다음 두 번 클릭 하 고 **전체 리소스 속성 목록**합니다.  
  
7.  클릭 **추가**, 클릭 한 다음 아래로 스크롤하여 및 **영향** 목록에 추가 합니다. 에 대해 동일한 작업을 수행 **개인 식별 정보**합니다. 클릭 **확인** 를 두 번 합니다.  
  
![해결 방법 가이드](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.  
  
```  
Set-ADResourceProperty -Enabled:$true -Identity:"CN=Impact_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com"  
Set-ADResourceProperty -Enabled:$true -Identity:"CN=PII_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com" 
```  
  
## <a name="BKMK_2"></a>2 단계: 분류 규칙 만들기  
이 단계를 만드는 방법에 설명는 **중대 한 영향** 분류 규칙 합니다. 이 규칙이 문서의 콘텐츠를 검색 하 고 높은 업무에 미치는 영향에 있는 것으로이 문서를 분류 됩니다 "Contoso 기밀" 문자열 발견 되 면 합니다. 이 분류 낮은 업무에 미치는 영향의 이전에 지정 된 모든 분류를 무시 합니다.  
  
또한 인해 발생 한 **높은 PII** 규칙 합니다. 이 규칙의 문서의 콘텐츠를 검색 하 고 높은 PII 것으로 문서를 분류 사회 보장 번호 발견 되 면 합니다.  
  
#### <a name="to-create-the-high-impact-classification-rule"></a>효과적인 분류 규칙을 만들려면  
  
1.  Hyper-v 관리자 ID_AD_FILE1 서버에 연결 됩니다. Contoso\Administrator 암호를 사용 하 여 서버에 로그인 **pass@word1**합니다.  
  
2.  글로벌 리소스 속성 Active directory에서를 새로 고칩니다 해야 합니다. Windows PowerShell 및 유형 열고: `Update-FSRMClassificationPropertyDefinition`, ENTER 키를 누릅니다. Windows PowerShell 닫습니다.  
  
3.  파일 서버 리소스 관리자를 엽니다. 파일 서버 리소스 관리자를 열을 클릭 **시작**, 입력 **파일 서버 리소스 관리자**을 차례로 클릭 하 고 **파일 서버 리소스 관리자**합니다.  
  
4.  파일 서버 리소스 관리자의 왼쪽된 창에서 확장 **분류 관리**를 선택한 다음 **분류 규칙**합니다.  
  
5.  에 **작업** 창 클릭 **구성 분류 일정**합니다. 에 **자동 분류** 탭을 선택 하 고 **고정된 일정을 사용 하도록 설정**는 **요일**, 선택한 다음는 **새 파일에 대 한 지속적인 분류 허용** 확인란을 선택 합니다. 클릭 **확인**합니다.  
  
6.  에 **작업** 창 클릭 **분류 규칙 만들기**합니다. 그러면 열립니다는 **분류 규칙 만들기** 대화 상자 합니다.  
  
7.  에 **규칙 이름** 상자에 입력 **높은 업무에 영향을**합니다.  
  
8.  에 **설명** 상자에 입력 **문서 "Contoso 기밀" 문자열의 있는지 여부에 따라 업무에 큰 영향을에 있는지 확인 **  
  
9. 에 **범위** 탭을 클릭 **폴더 관리 속성을 설정**선택 **폴더 사용**, 클릭 **추가**, 클릭 한 다음 **검색**경로로 D:\Finance 문서를 검색을 클릭 **확인**, 라는 속성 값을 선택 합니다 **그룹 파일** 클릭 **닫기**합니다. 관리 속성 설정 되 면는 **규칙 범위** 탭을 선택 **그룹 파일**합니다.  
  
10. 클릭 하 고 **분류** 탭 합니다.  아래에서 **파일 속성 지정 하는 방법 선택**선택 **콘텐츠 분류자** 드롭다운 목록에서 합니다.  
  
11. 아래에서 **속성 파일에 지정을 선택**선택 **영향** 드롭다운 목록에서 합니다.  
  
12. 아래에서 **값 지정**선택 **높은** 드롭다운 목록에서 합니다.  
  
13. 클릭 **구성** 아래 **매개**합니다.  **분류 매개** 대화 상자에서 **식 형식을** 목록에서 선택 **문자열**합니다. 에 **식** 상자에 입력: **Contoso 기밀**을 차례로 클릭 하 고 **확인**합니다.  
  
14. 클릭 하 고 **평가 유형** 탭 합니다.  클릭 **다시 기존 속성 값을 확인**, 클릭 **덮어쓰기를**값을 클릭 한 다음 기존 **확인** 완료 합니다.  
  
![해결 방법 가이드](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.  
  
```  
Update-FSRMClassificationPropertyDefinition  
$date = Get-Date  
$AutomaticClassificationScheduledTask = New-FsrmScheduledTask -Time $date -Weekly @(3, 2, 4, 5,1,6,0) -RunDuration 0;  
Set-FsrmClassification -Continuous -schedule $AutomaticClassificationScheduledTask  
New-FSRMClassificationRule -Name "High Business Impact" -Property "Impact_MS" -Description "Determines if the document has a high business impact based on the presence of the string 'Contoso Confidential'" -PropertyValue "3000" -Namespace @("D:\Finance Documents") -ClassificationMechanism "Content Classifier" -Parameters @("StringEx=Min=1;Expr=Contoso Confidential") -ReevaluateProperty Overwrite  
```  
  
#### <a name="to-create-the-high-pii-classification-rule"></a>높은 PII 분류 규칙을 만들려면  
  
1.  Hyper-v 관리자 ID_AD_FILE1 서버에 연결 됩니다. Contoso\Administrator 암호를 사용 하 여 서버에 로그인 **pass@word1**합니다.  
  
2.  바탕 화면에서 라는 폴더를 열고 **정기적으로 표현**, 라는 텍스트 문서를 열면 뷰어에서 **RegEx SSN**합니다. 선택한 다음 일반 식 문자열 복사: **^ (건가요? 000)([0-7]\d{2}|7([0-7]\d|7[012])) ([-]?) (?! 00) \d\d\3 (건가요? 0000) \d {4} $**합니다. 이 문자열이 나중에 사용이 단계 지금이 설정을 켜 두면 클립보드 합니다.  
  
3.  파일 서버 리소스 관리자를 엽니다. 파일 서버 리소스 관리자를 열을 클릭 **시작**, 입력 **파일 서버 리소스 관리자**을 차례로 클릭 하 고 **파일 서버 리소스 관리자**합니다.  
  
4.  파일 서버 리소스 관리자의 왼쪽된 창에서 확장 **분류 관리**를 선택한 다음 **분류 규칙**합니다.  
  
5.  에 **작업** 창 클릭 **구성 분류 일정**합니다. 에 **자동 분류** 탭을 선택 하 고 **고정된 일정을 사용 하도록 설정**는 **요일**, 선택한 다음는 **새 파일에 대 한 지속적인 분류 허용** 확인란을 선택 합니다. 확인을 클릭 합니다.  
  
6.  에 **규칙 이름** 상자에 입력 **높은 PII**합니다. 에 **설명** 상자에 입력 **결정 문서에 있는 경우 높은 사회 보장 번호 있는지 여부에 따라 PII 합니다.**  
  
7.  클릭 하 고 **범위** 탭을 선택는 **그룹 파일** 확인란을 선택 합니다.  
  
8.  클릭 하 고 **분류** 탭 합니다.  아래에서 **파일 속성 지정 하는 방법 선택**선택 **콘텐츠 분류자** 드롭다운 목록에서 합니다.  
  
9. 아래에서 **속성 파일에 지정을 선택**선택 **개인 식별 정보** 드롭다운 목록에서 합니다.  
  
10. 아래에서 **값 지정**선택 **높은** 드롭다운 목록에서 합니다.  
  
11. 클릭 **구성** 아래 **매개**합니다.   
    에 **분류 매개**창에서는 **식 형식을** 목록에서 선택 **일반 식**합니다. 에 **식** 상자에 클립보드에서 텍스트를 붙여: **^ (건가요? 000)([0-7]\d{2}|7([0-7]\d|7[012])) ([-]?) (?! 00) \d\d\3 (건가요? 0000) \d {4} $**을 차례로 클릭 하 고 **확인**합니다.  
  
    > [!NOTE]  
    > 이 식 잘못 된 사회 보장 번호 수 있습니다. 이 통해 데모 가상 사회 보장 번호를 사용 합니다.  
  
12. 클릭 하 고 **평가 유형** 탭 합니다.  선택 **기존 속성 값 다시 평가**, **덮어쓰기를**기존 값을 클릭 한 다음 **확인** 완료 합니다.  
  
![해결 방법 가이드](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.  
  
```  
New-FSRMClassificationRule -Name "High PII" -Description "Determines if the document has a high PII based on the presence of a Social Security Number." -Property "PII_MS" -PropertyValue "5000" -Namespace @("D:\Finance Documents") -ClassificationMechanism "Content Classifier" -Parameters @("RegularExpressionEx=Min=1;Expr=^(?!000)([0-7]\d{2}|7([0-7]\d|7[012]))([ -]?)(?!00)\d\d\3(?!0000)\d{4}$") -ReevaluateProperty Overwrite  
```  
  
이제 두 분류 규칙 있어야 합니다.  
  
-   업무에 큰 영향  
  
-   높은 PII  
  
## <a name="BKMK_3"></a>3 단계: 파일 관리 작업 AD RMS 문서를 자동으로 보호를 사용 하 여  
이제는 내용에 따라 문서를 자동으로 분류 규칙을 만든 다음 단계 AD RMS 자신의 분류에 따라 특정 문서를 자동으로 보호를 사용 하는 파일 관리 작업을 만드는 것입니다. 이 단계를 자동으로 높은 PII 된 모든 문서를 보호 하는 파일 관리 작업을 만듭니다. FinanceAdmin 그룹의 회원만 높은 PII 포함 된 문서에 액세스할을 수 됩니다.  
  
#### <a name="to-protect-documents-with-ad-rms"></a>AD RMS 문서를 보호 하기 위해  
  
1.  Hyper-v 관리자 ID_AD_FILE1 서버에 연결 됩니다. Contoso\Administrator 암호를 사용 하 여 서버에 로그인 **pass@word1**합니다.  
  
2.  파일 서버 리소스 관리자를 엽니다. 파일 서버 리소스 관리자를 열을 클릭 **시작**, 입력 **파일 서버 리소스 관리자**을 차례로 클릭 하 고 **파일 서버 리소스 관리자**합니다.  
  
3.  왼쪽된 창에서 **파일 관리 작업**합니다. 에 **작업** 창, **파일 관리 작업 만들기**합니다.  
  
4.  에 **작업 이름:** 필드를 입력 **높은 PII**합니다. 에 **설명** 필드를 입력 **높은 PII 문서에 대 한 자동 RMS 보호**합니다.  
  
5.  클릭 하 고 **범위** 탭을 선택는 **그룹 파일** 확인란을 선택 합니다.  
  
6.  클릭 하 고 **알림** 탭 합니다. 아래에서 **종류**선택 **RMS 암호화**합니다. 클릭 **찾아보기** 템플릿의 선택한 후에 **Contoso 금융 관리자만 해당** 서식 합니다.  
  
7.  클릭 하 고 **조건** 탭을 클릭 한 다음 **추가**합니다. 아래에서 **속성**선택 **개인 식별 정보**합니다. 아래에서 **통신사**선택 **같은**합니다. 아래에서 **값**선택 **높은**합니다. 클릭 **확인**합니다.  
  
8.  클릭 하 고 **일정** 탭 합니다. **일정** 섹션에서 클릭 **매주**를 선택한 다음 **일요일**합니다. 작업 주 한 번 실행 서비스 중단 또는 기타 갑작스러운 이벤트 인해 누락 되었을 수 있는 모든 문서를 반영 하는 것을 보장 합니다.  
  
9. 에 **계속 해 서 작업** 섹션을 **작업에 계속 해 서 새 파일을 실행**을 차례로 클릭 하 고 **확인**합니다. 이제 높은 PII 라는 파일 관리 작업이 있어야 합니다.  
  
![해결 방법 가이드](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.  
  
```  
$fmjRmsEncryption = New-FSRMFmjAction -Type 'Rms' -RmsTemplate 'Contoso Finance Admin Only'  
$fmjCondition1 = New-FSRMFmjCondition -Property 'PII_MS' -Condition 'Equal' -Value '5000'  
$date = get-date  
$schedule = New-FsrmScheduledTask -Time $date -Weekly @('Sunday')    
$fmj1=New-FSRMFileManagementJob -Name "High PII" -Description "Automatic RMS protection for high PII documents" -Namespace @('D:\Finance Documents') -Action $fmjRmsEncryption -Schedule $schedule -Continuous -Condition @($fmjCondition1)  
```  
  
## <a name="BKMK_4"></a>4 단계: 결과 보기  
실행 중인 새 자동 분류 및 AD RMS 보호 규칙 흘 낏 하도록입니다. 이 단계 문서 분류 검사 하 고에서 문서에 있는 콘텐츠를 변경 하면 변경 어떻게 확인 합니다.  
  
#### <a name="to-view-the-results"></a>결과를 보려면  
  
1.  Hyper-v 관리자 ID_AD_FILE1 서버에 연결 됩니다. Contoso\Administrator 암호를 사용 하 여 서버에 로그인 **pass@word1**합니다.  
  
2.  Windows 탐색기, D:\Finance 문서를 이동 합니다.  
  
3.  금융 메모 문서를 마우스 오른쪽 단추로 클릭 한 **속성**합니다. 클릭 하 고 **분류** 탭 및 영향을 속성 값 현재에 알림 합니다. 클릭 **취소**합니다.  
  
4.  마우스 오른쪽 단추로 클릭는 **승인 르 문서에 대 한 요청**를 선택한 다음 **속성**합니다.  
  
5.  클릭 하 고 **분류** 탭을 선택한 다음에 유의 **개인 식별 정보 속성** 현재 값이 없는 합니다. 클릭 **취소**합니다.  
  
6.  CLIENT1으로 전환 합니다. 로그인 되어 있는 모든 사용자 끄기 서명 하 고 다음 암호로 Contoso\MReid로 로그인 **pass@word1**합니다.  
  
7.  바탕 화면에서 열에서 **금융 문서** 공유 폴더 합니다.  
  
8.  열려 있는 **금융 메모** 문서 합니다. 문서 아래쪽 단어가 표시는 **기밀**합니다. 읽기 수정: **Contoso 기밀**합니다. 문서를 저장 하 고 닫습니다.  
  
9. 열려 있는 **르 승인에 대 한 요청이** 문서 합니다. 에 **사회 보안 #:** 섹션에서 입력: 777-77-7777 합니다. 문서를 저장 하 고 닫습니다.  
  
    > [!NOTE]  
    > 발생 하는 분류 30 초 정도 기다립니다 해야 할 수 있습니다.  
  
10. ID_AD_FILE1 다시 전환 합니다. Windows 탐색기, D:\Finance 문서를 이동 합니다.  
  
11. 금융 메모 문서를 마우스 오른쪽 단추로 클릭 한 **속성**합니다. 클릭 하 고 **분류** 탭 합니다. 알림이 표시 되는 **영향** 속성을 설정한 이제 **높은**합니다. 클릭 **취소**합니다.  
  
12. 이 르 문서를 클릭 승인에 대 한 요청을 마우스 오른쪽 단추로 클릭 **속성**합니다.  
  
13. . 클릭 하 고 **분류** 탭 합니다. 알림이 표시 되는 **개인 식별 정보** 속성을 설정한 이제 **높은**합니다. 클릭 **취소**합니다.  
  
## <a name="BKMK_5"></a>5 단계: AD RMS로 보호를 확인 합니다.  
  
#### <a name="to-verify-that-the-document-is-protected"></a>문서 보호 되 고 있는지 확인 하려면  
  
1.  ID_AD_CLIENT1 다시 전환 합니다.  
  
2.  열려 있는 **르 승인에 대 한 요청이** 문서 합니다.  
  
3.  클릭 **확인** 문서 AD RMS 서버에 연결할 수 있도록 합니다.  
  
4.  이제 사회 보장 번호 포함 되어 있으므로 문서 AD RMS로 보호 된 있는지 확인할 수 있습니다.  
  

