---
title: pubprn
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0bc7f7e3-84e1-4359-b477-7b1a1a0bd639
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 499ff2ade7ffc6c608791ba3da0ede0c3282c13d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831704"
---
# <a name="pubprn"></a>pubprn

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active directory Domain Services에 프린터를 게시합니다.

## <a name="syntax"></a>구문
```
cscript pubprn {<ServerName> | <UNCprinterpath>} 
"LDAP://CN=<Container>,DC=<Container>"
```

## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|\<ServerName>|프린터를 게시 하려면를 호스트 하는 Windows 서버 이름을 지정 합니다. 컴퓨터를 지정 하지 않으면 로컬 컴퓨터가 사용 됩니다.|
|\<UNCprinterpath>|게시 하려는 공유 프린터에 대 한 범용 명명 규칙 (UNC) 경로입니다.|
|"LDAP://CN=<Container>,DC =<Container>"|프린터를 게시 하려는 active directory Domain Services에서 컨테이너에 대 한 경로 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명
-   합니다 **pubprn** 명령입니다는 %WINdir%\System32\printing_Admin_Scripts에 있는 Visual Basic 스크립트\\ <language> 디렉터리입니다. 명령 프롬프트에서이 명령을 사용 하려면 입력 **cscript** 전체 경로 뒤에 pubprn 파일 또는 디렉터리 적절 한 폴더로 변경 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\pubprn
    ```
-   텍스트 주위에 따옴표를 사용 하 여 사용자가 제공한 정보에 공백이 있으면 (예를 들어 `"computer Name"`).

## <a name="BKMK_examples"></a>예제
모든 프린터를 게시 하는 \\\Server1 컴퓨터 MyDomain.company.Com 도메인의 MyContainer 컨테이너를 입력 합니다.
```
cscript Ppubprn Server1 "LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com"
```
Laserprinter1 프린터를 게시 하는 \\MyDomain.company.Com 도메인 유형 MyContainer 컨테이너 \Server1 서버:
```
cscript Ppubprn \\Server1\Laserprinter1 "LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com"
```

#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[인쇄 명령 참조](print-command-reference.md)
