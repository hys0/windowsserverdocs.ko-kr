---
title: logman 경고 만들기
description: 경고 데이터 수집기를 만드는 logman 경고 만들기 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 93e6fc2b-5bf5-413b-84b4-be8b9dd3a57d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d84dd52dd9d2d8ca45dc42df88a59cd4c16b54c
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820483"
---
# <a name="logman-create-alert"></a>logman 경고 만들기

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

경고 데이터 수집기를 만듭니다.

## <a name="syntax"></a>구문

```
logman create alert <[-n] <name>> [options]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| -s`<computer name>` | 지정된 된 원격 컴퓨터에서 명령을 수행 합니다. |
| -config`<value>` | 명령 옵션을 포함 하는 설정 파일을 지정 합니다. |
| [-n]`<name>` | 대상 개체의 이름입니다. |
| -[-] u`<user [password]>` | 사용자 계정으로 실행을 지정합니다. 암호에 `*` 대 한를 입력 하면 암호를 묻는 메시지가 생성 됩니다. 암호는 암호 프롬프트에 입력할 때 표시되지 않습니다. |
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
| -cf`<filename>` | 수집할 성능 카운터를 나열 하는 파일을 지정 합니다. 파일에는 줄당 하나의 성능 카운터 이름을 포함 되어야 합니다. |
| -[-] el | 이벤트 로그 보고를 사용 하지 않도록 설정 하거나 사용 합니다. |
| -번째`<threshold [threshold [...]]>` | 카운터와 경고의 임계값을 지정 합니다. |
| -[-] rdcs`<name>` | 경고가 발생할 때 시작 하도록 데이터 수집기 집합을 지정 합니다. |
| -[-] tn`<task>` | 경고가 발생할 때 실행 되도록 작업을 지정 합니다. |
| -[-]targ`<argument>` | -Tn를 사용 하 여 지정한 작업에 사용할 작업 인수를 지정 합니다. |
| /? | 도움말 상황에 맞는 표시 합니다. |

#### <a name="remarks"></a>설명

- 여기서 [-]이 나열 되 고, 추가 하이픈 (-)을 추가 하면 옵션이 무시 됩니다.

### <a name="examples"></a>예

프로세서 (_Total) 카운터 그룹의 성능 카운터% Processor time이 50의 카운터 값을 초과할 때 발생 하는 *new_alert*이라는 새 경고를 만들려면 다음을 입력 합니다.

```
logman create alert new_alert -th \Processor(_Total)\% Processor time>50
```

> [!NOTE]
> 정의 된 임계값은 카운터에 의해 수집 된 값을 기반으로 하기 때문에이 예제에서 50 값은 50% 프로세서 시간에 해당 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [logman](logman.md)
