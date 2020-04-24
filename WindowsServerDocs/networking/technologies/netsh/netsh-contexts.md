---
title: Netsh 명령 구문, 컨텍스트 및 서식 지정
description: 이 토픽을 사용하여 netsh 컨텍스트 및 하위 컨텍스트를 입력하고, netsh 구문 및 명령 서식 지정을 이해하고, Windows Server 2016 또는 Windows 10을 실행하는 로컬 및 원격 컴퓨터에서 netsh 명령을 실행하는 방법을 배울 수 있습니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 8cb9b59f-0255-4261-b49a-562c5ea50ee0
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 061d7252d5a7bbe09d3dca245d9b77ed20a4dedf
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80854766"
---
# <a name="netsh-command-syntax-contexts-and-formatting"></a>Netsh 명령 구문, 컨텍스트 및 서식 지정

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 토픽을 사용하여 netsh 컨텍스트 및 하위 컨텍스트를 입력하고, netsh 구문 및 명령 서식 지정을 이해하고, 로컬 및 원격 컴퓨터에서 netsh 명령을 실행하는 방법을 배울 수 있습니다.

Netsh는 현재 실행 중인 컴퓨터의 네트워크 구성을 표시하거나 수정할 수 있는 명령줄 스크립팅 유틸리티입니다. Netsh 명령은 netsh 프롬프트에 명령을 입력하여 실행할 수 있으며 일괄 처리 파일 또는 스크립트에 사용할 수 있습니다. netsh 명령을 사용하여 원격 컴퓨터와 로컬 컴퓨터를 구성할 수 있습니다.

또한 Netsh는 지정된 컴퓨터에 대해 배치 모드로 명령 그룹을 실행할 수 있게 해주는 스크립팅 기능을 제공합니다. Netsh를 사용하면 보관 목적으로 또는 다른 컴퓨터를 구성하는 데 유용하도록 구성 스크립트를 텍스트 파일로 저장할 수 있습니다.

## <a name="netsh-contexts"></a>Netsh 컨텍스트

Netsh는 동적\-연결 라이브러리 \(DLL\) 파일을 사용하여 다른 운영 체제 구성 요소와 상호 작용합니다. 

각 netsh 도우미 DLL은 네트워킹 서버 역할 또는 기능과 관련된 명령 그룹인 *컨텍스트*라는 광범위한 기능 세트를 제공합니다. 이러한 컨텍스트는 하나 이상의 서비스, 유틸리티 또는 프로토콜에 대한 구성 및 모니터링 지원을 제공하여 netsh의 기능을 확장합니다. 예를 들어 Dhcpmon.dll은 DHCP 서버를 구성하고 관리하는 데 필요한 컨텍스트 및 명령 세트를 netsh에 제공합니다.

### <a name="obtain-a-list-of-contexts"></a>컨텍스트 목록 가져오기

Windows Server 2016 또는 Windows 10을 실행하는 컴퓨터에서 명령 프롬프트 또는 Windows PowerShell을 열어 netsh 컨텍스트 목록을 가져올 수 있습니다. **netsh** 명령을 입력하고 Enter 키를 누릅니다. **/?** 를 입력하고 Enter 키를 누릅니다.

다음은 Windows Server 2016 Datacenter를 실행하는 컴퓨터에서 이러한 명령을 실행한 예제 출력입니다.

>    ```
>   PS C:\Windows\system32> netsh
>   netsh>/?
>    
>    The following commands are available:
>    
>    Commands in this context:
>    ..            - Goes up one context level.
>    ?             - Displays a list of commands.
>    abort         - Discards changes made while in offline mode.
>    add           - Adds a configuration entry to a list of entries.
>    advfirewall   - Changes to the `netsh advfirewall' context.
>    alias         - Adds an alias.
>    branchcache   - Changes to the `netsh branchcache' context.
>    bridge        - Changes to the `netsh bridge' context.
>    bye           - Exits the program.
>    commit        - Commits changes made while in offline mode.
>    delete        - Deletes a configuration entry from a list of entries.
>    dhcpclient    - Changes to the `netsh dhcpclient' context.
>    dnsclient     - Changes to the `netsh dnsclient' context.
>    dump          - Displays a configuration script.
>    exec          - Runs a script file.
>    exit          - Exits the program.
>    firewall      - Changes to the `netsh firewall' context.
>    help          - Displays a list of commands.
>    http          - Changes to the `netsh http' context.
>    interface     - Changes to the `netsh interface' context.
>    ipsec         - Changes to the `netsh ipsec' context.
>    ipsecdosprotection - Changes to the `netsh ipsecdosprotection' context.
>    lan           - Changes to the `netsh lan' context.
>    namespace     - Changes to the `netsh namespace' context.
>    netio         - Changes to the `netsh netio' context.
>    offline       - Sets the current mode to offline.
>    online        - Sets the current mode to online.
>    popd          - Pops a context from the stack.
>    pushd         - Pushes current context on stack.
>    quit          - Exits the program.
>    ras           - Changes to the `netsh ras' context.
>    rpc           - Changes to the `netsh rpc' context.
>    set           - Updates configuration settings.
>    show          - Displays information.
>    trace         - Changes to the `netsh trace' context.
>    unalias       - Deletes an alias.
>    wfp           - Changes to the `netsh wfp' context.
>    winhttp       - Changes to the `netsh winhttp' context.
>    winsock       - Changes to the `netsh winsock' context.
>    
>    The following sub-contexts are available:
>     advfirewall branchcache bridge dhcpclient dnsclient firewall http interface ipsec ipsecdosprotection lan namespace netio ras rpc trace wfp winhttp winsock
>    
>    To view help for a command, type the command, followed by a space, and then type ?.
>    ```

### <a name="subcontexts"></a>하위 컨텍스트

Netsh 컨텍스트는 *하위 컨텍스트*라고 하는 명령과 추가 컨텍스트를 모두 포함할 수 있습니다. 예를 들어 라우팅 컨텍스트 내에서 IP 및 IPv6 하위 컨텍스트를 변경할 수 있습니다.

컨텍스트 내에서 사용할 수 있는 명령 및 하위 컨텍스트 목록을 표시하려면 netsh 프롬프트에서 컨텍스트 이름을 입력한 다음, **/?** 를 입력합니다. 또는 **help**를 입력합니다. 예를 들어 라우팅 컨텍스트에서 사용할 수 있는 하위 컨텍스트 및 명령 목록을 표시하려면 netsh 프롬프트\(즉, **netsh&gt;** \)에 다음 중 하나를 입력합니다.

**routing /?**

**routing help**

현재 컨텍스트를 변경하지 않고 또 다른 컨텍스트에서 작업을 수행하려면 netsh 프롬프트에 사용하려는 명령의 컨텍스트 경로를 입력합니다. 예를 들어 먼저 IGMP 컨텍스트를 변경하지 않고 IGMP 컨텍스트에 "로컬 영역 연결"이라는 인터페이스를 추가하려면 netsh 프롬프트에 다음을 입력합니다.

**routing ip igmp add interface "Local Area Connection" startupqueryinterval=21**

## <a name="running-netsh-commands"></a>netsh 명령 실행

netsh 명령을 실행하려면 **netsh**를 입력하고 Enter 키를 눌러 명령 프롬프트에서 netsh를 시작해야 합니다. 다음으로, 사용하려는 명령이 포함된 컨텍스트로 변경할 수 있습니다. 사용 가능한 컨텍스트는 설치한 네트워킹 구성 요소에 따라 다릅니다. 예를 들어 netsh 프롬프트에 **dhcp**를 입력하고 Enter 키를 누르면 netsh가 DHCP 서버 컨텍스트로 변경됩니다. 그러나 DHCP를 설치하지 않은 경우에는 다음 메시지가 나타납니다.

**dhcp.**

## <a name="formatting-legend"></a>서식 지정 범례

netsh 프롬프트나 일괄 처리 파일 또는 스크립트에서 명령을 실행할 때 다음 서식 지정 범례를 사용하여 올바른 netsh 명령 구문을 해석하고 사용할 수 있습니다.

- *기울임꼴* 텍스트는 명령을 입력하는 동안 제공해야 하는 정보입니다. 예를 들어 명령에 -*UserName*이라는 매개 변수가 있으면 실제 사용자 이름을 입력해야 합니다.
- **굵게** 텍스트는 명령을 입력할 때 보이는 그대로 입력해야 하는 정보입니다.
- 뒤에 줄임표 \(...\)가 붙은 텍스트는 명령줄에서 여러 번 반복할 수 있는 매개 변수입니다.
- 대괄호 [&nbsp;] 사이의 텍스트는 선택적 항목입니다.
- 중괄호 {&nbsp;} 사이에 있고 파이프로 구분된 선택 항목을 포함하는 텍스트는 `{enable|disable}`처럼 하나만 선택해야 하는 선택 항목 세트를 제공합니다.
- Courier 글꼴로 서식이 지정된 텍스트는 코드 또는 프로그램 출력입니다.

## <a name="running-netsh-commands-from-the-command-prompt-or-windows-powershell"></a>명령 프롬프트 또는 Windows PowerShell에서 Netsh 명령 실행

네트워크 셸을 시작하고 명령 프롬프트 또는 Windows PowerShell에서 netsh를 입력하려면 다음 명령을 사용하면 됩니다.

### <a name="netsh"></a>netsh

Netsh는 현재 실행 중인 컴퓨터의 네트워크 구성을 로컬로 또는 원격으로 표시하거나 수정할 수 있는 명령줄 스크립팅 유틸리티입니다. 매개 변수 없이 사용할 경우 **netsh**는 Netsh.exe 명령 프롬프트(\(즉, **netsh&gt;** \))를 엽니다.

#### <a name="syntax"></a>구문

**netsh**\[ **-a**&nbsp;*AliasFile*\] \[ **-c**&nbsp;*Context* \] \[ **-r**&nbsp;*RemoteComputer*\] \[ **-u** \[ *DomainName\\* \] *UserName* \] \[ **-p**&nbsp;*Password* | \*\] \[{*NetshCommand* |  **-f**&nbsp;*ScriptFile*}\]

##### <a name="parameters"></a>매개 변수

**`-a`**

선택 사항입니다. *AliasFile*을 실행한 후 **netsh** 프롬프트로 돌아가도록 지정합니다.

**`AliasFile`**

선택 사항입니다. 하나 이상의 **netsh** 명령이 포함된 텍스트 파일 이름을 지정합니다.

**`-c`**

선택 사항입니다. netsh가 지정된 **netsh** 컨텍스트로 전환되도록 지정합니다.

**`Context`**

선택 사항입니다. 입력하려는 **netsh** 컨텍스트를 지정합니다. 

**`-r`**

선택 사항입니다. 원격 컴퓨터에서 명령을 실행하도록 지정합니다.

> [!IMPORTANT]
> 다른 컴퓨터에서 **netsh –r** 매개 변수를 사용하여 원격으로 일부 netsh 명령을 사용하는 경우 원격 컴퓨터에서 원격 레지스트리 서비스가 실행되고 있어야 합니다. 실행되고 있지 않으면 Windows에서 "네트워크 경로를 찾을 수 없음" 오류 메시지를 표시합니다.

***`RemoteComputer`***

선택 사항입니다. 구성하려는 원격 컴퓨터를 지정합니다.

**`-u`**

선택 사항입니다. 사용자 계정으로 netsh 명령을 실행하도록 지정합니다.

***`DomainName\\`***

선택 사항입니다. 사용자 계정이 있는 도메인을 지정합니다. *DomainName\\* 을 지정하지 않으면 기본값은 로컬 도메인입니다.

***`UserName`***

선택 사항입니다. 사용자 계정 이름을 지정합니다.

**`-p`**

선택 사항입니다. 사용자 계정의 암호를 입력하도록 지정합니다.

***`Password`***

선택 사항입니다. **-u** *UserName*을 사용하여 지정한 사용자 계정의 암호를 지정합니다.

***`NetshCommand`***

선택 사항입니다. 실행하려는 **netsh** 명령을 지정합니다.

**`-f`**

선택 사항입니다. *ScriptFile*을 사용하여 지정한 스크립트를 실행한 후 **netsh**를 종료합니다.

***`ScriptFile`***

선택 사항입니다. 실행하려는 스크립트를 지정합니다.

**`/?`**

선택 사항입니다. netsh 프롬프트에 도움말을 표시합니다.

> [!NOTE]
> **`-r`** 을 지정하고 뒤에 다른 명령을 붙이면 **netsh**는 원격 컴퓨터에서 명령을 실행한 다음, Cmd.exe 명령 프롬프트로 돌아갑니다. 다른 명령 없이 **`-r`** 을 지정하면 **netsh**가 원격 모드에서 열립니다. 이 프로세스는 Netsh 명령 프롬프트에서 **set machine**을 사용하는 것과 비슷합니다. **`-r`** 을 사용할 때 **netsh**의 현재 인스턴스에 대한 대상 컴퓨터만 설정합니다. **netsh**를 종료하고 다시 입력하면 대상 컴퓨터가 로컬 컴퓨터로 다시 설정됩니다. WINS에 저장된 컴퓨터 이름, UNC 이름, DNS 서버에서 확인할 인터넷 이름 또는 IP 주소를 지정하여 원격 컴퓨터에서 **netsh** 명령을 실행할 수 있습니다.

**netsh 명령의 매개 변수 문자열 값 입력**

모든 Netsh 명령 참조에는 문자열 값이 필요한 매개 변수를 포함하는 명령이 있습니다.

두 개 이상의 단어로 구성된 문자열 값처럼 문자열 값의 문자 사이에 공백이 포함된 경우 문자열 값을 따옴표로 묶어야 합니다. 예를 들어 **interface**라는 매개 변수의 문자열 값이 **Wireless Network Connection**이면 문자열 값을 따옴표로 묶습니다.

**`interface="Wireless Network Connection"`**

