---
ms.assetid: ee008835-7d3b-4977-adcb-7084c40e5918
title: Deploy Implementing Retention of Information on File Servers (Demonstration Steps)
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 994eadfa205b62c5a512ab130c71fa6c22d1cff6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357536"
---
# <a name="deploy-implementing-retention-of-information-on-file-servers-demonstration-steps"></a>Deploy Implementing Retention of Information on File Servers (Demonstration Steps)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

파일 분류 인프라 및 파일 서버 리소스 관리자를 사용하여 폴더에 대한 보존 기간을 설정하고 파일에 법적 보존을 적용할 수 있습니다.  
  
**이 문서의**  
  
-   [필수 구성 요소](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Prereqs)  
  
-   [1 단계: 리소스 속성 정의 만들기](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step1)  
  
-   [2 단계: 알림 구성](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md#BKMK_Step2)  
  
-   [3 단계: 파일 관리 작업 만들기](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step3)  
  
-   [4 단계: 수동으로 파일 분류](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md#BKMK_Step4)  
  
> [!NOTE]  
> 이 항목에는 설명한 절차의 일부를 자동화하는 데 사용할 수 있는 샘플 Windows PowerShell cmdlet이 포함되어 있습니다. 자세한 내용은 참조 [Cmdlet를 사용 하 여](https://go.microsoft.com/fwlink/p/?linkid=230693)합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
이 항목의 단계에서는 SMTP 서버에서 파일 만료 알림을 구성한 것으로 가정합니다.  
  
## <a name="BKMK_Step1"></a>1 단계: 리소스 속성 정의 만들기  
이 단계에서는 파일 분류 인프라에서 이러한 리소스 속성을 사용 하 여 네트워크 공유 폴더에서 검사 된 파일에 태그를 지정할 수 있도록 보존 기간 및 검색 기능 리소스 속성을 사용 하도록 설정 합니다.  
  
[Windows PowerShell을 사용 하 여이 단계 수행](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)  
  
#### <a name="to-create-resource-property-definitions"></a>리소스 속성 정의를 만들려면  
  
1.  도메인 컨트롤러에서 Domain Admins 보안 그룹의 구성원으로 서버에 로그인합니다.  
  
2.  Active Directory 관리 센터를 엽니다. 서버 관리자에서 **도구**를 클릭한 다음 **Active Directory 관리 센터**를 클릭합니다.  
  
3.  **동적 Access Control**을 확장하고 **리소스 속성**을 클릭합니다.  
  
4.  **보존 기간**을 마우스 오른쪽 단추로 클릭한 다음 **사용**을 클릭합니다.  
  
5.  **검색 기능**을 마우스 오른쪽 단추로 클릭한 다음 **사용**을 클릭합니다.  
  
![솔루션 가이드](media/Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em>***  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
Set-ADResourceProperty -Enabled:$true -Identity:'CN=RetentionPeriod_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'  
Set-ADResourceProperty -Enabled:$true -Identity:'CN=Discoverability_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'  
```  
  
## <a name="BKMK_Step2"></a>2 단계: 알림 구성  
이 단계에서는 파일 서버 리소스 관리자 콘솔을 사용하여 SMTP 서버, 기본 관리자 메일 주소 및 보고서를 보낼 기본 메일 주소를 구성합니다.  
  
[Windows PowerShell을 사용 하 여이 단계 수행](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)  
  
#### <a name="to-configure-notifications"></a>알림을 구성하려면  
  
1.  Administrators 보안 그룹의 구성원으로 파일 서버에 로그인합니다.  
  
2.  Windows PowerShell 명령 프롬프트에서 **Update-FsrmClassificationPropertyDefinition**을 입력하고 Enter 키를 누릅니다. 그러면 도메인 컨트롤러에서 만들어진 속성 정의가 파일 서버에 동기화됩니다.  
  
3.  파일 서버 리소스 관리자를 엽니다. 서버 관리자에서 **도구**를 클릭한 다음 **파일 서버 리소스 관리자**를 클릭합니다.  
  
4.  **파일 서버 리소스 관리자(로컬)** 를 마우스 오른쪽 단추로 클릭한 다음 **옵션 구성**을 클릭합니다.  
  
5.  **전자 메일 알림** 탭에서 다음을 구성합니다.  
  
    -   **SMTP 서버 이름 또는 IP 주소** 상자에 네트워크의 SMTP 서버 이름을 입력합니다.  
  
    -   **기본 수신 관리자** 상자에 알림을 받아야 하는 관리자의 전자 메일 주소를 입력합니다.  
  
    -   에 **기본 "보낸 사람" 전자 메일 주소** 상자에 알림을 보내는 데 사용 해야 하는 전자 메일 주소를 입력 합니다.  
  
6.  **확인**을 클릭합니다.  
  
![솔루션 가이드](media/Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em>***  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
Set-FsrmSetting -SmtpServer IP address of SMTP server -FromEmailAddress "FromEmailAddress" -AdminEmailAddress "AdministratorEmailAddress"  
```  
  
## <a name="BKMK_Step3"></a>3 단계: 파일 관리 작업 만들기  
이 단계에서는 파일 서버 리소스 관리자 콘솔을 사용하여 매월 마지막 날에 실행되고 다음 조건에 해당하는 모든 파일을 만료하는 파일 관리 작업을 만듭니다.  
  
-   법적 보존되도록 분류되지 않은 파일  
  
-   장기 보존 기간이 설정된 것으로 분류된 파일  
  
-   지난 10일 동안 수정되지 않은 파일  
  
[Windows PowerShell을 사용 하 여이 단계 수행](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep3)  
  
#### <a name="to-create-a-file-management-task"></a>파일 관리 작업을 만들려면  
  
1.  Administrators 보안 그룹의 구성원으로 파일 서버에 로그인합니다.  
  
2.  파일 서버 리소스 관리자를 엽니다. 서버 관리자에서 **도구**를 클릭한 다음 **파일 서버 리소스 관리자**를 클릭합니다.  
  
3.  **파일 관리 작업**을 마우스 오른쪽 단추로 클릭한 다음 **파일 관리 작업 만들기**를 클릭합니다.  
  
4.  **일반** 탭의 **작업 이름** 상자에 파일 관리 작업의 이름(예: Retention Task)을 입력합니다.  
  
5.  **범위** 탭에서 **추가**를 클릭하고 이 규칙에 포함할 폴더(예: D:\Finance Documents)를 선택합니다.  
  
6.  **작업** 탭의 **유형** 상자에서 **파일 만료**를 클릭합니다. **만료 디렉터리** 상자에 만료된 파일을 이동할 로컬 파일 서버의 폴더 경로를 입력합니다. 이 폴더에는 파일 서버 관리자에게만 액세스 권한을 부여하는 액세스 제어 목록이 있어야 합니다.  
  
7.  **알림** 탭에서 **추가**를 클릭합니다.  
  
    -   **다음 관리자에게 전자 메일 보내기** 확인란을 선택합니다.  
  
    -   **영향을 받는 파일과 함께 사용자에게 메일 보내기** 확인란을 선택하고 **확인**을 클릭합니다.  
  
8.  **조건** 탭에서 **추가**를 클릭하여 다음 속성을 추가합니다.  
  
    -   **속성** 목록에서 **검색 기능**을 클릭합니다. **연산자** 목록에서 **같지 않음**을 클릭합니다. **값** 목록에서 **유지**를 클릭합니다.  
  
    -   **속성** 목록에서 **보존 기간**을 클릭합니다. **연산자** 목록에서 **같음**을 클릭합니다. **값** 목록에서 **장기**를 클릭합니다.  
  
9. **조건** 탭에서 **마지막으로 파일을 수정한 이후 경과일** 확인란을 선택하고 값을 **3650**으로 설정합니다.  
  
10. **일정** 탭에서 **매월** 옵션을 클릭하고 **마지막** 확인란 합니다.  
  
11. **확인**을 클릭합니다.  
  
![솔루션 가이드](media/Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em>***  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
$fmjexpiration = New-FSRMFmjAction -Type 'Expiration' -ExpirationFolder folder  
$fmjNotificationAction = New-FsrmFmjNotificationAction -Type Email -MailTo "[FileOwner],[AdminEmail]"  
$fmjNotification = New-FsrmFMJNotification -Days 10 -Action @($fmjNotificationAction)  
$fmjCondition1 = New-FSRMFmjCondition -Property 'Discoverability_MS' -Condition 'NotEqual' -Value "Hold" 
$fmjCondition2 = New-FSRMFmjCondition -Property 'RetentionPeriod_MS' -Condition 'Equal' -Value "Long-term"  
$fmjCondition3 = New-FSRMFmjCondition -Property 'File.DateLastAccessed' -Condition 'Equal' -Value 3650  
$date = get-date  
$schedule = New-FsrmScheduledTask -Time $date -Monthly @(-1)    
$fmj1=New-FSRMFileManagementJob -Name "Retention Task" -Namespace @('D:\Finance Documents') -Action $fmjexpiration -Schedule $schedule -Notification @($fmjNotification) -Condition @( $fmjCondition1, $fmjCondition2, $fmjCondition3)  
```  
  
## <a name="BKMK_Step4"></a>4 단계: 수동으로 파일 분류  
이 단계에서는 파일을 법적 보존되도록 수동으로 분류합니다. 이 파일의 부모 폴더는 장기 보존 기간으로 분류됩니다.  
  
#### <a name="to-manually-classify-a-file"></a>파일을 수동으로 분류하려면  
  
1.  Administrators 보안 그룹의 구성원으로 파일 서버에 로그인합니다.  
  
2.  3단계에서 만든 파일 관리 작업의 범위 내에 구성된 폴더로 이동합니다.  
  
3.  폴더를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **분류** 탭에서 **보존 기간**, **장기**, **확인**을 차례로 클릭합니다.  
  
5.  해당 폴더 내의 파일을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
6.  **분류** 탭에서 **검색 기능**, **유지**, **적용**, **확인**을 차례로 클릭합니다.  
  
7.  파일 서버에서 파일 서버 리소스 관리자 콘솔을 사용하여 파일 관리 작업을 실행합니다. 파일 관리 작업이 완료되면 폴더를 확인하고 파일이 만료 디렉터리로 이동되지 않았는지 확인합니다.  
  
8.  해당 폴더 내의 같은 파일을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
9. **분류** 탭에서 **검색 기능**, **적용할 수 없음**, **적용**, **확인**을 차례로 클릭합니다.  
  
10. 파일 서버에서 파일 서버 리소스 관리자 콘솔을 사용하여 파일 관리 작업을 다시 실행합니다. 파일 관리 작업이 완료되면 폴더를 확인하고 파일이 만료 디렉터리로 이동되었는지 확인합니다.  
  
## <a name="BKMK_Links"></a>참고 항목  
  
-   [시나리오: 파일 서버에 대 한 정보 보존 구현](Scenario--Implement-Retention-of-Information-on-File-Servers.md)  
  
-   [파일 서버에 대 한 정보 보존 계획](assetId:///edf13190-7077-455a-ac01-f534064a9e0c)  
  
-   [동적 Access Control: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  
  

