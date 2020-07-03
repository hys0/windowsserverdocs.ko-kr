---
title: pubprn
description: Active Directory Domain Services에 프린터를 게시 하는 잘라냅니다 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0bc7f7e3-84e1-4359-b477-7b1a1a0bd639
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c73c79450d4feb4d2567f29bfed56364dea9b5a8
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932012"
---
# <a name="pubprn"></a>pubprn

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory 도메인 서비스에 프린터를 게시합니다. 이 명령은 디렉터리에 있는 Visual Basic 스크립트입니다 `%WINdir%\System32\printing_Admin_Scripts\<language>` . 명령 프롬프트에서이 명령을 사용 하려면 **cscript** 다음에 잘라냅니다 파일의 전체 경로를 입력 하거나 디렉터리를 적절 한 폴더로 변경 합니다. 예를 들어 `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\pubprn`을 참조하십시오.

## <a name="syntax"></a>구문

```
cscript pubprn {<servername> | <UNCprinterpath>} LDAP://CN=<container>,DC=<container>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| `<servername>` | 프린터를 게시 하려면를 호스트 하는 Windows 서버 이름을 지정 합니다. 컴퓨터를 지정 하지 않으면 로컬 컴퓨터가 사용 됩니다. |
| `<UNCprinterpath>` | 게시 하려는 공유 프린터에 대 한 범용 명명 규칙 (UNC) 경로입니다. |
| `LDAP://CN=<Container>,DC=<Container>` | 프린터를 게시 하려면 Active Directory 도메인 서비스에서 컨테이너에 대 한 경로 지정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 사용자가 제공 하는 정보에 공백이 포함 된 경우 텍스트에 따옴표를 사용 합니다 (예: "컴퓨터 이름").

### <a name="examples"></a>예

Server1 컴퓨터의 모든 프린터를 \\ MyDomain.company.com 도메인의 MyContainer 컨테이너에 게시 하려면 다음을 입력 합니다.

```
cscript pubprn Server1 LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com
```

\\\Server1 서버의 Laserprinter1 프린터를 MyDomain.company.com 도메인의 MyContainer 컨테이너에 게시 하려면 다음을 입력 합니다.

```
cscript pubprn \\Server1\Laserprinter1 LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [인쇄 명령 참조](print-command-reference.md)
