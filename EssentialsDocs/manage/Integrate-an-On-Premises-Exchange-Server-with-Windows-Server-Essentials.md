---
title: "Windows Server Essentials 온-프레미스 Exchange Server 통합"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b56a21e2-c9e3-4ba9-97d9-719ea6a0854b
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c2020e08b94800a9750f095a2f772afb14ba5f0b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="integrate-an-on-premises-exchange-server-with-windows-server-essentials"></a>Windows Server Essentials 온-프레미스 Exchange Server 통합

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

이 가이드 정보와 기본 설정 및 Windows Server Essentials 실행 하는 서버 Exchange Server을 실행 하는 온-프레미스 서버 통합 하는 데 도움이 지침을 제공 합니다.  
  
 Exchange Server Windows Server Essentials 네트워크에서 실행 되는 온-프레미스 서버를 배포 하기 전에이 가이드를 읽어야 합니다.  
  
> [!NOTE]
>  Exchange Server 2010 Windows Server 2012를 실행 하는 컴퓨터에 설치를 지원 하지 않습니다.  
  
## <a name="prerequisites"></a>필수  
 Exchange Server Windows Server Essentials 네트워크를 설치 하기 전에이 섹션에 설명 하는 작업을 완료 하면 있는지 확인 합니다.  
  
-   [Windows Server Essentials 실행 하는 서버 설정](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_SetUpSBS8)  
  
-   [두 번째 서버를 Exchange Server 설치할 준비](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_SecondServer)  
  
-   [인터넷 도메인 이름 구성](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_DomainNames)  
  
###  <a name="BKMK_SetUpSBS8"></a>Windows Server Essentials 실행 하는 서버 설정  
 Windows Server Essentials 실행 하는 서버를 이미 설정 있는 해야 합니다. Exchange Server 실행 하는 서버에 대 한 도메인 컨트롤러 됩니다. Windows Server Essentials를 설정 하는 방법에 대 한 내용은 [Windows Server Essentials 설치](../install/Install-Windows-Server-Essentials.md)합니다.  
  
###  <a name="BKMK_SecondServer"></a>두 번째 서버를 Exchange Server 설치할 준비  
 공식적으로 실행 Exchange Server 2010 지원 Windows Server 운영 체제의 버전을 실행 하는 두 번째 서버 또는 Exchange Server 2013 Exchange Server을 설치 해야 합니다. 다음 두 번째 서버를 Windows Server Essentials 도메인에 가입 해야 있습니다.  
  
 두 번째 서버 Windows Server Essentials 도메인에 가입 하는 방법에 대 한 정보를 참조 하세요. 두 번째 서버 네트워크에 가입 [연결](../use/Get-Connected-in-Windows-Server-Essentials.md)합니다.  
  
> [!NOTE]
>  Microsoft은 Windows Server Essentials 실행 하는 서버에 Exchange Server 설치를 지원 하지 않습니다.  
  
###  <a name="BKMK_DomainNames"></a>인터넷 도메인 이름 구성  
 Windows Server Essentials Exchange Server을 실행 하는 온-프레미스 서버를 통합 하 해야 등록 한 사업에 대 한 올바른 인터넷 도메인 이름 (와 같은 *contoso.com*). Exchange Server 필요한 리소스 DNS 레코드 만드는 도메인 이름 공급자에도 사용 해야 합니다.  
  
 예를 들어, 회사 인터넷 도메인 이름 contoso.com 이며의 정식된 도메인 이름 (FQDN)를 사용 하려는 경우 *mail.contoso.com* 다음 표에 있는 리소스 DNS 레코드 만드는 도메인 이름 공급자 함께 일 Exchange Server 실행 하는 온-프레미스 서버를 참조 하세요.  
  
|리소스 기록 이름|녹화 유형|녹화 설정|설명|  
|--------------------------|-----------------|--------------------|-----------------|  
|메일|호스트 (A)|주소 =*ISP에서 할당 공개 IP 주소*|Exchange Server mail.contoso.com 사람에 게 보내는 메일을 받게 됩니다.<br /><br /> 다른 이름에서 직접 선택을 사용할 수 있습니다.|  
|MX|메일 교환기 MX)|호스트 =<br /><br /> 주소 mail.contoso.com =<br /><br /> 기본 = 0|메일 메시지에 대 한 경로 제공 email@contoso.comExchange Server 실행 하는 온-프레미스 서버에 도착 하는 데 합니다.|  
|SPF|텍스트 (TXT)|v를 mx spf1 = ~ 모든|스팸 식별 되 고으로 서버에서 보낸 메일 하지 못하게 되는 리소스 기록 합니다.|  
|autodiscover._tcp|서비스 (SRV)|서비스: _autodiscover<br /><br /> 프로토콜: _tcp<br /><br /> 우선 순위 부여: 0<br /><br /> 무게: 0<br /><br /> 포트: 443<br /><br /> 대상 호스트: mail.contoso.com|Microsoft Office Outlook 및 모바일 장치 Exchange Server 실행 하는 온-프레미스 서버 자동으로 검색 하는 데 사용 합니다.<br /><br /> **참고:** 도 자동 검색 호스트 (는) 리소스 녹화를 구성 하 고 기록 Exchange Server를 실행 하는 온-프레미스 서버의 공개 IP 주소를 가리킨 수 있습니다. 그러나이 옵션을 구현 제공 해야 mail.contoso.com 및 autodiscover.contoso.com 도메인 이름을 지 원하는 제목 대체 이름 (산) SSL 인증서 합니다.|  
  
> [!NOTE]
>  -   인스턴스를 대체 *contoso.com* 을 인터넷 도메인 이름으로 등록 하면 여기서 합니다.  
  
 Windows Server Essentials 실행 하는 서버에 대 한 사용 중인 FQDN 보다 Exchange Server 실행 하는 온-프레미스 서버에 대 한 다른 FQDN 선택 해야 합니다. 예를 들어, 사용 하 여 수도 *remote.contoso.com* FQDN Windows Server Essentials은 인터넷에서 실행 하는 서버에 액세스 하려면 컴퓨터를 사용 하는으로 합니다. 사용할 수 있는 *mail.contoso.com* Exchange Server 실행 하는 온-프레미스 서버에 게 메일을 보낸 하는 데 사용 되는 FQDN으로 합니다.  
  
## <a name="install-exchange-server"></a>Exchange Server 설치  
 다음 버전의 Exchange Server Windows Server Essentials의 Exchange Server 통합 기능을 지원합니다.  
  
-   Exchange Server 2013  
  
-   Exchange Server 2010 서비스 팩 1 (SP1)  
  
 현재 관리자 계정을 Exchange Server 두 번째 서버에 설치 하기 전에 먼저 추가 해야는 **엔터프라이즈 관리자** 그룹입니다.  
  
#### <a name="to-add-the-current-administrator-account-to-the-enterprise-admins-group"></a>엔터프라이즈 관리자 그룹에 현재 관리자 계정을 추가 하려면  
  
1.  Windows Server Essentials 관리자 권한으로 로그온 합니다.  
  
2.  Windows PowerShell을 관리자 권한으로 실행 합니다.  
  
3.  Windows PowerShell 명령 프롬프트에 입력 **추가 ADGroupMember ˜Enterprise 관리자 $env: 사용자 이름**, Enter 키를 누릅니다.  
  
#### <a name="to-install-exchange-server"></a>Exchange Server 설치 하려면  
  
1.  두 번째 서버 관리자 권한으로 로그온 합니다.  
  
2.  인터넷 브라우저를 열고 다음 이동는 [Exchange Server 도우미 배포](https://go.microsoft.com/fwlink/p/?LinkID=249163) 웹 합니다.  
  
3.  클릭 **온-프레미스만**합니다.  
  
4.  Exchange Server을 설치 하는 버전에 대 한 새 설치 옵션을 클릭 합니다.  
  
    > [!NOTE]
    >  Small Business Server Windows 설치에서 마이그레이션하는 경우 마이그레이션 단계에 설명 하는 업그레이드 적절 한 옵션을 선택 해야 합니다.  
  
5.  다음 페이지에서 기본 설정을 클릭 한 다음 **다음**합니다.  
  
    > [!NOTE]
    >  공용 폴더 Exchange server 새로 설치에 사용 하려는 경우에 해당 설정을 변경 **예**합니다.  
  
6.  Exchange Server 배포할 검사 목록에 대 한 단계별 지침을 따릅니다.  
  
     Exchange Server 배포 도우미 수도 있습니다.  
  
    -   검사 복사본을 인쇄 합니다.  
  
    -   메일 받는 사람에 게 검사 목록의 복사본을 보냅니다.  
  
    -   PDF 파일로 검사를 다운로드 합니다.  
  
> [!NOTE]
>  -   Exchange Server 실행 하는 서버 관리 도구를 설치 하려면 항상 선택 해야 합니다. Windows Server Essentials의 Exchange Server 통합 기능을 통해 관리 도구 필요 합니다.  
> -   가상 디렉터리 구성 해야 할 경우도 설정 하는 것이 좋습니다는 **InternalUrl** 속성 동일한 URL을는 **ExternalUrl** 각 가상 디렉터리에 속성 합니다. 자세한 내용은 참조 [관리 클라이언트 액세스 서버 가상 디렉터리](https://go.microsoft.com/fwlink/p/?LinkId=251058) Exchange Server 2010 온라인 도움말 웹 사이트에서 합니다.  
> -   Windows Server Essentials의 원격 Web Access 사이트 내에서 Outlook OWA Web Access ()에서 액세스 하려는 경우 외부 URL 속성 owa 설정 해야 합니다.  
  
 Exchange Server 2010 새로 설치를 설치 하는 경우 다음 스크립트 Exchange Server를 설정 하려면 사용할 수도 있습니다.  
  
#### <a name="to-use-scripts-to-set-up-exchange-server"></a>Exchange Server를 설정 하려면 스크립트를 사용 하려면  
  
1.  메모장 열고 다음 스크립트 새 파일에 붙여 넣습니다.  
  
     `Import-Module ServerManager`  
  
     `Add-WindowsFeature NET-Framework,RSAT-ADDS,Web-Server,Web-Basic-Auth,Web-Windows-Auth,Web-Metabase,Web-Net-Ext,Web-Lgcy-Mgmt-Console,WAS-Process-Model,RSAT-Web-Server,Web-ISAPI-Ext,Web-Digest-Auth,Web-Dyn-Compression,NET-HTTP-Activation,Web-Asp-Net,Web-Client-Auth,Web-Dir-Browsing,Web-Http-Errors,Web-Http-Logging,Web-Http-Redirect,Web-Http-Tracing,Web-ISAPI-Filter,Web-Request-Monitor,Web-Static-Content,Web-WMI,RPC-Over-HTTP-Proxy  �Restart`  
  
2.  파일 저장 **InstallDependencies.ps1**합니다.  
  
3.  Exchange ssl 서버에 위치로 복사 합니다.  
  
4.  새 메모장 파일을 열고 다음 텍스트 파일을 복사 합니다.  
  
     `param (`  
  
     `[string]`  
  
     `[Parameter(Mandatory=$true, HelpMessage = "The path to your Certificate file, must be a *.pfx format")]`  
  
     `$CertPath = "c:\certificates\ExchangeCertificate.pfx",`  
  
     `[Security.SecureString]`  
  
     `[Parameter(Mandatory=$true, HelpMessage = "The password of your cert")]`  
  
     `$CertPassword = $null,`  
  
     `[string]`  
  
     `[Parameter(Mandatory=$true, HelpMessage = "Domain Name, eg. contoso.com")]`  
  
     `$DomainName = "contoso.com",`  
  
     `[string]`  
  
     `[Parameter(Mandatory=$true, HelpMessage = "Server IP Address, eg. 192.168.0.1")]`  
  
     `$ServerIpAddress = "192.168.0.1",`  
  
     `[string]`  
  
     `[Parameter(Mandatory=$true, HelpMessage = "Internal Ip Range, eg. 192.168.0.0-192.168.0.255")]`  
  
     `$InternalIpRange = "192.168.0.0-192.168.0.255"`  
  
     `)`  
  
     `#Import Exchange Certificate, and Enable it for POP IIS IMAP SMTP services.`  
  
     `Import-ExchangeCertificate  �FileData ([Byte[]]$(Get-content -Path $CertPath  �Encoding byte  �ReadCount 0)) -Password:$CertPassword -Force | Enable-ExchangeCertificate -Services 'POP, IIS, IMAP, SMTP' -Force`  
  
     `#New AcceptedDomain and set it to default`  
  
     `New-AcceptedDomain  �Name "official name"  �DomainName $domainname`  
  
     `Set-AcceptedDomain  �Identity "official name"  �MakeDefault $true`  
  
     `#New EmailAddress Policy`  
  
     `$address = "%m@" + $DomainName`  
  
     `New-EmailAddressPolicy -Name "Windows Server Essentials Email Address Policy" -IncludedRecipients AllRecipients -EnabledPrimarySMTPAddressTemplate $address`  
  
     `#Set owa and ecp VirtualDirectory ExternalUrl`  
  
     `$hostname = "mail." + $DomainName`  
  
     `$owa = "https://" + $hostname + "/owa"`  
  
     `$ecp = "https://" + $hostname + "/ecp"`  
  
     `$activesync = "https://" + $hostname + "/Microsoft-Server-ActiveSync"`  
  
     `$oab = "https://" + $hostname + "/OAB"`  
  
     `$ews = "https://" + $hostname + "/EWS/Exchange.asmx"`  
  
     `Get-OwaVirtualDirectory | Set-OwaVirtualDirectory  �ExternalUrl $owa  �InternalUrl $owa`  
  
     `Get-EcpVirtualDirectory | Set-EcpVirtualDirectory  �ExternalUrl $ecp  �InternalUrl $ecp`  
  
     `Get-ActiveSyncVirtualDirectory | Set-ActiveSyncVirtualDirectory -ExternalUrl $activesync  �InternalUrl $activesync`  
  
     `Get-OABVirtualDirectory | Set-OABVirtualDirectory -ExternalUrl $oab -InternalUrl $oab -RequireSSL:$true`  
  
     `Get-WebServicesVirtualDirectory | Set-WebServicesVirtualDirectory -ExternalUrl $ews -InternalUrl $ews -BasicAuthentication:$True -Force`  
  
     `#Enable outlook Anywhere`  
  
     `Enable-OutlookAnywhere  �ClientAuthenticationMethod:Basic  �ExternalHostname:$hostname  �SSLOffloading:$false`  
  
     `#new receive/send connector`  
  
     `$machinename = get-content env:computername`  
  
     `$bindingIpaddress = $ServerIpAddress + ":25"`  
  
     `$RecevieConnectorName = $machinename + "\Default " + $machinename`  
  
     `Set-ReceiveConnector $RecevieConnectorName -RemoteIPRanges $InternalIpRange`  
  
     `New-ReceiveConnector -Name "WSE Internet Receive Connector" -Usage "Internet" -Bindings $bindingIpaddress -Fqdn $hostname -Enabled $true -Server $machinename -AuthMechanism Tls,BasicAuth,BasicAuthRequireTLS,Integrated`  
  
     `New-SendConnector -Name "WSE Internet SendConnector" -Usage "Internet" -AddressSpaces 'SMTP:*;1' -IsScopedConnector $false -DNSRoutingEnabled $true -UseExternalDNSServersEnabled $true -SourceTransportServers $machinename`  
  
5.  네트워킹 환경 반영 하기 위해 스크립트의 시작 부분에 매개 변수를 설정 합니다.  
  
6.  파일 저장 **ConfigureExchange.ps1**합니다.  
  
7.  Windows PowerShell을 관리자 권한으로 실행 합니다.  
  
8.  Windows PowerShell 명령 프롬프트에 입력 **설정 ExecutionPolicy RemoteSigned**, Enter 키를 누릅니다.  
  
9. 스크립트를 실행할 **InstallDependencies.ps1**합니다.  
  
10. 서버 한 다음 실행 Windows PowerShell을 관리자 권한으로 다시 시작 합니다.  
  
11. Windows PowerShell 명령 프롬프트에서 다음 스크립트를 실행 합니다.  
  
     `E:\setup.com /mode:install /roles:mb,ht,ca /OrganizationName:"First Organization"`  
  
    > [!NOTE]
    >  올바른 경로 Exchange Server 설치 프로그램을 입력 해야 합니다.  
  
12. Exchange Server 설치가 완료 되 면 Exchange 관리 셸 관리자 권한으로 엽니다.  
  
13. Exchange 관리 셸 명령 프롬프트에 입력 **설정 ExecutionPolicy RemoteSigned**, Enter 키를 누릅니다.  
  
14. 스크립트를 실행할 **ConfigureExchange.ps1**합니다.  
  
15. 서버를 다시 시작 합니다.  
  
> [!NOTE]
>  공개적으로 신뢰할 수 있는 SSL 인증서 자체 발급 된 인증서를 대신 사용 하려는 경우 설정 가이드 인증서 요청을 만들고을 선택한 인증 기관 보내는의 지침을 따릅니다 수 있습니다. 또한 Exchange PowerShell cmdlet 인증서 요청을 만드는 데 사용할 수 있습니다. 예는 다음과 같습니다.  
>   
>  `New-ExchangeCertificate -GenerateRequest -SubjectName "C=US, S=Washington, L=Redmond, O=contoso, OU=contoso, CN=mail.contoso.com" -DomainName mail.contoso.com -PrivateKeyExportable $true | Set-Content -path "c:\Docs\MyCertRequest.req"`  
>   
>  네트워킹 환경 반영 하기 위해 스크립트 매개 변수를 사용자 지정 합니다.  
  
## <a name="post-installation-tasks"></a>이후 Post-installation 작업  
 이 섹션 설명 서버 구성 작업 Exchange Server Windows Server Essentials 네트워크에서 실행 되는 온-프레미스 서버 설정에 대 한 정보를 포함 하 여 설치 후 단계를 완료 해야 할 수 있습니다.  
  
### <a name="add-the-public-email-domain-and-configure-the-email-address-policies"></a>공용 메일 도메인 추가 하 고 메일 주소 정책 구성  
  
> [!NOTE]
>  새로 설치 하는 경우이 필요한 작업을 합니다. Windows Small Business Server에서 마이그레이션하는 하는 경우이 단계를 건너뛸 합니다.  
  
 기본 허용 도메인 메일 도메인 사용자 지정 하 고 메일 주소 정책을 구성 해야 합니다.  
  
##### <a name="to-add-your-email-domain-as-the-default-accepted-domain"></a>허용 도메인 기본적으로 메일 도메인을 추가 하려면  
  
1.  Exchange Server 문서의 지침에 따라 [허용 도메인 만들](https://go.microsoft.com/fwlink/p/?LinkId=249174) 허용된 도메인 추가 합니다.  
  
2.  두 번째 서버 관리자 권한으로 로그온 Exchange 관리 콘솔을 연 다음으로 이동는 **허브 전송** 탭에서 **조직 구성**합니다.  
  
3.  Exchange 관리 콘솔 클라우드 창에서 새로운 허용된 도메인 마우스 오른쪽 단추로 클릭 한 다음 클릭 **기본값으로 설정**합니다.  
  
4.  Exchange Server 문서의 지침을 따릅니다 [전자 메일 주소 정책 만드는](https://go.microsoft.com/fwlink/p/?LinkId=249179) 새 메일 주소 정책 만들 수 있습니다. 메일 주소를 제외 하 고 기본값의 모든 파일을 받을 수 있습니다. 공용 메일 도메인 이메일 주소를 지정 합니다.  
  
### <a name="create-smtp-send-and-receive-connectors"></a>SMTP 보내기 만들고 수신 커넥터  
  
> [!NOTE]
>  이 필요한 작업입니다.  
  
 SMTP 보내기 커넥터와 SMTP 수신 커넥터 돌아오는/아웃 바운드 전송의 메일 메시지를 구성 해야 합니다.  
  
 SMTP 보내기 커넥터를 만들려면 Exchange Server 문서의 지침에 따라 [SMTP 보내기 커넥터 만들기](https://technet.microsoft.com/library/aa997285.aspx)합니다.  
  
 Exchange Server 문서의 지침을 따릅니다 SMTP 수신 커넥터를 만들려면 [SMTP 수신 커넥터 만들](https://technet.microsoft.com/library/bb125159.aspx)합니다.  
  
 필요에 따라이 문서를 만드는 보내기 앞부분 스크립트를 참조 하 고 Exchange PowerShell cmdlet 사용 하 여 커넥터 받을 수 있습니다.  
  
### <a name="configure-the-network-router"></a>네트워크 라우터 구성  
  
> [!NOTE]
>  새로 설치 하는 경우이 필요한 작업을 합니다. Windows Small Business Server에서 마이그레이션하 하는 경우 참조 [Windows Server essentials 서버 데이터 마이그레이션](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md) 네트워크 구성 하는 방법에 대 한 지침은 합니다.  
  
 적어도 경우 라우터에서 다음 포트 설정을 구성 해야 합니다.  
  
|라우터 포트|대상 IP|대상 포트|노트|  
|-----------------|--------------------|----------------------|----------|  
|(SMTP) 25|Exchange Server 실행 하는 온-프레미스 서버 내부 IP 합니다.|25||  
|80 (HTTP)|Windows Server Essentials 실행 하는 서버 내부 IP|80||  
|443 (HTTPS)|Windows Server Essentials 실행 하는 서버 내부 IP|443||  
  
 POP3 또는 네트워크에 대 한 프로토콜 어디서 나 메시지 IMAP을 지 원하는 경우 해당 프로토콜에 대 한 포트 forwardings 구성 해야 합니다. 관련된 정보 섹션을 참조 **클라이언트 액세스 서버** 항목에서 [Exchange 네트워크 포트 참조](https://go.microsoft.com/fwlink/p/?LinkId=250773) Exchange Server TechNet 라이브러리에 있습니다.  
  
> [!NOTE]
>  -   Windows Server Essentials 실행 하는 서버에 대 한 고정 IP 주소를 구성 하 고 있는 두 번째 서버에 대 한 Exchange Server 실행 하는 것이 좋습니다. Windows Server 2008 R2 또는 Windows Server 2003을 실행 하는 컴퓨터에서 고정 IP 주소를 구성 하는 방법에 대 한 지침은 참조 [고정 IP 주소를 구성](https://technet.microsoft.com/library/cc754203\(v=ws.10\).aspx) Windows Server TechNet 라이브러리에 있는  
>   
>      **참고:** DNS 서버 설정을 Windows Server Essentials 실행 하는 서버의 IP 주소를 항상 가리키고 해야 합니다.  
> -   라우터에서 Windows Server Essentials 실행 하는 서버 및 Exchange Server 실행 하는 서버의 IP 주소는 예약 하거나 DHCP IP 주소 범위 밖으로 있는지 확인 합니다.  
> -   라우터 구성이이 섹션의 인터넷 서비스 공급자 (ISP)에서 지정 공용 하나만 IP 주소 있어야 합니다. 여러 공개 IP 주소를 사용 하는 경우 Windows Server Essentials 실행 하는 서버 및 Exchange Server 실행 하는 서버 다른 IP 주소를 지정 수 있으며 다음 포트 forwardings 공개 IP 주소를 기준 만들 수 있습니다.  
  
### <a name="enable-on-premises-exchange-server-integration-on-windows-server-essentials"></a>Windows Server Essentials의 온-프레미스 Exchange Server 통합 사용  
  
> [!NOTE]
>  Small Business Server Windows 설치에서 마이그레이션하는 경우이 단계는 현재 하 고 원본 서버의 Exchange Server의 이전 설치를 제거한 후 실행 하는 것이 좋습니다.  
  
 설치 하 고 Exchange Server 실행 하는 서버 구성 후 Windows Server Essentials 실행 하는 서버에 온-프레미스 Exchange Server 통합 사용 하도록 설정 해야 합니다.  
  
##### <a name="to-enable-on-premises-exchange-server-integration-from-the-dashboard"></a>온-프레미스 Exchange Server 통합 대시보드에서 사용 하도록 설정 하려면  
  
1.  Windows Server Essentials 관리자 권한으로 실행 하는 서버에에 로그인 하 고 대시보드를 엽니다.  
  
2.  에 **Home** 페이지, 클릭 **내 메일 서비스에 연결**을 차례로 클릭 하 고 **Exchange Server 통합**합니다.  
  
3.  정보 창에서 클릭 **Exchange Server 통합 설정**합니다.  
  
4.  마법사의 지침을 따릅니다.  
  
### <a name="configure-a-reverse-proxy"></a>역방향 프록시 구성을  
  
> [!NOTE]
>  인터넷 서비스 공급자 로부터 하나만 인터넷에 연결 되어 있는 경우이 필요한 작업을 합니다.  
  
 Windows Server Essentials 및 Exchange Server 네트워크 사용자에 대 한 원격 액세스 시나리오가 지원합니다. 예를 들어, Windows Server Essentials 실행 하는 서버에서 원하는 위치에 대 한 액세스를 켜면 원격 액세스할 수 원격 Web Access 사이트 하거나 가상 사설망 VPN ()를 사용 하 여 원격으로 Windows Server Essentials 네트워크에 연결 합니다. 원격으로 메일 메시지에 액세스 하려면 외부에서 Outlook, Outlook OWA Web Access (), 또는 ActiveSync 사용 해야 합니다.  
  
 Exchange Server 실행 하는 서버 및 Windows Server Essentials 인 둘 다 동일한 라우터에 연결 하 고 하나만 인바인드 인터넷에 연결 되어 인터넷 서비스 공급자 로부터 라우터에 대상 호스트 이름을 기반은 인터넷에서 다른 유형의 원격 액세스 요청 경로 역방향 프록시 솔루션을 사용 해야 합니다. Microsoft는 사용 하는 것이 좋습니다 IIS 응용 프로그램을 요청 경로 (ARR) 확장 역방향 프록시 솔루션으로 지원 합니다. IIS 응용 프로그램 경로 요청에 대 한 자세한 내용은 참조는 [웹 응용 프로그램 경로 요청](https://go.microsoft.com/fwlink/p/?LinkId=249181)합니다.  
  
##### <a name="to-install-and-configure-application-request-routing"></a>설치 및 구성 응용 프로그램 경로 요청 하려면  
  
1.  Windows Server Essentials 관리자 권한으로 로그온 합니다.  
  
2.  인터넷 브라우저를 열고 탐색 하 고 [웹 응용 프로그램 경로 요청](https://go.microsoft.com/fwlink/p/?LinkId=249181)합니다.  
  
3.  ARR 웹 사이트에서 클릭 **설치**, arr. 설치 지침에 따라 다음  
  
    > [!NOTE]
    >  URL을 다시 작성 모듈 ARR 설치 하는 동안 선택 해야 합니다.  
    >   
    >  KB 2589179 ARR 2.5에 대해 성공적으로 설치 되지 않은 ARR 설치 끝에 오류가 나타날 수 있습니다. 이 오류는 무시 해도 됩니다.  
  
4.  ARR 설치가 완료 될 때 다시 시작 하 고 **원격 데스크톱 게이트웨이의** 실행 하지 않는 경우 서비스입니다.  
  
    > [!NOTE]
    >  ARR를 설치한 후는 **원격 데스크톱 게이트웨이의** 서비스 중지 될 수 있습니다. 서비스를 다시 시작 수동으로 열고는 **서비스** 다음 다시 시작 하 고 관리 도구는 **원격 데스크톱 게이트웨이의** 서비스 합니다.  
  
5.  [ARR 2.5 KB2732764 다운로드](https://go.microsoft.com/fwlink/?LinkID=258302), 다음 Windows Server Essentials 실행 하는 서버에 업데이트를 설치 하 고 있습니다.  
  
6.  Exchange Server에 대 한 Windows Server Essentials 실행 하는 서버에 SSL 인증서 파일을 복사 합니다. 인증서 파일 개인 키 있어야 하 고 PFX 파일 형식에 있어야 합니다.  
  
    > [!NOTE]
    >  자체 발급 된 인증서를 사용 하는 경우 Exchange Server 문서에서 지침에 따라 [Exchange 인증서 내보내기](https://technet.microsoft.com/library/dd351274.aspx) 인증서를 내보내려면 합니다.  
  
7.  실행 중인 Windows Server Essentials의 버전에 따라 다음 중 하나를 수행 합니다.  
  
    -   Windows Server Essentials:에서 관리자 권한으로 명령 창을 열고 %ProgramFiles%\Windows 실행 디렉터리  
  
    -   Windows Server Essentials:에서 관리자 권한으로 명령 창 열기 한 다음 %Windir%\System32\Essentials 디렉터리를 엽니다.  
  
8.  설치 시나리오에서 based ARR 구성 하려면 다음이 단계 중 하나를 수행 합니다.  
  
    -   새로 설치를 수행 하는 경우 다음 명령을 실행 합니다.  
  
         * * ARRConfig 구성 인증서 * * *인증서 파일에 대 한 경로* * * 호스트 이름을 * * *호스트 Exchange server 이름* ****  
  
        > [!NOTE]
        >  예를 들어, * * ARRConfig 구성 인증서 ***c:\temp\certificate.pfx*** 호스트 이름 ***mail.contoso.com***  
        >   
        >  교체 *mail.contoso.com* 인증서에 의해 보호 되는 도메인의 이름으로 합니다.  
  
    -   Windows Small Business Server, 다음 명령을 실행에서 마이그레이션하는 다음과 같습니다.  
  
         * * ARRConfig 구성 인증서 * * *인증서 파일에 대 한 경로* * * 호스트 이름을 * * *호스트 Exchange server 이름* * * 대상 * * *Exchange server 서버 이름* ****  
  
         예를 들어, * * ARRConfig 구성 인증서 ***c:\temp\certificate.pfx*** 호스트 이름을 ***mail.contoso.com*** 대상 * * * ExchangeSvr * * *  
  
         교체 *mail.contoso.com* 도메인 이름입니다. 교체 *ExchangeSvr* Exchange Server 실행 하는 서버의 이름으로 합니다.  
  
9. 메시지가 표시 되 면 인증서에 대 한 암호를 입력 합니다.  
  
> [!NOTE]
>  -   사용자가 제공 하는 호스트 이름은 Exchange Server에 대 한 구매 ssl에서 포함 합니다.  
> -   여러 호스트 이름을 사용 하는 쉼표 (,) 사용 하 여 구분 합니다.  
  
 Exchange Server (https://mail 실행 하는 서버에 대 한 OWA 웹 사이트에 액세스 하려고 구성 작동 있는지 확인 하려면. *yourdomainname*.com/owa)는 도메인의 회원 하지 않은 컴퓨터에서 합니다. 연결 문제를 해결 하려면 사용할 수도 온라인 [Microsoft 원격 연결 분석기](https://go.microsoft.com/fwlink/p/?LinkId=249455) 도구입니다.  
  
### <a name="configure-split-dns-for-exchange-server"></a>구성 Exchange server DNS 분할  
  
> [!NOTE]
>  권장 되는 작업입니다.  
  
 나누기 DNS DNS 요청을 시작에 따라 동일한 호스트 이름에 대 한 다른 IP 주소 DNS 구성할 수 있습니다. 클라이언트 컴퓨터 인트라넷 켜져 있으면 DNS 요청 인트라넷 IP 주소를 확인 합니다. 클라이언트 컴퓨터가 인터넷에 연결 되어 있으면 DNS 요청 인터넷 IP 주소를 확인 합니다. 이 사용자에 게 투명 하 게 됩니다.  
  
 누적 시간을 구성 하는 것이 좋습니다 위치와 관계 없이 DNS 항상 호스트 이름이 같은 사용 하 여 Exchange Server 액세스할 수 있도록 하는 방식으로 서비스입니다.  
  
##### <a name="to-configure-split-dns-for-exchange-server"></a>누적 시간 DNS Exchange Server에 대 한 구성 하려면  
  
1.  Windows Server Essentials 관리자로 로그온 한 다음 DNS 관리자를 엽니다.  
  
2.  DNS 관리자 콘솔 트리에서 서버를 마우스 오른쪽 단추로 클릭 한 다음 **새 영역**합니다. **새로운 영역 마법사** 나타납니다.  
  
3.  에 **영역 종류** 페이지 마법사의 기본 옵션와 클릭 한 다음 **다음**합니다.  
  
4.  에 **Active Directory 영역 복제 범위** 페이지를 기본 옵션을 클릭 한 다음 **다음**합니다.  
  
5.  에 **앞으로 또는 역방향 조회 영역이** 페이지를 허용 하거나 선택 **앞으로 조회 영역이**을 차례로 클릭 하 고 **다음**합니다.  
  
6.  에 **영역 이름** 페이지에서 Exchange Server (예를 들어; 실행 하는 서버 FQDN 입력 *mail.contoso.com*)를 클릭 한 다음 **다음**합니다.  
  
7.  에 **동적 업데이트** 페이지 기본 옵션을 클릭 **다음**을 차례로 클릭 하 고 **완료**합니다.  
  
8.  새 앞으로 조회 영역이 마우스 클릭 한 다음 DNS 관리자 콘솔 트리에서 **A 등의 AAAA 새 호스트**합니다.  
  
9. 에 **새 호스트** 페이지에서 두고는 **이름** 빈 필드 Exchange Server 실행 하는 서버 인트라넷 IP 주소를 입력 하 고 클릭 한 다음 **호스트 추가**합니다.  
  
    > [!NOTE]
    >  나가면는 **이름** 필드 빈, 서버 부모 도메인 이름 기본적으로 사용 하 여 합니다.  
  
10. 에 **새 호스트** 페이지, 클릭 **완료**합니다.  
  
> [!NOTE]
>  ActiveSync 사용 하지만 일부 사서함 계정에 대 한 메일을 동기화 할 수 없는 경우 계정을 하나 이상의 보호 그룹 도메인 관리자 등의 회원 한지 확인 합니다. 이 문제를 해결 하는 데 도움이 되는 관련된 정보를 참조 하세요. [Exchange ActiveSync 반환 HTTP 500 오류](https://technet.microsoft.com/library/dd439375\(EXCHG.80\).aspx)합니다.  
  
## <a name="related-topics"></a>관련된 항목  
 통합 온-프레미스 Exchange Server에 대 한 자세한 내용은 다음 섹션을 참조 하십시오.  
  
### <a name="what-happens-if-i-disable-exchange-integration"></a>Exchange 통합을 사용 하지 않도록 설정 하는 경우 어떻게 되나요?  
 온-프레미스 Exchange Server와의 통합을 해제 하면 Windows Server Essentials 대시보드 보고 만들거나 Exchange Server 사서함 관리을 사용할 수 없게 됩니다.  
  
### <a name="what-do-i-need-to-know-about-email-accounts"></a>메일 계정에 대해 알아야 할 무엇이 필요 하나요?  
 여 호스팅된 메일 솔루션 서버 구성 되어 있습니다. Microsoft Office 365 같은 여 호스팅된 메일 공급자에서 솔루션 개별 이메일 계정을 네트워크 사용자에 게 제공할 수 있습니다. 사용자 계정 만들기를 Windows Server Essentials의 사용자 계정 마법사의 추가 실행 하면 마법사에 사용할 수 있는 호스팅된 메일 솔루션 사용자 계정을 추가 하려고 합니다. 이와 동시 마법사 메일 이름 (별칭)를 사용자 지정 하 고 사서함 (할당량)의 최대 크기를 설정 합니다. 사서함의 최대 크기 사용 하는 메일 공급자에 따라 다릅니다. 사용자 계정에 추가한 후에 사용자에 대 한 속성 페이지에서 사서함 별칭 및 할당 정보를 관리 하려면 계속할 수 있습니다. 사용자 계정 및 호스팅된 메일 공급자의 전체 관리에 대 한 여 호스팅된 공급자의 관리 콘솔을 사용 합니다. 공급자에 따라 대시보드 서버에서 탭 또는 웹 기반 포털에서 자녀가 management console에 액세스할 수 있습니다.  
  
 사용자 계정에 대 한 추천된 이름으로 별칭 추가 사용자 계정 마법사를 실행 하는 경우 사용자가 제공 하 여 호스팅된 메일 공급자에 게 전송 됩니다. 예를 들어 사용자 별칭 *FrankM*, s 사용자는 메일 주소로 수도 * FrankM@Contoso.com *합니다.  
  
 또한, 사용자 계정 마법사 추가에서 사용자에 대해 설정한 암호 여 호스팅된 메일 해결 방법에는 사용자의 초기 암호가 됩니다.  
  
 마지막으로, 서버에서 사용자 계정 마법사 삭제를 사용 하 여 사용자를 삭제 하면 마법사 요청 사용자도 시스템에서 삭제 하려면 호스팅된 메일 공급자에 게 에서도 보냅니다. S 사용자 계정 및 계정과 연결 된 메일 공급자 삭제할 수 있습니다.  
  
 필요한 메일 클라이언트 소프트웨어를 설정 하는 방법을 또는 메일 계정에 액세스 하는 방법에 대 한 사용자 정보를 여 호스팅된 메일 공급자가 제공한 도움말 문서를 참조 하세요.  
  
### <a name="what-is-a-mailbox-quota"></a>사서함 할당은 무엇 인가요?  
 네트워크 사용자의 교환 사서함 데이터에 대 한 할당는 저장소 공간의 크기를 사서함 할당량 이라고 합니다.  
  
 실행 하는 경우는 **Exchange Server 통합 설정** 마법사 대시보드에서 작업에 사서함 만들기를 적용 하 고 할당량 크기 지정할 수 여부를 선택할 수 있는 사용자 계정 추가 마법사에서 페이지를 추가 합니다. 기본적으로는 **사서함 할당량** (를) 옵션을 선택 하 고 사용자 사서함 2GB의 저장소 공간 지정 됩니다. Exchange 관리자가 들어왔습니다 요구에 맞게 사서함 할당량 설정이 사용자 지정할 수 있습니다.  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [Windows Server Essentials의 시스템 요구 사항](../get-started/system-requirements.md)  
  
-   [메일 서비스 통합 관리](Manage-Email-Service-Integration-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)
