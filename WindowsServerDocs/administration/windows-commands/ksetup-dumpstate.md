---
title: 'ksetup: 상태를'
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ef2f7b8-97af-4f42-9542-cff324840637
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 27a7e3154b9dfa663b88b04857ea7650995613c6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724646"
---
# <a name="ksetupdumpstate"></a>ksetup: 상태를



컴퓨터에 정의 된 모든 영역에 대 한 영역 설정의 현재 상태를 표시 합니다.

## <a name="syntax"></a>구문

```
ksetup /dumpstate
```

#### <a name="parameters"></a>매개 변수

None

## <a name="remarks"></a>설명

이 명령의 출력은 기본 영역 (컴퓨터의 구성원 인 도메인)를 포함 하 고이 컴퓨터에 정의 된 모든 영역입니다. 다음 각 영역에 대 한 포함 되어 있습니다.
-   모든 키 배포 센터 (Kdc)이이 영역에 연관 된
-   모든는 **집합 영역** 이 영역에 대 한 플래그
-   KDC 암호

이 명령은 DNS 검색 또는 명령 **ksetup/domain**에서 지정한 도메인 이름을 표시 하지 않습니다.

이 명령은 명령을 사용 하 여 설정 된 컴퓨터 암호를 표시 하지 않습니다 **ksetup /setcomputerpassword**합니다.

**Ksetup** 동일한 출력을 생성 **ksetup /dumpstate**합니다.

## <a name="examples"></a>예

컴퓨터에서 Kerberos 영역 구성의 대부분을 찾을:
```
ksetup /dumpstate
```

## <a name="additional-references"></a>추가 참조

-   [Ksetup](ksetup.md)
-   - [명령줄 구문 키](command-line-syntax-key.md)