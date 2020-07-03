---
title: nslookup ls
description: DNS 도메인 정보를 나열 하는 nslookup ls 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f15f06fe-67e7-41a9-93b5-192ab14ab380
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7c0c0aeb01cdffb1f2b779178f0298e1f120348e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936571"
---
# <a name="nslookup-ls"></a>nslookup ls

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

DNS 도메인 정보를 나열 합니다.

## <a name="syntax"></a>구문

```
ls [<option>] <DNSdomain> [{[>] <filename>|[>>] <filename>}]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<option>` | 유효한 옵션은 다음과 같습니다.<ul><li>**-t:** 지정 된 형식의 모든 레코드를 나열 합니다. 자세한 내용은 [nslookup set querytype](nslookup-set-querytype.md)를 참조 하세요.</li><li>**-a:** DNS 도메인에 있는 컴퓨터의 별칭을 나열 합니다. 이 매개 변수는 **-t CNAME** 와 동일 합니다.</li><li>**-d:** DNS 도메인에 대 한 모든 레코드를 나열 합니다. 이 매개 변수는 **-t ANY** 와 동일 합니다.</li><li>**-h:** DNS 도메인에 대 한 CPU 및 운영 체제 정보를 나열 합니다. 이 매개 변수는 **-t HINFO** 와 동일 합니다.</li><li>**-s:** DNS 도메인에 있는 컴퓨터의 잘 알려진 서비스를 나열 합니다. 이 매개 변수는 **-t WKS**와 동일 합니다. |
| `<DNSdomain>` | 정보를 표시할 수 있는 DNS 도메인을 지정 합니다. |
| `<filename>` | 저장 된 출력에 사용할 파일 이름을 지정 합니다. 보다 큼 ( `>` ) 및 이중 보다 큼 () 문자를 사용 `>>` 하 여 출력을 일반적인 방식으로 리디렉션할 수 있습니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |
| /help | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 이 명령의 기본 출력은 컴퓨터 이름 및 연결 된 IP 주소를 포함 합니다.

- 출력을 파일로 보내는 경우 서버에서 받은 모든 50 레코드에 대 한 해시 표시가 추가 됩니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [nslookup set querytype](nslookup-set-querytype.md)
