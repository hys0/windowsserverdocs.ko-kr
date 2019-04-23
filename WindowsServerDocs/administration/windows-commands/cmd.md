---
title: Cmd
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6ec588db-31a9-4a73-a970-65a2c6f4abbe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 966ac7f70984dff6d26265e07a26a6eebcde9fb6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874394"
---
# <a name="cmd"></a>Cmd



Cmd.exe 명령 인터프리터를의 새 인스턴스를 시작합니다. 매개 변수 없이 사용 하는 경우 **cmd** 운영 체제의 버전 및 저작권 정보를 표시 합니다.

## <a name="syntax"></a>구문

```
cmd [/c|/k] [/s] [/q] [/d] [/a|/u] [/t:{<B><F>|<F>}] [/e:{on|off}] [/f:{on|off}] [/v:{on|off}] [<String>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/c|지정 된 명령을 실행 *문자열* 한 후 중지 합니다.|
|/k|지정 된 명령을 실행 *문자열* 하 고 계속 합니다.|
|/s|처리를 수정 *문자열* 한 후 **/c** 하거나 **/k**합니다.|
|/q|에코를 해제합니다.|
|/d|자동 실행 명령의 실행을 사용 하지 않도록 설정 합니다.|
|/ a|내부 명령이 출력을 파이프 또는 파일이으로 ANSI American National Standards Institute () 형식을 지정합니다.|
|/u|내부 명령이 출력을 파이프 또는 파일이 유니코드 형식을 지정합니다.|
|/t:{\<B\>\<F\>\|\<F\>}|배경을 설정 (*B*) 및 전경색 (*F*) 색입니다.|
|/e:on|명령 확장을 사용 하도록 설정 합니다.|
|/e:off|명령 확장을 사용 하지 않도록 설정 합니다.|
|/f:on|파일 및 디렉터리 이름 완성을 사용 하도록 설정 합니다.|
|/f:off|파일 및 디렉터리 이름 완성을 사용 하지 않도록 설정 합니다.|
|/v:on|지연 된 환경 변수 확장을 사용 하도록 설정 합니다.|
|/v:off|지연 된 환경 변수 확장을 사용 하지 않도록 설정 합니다.|
|\<String>|수행 하려는 명령을 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

다음 표에서 대 한 값으로 사용할 수 있는 유효한 16 진수 \<B\> 고 \<F\>

|값|색|
|-----|-----|
|0|검정|
|1|파랑|
|2|녹색|
|3|Aqua|
|4|빨강|
|5|자주색|
|6|노랑|
|7|하얀|
|8|회색|
|9|연한 파랑|
|a|연한 녹색|
|b|연한 옥색|
|c|연한 빨간색|
|d|옅은 자주|
|e|밝은 노랑|
|f|밝은 백서|

## <a name="remarks"></a>설명

-   여러 명령 사용

    에 대 한 여러 명령을 사용 하 여 \<문자열 >, 명령 구분 기호로 구분 **&&** 고 따옴표로 묶습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
    ```
    "<Command>&&<Command>&&<Command>"
    ```  
-   인용 부호를 처리합니다.

    지정 하는 경우 **/c** 또는 **/k**에 **cmd** 나머지 처리 *문자열* 따옴표는 모든 경우에 유지 됩니다 중 조건 충족 됩니다.  
    -   사용 하지 않는 **/s**합니다.
    -   따옴표는 정확히 하나의 집합을 사용 합니다.
    -   따옴표 안의 모든 특수 문자를 사용 하지 마십시오 (예: & @ < > () ^ |).
    -   인용 부호 안에 하나 이상의 공백 문자를 사용할 수 있습니다.
    -   합니다 *문자열* 인용 부호 안에 실행 파일의 이름입니다.

    이전 조건이 충족 되지 않는 경우 *문자열* 여는 따옴표 인지 여부를 확인 하려면 첫 번째 문자를 검사 하 여 처리 됩니다. 첫 번째 문자를 여는 따옴표 인 경우에 닫는 따옴표와 함께 제거 됩니다. 닫는 따옴표 뒤 텍스트 유지 됩니다.
-   레지스트리 하위 키를 실행합니다.

    지정 하지 않는 경우 **/d** 에 *문자열*, Cmd.exe 다음 레지스트리 하위 키를 찾습니다.

    **HKEY_LOCAL_MACHINE\Software\Microsoft\Command Processor\AutoRun\REG_SZ**

    **HKEY_CURRENT_USER\Software\Microsoft\Command Processor\AutoRun\REG_EXPAND_SZ**

    하나 또는 두 개의 레지스트리 하위 키가 없는 경우 다른 모든 변수가 하기 전에 실행 됩니다.

> [!CAUTION]
> 레지스트리를 잘못 편집하면 시스템에 심각한 손상을 줄 수 있습니다. 따라서 레지스트리를 변경하기 전에 컴퓨터의 중요한 데이터를 백업해 두어야 합니다.
-   명령 확장을 사용 하도록 설정

    명령 확장은 Windows XP에서 기본적으로 활성화 됩니다. 특정 프로세스에 사용 하 여 비활성화할 수 있습니다 **/e: 해제**합니다. 모든 확장을 사용 하지 않도록 설정 하거나 설정할 수 있습니다 **cmd** 명령줄 옵션에 다음을 설정 하 여 컴퓨터 또는 사용자 세션 **REG_DWORD** 값:

    **HKEY_LOCAL_MACHINE\Software\Microsoft\Command Processor\EnableExtensions\REG_DWORD**

    **HKEY_CURRENT_USER\Software\Microsoft\Command Processor\EnableExtensions\REG_DWORD**

    설정 된 **REG_DWORD** 값을 **0 × 1** (사용) 또는 **0 × 0** (사용 안 함) 레지스트리에서 Regedit.exe를 사용 하 여 합니다. 사용자 지정 설정이 컴퓨터 설정 보다 우선 하며 명령줄 옵션 레지스트리 설정 보다 우선 합니다.

>     [!CAUTION]
>     Incorrectly editing the registry may severely damage your system. Before making changes to the registry, you should back up any valued data on the computer.

    When you enable command extensions, the following commands are affected:  
    -   **assoc**
    -   **call**
    -   **chdir (cd)**
    -   **color**
    -   **del (erase)**
    -   **endlocal**
    -   **for**
    -   **ftype**
    -   **goto**
    -   **if**
    -   **mkdir (md)**
    -   **popd**
    -   **prompt**
    -   **pushd**
    -   **set**
    -   **setlocal**
    -   **shift**
    -   **start** (also includes changes to external command processes)
-   지연 된 환경 변수 확장을 사용 하도록 설정

    지연 된 환경 변수 확장을 사용 하도록 설정 하면 런타임 시 환경 변수 값을 대체 느낌표 문자를 사용할 수 있습니다.
-   파일 및 디렉터리 이름 완성을 사용 하도록 설정

    파일 및 디렉터리 이름 완성 기본적으로 사용 되지 않습니다. 특정 프로세스에 대 한 파일 이름 완성을 사용 하지 않도록 설정 하거나 설정할 수 있습니다는 **cmd** 명령과 **/f:**{**온**|**해제**}. 모든 프로세스에 대 한 파일 및 디렉터리 이름 완성을 사용 하지 않도록 설정 하거나 설정할 수 있습니다 합니다 **cmd** 컴퓨터에서 또는 다음을 설정 하 여 사용자 로그온 세션에 대 한 명령을 **REG_DWORD** 값:

    **HKEY_LOCAL_MACHINE\Software\Microsoft\Command Processor\CompletionChar\REG_DWORD**

    **HKEY_LOCAL_MACHINE\Software\Microsoft\Command Processor\PathCompletionChar\REG_DWORD**

    **HKEY_CURRENT_USER\Software\Microsoft\Command Processor\CompletionChar\REG_DWORD**

    **HKEY_CURRENT_USER\Software\Microsoft\Command Processor\PathCompletionChar\REG_DWORD**

    설정 하는 **REG_DWORD** 값 Regedit.exe를 실행 하 고 특정 기능에 대 한 제어 문자의 16 진수 값을 사용 하 여 (예를 들어 **0 × 9** 은 탭 및 **0 × 08** 는 백스페이스)입니다. 사용자 지정 설정이 컴퓨터 설정 보다 우선 하며 명령줄 옵션 레지스트리 설정 보다 우선 합니다.

> [!CAUTION]
> 레지스트리를 잘못 편집하면 시스템에 심각한 손상을 줄 수 있습니다. 따라서 레지스트리를 변경하기 전에 컴퓨터의 중요한 데이터를 백업해 두어야 합니다.

사용 하 여 파일 및 디렉터리 이름 완성을 사용 하도록 설정 하면 **/f:에서**, 파일 이름 완성을 위해 디렉터리 이름 완성을 위해 CTRL + D 및 CTRL + F를 사용 합니다. 레지스트리의 특정 완료 문자를 사용 하지 않으려면 공백에 대 한 값을 사용 [**0 × 20**] 올바른 제어 문자 하지 않기 때문입니다.

CTRL + D 또는 CTRL + F를 누르면 **cmd** 파일 및 디렉터리 이름 완성을 처리 합니다. 이러한 키 조합을 함수에는 와일드 카드 문자를 추가 *문자열* (하나가 없는 경우), 다음 첫 번째 일치 하는 경로 표시 하 고 일치 하는 경로 목록을 작성 합니다. 경로가 일치 하는 경우 파일 및 디렉터리 이름 완성 기능은 경고음을 발생시킬지 및 표시를 변경 하지 않습니다. 일치 하는 경로 목록을 단계별로 이동, CTRL + D 또는 CTRL + F 여러 번 누릅니다. 이전 버전과 목록을 이동 하려면 동시에 SHIFT 키 및 CTRL + D 또는 CTRL + F를 누릅니다. 저장 된 목록이 일치 하는 경로 삭제 하 고 새 목록을 생성, 편집 *문자열* 고 CTRL + D 또는 CTRL + F 키를 누릅니다. CTRL + D 및 CTRL + F를 전환할 경우 일치 하는 경로 대 한 저장 된 목록을 삭제 되 고 새 목록이 생성 됩니다. 유일한 차이점은 키 조합 CTRL + D 및 CTRL + F CTRL + D에만 디렉터리 이름과 일치 하 고 CTRL + F 파일 및 디렉터리 이름과 일치 됩니다. 기본 제공 디렉터리 명령 중 하나에서 파일 및 디렉터리 이름 완성을 사용 하는 경우 (즉, **CD**를 **MD**, 또는 **RD**), 디렉터리 완성 것으로 간주 됩니다.

파일 및 디렉터리 이름 완성 일치 하는 경우 경로 앞뒤에 큰따옴표를 배치 하는 경우 공백이 나 특수 문자를 포함 하는 파일 이름을 올바르게 처리 합니다.

특수 문자에는 따옴표가 필요 합니다. & < > {} ^ =! '+,' ~ [공백].

사용자가 제공한 정보에 공백이 포함 된 경우 (예: "컴퓨터 이름") 텍스트 주위에 따옴표를 사용 합니다.

내에서 파일 및 디렉터리 이름 완성을 처리 하는 경우 *문자열*, 모든 부분을 *경로* 커서의 오른쪽에 삭제 됩니다 (시점에서 *문자열* 위치는 완료 된 처리).

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
