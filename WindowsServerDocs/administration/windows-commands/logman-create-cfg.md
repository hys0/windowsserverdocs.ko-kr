---
title: logman cfg 만들기
description: 구성 데이터 수집기를 만드는 logman create cfg 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bfc87093-3ff5-4e19-aa93-d185fb8e2239
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 518b0c7bddf1d74522a376aafb7da85abb849ac4
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222972"
---
# <a name="logman-create-cfg"></a>logman cfg 만들기

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

구성 데이터 수집기를 만듭니다.

## <a name="syntax"></a>구문

```
logman create cfg <[-n] <name>> [options]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| -s`<computer name>` | 지정 된 원격 컴퓨터에서 명령을 수행 합니다. |
| -config`<value>` | 명령 옵션을 포함 하는 설정 파일을 지정 합니다. |
| [-n]`<name>` | 대상 개체의 이름입니다. |
| -[-] u`<user [password]>` | 사용자 계정으로 실행을 지정합니다. 암호에 대해를 입력 하면 \* 암호를 묻는 메시지가 생성 됩니다. 암호는 암호 프롬프트에 입력할 때 표시되지 않습니다. |
| -m`<[start] [stop] [[start] [stop] [...]]>` | 예약 된 시작 또는 종료 시간 대신 수동 시작 또는 중지를 변경 합니다. |
| -rf`<[[hh:]mm:]ss>` | 지정 된 기간 동안 데이터 수집기를 실행 합니다. |
| -b`<M/d/yyyy h:mm:ss[AM|PM]>` | 지정 된 시간에 데이터 수집을 시작 합니다. |
| -e `<M/d/yyyy h:mm:ss[AM|PM]>` | 지정 된 시간에 데이터 컬렉션을 종료 합니다. |
| -si`<[[hh:]mm:]ss>` | 성능 카운터 데이터 수집기에 대 한 샘플 간격을 지정합니다. |
| -o`<path|dsn!log>` | SQL 데이터베이스에 출력 로그 파일 또는 DSN 및 로그 설정 이름을 지정 합니다. |
| -[-]r | 지정 된 시작 및 종료 시간에 매일 데이터 수집기를 반복 합니다. |
| -[-]a | 기존 로그 파일을 추가 합니다. |
| -[-] ow | 기존 로그 파일을 덮어씁니다. |
| -[-] v`<nnnnnn|mmddhhmm>` | 로그 파일 이름 끝에 파일 버전 정보를 첨부 합니다. |
| -[-] rc`<task>` | 로그가 닫힐 때마다 지정 된 명령을 실행 합니다. |
| -[-] 최대`<value>` | 최대 로그 파일 크기 (mb) 또는 SQL 로그에 대 한 레코드의 최대 수입니다. |
| -[-] my.cnf`<[[hh:]mm:]ss>` | Time이 지정 된 경우 지정 된 시간이 경과 하면에서 새 파일을 만듭니다. Time을 지정 하지 않으면에서 최대 크기를 초과할 때 새 파일을 만듭니다. |
| -y | 메시지를 표시 하지 않고 모든 질문에 답변 합니다. |
| -[-] ni | (-Ni) 또는 (-ni) 네트워크 인터페이스 쿼리를 사용 하지 않도록 설정 합니다. |
| -reg`<path [path [...]]>` | 수집할 레지스트리 값을 지정 합니다. |
| -mgt`<query [query [...]]>` | SQL 쿼리 언어를 사용 하 여 수집 하는 WMI 개체를 지정 합니다. |
| -ftc`<path [path [...]]>` | 수집할 파일의 전체 경로 지정 합니다. |
| /? | 도움말 상황에 맞는 표시 합니다. |

#### <a name="remarks"></a>설명

- 여기서 [-]이 나열 되 고, 추가 하이픈 (-)을 추가 하면 옵션이 무시 됩니다.

### <a name="examples"></a>예

레지스트리 키를 사용 하 여 cfg_log 이라는 구성 데이터 수집기를 만들려면 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Currentverion\` 다음을 입력 합니다.

```
logman create cfg cfg_log -reg HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Currentverion\\
```

데이터베이스 열에서 모든 WMI 개체를 기록 하는 cfg_log 라는 구성 데이터 수집기 `root\wmi` `MSNdis_Vendordriverversion` 를 만들려면 다음을 입력 합니다.

```
logman create cfg cfg_log -mgt root\wmi:select * FROM MSNdis_Vendordriverversion
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [logman 업데이트 cfg 명령](logman-update-cfg.md)

- [logman 명령](logman.md)
