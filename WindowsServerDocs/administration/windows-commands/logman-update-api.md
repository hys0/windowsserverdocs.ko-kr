---
title: logman api를 업데이트 합니다.
description: 기존 API 추적 데이터 수집기의 속성을 업데이트 하는 logman update api 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6f322e52-0f9f-42b1-bd64-8b8f8fe086fc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 40575772e5f82474c4afbd4809773f47d7e4e075
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933872"
---
# <a name="logman-update-api"></a>logman api를 업데이트 합니다.

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기존 API 추적 데이터 수집기의 속성을 업데이트 합니다.

## <a name="syntax"></a>구문

```
logman update api <[-n] <name>> [options]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| -s`<computer name>` | 지정 된 원격 컴퓨터에서 명령을 수행 합니다. |
| -config`<value>` | 명령 옵션을 포함 하는 설정 파일을 지정 합니다. |
| [-n]`<name>` | 대상 개체의 이름입니다. |
| -f`<bin|bincirc>` | 데이터 수집기에 대 한 로그 형식을 지정합니다. |
| -[-] u`<user [password]>` | 사용자 계정으로 실행을 지정합니다. 암호에 대해를 입력 하면 `*` 암호를 묻는 메시지가 생성 됩니다. 암호는 암호 프롬프트에 입력할 때 표시되지 않습니다. |
| -m`<[start] [stop] [[start] [stop] [...]]>` | 예약 된 시작 시간 또는 종료 시간 대신 수동 시작 또는 중지로 변경 되었습니다. |
| -rf`<[[hh:]mm:]ss>` | 지정 된 기간에 대 한 데이터 수집기를 실행 합니다. |
| -b`<M/d/yyyy h:mm:ss[AM|PM]>` | 지정된 된 시간에 데이터 수집을 시작 합니다. |
| -e `<M/d/yyyy h:mm:ss[AM|PM]>` | 지정된 된 시간에 대 한 데이터 수집을 종료 합니다. |
| -si`<[[hh:]mm:]ss>` | 성능 카운터 데이터 수집기에 대 한 샘플 간격을 지정합니다. |
| -o`<path|dsn!log>` | SQL 데이터베이스에 출력 로그 파일 또는 DSN 및 로그 설정 이름을 지정 합니다. |
| -[-]r | 지정 된 시작 및 종료 시간에 매일 데이터 수집기를 반복 합니다. |
| -[-]a | 기존 로그 파일을 추가 합니다. |
| -[-] ow | 기존 로그 파일을 덮어씁니다. |
| -[-] v`<nnnnnn|mmddhhmm>` | 로그 파일 이름 끝에 파일 버전 정보를 첨부 합니다. |
| -[-] rc`<task>` | 지정 된 명령을 실행 될 때마다 로그가 닫힙니다. |
| -[-] 최대`<value>` | 최대 로그 파일 크기 (mb) 또는 SQL 로그에 대 한 레코드의 최대 수입니다. |
| -[-] my.cnf`<[[hh:]mm:]ss>` | Time이 지정 된 경우 지정 된 시간이 경과 하면에서 새 파일을 만듭니다. Time을 지정 하지 않으면에서 최대 크기를 초과할 때 새 파일을 만듭니다. |
| -y | 메시지를 표시 하지 않고 모든 질문에 예로 답변 합니다. |
| -mods`<path [path [...]]>` | API 호출을 기록 하는 모듈의 목록을 지정 합니다. |
| -inapis` <module!api [module!api [...]]>` | 로깅에 포함할 API 호출의 목록을 지정 합니다. |
| -exapis`<module!api [module!api [...]]>` | API 호출을 로깅에서 제외 목록을 지정 합니다. |
| -[-] ano | Log (-ano) API 이름만 (-ano) API 이름만 기록 하거나 기록 하지 않습니다. |
| -[-] 재귀 | 첫 번째 계층을 벗어나 재귀적으로 (-recursive) 또는 로그 하지 않습니다 (-recursive). |
| -exe`<value>` | API 추적을 위한 실행 파일의 전체 경로 지정합니다. |
| /? | 도움말 상황에 맞는 표시 합니다. |

#### <a name="remarks"></a>설명

- 여기서 [-]이 나열 되 고, 추가 하이픈 (-)을 추가 하면 옵션이 무시 됩니다.

### <a name="examples"></a>예

*Trace_notepad*이라는 기존 api 추적 카운터를 업데이트 하려면 모듈 kernel32.dll에서 생성 된 Api 호출 TlsGetValue를 제외 하 여 실행 파일 c:\windows\notepad.exe에 대해 다음을 입력 합니다.

```
logman update api trace_notepad -exe c:\windows\notepad.exe -exapis kernel32.dll!TlsGetValue
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [logman api 만들기 명령](logman-create-api.md)

- [logman 명령](logman.md)
