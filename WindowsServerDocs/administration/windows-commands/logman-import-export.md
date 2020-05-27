---
title: logman 가져오기 및 logman 내보내기
description: XML 파일에서 데이터 수집기 집합을 가져오거나 데이터 수집기 집합을 XML 파일로 내보내는 logman 가져오기 및 logman 내보내기에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c258daba-fb93-47c0-a53b-2fe83ed2c743
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 44a659abc9e364bf10487e93a7937c1cf8d51bbc
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820573"
---
# <a name="logman-import-and-logman-export"></a>logman 가져오기 및 logman 내보내기

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

XML 파일에서 데이터 수집기 집합을 가져오거나 데이터 수집기 집합을 XML 파일로 내보냅니다.

## <a name="syntax"></a>구문

```
logman import <[-n] <name>> <-xml <name>> [options]
logman export <[-n] <name>> <-xml <name>> [options]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| -s`<computer name>` | 지정된 된 원격 컴퓨터에서 명령을 수행 합니다. |
| -config`<value>` | 명령 옵션을 포함 하는 설정 파일을 지정 합니다. |
| [-n]`<name>` | 대상 개체의 이름입니다. |
| -xml`<name>` | 가져오거나 내보낼 XML 파일의 이름입니다. |
| -ets | 는 이벤트 추적 세션에 명령을 저장 하거나 일정을 예약 하지 않고 직접 보냅니다. |
| -[-] u`<user [password]>` | 사용자 계정으로 실행을 지정합니다. 암호에 `*` 대 한를 입력 하면 암호를 묻는 메시지가 생성 됩니다. 암호는 암호 프롬프트에 입력할 때 표시되지 않습니다. |
| -y | 메시지를 표시 하지 않고 모든 질문에 답변 합니다. |
| /? | 도움말 상황에 맞는 표시 합니다. |

### <a name="examples"></a>예

XML 파일 *c:\windows\ perf_log* 를 컴퓨터 *server_1* 에서 *perf_log*라는 데이터 수집기 집합으로 가져오려면 다음을 입력 합니다.

```
logman import perf_log -s server_1 -xml c:\windows\perf_log.xml
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [logman](logman.md)
