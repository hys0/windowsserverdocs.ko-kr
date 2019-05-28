---
title: ksetup:removerealm
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 39f0c6f0-4c50-4781-941e-0893495405e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 579b0772e4642389b90aa370dad80a3eebea9d34
ms.sourcegitcommit: 08eba714d3ceb5f2dfb5486d6b990da1aa4dcbdd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65564724"
---
# <a name="ksetupremoverealm"></a>ksetup:removerealm



레지스트리에서 지정한 영역에 대 한 모든 정보를 삭제합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /removerealm <RealmName>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<RealmName>|영역 이름은 CORP. 같은 대문자는 DNS 이름으로 지정 됩니다. CONTOSO.COM 하며 기본 영역으로 표시 되 면 **ksetup** 실행 됩니다.|

## <a name="remarks"></a>설명

영역 이름은 레지스트리에 두 위치에 저장 됩니다. **HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001** 하 고 **\CurrentControlSet\Control\Lsa\Kerberos**합니다.

이렇게 하면 해당 DNS 정보를 다시 설정 하 고 제거 해야 도메인 컨트롤러를 사용할 수 없는 때문에 도메인 컨트롤러에서 기본 영역 이름을 제거할 수 없습니다.

## <a name="BKMK_Examples"></a>예제

실수로 영역 이름을 설정 ".COM"를 잘못 입력 하 여 로컬 컴퓨터의 CORP. CONTOSO입니다. CON
```
ksetup /setrealm CORP.CONTOSO.CON
```
로컬 컴퓨터에서 해당 잘못 된 영역 이름을 제거 합니다.
```
ksetup /removerealm CORP.CONTOSO.CON
```
실행 하 여 제거를 확인 하십시오 **ksetup** 출력을 검토 합니다.

#### <a name="additional-references"></a>추가 참조

-   [Ksetup](ksetup.md)
-   [Ksetup:setrealm](ksetup-setrealm.md)
-   [명령줄 구문 키](command-line-syntax-key.md)