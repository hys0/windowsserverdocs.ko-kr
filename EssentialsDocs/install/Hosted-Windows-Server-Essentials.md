---
title: 호스트된 Windows Server Essentials
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fda5628c-ad23-49de-8d94-430a4f253802
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1b78432ca92028bc96b2cbfc9fa40196f61e8bf8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833704"
---
# <a name="hosted-windows-server-essentials"></a>호스트된 Windows Server Essentials

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

이 문서에는 해당 환경에서 Windows Server Essentials를 배포 하 고 고객에 게 Windows Server Essentials를 서비스로 제공 하려는 호스팅 서비스 공급자에 관련 된 정보가 포함 됩니다.  
  
## <a name="what-is-windows-server-essentials"></a>Windows Server Essentials 란?  
 Windows Server Essentials는 대부분의 중소기업에 적합 한 서버 환경을 제공 하는 최고의 64 비트 제품 기술을 통합 하는 크로스 프레미스 중소기업용 솔루션으로 합니다. 다음 기술은 Windows Server Essentials에 포함 됩니다.  
  
 **서버 운영 체제:** Windows Server 2012 제품 기술은 Windows Server Essentials의 핵심을 제공합니다. 자세한 내용은 [Windows Server 2012 웹 사이트](https://www.microsoft.com/en-us/server-cloud/products/windows-server-2012-r2/default.aspx#fbid=ZH0GD_CRAWh)를 참조하세요.  
  
 **데이터 보호:** Windows Server Essentials는 크게 향상 된 데이터 보호 기능을 제공 하는 Windows Server 2012에서 사용할 수 있는 몇 가지 새로운 기능을 활용 합니다. [새 저장소 공간 기능](https://technet.microsoft.com/library/hh831739.aspx) 을 사용하면 개별 하드 드라이브의 실제 저장소 용량을 집계하고, 하드 드라이브를 동적으로 추가하며, 지정된 복원력 수준으로 데이터 볼륨을 만듭니다. Windows Server Essentials에는 전체 시스템 백업을 수행할 수 있습니다 하 고 네트워크에 연결 된 클라이언트 컴퓨터 뿐만 아니라 자체 베어 메탈 서버 복원?을 2TB가 넘는 볼륨에 대 한 지원. Windows Server 2012에서 새로 도입된 [Microsoft Azure Online Backup](https://technet.microsoft.com/library/hh831419.aspx) 을 사용하면 Microsoft가 관리하는 클라우드 기반 저장소 서비스에서 파일 및 폴더를 보호할 수 있습니다. Windows Server Essentials는 또한 중앙 집중식으로 관리 하 고 관리자 지원을 요청 하지 않고 실수로 삭제 하거나 덮어쓴 파일에서 복구 하는 사용자를 지원 되는 Windows 8.1 클라이언트의 파일 히스토리 기능을 구성 합니다.  
  
 **원격 액세스:** 원격 웹 액세스는 인터넷이 연결되는 거의 모든 곳에서 거의 모든 장치를 사용하여 응용 프로그램 및 데이터에 액세스할 수 있는 간소한 터치 지원 브라우저 경험을 제공합니다. Windows Server Essentials에서는 업데이트 된 Windows Phone 앱 및 새 앱을 Windows 8.1 클라이언트에 대 한 컴퓨터, 연결 검색 하 고 서버에서 파일 및 폴더에 액세스할 사용자를 직관적으로 허용 합니다. 또한 파일은 오프라인 액세스를 위해 자동으로 캐시되었다가 서버 연결을 사용할 수 있게 되면 동기화됩니다. Windows Server Essentials를 가상 사설망 (VPN)을 몇 번의 간편한, 마법사 기반 프로세스로 설정 설정 및 사용자에 대 한 VPN 액세스 관리를 간소화 합니다. 클라이언트 컴퓨터는 VPN 연결을 활용하여 사무실에 통근하지 않고도 Windows SBS 환경에 원격으로 참가할 수 있습니다.  
  
 **작업 유연성:** Windows Server Essentials는 고객이 응용 프로그램 및 서비스는 온-프레미스에서 실행 하 고 클라우드에서 실행 하는 선택할 수 있도록 설계 되었습니다. 이전 버전인 Windows Small Business Server Standard에는 Exchange Server가 구성 요소 제품으로 포함되어 클라우드 기반 메시징 및 협업 서비스를 활용하려는 고객 입장에서는 비용과 복잡성이 높았습니다. Windows Server Essentials를 사용 하 여 고객 것인지를 Exchange Server의 온-프레미스 복사본을 실행 하거나 호스트 된 Exchange 서비스에 가입 하거나 Microsoft Office 365를 구독할 선택할 수 있도록 동일한 유형의 통합된 관리 환경 활용을 걸릴 수 있습니다.  
  
 **상태 모니터링:** Windows Server Essentials는 자체 상태 및 Windows 8.1, Windows 7 및 Mac OS X 버전 10.5 이상을 실행 하는 클라이언트 컴퓨터의 상태를 모니터링 합니다. 상태 모니터링 이후 컴퓨터 백업, 서버 저장소, 디스크 공간 부족 등의 관련 문제에 대해 알립니다.  
  
 **확장성:** 새 웹 서비스 Api 집합을 추가 및 다른 소프트웨어 공급 업체가 핵심 제품에 기능 및 기능을 추가할 수 있는 Windows SBS 2011 Essentials의 확장성 모델을 기반으로 Windows Server Essentials. 또한 Windows SBS 2011 Essentials용으로 만든 기존 [SDK(소프트웨어 개발 키트)](https://msdn.microsoft.com/library/gg513958.aspx) 및 [추가 기능](https://pinpoint.microsoft.com/applications/search?fpt=300105&q=small+business+server+essentials) 과 호환성이 유지됩니다.  
  
## <a name="how-can-i-customize-an-image"></a>이미지를 사용자 지정하는 방법  
 참조 된 [Windows Server Essentials](https://go.microsoft.com/fwlink/p/?LinkID=249124), 추가 Windows Server Essentials 사용자 지정 단계를 사용 하 여 표준 Windows Server sysprep 프로세스입니다. 사용자 지정을 완료하려면 [단순 사용자 지정 이미지 만들기](https://technet.microsoft.com/library/jj200117) 및 [이미지 사용자 지정](https://technet.microsoft.com/library/jj200161)의 지침을 따른 다음 [배포용 이미지 준비](https://technet.microsoft.com/library/jj200142) 의 지침을 따라 최종 이미지를 캡처합니다.  
  
 다음과 같은 점에 주의해야 합니다.  
  
1.  임의의 드라이브 루트에 SkipIC.txt 파일을 추가하여 IC(초기 구성)를 건너뛰어야 합니다. 서버를 설치한 후 IC 전에 Shift+F10을 눌러 cmd 창을 시작하고 C:/ 드라이브 아래에 SkipIC.txt 파일을 만듭니다. 사용자 지정 후에는 SkipIC.txt 파일을 꼭 삭제해야 합니다.  
  
2.  90GB 미만의 디스크에 Windows Server Essentials를 배포 해야 할 경우 sysprep 전에 레지스트리 키를 추가 해야 합니다.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v HWRequirementChecks /t REG_DWORD /d 0 /f  
    ```  
  
 sysprep 후에는 sysprep을 완료한 디스크 이미지를 사용하거나 새 배포를 위해 Install.wim에 새로 봉인할 수 있습니다.  
  
 Virtual Machine Manager를 사용하는 경우 실행 중인 인스턴스를 사용하여 템플릿을 만들 수 있습니다. 템플릿을 만들면 인스턴스의 sysprep이 수행되고 서버가 종료됩니다. 라이브러리에 저장한 후 개별적으로 인스턴스를 불러 올 수 있습니다.  
  
##  <a name="BKMK_automatedeployment"></a> 배포를 자동화 하는 방법  
 사용자 지정된 이미지를 얻은 후에는 고유 이미지를 사용하여 배포할 수 있습니다. 반 무인 설치를 수행하려면 WinPE 설치를 위한 unattend.xml을 제공/배포해야 합니다. 완전 무인된 설치를 위해 Windows Server Essentials 초기 구성을 위한 cfg.ini 파일도 제공 해야 합니다.  
  
1.  무인 WinPE 설치만 수행합니다. 그러면 WinPE 설치만 자동화되며 최종 사용자가 직접 RDP 이후 서버 세션에 회사, 도메인 및 관리자 정보를 제공할 수 있도록 초기 구성 이전에 설치가 중지됩니다. 가상 하드 디스크 파일에 대한 중요 정보를 제공하려면  
  
    1.  unattend.xml 파일을 제공합니다. 에 따라 합니다 [Windows 8.1 ADK](https://go.microsoft.com/fwlink/?LinkId=248694) 파일을 생성 하 여 서버 이름, 제품 키, 관리자 암호 등 모든 필요한 정보를 제공 합니다. Unattend.xml 파일의 Microsoft Windows 설정 섹션에서는 다음과 같은 정보를 제공 합니다.  
  
        ```  
        <InstallFrom>  
                 <MetaData>  
                     <Key>IMAGE/WINDOWS/EDITIONID</Key>  
                     <Value>ServerSolution</Value>  
                 </MetaData>  
                 <MetaData>  
                     <Key>IMAGE/WINDOWS/INSTALLATIONTYPE</Key>  
                     <Value>Server</Value>  
                 </MetaData>  
           </InstallFrom>  
        ```  
  
    2.  고객 초기 구성을 완료 하려면 관리자 권한 및 서버에 RDP 하려면 unattend.xml 파일에 지정한 암호를 사용할 수 있도록 공용 IP에 RDP 포트 3389를 열어야 합니다.  
  
    > [!NOTE]
    >  기본 암호를 변경하지 않는 경우 서버 설치가 중지되고 화면에 암호를 입력하라는 메시지가 표시됩니다.**참고** 최종 사용자는 기본 관리자 계정을 사용하여 서버에 로그온하고 초기 구성을 수행해야 합니다.  
  
 Virtual Machine Manager를 사용 중인 경우 템플릿에서 새 인스턴스를 만들 때 콘솔에서 관리자 암호를 지정할 수 있습니다.  
  
1.  무인 초기 구성을 포함하여 완전 무인 설치를 수행합니다. 가상 하드 디스크 파일에 대한 중요 정보를 제공하려면  
  
    1.  배포가 WinPE 설치부터 시작되는 경우 위에서 한 것처럼 unattend.xml 파일을 제공합니다.  
  
    2.  Windows Server Essentials ADK 섹션을 참조 하세요 [Cfg.ini 파일 만들기](https://technet.microsoft.com/library/jj200150), 여 cfg.ini를 생성 합니다.  
  
    3.  [InitialConfiguration]에 정보를 제공합니다.  
  
        ```  
        WebDomainName=yourdomainname  
        TrustedCertFileName=c:\cert\a.pfx  
        TrustedCertPassword=Enteryourpassword  
        EnableVPN=true  
        EnableRWA=true  
        ; Provide all information so that after setup is complete, your customer can use your domain name to visit the server directly with the admin/user information you provide in the [InitialConfiguration] section.  
  
        VpnIPv4StartAddress=<IPV4Address>  
        VpnIPv4EndAddress=<IPV4Address>  
        VpnBaseIPv6Address=<IPV6Address>  
        VpnIPv6PrefixLength=<number>  
        ; Provide this information. IPv4StartAddress and IPv4Endaddress are required so that your VPN client can acquire valid IP through this range.  
  
        IPv4DNSForwarder=<IPV4Address,IPV4Address,Â¦>  
        IPv6DNSForwarder=<IPV6Address,IPV6Address,Â¦>  
        ; Provide this information as needed according to your network environment settings.  
        ```  
  
    4.  [PostOSInstall]에 정보를 제공합니다.  
  
        ```  
        IsHosted=true   
        ; Must have, this will prevent Initial Configure webpage available for other computers under same subnet.  
  
        StaticIPv4Address=<IPV4Address>  
        StaticIPv4Gateway=<IPV4Address>  
        StaticIPv6Address=<IPV6Address>  
        StaticIPv6SubnetPrefixLength=<number>  
        StaticIPv6Gateway=<IPV6Address>  
        ; All these are optional if you have DHCP Server Service on the subnet, otherwise provide static IP here.  
        ```  
  
    5.  WebDomainName 매개 변수를 제공 하는 경우 서버 s 공용 IP를 가리키도록 DNS 레코드를 업데이트도 있는지 확인 합니다.  
  
    6.  위의 WebDomainName 정보를 제공하지 않은 경우에는 고객이 RDP를 사용하여 서버에 연결하고 VPN 구성을 마칠 수 있도록 포트 3389를 열어야 합니다.  
  
> [!NOTE]
>  VM 호스트 서버 및 Windows Server Essentials VM의 표준 시간대 설정이 동일한 지 확인 합니다. 그렇지 않으면, 인증서 관련 작업에서 초기 구성이 실패하거나, 설치 후 몇 시간 동안 인증서가 작동하지 않거나, 장치 정보가 올바르게 업데이트되지 않는 등 몇 가지 오류가 발생할 수 있습니다.  
  
 배포 후 HKLM\software\microsoft\windows server\setup 아래에서 다음 레지스트리 키를 점검하여 초기 구성이 성공적인지 확인합니다. SetupStage == ICDone && ICStatus == 1인 경우 초기 구성이 성공적으로 완료되었음을 의미합니다.  
  
## <a name="what-is-the-supported-network-topology"></a>지원되는 네트워크 토폴로지  
 로밍 클라이언트에서 Windows Server Essentials를 사용 하려면 VPN 설정 되어야 합니다. VPN SSTP 연결에 포트 443을 사용하는 것이 좋습니다. 원격 웹 액세스 또는 웹 서비스 앱에 미디어 서버 기능이 필요한 경우에는 포트 80도 사용해야 합니다.  
  
 VPN 사용 설정은 무인 배포 도중에 Windows PowerShell 스크립트를 통해 수행하거나 초기 구성 후 마법사를 통해 구성할 수 있습니다.  
  

-   무인 배포 도중에 VPN을 사용 설정하려면 이 문서의 [How do I automate the deployment?](Hosted-Windows-Server-Essentials.md#BKMK_automatedeployment) 을 참조하세요.  

-   무인 배포 도중에 VPN을 사용 설정하려면 이 문서의 [How do I automate the deployment?](../install/Hosted-Windows-Server-Essentials.md#BKMK_automatedeployment) 을 참조하세요.  

  
-   Windows PowerShell을 통해 VPN을 사용 설정하려면 관리자 권한으로 다음 cmdlet을 실행하고 필요한 정보를 모두 제공합니다.  
  
    ```  
    ##  
    ## To configure external domain and SSL certificate (if not yet done in unattended Initial Configuration).  
    ##  
  
    $myExternalDomainName = 'remote.contoso.com';   ## corresponds to A or AAAA DNS record(s) that can be resolved on Internet and routed to the server  
    $mySslCertificateFile = 'C:\ssl.pfx';   ## full path to SSL certificate file  
    $mySslCertificatePassword = ConvertTo-SecureString '******';   ## password for private key of the SSL certificate  
    $skipCertificateVerification = $true;   ## whether or not, skip verification for the SSL certificate  
  
    Add-Type -AssemblyName 'Wssg.Web.DomainManagerObjectModel';  
    [Microsoft.WindowsServerSolutions.RemoteAccess.Domains.DomainConfigurationHelper]::SetDomainNameAndCertificate($myExternalDomainName,$mySslCertificateFile,$mySslCertificatePassword,$skipCertificateVerification);  
    ##  
    ## To install VPN with static IPv4 pool (and allow all existing users to establish VPN).  
    ##  
  
    Install-WssVpnServer -IPv4AddressRange ('192.168.0.160','192.168.0.240') -ApplyToExistingUsers;  
    ```  
  
 고객에게 서버를 제공하기 전에 VPN 연결을 제공할 수 없는 경우에는 최종 사용자가 RDP를 사용하여 서버에 연결하고 직접 구성할 수 있도록 인터넷 서버 포트 3389를 연결 가능하게 만들어야 합니다.  
  
 다음은 일반적인 서버 쪽 네트워킹 토폴로지 두 가지와 VPN/RWA(원격 웹 액세스) 구성 방법입니다.  
  
-   토폴로지 1(기본)  
  
    -   별도의 가상 네트워크에서 NAT 장치 아래에 서버가 위치합니다.  
  
    -   DHCP 서비스를 가상 네트워크에서 사용하거나 서버에 정적 IP 주소가 할당됩니다.  
  
    -   서버 포트 443을 공용 IP 포트 443에서 연결할 수 있습니다.  
  
    -   포트 443에 대해 VPN 통과가 허용됩니다.  
  
    -   VPN IPv4 주소 풀이 동일한 서버 주소 서브넷 범위에 있어야 합니다.  
  
    -   이차 서버에는 동일한 서브넷에 속하지만 VPN 주소 풀 범위 외의 정적 IP를 할당해야 합니다.  
  
-   토폴로지 2:  
  
    -   서버에 개인 IP 주소가 있습니다.  
  
    -   서버의 포트 443이 공용 IP 주소의 포트 443에서에서 연결할 수 있습니다.  
  
    -   포트 443에 대해 VPN 통과가 허용됩니다.  
  
    -   VPN IPv4 주소 풀이 다른 서버 주소 범위에 있습니다.  
  
 토폴로지 2에서는 이차 서버 시나리오가 지원되지 않습니다.  
  
## <a name="how-do-i-perform-common-tasks-via-windows-powershell"></a>Windows PowerShell을 통해 일반적인 작업을 수행하는 방법  
 **원격 웹 액세스 사용**  
  
```  
Enable-WssRemoteWebAccess [-SkipRouter] [-DenyAccessByDefault] [-ApplyToExistingUsers]  
```  
  
 예:  
  
```  
$Enable-WssRemoteWebAccess  œDenyAccessByDefault  œApplyToExistingUsers  
```  
  
 이 명령은 라우터를 자동으로 구성하여 원격 웹 액세스를 사용하도록 설정하며 모든 기존 사용자의 기본 액세스 권한을 변경합니다.  
  
 **사용자 추가**  
  
```  
Add-WssUser [-Name] <string> [-Password] <securestring> [-AccessLevel <string> {User | Administrator}] [-FirstName <string>] [-LastName <string>] [-AllowRemoteAccess] [-AllowVpnAccess]   [<CommonParameters>]  
```  
  
 예:  
  
```  
$password = ConvertTo-SecureString "Passw0rd!" -asplaintext  œforce  
$Add-WssUser -Name User2Test -Password $password -Accesslevel Administrator -FirstName User2 -LastName Test  
```  
  
 이 명령은 Passw0rd 암호로 user2test"라는 관리자로 추가 되었습니다.  
  
 **사용자 사용/사용 안 함**  
  
 예:  
  
```  
$CurrentUser = get-wssuser  œname user2test  
$CurrentUser.UserStatus = 0  
$CurrentUser.Commit()  
```  
  
 이 명령은 user2test"라는 사용자를 비활성화 합니다. UserStatus를 1로 설정하면 사용자를 사용합니다.  
  
 **서버 폴더 추가**  
  
```  
Add-WssFolder [-Name] <string> [-Path] <string> [[-Description] <string>] [-KeepPermissions] [<CommonParameters>]  
```  
  
 예:  
  
```  
$Add-WssFolder -Name "MyTestFolder" -Path "C:\ServerFolders\MyTestFolder"  
```  
  
 이 명령은 지정 된 위치의 MyTestFolder 라는 서버 폴더를 추가 합니다.  
  
## <a name="how-do-i-add-a-second-server-to-the-windows-server-essentials-domain"></a>Windows Server Essentials 도메인에 두 번째 서버를 추가 하려면 어떻게 하나요?  
 Windows Server Essentials 도메인 컨트롤러 이므로 표준 방식으로 도메인에 두 번째 서버를 조인할 수 있습니다.  
  
## <a name="which-email-solutions-can-be-integrated"></a>통합할 수 있는 메일 솔루션  
 Windows Server Essentials에서는 기본적으로 두 개의 전자 메일 솔루션과 통합을 지원합니다. 두 가지 전자 메일 솔루션 통합을 지원합니다. 자체 호스트 된 메일 솔루션을 실행 하는 경우에 추가 기능에 호스트 된 메일 솔루션을 사용 하 여 Windows Server Essentials 통합를 개발 해야 합니다.  
  
## <a name="how-do-i-migrate-on-premises-windows-sbs-201120082003-to-the-hosted-windows-server-essentials"></a>호스트 된 Windows Server Essentials에 온-프레미스 Windows SBS (2011/2008/2003) 마이그레이션하려면 어떻게 해야 하나요?  
 마이그레이션 가이드는 온-프레미스 Windows Small Business Server (Windows SBS) Windows Server Essentials 마이그레이션에 사용할 수 있습니다. 일부 단계는 호스트된 환경에 완전히 동일하게 적용되지 않을 수 있습니다. 하지만 마이그레이션할 일반 작업 및 작업량은 동일합니다. [마이그레이션 가이드](https://go.microsoft.com/fwlink/p/?LinkID=254292) 를 참조하여 호스팅 환경을 기준으로 필요한 사용자 지정을 수행하는 것이 좋습니다.  
  
 원본 서버 및 대상 서버를 동일한 서브넷에 배치하는 것이 좋습니다. 이것이 불가능한 경우 다음을 확인해야 합니다.  
  
-   원본 서버와 대상 서버의 내부 DNS 이름을 서로 연결할 수 있습니다.  
  
-   필요한 모든 포트가 열려 있습니다.  
  
## <a name="how-can-i-upgrade-windows-server-essentials-to-windows-server-standard"></a>Windows Server Essentials를 Windows Server Standard로 업그레이드할 수는 방법  
 Windows Server Essentials를 Windows Server Standard로 업그레이드할 수 있습니다. 잠금 및 제한을 제거하고 Windows Server Standard에 없는 패키지를 추가합니다. 자세한 내용을 보려면 [문서를 다운로드](https://go.microsoft.com/fwlink/p/?LinkID=253181)하세요.  
  
## <a name="what-are-the-native-tools-for-monitoring-and-management"></a>모니터링 및 관리를 위한 기본 도구  
  
### <a name="group-policy-management"></a>그룹 정책 관리  
 Windows Server Essentials는 Windows Server 2012의 기본 그룹 정책 지원을 활용 하 고 폴더 리디렉션 및 보안 설정을 구성 하는 사용자 인터페이스를 제공 합니다.  
  
> [!NOTE]
>  호스트된 환경에서 사용자 프로필에 대한 폴더 리디렉션을 사용하는 경우 데이터 크기가 크면 사용자가 로그온하는 데 걸리는 시간이 길어질 수 있습니다.  
  
### <a name="management-pack"></a>관리 팩  
 Windows Server Essentials 관리 팩이 다 수의 여러 소규모 회사에 전용된 Windows Server Essentials 서버를 관리 하는 호스팅 서비스 공급자를 Windows Server Essentials에서 상태 경고 시스템을 통해 모니터링 기능을 제공 합니다. 이 버전의 모니터링에는 시스템의 중요한 알림만 포함됩니다.  
  
#### <a name="management-pack-scope"></a>관리 팩 범위  
 이 관리 팩을 사용 하면 Windows Server Essentials에 특정 기능을 모니터링할 수 있습니다. Windows Server 2012 Standard 운영 체제의 일반적인 기능은 모니터링하지 않습니다. Windows Server Essentials를 모니터링 하려면 Windows Server Essentials 관리 팩 및는 관리 팩에 대 한 Windows Server 2012 Standard를 사용 해야 합니다.  
  
#### <a name="mandatory-configuration"></a>필수 구성  
 먼저 다음 단계를 수행해야 관리 팩을 사용할 수 있습니다.  
  
1.  에이전트를 설치하고 인증서 신뢰를 사용하여 신뢰를 구성합니다. Windows Server Essentials를 도메인 컨트롤러로 미리 구성 된 다른 도메인 또는 포리스트 트러스트를 사용할 수 없습니다 때문에 System Center Operation Manager 에이전트를 Windows Server Essentials를 설치 해야 하 고 관리를 사용 하 여 트러스트 구성 인증서를 사용 하는 서버입니다.  
  
2.  관리 팩을 다운로드합니다. Operations Manager 2007을 사용 하 여 Windows Server Essentials를 모니터링 하려면 먼저 다운로드 해야 합니다 [Windows Server 운영 체제 관리 팩](https://connect.microsoft.com/WindowsServer/Downloads/DownloadDetails.aspx?DownloadID=45010) 관리 팩 카탈로그에서 합니다.  
  
3.  관리 팩 파일을 가져옵니다. 지역화 버전의 관리 팩을 사용 중인 경우 주 관리 팩 파일과 언어 팩을 모두 가져와야 합니다.  
  
#### <a name="files-in-this-monitoring-pack"></a>이 모니터링 팩의 파일  
 모니터링 팩에 대 한 Windows Server Essentials에는 다음 파일이 포함 됩니다.  
  
-   Microsoft.Windows.Server.2012.Essentials.mp  
  
-   Microsoft.Windows.Server.2012.Essentials.<locale\>.mp  
  
### <a name="back-up-and-restore"></a>백업 및 복원  
 Windows Server Essentials를 사용 하면 서버와 클라이언트 모두를 백업할 수 있습니다.  
  
#### <a name="back-up-the-server"></a>서버 백업  
 Windows Server Essentials 서버 백업 과정의 두 가지 방법을 지원 합니다: 온-프레미스 백업 및 오프-프레미스 백업 합니다.  
  
 **온-프레미스 백업** 은 정기적으로 별도의 디스크에 블록 수준의 증분 백업을 수행할 수 있습니다. 호스팅 서비스 공급자를 Windows Server Essentials VM에 가상 디스크를 연결 하 고이 가상 디스크에 서버 백업을 구성할 수 있습니다. 가상 디스크를 Windows Server Essentials VM 보다 다른 물리적 디스크에 있어야 합니다.  
  
-   Windows Server Essentials VM을 백업 하는 다른 메커니즘 있고 Windows Server Essentials 기본 서버 백업 기능을 확인 하려면 사용자를 원하지 않는 경우이 해제 하 고 Windows Server Essentials에서 모든 관련된 사용자 인터페이스를 제거 수 있습니다. 대시보드입니다. 자세한 내용은의 서버 백업 사용자 지정 섹션을 참조 합니다 [ADK 문서](https://go.microsoft.com/fwlink/p/?LinkID=249124)합니다.  
  
 **오프-프레미스 백업**은 정기적으로 서버 데이터를 클라우드 서비스로 백업할 수 있습니다. 다운로드 하 고 Microsoft Azure Backup 통합 모듈에 대 한 Windows Server Essentials Microsoft에서 제공 하는 Azure Backup을 활용 하 여 설치할 수 있습니다.  
  
 관리자 또는 사용자가 다른 클라우드 서비스를 선호하는 경우 다음을 수행해야 합니다.  
  
1.  기본 Azure Backup 대신 원하는 클라우드 서비스에 대 한 링크를 제공 하도록 Windows Server Essentials 대시보드의 사용자 인터페이스를 업데이트 합니다. 자세한 내용은 [ADK 문서](https://go.microsoft.com/fwlink/p/?LinkID=249124)의 이미지 사용자 지정 섹션을 참조하세요.  
  
2.  (선택 사항) 구성 하 고 클라우드 백업 서비스를 관리 하는 Windows Server Essentials 대시보드용으로 추가 기능을 개발 합니다.  
  
#### <a name="back-up-the-client"></a>클라이언트 백업  
 Windows Server Essentials에서는 두 가지 유형의 클라이언트 데이터 백업: 전체 클라이언트 백업 및 파일 기록 합니다.  
  
> [!NOTE]
>  클라이언트 백업은 VPN을 통해 클라이언트에서 서버로 데이터를 전송해야 하므로 성능에 영향을 줄 수 있습니다.  
  
 **전체 클라이언트 백업** 켜져 기본적으로 Windows Server Essentials 네트워크에 연결 하는 모든 클라이언트 장치에 대 한 합니다. 전체 클라이언트(시스템 및 데이터)를 증분식으로 백업하며 데이터 중복 제거를 지원합니다. 백업 데이터를 Windows Server Essentials를 실행 하는 서버에 됩니다. 실패한 클라이언트는 이전 백업 지점으로 데이터를 복원할 수 있습니다. 끌 수 있습니다이 기능은 만들기에서 단계를 수행 하 여 Cfg.ini 파일 부분을 [ADK 문서](https://technet.microsoft.com/library/jj200150)합니다.  
  
 전체 클라이언트 백업에 대한 고려 사항은 다음과 같습니다.  
  
-   성능: 초기 클라이언트 백업은 업로드할 데이터 양 때문에 많은 시간이 소요될 수 있습니다.  
  
-   안정성: 클라이언트 쪽 인터넷 연결이 안정적이지 않은 경우가 있습니다. 클라이언트 백업은 다시 계속할 수 있도록 설계되며, 기본 검사점은 40GB입니다. 즉, 클라이언트 백업 데이터베이스는 40GB의 데이터가 백업될 때마다 검사점을 만듭니다. 인터넷 연결을 불안정할 것으로 예상되는 경우 이 값을 낮출 수 있습니다.  
  
    -   검사점 작업을 사용하려면 서버에서 레지스트리 키 HKLM\Software\Microsoft\Windows Server\Backup\GetCheckPointJobs를 1로 설정합니다.  
  
    -   검사점 임계값을 변경하려면 클라이언트에서 HKLM\Software\Microsoft\Windows Server\Backup\CheckPointThreshold의 기본값(40GB)을 변경합니다.  
  
-   BMR(Bare Metal Recovery): Windows 사전 설치 환경은 VPN 연결을 지원하지 않기 때문에 클라이언트 BMR(Bare Metal Recovery)이 지원되지 않습니다.  
  
 **파일 히스토리** 네트워크 공유에 프로필 데이터 (라이브러리, 데스크톱, 연락처, 즐겨찾기)를 백업 하기 위한 Windows 8.1 기능입니다. Windows Server Essentials에서 Windows Server Essentials에 가입 된 모든 Windows 8.1 클라이언트의 파일 히스토리 설정 중앙에서 관리할을 수 있습니다. 백업 데이터는 Windows Server Essentials를 실행하는 서버에 저장됩니다. 해제할 수 있습니다이 기능은 만들기에서 단계를 수행 하 여 Cfg.ini 파일 부분을 [ADK 문서](https://technet.microsoft.com/library/jj200150)합니다.  
  
### <a name="storage-management"></a>저장소 관리  
 [새 저장소 공간 기능](https://technet.microsoft.com/library/hh831739.aspx) 을 사용하면 개별 하드 드라이브의 실제 저장소 용량을 집계하고, 하드 드라이브를 동적으로 추가하며, 지정된 복원력 수준으로 데이터 볼륨을 만듭니다. 또한 해당 저장소를 확장 하려면 Windows Server Essentials에 iSCSI 디스크를 연결할 수 있습니다.  
  
## <a name="what-are-the-main-scenarios-i-should-test"></a>테스트할 주요 시나리오  
 호스트 관점에서 다음 시나리오를 테스트하는 것이 좋습니다.  
  
 **서버 배포**  
  
-   랩 환경에서 Windows Server Essentials 서버를 배포 합니다.  
  
-   필요한 경우 Windows Server Essentials 이미지를 사용자 지정합니다.  
  
-   무인된 파일 및 cfg.ini를 사용 하 여 Windows Server Essentials 배포를 자동화 합니다.  
  
-   호스트 된 Windows Server Essentials에 온-프레미스 Windows SBS를 마이그레이션하십시오.  
  
-   Windows Server Essentials에서 Windows Server 2012로 업그레이드 합니다.  
  
 **서버 구성**  
  
-   원격 액세스(VPN, 원격 웹 액세스, DirectAccess)를 구성합니다.  
  
-   저장소 및 서버 폴더를 구성합니다.  
  
-   (해당하는 경우) 서버 백업, 온라인 백업, 클라이언트 백업, 파일 기록을 구성합니다.  
  
-   (해당하는 경우) 저장소 공간을 구성하고 관리합니다.  
  
-   (해당하는 경우) 메일 솔루션 통합(Office 365, 호스트된 Exchange 등)을 구성합니다.  
  
-   (해당하는 경우) 미디어 서버를 구성합니다.  
  
 **서버 관리**  
  
-   사용자를 관리합니다.  
  
-   경고 메일 알림을 구성하고 수신합니다.  
  
-   오류/경고가 발생한 경우 BPA를 실행합니다.  
  
-   System Center 모니터링 팩을 구성합니다.  
  
-   손상이 발생한 경우 서버 복구를 구성합니다.  
  
 **클라이언트 환경**  
  
-   인터넷을 통한 클라이언트 배포(개인용 컴퓨터 또는 Mac OS).  
  
-   클라이언트에서 실행 패드를 사용하여 공유 폴더에 액세스합니다.  
  
-   개인용 컴퓨터, 휴대폰, 태블릿 등의 여러 장치에서 원격 웹 액세스를 통해 서버 자산에 액세스합니다.  
  
-   Windows Phone용 내 서버 앱.  
  
-   (해당하는 경우) 파일 기록, 클라이언트 백업 및 복원(BMR 안 됨), 폴더 리디렉션.  
  
-   (해당하는 경우) 메일 통합 환경.  
  
## <a name="where-can-i-get-more-support"></a>추가 지원을 받을 수 있는 위치  
 아래 링크에서 SDK 및 ADK 문서를 구할 수 있습니다.  
  
-   [SDK](https://go.microsoft.com/fwlink/p/?LinkID=248648)  
  
-   [ADK](https://go.microsoft.com/fwlink/p/?LinkID=249124)  
  
 Connect를 통해 기능 팀에 버그를 보고할 수 있습니다. 로그를 생성하려면 서버 및 서버에 연결한 클라이언트에서 C:\ProgramData\Microsoft\Windows Server\Logs 폴더를 압축합니다.
