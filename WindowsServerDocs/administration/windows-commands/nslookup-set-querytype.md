---
title: nslookup set querytype
description: 쿼리의 리소스 레코드 종류를 변경 하는 nslookup set querytype 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5af54ac5-fc1a-4af6-977b-f8e97c8eba90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c54671d23fb7fd9500ba7aac1d59cf50fef78ead
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721612"
---
# <a name="nslookup-set-querytype"></a>nslookup set querytype

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

쿼리에 대 한 리소스 레코드 종류를 변경합니다. 리소스 레코드 종류에 대 한 자세한 내용은 [요청 설명 (Rfc) 1035](https://tools.ietf.org/html/rfc1035)을 참조 하세요.

> [!NOTE]
> 이 명령은 [nslookup set type](nslookup-set-type.md) 명령과 동일 합니다.

## <a name="syntax"></a>구문

```
set querytype=<resourcerecordtype>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| `<resourcerecordtype>` | DNS 리소스 레코드 종류를 지정합니다. 기본 리소스 레코드 형식은 이지만 다음 값 중 **하나를 사용할**수 있습니다.<ul><li>**A:** 컴퓨터의 IP 주소를 지정 합니다.</li><li>**ANY:** 컴퓨터의 IP 주소를 지정 합니다.</li><li>**CNAME:** 별칭의 정식 이름을 지정 합니다.</li><li>**GID** 그룹 이름의 그룹 식별자를 지정 합니다.</li><li>**HINFO:** 컴퓨터의 CPU 및 운영 체제 유형을 지정 합니다.</li><li>**MB:** 사서함 도메인 이름을 지정 합니다.</li><li>**MG:** 메일 그룹 구성원을 지정 합니다.</li><li>**MINFO:** 사서함 또는 메일 목록 정보를 지정 합니다.</li><li>**MR:** 메일 이름 바꾸기 도메인 이름을 지정 합니다.</li><li>**MX:** 메일 교환기를 지정 합니다.</li><li>**NS:** 명명 된 영역에 대 한 DNS 이름 서버를 지정 합니다.</li><li>**PTR:** 쿼리가 IP 주소인 경우 컴퓨터 이름을 지정 합니다. 그렇지 않으면 다른 정보에 대 한 포인터를 지정 합니다.</li><li>**SOA:** DNS 영역에 대 한 권한을 지정 합니다.</li><li>**TXT:** 텍스트 정보를 지정 합니다.</li><li>**UID:** 사용자 식별자를 지정 합니다.</li><li>**Uinfo:** 사용자 정보를 지정 합니다.</li><li>**WKS:** 잘 알려진 서비스에 대해 설명 합니다.</li></ul> |
| /? | 명령 프롬프트에 도움말을 표시합니다. |
| /help | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [nslookup set type](nslookup-set-type.md)
