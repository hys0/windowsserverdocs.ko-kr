---
title: Netsh 명령 구문, 컨텍스트 및 서식 지정
description: Netsh 컨텍스트와 하위 컨텍스트의 입력, netsh 구문 및 명령 서식 지정, 이해 하는 방법 및 Windows Server 2016 또는 Windows 10 실행 하는 로컬 및 원격 컴퓨터에서 netsh 명령을 실행 하는 방법에 알아보려면이 항목에서는 사용할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 8cb9b59f-0255-4261-b49a-562c5ea50ee0
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: adb77d841ba4d69b0d36bc7f19d4707638530c97
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823694"
---
# <a name="netsh-command-syntax-contexts-and-formatting"></a>Netsh 명령 구문, 컨텍스트 및 서식 지정

>적용 대상: Windows Server (반기 채널), Windows Server 2016

Netsh 컨텍스트와 하위 컨텍스트의 입력, netsh 구문 및 명령 서식 지정, 이해 하는 방법 및 로컬 및 원격 컴퓨터에서 netsh 명령을 실행 하는 방법에 알아보려면이 항목에서는 사용할 수 있습니다.

Netsh는 표시 하거나 현재 실행 중인 컴퓨터의 네트워크 구성을 수정할 수 있도록 명령줄 스크립팅 유틸리티입니다. Netsh 명령 프롬프트에서 netsh 명령을 입력 하 여 실행할 수 있습니다 및 배치 파일 또는 스크립트에서 사용할 수 있습니다. Netsh 명령을 사용 하 여 원격 컴퓨터와 로컬 컴퓨터를 구성할 수 있습니다.

또한 Netsh는 지정된 컴퓨터에 대해 배치 모드로 명령 그룹을 실행할 수 있게 해주는 스크립팅 기능을 제공합니다. Netsh를 사용하면 보관 목적으로 또는 다른 컴퓨터를 구성하는 데 유용하도록 구성 스크립트를 텍스트 파일로 저장할 수 있습니다.

## <a name="netsh-contexts"></a>Netsh 컨텍스트

Netsh 다른 운영 체제 구성 요소를 사용 하 여 동적와 상호 작용\-연결 라이브러리 \(DLL\) 파일입니다. 

각 netsh 도우미 DLL은 광범위 하 게 호출 하는 기능 집합을 제공 된 *상황에 맞는*, 네트워킹 서버 역할 또는 기능에 특정 명령 그룹에는 합니다. 이러한 컨텍스트는 구성을 제공 하 고 하나 이상의 서비스, 유틸리티 또는 프로토콜에 대 한 지원을 모니터링 하 여 netsh 기능을 확장 합니다. 예를 들어 Dhcpmon.dll netsh 된 컨텍스트 및 구성 하 고 DHCP 서버를 관리 하는 데 필요한 명령 집합을 제공 합니다.

### <a name="obtain-a-list-of-contexts"></a>컨텍스트 목록을 가져오려면

Windows Server 2016 또는 Windows 10을 실행 하는 컴퓨터에서 명령 프롬프트 또는 Windows PowerShell을 열어 netsh 컨텍스트의 목록을 얻을 수 있습니다. 명령을 입력 하 여 **netsh** ENTER 키를 누릅니다. 형식 **/?**, 한 다음 ENTER를 누릅니다.

다음은 Windows Server 2016 Datacenter를 실행 하는 컴퓨터에서 이러한 명령에 대 한 출력 예입니다.

    PS C:\Windows\system32> netsh
    netsh>/?
    
    The following commands are available:
    
    Commands in this context:
    ..            - Goes up one context level.
    ?             - Displays a list of commands.
    abort         - Discards changes made while in offline mode.
    add           - Adds a configuration entry to a list of entries.
    advfirewall   - Changes to the `netsh advfirewall' context.
    alias         - Adds an alias.
    branchcache   - Changes to the `netsh branchcache' context.
    bridge        - Changes to the `netsh bridge' context.
    bye           - Exits the program.
    commit        - Commits changes made while in offline mode.
    delete        - Deletes a configuration entry from a list of entries.
    dhcpclient    - Changes to the `netsh dhcpclient' context.
    dnsclient     - Changes to the `netsh dnsclient' context.
    dump          - Displays a configuration script.
    exec          - Runs a script file.
    exit          - Exits the program.
    firewall      - Changes to the `netsh firewall' context.
    help          - Displays a list of commands.
    http          - Changes to the `netsh http' context.
    interface     - Changes to the `netsh interface' context.
    ipsec         - Changes to the `netsh ipsec' context.
    ipsecdosprotection - Changes to the `netsh ipsecdosprotection' context.
    lan           - Changes to the `netsh lan' context.
    namespace     - Changes to the `netsh namespace' context.
    netio         - Changes to the `netsh netio' context.
    offline       - Sets the current mode to offline.
    online        - Sets the current mode to online.
    popd          - Pops a context from the stack.
    pushd         - Pushes current context on stack.
    quit          - Exits the program.
    ras           - Changes to the `netsh ras' context.
    rpc           - Changes to the `netsh rpc' context.
    set           - Updates configuration settings.
    show          - Displays information.
    trace         - Changes to the `netsh trace' context.
    unalias       - Deletes an alias.
    wfp           - Changes to the `netsh wfp' context.
    winhttp       - Changes to the `netsh winhttp' context.
    winsock       - Changes to the `netsh winsock' context.
    
    The following sub-contexts are available:
     advfirewall branchcache bridge dhcpclient dnsclient firewall http interface ipsec ipsecdosprotection lan namespace netio ras rpc trace wfp winhttp winsock
    
    To view help for a command, type the command, followed by a space, and then
     type ?.


### <a name="subcontexts"></a>하위 컨텍스트

Netsh 컨텍스트 명령과 라는 추가 컨텍스트를 모두 포함할 수 있습니다 *하위 컨텍스트의*합니다. 예를 들어 라우팅 컨텍스트 내에서 IP 및 IPv6 하위 컨텍스트를 변경할 수 있습니다.

명령 및 netsh 프롬프트의 컨텍스트 내에서 사용할 수 있는 하위 컨텍스트의 목록을 표시 하려면 상황에 맞는 이름을 입력 하 고 다음 중 하나를 입력 **/?** 또는 **도움말**합니다. 예를 들어, netsh 프롬프트 라우팅 컨텍스트에서 컨텍스트와 사용할 수 있는 명령의 목록을 표시 하려면 \(이므로 **netsh&gt;**\), 다음 중 하나를 입력 합니다.

**routing /?**

**라우팅 도움말**

현재 컨텍스트에서를 변경 하지 않고 다른 컨텍스트에서 작업을 수행 하려면 명령 프롬프트에서 netsh 사용 하려면 상황에 맞는 경로 입력 합니다. 예를 들어, IGMP 컨텍스트에 netsh 프롬프트에서 첫 번째 변경 하지 않고 IGMP 컨텍스트에서 "Local Area Connection" 이라는 인터페이스를 추가 하려면 다음을 입력 합니다.

**인터페이스 "Local Area Connection" startupqueryinterval 추가 ip igmp 라우팅 = 21**

## <a name="running-netsh-commands"></a>Netsh 명령을 실행합니다.

Netsh 명령을 실행 하려면 시작 해야 netsh 명령 프롬프트에서를 입력 하 여 **netsh** 한 다음 ENTER 키를 눌러 합니다. 다음으로, 사용 하려는 명령을 포함 하는 컨텍스트를 변경할 수 있습니다. 사용할 수 있는 컨텍스트는 설치 된 네트워킹 구성 요소에 따라 달라 집니다. 예를 들어 입력할 **dhcp** netsh 프롬프트에서 ENTER 키를 눌러 netsh DHCP 서버 컨텍스트를 변경 합니다. 설치 하는 DHCP가 없는 단, 다음과 같은 메시지가 나타납니다.

**다음 명령을 찾을 수 없습니다: dhcp 합니다.**

## <a name="formatting-legend"></a>범례를 서식 지정

해석 하 고 netsh 프롬프트 또는 배치 파일 또는 스크립트에서 명령을 실행 하는 경우 올바른 netsh 명령 구문을 사용 하 여 다음 서식 범례를 사용할 수 있습니다.

- 텍스트 *기울임꼴* 명령을 입력 하는 동안 제공 해야 하는 정보입니다. 예를 들어, 명령에-라는 매개 변수*UserName*, 실제 사용자 이름을 입력 해야 합니다.
- 텍스트 **굵게** 명령을 입력 하는 동안 표시 된 대로 정확히 입력 해야 하는 정보입니다.
- 텍스트 뒤에 줄임표가 \(... \) 명령줄에서 여러 번 반복 될 수 있는 매개 변수입니다.
- 대괄호 사이 있는 텍스트 [&nbsp;] 선택적 항목입니다.
- 중괄호 사이 있는 텍스트 {&nbsp;} 파이프로 구분 하는 옵션과 함께 선택할 수 있는 하나를 선택 해야만,와 같은 집합을 제공 `{enable|disable}`합니다.
- Courier 글꼴로 서식이 지정 된 텍스트에는 코드나 프로그램 출력 됩니다.

## <a name="running-netsh-commands-from-the-command-prompt-or-windows-powershell"></a>Windows PowerShell 명령 프롬프트에서 Netsh 명령 실행

네트워크 셸 시작 Windows PowerShell 또는 명령 프롬프트에서 netsh를 입력 하 고에 다음 명령을 사용할 수 있습니다.

### <a name="netsh"></a>netsh

Netsh는 로컬 또는 원격으로 표시 하거나 현재 실행 중인 컴퓨터의 네트워크 구성을 수정할 수 있도록 명령줄 스크립팅 유틸리티입니다. 매개 변수 없이 사용 **netsh** Netsh.exe 명령 프롬프트가 열립니다 \(이므로 **netsh&gt;**\)합니다.

#### <a name="syntax"></a>구문

**netsh** \[ **-**&nbsp;*AliasFile* \] \[ **-c** &nbsp;  *상황에 맞는* \] \[ **-r**&nbsp;*RemoteComputer* \] \[ **-u** \[ *DomainName\\*  \] *UserName* \] \[ **-p** &nbsp; *암호*  |  \* \] \[{*NetshCommand* | **-f** &nbsp; *ScriptFile*}\]

#### <a name="parameters"></a>매개 변수

**`-a`**

(선택 사항) 에 반환 되도록 지정 합니다 **netsh** 실행 한 후 프롬프트 *AliasFile*합니다.

**`AliasFile`**

(선택 사항) 하나 이상의 포함 된 텍스트 파일의 이름을 지정 **netsh** 명령입니다.

**`-c`**

(선택 사항) Netsh는 지정 된 입력을 지정 **netsh** 컨텍스트.

**`Context`**

(선택 사항) 지정 된 **netsh** 입력 하려는 컨텍스트. 

**`-r`**

(선택 사항) 원격 컴퓨터에서 실행할 명령을 지정 합니다.

>[!IMPORTANT]
>사용 하는 경우 일부 netsh 명령을 원격으로 사용 하 여 다른 컴퓨터에는 **netsh – r** 매개 변수를 원격 컴퓨터에서 원격 레지스트리 서비스를 실행 해야 합니다. 실행 하지 않는 경우 Windows는 "네트워크 경로 찾을 수 없음" 오류 메시지를 표시 합니다.

***`RemoteComputer`***

(선택 사항) 구성 하려는 원격 컴퓨터를 지정 합니다.

**`-u`**

(선택 사항) Netsh 명령을 사용자 계정으로 실행 되도록 지정 합니다.

***`DomainName\\`***

(선택 사항) 사용자 계정이 있는 도메인을 지정 합니다. 기본값은 로컬 도메인의 경우 *DomainName\\*  지정 하지 않으면.

***`UserName`***

(선택 사항) 사용자 계정 이름을 지정합니다.

**`-p`**

(선택 사항) 사용자 계정의 암호를 제공 한다고 지정 합니다.

***`Password`***

(선택 사항) 지정 된 사용자 계정의 암호를 지정 합니다 **-u** *UserName*합니다.

***`NetshCommand`***

(선택 사항) 지정 된 **netsh** 실행 하려는 명령을 합니다.

**`-f`**

(선택 사항) 종료 **netsh** 으로 지정 하는 스크립트를 실행 한 후 *ScriptFile*합니다.

***`ScriptFile`***

(선택 사항) 실행 하려는 스크립트를 지정 합니다.

**`/?`**

(선택 사항) Netsh 프롬프트에서 도움말을 표시 합니다.

>[!NOTE]
>지정 하는 경우 **`-r`** 뒤에 또 다른 명령인 **netsh** 원격 컴퓨터에서 명령을 실행 하 고 Cmd.exe 명령 프롬프트로 돌아갑니다. 지정 하는 경우 **`-r`** 없이 또 다른 명령인 **netsh** 원격 모드에서 열립니다. 프로세스를 사용 하 여 비슷합니다 **영구** Netsh 명령 프롬프트에서. 사용 하는 경우 **`-r`**, 현재 인스턴스에 대 한 대상 컴퓨터를 설정한 **netsh** 만 합니다. 종료 하 고 다시 입력 한 후 **netsh**, 로컬 컴퓨터와 대상 컴퓨터를 다시 설정 됩니다. 실행할 수 있습니다 **netsh** 컴퓨터를 지정 하 여 원격 컴퓨터에서 명령 이름을 WINS에서 저장, UNC 이름, IP 주소나 DNS 서버를가 확인할 수 있도록 인터넷 이름입니다.

**Netsh 명령에 대 한 입력 매개 변수 문자열 값**

전체 Netsh 명령 참조는 문자열 값은 필수 매개 변수를 포함 하는 명령이 있습니다.

문자열 값을 여러 단어로 구성 된 문자열 값 등 문자 간의 공백이 있는 경우에 필요는 문자열 값을 따옴표로 묶어야 하는 합니다. 예를 들어, 명명 된 매개 변수의 **인터페이스** 문자열 값을 사용 하 여 **무선 네트워크 연결**, 문자열 값 주위에 따옴표를 사용 하 여:

**`interface="Wireless Network Connection"`**

