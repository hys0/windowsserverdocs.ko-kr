---
title: 'ksetup: 상태를'
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ef2f7b8-97af-4f42-9542-cff324840637
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 46f827d26d867392db4cbef92cf5be496aee8d74
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841516"
---
# <a name="ksetupdumpstate"></a>ksetup: 상태를



컴퓨터에 정의 된 모든 영역에 대 한 영역 설정의 현재 상태를 표시 합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /dumpstate
```

#### <a name="parameters"></a>매개 변수

없음

## <a name="remarks"></a>주의

이 명령의 출력은 기본 영역 (컴퓨터의 구성원 인 도메인)를 포함 하 고이 컴퓨터에 정의 된 모든 영역입니다. 다음 각 영역에 대 한 포함 되어 있습니다.
-   모든 키 배포 센터 (Kdc)이이 영역에 연관 된
-   모든는 **집합 영역** 이 영역에 대 한 플래그
-   KDC 암호

이 명령은 DNS 검색 또는 명령 **ksetup/domain**에서 지정한 도메인 이름을 표시 하지 않습니다.

이 명령은 명령을 사용 하 여 설정 된 컴퓨터 암호를 표시 하지 않습니다 **ksetup /setcomputerpassword**합니다.

**Ksetup** 동일한 출력을 생성 **ksetup /dumpstate**합니다.

## <a name="examples"></a><a name=BKMK_Examples></a>예와

컴퓨터에서 Kerberos 영역 구성의 대부분을 찾을:
```
ksetup /dumpstate
```

## <a name="additional-references"></a>추가 참조

-   [Ksetup](ksetup.md)
-   - [명령줄 구문 키](command-line-syntax-key.md)