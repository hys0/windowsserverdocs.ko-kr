---
title: nslookup server
description: 지정 된 DNS (Domain Name System) 도메인으로 기본 서버를 변경 하는 nslookup 서버 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 608267f8-f7b4-412a-8dcd-e08b5ffc2085
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ec66534d475502ee68f9fabb58b214d25e6e0aaf
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931266"
---
# <a name="nslookup-server"></a>nslookup server

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 도메인 이름 시스템 (DNS) 도메인에 기본 서버를 변경합니다.

이 명령은 현재 기본 서버를 사용 하 여 지정 된 DSN 도메인에 대 한 정보를 조회 합니다. 초기 서버를 사용 하 여 정보를 조회 하려면 [nslookup](nslookup-lserver.md) 명령을 사용 합니다.

## <a name="syntax"></a>구문

```
server <DNSdomain>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<DNSdomain>` | 기본 서버에 대 한 DNS 도메인을 지정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |
| /help | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [nslookup lserver](nslookup-lserver.md)
