---
title: "Cfg.ini 파일 만들기"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 93a73556-22ef-402d-b8d4-582b74c22bcf
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 967db5f36ea27fb04eab9a6682a106ba0072d45d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="create-the-cfgini-file"></a>Cfg.ini 파일 만들기

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

다음과 같은 경우에는 운영 체제의 설치 자동화 cfg.ini 파일 사용 됩니다.  
  
-   대상 컴퓨터에 사전 설치 된 이미지 최종 사용자의 경험을 테스트 하는 경우 초기 구성 섹션 자동 또는 수동 모드에서 설치 과정을 안내 하는 데 사용 됩니다. 이 위해 표시 [초기 구성 섹션 만들기](Create-the-Cfg.ini-File.md#BKMK_CreateInit2)합니다.  
  
##  <a name="BKMK_CreateInit2"></a>초기 구성 섹션 만들기  
 Cfg.ini 파일 초기 구성 섹션을 사용 하 여 자동 또는 수동 모드에서 설치를 안내 합니다.  
  
#### <a name="to-define-the-initial-configuration-section"></a>초기 구성 섹션을 정의 하  
  
1.  있으면; 메모장에서 cfg.ini 파일 열기 그렇지 않으면 새 파일을 만듭니다.  
  
2.  InitialConfiguration 섹션을 만드는 다음 텍스트를 추가 합니다.  
  
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
    >  초기 구성 하는 동안 다른 언어를 선택 하는 옵션이 제공 되지 않습니다. 시스템을 다시 설정 운영 체제의 언어를 처음 설치할 됩니다.  
  
    |매개 이름|매개 설명|  
    |--------------------|---------------------------|  
    |*AcceptEula*|사용자가 Microsoft 소프트웨어 사용 조건 있는지를 나타냅니다. 참 또는 False는 값와 수 있지만 설치가 참으로 설정 되어 있는 경우에 진행 됩니다.|  
    |*AcceptOEMEula*|(선택 사항) 사용자가 파트너 사용권 계약에 동의 나타냅니다. 값 참 또는 False 가질 수 없습니다. 이 필드는 별도 사용권 계약을 제공 하는 파트너 로부터 서버를 구입한 경우에 필요 합니다.|  
    |*회사 이름*|(선택 사항) 회사의 이름입니다. 회사와 서버에 연결 하 고 사용자 지정 하는 회사 보고서 회사 이름을 사용 됩니다. 최대 254 자 사용할 수 있습니다.|  
    |*국가*|(선택 사항) 원하는 국가/지역 나타내는 문자열입니다. 예: 미국 미국입니다.|  
    |*서버 이름*|서버 이름 네트워크에서 서버를 고유 하 게 식별 합니다. 서버 이름은 다음 조건을 충족 해야 합니다.<br /><br /> -최대 15 개의 자 가능 합니다.<br /><br /> -문자, 숫자, 하이픈 (-)를 포함 수 있습니다.<br /><br /> -하이픈 시작 해야 합니다.<br /><br /> -공백 포함 되어 있지 해야 합니다.<br /><br /> -숫자를 포함 되어야 합니다.<br /><br /> 예: ContosoServer 합니다.|  
    |*DNSName*|내부 도메인 서버와 함께 사용자 이름, 암호 및 기타 일반적인 정보의 일반적인 데이터베이스를 공유 하는 클라이언트 컴퓨터를 그룹화 합니다. 사용자가 컴퓨터에 로그온 할 하지만 내부는 것 같지 않습니다 인터넷 도메인 이름으로 때이 이름이 표시 됩니다. 내부 도메인 이름에 대해 지정 동일한 조건을 충족 해야는 *서버 이름*합니다.<br /><br /> 예: contoso.local 합니다.|  
    |*NetbiosName*|NetBIOS 이름은 서버에서 실행 중인 리소스를 식별 하는 데 사용 됩니다. 최대 15 개의 자를 수 있습니다. 예: Contoso 합니다.|  
    |*언어*|(선택 사항) 표시 언어를 지정합니다. 설치 된 언어 중 하나 수만 있습니다. 예: en-미국에서 사용 되는 영어 해 주세요.|  
    |*로캘*|(선택 사항) 시간 및 통화 형식을 사용 하 여 지정는 *LocaleID* 형식 있습니다. 예: en-영어로 표시 하 고 미국에서 사용 되는 표준에 따라 포맷 통화 및 시간에 대 한 주세요.|  
    |*키보드*|키보드는 다음과 같은 두 가지 형식 될 수 있습니다.<br /><br /> - **입력된 언어: 자판 배열 합니다.** 예를 들어 0409:00000409 0409 나타나는 하기 전에 **:** 입력된 언어는 및 **00000409** 자판 배열을입니다. 레지스트리 키에서 자판 배열의 목록을 볼 수 있는 **HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Keyboard 레이아웃**합니다.<br /><br /> - **입력 언어: IME 식별자입니다.** 다음 IME 식별자의 전체 목록은입니다.<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1}{8F96574E-C86C-4bd6-9666-3F7327D4CBE8} 암하라어 입력 방법을<br /><br /> -{81d4e9c9-1d3b-41bc-9e6c-4b40bf79e35e}{FA550B04-5AD7-411F-A5AC-CA038EC515D7} Microsoft Pinyin-간단한 패스트 (중국어 간체)<br /><br /> {531FDEBF-9B4C-4A43-A2AA-960E8FCDC732}{B2F9C502-1742-11D4-9790-0080C882687E} 중국어 (번체)-새로운 표음 문자<br /><br /> {531FDEBF-9B4C-4A43-A2AA-960E8FCDC732}{4BDF9F03-C7D3-11D4-B2AB-0080C882687E} 중국어 (번체)-ChangJie<br /><br /> {531FDEBF-9B4C-4A43-A2AA-960E8FCDC732}{6024B45F-5C54-11D4-B921-0080C882687E} 중국어 (번체)-빠른<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1}{D38EFF65-AA46-4FD5-91A7-67845FB02F5B} 중국어 번체 배열<br /><br /> -중국어 번체 DaYi {E429B25A-E5D3-4D1F-9BE3-0C608477E3A1}{037B2C25-480C-4D7F-B027-D6CA6B69788A}<br /><br /> -{03B5835F-F03C-411B-9CE2-AA23E1171E36}{A76C93D9-5523-4E90-AAFA-4DB112F9AC76} Microsoft IME (일본)<br /><br /> -{A028AE76-01B1-46C2-99C4-ACD9858AE02F}{B5FE1F02-D5F2-4445-9C03-C568F23C99A1} Microsoft 한국어 IME<br /><br /> -{A1E2B86B-924A-4D43-80F6-8A820DF7190F}{B60AF051-257A-46BC-B9D3-84DAD819BAFB} 이전 한글 IME (한국어)<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1}{409C8376-007B-4357-AE8E-26316EE3FB0D}이 문자 입력 방법<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1}{3CAB88B7-CC3E-46A6-9765-B772AD7761FF} Tigrinya 입력 방법|  
    |*설정*|업데이트에 대 한 사용자가 선택한을 설정합니다. 값 다음 중 하나를 사용 합니다.<br /><br /> **-모두** 권장 설정 사용와 같습니다.<br /><br /> **-업데이트** 같음 중요 업데이트를 설치 합니다. 만<br /><br /> **-없음** 같음 업데이트 확인 하지 않습니다.|  
    |*사용자 이름*|-를 설치 하는 동안 만든 새 관리자 계정 이름입니다. 관리자와 표준 사용자 계정 이름을 다음 조건을 충족 해야 합니다.<br /><br /> -19 최대 자 가능 합니다.<br /><br /> -없습니다 / \ & #124; < > + =; , ? *<br /><br /> -시작 하거나 마침표 하지 해야 합니다.<br /><br /> -해야 마침표 두 가지입니다.<br /><br /> -서버 이름 또는 내부 도메인 이름와 동일 이어야 합니다.<br /><br /> -미리 정의 된 사용자 이름과 같은 관리자 또는 게스트 같은 이어야 합니다.|  
    |*PlainTextPassword*|설치 시 생성 되는 새 관리자 계정에 대 한 암호입니다.<br /><br /> -여야 8 이상 자 합니다.<br /><br /> -다음 네 가지 범주 중 최소 3 포함 해야 합니다.<br /><br /> -대문자 합니다.<br /><br /> -소문자 합니다.<br /><br /> -번호입니다.<br /><br /> -기호 합니다.|  
    |*StdUserName*|설치 시 생성 되는 새로운 표준 사용자 계정의 이름입니다. 참조는 *사용자 이름* 요구 사항에 대 한 매개 합니다.|  
    |*StdUserPlainTextPassword*|설치 시 생성 되는 표준 사용자 계정에 대 한 암호입니다.|  
    |WebDomainName|(선택 사항) 서버 도메인 이름 인터넷을 구성 합니다. 이 파일은 도메인 이름 설치 마법사에서 수동으로 구성 사용 하는 방법과 유사한 도메인 이름 구성할 수 있습니다.|  
    |TrustedCertFileName|(선택 사항) 도메인 이름에 대 한 신뢰할 수 있는 인증서를 구성 합니다. 이렇게 하면 이용할 수는 있습니다. PFX 인증서를 개인 키가 포함 되어 있습니다.|  
    |TrustedCertPassword|(선택 사항) 가져올에 대 한 암호는 합니다. PFX 합니다.|  
    |EnableVPN|(선택 사항) VPN 기본적으로 설정 합니다.|  
    |VpnIPv4StartAddress|(선택 사항) VPN 시작 주소를 설정 합니다.|  
    |VpnIPv4EndAddress|(선택 사항) VPN 종료 주소를 설정 합니다.|  
    |VpnBaseIPv6Address|(선택 사항) VPN에 대 한 기본 IPV6 주소를 설정 합니다.|  
    |VpnIPv6PrefixLength|(선택 사항) VPN IPv6 주소 접두사 길이 설정 합니다.|  
    |IsHosted|(선택 사항) 기본값은 false 지정 되지 않은 경우입니다. 이 값 호스팅 환경에서이를 설정한 경우 설정 합니다. 라우터 구성을 비활성화 합니다.|  
    |StaticIPv4Address|(선택 사항) 동적 주소 대신 고정 IP 주소를 구성 하 고 싶은 경우 고정 IP 주소를 지정 합니다.|  
    |StaticIPv4Gateway|(선택 사항) 동적 주소 대신 고정 IP 주소를 구성 하 고 싶은 경우 기본 게이트웨이 주소를 지정 합니다.|  
    |StaticIPv4SubnetMask|(선택 사항) 동적 주소 대신 고정 IP 주소를 구성 하 고 싶은 경우 서브넷 마스크를 지정 합니다.|  
    |StaticIPv6Address|(선택 사항) 동적 주소 대신 고정 IP 주소를 구성 하 고 싶은 경우 기본 IP 주소를 지정 합니다.|  
    |StaticIPv6SubnetPrefixLength|(선택 사항) 동적 주소 대신 고정 IP 주소를 구성 하 고 싶은 경우 기본 IPV6 서브넷 접두사 길이 지정 합니다.|  
    |StaticIPv6Gateway|(선택 사항) 동적 대신 고정 IP 주소를 구성 하 고 싶은 경우 기본 게이트웨이 주소를 지정 합니다.|  
    |ClientBackupOn|(선택 사항) 클라이언트 백업 기본적으로 해제 새로운 클라이언트는 서버 참가 합니다.|  
    |FileHistoryOn|(선택 사항) 파일 히스토리 백업 기본적으로 해제 Windows 8 Consumer Preview를 실행 하는 새로운 클라이언트는 서버에 연결 된 때 합니다.|  
    |EnableRWA|Windows Server Essentials를 설치할 때 원격 웹 액세스할 수 있게 됩니다 라우터 구성 건너뛸 수 있지만 합니다. 이 해당 제품의 새로 설치에만 지원 됩니다. 기본값은 false 합니다.|  
    |IPv4DNSForwarder|IPv4 DNS 전달자를 설정 합니다.|  
    |IPv6DNSForwarder|IPv6 DNS 전달자를 설정 합니다.|  
    |LaunchPadHiddenTasks|-(옵션) 백업 항목을 숨길 수 또는 / 실행 창에서 관리자 대시보드 입력 하 고 있습니다.<br /><br /> -대시보드 사용 하지 않도록 설정 하려면: LaunchPadHiddenTasks=Microsoft.LaunchPad.AdminDashboard<br /><br /> 백업 사용 안 함으로: LaunchPadHiddenTasks=Microsoft.LaunchPad.Backup<br /><br /> 백업 및 대시보드 사용 하지 않도록 설정으로: LaunchPadHiddenTasks=Microsoft.LaunchPad.Backup,Microsoft.LaunchPad.AdminDashboard|  
  
3.  파일을 저장 합니다. Cfg.ini, 하지 cfg.ini.txt으로 파일을 저장 하 고 있는지 확인 합니다.  
  
    > [!NOTE]
    >  특정 단계는 설치에 사용할 수 있는 USB 플래시 드라이브에 파일을 저장할 수 있습니다 또는 cfg.ini 파일 된 하드 드라이브 대상 서버의 루트 있을 수 있습니다. ANSI 또는 유니코드도 설정 된 파일에 대 한 인코딩, F-8 인코딩 지원 되지 확인 해야 합니다.  
  
> [!IMPORTANT]
>  Cfg.ini의 초기 구성 섹션 서버 개인 설정 하는 최종 사용자가 전화 걸기 또는 자리를 비운 사이 응답 파일을 사용 하 여 사용자 환경을 서버 테스트를 파트너에만 사용 해야 합니다. 파일의이 섹션은 이미지를 만들기 위한 사용할 수 없습니다.  
  
## <a name="see-also"></a>참조 하십시오  

 [Windows Server Essentials ADK 시작](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)

 [Windows Server Essentials ADK 시작](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [만들기 및 이미지를 사용자 지정](../install/Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](../install/Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](../install/Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](../install/Testing-the-Customer-Experience.md)

