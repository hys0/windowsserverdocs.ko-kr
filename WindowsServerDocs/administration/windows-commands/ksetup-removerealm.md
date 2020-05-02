---
title: 'ksetup: removerealm'
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 39f0c6f0-4c50-4781-941e-0893495405e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bb7bf4663594a6c164d6495a9ba4cd81942afb79
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724604"
---
# <a name="ksetupremoverealm"></a>ksetup: removerealm



레지스트리에서 지정한 영역에 대 한 모든 정보를 삭제합니다.

## <a name="syntax"></a>구문

```
ksetup /removerealm <RealmName>
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<RealmName>|영역 이름은 CORP와 같은 대문자 DNS 이름으로 명시 됩니다. CONTOSO.COM는 **ksetup** 가 실행 될 때 기본 영역으로 나열 됩니다.|

## <a name="remarks"></a>설명

영역 이름은 **HKEY_LOCAL_MACHINE \system\controlset001** 및 **\CurrentControlSet\Control\Lsa\Kerberos**레지스트리의 두 위치에 저장 됩니다.

도메인 컨트롤러에서 기본 영역 이름을 제거할 수 없습니다. DNS 정보를 다시 설정 하 고 제거 하면 도메인 컨트롤러를 사용할 수 없게 될 수 있습니다.

## <a name="examples"></a>예

실수로 로컬 컴퓨터에서 영역 이름을 잘못 된 이름으로 설정 합니다. CONTOSO.COM. 이라는
```
ksetup /setrealm CORP.CONTOSO.CON
```
로컬 컴퓨터에서 잘못 된 영역 이름을 제거 합니다.
```
ksetup /removerealm CORP.CONTOSO.CON
```
**Ksetup** 를 실행 하 여 제거를 확인 하 고 출력을 검토 합니다.

## <a name="additional-references"></a>추가 참조

-   [Ksetup](ksetup.md)
-   [Ksetup:setrealm](ksetup-setrealm.md)
-   - [명령줄 구문 키](command-line-syntax-key.md)