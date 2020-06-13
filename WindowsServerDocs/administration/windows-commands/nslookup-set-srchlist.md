---
title: nslookup set srchlist
description: 기본 DNS (Domain Name System) 도메인 이름 및 검색 목록을 변경 하는 nslookup set srchlist 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8486266d-22ac-4ce5-aad6-1cd0c08110a2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ed9bbce1910324c4cae5da4228a6d3d1f269d050
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721403"
---
# <a name="nslookup-set-srchlist"></a>nslookup set srchlist

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기본 도메인 이름 시스템 (DNS) 도메인 이름 및 검색 목록을 변경합니다. 이 명령은 [nslookup 도메인 설정](nslookup-set-domain.md) 명령의 기본 DNS 도메인 이름 및 검색 목록을 재정의 합니다.

## <a name="syntax"></a>구문

```
set srchlist=<domainname>[/...]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| `<domainname>` | 기본 DNS 도메인 및 검색 목록에 대 한 새 이름을 지정합니다. 기본 도메인 이름 값은 호스트 이름을 기반으로 합니다. 최대 6 개의 이름 슬래시 (/) 구분 하 여 지정할 수 있습니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |
| /help | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- [Nslookup set all](nslookup-set-all.md) 명령을 사용 하 여 목록을 표시 합니다.

### <a name="examples"></a>예제

DNS 도메인을 *mfg.widgets.com* 로 설정 하 고 검색 목록을 세 개의 이름으로 설정 합니다.

```
set srchlist=mfg.widgets.com/mrp2.widgets.com/widgets.com
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [nslookup set domain](nslookup-set-domain.md)

- [nslookup set all](nslookup-set-all.md)
