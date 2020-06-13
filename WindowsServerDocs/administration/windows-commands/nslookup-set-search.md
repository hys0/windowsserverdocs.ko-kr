---
title: nslookup set search
description: 응답을 받을 때까지 요청에 DNS 도메인 검색 목록의 DNS (Domain Name System) 도메인 이름을 추가 하는 nslookup set search 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 064ac660-8b04-4af9-8b2c-e4e0549771b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c3219434f768a573c9e433c44b6b38bc9dc75f14
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721428"
---
# <a name="nslookup-set-search"></a>nslookup set search

응답을 받을 때까지 요청에 DNS 도메인 검색 목록에서 도메인 이름 시스템 (DNS) 도메인 이름을 추가 합니다. 집합과 조회 요청 하나 이상의 기간을 포함 하는 경우에 적용 됩니다 있지만 뒤에 마침표 종료 하지 마십시오.

## <a name="syntax"></a>구문

```
set [no]search
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| nosearch | 요청에 대 한 DNS 도메인 검색 목록에 DNS (Domain Name System) 도메인 이름을 추가 하는 것을 중지 합니다. |
| search | 응답을 받을 때까지 요청에 대 한 dns (Domain Name System) 도메인 이름을 dns 도메인 검색 목록에 추가 합니다. 이것은 기본값입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |
| /help | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
