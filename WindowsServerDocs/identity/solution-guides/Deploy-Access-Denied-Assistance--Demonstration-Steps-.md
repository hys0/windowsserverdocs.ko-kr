---
ms.assetid: b035e9f8-517f-432a-8dfb-40bfc215bee5
title: "액세스 거부 Assistance (데모 단계)를 배포 합니다."
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 5201441ba884fe4658b917919e60c7d20530341b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="deploy-access-denied-assistance-demonstration-steps"></a>액세스 거부 Assistance (데모 단계)를 배포 합니다.

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에 액세스 거부 assistance 구성 하 고 제대로 작동 하는지 확인 하는 방법을 설명 합니다.  
  
**이 문서에서**  
  
-   [1 단계: 지원 액세스 거부 구성](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md#BKMK_1)  
  
-   [2 단계: 구성 메일 알림 설정](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md#BKMK_2)  
  
-   [3 단계: 지원 액세스 거부 올바르게 구성 되어 있는지 확인](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md#BKMK_3)  
  
> [!NOTE]  
> 이 항목에 설명 된 절차 일부 자동화 데 사용할 수 있는 샘플 Windows PowerShell cmdlet 포함 되어 있습니다. 자세한 내용은 참조 [사용 하 여 Cmdlet](https://go.microsoft.com/fwlink/p/?linkid=230693)합니다.  
  
## <a name="BKMK_1"></a>1 단계: 지원 액세스 거부 구성  
그룹 정책을 사용 하 여 액세스 거부 지원 도메인 내 구성 하거나 수 있으므로 파일 서버 리소스 관리자 본체를 사용 하 여 각 파일 서버에 도움을 개별적으로 구성할 수 있습니다. 파일 서버에 특정 공유 폴더에 대 한 액세스 거부 메시지를 변경할 수 있습니다.  
  
다음과 같이 그룹 정책을 사용 하 여 도메인에 대 한 지원을 액세스 거부 구성할 수 있습니다.  
  
[Windows PowerShell를 사용 하 여이 단계를 수행 합니다.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)  
  
#### <a name="to-configure-access-denied-assistance-by-using-group-policy"></a>그룹 정책을 사용 하 여 액세스 거부 지원 구성 하려면  
  
1.  열기 그룹 정책 관리 합니다. 서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **그룹 정책 관리**합니다.  
  
2.  적절 한 그룹 정책 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **편집**합니다.  
  
3.  클릭 **컴퓨터 구성**, 클릭 **정책**, 클릭 **관리 템플릿**, 클릭 **시스템**을 차례로 클릭 하 고 **Access-Denied 지원**합니다.  
  
4.  마우스 오른쪽 단추로 클릭 **액세스 거부 오류에 대 한 사용자 지정 메시지**을 차례로 클릭 하 고 **편집**합니다.  
  
5.  선택는 **사용** 옵션이 있습니다.  
  
6.  다음 옵션을 구성 합니다.  
  
    1.  에 **액세스할 수 있는 사용자에 게 다음 메시지가 표시** 상자에 파일 또는 폴더에 대 한 액세스 거부 됩니다 때 사용자가 볼 수 있도록 메시지를 입력 합니다.  
  
        사용자 지정 된 텍스트 삽입 하는 메시지에 접사 추가할 수 있습니다. 매크로 다음과 같습니다.  
  
        -   **[원래 파일 경로가] **사용자가 액세스 원래 파일 경로 합니다.  
  
        -   **[원래 파일 경로 폴더] **사용자가 액세스 원래 파일 경로의 부모 폴더 합니다.  
  
        -   **[관리자 메일] **관리자 메일 받는 사람 목록입니다.  
  
        -   **[데이터 소유자 메일] **데이터 소유자 메일 받는 사람 목록입니다.  
  
    2.  선택는 **지원 요청 수 있도록** 확인란을 선택 합니다.  
  
    3.  나머지 기본 설정을 유지 됩니다.  
  
![해결 방법 가이드](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.  
  
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
  
또는 지원을 구성할 수 있습니다 액세스 거부 개별적으로 각 파일 서버에서 파일 서버 리소스 관리자 본체를 사용 하 여 합니다.  
  
[Windows PowerShell를 사용 하 여이 단계를 수행 합니다.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1a)  
  
#### <a name="to-configure-access-denied-assistance-by-using-file-server-resource-manager"></a>파일 서버 리소스 관리자를 사용 하 여 액세스 거부 assistance 구성 하려면  
  
1.  파일 서버 리소스 관리자를 엽니다. 서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **파일 서버 리소스 관리자**합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **파일 서버 리소스 관리자 (로컬)**을 차례로 클릭 하 고 **옵션 구성**합니다.  
  
3.  클릭 하 고 **Access-Denied 지원** 탭 합니다.  
  
4.  선택는 **액세스 거부 지원 사용** 확인란을 선택 합니다.  
  
5.  에 **폴더 또는 파일에 액세스할 수 있는 사용자에 게 다음 메시지가 표시** 상자에 파일 또는 폴더에 대 한 액세스 거부 됩니다 때 사용자가 볼 수 있도록 메시지를 입력 합니다.  
  
    사용자 지정 된 텍스트 삽입 하는 메시지에 접사 추가할 수 있습니다. 매크로 다음과 같습니다.  
  
    -   **[원래 파일 경로가] **사용자가 액세스 원래 파일 경로 합니다.  
  
    -   **[원래 파일 경로 폴더] **사용자가 액세스 원래 파일 경로의 부모 폴더 합니다.  
  
    -   **[관리자 메일] **관리자 메일 받는 사람 목록입니다.  
  
    -   **[데이터 소유자 메일] **데이터 소유자 메일 받는 사람 목록입니다.  
  
6.  클릭 **구성 메일 요청**는 **지원 요청 수 있도록** 확인란을 선택한 다음 클릭 **확인**합니다.  
  
7.  클릭 **미리 보기** 오류 메시지는 사용자에 게 모양을 확인 하려면.  
  
8.  클릭 **확인**합니다.  
  
![해결 방법 가이드](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.
  
```  
Set-FSRMAdrSetting -Event "AccessDenied" -DisplayMessage "Type the text that the user will see in the error message dialog box." -Enabled:$true -AllowRequests:$true  
```  
  
액세스 거부 도움을 구성 하 고 나면 그룹 정책을 사용 하 여 모든 파일 형식에 대 한 설정 해야 있습니다.  
  
[Windows PowerShell를 사용 하 여이 단계를 수행 합니다.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1c)  
  
#### <a name="to-configure-access-denied-assistance-for-all-file-types-by-using-group-policy"></a>그룹 정책을 사용 하 여 모든 파일 형식에 대 한 액세스 거부 assistance 구성 하려면  
  
1.  열기 그룹 정책 관리 합니다. 서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **그룹 정책 관리**합니다.  
  
2.  적절 한 그룹 정책 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **편집**합니다.  
  
3.  클릭 **컴퓨터 구성**, 클릭 **정책**, 클릭 **관리 템플릿**, 클릭 **시스템**을 차례로 클릭 하 고 **Access-Denied 지원**합니다.  
  
4.  마우스 오른쪽 단추로 클릭 **모든 파일 형식에 대 한 클라이언트를 지원 액세스 거부 사용**을 차례로 클릭 하 고 **편집**합니다.  
  
5.  클릭 **사용**을 차례로 클릭 하 고 **확인**합니다.  
  
![해결 방법 가이드](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다. 
  
```  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\SOFTWARE\Policies\Microsoft\Windows\Explore" -ValueName EnableShellExecuteFileStreamCheck -Type DWORD -value 1  
  
```  
  
파일 서버 리소스 관리자 본체를 사용 하 여 파일 서버에 각 공유 폴더에 대 한 액세스 거부 별도 메시지를 지정할 수 있습니다.  
  
[Windows PowerShell를 사용 하 여이 단계를 수행 합니다.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1b)  
  
#### <a name="to-specify-a-separate-access-denied-message-for-a-shared-folder-by-using-file-server-resource-manager"></a>파일 서버 리소스 관리자를 사용 하 여 공유 폴더에 대 한 액세스 거부 별도 메시지를 지정 하려면  
  
1.  파일 서버 리소스 관리자를 엽니다. 서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **파일 서버 리소스 관리자**합니다.  
  
2.  확장 **파일 서버 리소스 관리자 (로컬)**을 차례로 클릭 하 고 **분류 관리**합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **분류 속성**을 차례로 클릭 하 고 **폴더 관리 속성 설정**합니다.  
  
4.  **속성** 상자를 클릭 **Access-Denied 지원 메시지**을 차례로 클릭 하 고 **추가**합니다.  
  
5.  클릭 **찾아보기**, 한 다음 사용자 지정 액세스 거부 메시지 해야 하는 폴더를 선택 합니다.  
  
6.  에 **값** 상자에서 해당 폴더 리소스에 액세스할 수 없는 경우 사용자에 게 제공 해야 하는 메시지를 입력 합니다.  
  
    사용자 지정 된 텍스트 삽입 하는 메시지에 접사 추가할 수 있습니다. 매크로 다음과 같습니다.  
  
    -   **[원래 파일 경로가] **사용자가 액세스 원래 파일 경로 합니다.  
  
    -   **[원래 파일 경로 폴더] **사용자가 액세스 원래 파일 경로의 부모 폴더 합니다.  
  
    -   **[관리자 메일] **관리자 메일 받는 사람 목록입니다.  
  
    -   **[데이터 소유자 메일] **데이터 소유자 메일 받는 사람 목록입니다.  
  
7.  클릭 **확인**을 차례로 클릭 하 고 **닫기**합니다.  
  
![해결 방법 가이드](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다. 
  
```  
Set-FSRMMgmtProperty -Namespace "folder path" -Name "AccessDeniedMessage_MS" -Value "Type the text that the user will see in the error message dialog box."  
```  
  
## <a name="BKMK_2"></a>2 단계: 구성 메일 알림 설정  
보낼 assistance 액세스 거부 메시지 각 파일 서버에서 메일 알림 설정을 구성 해야 합니다.  
  
[Windows PowerShell를 사용 하 여이 단계를 수행 합니다.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)  
  
1.  파일 서버 리소스 관리자를 엽니다. 서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **파일 서버 리소스 관리자**합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **파일 서버 리소스 관리자 (로컬)**을 차례로 클릭 하 고 **옵션 구성**합니다.  
  
3.  클릭 하 고 **메일 알림** 탭 합니다.  
  
4.  다음 설정을 구성.  
  
    -   에 **SMTP 서버 이름 또는 IP 주소** 상자 조직에 IP 주소 SMTP 서버의 이름을 입력 합니다.  
  
    -   에 **기본 수신 관리자** 및 **'메일 주소 에서' 기본** 상자, 파일 서버 관리자의 메일 주소를 입력 합니다.  
  
5.  클릭 **테스트 전자 메일 보내기** 에 메일 알림 올바르게 구성 되어 있는지 확인 합니다.  
  
6.  클릭 **확인**합니다.  
  
![해결 방법 가이드](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.
  
```  
set-FSRMSetting -SMTPServer "server1" -AdminEmailAddress "fileadmin@contoso.com" -FromEmailAddress "fileadmin@contoso.com"  
```  
  
## <a name="BKMK_3"></a>3 단계: 지원 액세스 거부 올바르게 구성 되어 있는지 확인  
사용자는 것에 대 한 액세스 없는 공유 하는 공유 또는 파일에 액세스 하려고 하는 Windows 8을 실행 하 여 액세스 거부 assistance 올바르게 구성 되어 있는지 확인할 수 있습니다. 때 액세스 거부 하 고 메시지가 표시 사용자 표시 되어야는 **도움 요청** 단추. 도움 요청 단추를 클릭 한 후 사용자 이유 액세스를 선택 하 고 소유자 폴더 또는 파일 서버 관리자에 메일을 보낼 수 있습니다. 메일에 도착 하 고 적절 한 세부 정보가 포함 된 폴더 소유자 또는 파일 서버 관리자를 확인할 수 있습니다.  
  
> [!IMPORTANT]  
> 사용자는 Windows Server 2012에서 실행 하 여 액세스 거부 도움을 확인 하려는 경우 데스크톱 경험 파일 공유 연결 하기 전에 설치 해야 합니다.  
  
## <a name="BKMK_Links"></a>참조 하십시오  
  
-   [액세스 거부 Assistance 시나리오:](Scenario--Access-Denied-Assistance.md)  
  
-   [요금제에 대 한 액세스 거부 지원](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1)  
  
-   [동적 액세스 제어: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  
  

