---
title: logman 추적 만들기
description: Logman create trace 명령에 대 한 참조 항목으로, 이벤트 추적 데이터 수집기를 만듭니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1b4dfecd-6f56-4c51-b622-c2054b4aabd7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 015fb7842146e372b36c71fe95a3598bdfa48676
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222982"
---
# <a name="logman-create-trace"></a>logman 추적 만들기

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이벤트 추적 데이터 수집기를 만듭니다.

## <a name="syntax"></a>구문

```
logman create trace <[-n] <name>> [options]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| -s`<computer name>` | 지정 된 원격 컴퓨터에서 명령을 수행 합니다. |
| -config`<value>` | 명령 옵션을 포함 하는 설정 파일을 지정 합니다. |
| -ets | 는 이벤트 추적 세션에 명령을 저장 하거나 일정을 예약 하지 않고 직접 보냅니다. |
| [-n]`<name>` | 대상 개체의 이름입니다. |
| -f`<bin|bincirc>` | 데이터 수집기에 대 한 로그 형식을 지정합니다. |
| -[-] u`<user [password]>` | 사용자 계정으로 실행을 지정합니다. 암호에 `*` 대 한를 입력 하면 암호를 묻는 메시지가 생성 됩니다. 암호는 암호 프롬프트에 입력할 때 표시되지 않습니다. |
| -m`<[start] [stop] [[start] [stop] [...]]>` | 예약 된 시작 또는 종료 시간 대신 수동 시작 또는 중지를 변경 합니다. |
| -rf`<[[hh:]mm:]ss>` | 지정 된 기간 동안 데이터 수집기를 실행 합니다. |
| -b`<M/d/yyyy h:mm:ss[AM|PM]>` | 지정 된 시간에 데이터 수집을 시작 합니다. |
| -e `<M/d/yyyy h:mm:ss[AM|PM]>` | 지정 된 시간에 데이터 컬렉션을 종료 합니다. |
| -o`<path|dsn!log>` | SQL 데이터베이스에 출력 로그 파일 또는 DSN 및 로그 설정 이름을 지정 합니다. |
| -[-]r | 지정 된 시작 및 종료 시간에 매일 데이터 수집기를 반복 합니다. |
| -[-]a | 기존 로그 파일을 추가 합니다. |
| -[-] ow | 기존 로그 파일을 덮어씁니다. |
| -[-] v`<nnnnnn|mmddhhmm>` | 로그 파일 이름 끝에 파일 버전 정보를 첨부 합니다. |
| -[-] rc`<task>` | 로그가 닫힐 때마다 지정 된 명령을 실행 합니다. |
| -[-] 최대`<value>` | 최대 로그 파일 크기 (mb) 또는 SQL 로그에 대 한 레코드의 최대 수입니다. |
| -[-] my.cnf`<[[hh:]mm:]ss>` | Time이 지정 된 경우 지정 된 시간이 경과 하면에서 새 파일을 만듭니다. Time을 지정 하지 않으면에서 최대 크기를 초과할 때 새 파일을 만듭니다. |
| -y | 메시지를 표시 하지 않고 모든 질문에 답변 합니다. |
| -ct`<perf|system|cycle>` | 이벤트 추적 세션 클록 유형을 지정합니다. |
| -ln`<logger_name>` | 이벤트 추적 세션에 대해로 거 이름을 지정합니다. |
| -ft`<[[hh:]mm:]ss>` | 이벤트 추적 세션의 플러시 타이머를 지정합니다. |
| -[-] p`<provider [flags [level]]>` | 사용할 수 있도록 단일 이벤트 추적 공급자를 지정 합니다. |
| -pf`<filename>` | 사용할 수 있도록 여러 이벤트 추적 공급자를 나열 하는 파일을 지정 합니다. 파일에는 줄당 하나의 공급자를 포함 하는 텍스트 파일 이어야 합니다. |
| -[-] rt | 실시간 모드에서 이벤트 추적 세션을 실행 합니다. |
| -[-] ul | 사용자의 이벤트 추적 세션을 실행 합니다. |
| -bs`<value>` | 이벤트 추적 세션 버퍼 크기 (kb)를 지정 합니다. |
| -nb`<min max>` | 이벤트 추적 세션 버퍼의 수를 지정합니다. |
| -모드`<globalsequence|localsequence|pagedmemory>` | 다음을 포함 하 여 이벤트 추적 세션로 거 모드를 지정 합니다.<ul><li>**Globalsequence** -이벤트 추적 프로그램이 이벤트를 받은 추적 세션에 관계 없이 받는 모든 이벤트에 시퀀스 번호를 추가 하도록 지정 합니다.</li><li>**Localsequence** -이벤트 추적 프로그램에서 특정 추적 세션에서 받은 이벤트의 시퀀스 번호를 추가 하도록 지정 합니다. 이 옵션을 사용 하면 모든 세션에서 중복 시퀀스 번호가 존재할 수 있지만 각 추적 세션 내에서 고유 합니다.</li><li>**Pagedmemory** -이벤트 추적 프로그램에서 내부 버퍼 할당에 대 한 기본 비페이징 메모리 풀 대신 페이징된 메모리를 사용 하도록 지정 합니다.</li></ul> |
| /? | 도움말 상황에 맞는 표시 합니다. |

#### <a name="remarks"></a>설명

- 여기서 [-]이 나열 되 고, 추가 하이픈 (-)을 추가 하면 옵션이 무시 됩니다.

### <a name="examples"></a>예

256 개 이하의 버퍼를 사용 하 여 *trace_log*이라는 이벤트 추적 데이터 수집기를 만들려면 각 버퍼의 크기가 64kb 이며, 그 결과를 c:\logfile에 배치 하려면 다음을 입력 합니다.

```
logman create trace trace_log -nb 16 256 -bs 64 -o c:\logfile
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [logman update 추적 명령](logman-update-trace.md)

- [logman 명령](logman.md)
