---
ms.assetid: ee008835-7d3b-4977-adcb-7084c40e5918
title: "보유 한 정보 (데모 단계) 파일 서버에 구현 배포"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e0f79dd72190888340144bc5c109ee31fa301937
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="deploy-implementing-retention-of-information-on-file-servers-demonstration-steps"></a>보유 한 정보 (데모 단계) 파일 서버에 구현 배포

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

폴더에 대 한 보존 기간을 설정 하 고 파일 분류 인프라와 파일 서버 리소스 관리자를 사용 하 여 법적 대기 파일을 저장 수 있습니다.  
  
**이 문서에서**  
  
-   [필수](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Prereqs)  
  
-   [1 단계: 속성 정의 리소스 만들기](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step1)  
  
-   [2 단계: 구성 알림](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md#BKMK_Step2)  
  
-   [3 단계: 만들기 파일 관리 작업](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step3)  
  
-   [4 단계: 수동으로 파일을을 분류합니다](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md#BKMK_Step4)  
  
> [!NOTE]  
> 이 항목에 설명 된 절차 일부 자동화 데 사용할 수 있는 샘플 Windows PowerShell cmdlet 포함 되어 있습니다. 자세한 내용은 참조 [사용 하 여 Cmdlet](https://go.microsoft.com/fwlink/p/?linkid=230693)합니다.  
  
## <a name="prerequisites"></a>필수  
이 항목의 단계 만료 알림이 파일에 대 한 구성 SMTP 서버 가정 합니다.  
  
## <a name="BKMK_Step1"></a>1 단계: 속성 정의 리소스 만들기  
저희이 단계에서 파일 분류 Infrastructure 리소스 속성 이러한 태그는 네트워크 공유 폴더에서 검색 된 파일을 사용할 수 있도록 보존 기간와 검색 리소스 속성 수 있도록 합니다.  
  
[Windows PowerShell를 사용 하 여이 단계를 수행 합니다.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)  
  
#### <a name="to-create-resource-property-definitions"></a>속성 정의 리소스를 만들려면  
  
1.  도메인 컨트롤러 서버에로 로그인 도메인 관리자 보안 그룹의 회원 합니다.  
  
2.  관리 센터를 Active Directory를 엽니다. 서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **Active Directory 관리 센터**합니다.  
  
3.  확장 **동적 액세스 제어**을 차례로 클릭 하 고 **리소스 속성**합니다.  
  
4.  마우스 오른쪽 단추로 클릭 **보존 기간**을 차례로 클릭 하 고 **활성화**합니다.  
  
5.  마우스 오른쪽 단추로 클릭 **검색**을 차례로 클릭 하 고 **사용**합니다.  
  
![해결 방법 가이드](media/Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.  
  
```  
Set-ADResourceProperty -Enabled:$true -Identity:'CN=RetentionPeriod_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'  
Set-ADResourceProperty -Enabled:$true -Identity:'CN=Discoverability_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'  
```  
  
## <a name="BKMK_Step2"></a>2 단계: 구성 알림  
이 단계를 사용 하 여 파일 서버 리소스 관리자 콘솔 SMTP 서버, 기본 관리자 메일 주소와 보고서에서 보낸 기본 메일 주소를 구성 합니다.  
  
[Windows PowerShell를 사용 하 여이 단계를 수행 합니다.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)  
  
#### <a name="to-configure-notifications"></a>알림을 구성 하려면  
  
1.  관리자 보안 그룹의 회원으로 파일 서버에 로그인 합니다.  
  
2.  Windows PowerShell 명령 프롬프트에 입력 **업데이트 FsrmClassificationPropertyDefinition**, ENTER 키를 누릅니다. 이 파일 서버에 도메인 컨트롤러에서 생성 된 속성 정의 동기화 됩니다.  
  
3.  파일 서버 리소스 관리자를 엽니다. 서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **파일 서버 리소스 관리자**합니다.  
  
4.  마우스 오른쪽 단추로 클릭 **파일 서버 리소스 관리자 (로컬)**을 차례로 클릭 하 고 **옵션 구성**합니다.  
  
5.  에 **메일 알림** 탭에서 다음을 구성 합니다.  
  
    -   에 **SMTP 서버 이름 또는 IP 주소** 상자 네트워크에서 SMTP 서버의 이름을 입력 합니다.  
  
    -   에 **기본 수신 관리자** 상자 알림을 받아야 관리자의 메일 주소를 입력 합니다.  
  
    -   에 **"에서" 메일 주소 기본** 상자, 알림을 보내는 데 사용할 해야 하는 메일 주소를 입력 합니다.  
  
6.  클릭 **확인**합니다.  
  
![해결 방법 가이드](media/Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.  
  
```  
Set-FsrmSetting -SmtpServer IP address of SMTP server -FromEmailAddress "FromEmailAddress" -AdminEmailAddress "AdministratorEmailAddress"  
```  
  
## <a name="BKMK_Step3"></a>3 단계: 만들기 파일 관리 작업  
이 단계에서 달의 마지막 날에 실행 되 고 모든 파일은 다음 조건와 만료 되는 파일 관리 작업을 만들려면 파일 서버 리소스 관리자 콘솔 사용:  
  
-   파일 법적 보류 중으로 분류 되지 않습니다.  
  
-   장기 보존 기간 하는 데로 파일 분류 됩니다.  
  
-   파일에서 지난 10 년 동안 하지 수정 되었습니다.  
  
[Windows PowerShell를 사용 하 여이 단계를 수행 합니다.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep3)  
  
#### <a name="to-create-a-file-management-task"></a>파일 관리 작업을 만들려면  
  
1.  관리자 보안 그룹의 회원으로 파일 서버에 로그인 합니다.  
  
2.  파일 서버 리소스 관리자를 엽니다. 서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **파일 서버 리소스 관리자**합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **파일 관리 작업**을 차례로 클릭 하 고 **파일 관리 작업 만들기**합니다.  
  
4.  에 **일반** 탭에 있는 **작업 이름** 상자에 파일 관리 작업 보존 작업 등의 이름을 입력 합니다.  
  
5.  에 **범위** 탭을 클릭 **추가**, D:\Finance 문서 등이 규칙에 포함 되는 폴더를 선택 합니다.  
  
6.  에 **알림** 탭에 **종류** 상자를 클릭 **만료 파일**합니다. 에 **만료 디렉터리** 상자에 만료 된 파일을 이동 있는 로컬 파일 서버에 경로 폴더를 입력 합니다. 이 폴더에 파일 서버 관리자 액세스 권한을 부여 하 액세스 제어 목록이 있어야 합니다.  
  
7.  에 **알림** 탭을 클릭 **추가**합니다.  
  
    -   선택는 **다음 관리자에 게 메일 보내기** 확인란을 선택 합니다.  
  
    -   선택는 **영향을 받는 파일을 사용자에 게 메일을 보낼** 확인란을 선택한 다음 클릭 **확인**합니다.  
  
8.  에 **조건** 탭을 클릭 **추가**, 다음 속성 추가 하 고 다음과 같습니다.  
  
    -   에 **속성** 목록에서 클릭 **검색**합니다. 에 **통신사** 목록에서 클릭 **같지**합니다. 에 **값** 목록에서 클릭 **길게**합니다.  
  
    -   에 **속성** 목록에서 클릭 **보존 기간**합니다. 에 **통신사** 목록에서 클릭 **같은**합니다. 에 **값** 목록에서 클릭 **장기**합니다.  
  
9. 에 **조건** 탭을 선택 하 고는 **일 이후 수정한** 확인란을 선택한 다음 값으로 설정 **3650**합니다.  
  
10. 에 **일정** 탭을 클릭는 **월별** 옵션을 선택한 다음는 **마지막** 확인란을 선택 합니다.  
  
11. 클릭 **확인**합니다.  
  
![해결 방법 가이드](media/Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.  
  
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
  
## <a name="BKMK_Step4"></a>4 단계: 수동으로 파일을을 분류합니다  
이 단계에서 수동으로 법적 길게에 파일을을 분류 했습니다. 이 파일의 상위 폴더 장기 보존 마침표 분류 됩니다.  
  
#### <a name="to-manually-classify-a-file"></a>파일을을 분류 수동으로 하기  
  
1.  관리자 보안 그룹의 회원으로 파일 서버에 로그인 합니다.  
  
2.  3 단계에서에서 만든 파일 관리 작업 범위에서 구성 된 폴더로 이동 합니다.  
  
3.  폴더를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **속성**합니다.  
  
4.  에 **분류** 탭을 클릭 **보존 기간**, 클릭 **장기**을 차례로 클릭 하 고 **확인**합니다.  
  
5.  해당 폴더에 파일을 마우스 오른쪽 단추로 클릭 한 다음 한 **속성**합니다.  
  
6.  에 **분류** 탭을 클릭 **검색 기능을**, 클릭 **길게**, 클릭 **적용**을 차례로 클릭 하 고 **확인**합니다.  
  
7.  파일 서버에서 파일 서버 리소스 관리자 본체를 사용 하 여 파일 관리 작업을 실행 합니다. 파일 관리 작업이 완료 되 면 폴더 확인 하 고 파일을 만료 디렉터리에 이동할 수 없습니다.  
  
8.  해당 폴더를 내 같은 파일을 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **속성**합니다.  
  
9. 에 **분류** 탭을 클릭 **검색 기능을**, 클릭 **해당 없음**, 클릭 **적용**, 클릭 한 다음 **확인**합니다.  
  
10. 파일 서버에서 파일 관리 작업 파일 서버 리소스 관리자 본체를 사용 하 여 다시 실행 합니다. 파일 관리 작업이 완료 되 면 폴더를 확인 하 고 만료 디렉터리에 해당 파일을 이동한 있는지 확인 합니다.  
  
## <a name="BKMK_Links"></a>참조 하십시오  
  
-   [파일 서버에 보유 한 정보를 구현 하는 시나리오:](Scenario--Implement-Retention-of-Information-on-File-Servers.md)  
  
-   [보유 한 파일 서버에 대 한 정보에 대 한 계획](assetId:///edf13190-7077-455a-ac01-f534064a9e0c)  
  
-   [동적 액세스 제어: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  
  

