---
title: Scwcmd 롤백
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fd9f89b-0420-420a-ad20-4a328636b1e7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0cd4eeec1113717a40dca43f0320f2db3c4c414e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722129"
---
# <a name="scwcmd-rollback"></a>Scwcmd: 롤백

> 적용 대상: Windows Server 2012 R2, Windows Server 2012

를 사용할 수 있는 가장 최근의 롤백 정책을 적용 하 고 롤백 정책을 삭제 합니다.

## <a name="syntax"></a>구문

```
scwcmd rollback /m:<ComputerName> [/u:<UserName>] [/pw:<Password>]
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/m:\<ComputerName>|NetBIOS 이름, DNS 이름 또는 롤백 작업을 수행할 수 해야 하는 컴퓨터의 IP 주소를 지정 합니다.|
|/u:\<UserName>|원격 롤백을 수행할 때 사용 하는 다른 사용자 계정을 지정 합니다. 기본값은 로그온 된 사용자입니다.|
|/pw:\<암호>|원격 롤백을 수행할 때 사용 하는 대체 사용자 자격 증명을 지정 합니다. 기본값은 로그온 된 사용자입니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

Scwcmd.exe은 Windows Server 2008 R2, Windows Server 2008 또는 Windows Server 2003을 실행 하는 컴퓨터에서 사용할 수만 있습니다.

## <a name="examples"></a>예

보안 정책이 컴퓨터에서 IP 주소 172.16.0.0 롤백하려면 다음을 입력 합니다.
```
scwcmd rollback /m:172.16.0.0
```

## <a name="additional-references"></a>추가 참조

-   - [명령줄 구문 키](command-line-syntax-key.md)