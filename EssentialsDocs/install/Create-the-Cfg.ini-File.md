---
title: Cfg.ini 파일 만들기
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 93a73556-22ef-402d-b8d4-582b74c22bcf
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 52a4af1e5cadcec1bae46aacb4ac4624c3ecc584
ms.sourcegitcommit: 6d6a0225b1f83b71fcb494b94d666cd5e54c7566
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85267654"
---
# <a name="create-the-cfgini-file"></a>Cfg.ini 파일 만들기

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

cfg.ini 파일은 다음 시나리오에서 운영 체제의 설치를 자동화하는 데 사용됩니다.  
  
-   사전 설치된 이미지를 사용하여 대상 컴퓨터에 최종 사용자 환경을 테스트할 경우 유인 또는 무인 모드로 설치를 진행하기 위해 초기 구성 섹션이 사용됩니다. 이렇게 하려면 [초기 구성 섹션 만들기](Create-the-Cfg.ini-File.md#BKMK_CreateInit2)를 참조하세요.  
  
##  <a name="create-the-initial-configuration-section"></a><a name="BKMK_CreateInit2"></a>초기 구성 섹션 만들기  
 cfg.ini 파일에서 초기 구성 섹션을 사용하여 유인 또는 무인 모드로 설치를 진행할 수 있습니다.  
  
#### <a name="to-define-the-initial-configuration-section"></a>초기 구성 섹션을 정의하려면  
  
1.  cfg.ini 파일이 있으면 메모장에서 엽니다. 파일이 없으면 새 파일을 만듭니다.  
  
2.  다음 텍스트를 추가하여 InitialConfiguration 섹션을 만듭니다.  
  
    ```  
  
    [InitialConfiguration]  
    ;Optional, display language can only be one of the installed language  
    Language=en-us  
    ;Optional, The name of a script that runs after setupComplete.cmd but before the initial configuration begins.  
    ;Optional  
    Locale=en-us  
    ;Optional  
    Country=US  
    ;Optional  
    Keyboard=0409:00000409  
    AcceptEula=true  
    ;This is only required on a server where an OEM EULA has been specified   
    ;by using the OOBE.xml file  
    AcceptOEMEula=true  
    ;Optional. Example: My Company Name  
    CompanyName=EnterCompanyName  
    ServerName=EnterServerName  
    ; Example: CONTOSO  
    NetbiosName=EnterNetbiosDomainName  
    ; Example: contoso.local  
    DNSName=EnterDNSDomain   
    ; Used to set the user name for the domain admin  
    UserName=EnterDomainAdminUserName  
    ;The password has to be strong and at least 8 characters  
    PlainTextPassword=EnterAdminPassword  
    ;. Used to set the user name for the domain standard user account. Ignored in migration mode.  
    StdUserName=EnterDomainStandardUserName  
    ;. The password for the domain standard user account has to be strong and at least 8 characters  
    StdUserPlainTextPassword=EnterStandardUserPassword  
    ;Controls the Watson and automatic update settings  
    Settings=All or Updates or None  
    WebDomainName=www.abc.com  
    TrustedCertFileName=c:\cert\a.pfx  
    TrustedCertPassword=Enteryourpassword  
    EnableVPN=true  
    EnableRWA=true  
    IPv4DNSForwarder=<IPV4Address,IPV4Address,¦>  
    IPv6DNSForwarder=<IPV6Address,IPV6Address,¦>  
    VpnIPv4StartAddress=<IPV4Address>  
    VpnIPv4EndAddress=<IPV4Address>  
    VpnBaseIPv6Address=<IPV6Address>  
    VpnIPv6PrefixLength=<number>  
    ;All these section are optional.  
     [PostOSInstall]  
    ;Optional, The name of a script that runs after setupComplete.cmd but before the initial configuration begins.  
  
    IsHosted=true  
    StaticIPv4Address=<IPV4Address>  
    StaticIPv4Gateway=<IPV4Address>  
    StaticIPv4SubnetMask=<IPV4SubnetMask>   
    StaticIPv6Address=<IPV6Address>  
    StaticIPv6SubnetPrefixLength=<number>  
    StaticIPv6Gateway=<IPV6Address>  
    ClientBackupOn=true  
    FileHistoryOn=true  
    LaunchPadHiddenTasks=<Microsoft.LaunchPad.AdminDashboard,Microsoft.LaunchPad.Backup>  
  
    ```  
  
    > [!NOTE]
    >  초기 구성 중 다른 언어를 선택할 수 있는 옵션은 제공되지 않습니다. 시스템을 다시 설정하면 운영 체제의 언어가 처음에 설치했던 언어가 됩니다.  
  
    |매개 변수 이름|매개 변수 설명|  
    |--------------------|---------------------------|  
    |*AcceptEula*|사용자가 Microsoft 소프트웨어 사용 조건에 동의하는지를 나타냅니다. 값은 True 또는 False일 수 있지만 이 값이 True로 설정된 경우에만 설치가 진행됩니다.|  
    |*AcceptOEMEula*|(선택 사항) 사용자가 파트너 사용권 계약에 동의하는지를 나타냅니다. 값은 True 또는 False일 수 있습니다. 이 필드는 별도의 사용권 계약을 제공한 파트너로부터 서버를 구매한 경우에만 필요합니다.|  
    |*CompanyName*|(선택 사항) 회사의 이름입니다. 회사 이름은 사용자의 서버를 회사에 연결하고 회사 보고서를 사용자 지정하는 데 사용됩니다. 최대 254자까지 입력할 수 있습니다.|  
    |*국가*|(선택 사항) 원하는 국가/지역을 나타내는 스트링입니다. 예: 미국의 경우 US입니다.|  
    |*데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면*|서버 이름은 네트워크에서 서버를 고유하게 식별합니다. 서버 이름은 다음 조건을 만족해야 합니다.<br /><br /> -최대 15 자까지 지정할 수 있습니다.<br /><br /> -문자, 숫자 및 하이픈 (-)을 포함할 수 있습니다.<br /><br /> -하이픈으로 시작 하면 안 됩니다.<br /><br /> -공백을 포함 하지 않아야 합니다.<br /><br /> -숫자만 포함 해서는 안 됩니다.<br /><br /> 예: ContosoServer|  
    |*DNSName*|내부 도메인이 서버 및 클라이언트 컴퓨터를 함께 그룹화하여 사용자 이름, 암호의 공통 데이터베이스 및 기타 공통 정보를 공유하도록 합니다. 사용자는 자신의 컴퓨터에 로그인할 때 이 이름을 보게 되지만 내부에서만 사용되며 인터넷 도메인 이름과 동일하지 않습니다. 내부 도메인 이름은 *ServerName*에 대해 지정된 동일한 조건을 만족해야 합니다.<br /><br /> 예: contoso.local|  
    |*NetbiosName*|NetBIOS 이름은 서버에서 실행되고 있는 리소스를 식별하는 데 사용됩니다. 최대 15자까지 입력할 수 있습니다. 예: Contoso|  
    |*언어*|(선택 사항) 표시 언어를 지정합니다. 설치된 언어 중 하나일 수만 있습니다. 예: 미국에서 사용되는 영어의 경우 en-us입니다.|  
    |*로캘을*|(선택 사항) *LocaleID* 형식을 사용하여 시간 및 통화 형식을 지정합니다. 예: 영어로 표시되는 통화 및 시간과 미국에서 사용되는 표준에 따라 형식이 지정된 경우 en-us입니다.|  
    |*키보드*|키보드는 다음 두 형식 중 하나가 될 수 있습니다.<br /><br /> - **입력 언어: 키보드 레이아웃.** 예를 들어 0409:00000409에서 **:** 앞의 0409는 입력 언어이며 **00000409**는 키보드 레이아웃입니다. 레지스트리 키(**HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Keyboard Layouts**)에서 키보드 레이아웃 목록을 찾을 수 있습니다.<br /><br /> - **입력 언어: IME 식별자입니다.** 아래는 IME 식별자의 전체 목록입니다.<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1} {8F96574E-C86C-4bd6-9666-3F7327D4CBE8} 암하라어 입력 방법<br /><br /> -{81d4e9c9-1d3b-41bc-9e6c-4b40bf79e35e} {FA550B04-5AD7-411F-A5AC-CA038EC515D7} Microsoft 병음-Simple Fast (중국어 간체)<br /><br /> -{531FDEBF-9B4C-4A43-A2AA-960E8FCDC732} {B2F9C502-1742-11D4-9790-0080C882687E} 중국어 (번체)-새 음성<br /><br /> -{531FDEBF-9B4C-4A43-A2AA-960E8FCDC732} {4BDF9F03-C7D3-11D4-B2AB-0080C882687E} 중국어 (번체)-ChangJie<br /><br /> -{531FDEBF-9B4C-4A43-A2AA-960E8FCDC732} {6024B45F-5C54-11D4-B921-0080C882687E} 중국어 (번체)-Quick<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1} {D38EFF65-AA46-4FD5-91A7-67845FB02F5B} 중국어 번체 배열<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1} {037B2C25-480C-4D7F-B027-D6CA6B69788A} 중국어 번체 DaYi<br /><br /> -{03B5835F-F03C-411B-9CE2-AA23E1171E36} {A76C93D9-5523-4E90-AAFA-4DB112F9AC76} Microsoft IME (일본어)<br /><br /> -{A028AE76-01B1-46C2-99C4-ACD9858AE02F} {B5FE1F02-D5F2-4445-9C03-C568F23C99A1} Microsoft IME (한국어)<br /><br /> -{A1E2B86B-924A-4D43-80F6-8A820DF7190F} {B60AF051-257A-46BC-B9D3-84DAD819BAFB} 이전 한글 IME (한국어)<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1} {409C8376-007b-007B-4357-AE8E} Yi Input 메서드<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1} {3CAB88B7-CC3E-46A6-9765-B772AD7761FF} 티그리냐어 입력 방법|  
    |*설정*|업데이트에 대한 사용자 선택을 설정합니다. 다음 값 중 하나를 사용합니다.<br /><br /> **-모두** 권장 설정을 사용 합니다.<br /><br /> **-업데이트** 는 중요 업데이트를 설치 하는 것과 같습니다. 전용<br /><br /> **-없음은** 업데이트를 확인 하지 않습니다.|  
    |*이름*|-설치 중에 생성 되는 새 관리자 계정의 이름입니다. 관리자 및 표준 사용자 계정 이름은 다음 조건을 만족해야 합니다.<br /><br /> -최대 19 자까지 입력할 수 있습니다.<br /><br /> -/\ []  &#124; < > + =;을 (를) 포함할 수 없습니다. , ? *<br /><br /> -마침표로 시작 하거나 끝날 수 없습니다.<br /><br /> -연속 된 두 개의 마침표를 포함 해서는 안 됩니다.<br /><br /> -서버 이름 또는 내부 도메인 이름과 달라 야 합니다.<br /><br /> -관리자 또는 게스트와 같은 미리 정의 된 사용자 이름과 달라 야 합니다.|  
    |*PlainTextPassword*|설치하는 동안 만들어진 새 관리자 계정의 암호입니다.<br /><br /> -길이가 8 자 이상 이어야 합니다.<br /><br /> -다음 네 가지 범주 중 세 가지 이상을 포함 해야 합니다.<br /><br /> -대문자 문자.<br /><br /> -소문자 문자.<br /><br /> 번호.<br /><br /> 기호만.|  
    |*StdUserName*|설치하는 동안 만들어진 새 표준 사용자 계정의 이름입니다. 요구 사항에 대해서는 *UserName* 매개 변수를 참조하세요.|  
    |*StdUserPlainTextPassword*|설치하는 동안 만들어진 표준 사용자 계정의 암호입니다.|  
    |WebDomainName|(선택 사항) 서버의 인터넷 도메인 이름을 구성합니다. 이 파일을 통해 도메인 이름 설정 마법사의 수동 구성에서 사용한 것과 유사한 방식의 도메인 이름을 구성할 수 있습니다.|  
    |TrustedCertFileName|(선택 사항) 도메인 이름에 대한 신뢰할 수 있는 인증서를 구성합니다. 프라이빗 키를 포함하는 .PFX 인증서를 구성할 수 있습니다.|  
    |TrustedCertPassword|(선택 사항) .PFX를 가져오기 위한 암호입니다.|  
    |EnableVPN|(선택 사항) 기본적으로 VPN을 켭니다.|  
    |VpnIPv4StartAddress|(선택 사항) VPN 시작 주소를 설정합니다.|  
    |VpnIPv4EndAddress|(선택 사항) VPN 끝 주소를 설정합니다.|  
    |VpnBaseIPv6Address|(선택 사항) VPN에 대한 기본 IPV6 주소를 설정합니다.|  
    |VpnIPv6PrefixLength|(선택 사항) VPN IPv6 주소의 접두사 길이를 설정합니다.|  
    |IsHosted|(선택 사항) 지정하지 않으면 기본 값은 false입니다. 호스팅 서비스 공급자 환경에서 설정하는 경우 이 값을 설정합니다. 라우터 구성이 비활성화됩니다.|  
    |StaticIPv4Address|(선택 사항) 동적 주소 대신 고정 IP 주소를 할당하려면 고정 IP 주소를 지정합니다.|  
    |StaticIPv4Gateway|(선택 사항) 동적 주소 대신 고정 IP 주소를 할당하려면 기본 게이트웨이 주소를 지정합니다.|  
    |StaticIPv4SubnetMask|(선택 사항) 동적 주소 대신 고정 IP 주소를 구성하려면 서브넷 마스크를 지정합니다.|  
    |StaticIPv6Address|(선택 사항) 동적 주소 대신 고정 IP 주소를 할당하려면 기본 IP 주소를 지정합니다.|  
    |StaticIPv6SubnetPrefixLength|(선택 사항) 동적 IP 주소 대신 고정 IP 주소를 구성하려면 기본 IPV6 서브넷 접두사 길이를 지정합니다.|  
    |StaticIPv6Gateway|(선택 사항) 동적 IP 주소 대신 고정 IP 주소를 구성하려면 기본 게이트웨이 주소를 지정합니다.|  
    |ClientBackupOn|(선택 사항) 새로운 클라이언트가 서버에 참가할 때 기본적으로 클라이언트 백업을 끕니다.|  
    |FileHistoryOn|(선택 사항) Windows 8 Consumer Preview를 사용하는 새로운 클라이언트가 서버에 참가할 때 기본적으로 파일 기록 백업을 끕니다.|  
    |EnableRWA|Windows Server Essentials를 설치할 때 원격 웹 액세스를 사용 하도록 설정 하지만 라우터 구성을 건너뜁니다. 제품을 새로 설치하는 경우에만 지원됩니다. 기본값은 False입니다.|  
    |IPv4DNSForwarder|IPv4 DNS 전달자를 설정합니다.|  
    |IPv6DNSForwarder|IPv6 DNS 전달자를 설정합니다.|  
    |LaunchPadHiddenTasks|-(선택 사항) 실행 패드에서 백업 항목 또는/및 관리 대시보드 항목을 숨길 수 있습니다.<br /><br /> -대시보드를 사용 하지 않도록 설정 하려면: LaunchPadHiddenTasks = Microsoft 실행 패드.<br /><br /> -백업을 사용 하지 않도록 설정 하려면: LaunchPadHiddenTasks = Microsoft 실행 패드. 백업<br /><br /> -백업 및 대시보드를 모두 사용 하지 않도록 설정 하려면: LaunchPadHiddenTasks = Microsoft 실행 패드.|  
  
3.  파일을 저장합니다. cfg.ini.txt가 아닌 cfg.ini로 파일을 저장해야 합니다.  
  
    > [!NOTE]
    >  cfg.ini 파일은 특정 설치 단계에 사용할 수 있는 USB 플래시 드라이브나 대상 서버의 하드 드라이브 루트에 저장할 수 있습니다. 파일 인코딩은 ANSI 또는 유니코드로 설정해야 합니다. UTF-8 인코딩은 지원되지 않습니다.  
  
> [!IMPORTANT]
>  cfg.ini의 초기 구성 섹션은 서버를 개인화하거나 파트너에서 무인 응답 파일을 사용하여 서버의 사용자 환경을 테스트하려는 경우에만 최종 사용자가 사용해야 합니다. 파일의 이 섹션은 이미지를 만들기 위한 것이 아닙니다.  
  
## <a name="see-also"></a>참고 항목  

 [Windows Server Essentials ADK 시작 하기](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [이미지 만들기 및 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포를 위한 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)

