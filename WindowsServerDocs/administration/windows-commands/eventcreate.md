---
title: eventcreate
description: 관리자가 지정 된 이벤트 로그에 사용자 지정 이벤트를 만들 수 있도록 하는 eventcreate 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f2b1b26d-a70e-49a6-832b-91eb5a1a159a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 60ed97eeffc8ae2410fdd8f296a0e8348f376652
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925313"
---
# <a name="eventcreate"></a>eventcreate

관리자가 지정된 된 이벤트 로그에서 사용자 지정 이벤트를 만들 수 있습니다.

> [!IMPORTANT]
> 사용자 지정 이벤트는 보안 로그에 쓸 수 없습니다.

## <a name="syntax"></a>구문

```
eventcreate [/s <computer> [/u <domain\user> [/p <password>]] {[/l {APPLICATION|SYSTEM}]|[/so <srcname>]} /t {ERROR|WARNING|INFORMATION|SUCCESSAUDIT|FAILUREAUDIT} /id <eventID> /d <description>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- |------------ |
| /s`<computer>` | 이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다. |
| /u`<domain\user>` | 또는로 지정 된 사용자의 계정 권한으로 명령을 실행 합니다 `<user>` `<domain\user>` . 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한. |
| /p`<password>` | 에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다. |
| /l`{APPLICATION | SYSTEM}` | 이벤트 만들어지는 이벤트 로그의 이름을 지정 합니다. 유효한 로그 이름은 **응용 프로그램** 또는 **시스템**입니다. |
| /so`<srcname>` | 이벤트에 사용할 소스를 지정 합니다. 올바른 소스 모든 문자열이 될 수 있으며 애플리케이션 또는 이벤트를 생성 하는 구성 요소를 나타내야 합니다. |
| /t`{ERROR | WARNING | INFORMATION | SUCCESSAUDIT | FAILUREAUDIT}` | 만들 이벤트의 유형을 지정 합니다. 유효한 유형은 **ERROR**, **WARNING**, **INFORMATION**, **SUCCESSAUDIT**및 **FAILUREAUDIT**입니다. |
| 더불어`<eventID>` | 이벤트에 대 한 이벤트 ID를 지정합니다. 유효한 ID는 1에서 1000 사이의 숫자입니다. |
| d`<description>` | 새로 만든된 이벤트에 사용할 설명을 지정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

다음 예에서는 **eventcreate** 명령을 사용 하는 방법을 보여 줍니다.

```
eventcreate /t error /id 100 /l application /d Create event in application log
eventcreate /t information /id 1000 /so winmgmt /d Create event in WinMgmt source
eventcreate /t error /id 2001 /so winword /l application /d new src Winword in application log
eventcreate /s server /t error /id 100 /l application /d Remote machine without user credentials
eventcreate /s server /u user /p password /id 100 /t error /l application /d Remote machine with user credentials
eventcreate /s server1 /s server2 /u user /p password /id 100 /t error /so winmgmt /d Creating events on Multiple remote machines
eventcreate /s server /u user /id 100 /t warning /so winmgmt /d Remote machine with partial user credentials
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
