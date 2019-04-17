---
title: "호스팅된 Windows Server Essentials"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 23e586c22ca14af7b02550e2fa1c9522e379170c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="hosted-windows-server-essentials"></a>호스팅된 Windows Server Essentials

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

이 문서는 Windows Server Essentials의 랩에서 배포 및 Windows Server Essentials 서비스로 고객에 게 제공 하 게 호스팅 업체와 관련 된 정보가 포함 됩니다.  
  
## <a name="what-is-windows-server-essentials"></a>Windows Server Essentials 란?  
 Windows Server Essentials의 최고의 64 비트 제품 기술을 기술이 대부분의 소기업 적합 서버 환경을 제공 하기 위해 포함 된 간 온-프레미스 중소기업 솔루션을입니다. Windows Server Essentials에는 다음과 같은 기술은 포함 됩니다.  
  
 **서버 운영 체제:** Windows Server 2012 제품 기술 Windows Server Essentials의 핵심 제공 합니다. 자세한 내용은 참조는 [Windows Server 2012 웹 사이트](https://www.microsoft.com/en-us/server-cloud/products/windows-server-2012-r2/default.aspx#fbid=ZH0GD_CRAWh)합니다.  
  
 **데이터 보호:** Windows Server Essentials 향상된 데이터 보호 기능을 제공 하기 위해 Windows Server 2012에서 사용할 수 있는 몇 가지 새로운 기능을 활용 합니다. [새 저장소 공간 기능](https://technet.microsoft.com/library/hh831739.aspx) 동적으로 하드 드라이브를 추가 하 고 데이터 볼륨의 복원 력이 지정된 수준으로 만들기 서로 다른 하드 드라이브의 실제 저장소 용량 결합할 수 있습니다. Windows Server Essentials 시스템 전체 백업을 수행할 수 하 고 네트워크에 연결 하는 클라이언트 컴퓨터 뿐만 아니라 자체 완전 서버 복원? 이제에 대 한 지원이 되었습니다 보다 큰 볼륨 합니다. Windows Server 2012와 새로운는 [Azure Online Backup-Windows](https://technet.microsoft.com/library/hh831419.aspx) Microsoft 관리 하는 클라우드 기반 저장소 서비스의 파일 및 폴더를 보호 하는 데 사용 됩니다. Windows Server Essentials 중앙도 관리 하 고 Windows 8.1 클라이언트를 지원 관리자를 않고도 파일 삭제 또는 덮어쓰여집니다 실수로 복구 하는 사용자의 파일 히스토리 기능을 구성 합니다.  
  
 **어디서 나 액세스:** 원격 Web Access 능률적인을 쉽게 터치 할 브라우저 환경을 제공 하는 인터넷 연결과 거의 모든 디바이스를 사용 하는 거의 모든 곳에서 응용 프로그램 및 데이터에 액세스 하기 위한 합니다. Windows Server Essentials 제공 하는 Windows Phone 앱 업데이트 및 새로운 앱 클라이언트 Windows 8.1 대 한 컴퓨터, 연결, 검색할 하 고 서버에서 파일 및 폴더에 액세스 하도록 허용 직관적 합니다. 파일은 자동으로 액세스 오프 라인에 대 한 캐시 고 서버에 연결을 사용할 수 있게 되 면 동기화 됩니다. Windows Server Essentials 가상 사설망 (VPN) 몇 번의 손쉽게, 마법사 기반 프로세스로 설정을 켜 하 고 사용자에 대 한 액세스 VPN 간단 합니다. 클라이언트 컴퓨터 원격 사무실에 통근를 않고도 Windows SBS 환경에 참여 하는 VPN 연결을 활용할 수 있습니다.  
  
 **작업 유연성:** Windows Server Essentials 허용 하는 고객 응용 프로그램을 선택 하는 유연성을 제공 하도록 설계 된 및 서비스가 프레미스 클라우드에서 실행 되 고에서 실행 됩니다. 이전 버전의 Windows 소규모 기업 서버 표준 포함 Exchange Server 지출 및 복잡성 바란 클라우드 기반 메시지 및 공동 작업 서비스를 이용 하는 고객에 대 한 추가 구성 요소 제품은 합니다. Windows Server Essentials와 고객 Exchange Server의 온-프레미스 복사본을 실행 하 여 호스팅된 Exchange 서비스를 구독 또는 Microsoft Office 365에 가입할 선택 있는지 여부 같은 유형의 통합된 관리 환경 이용을 걸릴 수 있습니다.  
  
 **상태: 모니터링** Windows Server Essentials 자체 상태 및 10.5 하 고 이후 Windows 8.1, Windows 7, Mac Osx 버전을 실행 하는 클라이언트 컴퓨터의 상태를 모니터링 합니다. 상태는 컴퓨터 백업, 서버 메모리, 디스크 공간 부족 및 더 관련 된 문제를 알려줍니다.  
  
 **확장성:** Windows SBS 2011 필수 패키지를 통해 다른 소프트웨어 공급 업체는 핵심 제품에 기능과 기능을 추가 하 고 새로운 집합이 웹 서비스 Api를 추가 하는 확장성 모델이에서 빌드를 Windows Server Essentials 합니다. 또한 기존와 호환성을 유지 [소프트웨어 개발 키트](https://msdn.microsoft.com/library/gg513958.aspx) (SDK) 및 [추가 기능](https://pinpoint.microsoft.com/applications/search?fpt=300105&q=small+business+server+essentials) SBS 2011 Essentials Windows 용으로 작성 합니다.  
  
## <a name="how-can-i-customize-an-image"></a>어떻게 이미지 사용자 지정할 수 있습니까?  
 참조는 [Windows Server Essentials](https://go.microsoft.com/fwlink/p/?LinkID=249124), 하는 Windows Server Essentials 사용자 지정 조치를 표준 Windows Server sysprep 프로세스입니다. 사용자 지정을 완료 하려면 지침에 따라 [간단한 사용자 지정 이미지를 만들려면](https://technet.microsoft.com/en-us/library/jj200117) 및 [이미지를 사용자 지정](https://technet.microsoft.com/en-us/library/jj200161)의 지침을 따릅니다 [이미지 배포 준비](https://technet.microsoft.com/en-us/library/jj200142) 최종 이미지를 캡처할 수 있습니다.  
  
 다음 사항에 주의 해야 합니다.  
  
1.  초기 구성 (회사 간)의 모든 드라이브 루트 SkipIC.txt 파일을 추가 하 여 건너뛰어야. 회사를 간 하기 전에 서버를 설치한 다음 Shift + F10 cmd 창의 시작 하는 c: 아래 SkipIC.txt 파일을 만듭니다 누릅니다 드라이브 / 합니다. 사용자 지정 후 SkipIC.txt 파일을 삭제 해야 합니다.  
  
2.  Windows Server Essentials 90 g B 보다 작은 디스크에 배포 해야 하는 경우 sysprep 전에 레지스트리 키를 추가 해야 합니다.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v HWRequirementChecks /t REG_DWORD /d 0 /f  
    ```  
  
 Sysprep 후 sysprep을 적용 디스크 이미지나 reseal 새 배포에 대 한 Install.wim 다시 사용할 수 있습니다.  
  
 가상 컴퓨터 관리자를 사용 하는 경우 실행 중인 인스턴스를 사용 하 여 템플릿을 만들 수 있습니다. 서식 sysprep 인스턴스는 만들고 서버를 종료 합니다. 라이브러리에 있는 저장 한 후 개별적으로에 인스턴스를 가져올 수 있습니다.  
  
##  <a name="BKMK_automatedeployment"></a>배포를 자동화 어떻게 하나요?  
 사용자 지정 된 이미지를 다운로드 한 후 사용자 이미지를 배포를 수행할 수 있습니다. Semiunattended 설치를 위해 제공/배포 unattend.xml WinPE 설정에 대 한 해야 합니다. 완전히 자동된 설치를 위해 또한 Windows Server Essentials 초기 구성 cfg.ini 파일 제공 해야 합니다.  
  
1.  자동된 WinPE 설치를 수행 합니다. 이 자동화 WinPE 설치 하 고 중지 한 후 초기 구성 최종 사용자에 게 제공할 수 있도록 Corp, 도메인 및 관리자 정보 자체적으로 RDP 후 서버 세션에 설치 합니다. 이렇게 하려면.  
  
    1.  Windows unattend.xml 파일을 제공 합니다. 에 따라는 [Windows 8.1 ADK](https://go.microsoft.com/fwlink/?LinkId=248694) 파일을 생성 하 고 서버 이름, 제품 키를 및 관리자 암호를 포함 하 여 필요한 모든 정보를 제공 하 합니다. Microsoft Windows 설치 부분이 unattend.xml 파일에서 아래와 같이 정보를 제공 합니다.  
  
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
  
    2.  고객이 초기 구성을 완료 관리자 및 RDP unattend.xml 파일 서버에에 지정 된 암호를 사용할 수 있도록 공용 IP에 3389 RDP 포트를 열어야 합니다.  
  
    > [!NOTE]
    >  기본 암호를 변경 하면 서버 설치 암호를 입력에 대 한 화면에 중지 됩니다. **노트** 최종 사용자가 기본 관리자 계정을 사용 하 여 서버에에 로그인 하 고 초기 구성 작업을 수행 하 해야 합니다.  
  
 가상 컴퓨터 관리자를 사용 하는 새 인스턴스 서식 파일을 만들 때 콘솔에서 관리자 암호를 지정할 수 있습니다.  
  
1.  초기 구성 자리를 비운 사이 포함 하 여 자동된 설정을 완료 수행 합니다. 이렇게 하려면.  
  
    1.  배포 WinPE 설정에서 시작 하는 경우, 위에 했던 것 처럼 unattend.xml 파일을 제공 합니다.  
  
    2.  Windows Server Essentials ADK 섹션을 참조 [Cfg.ini 파일을 만들](https://technet.microsoft.com/en-us/library/jj200150)는 cfg.ini 얻기 위해 합니다.  
  
    3.  [InitialConfiguration]에 정보를 제공 합니다.  
  
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
  
    4.  [PostOSInstall]에 정보를 제공 합니다.  
  
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
  
    5.  WebDomainName 매개 변수를 제공 하는 경우 DNS 레코드도 서버 s 공개 IP 가리키도록 업데이트 되 고 있는지 확인 합니다.  
  
    6.  위의 WebDomainName 정보를 제공 하지 않은 경우 고객 RDP VPN 구성을 완료 하 고 서버에 연결에 사용할 수 있도록 3389 포트를 열 수 있는지 확인 합니다.  
  
> [!NOTE]
>  VM 호스트 server 및 Windows Server Essentials VM의 표준 시간대 설정을 동일 인지 확인 합니다. 그렇지 않은 경우 몇 가지 다른 오류가 발생할 수 있습니다 (초기 구성에서 되지 않을 수 있습니다 인증서 관련 작업; 설치 후 몇 시간 동안 인증서 작동 하지 않을 수 장치 정보 등; 올바르게 업데이트 되지).  
  
 배포 후 다음 레지스트리 키 HKLM\software\microsoft\windows server\setup 초기 구성 성공 했는지 확인 하려면 아래를 확인 합니다. 하는 경우 SetupStage ICDone = = & & ICStatus = = 1, 초기 구성 성공적으로 완료 된 것을 의미 합니다.  
  
## <a name="what-is-the-supported-network-topology"></a>지원 되는 네트워크 토폴로지 무엇 인가요?  
 Windows Server Essentials 로밍 클라이언트에서를 사용 하려면 VPN은 사용 해야 합니다. 포트 443 SSTP VPN 연결을 사용 하는 것이 좋습니다. 미디어 서버 기능, 웹에 대 한 원격 액세스 또는 웹 서비스 앱에 필요한 경우 포트 80도 사용 해야 합니다.  
  
 Windows PowerShell 스크립트를 통해 자동된 배포 하는 동안 VPN 되도록 수행할 수 있습니다 또는 초기 구성 후 우리의 마법사를 구성할 수 있습니다.  
  

-   자동된 배포 하는 동안 VPN을 사용 하려면 참조 [배포를 자동화 어떻게 하나요? ](Hosted-Windows-Server-Essentials.md#BKMK_automatedeployment) 이 문서의 합니다.  

-   자동된 배포 하는 동안 VPN을 사용 하려면 참조 [배포를 자동화 어떻게 하나요? ](../install/Hosted-Windows-Server-Essentials.md#BKMK_automatedeployment) 이 문서의 합니다.  

  
-   Windows PowerShell를 통해 VPN을 사용 하려면 다음 cmdlet 관리자 권한으로 실행 하 고 필요한 모든 정보를 제공 합니다.  
  
    ```  
    ##  
    ## To configure external domain and SSL certificate (if not yet done in unattended Initial Configuration).  
    ##  
  
    $myExternalDomainName = 'remote.contoso.com';   ## corresponds to A or AAAA DNS record(s) that can be resolved on Internet and routed to the server  
    $mySslCertificateFile = 'C:\ssl.pfx';   ## full path to SSL certificate file  
    $mySslCertificatePassword = ConvertTo-SecureString '******';   ## password for private key of the SSL certificate  
    $skipCertificateVerification = $true;   ## whether or not, skip verification for the SSL certificate  
  
    Add-Type -AssemblyName 'Wssg.Web.DomainManagerObjectModel';  
    [Microsoft.WindowsServerSolutions.RemoteAccess.Domains.DomainConfigurationHelper]::SetDomainNameAndCertificate($myExternalDomainName,$mySslCertificateFile,$mySslCertificatePassword,$skipCertificateVerification);  
    ##  
    ## To install VPN with static IPv4 pool (and allow all existing users to establish VPN).  
    ##  
  
    Install-WssVpnServer -IPv4AddressRange ('192.168.0.160','192.168.0.240') -ApplyToExistingUsers;  
    ```  
  
 서버 고객에 게 제공 하기 전에 VPN 연결을 제공할 수 없는 경우 최종 사용자가 RDP 서버에 연결 하 고 구성 자체적으로 수행를 사용할 수 있도록 서버 포트 3389 인터넷에 연결할 수 있는 인지 확인 합니다.  
  
 다음은 두 가지 일반적인 서버 쪽 네트워킹, 토폴로지와 어떻게 VPN/원격 웹 Access (RWA)를 구성할 수 있습니다.  
  
-   토폴로지 1 (권장)  
  
    -   NAT에 장치에서 별도 가상 네트워크에서 서버 합니다.  
  
    -   가상 네트워크에서 DHCP 서비스를 사용 하거나 서버에서 고정 IP 주소를 지정 된 합니다.  
  
    -   서버 포트 443는 공개 IP 443 포트에서 연결할 수 있습니다.  
  
    -   VPN 통과 포트 443 허용 됩니다.  
  
    -   VPN IPv4 주소 풀 서버 주소 같은 서브넷에서 공격 해야 합니다.  
  
    -   두 번째 모든 서버 내 같은 서브넷 하지만 VPN 주소 풀에서 고정 IP 할당 되어야 합니다.  
  
-   토폴로지 2:  
  
    -   서버 개인 IP 주소가 되었습니다.  
  
    -   공용 IP 주소의 포트 443에서에서 포트 443 서버에 연결할 수 있는입니다.  
  
    -   VPN 통과 포트 443 허용 됩니다.  
  
    -   VPN IPv4 주소 풀 서버 주소 다른 범위 내에입니다.  
  
 토폴로지 2 두 번째 서버 시나리오를 지원 하지 않습니다.  
  
## <a name="how-do-i-perform-common-tasks-via-windows-powershell"></a>Windows PowerShell를 통해 일반적인 작업을 수행 하려면 어떻게 해야 하나요?  
 **원격 웹 액세스**  
  
```  
Enable-WssRemoteWebAccess [-SkipRouter] [-DenyAccessByDefault] [-ApplyToExistingUsers]  
```  
  
 예:  
  
```  
$Enable-WssRemoteWebAccess  œDenyAccessByDefault  œApplyToExistingUsers  
```  
  
 이 명령을 자동으로 구성 라우터 원격 웹 액세스를 활성화 되 고 모든 사용자에 게 기존의 기본 액세스 권한을 변경 합니다.  
  
 **사용자 추가**  
  
```  
Add-WssUser [-Name] <string> [-Password] <securestring> [-AccessLevel <string> {User | Administrator}] [-FirstName <string>] [-LastName <string>] [-AllowRemoteAccess] [-AllowVpnAccess]   [<CommonParameters>]  
```  
  
 예:  
  
```  
$password = ConvertTo-SecureString "Passw0rd!" -asplaintext  œforce  
$Add-WssUser -Name User2Test -Password $password -Accesslevel Administrator -FirstName User2 -LastName Test  
```  
  
 이 명령을 User2Test 암호 Passw0rd 붙은 관리자가 추가 됩니다!.  
  
 **사용자 설정/해제**  
  
 예:  
  
```  
$CurrentUser = get-wssuser  œname user2test  
$CurrentUser.UserStatus = 0  
$CurrentUser.Commit()  
```  
  
 이 명령을 user2test 라는 이름의 사용자 사용 되지 것입니다. 1 UserStatus 설정 사용자 수 있게 합니다.  
  
 **서버 폴더 추가**  
  
```  
Add-WssFolder [-Name] <string> [-Path] <string> [[-Description] <string>] [-KeepPermissions] [<CommonParameters>]  
```  
  
 예:  
  
```  
$Add-WssFolder -Name "MyTestFolder" -Path "C:\ServerFolders\MyTestFolder"  
```  
  
 이 명령을 MyTestFolder 지정된 위치에 라는 서버 폴더를 추가 합니다.  
  
## <a name="how-do-i-add-a-second-server-to-the-windows-server-essentials-domain"></a>두 번째 서버 Windows Server Essentials 도메인에 추가 하려면 어떻게 해야 하나요?  
 Windows Server Essentials 도메인 컨트롤러 이기 때문에 두 번째 서버 도메인 표준 방식에서으로 연결할 수 있습니다.  
  
## <a name="which-email-solutions-can-be-integrated"></a>어떤 메일 솔루션 통합할 수 있나요?  
 Windows Server Essentials 통합은 개봉 후 두 메일 솔루션을 지원: Office 365와 온-프레미스 Exchange 합니다. 호스팅된 메일 솔루션을 실행 하는 경우 추가 기능에 Windows Server Essentials 여 호스팅된 메일 솔루션 부합 개발 해야 합니다.  
  
## <a name="how-do-i-migrate-on-premises-windows-sbs-201120082003-to-the-hosted-windows-server-essentials"></a>온-프레미스 Windows SBS (2011/2008/2003) 하 여 호스팅된 Windows Server Essentials 마이그레이션을 하려면는 방법  
 마이그레이션 가이드는 온-프레미스 Windows Small Business Server (Windows SBS) Windows Server Essentials 마이그레이션을를 사용할 수 있습니다. 단계 중 일부 수에 적용 되지 똑같이 여 호스팅된 환경 합니다. 그러나 일반 작업 및 마이그레이션될 작업 동일 해야 합니다. 참조 하는 것이 좋습니다는 [마이그레이션 가이드](https://go.microsoft.com/fwlink/p/?LinkID=254292) 호스팅 귀하의 환경에 따라 필요한 사용자 지정 하 고 있습니다.  
  
 원본 서버와 대상 서버 같은 서브넷에 저장 하는 것이 좋습니다. 없는 경우 있는지 확인 해야 하는 다음과 같습니다.  
  
-   원본 서버와 대상 서버의 내부 DNS 이름은 서로 하 여 연결할 수 있습니다.  
  
-   필요한 모든 포트 열려 있습니다.  
  
## <a name="how-can-i-upgrade-windows-server-essentials-to-windows-server-standard"></a>Windows Server Essentials Windows Server 표준으로 업그레이드 수 어떻게 해야 하나요?  
 Windows Server Essentials Windows Server 표준로 업그레이드할 수 있습니다. 잠금 하 고 한계를 제거 하 고 Windows Server 표준에서 누락 된 패키지를 추가 합니다. 자세한 내용은 [문서 다운로드](https://go.microsoft.com/fwlink/p/?LinkID=253181)합니다.  
  
## <a name="what-are-the-native-tools-for-monitoring-and-management"></a>기본 도구를 모니터링 하 고 관리 이란 무엇 인가요?  
  
### <a name="group-policy-management"></a>그룹 정책 관리  
 Windows Server Essentials Windows Server 2012에서 기본적으로 그룹 정책 지원 활용 하 고 폴더 리디렉션 및 보안 설정을 구성 하려면 사용자 인터페이스를 제공 합니다.  
  
> [!NOTE]
>  여 호스팅된 환경에 대 한 사용자 프로필을 폴더 리디렉션을 사용 하는 경우 데이터 크기가 큰 경우 로그인에 사용한 최종 사용자에 대 한 시간을 늘어날 수 있습니다.  
  
### <a name="management-pack"></a>관리 팩  
 Windows Server Essentials 관리 팩 호스팅 업체 많은 다른 중소기업 회사 전용된 Windows Server Essentials 서버 관리를 위해 Windows Server Essentials의 상태 알림 시스템에 대해 모니터링 기능을 제공 합니다. 이 버전에서는 모니터링 중요 한 경고가 시스템에 포함 됩니다.  
  
#### <a name="management-pack-scope"></a>관리 팩 범위  
 이 관리 팩 Windows Server Essentials에 특정 기능을 모니터링할 수 있습니다. Windows Server 2012 표준 운영 체제의 일반적인 기능 모니터링 하지 않습니다. Windows Server Essentials 모니터를 위해 Windows Server Essentials 관리 팩 및 관리 팩에 대 한 Windows Server 2012 표준 모두 사용 해야 합니다.  
  
#### <a name="mandatory-configuration"></a>필수 구성  
 다음 단계 관리 팩은 사용 하려면 먼저 수행 해야 합니다.  
  
1.  에이전트 설치 하 고 보안 인증서를 사용 하 여 신뢰를 구성 합니다. Windows Server Essentials 도메인 컨트롤러 미리 다른 도메인 또는 숲 신뢰를 사용할 수 없습니다 하므로, 시스템 센터 작업 관리자 에이전트 Windows Server Essentials를 설치 해야 하 고 보안 인증서를 사용 하 여 관리 서버를 구성 합니다.  
  
2.  관리 팩을 다운로드할 수 있습니다. Windows Server Essentials 모니터링할 Operations Manager 2007를 사용 하 여 먼저 다운로드 해야는 [Windows Server 운영 체제의 관리 팩](https://connect.microsoft.com/WindowsServer/Downloads/DownloadDetails.aspx?DownloadID=45010) 관리 팩 카탈로그에서 합니다.  
  
3.  관리 팩 파일을 가져옵니다. 관리 팩의 지역화 된 버전을 사용 하는 경우 언어 팩 및 관리 주 팩 파일을 가져올 필요 합니다.  
  
#### <a name="files-in-this-monitoring-pack"></a>이 모니터링 팩의 파일  
 다음 파일을 모니터링 팩에 대 한 Windows Server Essentials은 다음과 같습니다.  
  
-   Microsoft.Windows.Server.2012.Essentials.mp  
  
-   Microsoft.Windows.Server.2012.Essentials입니다. < locale\ >.mp  
  
### <a name="back-up-and-restore"></a>백업 및 복원  
 Windows Server Essentials 서버와 클라이언트 백업할 수 있습니다.  
  
#### <a name="back-up-the-server"></a>서버를 백업  
 Windows Server Essentials의 서버에 백업 두 가지 방법을 지원: 온-프레미스 백업 및 끄기 온-프레미스 백업 합니다.  
  
 **온-프레미스 백업** 별도 디스크를 정기적으로 차단 수준을 증분 백업을 수행할 수 있습니다. 호스팅,으로 Windows Server Essentials VM에 가상 디스크를 연결 하 고 서버 백업을 가상이 디스크를 구성 수 있습니다. 가상 디스크는 다른 Windows Server Essentials VM 실제 디스크에 있어야 합니다.  
  
-   Windows Server Essentials VM 백업할 수 있고 사용자 사용자에 게 기본 Windows Server Essentials 서버 백업 기능 표시 하지 않으려는 경우 끌 및 Windows Server Essentials 대시보드에서 모든 관련 된 사용자 인터페이스를 제거 될 수 있습니다. 자세한 내용은 사용자 지정 서버 백업 섹션을 참조는 [ADK 문서](https://go.microsoft.com/fwlink/p/?LinkID=249124)합니다.  
  
 **끄기 온-프레미스 백업** 서버 데이터 클라우드 서비스를 정기적으로 백업 수 있습니다. 다운로드 하 고 있는 Microsoft Azure 백업 통합 모듈에 대 한 Windows Server Essentials Microsoft에서 제공 하는 Azure 백업 활용할 수 있도록 설치할 수 있습니다.  
  
 사용자 또는 사용자가 원하는 다른 클라우드 서비스를 하는 경우 다음을 수행 해야 합니다.  
  
1.  기본 Azure 백업 하는 대신 사용자 기본 클라우드 서비스에 대 한 링크를 제공 하도록 Windows Server Essentials 대시보드의 사용자 인터페이스를 업데이트 합니다. 자세한 내용은 참조 사용자 지정의 이미지 섹션은 [ADK 문서](https://go.microsoft.com/fwlink/p/?LinkID=249124)합니다.  
  
2.  (선택 사항) Windows Server Essentials 대시보드 구성 하 고 관리 클라우드 백업 서비스에 대 한 추가 기능을 개발 합니다.  
  
#### <a name="back-up-the-client"></a>클라이언트 백업  
 Windows Server Essentials에서는 두 가지 유형의 클라이언트 데이터 백업: 전체 클라이언트 백업 및 파일 히스토리 합니다.  
  
> [!NOTE]
>  클라이언트를 백업 데이터를 통해 VPN 클라이언트는 서버 전송할 수 하기 때문에 성능이 저하 될 수 있습니다.  
  
 **전체 클라이언트 백업** Windows Server Essentials 네트워크에 연결 된 모든 클라이언트 디바이스에 대 한에 기본적으로 합니다. 증분 전체 클라이언트 시스템와 데이터를 백업 하 고 데이터 중복 제거를 지원 합니다. Windows Server Essentials 실행 하는 서버에 데이터 백업 됩니다. 실패 하는 클라이언트 백업를 이전 시점으로 다시 데이터를 가져올 수 있습니다. 끌 수 있습니다이 기능은 만들기의 단계를 수행 하 여의 Cfg.ini 파일 섹션은 [ADK 문서](https://technet.microsoft.com/en-us/library/jj200150)합니다.  
  
 전체 클라이언트 백업에 대 한 몇 가지 사항을 다음과 같습니다.  
  
-   성능: 초기 클라이언트 백업 시간이 오래 걸릴 때문에 수도 업로드 하는 데이터의 양을 합니다.  
  
-   안정성: 때때로 인터넷 연결이 없는 경우 클라이언트 쪽 안정적인 클라이언트 백업을 다시 시작 될 수 있도록 되어 있고 기본 검사점 40 g B (클라이언트 백업 데이터베이스 만들어집니다 검사점 40 g B 데이터를 백업 때마다). 이 값 신뢰할 수 있는 인터넷 연결을 원하는 경우 더 적은 수를 변경할 수 있습니다.  
  
    -   서버에서 검사점 작업을 사용 하도록 설정 하려면 1 레지스트리 키 HKLM\Software\Microsoft\Windows Server\Backup\GetCheckPointJobs 설정 합니다.  
  
    -   검사점 임계값 클라이언트에서 변경 하려면 HKLM\Software\Microsoft\Windows Server\Backup\CheckPointThreshold 기본값 40 1GB에서에서 변경 합니다.  
  
-   앙상한 금속 복원 클라이언트: Windows 사전 설치 환경 VPN 연결을 지원 하지 않으므로 클라이언트 앙상한 Metal 복원 지원 되지 않습니다.  
  
 **파일 히스토리** 네트워크 공유를 (라이브러리, 바탕 화면, 연락처, 즐겨찾기) 프로필 데이터를 백업에 대 한 Windows 8.1 기능입니다. Windows Server Essentials Windows Server Essentials에 가입 하는 일부 Windows 8.1 클라이언트의 파일 히스토리 설정의 중앙 관리 수 있도록 했습니다. 백업 하는 데이터는 Windows Server Essentials 실행 하는 서버에 저장 됩니다. 끌 수 있습니다이 기능은 만들기의 단계를 수행 하 여의 Cfg.ini 파일 섹션은 [ADK 문서](https://technet.microsoft.com/en-us/library/jj200150)합니다.  
  
### <a name="storage-management"></a>저장소 관리  
 [새 저장소 공간 기능](https://technet.microsoft.com/library/hh831739.aspx) 동적으로 하드 드라이브를 추가 하 고 데이터 볼륨의 복원 력이 지정된 수준으로 만들기 서로 다른 하드 드라이브의 실제 저장소 용량 결합할 수 있습니다. 또한 Windows Server Essentials의 저장소를 iSCSI 디스크를 첨부할 수 있습니다.  
  
## <a name="what-are-the-main-scenarios-i-should-test"></a>저는 테스트 해야 주요 시나리오 이란 무엇 인가요?  
 호스팅 관점에서 다음과 같은 경우 테스트 하는 것이 좋습니다.  
  
 **서버 배포**  
  
-   사용자 환경에서 Windows Server Essentials 서버를 배포 합니다.  
  
-   필요에 따라 Windows Server Essentials 이미지를 사용자 지정 합니다.  
  
-   자동 자동된 파일 cfg.ini와 Windows Server Essentials 구축 합니다.  
  
-   온-프레미스 Windows SBS 호스팅된 Windows Server Essentials 마이그레이션을 합니다.  
  
-   Windows Server 2012 Windows Server Essentials에서 업그레이드 합니다.  
  
 **서버 구성**  
  
-   어디서 나 액세스 (원격 Web Access VPN DirectAccess) 구성 합니다.  
  
-   저장소 및 서버 폴더를 구성할 합니다.  
  
-   해당 하는 경우 서버 백업, Online Backup-, 백업 클라이언트 파일 히스토리를 구성 합니다.  
  
-   해당 하는 경우 구성 하 고 저장소 공간을 관리 합니다.  
  
-   해당 하는 경우 메일 솔루션 통합 (Office 365, 호스팅된 교환 및 등)을 구성 합니다.  
  
-   해당 하는 경우 미디어 서버를 구성 합니다.  
  
 **서버 관리**  
  
-   사용자가 관리 합니다.  
  
-   구성 하 고 메일 알림 알림을 받게 됩니다.  
  
-   발생할 경우 오류/경고 BPA 실행 합니다.  
  
-   System Center 팩을 모니터링 구성 합니다.  
  
-   서버 복구 손상이 발생할 경우를 구성 합니다.  
  
 **클라이언트 환경**  
  
-   (Mac OS 또는 개인용 컴퓨터) 인터넷을 통해 클라이언트 배포 됩니다.  
  
-   클라이언트의 실행 패드를 사용 하 여 공유 폴더에 액세스할 수 있습니다.  
  
-   액세스 서버 자산 원격 Web Access을 통해 다양 한 장치 (개인용 컴퓨터, 휴대폰, 태블릿)의 합니다.  
  
-   Windows Phone 대 한 서버 앱 내 합니다.  
  
-   해당 하는 경우 파일 히스토리, 클라이언트 백업 및 복원 (BMR 없음) 폴더 리디렉션 합니다.  
  
-   해당 하는 경우 메일 통합 경험 합니다.  
  
## <a name="where-can-i-get-more-support"></a>더 많은 지원이 가져오기  
 아래 링크를 통해 SDK 및 ADK 문서를 이동할 수 있습니다.  
  
-   [SDK](https://go.microsoft.com/fwlink/p/?LinkID=248648)  
  
-   [ADK](https://go.microsoft.com/fwlink/p/?LinkID=249124)  
  
 연결을 통해 기능 팀에 게 버그를 보고할 수 있습니다. 로그를 생성 하려면 서버와 서버에 참여 하는 클라이언트에서 폴더를 압축: C:\ProgramData\Microsoft\Windows Server\Logs 합니다.
