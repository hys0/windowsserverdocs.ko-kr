---
title: cmd를
description: 명령 인터프리터의 새 인스턴스를 시작 하는 cmd의 Windows 명령 항목. Cmd.exe.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6ec588db-31a9-4a73-a970-65a2c6f4abbe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 83b5e27017a9a0f979acec428b8ddaa73cd9d46b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847626"
---
# <a name="cmd"></a>cmd를

명령 인터프리터 인 Cmd.exe의 새 인스턴스를 시작 합니다. 매개 변수 없이 사용 하는 경우 **cmd** 운영 체제의 버전 및 저작권 정보를 표시 합니다.

## <a name="syntax"></a>구문

```
cmd [/c|/k] [/s] [/q] [/d] [/a|/u] [/t:{<B><F>|<F>}] [/e:{on|off}] [/f:{on|off}] [/v:{on|off}] [<String>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/c|*문자열* 에 지정 된 명령을 수행 하 고 중지 합니다.|
|/k|*문자열로* 지정 된 명령을 수행 하 고 계속 합니다.|
|/s|**/C** 또는 **/K**뒤의 *문자열* 처리를 수정 합니다.|
|/q|에코를 끕니다.|
|/d|자동 실행 명령의 실행을 사용 하지 않도록 설정 합니다.|
|/a|ANSI(American National Standards Institute) (ANSI)로 파이프 또는 파일에 대 한 내부 명령 출력의 서식을 지정 합니다.|
|/u|파이프 또는 파일에 대 한 내부 명령 출력의 형식을 유니코드로 지정 합니다.|
|/t: {\<B\>\<F\>\|\<F\>}|배경 (*B*) 및 전경 (*F*) 색을 설정 합니다.|
|/e: on|명령 확장을 사용 하도록 설정 합니다.|
|/e: off|명령 확장을 사용 하지 않습니다.|
|/f: 설정|파일 및 디렉터리 이름 완성을 사용 하도록 설정 합니다.|
|/f: off|파일 및 디렉터리 이름 완성을 사용 하지 않습니다.|
|/v: 켜기|지연 된 환경 변수 확장을 사용 하도록 설정 합니다.|
|/v: off|지연 된 환경 변수 확장을 사용 하지 않습니다.|
|\<문자열 >|수행 하려는 명령을 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

다음 표에서는 \<B\> 및 \<F의 값으로 사용할 수 있는 유효한 16 진수를 보여 줍니다\>

|값|색|
|-----|-----|
|0|검정|
|1|파랑|
|2|녹색|
|3|Aqua|
|4|빨강|
|5|Purple|
|6|Yellow|
|7|하얀|
|8|회색|
|9|연한 파랑|
|a|연한 녹색|
|b|연한 바다색|
|c|연한 빨간색|
|d|연한 자주색|
|e|밝은 노랑|
|f|밝은 백서|

## <a name="remarks"></a>주의

-   여러 명령 사용

    문자열 > \<대 한 여러 명령을 사용 하려면 명령 구분 기호 **&&** 를 사용 하 여 구분 하 고 따옴표로 묶습니다. 예를 들면 다음과 같습니다.

    ```
    <Command>&&<Command>&&<Command>
    ``` 
 
-   따옴표 처리

    **/C** 또는 **/k**를 지정 하는 경우 **cmd** 는 *문자열* 의 나머지를 처리 하 고 따옴표는 다음 조건이 모두 충족 되는 경우에만 유지 됩니다.  
    -   **/S**를 사용 하지 않습니다.
    -   정확 하 게 한 개의 따옴표를 사용 합니다.
    -   따옴표 안에 특수 문자 (예: & < > () @ ^ |)를 사용 하지 않습니다.
    -   따옴표 안에 하나 이상의 공백 문자를 사용 합니다.
    -   따옴표 안의 *문자열* 은 실행 파일의 이름입니다.

    이전 조건이 충족 되지 않으면 첫 번째 문자를 검사 하 여 여는 따옴표 인지 여부를 확인 하 여 *문자열* 을 처리 합니다. 첫 번째 문자가 여는 따옴표 이면 닫는 따옴표와 함께 제거 됩니다. 닫는 따옴표 뒤에 나오는 모든 텍스트는 그대로 유지 됩니다.
-   레지스트리 하위 키 실행

    *문자열*에 **/d** 를 지정 하지 않으면 cmd.exe는 다음 레지스트리 하위 키를 찾습니다.

    **HKEY_LOCAL_MACHINE \Software\Microsoft\Command Processor\AutoRun\ REG_SZ**

    **HKEY_CURRENT_USER \Software\Microsoft\Command Processor\AutoRun\ REG_EXPAND_SZ**

    하나 또는 두 레지스트리 하위 키가 있는 경우 다른 모든 변수 보다 먼저 실행 됩니다.

> [!CAUTION]
> 레지스트리를 잘못 편집하면 시스템이 크게 손상될 수 있습니다. 따라서 레지스트리를 변경하기 전에 컴퓨터의 중요한 데이터를 백업해 두어야 합니다.

-   명령 확장 사용 및 사용 안 함

    Windows XP에서 명령 확장은 기본적으로 사용 하도록 설정 되어 있습니다. **/E: off**를 사용 하 여 특정 프로세스에 대해 사용 하지 않도록 설정할 수 있습니다. 다음 **REG_DWORD** 값을 설정 하 여 컴퓨터 또는 사용자 세션에서 모든 **cmd** 명령줄 옵션에 대 한 확장을 사용 하거나 사용 하지 않도록 설정할 수 있습니다.

    **HKEY_LOCAL_MACHINE \Software\Microsoft\Command Processor\EnableExtensions\ REG_DWORD**

    **HKEY_CURRENT_USER \Software\Microsoft\Command Processor\EnableExtensions\ REG_DWORD**

    Regedit.exe를 사용 하 여 레지스트리에서 **REG_DWORD** 값을 **0 × 1** (사용) 또는 **0 x 0** (사용 안 함)으로 설정 합니다. 사용자 지정 설정이 컴퓨터 설정 보다 우선 하며 명령줄 옵션 레지스트리 설정 보다 우선 합니다.

> [!CAUTION]
> 레지스트리를 잘못 편집하면 시스템이 크게 손상될 수 있습니다. 따라서 레지스트리를 변경하기 전에 컴퓨터의 중요한 데이터를 백업해 두어야 합니다.

    When you enable command extensions, the following commands are affected:  
    -  **assoc**
    -  **call**
    -  **chdir (cd)**
    -  **color**
    -  **del (erase)**
    -  **endlocal**
    -  **for**
    -  **ftype**
    -  **goto**
    -  **if**
    -  **mkdir (md)**
    -  **popd**
    -  **prompt**
    -  **pushd**
    -  **set**
    -  **setlocal**
    -  **shift**
    -  **start** (also includes changes to external command processes)

-   지연 된 환경 변수 확장 사용

    지연 된 환경 변수 확장을 사용 하도록 설정 하면 런타임에 느낌표 문자를 사용 하 여 환경 변수 값을 대체할 수 있습니다.
-   파일 및 디렉터리 이름 완성 사용

    파일 및 디렉터리 이름 완성은 기본적으로 사용 되지 않습니다. **/F:** {**on**|**off**}를 사용 하 여 **cmd** 명령의 특정 프로세스에 대해 파일 이름 완성을 사용 하거나 사용 하지 않도록 설정할 수 있습니다. 다음 **REG_DWORD** 값을 설정 하 여 컴퓨터의 **cmd** 명령 또는 사용자 로그온 세션의 모든 프로세스에 대해 파일 및 디렉터리 이름 완성을 사용 하거나 사용 하지 않도록 설정할 수 있습니다.

    **HKEY_LOCAL_MACHINE \Software\Microsoft\Command Processor\CompletionChar\ REG_DWORD**

    **HKEY_LOCAL_MACHINE \Software\Microsoft\Command Processor\PathCompletionChar\ REG_DWORD**

    **HKEY_CURRENT_USER \Software\Microsoft\Command Processor\CompletionChar\ REG_DWORD**

    **HKEY_CURRENT_USER \Software\Microsoft\Command Processor\PathCompletionChar\ REG_DWORD**

    **REG_DWORD** 값을 설정 하려면 regedit.exe를 실행 하 고 특정 함수에 대 한 제어 문자의 16 진수 값을 사용 합니다. 예를 들어 **0 x 9** 는 TAB이 고 **0 x 08** 은 백스페이스입니다. 사용자 지정 설정이 컴퓨터 설정 보다 우선 하며 명령줄 옵션 레지스트리 설정 보다 우선 합니다.

> [!CAUTION]
> 레지스트리를 잘못 편집하면 시스템이 크게 손상될 수 있습니다. 따라서 레지스트리를 변경하기 전에 컴퓨터의 중요한 데이터를 백업해 두어야 합니다.

**/F: on**을 사용 하 여 파일 및 디렉터리 이름 완성을 사용 하도록 설정 하는 경우 디렉터리 이름 완성을 위해 Ctrl + D를 사용 하 고 파일 이름 완성에는 Ctrl + f를 사용 합니다. 레지스트리에서 특정 완료 문자를 사용 하지 않도록 설정 하려면 올바른 제어 문자가 아니기 때문에 공백 [**0 x 20**]에 대 한 값을 사용 합니다.

CTRL + D 또는 CTRL + F를 누르면 **cmd** 에서 파일 및 디렉터리 이름 완료를 처리 합니다. 이러한 키 조합 함수는 와일드 카드 문자를 *문자열* 에 추가 하 고 (있는 경우) 일치 하는 경로 목록을 작성 한 다음 첫 번째 일치 하는 경로를 표시 합니다. 일치 하는 경로가 없으면 파일 및 디렉터리 이름 완성 함수는 경고음을 들리고 표시를 변경 하지 않습니다. 일치 하는 경로 목록을 이동 하려면 CTRL + D 또는 CTRL + F를 반복 해 서 누릅니다. 목록을 뒤로 이동 하려면 SHIFT 키와 CTRL + D 또는 CTRL + F를 동시에 누릅니다. 일치 하는 경로의 저장 된 목록을 삭제 하 고 새 목록을 생성 하려면 *문자열* 을 편집 하 고 Ctrl + D 또는 Ctrl + F를 누릅니다. CTRL + D와 CTRL + F 사이를 전환 하면 일치 하는 경로의 저장 된 목록이 삭제 되 고 새 목록이 생성 됩니다. Ctrl + D와 CTRL + F의 키 조합 간 유일한 차이점은 CTRL + D는 디렉터리 이름과 일치 하 고 CTRL + F는 파일 및 디렉터리 이름과 일치 한다는 것입니다. 기본 제공 디렉터리 명령 ( **CD**, **MD**또는 **RD**)에서 파일 및 디렉터리 이름 완성을 사용 하는 경우 디렉터리 완료를 가정 합니다.

일치 하는 경로 주위에 따옴표를 넣으면 파일 및 디렉터리 이름 완성에서 공백이 나 특수 문자를 포함 하는 파일 이름을 올바르게 처리 합니다.

다음 특수 문자에는 따옴표가 필요 합니다. & < > [] {} ^ =;! ' +, ' ~ [공백].

사용자가 제공 하는 정보에 공백이 포함 된 경우 텍스트에 따옴표를 사용 합니다 (예: 컴퓨터 이름).

*문자열*내에서 파일 및 디렉터리 이름 완성을 처리 하는 경우 커서 오른쪽의 *경로* 부분은 모두 삭제 됩니다 (완료가 처리 된 *문자열* 의 지점).

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
