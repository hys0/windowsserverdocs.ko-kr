---
ms.assetid: b035e9f8-517f-432a-8dfb-40bfc215bee5
title: Deploy Access-Denied Assistance (Demonstration Steps)
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 5201441ba884fe4658b917919e60c7d20530341b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835584"
---
# <a name="deploy-access-denied-assistance-demonstration-steps"></a>Deploy Access-Denied Assistance (Demonstration Steps)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 액세스 거부 지원을 구성하고 제대로 작동하는지 확인하는 방법에 대해 설명합니다.  
  
**이 문서에서는**  
  
-   [1단계: 액세스 거부 지원 구성](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md#BKMK_1)  
  
-   [2단계: 전자 메일 알림 설정 구성](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md#BKMK_2)  
  
-   [3 단계: 액세스 거부 지원이 올바르게 구성 되어 있는지 확인 합니다.](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md#BKMK_3)  
  
> [!NOTE]  
> 이 항목에는 설명한 절차의 일부를 자동화하는 데 사용할 수 있는 샘플 Windows PowerShell cmdlet이 포함되어 있습니다. 자세한 내용은 참조 [Cmdlet를 사용 하 여](https://go.microsoft.com/fwlink/p/?linkid=230693)합니다.  
  
## <a name="BKMK_1"></a>1 단계: 액세스 거부 지원 구성  
그룹 정책을 사용하여 도메인 내에서 액세스 거부 지원을 구성하거나, 파일 서버 리소스 관리자 콘솔을 사용하여 각 파일 서버에서 개별적으로 지원을 구성할 수 있습니다. 또한 파일 서버의 특정 공유 폴더에 대한 액세스 거부 메시지를 변경할 수 있습니다.  
  
다음과 같이 그룹 정책을 사용하여 도메인에 대한 액세스 거부 지원을 구성할 수 있습니다.  
  
[Windows PowerShell을 사용 하 여이 단계를 수행 합니다.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)  
  
#### <a name="to-configure-access-denied-assistance-by-using-group-policy"></a>그룹 정책을 사용하여 액세스 거부 지원을 구성하려면  
  
1.  그룹 정책 관리를 엽니다. 서버 관리자에서 **도구**를 클릭한 다음 **그룹 정책 관리**를 클릭합니다.  
  
2.  해당 그룹 정책을 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.  
  
3.  **컴퓨터 구성**, **정책**, **관리 템플릿**, **시스템**, **액세스 거부 지원**을 차례로 클릭합니다.  
  
4.  **액세스 거부 오류 메시지 사용자 지정**을 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.  
  
5.  **사용** 옵션을 선택합니다.  
  
6.  다음 옵션을 구성합니다.  
  
    1.  **폴더 또는 파일에 대한 액세스가 거부된 사용자에게 다음 메시지 표시** 상자에 파일 또는 폴더에 대한 액세스가 거부된 사용자에게 표시할 메시지를 입력합니다.  
  
        사용자 지정 텍스트를 삽입하는 매크로를 메시지에 추가할 수 있습니다. 매크로는 다음과 같습니다.  
  
        -   **[원본 파일 경로]** 사용자가 액세스한 원본 파일 경로입니다.  
  
        -   **[원본 파일 경로 폴더]** 사용자가 액세스한 원본 파일 경로의 부모 폴더입니다.  
  
        -   **[관리자 전자 메일]** 관리자 전자 메일 받는 사람 목록입니다.  
  
        -   **[데이터 소유자 전자 메일]** 데이터 소유자 전자 메일 받는 사람 목록입니다.  
  
    2.  **사용자가 지원을 요청할 수 있음** 확인란을 선택합니다.  
  
    3.  나머지 기본 설정을 그대로 둡니다.  
  
![솔루션 가이드](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName AllowEmailRequests -Type DWORD -value 1  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName GenerateLog -Type DWORD -value 1  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName IncludeDeviceClaims -Type DWORD -value 1  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName IncludeUserClaims -Type DWORD -value 1  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName PutAdminOnTo -Type DWORD -value 1  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName PutDataOwnerOnTo -Type DWORD -value 1  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName ErrorMessage -Type MultiString -value "Type the text that the user will see in the error message dialog box."  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName Enabled -Type DWORD -value 1 
  
```  
  
또는 파일 서버 리소스 관리자 콘솔을 사용하여 각 파일 서버에서 개별적으로 액세스 거부 지원을 구성할 수 있습니다.  
  
[Windows PowerShell을 사용 하 여이 단계를 수행 합니다.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1a)  
  
#### <a name="to-configure-access-denied-assistance-by-using-file-server-resource-manager"></a>파일 서버 리소스 관리자를 사용하여 액세스 거부 지원을 구성하려면  
  
1.  파일 서버 리소스 관리자를 엽니다. 서버 관리자에서 **도구**를 클릭한 다음 **파일 서버 리소스 관리자**를 클릭합니다.  
  
2.  **파일 서버 리소스 관리자(로컬)** 를 마우스 오른쪽 단추로 클릭한 다음 **옵션 구성**을 클릭합니다.  
  
3.  **액세스 거부 지원** 탭을 클릭합니다.  
  
4.  **액세스 거부 지원 사용** 확인란을 선택합니다.  
  
5.  **폴더 또는 파일에 대한 액세스가 거부된 사용자에게 다음 메시지 표시** 상자에 파일 또는 폴더에 대한 액세스가 거부된 사용자에게 표시할 메시지를 입력합니다.  
  
    사용자 지정 텍스트를 삽입하는 매크로를 메시지에 추가할 수 있습니다. 매크로는 다음과 같습니다.  
  
    -   **[원본 파일 경로]** 사용자가 액세스한 원본 파일 경로입니다.  
  
    -   **[원본 파일 경로 폴더]** 사용자가 액세스한 원본 파일 경로의 부모 폴더입니다.  
  
    -   **[관리자 전자 메일]** 관리자 전자 메일 받는 사람 목록입니다.  
  
    -   **[데이터 소유자 전자 메일]** 데이터 소유자 전자 메일 받는 사람 목록입니다.  
  
6.  **전자 메일 요청 구성**을 클릭하고 **사용자가 지원을 요청할 수 있음** 확인란을 선택한 다음 **확인**을 클릭합니다.  
  
7.  사용자에게 표시되는 오류 메시지를 확인하려면 **미리 보기** 를 클릭합니다.  
  
8.  **확인**을 클릭합니다.  
  
![솔루션 가이드](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.
  
```  
Set-FSRMAdrSetting -Event "AccessDenied" -DisplayMessage "Type the text that the user will see in the error message dialog box." -Enabled:$true -AllowRequests:$true  
```  
  
액세스 거부 지원을 구성한 후에는 그룹 정책을 사용하여 모든 파일 형식에 액세스 거부 지원을 사용하도록 설정해야 합니다.  
  
[Windows PowerShell을 사용 하 여이 단계를 수행 합니다.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1c)  
  
#### <a name="to-configure-access-denied-assistance-for-all-file-types-by-using-group-policy"></a>그룹 정책을 사용하여 모든 파일 형식에 대해 액세스 거부 지원을 구성하려면  
  
1.  그룹 정책 관리를 엽니다. 서버 관리자에서 **도구**를 클릭한 다음 **그룹 정책 관리**를 클릭합니다.  
  
2.  해당 그룹 정책을 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.  
  
3.  **컴퓨터 구성**, **정책**, **관리 템플릿**, **시스템**, **액세스 거부 지원**을 차례로 클릭합니다.  
  
4.  **모든 파일 형식에 대해 클라이언트에서 액세스 거부 지원 사용**을 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.  
  
5.  **사용**을 클릭한 다음 **확인**을 클릭합니다.  
  
![솔루션 가이드](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요. 
  
```  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\SOFTWARE\Policies\Microsoft\Windows\Explore" -ValueName EnableShellExecuteFileStreamCheck -Type DWORD -value 1  
  
```  
  
또한 파일 서버 리소스 관리자 콘솔을 사용하여 파일 서버의 각 공유 폴더에 대해 별도의 액세스 거부 메시지를 지정할 수 있습니다.  
  
[Windows PowerShell을 사용 하 여이 단계를 수행 합니다.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1b)  
  
#### <a name="to-specify-a-separate-access-denied-message-for-a-shared-folder-by-using-file-server-resource-manager"></a>파일 서버 리소스 관리자를 사용하여 공유 폴더에 대해 별도의 액세스 거부 메시지를 지정하려면  
  
1.  파일 서버 리소스 관리자를 엽니다. 서버 관리자에서 **도구**를 클릭한 다음 **파일 서버 리소스 관리자**를 클릭합니다.  
  
2.  **파일 서버 리소스 관리자(로컬)** 를 확장하고 **분류 관리**를 클릭합니다.  
  
3.  **분류 속성**을 마우스 오른쪽 단추로 클릭한 다음 **폴더 관리 속성 설정**을 클릭합니다.  
  
4.  **속성** 상자에서 **액세스 거부 지원 메시지**를 클릭한 다음 **추가**를 클릭합니다.  
  
5.  **찾아보기**를 클릭한 다음 사용자 지정 액세스 거부 메시지를 저장할 폴더를 선택합니다.  
  
6.  **값** 상자에 해당 폴더 내의 리소스에 액세스할 수 없는 경우 사용자에게 표시되는 메시지를 입력합니다.  
  
    사용자 지정 텍스트를 삽입하는 매크로를 메시지에 추가할 수 있습니다. 매크로는 다음과 같습니다.  
  
    -   **[원본 파일 경로]** 사용자가 액세스한 원본 파일 경로입니다.  
  
    -   **[원본 파일 경로 폴더]** 사용자가 액세스한 원본 파일 경로의 부모 폴더입니다.  
  
    -   **[관리자 전자 메일]** 관리자 전자 메일 받는 사람 목록입니다.  
  
    -   **[데이터 소유자 전자 메일]** 데이터 소유자 전자 메일 받는 사람 목록입니다.  
  
7.  **확인**을 클릭하고 **닫기**를 클릭합니다.  
  
![솔루션 가이드](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요. 
  
```  
Set-FSRMMgmtProperty -Namespace "folder path" -Name "AccessDeniedMessage_MS" -Value "Type the text that the user will see in the error message dialog box."  
```  
  
## <a name="BKMK_2"></a>2 단계: 전자 메일 알림 설정 구성  
각 파일 서버에서 액세스 거부 지원 메시지를 보낼 전자 메일 알림 설정을 구성해야 합니다.  
  
[Windows PowerShell을 사용 하 여이 단계를 수행 합니다.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)  
  
1.  파일 서버 리소스 관리자를 엽니다. 서버 관리자에서 **도구**를 클릭한 다음 **파일 서버 리소스 관리자**를 클릭합니다.  
  
2.  **파일 서버 리소스 관리자(로컬)** 를 마우스 오른쪽 단추로 클릭한 다음 **옵션 구성**을 클릭합니다.  
  
3.  **전자 메일 알림** 탭을 클릭합니다.  
  
4.  다음 설정을 구성합니다.  
  
    -   **SMTP 서버 이름 또는 IP 주소** 상자에 조직에서 사용하는 SMTP 서버의 IP 주소 이름을 입력합니다.  
  
    -   에 **기본 수신 관리자** 및 **'전자 메일 주소 에서' 기본** 상자, 파일 서버 관리자의 전자 메일 주소를 입력 합니다.  
  
5.  **테스트 전자 메일 보내기**를 클릭하여 전자 메일 알림이 올바르게 구성되었는지 확인합니다.  
  
6.  **확인**을 클릭합니다.  
  
![솔루션 가이드](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.
  
```  
set-FSRMSetting -SMTPServer "server1" -AdminEmailAddress "fileadmin@contoso.com" -FromEmailAddress "fileadmin@contoso.com"  
```  
  
## <a name="BKMK_3"></a>3 단계: 액세스 거부 지원이 올바르게 구성되었는지 확인  
에 액세스할 수 없는 공유 하는 공유 또는 파일에 액세스 하려고 하는 Windows 8을 실행 하는 사용자 액세스 거부 지원이 올바르게 구성 되어 있는지 확인할 수 있습니다. 액세스 거부 메시지가 나타날 때 사용자에게 **지원 요청** 단추가 표시됩니다. 사용자는 지원 요청 단추를 클릭하여 액세스 이유를 지정한 다음 폴더 소유자 또는 파일 서버 관리자에게 전자 메일을 보낼 수 있습니다. 폴더 소유자 또는 파일 서버 관리자는 전자 메일이 도착했으며 적절한 세부 정보를 포함하고 있는지 확인해 줄 수 있습니다.  
  
> [!IMPORTANT]  
> Windows Server 2012를 실행 하는 사용자 액세스 거부 지원을 확인 하려는 경우 파일 공유에 연결 하기 전에 데스크톱 경험을 설치 해야 합니다.  
  
## <a name="BKMK_Links"></a>참고 항목  
  
-   [시나리오: 액세스 거부 지원](Scenario--Access-Denied-Assistance.md)  
  
-   [액세스 거부 지원 계획](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1)  
  
-   [동적 Access Control: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  
  

