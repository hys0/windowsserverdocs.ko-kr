---
title: nslookup set domain
description: 기본 DNS (Domain Name System) 도메인 이름을 지정 된 이름으로 변경 하는 nslookup 도메인 설정 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9d4d28e8-6e88-42cc-801f-94e9d8e051f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e672bf53e655ef12cadb2a30aaa377b24e49afec
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721636"
---
# <a name="nslookup-set-domain"></a>nslookup set domain

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기본 DNS (Domain Name System) 도메인 이름을 지정 된 이름으로 변경 합니다.

## <a name="syntax"></a>구문

```
set domain=<domainname>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| `<domainname>` | 기본 DNS 도메인 이름에 대 한 새 이름을 지정합니다. 기본값은 호스트의 이름입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |
| /help | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 기본 DNS 도메인 이름 상태에 따라 조회 요청에 추가 됩니다는 **defname** 및 **검색** 옵션입니다.

- DNS 도메인 검색 목록 두 개 이상의 구성 요소 이름에 있으면 기본 DNS 도메인의 부모를 포함 합니다. 예를 들어, 기본 DNS 도메인이 mfg.widgets.com 이면 mfg.widgets.com와 widgets.com 검색 목록 이름은입니다.

- [Nslookup set srchlist](nslookup-set-srchlist.md) 명령을 사용 하 여 다른 목록을 지정 하 고 [nslookup set all](nslookup-set-all.md) 명령을 사용 하 여 목록을 표시 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [nslookup set srchlist](nslookup-set-srchlist.md)

- [nslookup set all](nslookup-set-all.md)
