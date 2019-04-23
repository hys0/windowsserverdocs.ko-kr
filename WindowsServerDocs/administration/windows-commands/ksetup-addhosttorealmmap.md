---
title: ksetup:addhosttorealmmap
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 237742d5-fa68-466c-b97e-636f489248ea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 25cf258309c94f0efde980018dd5dcf3c7df4d60
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837504"
---
# <a name="ksetupaddhosttorealmmap"></a>ksetup:addhosttorealmmap



명시 된 호스트 사이 영역에 서비스 사용자 이름 (SPN) 매핑을 추가합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /addhosttorealmmap <HostName> <RealmName>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<HostName>|호스트 이름은 컴퓨터 이름 및 컴퓨터의 정규화 된 도메인 이름으로 정의할 수 있습니다.|
|\<RealmName>|영역 이름은 CORP. 같은 대문자는 DNS 이름으로 명시 CONTOSO.COM입니다.|

## <a name="remarks"></a>설명

이 명령은 사용 하는 호스트 또는 영역에는 동일한 DNS 접미사를 공유 하는 여러 호스트에 매핑할 수 있습니다.

매핑을 레지스트리에 기록 됩니다 **HKEY_LOCAL_MACHINE\SYSTEM\CurrentContolSet\Lsa\Kerberos\HostToRealm**합니다.

## <a name="BKMK_Examples"></a>예제

CONTOSO 영역 구성의 일환으로, 호스트 컴퓨터를 IPops897 영역에 매핑됩니다.
```
ksetup /addhosttorealmmap IPops897 CONTOSO
```
레지스트리에서 매핑을 의도 한 대로 인지 확인 합니다.

#### <a name="additional-references"></a>추가 참조

-   [Ksetup:delhosttorealmmap](ksetup-delhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   [명령줄 구문 키](command-line-syntax-key.md)