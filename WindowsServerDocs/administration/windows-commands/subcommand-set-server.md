---
title: 하위 명령 서버 설정
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da55c29d-a94a-4d73-877b-af480f906ca0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: abc3fe23558f077e0ba9ac69f2641e3b8c9cde4f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858384"
---
# <a name="subcommand-set-server"></a>하위 명령: 서버 설정

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 배포 서비스 서버에 대 한 설정을 구성합니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /Set-Server [/Server:<Server name>]
    [/Authorize:{Yes | No}]
    [/RogueDetection:{Yes | No}]
    [/AnswerClients:{All | Known | None}]
    [/Responsedelay:<time in seconds>]
    [/AllowN12forNewClients:{Yes | No}]
    [/ArchitectureDiscovery:{Yes | No}]
    [/resetBootProgram:{Yes | No}]
    [/DefaultX86X64Imagetype:{x86 | x64 | Both}]
    [/UseDhcpPorts:{Yes | No}]
    [/DhcpOption60:{Yes | No}]
    [/RpcPort:<Port number>]
    [/PxepromptPolicy 
        [/Known:{OptIn | Noprompt | OptOut}]
        [/New:{OptIn | Noprompt | OptOut}] 
    [/BootProgram:<Relative path>]
         /Architecture:{x86 | ia64 | x64}
    [/N12BootProgram:<Relative path>]
         /Architecture:{x86 | ia64 | x64}
    [/BootImage:<Relative path>]
         /Architecture:{x86 | ia64 | x64}
    [/PreferredDC:<DC Name>]
    [/PreferredGC:<GC Name>]
    [/PrestageUsingMAC:{Yes | No}]
    [/NewMachineNamingPolicy:<Policy>]
    [/NewMachineOU]
         [/type:{Serverdomain | Userdomain | UserOU | Custom}]
         [/OU:<Domain name of OU>]
    [/DomainSearchOrder:{GCOnly | DCFirst}]
    [/NewMachineDomainJoin:{Yes | No}]
    [/OSCMenuName:<Name>]
    [/WdsClientLogging]
         [/Enabled:{Yes | No}]
         [/LoggingLevel:{None | Errors | Warnings | Info}]
    [/WdsUnattend]
         [/Policy:{Enabled | Disabled}]
         [/CommandlinePrecedence:{Yes | No}]
         [/File:<path>]
             /Architecture:{x86 | ia64 | x64}
    [/AutoaddPolicy]
         [/Policy:{AdminApproval | Disabled}]
         [/PollInterval:{time in seconds}]
         [/MaxRetry:{Retries}]
         [/Message:<Message>]
         [/RetentionPeriod]
             [/Approved:<time in days>]
             [/Others:<time in days>]
    [/AutoaddSettings]
         /Architecture:{x86 | ia64 | x64}
         [/BootProgram:<Relative path>]
         [/ReferralServer:<Server name>
         [/WdsClientUnattend:<Relative path>]
         [/BootImage:<Relative path>]
         [/User:<Owner>]
         [/JoinRights:{JoinOnly | Full}]
         [/JoinDomain:{Yes | No}]
    [/BindPolicy]
         [/Policy:{Include | Exclude}]
         [/add]
              /address:<IP or MAC address>
              /addresstype:{IP | MAC}
         [/remove]
              /address:<IP or MAC address>
              /addresstype:{IP | MAC}
    [/RefreshPeriod:<time in seconds>]
    [/BannedGuidPolicy]
         [/add]
              /Guid:<GUID>
         [/remove]
             /Guid:<GUID>
    [/BcdRefreshPolicy]
         [/Enabled:{Yes | No}]
         [/RefreshPeriod:<time in minutes>]
    [/Transport]
         [/ObtainIpv4From:{Dhcp | Range}]
             [/start:<start IP address>]
             [/End:<End IP address>]
         [/ObtainIpv6From:Range]
             [/start:<start IP address>]
             [/End:<End IP address>]
         [/startPort:<start Port>
             [/EndPort:<start Port>
        [/Profile:{10Mbps | 100Mbps | 1Gbps | Custom}]
        [/MulticastSessionPolicy]
             [/Policy:{None | AutoDisconnect | Multistream}]
                 [/Threshold:<Speed in KBps>]
                 [/StreamCount:{2 | 3}]
                 [/Fallback:{Yes | No}]    
        [/forceNative]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
|[/ 권한 부여: {예 & #124; No}]|이 서버에서 제어 프로토콜 DHCP (Dynamic Host) 권한을 부여 것인지 지정 합니다.|
|[/ RogueDetection: {예 & #124; No}]|DHCP rogue 검색을 사용 하지 않도록 설정 하거나 사용 합니다.|
|[/ AnswerClients: {모든 & #124; 알려진 & #124; 없음}]|이 서버에 응답 하는 클라이언트를 지정 합니다. 이 값을 설정 하는 경우 **알려진**, active directory Domain Services (AD DS)에서 컴퓨터를 준비 해야 Windows 배포 서비스 서버에 의해 자세할수록 전에 합니다.|
|[/Responsedelay:<time in seconds>]|부팅 클라이언트에 응답 하기 전에 서버 대기 시간의 양입니다. 이 설정은 사전 준비 된 컴퓨터에 적용 되지 않습니다.|
|[/ AllowN12forNewClients: {예 &#124; No}]|Windows Server 2008에 대 한 알 수 없는 클라이언트는 네트워크 부팅을 시작 하려면 F12 키를 눌러 필요가 없음을 지정 합니다. 클라이언트 컴퓨터에 대해 지정 된 부팅 프로그램 수신 하거나 지정 하지 않으면 부팅 프로그램에 대해 지정 된 알려진 아키텍처입니다.<br /><br />Windows Server 2008 R2에서는 다음 명령을 사용 하 여이 옵션 대체 되었습니다: wdsutil /Set-Server /PxepromptPolicy /New:Noprompt|
|[/ ArchitectureDiscovery: {예 & #124; No}]|아키텍처 검색을 사용 하지 않도록 설정 하거나 사용 합니다. 이 아키텍처를 올바르게 브로드캐스팅하지 않도록 하는 x64 기반 클라이언트의 검색을 용이해 집니다.|
|[/ resetBootProgram: {예 &#124; No}]|F12 키 누름을 요구 하지 않고 부팅에 클라이언트에 대 한 부팅 경로 지워지는지 여부를 결정 합니다.|
|[/ DefaultX86X64Imagetype: {x86 &#124; x64 &#124; 둘 다}]|부팅 이미지는 컨트롤은 x64 기반 클라이언트에 표시 됩니다.|
|[/ UseDhcpPorts: {예 & #124; No}]|지정 TCP 포트 67 여부 PXE 서버는 DHCP 포트에 바인딩하지 하려고 해야 합니다. 이 옵션을 설정 해야 DHCP 및 Windows 배포 서비스는 동일한 컴퓨터에서 실행 중인 경우 **No** 해당 포트를 사용 하 고 설정 하도록 DHCP 서버를 사용 하도록 설정 하는 **/DhcpOption60** 매개 변수를 **예**합니다. 기본 설정은이 값은 **예**합니다.|
|[/ DhcpOption60: {예 & #124; No}]|PXE를 지원 하는지 DHCP 옵션 60 구성 해야 하는지 여부를 지정 합니다. DHCP 및 Windows 배포 서비스는 동일한 서버에서 실행 중인 경우이 옵션을 설정 **예** 설정 하 고는 **/UseDhcpPorts** 옵션을 **No**합니다. 기본 설정은이 값은 **No**합니다.|
|[/ RpcPort:<Port number>]|클라이언트 요청을 처리 하는 데 사용할 TCP 포트 번호를 지정 합니다.|
|[/PxepromptPolicy]|구성 방법을 알려진 (준비) 새 클라이언트가 PXE 부팅을 시작 합니다. 이 옵션은 Windows Server 2008 r 2에만 적용 됩니다. 다음 옵션을 사용 하는 설정 설정:<br /><br />-[/ 알려진: {OptIn&#124;OptOut&#124;Noprompt}]-사전 준비 된 클라이언트 정책을 가져오거나 설정 합니다.<br />-[/ 새로 만들기: {OptIn&#124;OptOut&#124;Noprompt}]-새 클라이언트 정책을 가져오거나 설정 합니다.<br /><br />**OptIn** 클라이언트가 PXE 부팅 하려면에서 아무 키나 해야 하는 방법, 그렇지 않으면 대체 됩니다 다음 부팅 장치에 있습니다.<br /><br />**Noprompt** 클라이언트는 항상 PXE 부팅을 의미 합니다.<br /><br />**OptOut** 클라이언트 Esc 키를 누르면 하지 않으면 PXE 부팅을는 것을 의미 합니다.|
|[/ BootProgram:<Relative path>] / 아키텍처: {x86 & #124 ia64 & #124; x64}|부팅 프로그램에 상대 경로 remoteInstall 폴더에서 지정 (예를 들어 **boot\x86\pxeboot.n12**), 부팅 프로그램의 아키텍처를 지정 합니다.|
|[/ N12BootProgram:<Relative path>] / 아키텍처: {x86 & #124 ia64 & #124; x64}|F12 키를 눌러 필요 하지 않은 부팅 프로그램에 상대 경로 지정 합니다 (예를 들어 **boot\x86\pxeboot.n12**), 부팅 프로그램의 아키텍처를 지정 하 고 있습니다.|
|[/ 부트 이미지:<Relative path>] / 아키텍처: {x86 & #124 ia64 & #124; x64}|부팅 클라이언트 수신 해야 및 부팅 이미지의 아키텍처를 지정 하는 부팅 이미지에 상대 경로 지정 합니다. 각 아키텍처에 대해 다음과 같이 지정할 수 있습니다.|
|[/ PreferredDC:<DC Name>]|Windows 배포 서비스를 사용 해야 하는 도메인 컨트롤러의 이름을 지정 합니다. 이 NetBIOS 이름 또는 FQDN 수 있습니다.|
|[/ PreferredGC:<GC Name>]|Windows 배포 서비스를 사용 해야 하는 글로벌 카탈로그 서버의 이름을 지정 합니다. 이 NetBIOS 이름 또는 FQDN 수 있습니다.|
|[/ PrestageUsingMAC: {예 & #124; No}]|Windows 배포 서비스를 AD DS에서 컴퓨터 계정을 만들 때 GUID/UUID 보다는 MAC 주소 컴퓨터를 식별 하려면 사용 여부를 지정 합니다.|
|[/ NewMachineNamingPolicy:<Policy>]|클라이언트 컴퓨터 이름을 생성할 때 사용할 형식을 지정 합니다. 에 사용할 형식에 대 한 자세한 <policy>mmc 스냅인에서 서버를 마우스 오른쪽 단추로 클릭, 클릭 **속성**, 및 보기를 **directory Services** 탭 합니다. 예를 들어 **/NewMachineNamingPolicy: %61Username % #** 합니다.|
|[/NewMachineOU]|클라이언트 컴퓨터 계정을 만들어지는 AD DS의 위치를 지정 하는 데 사용 합니다. 다음 옵션을 사용 하 여 위치를 지정 합니다.<br /><br />-   [/type: Serverdomain &#124; Userdomain &#124; UserOU &#124; 사용자 지정] 위치 유형을 지정 합니다. **Serverdomain** Windows 배포 서비스 서버와 동일한 도메인 계정을 만듭니다. **Userdomain** 설치를 수행 하는 사용자와 동일한 도메인 계정을 만듭니다. **UserOU** 설치를 수행 하는 사용자의 조직 구성 단위에서 계정을 만듭니다. **사용자 지정** 사용자 지정 위치를 지정할 수 있습니다 (에 대 한 값을 지정 해야 **/OU** 이 옵션 사용).<br />-[/ OU:<Domain name of OU>]-지정 된 경우 **사용자 지정** 에 대 한 합니다 **입력/** 옵션을이 옵션 컴퓨터 계정을 만들어야 하는 조직 구성 단위를 지정 합니다.|
|[/ DomainSearchOrder: {GCOnly & #124; DCFirst}]|AD DS (글로벌 카탈로그 또는 도메인 컨트롤러)에 컴퓨터 계정을 검색 하는 것에 대 한 정책을 지정 합니다.|
|[/ NewMachineDomainJoin: {예 & #124; No}]|이미 AD DS에서 사전 준비 되지 않은 컴퓨터를 설치 하는 동안 도메인에 가입 해야 여부를 지정 합니다. 기본 설정은 **예**합니다.|
|[/WdsClientLogging]|서버에 대 한 로깅 수준을 지정합니다.<br /><br />-[/ 활성화: {예 & #124; 아니오}]-사용 하거나 Windows 배포 서비스 클라이언트 작업의 로깅을 사용 하지 않도록 설정 합니다.<br />-[/ LoggingLevel: {None & #124; 오류 및 #124; 경고 및 #124; 정보}-로깅 수준을 설정 합니다. **None** 로깅을 사용 하지 않도록 설정 하는 것과 같습니다. **오류** 는 가장 낮은 수준의 로깅 및 오류만 기록 됩니다 있는지를 나타냅니다. **경고** 경고 및 오류를 모두 포함 됩니다. **정보** 는 가장 높은 수준의 로깅 및 오류, 경고 및 정보 이벤트를 포함 합니다.|
|[/WdsUnattend]|이러한 설정은 Windows 배포 서비스 클라이언트의 무인된 설치 동작을 제어합니다. 다음 옵션을 사용 하는 설정 설정:<br /><br />-[/ 정책: {사용 (& a) #124; 사용 안 함}]-무인된 설치 사용 되는지 여부를 지정 합니다.<br />-[/ CommandlinePrecedence: {예 & #124; 아니오}]-는 Autounattend.xml 파일 (있는 경우 클라이언트에서) 또는 /Unattend 옵션을 사용 하 여 Windows 배포 서비스 클라이언트에 직접 전달 된 무인된 설치 파일을 사용할지 여부를 이미지 무인 파일 대신 클라이언트 설치 중 지정 합니다. 기본 설정은 **No**합니다.<br />-[/ 파일:<Relative path> /Architecture: {x86 & #124 ia64 & #124; x64}]-파일 이름, 경로 및 무인 파일의 아키텍처를 지정 합니다.|
|[/AutoaddPolicy]|이러한 설정은 자동 추가 정책을 제어합니다. 다음 옵션을 사용 하 여 설정을 정의할 수 있습니다.<br /><br />-[/ 정책: {AdminApproval & #124; 사용 안 함}]- **AdminApprove** 모든 알 수 없는 컴퓨터가 여기서 관리자 다음 컴퓨터의 목록을 검토 하 고 승인 또는 거부할 수 적절 하 게 각 요청을 보류 중인 큐에 추가할 수 있습니다. **비활성화 된** 알 수 없는 컴퓨터가 서버에 부팅 하려고 할 때 없는 다른 작업은 실행을 나타냅니다.<br />-[/ PollInterval: {time (초)에서}]-폴링하는 간격을 초 단위로 네트워크 부팅 프로그램은 Windows 배포 서비스 서버를 지정 합니다.<br />-[/ MaxRetry: <Number>]-네트워크 부팅 프로그램 Windows 배포 서비스 서버를 폴링하는 횟수를 지정 합니다. 이 값을 함께 **/PollInterval**, 를 승인 하거나 시간이 초과 되기 전에 컴퓨터를 거부 하려면 관리자에 대 한 네트워크 부팅 프로그램은 대기 하는 기간을 지정 합니다. 예를 들어 한 MaxRetry 값 10 및 **PollInterval** 60 vlue는 클라이언트는 폴링해야 서버 10 번 시도 사이의 60 초 대기 나타냅니다. 따라서 클라이언트는 10 분 (10 x 60 초 = 10 분) 후 시간 초과 합니다.<br />-[/ 메시지: <Message>]-클라이언트 네트워크 부팅 프로그램 대화 상자 페이지에 표시 되는 메시지를 지정 합니다.<br />-[/RetentionPeriod]-컴퓨터는 자동으로 제거 하기 전에 보류 중 상태로 있을 수 일 수를 지정 합니다.<br />-[승인 /: <time in days>]-승인 된 컴퓨터에 대 한 보존 기간을 지정 합니다. 이 매개 변수를 사용 해야는 **/RetentionPeriod** 옵션입니다.<br />-[/ 다른: <time in days>]-승인 되지 않은 컴퓨터에 대 한 보존 기간 (거부 또는 보류 중). 이 매개 변수를 사용 해야는 **/RetentionPeriod** 옵션입니다.|
|[/AutoaddSettings]|각 컴퓨터에 적용할 기본 설정을 지정 합니다. 다음 옵션을 사용 하 여 설정을 정의할 수 있습니다.<br /><br />-/Architecture: {x86 & #124 ia64 & #124; x64}-아키텍처를 지정 합니다.<br />-[/ BootProgram: <Relative path>]-승인 된 컴퓨터에 전송 부팅 프로그램을 지정 합니다. 부팅 프로그램을 지정 하는 경우 (지정 된 대로 서버)는 컴퓨터의 아키텍처에 대 한 기본 사용 됩니다.<br />-[/ WdsClientUnattend: <Relative path>]-승인 된 클라이언트가 수신 해야 하는 무인 파일에 대 한 상대 경로 설정 합니다.<br />-[/ ReferralServer: <Server name>]-이미지를 다운로드 하려면 클라이언트에서 사용 되는 Windows 배포 서비스 서버를 지정 합니다.<br />-[/ 부트 이미지: <Relative path>]-승인 된 클라이언트가 받을 부팅 이미지를 지정 합니다.<br />-[/ 사용자: < 도메인 \ 사용자 &#124; User@Domain>]-지정 된 사용자에 게 컴퓨터를 도메인에 가입 하는 데 필요한 권한을 제공 컴퓨터 계정 개체에 사용 권한을 설정 합니다.<br />-[JoinRights: {JoinOnly & #124; 전체}]-사용자에 게 할당할 권한의 유형을 지정 합니다. **JoinOnly** 는 관리자가 사용자 수를 도메인에 컴퓨터를 가입 하기 전에 컴퓨터 계정 다시 설정 해야 합니다. **전체** 를 포함 하 여 컴퓨터를 도메인에 가입 하는 사용자에 대 한 모든 권한을 제공 합니다.<br />-[/ JoinDomain: {예 & #124; 아니오}]-컴퓨터가 Windows 배포 서비스를 설치 하는 동안이 컴퓨터 계정으로 도메인에 가입 되어야 해야 여부를 지정 합니다. 기본 설정은 **예**합니다.|
|[/BindPolicy]|네트워크 인터페이스에서 수신 대기 하도록 PXE 공급자를 구성 합니다. 다음 옵션을 사용 하 여 정책을 정의 합니다.<br /><br />-[/ 정책: {포함 (& a) #124; 제외}]-포함 하거나 제외할 인터페이스 목록에 있는 주소 인터페이스 바인딩 정책을 가져오거나 설정 합니다.<br />-[/ [추가]-목록에 인터페이스를 추가 합니다. /Addresstype 및/주소 지정 해야 합니다.<br />-[/remove]-목록에서 인터페이스를 제거합니다. /Addresstype 및/주소 지정 해야 합니다.<br />-/ 주소:<IP or MAC address> -추가 또는 제거 하는 인터페이스의 IP 또는 MAC 주소를 지정 합니다.<br />-/addresstype: {IP &#124; MAC}-에 지정 된 주소 유형을 나타냅니다는 **주소** 옵션입니다.|
|[/ RefreshPeriod: <seconds>]|Server는 해당 설정을 새로 고칩니다 빈도 (초)을 지정 합니다.|
|[/BannedGuidPolicy]|다음 옵션을 사용 하 여 차단 된 Guid의 목록을 관리 합니다.<br /><br />-[/ [추가] /Guid:<GUID> -금지 된 Guid의 목록에 지정 된 GUID를 추가 합니다. 이 GUID 사용 하 여 모든 클라이언트를 MAC 주소 대신 식별 됩니다.<br />-[/remove] /Guid:<GUID> -금지 된 Guid의 목록에서 지정된 된 GUID를 제거 합니다.|
|[/BcdRefreshPolicy]|다음 옵션을 사용 하 여 Bcd 파일을 새로 고침에 대 한 설정을 구성 합니다.<br /><br />-[/ 활성화: {예 &#124; No}]-정책 새로 고침 Bcd를 지정 합니다. 때 **/을 사용 하도록** 로 설정 된 **예**, Bcd 파일 지정 된 시간 간격으로 새로 고쳐집니다.<br />-[/ RefreshPeriod:<time in minutes>]-파일이 새로 고쳐질는 Bcd에 시간 간격을 지정 합니다.|
|[/Transport]|다음 옵션을 구성합니다.<br /><br /><ul><li>[/ ObtainIpv4From: {Dhcp & #124; 범위}]-IPv4 주소의 원본을 지정 합니다.<br /><br /><ul><li>[/ 시작: <starting Ipv4 address>]-IP 주소 범위의 시작을 지정 합니다. 이 옵션은 필요한 경우에 유효한 **/ObtainIpv4From** 로 설정 된 **범위**</li><li>[/ 끝: <Ending Ipv4 address>] -IP 주소 범위의 끝을 지정 합니다. 이 옵션은 필요 하 고 유효한 경우에만 **/ObtainIpv4From** 로 설정 된 **범위**합니다.</li></ul></li><li>[/ ObtainIpv6From:Range] [/ 시작:<start IP address>] [/ 끝:<End IP address>] 소스 IPv6 주소를 지정 합니다. 이 옵션 Windows Server 2008 r 2에만 적용 하 고 지원 되는 유일한 값은 범위입니다.</li><li>[/ startPort: <starting port>]-포트 범위의 시작을 지정 합니다.</li><li>[/ EndPort: <Ending port>] -포트 범위의 끝을 지정합니다.</li><li>[/ 프로필: {10Mbps (& a) #124; 100Mbps & #124; 1Gbps & #124; 사용자 지정}]-사용할 네트워크 프로필을 지정 합니다. 이 옵션은 지원 되는 forservers만 Windows Server 2008을 실행 합니다.</li><li>[/MulticastSessionPolicy]  멀티 캐스트 전송에 대 한 전송 설정을 구성합니다. 이 명령은 Windows Server 2008 r 2만 있습니다.<br /><br /><ul><li>[/ 정책: {None & #124; 자동 연결 끊기 & #124; Multistream}]-느린 클라이언트를 처리 하는 방법을 결정 합니다. 없음 같은 속도로 한 세션에서 모든 클라이언트를 유지 하는 의미 합니다. 자동 연결 끊기 지정 된 /Threshold 아래를 삭제 하는 모든 클라이언트 연결이 끊어집니다을 의미 합니다. Multistream은 클라이언트 나뉩니다 /StreamCount에 지정 된 대로 여러 세션을 의미 합니다.</li><li>[/ 임계값:<Speed in KBps>]-/Policy:AutoDisconnect, 최소 전송 속도 kbps 단위로이 옵션 집합에 대 한 합니다. 이 속도 아래로 떨어지면 하는 클라이언트에서 멀티 캐스트 전송을 끊어집니다.</li><li>[/ StreamCount: {2 &#124; 3}] [/ 대체 (fallback): {예 &#124; No}]-이 옵션을 multistream에 대 한 세션의 수를 결정 합니다. 2는 두 개의 세션 (고속 및 저속) 3 이면 3 개의 세션 느린, 중간, fast ()을 의미합니다.</li><li>[/ 대체 (fallback): {예 & #124; 아니오}]-연결이 끊어진 클라이언트는 (클라이언트에서 지 원하는) 경우에 다른 메서드를 사용 하 여 전송을 계속할지 여부를 결정 합니다. WDS 클라이언트를 사용 하는 경우 컴퓨터의 유니캐스트 대체를 않습니다. Wdsmcast.exe 대체 메커니즘을 지원 하지 않습니다. 이 옵션은 Multistream를 지원 하지 않는 클라이언트에도 적용 됩니다. 이 경우 컴퓨터는 느린 전송 세션으로 이동 하는 대신 다른 메서드로 다시 대체 됩니다.</li></ul></li></ul>|
## <a name="BKMK_examples"></a>예제
서버 응답 지연 시간을 4 분 알려진된 클라이언트만 응답 하도록 설정 하려면 다음을 입력 합니다.
```
wdsutil /Set-Server /AnswerClients:Known /Responsedelay:4
```
부팅 프로그램 및 아키텍처에 대 한 서버를 설정 하려면 다음을 입력 합니다.
```
wdsutil /Set-Server /BootProgram:boot\x86\pxeboot.n12 /Architecture:x86
```
서버 로그온을 사용 하려면 다음을 입력 합니다.
```
wdsutil /Set-Server /WdsClientLogging /Enabled:Yes /LoggingLevel:Warnings
```
사용 하도록 설정 하는 서버 뿐만 아니라 아키텍처와 클라이언트 무인 파일 형식에서 무인:
```
wdsutil /Set-Server /WdsUnattend /Policy:Enabled /File:WDSClientUnattend \unattend.xml /Architecture:x86
```
TCP 포트 67 및 60에 바인딩하려에 사전 부팅 실행 환경 (PXE) 서버를 설정 하려면 다음을 입력 합니다.
```
wdsutil /Set-server /UseDhcpPorts:No /DhcpOption60:Yes
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[는 서버 사용 안 함-명령을 사용 하 여](using-the-disable-server-command.md)
[사용 서버 명령을 사용 하 여](using-the-enable-server-command.md)
[get 서버 명령을 사용 하 여](using-the-get-server-command.md)
[Initialize 서버 명령을 사용 하 여](using-the-initialize-server-command.md)
[하위 명령: 서버 시작](subcommand-start-server.md)
[하위 명령: 서버 중지](subcommand-stop-server.md)
[초기화 서버 옵션](the-uninitialize-server-option.md)
