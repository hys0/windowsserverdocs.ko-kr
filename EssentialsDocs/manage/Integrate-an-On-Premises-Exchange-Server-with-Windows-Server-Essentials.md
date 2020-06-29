---
title: 온-프레미스 Exchange Server와 Windows Server Essentials 통합
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: b56a21e2-c9e3-4ba9-97d9-719ea6a0854b
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 13de76ba7e9452e6498479b060712d06c0571c1a
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470888"
---
# <a name="integrate-an-on-premises-exchange-server-with-windows-server-essentials"></a>온-프레미스 Exchange Server와 Windows Server Essentials 통합

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

이 가이드에서는 Exchange Server를 실행하는 온-프레미스 서버를 설치하고 Windows Server Essentials를 실행하는 서버와 통합하는 데 도움이 되는 정보 및 기본 지침을 제공합니다.

 Exchange Server를 실행하는 온-프레미스 서버를 Windows Server Essentials 네트워크에 배포하기 전에 이 가이드를 읽어야 합니다.

> [!NOTE]
>  Exchange Server 2010은 Windows Server 2012를 실행하는 컴퓨터에 설치할 수 없습니다.

## <a name="prerequisites"></a>전제 조건
 Windows Server Essentials 네트워크에 Exchange Server를 설치하기 전에 이 섹션에 설명된 작업을 완료해야 합니다.

-   [Windows Server Essentials를 실행하는 서버 설치](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_SetUpSBS8)

-   [Exchange Server를 설치할 두 번째 서버 준비](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_SecondServer)

-   [인터넷 도메인 이름 구성](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_DomainNames)

###  <a name="set-up-a-server-that-is-running-windows-server-essentials"></a><a name="BKMK_SetUpSBS8"></a>Windows Server Essentials를 실행 하는 서버 설정
 Windows Server Essentials를 실행하는 서버가 이미 설치되어 있어야 합니다. 이 서버는 Exchange Server를 실행하는 서버의 도메인 컨트롤러 역할을 합니다. Windows Server Essentials를 설치하는 방법에 대한 자세한 내용은 [Windows Server Essentials 설치](../install/Install-Windows-Server-Essentials.md)를 참조하세요.

###  <a name="prepare-a-second-server-on-which-to-install-exchange-server"></a><a name="BKMK_SecondServer"></a>Exchange Server를 설치할 두 번째 서버 준비
 Exchange Server 2010 또는 Exchange Server 2013 실행을 정식으로 지원하는 버전의 Windows Server 운영 체제를 실행 중인 두 번째 서버에 Exchange Server를 설치해야 합니다. 그런 다음 두 번째 서버를 Windows Server Essentials 도메인에 가입시켜야 합니다.

 두 번째 서버를 Windows Server Essentials 도메인에 가입 하는 방법에 대 한 자세한 내용은 [연결 된 Get](../use/Get-Connected-in-Windows-Server-Essentials.md)에서 두 번째 서버를 네트워크에 가입을 참조 하세요.

> [!NOTE]
>  Microsoft에서는 Windows Server Essentials를 실행하는 서버에 Exchange Server 설치를 지원하지 않습니다.

###  <a name="configure-your-internet-domain-name"></a><a name="BKMK_DomainNames"></a>인터넷 도메인 이름 구성
 Exchange Server를 실행하는 온-프레미스 서버를 Windows Server Essentials와 통합하려면 회사의 올바른 인터넷 도메인 이름(예: *contoso.com*)을 등록해야 합니다. 또한 도메인 이름 공급자와 함께 Exchange Server에 필요한 DNS 리소스 레코드를 만들어야 합니다.

 예를 들어 회사의 인터넷 도메인 이름이 contoso.com인 경우 *mail.contoso.com*의 FQDN(정규화된 도메인 이름)을 사용하여 Exchange Server를 실행하는 온-프레미스 서버를 참조하려면 도메인 이름 공급자와 함께 다음 표의 DNS 리소스 레코드를 만들어야 합니다.


| 리소스 레코드 이름 |     레코드 형식     |                                                                         레코드 설정                                                                          |                                                                                                                                                                                                                                                              설명                                                                                                                                                                                                                                                              |
|----------------------|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         mail         |      호스트(A)       |                                                        Address=*ISP가 할당한 공용 IP 주소*                                                         |                                                                                                                                                                                                   Exchange Server에서 mail.contoso.com으로 주소가 지정된 메일을 받습니다.<br /><br /> 원하는 다른 이름을 사용할 수 있습니다.                                                                                                                                                                                                    |
|          MX          | MX(메일 교환기) |                                            Hostname=@<br /><br /> Address=mail.contoso.com<br /><br /> Preference=0                                             |                                                                                                                                                                                                      는 email@contoso.com Exchange server를 실행 하는 온-프레미스 서버에 도착할 메일 메시지 라우팅을 제공 합니다.                                                                                                                                                                                                       |
|         SPF          |     텍스트(TXT)      |                                                                        v=spf1 a mx ~all                                                                         |                                                                                                                                                                                                                      서버에서 보낸 메일이 스팸으로 식별되지 않도록 도와주는 리소스 레코드입니다.                                                                                                                                                                                                                      |
|  autodiscover._tcp   |    서비스(SRV)    | 서비스: _autodiscover<br /><br /> Protocol: _tcp<br /><br /> 우선 순위: 0<br /><br /> 가중치: 0<br /><br /> 포트: 443<br /><br /> Target host: mail.contoso.com | Microsoft Office Outlook 및 모바일 디바이스에서 Exchange Server를 실행하는 온-프레미스 서버를 자동으로 검색하도록 해줍니다.<br /><br /> **참고:** 또한 자동 검색 호스트 (A) 리소스 레코드를 구성 하 고 Exchange Server를 실행 하는 온-프레미스 서버의 공용 IP 주소에 대 한 레코드를 가리킬 수 있습니다. 그러나 이 옵션을 구현하려면 mail.contoso.com 및 autodiscover.contoso.com 도메인 이름을 둘 다 지원하는 SAN(주체 대체 이름) SSL 인증서도 제공해야 합니다. |

> [!NOTE]
>  -   이 예의 *contoso.com* 인스턴스를 등록한 인터넷 도메인 이름으로 바꾸세요.

 Exchange Server를 실행하는 온-프레미스 서버에 대해 Windows Server Essentials를 실행하는 서버에 사용 중인 FQDN과 다른 FQDN을 선택해야 합니다. 예를 들어 컴퓨터에서 인터넷을 통해 Windows Server Essentials를 실행하는 서버에 액세스하는 데 사용하는 FQDN으로 *remote.contoso.com*을 사용하도록 선택할 수 있습니다. *mail.contoso.com*은 Exchange Server를 실행하는 온-프레미스 서버로 메일을 라우팅하는 데 사용되는 FQDN으로 사용할 수 있습니다.

## <a name="install-exchange-server"></a>Exchange Server 설치
 Windows Server Essentials에서 Exchange Server 통합 기능은 다음 버전의 Exchange Server를 지원합니다.

- Exchange Server 2013

- Exchange Server 2010 서비스 팩 1(SP1)

  두 번째 서버에 Exchange Server를 설치하기 전에 먼저 **Enterprise Admins** 그룹에 현재 관리자 계정을 추가해야 합니다.

#### <a name="to-add-the-current-administrator-account-to-the-enterprise-admins-group"></a>Enterprise Admins 그룹에 현재 관리자 계정을 추가하려면

1.  Windows Server Essentials에 관리자로 로그온합니다.

2.  관리자 권한으로 Windows PowerShell을 실행합니다.

3.  Windows PowerShell 명령 프롬프트에서 **Add-ADGroupMember "Enterprise Admins" $env: username**을 입력 한 다음 enter 키를 누릅니다.

#### <a name="to-install-exchange-server"></a>Exchange Server를 설치하려면

1.  두 번째 서버에 관리자로 로그온합니다.

2.  인터넷 브라우저를 열고 [Exchange Server 배포 도우미](https://go.microsoft.com/fwlink/p/?LinkID=249163) 웹 사이트로 이동합니다.

3.  **On-Premises Only**를 클릭합니다.

4.  설치할 Exchange Server의 버전에 대해 새 설치 옵션을 클릭합니다.

    > [!NOTE]
    >  Windows Small Business Server 설치에서 마이그레이션 중인 경우 마이그레이션 단계를 포함하는 적절한 업그레이드 옵션을 선택해야 합니다.

5.  다음 페이지에서 기본 설정을 그대로 사용하고 **다음**을 클릭합니다.

    > [!NOTE]
    >  Exchange Server의 새 설치에서 공용 폴더를 사용하려면 해당 설정을 **예**로 변경합니다.

6.  검사 목록의 단계별 지침에 따라 Exchange Server를 배포합니다.

     Exchange Server 배포 도우미를 통해 다음 작업을 수행할 수도 있습니다.

    -   검사 목록 복사본을 인쇄합니다.

    -   메일 받는 사람에게 검사 목록 복사본을 보냅니다.

    -   PDF 파일로 검사 목록 다운로드

> [!NOTE]
> - 항상 Exchange Server를 실행하는 서버에 관리 도구를 설치하도록 선택해야 합니다. 관리 도구는 Windows Server Essentials의 Exchange Server 통합 기능에 필요합니다.
>   -   가상 디렉터리를 구성해야 하는 경우 **InternalUrl** 속성을 각 가상 디렉터리의 **ExternalUrl** 속성과 동일한 URL로 설정하는 것이 좋습니다. 자세한 내용은 Exchange Server 2010 온라인 도움말 웹 사이트에서 [클라이언트 액세스 서버 가상 디렉터리 관리](https://go.microsoft.com/fwlink/p/?LinkId=251058) 를 참조하세요.
>   -   Windows Server Essentials의 원격 웹 액세스 사이트 내에서 OWA(Outlook Web Access)에 액세스하려면 OWA에 대한 외부 URL 속성을 설정해야 합니다.

 Exchange Server 2010을 새로 설치하는 경우에는 다음 스크립트를 사용하여 Exchange Server를 설치할 수도 있습니다.

#### <a name="to-use-scripts-to-set-up-exchange-server"></a>스크립트를 사용하여 Exchange Server를 설치하려면

1.  메모장을 열고 다음 스크립트를 새 파일에 붙여 넣습니다.

```powershell
Import-Module ServerManager

Add-WindowsFeature NET-Framework,RSAT-ADDS,Web-Server,Web-Basic-Auth,Web-Windows-Auth,Web-Metabase,Web-Net-Ext,Web-Lgcy-Mgmt-Console,WAS-Process-Model,RSAT-Web-Server,Web-ISAPI-Ext,Web-Digest-Auth,Web-Dyn-Compression,NET-HTTP-Activation,Web-Asp-Net,Web-Client-Auth,Web-Dir-Browsing,Web-Http-Errors,Web-Http-Logging,Web-Http-Redirect,Web-Http-Tracing,Web-ISAPI-Filter,Web-Request-Monitor,Web-Static-Content,Web-WMI,RPC-Over-HTTP-Proxy  Restart
```

2. 파일을 **InstallDependencies.ps1**로 저장합니다.

3. 서버의 한 곳에 Exchange SSL 인증서를 복사합니다.

4. 새 메모장 파일을 열고 다음 텍스트를 파일에 복사합니다.

```powershell
param (
    [string]
    [Parameter(Mandatory=$true, HelpMessage = "The path to your Certificate file, must be a *.pfx format")]
    $CertPath = "c:\certificates\ExchangeCertificate.pfx",
    [Security.SecureString]
    [Parameter(Mandatory=$true, HelpMessage = "The password of your cert")]
    $CertPassword = $null,
    [string]
    [Parameter(Mandatory=$true, HelpMessage = "Domain Name, eg. contoso.com")]
    $DomainName = "contoso.com",
    [string]
    [Parameter(Mandatory=$true, HelpMessage = "Server IP Address, eg. 192.168.0.1")]
    $ServerIpAddress = "192.168.0.1",
    [string]
    [Parameter(Mandatory=$true, HelpMessage = "Internal Ip Range, eg. 192.168.0.0-192.168.0.255")]
    $InternalIpRange = "192.168.0.0-192.168.0.255"
)

#Import Exchange Certificate, and Enable it for POP IIS IMAP SMTP services.

Import-ExchangeCertificate  -FileData ([Byte[]]$(Get-content -Path $CertPath  -Encoding byte  -ReadCount 0)) -Password:$CertPassword -Force | Enable-ExchangeCertificate -Services 'POP, IIS, IMAP, SMTP' -Force

#New AcceptedDomain and set it to default

New-AcceptedDomain  -Name "official name"  -DomainName $domainname

Set-AcceptedDomain  -Identity "official name"  -MakeDefault $true

#New EmailAddress Policy

$address = "%m@" + $DomainName

New-EmailAddressPolicy -Name "Windows Server Essentials Email Address Policy" -IncludedRecipients AllRecipients -EnabledPrimarySMTPAddressTemplate $address

#Set owa and ecp VirtualDirectory ExternalUrl

$hostname = "mail." + $DomainName

$owa = "https://" + $hostname + "/owa"

$ecp = "https://" + $hostname + "/ecp"

$activesync = "https://" + $hostname + "/Microsoft-Server-ActiveSync"

$oab = "https://" + $hostname + "/OAB"

$ews = "https://" + $hostname + "/EWS/Exchange.asmx"

Get-OwaVirtualDirectory | Set-OwaVirtualDirectory  -ExternalUrl $owa  -InternalUrl $owa

Get-EcpVirtualDirectory | Set-EcpVirtualDirectory  -ExternalUrl $ecp  -InternalUrl $ecp

Get-ActiveSyncVirtualDirectory | Set-ActiveSyncVirtualDirectory -ExternalUrl $activesync  -InternalUrl $activesync

Get-OABVirtualDirectory | Set-OABVirtualDirectory -ExternalUrl $oab -InternalUrl $oab -RequireSSL:$true

Get-WebServicesVirtualDirectory | Set-WebServicesVirtualDirectory -ExternalUrl $ews -InternalUrl $ews -BasicAuthentication:$True -Force

#Enable outlook Anywhere

Enable-OutlookAnywhere  -ClientAuthenticationMethod:Basic  -ExternalHostname:$hostname  -SSLOffloading:$false

#new receive/send connector

$machinename = get-content env:computername

$bindingIpaddress = $ServerIpAddress + ":25"

$ReceiveConnectorName = $machinename + "\Default " + $machinename

Set-ReceiveConnector $ReceiveConnectorName -RemoteIPRanges $InternalIpRange

New-ReceiveConnector -Name "WSE Internet Receive Connector" -Usage "Internet" -Bindings $bindingIpaddress -Fqdn $hostname -Enabled $true -Server $machinename -AuthMechanism Tls,BasicAuth,BasicAuthRequireTLS,Integrated

New-SendConnector -Name "WSE Internet SendConnector" -Usage "Internet" -AddressSpaces 'SMTP:*;1' -IsScopedConnector $false -DNSRoutingEnabled $true -UseExternalDNSServersEnabled $true -SourceTransportServers $machinename
```

5. 스크립트 시작 부분의 스크립트를 네트워킹 환경에 맞게 설정합니다.

6. 파일을 **ConfigureExchange.ps1**로 저장합니다.

7. 관리자 권한으로 Windows PowerShell을 실행합니다.

8. Windows PowerShell 명령 프롬프트에 **Set-ExecutionPolicy RemoteSigned**를 입력하고 Enter 키를 누릅니다.

9. **InstallDependencies.ps1** 스크립트를 실행합니다.

10. 서버를 다시 시작한 후 관리자 권한으로 Windows PowerShell을 실행합니다.

11. Windows PowerShell 명령 프롬프트에서 다음 스크립트를 실행합니다.

    `E:\setup.com /mode:install /roles:mb,ht,ca /OrganizationName:"First Organization"`

   > [!NOTE]
   >  Exchange Server 설치 프로그램의 정확한 경로를 입력해야 합니다.

12. Exchange Server 설치가 완료되면 관리자 권한으로 Exchange 관리 셸을 엽니다.

13. Exchange 관리 셸 명령 프롬프트에 **Set-ExecutionPolicy RemoteSigned**를 입력한 후 Enter 키를 누릅니다.

14. **ConfigureExchange.ps1**스크립트를 실행합니다.

15. 서버를 다시 시작합니다.

> [!NOTE]
>  자체 발급 된 인증서 대신 공개적으로 신뢰할 수 있는 SSL 인증서를 사용 하려는 경우 설치 가이드의 지침에 따라 인증서 요청을 만들어 선택한 인증 기관에 보낼 수 있습니다. 또한 Exchange PowerShell cmdlet을 사용하여 인증서 요청을 만들 수도 있습니다. 예제는 다음과 같습니다.
>
>  `New-ExchangeCertificate -GenerateRequest -SubjectName "C=US, S=Washington, L=Redmond, O=contoso, OU=contoso, CN=mail.contoso.com" -DomainName mail.contoso.com -PrivateKeyExportable $true | Set-Content -path "c:\Docs\MyCertRequest.req"`
>
>  네트워킹 환경에 맞게 스크립트 매개 변수를 사용자 지정합니다.

## <a name="post-installation-tasks"></a>사후 설치 태스크
 이 섹션에서는 사후 설치 단계에서 완료해야 할 수 있는 서버 구성 작업을 설명합니다. 여기에는 Exchange Server를 실행하는 온-프레미스 서버를 Windows Server Essentials 네트워크에 설치하는 작업과 관련된 정보가 포함됩니다.

### <a name="add-the-public-email-domain-and-configure-the-email-address-policies"></a>공용 메일 도메인 추가 및 메일 주소 정책 구성

> [!NOTE]
>  이 작업은 새로 설치를 수행하는 경우에 필요합니다. Windows Small Business Server에서 마이그레이션하는 경우에는 이 단계를 건너뛰세요.

 메일 도메인을 기본 허용 도메인으로 지정하고 메일 주소 정책을 구성해야 합니다.

##### <a name="to-add-your-email-domain-as-the-default-accepted-domain"></a>메일 도메인을 기존 허용 도메인으로 추가하려면

1.  Exchange Server 문서 [허용 도메인 만들기](https://go.microsoft.com/fwlink/p/?LinkId=249174) 의 지침에 따라 허용 도메인을 추가합니다.

2.  두 번째 서버에 관리자로 로그온하여 Exchange 관리 콘솔을 열고 **조직 구성**의 **허브 전송** 탭으로 이동합니다.

3.  Exchange 관리 콘솔 작업 창에서 새 허용 도메인을 마우스 오른쪽 단추로 클릭한 다음 **기본값으로 설정**을 클릭합니다.

4.  Exchange Server 문서 [메일 주소 정책 만들기](https://go.microsoft.com/fwlink/p/?LinkId=249179) 의 지침에 따라 새 메일 주소 정책을 만듭니다. 메일 주소를 제외하고 모든 기본값을 그대로 사용할 수 있습니다. 메일 주소에 대해 공용 메일 도메인을 지정합니다.

### <a name="create-smtp-send-and-receive-connectors"></a>SMTP 송신 및 수신 커넥터 만들기

> [!NOTE]
>  필수 작업입니다.

 메일 메시지의 아웃바운드/인바운드 전송을 위한 SMTP 송신 커넥터 및 SMTP 수신 커넥터를 구성해야 합니다.

 SMTP 송신 커넥터를 만들려면 Exchange Server 문서 [SMTP 송신 커넥터 만들기](https://technet.microsoft.com/library/aa997285.aspx)의 지침을 따릅니다.

 SMTP 수신 커넥터를 만들려면 Exchange Server 문서 [SMTP 수신 커넥터 만들기](https://technet.microsoft.com/library/bb125159.aspx)의 지침을 따릅니다.

 필요한 경우 이 문서 앞부분에 설명된 스크립트를 참조하여 Exchange PowerShell cmdlet을 통해 송신 및 수신 커넥터를 만들 수 있습니다.

### <a name="configure-the-network-router"></a>네트워크 라우터 구성

> [!NOTE]
>  이 작업은 새로 설치를 수행하는 경우에 필요합니다. Windows Small Business Server에서 마이그레이션하는 경우에는 [Windows Server Essentials로 서버 데이터 마이그레이션](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)에서 네트워크 구성 방법에 대한 지침을 참조하세요.

 최소한 라우터의 다음 포트 설정을 구성해야 합니다.

|라우터 포트|대상 IP|대상 포트|참고|
|-----------------|--------------------|----------------------|----------|
|25(SMTP)|Exchange Server를 실행하는 온-프레미스 서버의 내부 IP|25||
|80(HTTP)|Windows Server Essentials를 실행하는 서버의 내부 IP|80||
|443(HTTPS)|Windows Server Essentials를 실행하는 서버의 내부 IP|443||

 네트워크에서 POP3 또는 IMAP 메시징 프로토콜을 지원하는 경우 이러한 프로토콜에 대한 포트 전달도 구성해야 합니다. 관련 정보는 Exchange Server TechNet 라이브러리에서 **Exchange 네트워크 포트 참조** 항목의 [클라이언트 액세스 서버](https://go.microsoft.com/fwlink/p/?LinkId=250773) 섹션을 참조하세요.

> [!NOTE]
> - Windows Server Essentials를 실행하는 서버와 Exchange Server를 실행하는 두 번째 서버에 대해 고정 IP 주소를 구성하는 것이 좋습니다. Windows Server 2003 또는 Windows Server 2008 R2를 실행하는 컴퓨터에서 고정 IP 주소를 구성하는 방법에 대한 자세한 내용은 Windows Server TechNet 라이브러리에서 [고정 IP 주소 구성](https://technet.microsoft.com/library/cc754203\(v=ws.10\).aspx) 을 참조하세요.
>
>   **참고:** DNS 서버 설정은 항상 Windows Server Essentials를 실행 하는 서버의 IP 주소를 가리켜야 합니다.
>   -   라우터에서 Windows Server Essentials를 실행하는 서버의 IP 주소와 Exchange Server를 실행하는 서버의 IP 주소가 예약되어 있거나 DHCP IP 주소 범위를 벗어나는지 확인하세요.
>   -   이 섹션의 라우터 구성에서는 ISP(인터넷 서비스 공급자)가 할당한 공용 IP 주소가 하나만 있는 것으로 가정합니다. 공용 IP 주소가 여러 개인 경우 Windows Server Essentials를 실행하는 서버와 Exchange Server를 실행하는 서버에 서로 다른 IP 주소를 할당한 후 공용 IP 주소를 기반으로 포트 전달을 만들 수 있습니다.

### <a name="enable-on-premises-exchange-server-integration-on-windows-server-essentials"></a>Windows Server Essentials에서 온-프레미스 Exchange Server 통합 사용

> [!NOTE]
>  Windows Small Business Server 설치에서 마이그레이션하는 경우 지금은 이 단계를 건너뛰고 나중에 원본 서버에서 Exchange Server의 이전 설치를 제거한 후 실행하는 것이 좋습니다.

 Exchange Server를 실행하는 서버를 설치하고 구성한 후에는 Windows Server Essentials를 실행하는 서버에서 온-프레미스 Exchange Server 통합을 사용하도록 설정해야 합니다.

##### <a name="to-enable-on-premises-exchange-server-integration-from-the-dashboard"></a>대시보드에서 온-프레미스 Exchange Server 통합을 사용하도록 설정하려면

1.  Windows Server Essentials를 실행하는 서버에 관리자로 로그온하여 대시보드를 엽니다.

2.  **홈** 페이지에서 **내 메일 서비스에 연결**을 클릭한 다음 **Exchange Server 통합**을 클릭합니다.

3.  정보 창에서 **Exchange Server 통합 설정**을 클릭합니다.

4.  마법사의 지시를 따릅니다.

### <a name="configure-a-reverse-proxy"></a>역방향 프록시 구성

> [!NOTE]
>  이 작업은 인터넷 서비스 공급자의 인터넷 연결이 하나만 있는 경우에 필요합니다.

 Windows Server Essentials와 Exchange Server 둘 다 네트워크 사용자에 대한 몇 가지 원격 액세스 시나리오를 지원합니다. 예를 들어 Windows Server Essentials를 실행하는 서버에서 원격 액세스를 설정한 경우 원격 웹 액세스 사이트에 원격으로 액세스하거나 VPN(가상 사설망)을 사용하여 Windows Server Essentials 네트워크에 원격으로 연결할 수 있습니다. 메일 메시지에 원격으로 액세스하려면 외부에서 Outlook 사용, Outlook Web Access(OWA) 또는 ActiveSync를 사용해야 합니다.

 Exchange Server를 실행하는 서버와 Windows Server Essentials가 둘 다 같은 라우터에 연결되어 있고 인터넷 서비스 공급자와 라우터 간의 인바운드 인터넷 연결이 하나뿐인 경우에는 역방향 프록시 솔루션을 사용하여 인터넷을 통한 여러 유형의 원격 액세스 요청을 대상 호스트 이름에 따라 라우팅해야 합니다. Microsoft에서 지원하는 IIS ARR(애플리케이션 요청 라우팅) 확장을 역방향 프록시 솔루션으로 사용하는 것이 좋습니다. IIS 애플리케이션 요청 라우팅에 대한 자세한 내용은 [애플리케이션 요청 라우팅 웹 사이트](https://go.microsoft.com/fwlink/p/?LinkId=249181)를 참조하세요.

##### <a name="to-install-and-configure-application-request-routing"></a>애플리케이션 요청 라우팅을 설치 및 구성하려면

1. Windows Server Essentials에 관리자로 로그온합니다.

2. 인터넷 브라우저를 열고 [애플리케이션 요청 라우팅 웹 사이트](https://go.microsoft.com/fwlink/p/?LinkId=249181)로 이동합니다.

3. ARR 웹 사이트에서 **설치**를 클릭한 후 지시에 따라 ARR을 설치합니다.

   > [!NOTE]
   >  ARR을 설치하는 동안 URL 재작성 모듈을 선택해야 합니다.
   >
   >  ARR 설치가 끝난 후 KB 2589179 for ARR 2.5가 제대로 설치되지 않았음을 나타내는 오류가 발생할 수 있습니다. 이 오류는 무시해도 됩니다.

4. ARR 설치가 완료되면 **원격 데스크톱 게이트웨이** 서비스(실행 중이지 않은 경우)를 다시 시작합니다.

   > [!NOTE]
   >  ARR 설치 후 **원격 데스크톱 게이트웨이** 서비스가 중지될 수도 있습니다. 서비스를 수동으로 다시 시작하려면 **서비스** 관리 도구를 열고 **원격 데스크톱 게이트웨이** 서비스를 다시 시작하세요.

5. [KB2732764 for ARR 2.5를 다운로드](https://go.microsoft.com/fwlink/?LinkID=258302)한 다음 Windows Server Essentials를 실행하는 서버에 업데이트를 설치합니다.

6. Windows Server Essentials를 실행하는 서버에 Exchange Server의 SSL 인증서 파일을 복사합니다. 인증서 파일은 프라이빗 키를 포함해야 하며 PFX 파일 형식이어야 합니다.

   > [!NOTE]
   >  자체 발급된 인증서를 사용하는 경우 Exchange Server 문서 [Exchange 인증서 내보내기](https://technet.microsoft.com/library/dd351274.aspx) 의 지침에 따라 인증서를 내보냅니다.

7. 실행 중인 Windows Server Essentials 버전에 따라 다음 중 하나를 수행합니다.

   -   Windows Server Essentials에서: 관리자 권한으로 명령 창을 열고%ProgramFiles%\Windows Server\Bin 디렉터리를 엽니다.

   -   Windows Server Essentials에서: 관리자 권한으로 명령 창을 열고%Windir%\System32\Essentials 디렉터리를 엽니다.

8. 설치 시나리오에 따라 다음 단계 중 하나를 수행하여 ARR을 구성합니다.

   - 새로 설치를 수행하는 경우 다음 명령을 실행합니다.

      **Arrconfig 구성-** _인증서 파일에_ 대 한 인증서 경로 **-** _Exchange Server에 대 한 호스트 이름 호스트 이름_

     > [!NOTE]
     >  예를 들면 **Arrconfig 구성-cert** _c:\temp\certificate.pfx_ **-호스트 이름** _mail.contoso.com_
     >
     >  *mail.contoso.com*을 인증서로 보호되는 도메인 이름으로 바꿉니다.

   - Windows Small Business Server에서 마이그레이션하는 경우 다음 명령을 실행합니다.

      **Arrconfig 구성-** _인증서 파일에_ 대 한 인증서 경로 **-** exchange _server의 호스트 이름 호스트 이름_ **-targetserver** _서버 이름 (exchange server의_ 경우)

      예를 들면 **Arrconfig config-cert** _c:\temp\certificate.pfx_ **-** _mail.contoso.com_ **-targetserver** _ExchangeSvr_

      *mail.contoso.com*을 도메인 이름으로 바꾸고, *ExchangeSvr*를 Exchange Server를 실행하는 서버 이름으로 바꿉니다.

9. 메시지가 나타나면 인증서 암호를 입력합니다.

> [!NOTE]
> - 제공한 호스트 이름은 Exchange Server용으로 구입한 SSL 인증서에 포함되어 있어야 합니다.
>   -   호스트 이름이 여러 개인 경우 쉼표(,)를 사용하여 구분합니다.

 구성이 작동 하는지 확인 하려면 Exchange Server를 실행 하는 서버의 OWA 웹 사이트 ()에 액세스 해 봅니다 https://mail . *yourdomainname*.com/owa)에 액세스해 봅니다. 연결 문제를 해결하기 위해 온라인 [Microsoft 원격 연결 분석기](https://go.microsoft.com/fwlink/p/?LinkId=249455) 도구를 사용할 수도 있습니다.

### <a name="configure-split-dns-for-exchange-server"></a>Exchange Server에 대해 분할 DNS 구성

> [!NOTE]
>  이 작업은 권장 작업입니다.

 분할 DNS를 사용하면 DNS 요청이 발생한 위치에 따라 동일한 호스트 이름에 대해 DNS에서 여러 IP 주소를 구성할 수 있습니다. 클라이언트 컴퓨터가 인트라넷에 있는 경우 DNS 요청은 인트라넷 IP 주소로 확인되고, 클라이언트 컴퓨터가 인터넷에 있는 경우 DNS 요청은 인터넷 IP 주소로 확인됩니다. 이는 사용자에게 투명하게 작동합니다.

 사용자가 위치에 관계없이 항상 같은 호스트 이름을 사용하여 Exchange Server 서비스에 액세스할 수 있도록 분할 DNS를 구성하는 것이 좋습니다.

##### <a name="to-configure-split-dns-for-exchange-server"></a>Exchange Server에 대해 분할 DNS를 구성하려면

1.  Windows Server Essentials에 관리자로 로그온하여 DNS 관리자를 엽니다.

2.  DNS 관리자 콘솔 트리에서 서버를 마우스 오른쪽 단추로 클릭한 후 **새 영역**을 클릭합니다. **새 영역 마법사**가 표시됩니다.

3.  마법사의 **영역 형식** 페이지에서 기본 옵션을 그대로 사용하고 **다음**을 클릭합니다.

4.  **Active Directory 영역 복제 범위** 페이지에서 기본 옵션을 그대로 사용하고 **다음**을 클릭합니다.

5.  **정방향 또는 역방향 조회 영역** 페이지에서 **정방향 조회 영역**을 그대로 사용하거나 선택하고 **다음**을 클릭합니다.

6.  **영역 이름** 페이지에서 Exchange Server를 실행하는 서버의 FQDN(예: *mail.contoso.com*)을 입력한 후 **다음**을 클릭합니다.

7.  **동적 업데이트** 페이지에서 기본 옵션을 그대로 사용하고 **다음**, **마침**을 차례로 클릭합니다.

8.  DNS 관리자 콘솔 트리에서 새 정방향 조회 영역을 마우스 오른쪽 단추로 클릭한 다음 **새 호스트(A 또는 AAAA)** 를 클릭합니다.

9. **새 호스트** 페이지에서 **이름** 필드를 빈 상태로 두고 Exchange Server를 실행하는 서버의 인트라넷 IP 주소를 입력한 후 **호스트 추가**를 클릭합니다.

    > [!NOTE]
    >  **이름** 필드를 빈 상태로 두면 서버에서 기본적으로 상위 도메인 이름을 사용합니다.

10. **새 호스트** 페이지에서 **완료**를 클릭합니다.

> [!NOTE]
>  ActiveSync를 사용하지만 일부 사서함 계정에 대해 메일을 동기화할 수 없는 경우 해당 계정이 Domain Administrators와 같은 하나 이상의 보호된 그룹에 속해 있는지 확인하세요. 이 문제를 해결하는 데 도움이 될 수 있는 관련 정보는 [Exchange ActiveSync에서 HTTP 500 오류를 반환함](https://technet.microsoft.com/library/dd439375\(EXCHG.80\).aspx)을 참조하세요.

## <a name="related-topics"></a>관련 항목
 온-프레미스 Exchange Server를 통합하는 방법에 대한 자세한 내용은 다음 섹션을 참조하세요.

### <a name="what-happens-if-i-disable-exchange-integration"></a>Exchange 통합을 사용하지 않도록 설정하면 어떻게 되나요?
 온-프레미스 Exchange Server와의 통합을 사용하지 않도록 설정하면 더 이상 Windows Server Essentials Dashboard를 사용하여 Exchange Server 사서함을 보고 만들거나 관리할 수 없습니다.

### <a name="what-do-i-need-to-know-about-email-accounts"></a>메일 계정에 대해 알아야 할 내용은 무엇인가요?
 호스트된 메일 솔루션은 서버에서 구성됩니다. 호스트 된 전자 메일 공급자의 솔루션 (예: Microsoft Office 365)은 네트워크 사용자에 게 개별 메일 계정을 제공할 수 있습니다. Windows Server Essentials에서 사용자 계정 추가 마법사를 실행하여 사용자 계정을 만들면 마법사는 사용자 계정을 사용 가능한 호스트된 메일 솔루션에 추가하려고 합니다. 동시에 마법사는 사용자에게 메일 이름(별칭)을 할당하고 사서함의 최대 크기(할당량)를 설정합니다. 사서함의 최대 크기는 사용하는 메일 공급자에 따라 다릅니다. 사용자 계정을 추가한 후 계속해서 사용자의 속성 페이지에서 사서함 별칭 및 할당량 정보를 관리할 수 있습니다. 사용자 계정 및 호스트된 메일 공급자의 전체 관리를 위해서는 호스트된 공급자의 관리 콘솔을 사용합니다. 공급자에 따라 웹 기반 포털 또는 서버 대시보드의 탭에서 해당 관리 콘솔에 액세스할 수 있습니다.

 사용자 계정 추가 마법사를 실행할 때 입력한 별칭은 사용자 별칭에 대한 제안된 이름으로 호스트된 메일 공급자에게 전송됩니다. 예를 들어 사용자 별칭이 *FrankM*인 경우 사용자의 전자 메일 주소는 일 수 있습니다 <em>FrankM@Contoso.com</em> .

 또한 사용자 계정 추가 마법사에서 사용자에 대해 설정한 암호는 호스트된 메일 솔루션에서 사용자의 초기 암호가 됩니다.

 마지막으로, 서버에서 사용자 계정 삭제 마법사를 사용하여 사용자를 삭제하는 경우 마법사는 호스트된 메일 공급자에게 해당 시스템에서 사용자를 삭제하라는 요청도 보냅니다. 공급자는 사용자 계정 및 계정과 연결 된 전자 메일을 모두 삭제할 수 있습니다.

 필요한 메일 클라이언트 소프트웨어를 설치하는 방법 또는 메일 계정에 액세스하는 방법에 대한 사용자 정보는 해당 호스트된 메일 공급자가 제공한 도움말 설명서를 참조하세요.

### <a name="what-is-a-mailbox-quota"></a>사서함 할당량이란 무엇인가요?
 네트워크 사용자의 Exchange 사서함 데이터에 할당 된 저장소 공간의 크기를 사서함 할당량 이라고 합니다.

 대시보드에서 **Exchange Server 통합 설정** 작업을 실행하면 마법사가 사서함 할당량을 적용하고 할당량 크기를 지정할지 여부를 선택할 수 있는 페이지를 사용자 계정 추가 마법사에 추가합니다. 기본적으로 **사서함 할당량 적용** 옵션은 선택(설정)되어 있고 사용자 사서함에는 2GB의 저장소 공간이 할당됩니다. Exchange 관리자는 비즈니스 요구에 맞게 사서함 할당량 설정을 사용자 지정할 수 있습니다.

## <a name="additional-references"></a>추가 참조

-   [Windows Server Essentials의 시스템 요구 사항](../get-started/system-requirements.md)

-   [메일 서비스 통합 관리](Manage-Email-Service-Integration-in-Windows-Server-Essentials.md)

-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)
