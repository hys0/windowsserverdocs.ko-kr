---
title: 'ksetup: addhosttorealmmap'
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: e6a28c6001707fac245de7136b5fb5bd38495027
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375653"
---
# <a name="ksetupaddhosttorealmmap"></a>ksetup: addhosttorealmmap



명시 된 호스트와 영역 사이에 SPN (서비스 사용자 이름) 매핑을 추가 합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /addhosttorealmmap <HostName> <RealmName>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<호스트 이름 >|호스트 이름은 컴퓨터 이름이 며 컴퓨터의 정규화 된 도메인 이름으로 지정할 수 있습니다.|
|\<RealmName >|영역 이름은 CORP. 같은 대문자는 DNS 이름으로 명시 CONTOSO.COM입니다.|

## <a name="remarks"></a>설명

이 명령을 사용 하면 동일한 DNS 접미사를 공유 하는 여러 호스트 또는 호스트를 영역에 매핑할 수 있습니다.

매핑은 **HKEY_LOCAL_MACHINE \system\currentcontolset\lsa\kerberos\hosttorealm**의 레지스트리에 기록 됩니다.

## <a name="BKMK_Examples"></a>예와

영역 CONTOSO를 구성 하는 과정에서 호스트 컴퓨터 IPops897를 영역에 매핑합니다.
```
ksetup /addhosttorealmmap IPops897 CONTOSO
```
레지스트리에서 매핑이 올바른지 확인 합니다.

#### <a name="additional-references"></a>추가 참조

-   [Ksetup:delhosttorealmmap](ksetup-delhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   [명령줄 구문 키](command-line-syntax-key.md)