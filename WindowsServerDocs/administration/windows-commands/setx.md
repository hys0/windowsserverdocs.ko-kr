---
title: setx
description: 프로그래밍 또는 스크립팅이 필요 하지 않고 사용자 또는 시스템 환경에서 환경 변수를 만들거나 수정 하는 setx에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ef37482f-f8a8-4765-951a-2518faac3f44
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 63cfb28770f635f97c8f3c7a701d9e959cee4a05
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721849"
---
# <a name="setx"></a>setx

만들거나 프로그래밍 또는 스크립팅 필요 없이 사용자 또는 시스템 환경에서 환경 변수를 수정 합니다. **Setx** 또한 레지스트리 키의 값을 검색 하 고 텍스트 파일에 씁니다.



## <a name="syntax"></a>구문

```
setx [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] <Variable> <Value> [/m]
setx [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] [<Variable>] /k <Path> [/m]
setx [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] /f <FileName> {[<Variable>] {/a <X>,<Y> | /r <X>,<Y> <String>} [/m] | /x} [/d <Delimiters>]
```

### <a name="parameters"></a>매개 변수

|         매개 변수          |                                                                                                                                              설명                                                                                                                                              |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       /s \<컴퓨터>       |                                                                                  이름 또는 원격 컴퓨터의 IP 주소를 지정합니다. 백슬래시를 사용 하지 마십시오. 기본값은 로컬 컴퓨터의 이름입니다.                                                                                  |
| /u [\<도메인>\]<User name> |                                                                                           지정 된 사용자 계정의 자격 증명으로 스크립트를 실행합니다. 기본값은 시스템 사용 권한.                                                                                            |
|      /p [\<암호>]      |                                                                                                         에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.                                                                                                         |
|        \<변수>         |                                                                                                                 설정할 환경 변수의 이름을 지정 합니다.                                                                                                                  |
|          \<값>          |                                                                                                                환경 변수를 설정 하려는 값을 지정 합니다.                                                                                                                 |
|         /k \<경로>         | 레지스트리 키에서 정보에 변수가 기반으로 설정 되도록 지정 합니다. P *"ath"* 는 다음 구문을 사용 합니다.</br>`\\<HIVE>\<KEY>\...\<Value>`</br>예를 들어 다음 경로 지정할 수 있습니다.</br>`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName` |
|      /f \<파일 이름>       |                                                                                                                               사용 하 여 원하는 파일을 지정 합니다.                                                                                                                                |
|        /a \<X>,<Y>         |                                                                                                                    검색 매개 변수로 절대 좌표와 오프셋을 지정합니다.                                                                                                                    |
|   /r \<X>,<Y><String>   |                                                                                                            상대 좌표 및 오프셋이 지정 **문자열** 매개 변수를 검색으로 합니다.                                                                                                            |
|             /m             |                                                                                                시스템 환경에서 변수를 설정 하도록 지정 합니다. 기본 설정은 로컬 환경입니다.                                                                                                 |
|             /x             |                                                                                                       표시 파일을 무시 하 고 좌표는 **/a**, **/r**, 및 **/d** 명령줄 옵션입니다.                                                                                                        |
|      /d \<구분 기호>      |                    공백, 탭, ENTER 및 **\\** 줄 바꿈 등 네 가지 기본 제공 구분 기호 외 **에도 사용할** 구분 기호를 지정 합니다. 모든 ASCII 문자를 포함 하는 유효한 구분 기호. 구분 기호는 최대 수는 15, 기본 제공 구분 기호를 포함 합니다.                    |
|             /?             |                                                                                                                                 명령 프롬프트에 도움말을 표시합니다.                                                                                                                                  |

## <a name="remarks"></a>설명

-   **Setx** 명령 SETENV UNIX 유틸리티와 비슷합니다.
-   **Setx** 직접 고 영구적으로 시스템 환경 값을 설정 하는 명령줄 또는 프로그램 방법을 제공 합니다. 시스템 환경 변수를 통해 수동으로 구성할 수는 **제어판** 또는 레지스트리 편집기를 통해. **설정** 명령 인터프리터 (Cmd.exe)의 내부 인 명령의 현재 콘솔 창에 사용자 환경 변수를 설정 합니다.
-   사용할 수는 **setx** 세 가지 소스 (모드) 중 하나에서 사용자 및 시스템에 대 한 값 환경 변수를 설정 하는 명령: 명령줄 모드, 레지스트리 모드 또는 파일 모드입니다.
-   **Setx** 레지스트리에 마스터 환경 변수를 기록 합니다. 사용 하 여 변수 설정 **setx** 변수가 다음 명령 창 에서만 사용할 수 있는 현재 명령 창에 있습니다.
-   **HKEY_CURRENT_USER** 및 **HKEY_LOCAL_MACHINE** 만 지원 되는 하이브 됩니다. REG_DWORD, REG_EXPAND_SZ, REG_SZ, 및 REG_MULTI_SZ는 유효한 **RegKey** 데이터 형식입니다.
-   에 대 한 액세스를 얻을 때 **REG_MULTI_SZ** 첫 번째 항목만 레지스트리 값을 추출 하 고 사용 합니다.
-   사용할 수 없습니다는 **setx** 로컬 시스템 또는 시스템 환경에 추가 된 값을 제거 하는 명령입니다. 사용할 수 있습니다 **설정** 변수 이름 및 값이 없는 로컬 환경에서 해당 값을 제거 하려면.
-   REG_DWORD 레지스트리 값 추출 되 고 16 진수 모드에서 사용 됩니다.
-   캐리지 리턴를 구문 분석 하는 파일 모드를 지원 하 고 줄 바꿈 (CRLF) 텍스트 파일에만 합니다.

## <a name="examples"></a>예

Brand1 값에 로컬 환경에서 컴퓨터 환경 변수를 설정 하려면 다음을 입력 합니다.
```
setx MACHINE Brand1
```
값 Brand1 컴퓨터에 시스템 환경에서 컴퓨터 환경 변수를 설정 하려면 다음을 입력 합니다.
```
setx MACHINE Brand1 Computer /m
```
PATH 환경 변수에 정의 된 검색 경로 사용 하 여 로컬 환경에서 MYPATH 환경 변수를 설정 하려면 다음을 입력 합니다.
```
setx MYPATH %PATH%
```
로 **~** **%** 바꾼 후 path 환경 변수에 정의 된 검색 경로를 사용 하도록 로컬 환경에서 MYPATH 환경 변수를 설정 하려면 다음을 입력 합니다.
```
setx MYPATH ~PATH~ 
```
Brand1 Computer1 라는 원격 컴퓨터에 로컬 환경에서 컴퓨터 환경 변수를 설정 하려면 다음을 입력 합니다.
```
setx /s computer1 /u maindom\hiropln /p p@ssW23 MACHINE Brand1
```
PATH 환경 변수에 Computer1 라는 원격 컴퓨터에 정의 된 검색 경로 사용 하 여 로컬 환경에서 MYPATH 환경 변수를 설정 하려면 다음을 입력 합니다.
```
setx /s computer1 /u maindom\hiropln /p p@ssW23 MYPATH %PATH%
```
에 있는 값에 로컬 환경에서 TZONE 환경 변수를 설정 하는 **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName** 레지스트리 키, 유형:
```
setx TZONE /k HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName 
```
에 있는 값을 Computer1 라는 원격 컴퓨터의 로컬 환경에서 TZONE 환경 변수를 설정 하는 **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName** 레지스트리 키, 유형:
```
setx /s computer1 /u maindom\hiropln /p p@ssW23 TZONE /k HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName 
```
에 있는 값에 시스템 환경에서 빌드 환경 변수를 설정 하는 **HKEY_LOCAL_MACHINE\Software\Microsoft\WindowsNT\CurrentVersion\CurrentBuildNumber** 레지스트리 키, 유형:
```
setx BUILD /k HKEY_LOCAL_MACHINE\Software\Microsoft\WindowsNT\CurrentVersion\CurrentBuildNumber /m
```
에 있는 값을 Computer1 라는 원격 컴퓨터의 시스템 환경에서 빌드 환경 변수를 설정 하는 **HKEY_LOCAL_MACHINE\Software\Microsoft\WindowsNT\CurrentVersion\CurrentBuildNumber** 레지스트리 키, 유형:
```
setx /s computer1 /u maindom\hiropln /p p@ssW23  BUILD /k HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\CurrentBuildNumber /m
```
내용 해당 하는 좌표와 함께 Ipconfig.out, 라는 파일의 내용을 표시 하려면 다음을 입력 합니다.
```
setx /f ipconfig.out /x
```
파일 Ipconfig.out 5,11 좌표에 있는 값에 로컬 환경에서 IPADDR 환경 변수를 설정 하려면 다음을 입력 합니다.
```
setx IPADDR /f ipconfig.out /a 5,11
```
로컬 환경에서 OCTET1 환경 변수를 좌표 5에 있는 값으로 설정 하려면 다음을 입력 합니다. 여기서 ** #$ \*는 구분 기호**를 사용 하 여 출력 합니다.
```
setx OCTET1 /f ipconfig.out /a 5,3 /d #$*. 
```
로컬 환경의 IPGATEWAY 환경 변수를 파일 Ipconfig의 게이트웨이 좌표를 기준으로 0, 7 좌표에 있는 값으로 설정 하려면 다음을 입력 합니다.
```
setx IPGATEWAY /f ipconfig.out /r 0,7 Gateway 
```
Ipconfig.out 라는 파일의 내용을 표시 하려면-내용 해당 하는 좌표와 함께-Computer1 라는 컴퓨터를 입력 합니다.
```
setx /s computer1 /u maindom\hiropln /p p@ssW23 /f ipconfig.out /x 
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)