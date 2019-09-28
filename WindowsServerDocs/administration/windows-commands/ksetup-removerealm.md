---
title: 'ksetup: removerealm'
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 11858d8a24d4f125c83b3e4092ac48f336a9ef0b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374951"
---
# <a name="ksetupremoverealm"></a>ksetup: removerealm



레지스트리에서 지정한 영역에 대 한 모든 정보를 삭제합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /removerealm <RealmName>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|@no__t 0RealmName >|영역 이름은 CORP와 같은 대문자 DNS 이름으로 명시 됩니다. CONTOSO.COM는 **ksetup** 가 실행 될 때 기본 영역으로 나열 됩니다.|

## <a name="remarks"></a>설명

영역 이름은 레지스트리의 두 위치에 저장 됩니다. **HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001** 및 **\CurrentControlSet\Control\Lsa\Kerberos**.

도메인 컨트롤러에서 기본 영역 이름을 제거할 수 없습니다. DNS 정보를 다시 설정 하 고 제거 하면 도메인 컨트롤러를 사용할 수 없게 될 수 있습니다.

## <a name="BKMK_Examples"></a>예와

로컬 컴퓨터에서 CORP로 영역 이름을 잘못 된 ".COM"으로 설정 합니다. CONTOSO.COM. 이라는
```
ksetup /setrealm CORP.CONTOSO.CON
```
로컬 컴퓨터에서 잘못 된 영역 이름을 제거 합니다.
```
ksetup /removerealm CORP.CONTOSO.CON
```
**Ksetup** 를 실행 하 여 제거를 확인 하 고 출력을 검토 합니다.

#### <a name="additional-references"></a>추가 참조

-   [Ksetup](ksetup.md)
-   [Ksetup:setrealm](ksetup-setrealm.md)
-   [명령줄 구문 키](command-line-syntax-key.md)