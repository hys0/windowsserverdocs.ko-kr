---
title: Windows Admin Center 일반적인 문제 해결 단계
description: Windows Admin Center 일반적인 문제 해결 단계(Project Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 02/12/2019
ms.openlocfilehash: a91a8dcf6f05ef0ef66dee603851150b2145d559
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297083"
---
# Windows Admin Center 문제 해결

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

> [!Important]
> 이 가이드는 Windows Admin Center를 사용할 수 없게 만드는 문제를 진단하고 해결하는데 도움이 됩니다. 특정 도구에 문제가 발생하는 경우 [알려진 문제](http://aka.ms/wacknownissues)를 참조하여 확인하십시오.

<a id="toc"></a>

## 빠른 링크

* [메시지와 함께 설치 실패: ** _The 모듈 'Microsoft.PowerShell.LocalAccounts'를 로드할 수 없습니다._**](#psmodulepath)

* 웹 브라우저 내에서 **이 사이트/페이지를 연결할 수 없음** 오류를 받음(배포 형식 선택)
    * [Windows 10에서 앱으로 설치된 Windows Admin Center가 있음](#whitescreenw10)
    * [Windows Server에 게이트웨이로 설치된 Windows Admin Center가 있음](#whitescreenws)
    * [Azure VM에 게이트웨이로 설치된 Windows Admin Center가 있음](#whitescreenazvm)

* [Windows Admin Center 홈 페이지가 로드 되지만 연결 추가 창에서 진행 되지 않음 또는 모든 컴퓨터에 연결할 수 없습니다.](#winvercompat)

* [다음 메시지가 표시됨: "모듈을 로드하는 동안 오류가 발생했습니다. Rpc: 만료된 다시 시도 'Ping'."](#winvercompat)

* [메시지를 받음: "불가능이이 페이지에 안전 하 게 연결 합니다. 이 때문일 수 사이트에서 오래 된 또는 안전 하지 않은 TLS 보안 설정을 사용 합니다. "](#tls)

* [원격 데스크톱, 이벤트 및 PowerShell 도구를 사용 하 여 문제가 있습니다.](#websockets)

* [Edge에서 Azure 기능을 사용 하 여 문제 발생](#azlogin)

* [일부 서버에 연결할 수 있지만 일부 서버에는 연결할 수 없음](#connectionissues)

* [**작업 그룹**에서 Windows Admin Center를 사용하고 있음](#workgroup)

* [이미 Windows Admin Center를 설치 하 고 이제 가기만 동일한 TCP/IP 포트를 사용할 수 있습니다.](#urlacl)

* [내 문제가 여기에 나열되지 않았거나 이 페이지의 단계로 내 문제가 해결되지 않았습니다.](#filebug)

<a id="psmodulepath"></a>

## 메시지와 함께 설치 실패: ** _The 모듈 'Microsoft.PowerShell.LocalAccounts'를 로드할 수 없습니다._**

이 기본 PowerShell 모듈 경로 수정 되거나 제거 된 경우 발생할 수 있습니다. 이 문제를 해결 하려면 있는지 확인 하는 ```%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules``` PSModulePath 환경 변수에서 **첫 번째** 항목입니다. 다음 PowerShell 사용 하 여이 얻을 수 있습니다.

```powershell
[Environment]::SetEnvironmentVariable("PSModulePath","%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules;" + ([Environment]::GetEnvironmentVariable("PSModulePath","User")),"User")
```

## 웹 브라우저 내에서 **이 사이트/페이지를 연결할 수 없음** 오류를 받음

<a id="whitescreenw10"></a>

### **Windows 10의 앱**으로 Windows Admin Center를 설치한 경우

* Windows Admin Center가 실행되고 있는지 확인합니다. Windows Admin Center 아이콘 ![](../media/trayIcon.PNG) 시스템 트레이에서 또는 **Windows Admin Center 데스크톱 / SmeDesktop.exe** 작업 관리자에서 합니다. 그렇지 않은 경우 시작 메뉴에서 **Windows Admin Center**를 실행합니다.

> [!NOTE] 
> 다시 부팅한 후 시작 메뉴에서 Windows Admin Center를 시작해야 합니다.  

* [Windows 버전 확인](#winvercompat)

* 웹 브라우저로 Microsoft Edge 또는 Google Chrome 중 하나를 사용하고 있는지 확인합니다.

* [처음 실행](../use/get-started.md#selecting-a-client-certificate) 시 올바른 인증서를 선택했습니까?

  * 개인 세션에서 브라우저를 열어 보십시오. 작동하는 경우 캐시를 지워야 합니다.

* 최근에 업그레이드 했습니까 Windows 10 버전 또는 새 빌드를?

  * 신뢰할 수 있는 호스트 설정 삭제이. [신뢰할 수 있는 호스트 설정을 업데이트 하려면 다음이 지침을 따릅니다.](#configure-trustedhosts) 

[[맨 위로]](#toc)

<a id="whitescreenws"></a>

### **Windows Server에서 게이트웨이**로 Windows Admin Center를 설치한 경우

* Windows Admin Center의 이전 버전에서 업그레이드 했습니까? 방화벽 규칙이 [이 알려진된 문제로](known-issues.md#upgrade)인해 삭제 되지 않은 있는지 확인 합니다. 규칙이 있는지 확인 하려면 다음 PowerShell 명령을 사용 합니다. 그렇지 않은 경우 다시 [다음이 지침](known-issues.md#upgrade) 따릅니다.
    ```powershell
    Get-NetFirewallRule -DisplayName "SmeInboundOpenException"
    ```

* 클라이언트 및 서버의 [Windows 버전을 확인](#winvercompat)합니다.

* 웹 브라우저로 Microsoft Edge 또는 Google Chrome 중 하나를 사용하고 있는지 확인합니다.

* 서버에서 작업 관리자 gt_ 서비스 열고 있는지 **ServerManagementGateway / Windows Admin Center** 실행 됩니다.
![](../media/Service-TaskMan.PNG)

* 게이트웨이에 대한 네트워크 연결 테스트(\<값>을 배포의 정보로 교체)
    ```powershell
    Test-NetConnection -Port <port> -ComputerName <gateway> -InformationLevel Detailed
    ```

[[맨 위로]](#toc)

<a id="whitescreenazvm"></a>  

### Azure Windows Server VM에서 Windows Admin Center를 설치한 경우

* [Windows 버전 확인](#winvercompat)
* HTTPS에 대한 인바운드 포트 규칙을 추가했습니까? 
* [Azure VM에서 Windows Admin Center를 설치하는 방법에 대한 자세한 내용](https://docs.microsoft.com/windows-server/manage/windows-admin-center/configure/azure-integration#use-a-windows-admin-center-gateway-deployed-in-azure)

[[맨 위로]](#toc)

<a id="winvercompat"></a>

### Windows 버전 확인

* 대화 상자(Windows 키 + R)를 열고 ```winver```를 실행합니다.

* Windows 10 버전 1703 또는 이전을 사용하는 경우 Windows Admin Center는 귀하의 Microsoft Edge 버전에서 지원되지 않습니다. Windows 10의 최신 버전으로 업그레이드하거나 Chrome을 사용하십시오.

* 서버 또는 Windows 10 참가자 미리 보기 버전 17134 17637 사이의 빌드 버전을 사용 하는 경우 Windows는 Windows Admin Center에 실패를 일으킨 버그를 했습니다. 현재 지원 되는 버전의 Windows 사용 하세요.

### Windows 원격 관리 (WinRM) 서비스가 게이트웨이 컴퓨터와 관리 되는 노드 모두에서 실행 되 고 있는지 확인

* WindowsKey + R을 사용 하 여 실행된 대화 상자 열기
* 유형 ```services.msc``` 하 고 enter
* Windows 원격 관리 (WinRM)에 대 한 보기 창이 열리면에서 실행 되 고 자동으로 시작 되도록 설정 되어 있는지 확인

### 가 서버에서에서 업그레이드 2016 2019?

* 신뢰할 수 있는 호스트 설정 삭제이. [신뢰할 수 있는 호스트 설정을 업데이트 하려면 다음이 지침을 따릅니다.](#configure-trustedhosts) 

[[맨 위로]](#toc)

<a id="tls"></a>

## 메시지를 받음: "불가능이이 페이지에 안전 하 게 연결 합니다. 사이트에서 오래 된 또는 안전 하지 않은 TLS 보안 설정을 사용 하기 때문에 수 있습니다.

<!--REF: https://docs.microsoft.com/iis/get-started/whats-new-in-iis-10/http2-on-iis#when-is-http2-not-supported -->
컴퓨터는 HTTP/2 연결으로 제한 됩니다. Windows Admin Center는 HTTP/2에서 지원 되지 않는 통합된 Windows 인증을 사용 합니다. 아래에서 다음 두 레지스트리 값을 추가 합니다 ```HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Http\Parameters``` HTTP/2 제한 제거 하 **는 브라우저를 실행 하는 컴퓨터** 키:

```
EnableHttp2Cleartext=dword:00000000
EnableHttp2Tls=dword:00000000
```

[[맨 위로]](#toc)

<a id="websockets"></a> 

## 원격 데스크톱, 이벤트 및 PowerShell 도구를 사용 하 여 문제가 있습니다.

이러한 세 가지 도구는 일반적으로 프록시 서버 및 방화벽에 의해 차단 되는 websocket 프로토콜을 필요 합니다. Google Chrome을 사용 하는 경우에는 [알려진 문제](known-issues.md#google-chrome) websockets 및 NTLM 인증 됩니다.

[[맨 위로]](#toc)


<a id="connectionissues"></a> 

## 일부 서버에 연결할 수 없지만 다른 서버에는 연결할 수 있음
* 로컬로 게이트웨이 컴퓨터에 로그인하고 PowerShell에서 \<컴퓨터 이름>을 Windows Admin Center에서 관리할 컴퓨터의 이름으로 변경하여 ```Enter-PSSession <machine name>```을 시도합니다. 

* 귀하의 환경에서 도메인 대신 작업 그룹을 사용하는 경우 [작업 그룹에서 Windows Admin Center 사용](#workgroup)을 참조하십시오.

* **로컬 관리자 계정 사용:** 기본 제공 관리자 계정이 아닌 로컬 사용자 계정을 사용하는 경우 PowerShell에서 다음 명령을 실행하여 대상 컴퓨터에서 또는 대상 컴퓨터의 명령 프롬프트에서 관리자로 정책을 사용하도록 설정해야 합니다.

        REG ADD HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1


[[맨 위로]](#toc)

<a id="workgroup"></a>

## 작업 그룹에서 Windows Admin Center 사용 

### 사용하는 계정이 무엇입니까?
사용하는 자격 증명이 대상 서버의 로컬 관리자 그룹의 구성원인지 확인합니다. 경우에 따라 WinRM은 원격 관리 사용자 그룹의 구성원도 요구합니다. **기본 제공 관리자 계정이 아닌** 로컬 사용자 계정을 사용하는 경우 PowerShell에서 다음 명령을 실행하여 대상 컴퓨터에서 또는 대상 컴퓨터의 명령 프롬프트에서 관리자로 정책을 사용하도록 설정해야 합니다

```cmd
REG ADD HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1
```
### 다른 서브넷에서 작업 그룹 컴퓨터에 연결되어 있습니까?

게이트웨이와 동일한 서브넷에 있지 않은 작업 그룹 컴퓨터에 연결하려면 WinRM(TCP 5985)에 대한 방화벽 포트가 대상 컴퓨터의 인바운드 트래픽을 허용하는지 확인합니다. PowerShell에서 다음 명령을 실행하여 또는 대상 컴퓨터의 명령 프롬프트에서 관리자로 방화벽 규칙을 만들 수 있습니다.

- **Windows Server**

    ```powershell
    Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any
    ```

- **Windows10**

    ```powershell
    Set-NetFirewallRule -Name WINRM-HTTP-In-TCP -RemoteAddress Any
    ```

### TrustedHosts 구성

Windows Admin Center를 설치할 때 Windows Admin Center가 게이트웨이의 TrustedHosts 설정을 관리하도록 할 수 있는 옵션이 제공됩니다. 작업 그룹 환경에서 또는 도메인에서 로컬 관리자 자격 증명을 사용하는 경우 필요합니다. 이 설정을 중단하고 싶으면 반드시 TrustedHosts를 수동으로 구성해야 합니다.

**PowerShell 명령을 사용하여 TrustedHosts를 수정하는 방법:**

1. 관리자 PowerShell 세션을 엽니다.
2. 현재 TrustedHosts 설정 보기:

    ```powershell
    Get-Item WSMan:\localhost\Client\TrustedHosts
    ```

    > [!WARNING]
    > 사용자 TrustedHosts의 현재 설정이 비어 있지 않으면 아래 명령이 설정을 덮어씁니다. 필요한 경우에 복원할 수 있도록 다음 명령을 사용하여 텍스트 파일로 현재 설정을 저장하는 것이 좋습니다.

    > `Get-Item WSMan:localhost\Client\TrustedHosts | Out-File C:\OldTrustedHosts.txt`

3. TrustedHosts를 관리하려는 컴퓨터의 NetBIOS, IP, 또는 FQDN으로 설정:

    ```powershell
    Set-Item WSMan:localhost\Client\TrustedHosts -Value '192.168.1.1,server01.contoso.com,server02'
    ```

    > [!TIP] 
    >한번에 모든 TrustedHosts를 설정하는 간단한 방법은 와일드카드를 사용하는 것입니다.

    >     Set-Item WSMan:\localhost\Client\TrustedHosts -Value '*'

4. 테스트가 완료되면 관리자 권한 PowerShell 세션에서 다음 명령을 발급하여 TrustedHosts 설정을 지울 수 있습니다.

    ```powershell
    Clear-Item WSMan:localhost\Client\TrustedHosts
    ```

5. 이전에 설정을 내보낸 경우 파일을 열고, 값을 복사한 다음 이 명령을 사용합니다.

    ```powershell
    Set-Item WSMan:localhost\Client\TrustedHosts -Value '<paste values from text file>'
    ```

[[맨 위로]](#toc)

<a id="urlacl"></a>

## 이미 Windows Admin Center를 설치 하 고 이제 가기만 동일한 TCP/IP 포트를 사용할 수 있습니다.

수동으로 관리자 권한 명령 프롬프트에서 다음 두 명령을 실행 합니다.

```cmd
netsh http delete sslcert ipport=0.0.0.0:443
netsh http delete urlacl url=https://+:443/
```

[[맨 위로]](#toc)

<a id="azlogin"></a>

## Edge에서 Azure 기능을 사용 하 여 문제 발생

Edge와 관련 된 Windows 관리 센터에서 Azure 로그인에 영향을 주는 보안 영역으로 [알려진 문제](https://github.com/AzureAD/azure-activedirectory-library-for-js/wiki/Known-issues-on-Edge) 에 있습니다. Edge를 사용 하는 경우 Azure 기능을 사용 하는 데 문제가 있는 경우 추가 해 보세요 https://login.microsoftonline.com, https://login.live.com 으로 게이트웨이의 URL 신뢰할 수 있는 사이트 및 Edge 팝업 차단 설정 클라이언트 쪽 브라우저에 대 한 허용 사이트 및 합니다. 

이렇게 하려면 다음을 수행합니다.
1. Windows 시작 메뉴에서 **인터넷 옵션** 대 한 검색
2. **보안** 탭으로 이동
3. **신뢰할 수 있는 사이트** 옵션 아래에서 **사이트** 단추를 클릭 하 고 표시 되는 대화 상자에서 Url을 추가 합니다. 게이트웨이 URL을 추가 해야로 https://login.microsoftonline.com 및 https://login.live.com.
4. **개인 정보** 탭으로 이동
5. **팝업 차단** 섹션에서 **설정** 단추를 클릭 하 고 표시 되는 대화 상자에 Url을 추가 합니다. 게이트웨이 URL을 추가 해야로 https://login.microsoftonline.com 및 https://login.live.com.


[[맨 위로]](#toc)

<a id="azissue"></a>

## 문제가 발생 하는 Azure 관련 기능?

하세요 보내려면 전자 메일에서 다음 정보를 사용 하 여 wacFeedbackAzure@microsoft.com:
* [질문 아래에 나열 된](#filebug)일반 문제 정보입니다. 
* 문제 및 문제를 재현 하는 데 걸린 단계를 설명 합니다. 
* 가 이전에 게이트웨이를 새로 AadApp.ps1 다운로드할 수 있는 스크립트를 사용 하 여 Azure에 등록 하 고 1807 버전으로 업그레이드 한 후? 또는 게이트웨이를 게이트웨이 설정 gt_ Azure에서에서 UI를 사용 하 여 Azure에 등록할 수 있나요?
* 여러 디렉터리/테 넌 트와 연결 된 Azure 계정 인가요?
    * 예: Windows Admin Center를 Azure AD 응용 프로그램을 등록할 때 기본 디렉터리를 사용 하는 Azure의 디렉터리를? 
* Azure 계정에 여러 구독에 액세스할 수 있습니까?
* 사용 중인 구독 청구 연결 되어 있습니까?
* 사용자 로그인 한 여러 Azure 계정에 문제가 발생 했을 때?
* Azure 계정에 다단계 인증을 해야 합니까?
* Azure VM 관리 하려는 컴퓨터 인가요?
* Azure VM에서 Windows Admin Center 설치 되어 있습니까?

[[맨 위로]](#toc)

<a id="filebug"></a>

## 작동 하는 여전히 하지 않거나 여기 캡처되지 문제가 발생 하는? [문제 해결 일반적인 질문]

이벤트 뷰어 > 응용 프로그램 및 서비스 > Microsoft-ServerManagementExperience로 이동하여 오류나 경고를 찾습니다.

문제를 설명하는 [UserVoice](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5BBug%5D)에서 버그를 보고합니다.

다음 정보를 비롯하여 이벤트 로그에서 찾은 오류 또는 경고를 포함하십시오. 

* Windows Admin Center가 **설치된** 플랫폼(Windows 10 또는 Windows Server):
    * 서버에 설치 된 경우는 Windows Admin Center에 액세스할 수 있는 **브라우저를 실행 하는 컴퓨터** 의 Windows [버전](#winvercompat) : 
    * 설치 관리자를 통해 만들어진 자체 서명 된 인증서를 사용 하 고 있습니까?
    * 자체 인증서를 사용하는 경우 주체 이름이 컴퓨터와 일치합니까?
    * 자체 인증서를 사용하는 경우 대체 주체 이름이 지정되었습니까?
* 기본 포트 설정을 사용하여 설치했습니까?
    * 그렇지 않은 경우 어떤 포트를 지정했습니까?
* Windows Admin Center가 **설치된** 컴퓨터가 도메인에 가입되어 있습니까?
* Windows Admin Center가 **설치된** Windows [버전](#winvercompat):
* **관리하려는** 컴퓨터가 도메인에 가입되었습니까?
* **관리하려는** 컴퓨터의 Windows [버전](#winvercompat):
* 어떤 브라우저를 사용하고 있습니까?
    * Google Chrome을 사용하는 경우 버전은 무엇입니까? (도움말 > Google Chrome 정보)

[[맨 위로]](#toc)