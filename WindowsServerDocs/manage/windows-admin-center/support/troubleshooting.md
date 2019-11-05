---
title: Windows Admin Center 일반적인 문제 해결 단계
description: Windows Admin Center 일반적인 문제 해결 단계(Project Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 06/07/2019
ms.openlocfilehash: 0b4e02e6759bdb91ea51b5dcf5e1d0ae307d13b4
ms.sourcegitcommit: 1da993bbb7d578a542e224dde07f93adfcd2f489
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73567095"
---
# <a name="troubleshooting-windows-admin-center"></a>Windows Admin Center 문제 해결

> 적용 대상: Windows 관리 센터, Windows 관리 센터 미리 보기

> [!Important]
> 이 가이드는 Windows Admin Center를 사용할 수 없게 만드는 문제를 진단하고 해결하는데 도움이 됩니다. 특정 도구에 문제가 발생하는 경우 [알려진 문제](https://aka.ms/wacknownissues)를 참조하여 확인하십시오.

## <a name="installer-fails-with-message-_the-module-microsoftpowershelllocalaccounts-could-not-be-loaded_"></a>설치 관리자가 실패 하  **_고 ' Microsoft. PowerShell. Localaccounts ' 모듈을 로드할 수 없습니다._**

이는 기본 PowerShell 모듈 경로를 수정 하거나 제거 하는 경우에 발생할 수 있습니다. 이 문제를 해결 하려면 ```%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules```이 PSModulePath 환경 변수의 **첫 번째** 항목 인지 확인 합니다. PowerShell의 다음 줄을 사용 하 여이 작업을 수행할 수 있습니다.

```powershell
[Environment]::SetEnvironmentVariable("PSModulePath","%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules;" + ([Environment]::GetEnvironmentVariable("PSModulePath","User")),"User")
```

## <a name="i-get-a-this-sitepage-cant-be-reached-error-in-my-web-browser"></a>웹 브라우저 내에서 **이 사이트/페이지를 연결할 수 없음** 오류를 받음

### <a name="if-youve-installed-windows-admin-center-as-an-app-on-windows-10"></a>**Windows 10의 앱**으로 Windows Admin Center를 설치한 경우

* Windows Admin Center가 실행되고 있는지 확인합니다. 작업 관리자의 시스템 트레이 또는 **Windows 관리 센터 Desktop/SmeDesktop** 에서 ![](../media/trayIcon.PNG) Windows 관리 센터 아이콘을 찾습니다. 그렇지 않은 경우 시작 메뉴에서 **Windows Admin Center**를 실행합니다.

> [!NOTE] 
> 다시 부팅한 후 시작 메뉴에서 Windows Admin Center를 시작해야 합니다.  

* [Windows 버전 확인](#check-the-windows-version)

* 웹 브라우저로 Microsoft Edge 또는 Google Chrome 중 하나를 사용하고 있는지 확인합니다.

* [처음 실행](../use/get-started.md#selecting-a-client-certificate) 시 올바른 인증서를 선택했습니까?

  * 개인 세션에서 브라우저를 열어 보십시오. 작동하는 경우 캐시를 지워야 합니다.

* 최근에 Windows 10을 새 빌드 또는 버전으로 업그레이드 했나요?

  * 이렇게 하면 신뢰할 수 있는 호스트 설정이 지워질 수 있습니다. [다음 지침에 따라 신뢰할 수 있는 호스트 설정을 업데이트 합니다.](#configure-trustedhosts)

### <a name="if-youve-installed-windows-admin-center-as-a-gateway-on-windows-server"></a>**Windows Server에서 게이트웨이**로 Windows Admin Center를 설치한 경우

* 클라이언트 및 서버의 [Windows 버전을 확인](#check-the-windows-version)합니다.

* 웹 브라우저로 Microsoft Edge 또는 Google Chrome 중 하나를 사용하고 있는지 확인합니다.

* 서버에서 작업 관리자 > 서비스를 열고 **Servermanagementgateway/Windows 관리 센터가** 실행 중인지 확인 합니다.
![](../media/Service-TaskMan.PNG)

* 게이트웨이에 대 한 네트워크 연결 테스트 (\<값 >를 배포의 정보로 바꾸기)

    ```powershell
    Test-NetConnection -Port <port> -ComputerName <gateway> -InformationLevel Detailed
    ```

### <a name="if-you-have-installed-windows-admin-center-in-an-azure-windows-server-vm"></a>Azure Windows Server VM에 Windows 관리 센터를 설치한 경우

* [Windows 버전 확인](#check-the-windows-version)
* HTTPS에 대한 인바운드 포트 규칙을 추가했습니까? 
* [Azure VM에 Windows 관리 센터를 설치 하는 방법에 대 한 자세한 정보](https://docs.microsoft.com/windows-server/manage/windows-admin-center/configure/azure-integration#use-a-windows-admin-center-gateway-deployed-in-azure)

### <a name="check-the-windows-version"></a>Windows 버전 확인

* 대화 상자(Windows 키 + R)를 열고 ```winver```를 실행합니다.

* Windows 10 버전 1703 또는 이전을 사용하는 경우 Windows Admin Center는 귀하의 Microsoft Edge 버전에서 지원되지 않습니다. Windows 10의 최신 버전으로 업그레이드하거나 Chrome을 사용하십시오.

* Windows 10의 insider preview 버전 또는 17134과 17637 사이의 빌드 버전이 포함 된 서버를 사용 하는 경우 windows 관리 센터에 오류가 발생 하는 버그가 발생 했습니다. 현재 지원 되는 Windows 버전을 사용 하세요.

### <a name="make-sure-the-windows-remote-management-winrm-service-is-running-on-both-the-gateway-machine-and-managed-node"></a>Windows 원격 관리 (WinRM) 서비스가 게이트웨이 컴퓨터와 관리 되는 노드에서 모두 실행 되 고 있는지 확인 합니다.

* WindowsKey + R을 사용 하 여 실행 대화 상자 열기
* ```services.msc```를 입력 하 고 enter 키를 누릅니다.
* 열리는 창에서 WinRM (Windows 원격 관리)을 찾고, 실행 중이 고 자동으로 시작 되도록 설정 되어 있는지 확인 합니다.

### <a name="did-you-upgrade-your-server-from-2016-to-2019"></a>서버를 2016에서 2019로 업그레이드 했나요?

* 이렇게 하면 신뢰할 수 있는 호스트 설정이 지워질 수 있습니다. [다음 지침에 따라 신뢰할 수 있는 호스트 설정을 업데이트 합니다.](#configure-trustedhosts) 

## <a name="i-get-the-message-cant-connect-securely-to-this-page-this-might-be-because-the-site-uses-outdated-or-unsafe-tls-security-settings"></a>"이 페이지에 안전 하 게 연결할 수 없습니다." 라는 메시지를 받게 됩니다. 사이트에서 오래 되거나 안전 하지 않은 TLS 보안 설정을 사용 하기 때문일 수 있습니다.

사용자의 컴퓨터는 HTTP/2 연결로 제한 됩니다. Windows 관리 센터는 HTTP/2에서 지원 되지 않는 통합 Windows 인증을 사용 합니다. **브라우저를 실행** 하는 컴퓨터의 ```HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Http\Parameters``` 키 아래에 다음 두 개의 레지스트리 값을 추가 하 여 HTTP/2 제한을 제거 합니다.

```
EnableHttp2Cleartext=dword:00000000
EnableHttp2Tls=dword:00000000
```

## <a name="im-having-trouble-with-the-remote-desktop-events-and-powershell-tools"></a>원격 데스크톱, 이벤트 및 PowerShell 도구에 문제가 있습니다.

이러한 세 가지 도구에는 일반적으로 프록시 서버 및 방화벽에 의해 차단 되는 websocket 프로토콜이 필요 합니다. Google Chrome을 사용 하는 경우 websocket 및 NTLM 인증에 [알려진 문제가](known-issues.md#google-chrome) 있습니다.

## <a name="i-can-connect-to-some-servers-but-not-others"></a>일부 서버에 연결할 수 없지만 다른 서버에는 연결할 수 있음

* 게이트웨이 컴퓨터에 로컬로 로그온 하 고 PowerShell에서 ```Enter-PSSession <machine name>``` 하 \<컴퓨터 이름 >를 Windows 관리 센터에서 관리 하려는 컴퓨터 이름으로 바꿉니다. 

* 귀하의 환경에서 도메인 대신 작업 그룹을 사용하는 경우 [작업 그룹에서 Windows Admin Center 사용](#using-windows-admin-center-in-a-workgroup)을 참조하십시오.

* **로컬 관리자 계정 사용:** 기본 제공 관리자 계정이 아닌 로컬 사용자 계정을 사용하는 경우 PowerShell에서 다음 명령을 실행하여 대상 컴퓨터에서 또는 대상 컴퓨터의 명령 프롬프트에서 관리자로 정책을 사용하도록 설정해야 합니다.

    ```
    REG ADD HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1
    ```

## <a name="using-windows-admin-center-in-a-workgroup"></a>작업 그룹에서 Windows Admin Center 사용

### <a name="what-account-are-you-using"></a>사용하는 계정이 무엇입니까?
사용하는 자격 증명이 대상 서버의 로컬 관리자 그룹의 구성원인지 확인합니다. 경우에 따라 WinRM은 원격 관리 사용자 그룹의 구성원도 요구합니다. **기본 제공 관리자 계정이 아닌** 로컬 사용자 계정을 사용하는 경우 PowerShell에서 다음 명령을 실행하여 대상 컴퓨터에서 또는 대상 컴퓨터의 명령 프롬프트에서 관리자로 정책을 사용하도록 설정해야 합니다

```cmd
REG ADD HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1
```
### <a name="are-you-connecting-to-a-workgroup-machine-on-a-different-subnet"></a>다른 서브넷에서 작업 그룹 컴퓨터에 연결되어 있습니까?

게이트웨이와 동일한 서브넷에 있지 않은 작업 그룹 컴퓨터에 연결하려면 WinRM(TCP 5985)에 대한 방화벽 포트가 대상 컴퓨터의 인바운드 트래픽을 허용하는지 확인합니다. PowerShell에서 다음 명령을 실행하여 또는 대상 컴퓨터의 명령 프롬프트에서 관리자로 방화벽 규칙을 만들 수 있습니다.

- **Windows Server**

    ```powershell
    Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any
    ```

- **Windows 10**

    ```powershell
    Set-NetFirewallRule -Name WINRM-HTTP-In-TCP -RemoteAddress Any
    ```

### <a name="configure-trustedhosts"></a>TrustedHosts 구성

Windows Admin Center를 설치할 때 Windows Admin Center가 게이트웨이의 TrustedHosts 설정을 관리하도록 할 수 있는 옵션이 제공됩니다. 작업 그룹 환경에서 또는 도메인에서 로컬 관리자 자격 증명을 사용하는 경우 필요합니다. 이 설정을 중단하고 싶으면 반드시 TrustedHosts를 수동으로 구성해야 합니다.

**PowerShell 명령을 사용 하 여 TrustedHosts를 수정 하려면:**

1. 관리자 PowerShell 세션을 엽니다.
2. 현재 TrustedHosts 설정 보기:

    ```powershell
    Get-Item WSMan:\localhost\Client\TrustedHosts
    ```

   > [!WARNING]
   > 사용자 TrustedHosts의 현재 설정이 비어 있지 않으면 아래 명령이 설정을 덮어씁니다. 필요한 경우에 복원할 수 있도록 다음 명령을 사용하여 텍스트 파일로 현재 설정을 저장하는 것이 좋습니다.
   > 
   > `Get-Item WSMan:localhost\Client\TrustedHosts | Out-File C:\OldTrustedHosts.txt`

3. TrustedHosts를 관리하려는 컴퓨터의 NetBIOS, IP, 또는 FQDN으로 설정:

    ```powershell
    Set-Item WSMan:localhost\Client\TrustedHosts -Value '192.168.1.1,server01.contoso.com,server02'
    ```

   > [!TIP]
   > 한번에 모든 TrustedHosts를 설정하는 간단한 방법은 와일드카드를 사용하는 것입니다.
   > 
   >     Set-Item WSMan:\localhost\Client\TrustedHosts -Value '*'

4. 테스트가 완료되면 관리자 권한 PowerShell 세션에서 다음 명령을 발급하여 TrustedHosts 설정을 지울 수 있습니다.

    ```powershell
    Clear-Item WSMan:localhost\Client\TrustedHosts
    ```

5. 이전에 설정을 내보낸 경우 파일을 열고, 값을 복사한 다음 이 명령을 사용합니다.

    ```powershell
    Set-Item WSMan:localhost\Client\TrustedHosts -Value '<paste values from text file>'
    ```

## <a name="i-previously-had-windows-admin-center-installed-and-now-nothing-else-can-use-the-same-tcpip-port"></a>이전에 Windows 관리 센터를 설치 했 고 이제 동일한 TCP/IP 포트를 사용할 수 없습니다.

관리자 권한 명령 프롬프트에서 다음 두 명령을 수동으로 실행 합니다.

```cmd
netsh http delete sslcert ipport=0.0.0.0:443
netsh http delete urlacl url=https://+:443/
```

## <a name="azure-features-dont-work-properly-in-edge"></a>Edge에서 Azure 기능이 제대로 작동 하지 않음

Edge에는 Windows 관리 센터의 Azure 로그인에 영향을 주는 보안 영역과 관련 된 [알려진 문제가](https://github.com/AzureAD/azure-activedirectory-library-for-js/wiki/Known-issues-on-Edge) 있습니다. Edge를 사용할 때 Azure 기능을 사용 하는 데 문제가 있는 경우 https://login.microsoftonline.com , https://login.live.com 및 게이트웨이의 URL을 신뢰할 수 있는 사이트로 추가 하 고 클라이언트 쪽 브라우저에서 Edge 팝업 차단 설정에 허용 된 사이트에 추가 해 보세요. 

이렇게 하려면 다음을 수행합니다.
1. Windows 시작 메뉴에서 **인터넷 옵션** 을 검색 합니다.
2. **보안** 탭으로 이동 합니다.
3. **신뢰할 수 있는 사이트** 옵션에서 **사이트** 단추를 클릭 하 고 열리는 대화 상자에 url을 추가 합니다. 게이트웨이 URL 뿐만 아니라 https://login.microsoftonline.com 및 https://login.live.com 를 추가 해야 합니다.
4. **개인 정보** 탭으로 이동
5. **팝업 차단** 섹션 아래에서 **설정** 단추를 클릭 하 고 열리는 대화 상자에 url을 추가 합니다. 게이트웨이 URL 뿐만 아니라 https://login.microsoftonline.com 및 https://login.live.com 를 추가 해야 합니다.

## <a name="having-an-issue-with-an-azure-related-feature"></a>Azure 관련 기능을 사용 하는 데 문제가 있나요?

다음 정보를 사용 하 여 wacFeedbackAzure@microsoft.com 전자 메일을 보내 주세요.
* [아래에 나열 된 질문](#providing-feedback-on-issues)의 일반적인 문제 정보
* 문제 및 문제를 재현 하기 위해 수행한 단계를 설명 합니다. 
* 이전에 New-AadApp 다운로드 가능한 스크립트를 사용 하 여 게이트웨이를 Azure에 등록 한 다음 버전 1807로 업그레이드 했습니까? 또는 Azure > 게이트웨이 설정의 UI를 사용 하 여 Azure에 게이트웨이를 등록 하셨습니까?
* Azure 계정이 여러 디렉터리/테 넌 트와 연결 되어 있나요?
    * 예: Windows 관리 센터에 Azure AD 응용 프로그램을 등록 하는 경우 Azure에서 기본 디렉터리를 사용한 디렉터리 입니까? 
* Azure 계정에 여러 구독에 대 한 액세스 권한이 있나요?
* 사용 중인 구독에 청구가 연결 되어 있나요?
* 문제가 발생 했을 때 여러 Azure 계정에 로그인 했습니까?
* Azure 계정에 다단계 인증이 필요 한가요?
* Azure VM을 관리 하려는 컴퓨터가 있나요?
* Azure VM에 Windows 관리 센터가 설치 되어 있나요?

## <a name="providing-feedback-on-issues"></a>문제에 대 한 피드백 제공

이벤트 뷰어 > 응용 프로그램 및 서비스 > Microsoft-ServerManagementExperience로 이동하여 오류나 경고를 찾습니다.

문제를 설명하는 [UserVoice](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5BBug%5D)에서 버그를 보고합니다.

다음 정보를 비롯하여 이벤트 로그에서 찾은 오류 또는 경고를 포함하십시오. 

* Windows Admin Center가 **설치된** 플랫폼(Windows 10 또는 Windows Server):
    * 서버에 설치 된 경우 Windows 관리 센터에 액세스 하기 위해 **브라우저를 실행** 하는 컴퓨터의 windows [버전](#check-the-windows-version) 은 다음과 같습니다. 
    * 설치 관리자에서 만든 자체 서명 된 인증서를 사용 하 고 있습니까?
    * 자체 인증서를 사용하는 경우 주체 이름이 컴퓨터와 일치합니까?
    * 자체 인증서를 사용하는 경우 대체 주체 이름이 지정되었습니까?
* 기본 포트 설정을 사용하여 설치했습니까?
    * 그렇지 않은 경우 어떤 포트를 지정했습니까?
* Windows Admin Center가 **설치된** 컴퓨터가 도메인에 가입되어 있습니까?
* Windows Admin Center가 **설치된** Windows [버전](#check-the-windows-version):
* **관리하려는** 컴퓨터가 도메인에 가입되었습니까?
* **관리하려는** 컴퓨터의 Windows [버전](#check-the-windows-version):
* 어떤 브라우저를 사용하고 있습니까?
    * Google Chrome을 사용하는 경우 버전은 무엇입니까? (도움말 > Google Chrome 정보)

