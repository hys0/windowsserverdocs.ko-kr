---
title: Netsh 명령 구문을, 컨텍스트 및 포맷
description: Netsh 구문 및 명령 서식, 이해, netsh 컨텍스트와 하위 컨텍스트를 입력 하는 방법 및 Windows Server 2016 또는 Windows 10을 실행 하는 지역 및 원격 컴퓨터에서 netsh 명령을 실행 하는 방법을 자세히 알아보려면이 항목을 사용할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 8cb9b59f-0255-4261-b49a-562c5ea50ee0
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c7c16674b831431ff5bb1d0172cc2b2a939008f6
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="netsh-command-syntax-contexts-and-formatting"></a>Netsh 명령 구문을, 컨텍스트 및 포맷

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

Netsh 구문 및 명령 서식, 이해, netsh 컨텍스트와 하위 컨텍스트를 입력 하는 방법과 netsh 명령을 지역 및 원격 컴퓨터에서 실행 하는 방법을 자세히 알아보려면이 항목을 사용할 수 있습니다.

Netsh을 표시 하거나 현재 실행 중인 컴퓨터의 네트워크 구성 수정할 수 있도록 해 주는 스크립팅 명령줄 유틸리티입니다. Netsh 명령을 netsh 프롬프트 명령을 입력 하 여 실행할 수 있으며 배치 파일이 나 스크립트에서 사용할 수 있습니다. Netsh 명령을 사용 하 여 원격 컴퓨터와 로컬 컴퓨터를 구성할 수 있습니다.

Netsh 명령 일련 지정 된 컴퓨터에 대해 배치 모드에서 실행할 수 있게 해 주는 스크립팅 기능도 제공 합니다. Netsh, 구성 스크립트 보관 용도로 또는 다른 컴퓨터를 구성 하는 데 도움이 되는 텍스트 파일에 저장할 수 있습니다.

## <a name="netsh-contexts"></a>Netsh 컨텍스트

Netsh는 dynamic\ 연결 라이브러리 \(DLL\) 파일을 사용 하 여 다른 운영 체제의 구성 요소와 상호 작용 합니다. 

각 netsh 도우미 DLL 다양 한 이라는 기능 집합을 제공는 *상황에 맞는*, 네트워킹 서버 역할 나 기능에 따라 다른 명령 그룹입니다. 이러한 컨텍스트 구성 하 고 모니터링 하나 이상의 서비스, 유틸리티, 또는 프로토콜에 대 한 지원을 netsh의 기능을 확장 합니다. 예를 들어, Dhcpmon.dll netsh 된 상황에 맞 및 명령 구성 하 고 DHCP 서버 관리 하는 데 필요한 집합을 제공 합니다.

### <a name="obtain-a-list-of-contexts"></a>컨텍스트의 목록을 보려면

Windows Server 2016 또는 Windows 10을 실행 하는 컴퓨터에서 명령 프롬프트 또는 Windows PowerShell 열어 netsh 컨텍스트의 목록을 얻을 수 있습니다. 명령 입력 **netsh** ENTER 키를 누릅니다. 입력 **/ 있나요? **, ENTER 키를 누릅니다.

다음은 Windows Server 2016 Datacenter 실행 하는 컴퓨터에서 다음이 명령에 대 한 출력 예입니다.

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

Netsh 컨텍스트 명령 및 라고 추가 컨텍스트 포함 될 수 있습니다 *하위 컨텍스트*합니다. 예를 들어, 라우팅 컨텍스트가 내 IP 및 IPv6 하위 컨텍스트를 변경할 수 있습니다.

다양 한 명령과 netsh 프롬프트 컨텍스트를 내에서 사용할 수 있는 하위 컨텍스트 목록을 표시 하려면 상황에 맞는 이름을 입력 하 고 다음 중 하나를 입력 **/ 있나요?** 또는 **도움말**합니다. 예를 들어 하위 컨텍스트 및 사용할 수 있는 명령 목록이 라우팅 컨텍스트가 netsh 프롬프트를 표시 하려면 \ (즉, **netsh&gt;**\)를 입력 하 고 다음 중 하나를 다음과 같습니다.

**경로 /?**

**라우팅 도움말**

현재 컨텍스트에서를 변경 하지 않고 다른 상황에 맞는의 작업을 수행 하려면 netsh 프롬프트 사용 하려는 명령의 상황에 맞는 경로 입력 합니다. 예를 들어, IGMP 컨텍스트가 netsh 프롬프트를 첫 번째 변경 하지 않고 IGMP 컨텍스트가에서 "로컬 지역 연결" 이라는 인터페이스 추가를 입력 합니다.

**"로컬 지역 연결" startupqueryinterval 인터페이스 추가 ip igmp 경로 21 =**

## <a name="running-netsh-commands"></a>Netsh 명령을 실행

Netsh 명령을 실행 하려면 시작 해야 netsh 명령 프롬프트에서 입력 하 여 **netsh** 하 고 ENTER 키를 합니다. 다음에 사용 하려는 명령 포함 된 상황에 맞는을 변경할 수 있습니다. 컨텍스트를 사용할 수 있는 사용자가 설치한 네트워킹 구성 요소에 따라 다릅니다. 예를 들어, 사용자가 입력 **dhcp** DHCP 서버 컨텍스트로 변경 netsh netsh 프롬프트에서 ENTER 키를 누릅니다. 하지만 설치 된 DHCP 없는, 다음과 같은 메시지가 나타납니다.

**다음 명령을 찾을 수 없습니다: dhcp 합니다.**

## <a name="formatting-legend"></a>전설 형식

다음과 같은 서식 지정 전설 해석 하 고 올바른 netsh 명령 구문을 또는 배치 파일이 나 스크립트 netsh 프롬프트 명령을 실행 될 때 사용 하 여 사용할 수 있습니다.

- 텍스트를 *기울임꼴* 명령을 입력 하는 동안 제공 해야 하는 정보입니다. 예를 들어 명령을 라는-매개*사용자 이름*, 실제 사용자 이름을 입력 해야 합니다.
- 텍스트를 **굵게** 명령을 입력 하는 동안 표시 된 대로 입력 해야 하는 정보입니다.
- 줄임표 \(...\) 이어서 텍스트 명령줄에서 여러 번 반복 될 수 있는 매개입니다.
- 괄호 사이 있는 텍스트 [&nbsp;]는 선택 항목이 있습니다.
- 괄호 사이 있는 텍스트 {&nbsp;}로 구분 제공 선택 항목을 선택 해야 하나만 같은 집합이 `{enable|disable}`합니다.
- Courier 글꼴으로 포맷 되는 텍스트 출력 코드나 프로그램입니다.

## <a name="running-netsh-commands-from-the-command-prompt-or-windows-powershell"></a>명령 프롬프트를 Windows PowerShell Netsh 명령을 실행

네트워크 셸 시작 netsh 또는 Windows PowerShell 명령 프롬프트에 입력 하 고 다음 명령을 사용할 수 있습니다.

### <a name="netsh"></a>netsh

Netsh 로컬 또는 원격, 표시 하거나 현재 실행 중인 컴퓨터의 네트워크 구성 수정할 수 있는 스크립팅 명령줄 유틸리티입니다. 매개 변수를 않고도 사용 **netsh** Netsh.exe 명령 프롬프트를 열고 \ (즉, **netsh&gt;**\).

#### <a name="syntax"></a>구문

**netsh**\[ **-a**&nbsp;*AliasFile*\] \[ **-c**&nbsp;*Context* \] \[**-r**&nbsp;*RemoteComputer*\] \[ **-u** \[ *DomainName\\* \] *UserName* \] \[ **-p**&nbsp;*Password* | \*\] \[{*NetshCommand* | **-f**&nbsp;*ScriptFile*}\]

#### <a name="parameters"></a>매개

**`-a`**

선택 사항입니다. 으로 돌아갑니다 지정는 **netsh** 실행 한 후 프롬프트 *AliasFile*합니다.

**`AliasFile`**

선택 사항입니다. 하나 이상의 포함 된 텍스트 파일의 이름을 지정 **netsh** 명령을 합니다.

**`-c`**

선택 사항입니다. 해당 netsh 입력 지정 된 지정 **netsh** 컨텍스트가 합니다.

**`Context`**

선택 사항입니다. 지정는 **netsh** 컨텍스트를 입력 합니다. 

**`-r`**

선택 사항입니다. 원격 컴퓨터에서 실행 하도록 명령 지정 합니다.

>[!IMPORTANT]
>때 명령을 사용 하 여 일부 netsh 원격으로 사용 하는 다른 컴퓨터에서 **netsh-r** 매개 원격 컴퓨터에서 원격 레지스트리 서비스가 실행 해야 합니다. 를 실행 하지 않는 Windows "네트워크 경로 찾을 수 없습니다" 오류 메시지가 표시 됩니다.

***`RemoteComputer`***

선택 사항입니다. 원격 컴퓨터 구성 하려면를 지정 합니다.

**`-u`**

선택 사항입니다. 사용자 계정 netsh 명령을 실행 하려면를 지정 합니다.

***`DomainName\\`***

선택 사항입니다. 사용자 계정이 있는 도메인을 지정 합니다. 기본값은 기다렸다가 경우 *DomainName\\* 지정 되지 않습니다.

***`UserName`***

선택 사항입니다. 사용자 계정 이름을 지정합니다.

**`-p`**

선택 사항입니다. 사용자 계정에 대 한 암호를 지정 합니다.

***`Password`***

선택 사항입니다. 지정 된 사용자 계정의 암호를 지정 **-u** *사용자 이름*합니다.

***`NetshCommand`***

선택 사항입니다. 지정는 **netsh** 명령을 실행 합니다.

**`-f`**

선택 사항입니다. 종료 **netsh** 스크립트도 지정 하면를 실행 한 후 *스크립트 파일*합니다.

***`ScriptFile`***

선택 사항입니다. 스크립트를 실행할를 지정 합니다.

**`/?`**

선택 사항입니다. Netsh 프롬프트에서 도움말을 표시 합니다.

>[!NOTE]
>사용자가 지정 하는 경우 ** `-r` ** 다음에 다른 명령을 **netsh** 원격 컴퓨터에서 명령을 실행 하 고 다음 Cmd.exe 명령 프롬프트를 반환 합니다. 사용자가 지정 하는 경우 ** `-r` ** 다른 명령을 않고도 **netsh** 원격 모드로 엽니다. 프로세스를 사용 하는 것과 비슷합니다 **영구** Netsh 명령 프롬프트에 있습니다. 사용 하는 경우 ** `-r` **, 대상 컴퓨터의 현재 인스턴스 설정 **netsh** 만 합니다. 종료 하 고 다시 입력 한 후 **netsh**, 로컬 컴퓨터와 대상 컴퓨터 다시 설정 됩니다. 실행할 수 **netsh** 명령을 컴퓨터를 지정 하 여 원격 컴퓨터의 이름을 WINS에 저장 된, UNC 이름, IP 주소 또는 DNS 서버를 확인 하는 인터넷 이름입니다.

**Netsh 명령에 대 한 추가적인 매개 입력**

Netsh 명령 참조 전반에 걸쳐 문자열 값이 필요 매개 변수를 포함 하는 명령 가지가 있습니다.

문자열 값을 여러 개 단어를 구성 하는 추가적인 등의 문자 사이의 공백에 포함 된 경우에 필요한는 따옴표 안에 문자열 값을 포함 하는 합니다. 라는 매개 예를 들어 **인터페이스** 문자열 값으로 **무선 네트워크 연결**, 큰따옴표 문자열 값 주위를 사용:

**`interface="Wireless Network Connection"`**

