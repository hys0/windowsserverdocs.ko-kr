---
title: 'ksetup: setrealm'
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ab268c40-276b-46ef-ab16-d5ce7667fbed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 453977ac39dd3a52b4f5a3104995f944e4a48392
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724554"
---
# <a name="ksetupsetrealm"></a>ksetup: setrealm



Kerberos 영역의 이름을 설정합니다.

## <a name="syntax"></a>구문

```
ksetup /setrealm <DNSDomainName>
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<DNSDomainName>|DNS 도메인 이름을 간단한 도메인 이름 또는 정규화 된 도메인 이름 형식일 수 있습니다.|

## <a name="remarks"></a>설명

DNS 도메인 이름 매개 변수가 대문자로 입력 해야 합니다. 그렇지 않은 경우는 **ksetup** 명령을 계속 하려면 확인을 묻는 메시지가 표시 됩니다.

도메인 컨트롤러에서 Kerberos 영역을 설정 하는 것은 지원 되지 않습니다. 그렇게 하려고 하면 경고 및 명령 실패 합니다.

## <a name="examples"></a>예

비-도메인 컨트롤러에서 CONTOSO Kerberos 영역에만 액세스를 제한 하는 특정 도메인 이름에이 컴퓨터에 대 한 영역을 설정 합니다.
```
ksetup /setrealm CONTOSO
```

## <a name="additional-references"></a>추가 참조

-   - [명령줄 구문 키](command-line-syntax-key.md)
-   [Ksetup](ksetup.md)
-   [Ksetup:removerealm](ksetup-removerealm.md)