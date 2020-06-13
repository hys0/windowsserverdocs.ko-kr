---
title: nslookup set
description: 조회가 동작 하는 방식에 영향을 주는 구성 설정을 변경 하는 nslookup set 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1fe5b36d-e93e-468b-abca-43b0204b32d1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 579334b3b6b0cd5e9373876144f46fa21d57c745
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721186"
---
# <a name="nslookup-set"></a>nslookup set

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

구성 설정에 영향을 주는 변경 방법을 조회 함수입니다.

## <a name="syntax"></a>구문

```
set all [class | d2 | debug | domain | port | querytype | recurse | retry | root | search | srchlist | timeout | type | vc] [options]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| [nslookup set all](nslookup-set-all.md) | 모든 현재 설정을 나열 합니다. |
| [nslookup set class](nslookup-set-class.md) | 정보의 프로토콜 그룹을 지정 하는 쿼리 클래스를 변경 합니다. |
| [nslookup set d2](nslookup-set-d2.md) | 자세한 디버깅 모드를 설정 하거나 해제 합니다. |
| [nslookup set debug](nslookup-set-debug.md) | 디버깅 모드를 완전히 해제 합니다. |
| [nslookup set domain](nslookup-set-domain.md) | 기본 DNS (Domain Name System) 도메인 이름을 지정 된 이름으로 변경 합니다. |
| [nslookup set port](nslookup-set-port.md) | 기본 TCP/UDP 도메인 이름 시스템 (DNS) 이름 서버 포트를 지정 된 값으로 변경 합니다.
| [nslookup set querytype](nslookup-set-querytype.md) | 쿼리에 대 한 리소스 레코드 종류를 변경합니다. |
| [nslookup set recurse](nslookup-set-recurse.md) | 정보를 찾을 수 없는 경우 다른 서버를 쿼리하도록 DNS (Domain Name System) 이름 서버에 지시 합니다. |
| [nslookup set retry](nslookup-set-retry.md) | 재시도 횟수를 설정합니다. |
| [nslookup set root](nslookup-set-root.md) | 쿼리에 사용 되는 루트 서버 이름을 변경 합니다. |
| [nslookup set search](nslookup-set-search.md) | 응답을 받을 때까지 요청에 DNS 도메인 검색 목록에서 도메인 이름 시스템 (DNS) 도메인 이름을 추가 합니다. |
| [nslookup set srchlist](nslookup-set-srchlist.md) | 기본 도메인 이름 시스템 (DNS) 도메인 이름 및 검색 목록을 변경합니다. |
| [nslookup set timeout](nslookup-set-timeout.md) | 초기 조회 요청에 회신을 기다릴 시간 (초) 수를 변경 합니다. |
| [nslookup set type](nslookup-set-type.md) | 쿼리에 대 한 리소스 레코드 종류를 변경합니다. |
| [nslookup set vc](nslookup-set-vc.md) | 서버에 요청을 보낼 때 가상 회로를 사용할지 여부를 지정 합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
