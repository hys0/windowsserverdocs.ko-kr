---
title: 'ksetup: delhosttorealmmap'
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3faee482-a96c-4614-86fd-aaa446643ec4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 70b54aaebc0b7b46c34c6f52e45f6583afd6c477
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375154"
---
# <a name="ksetupdelhosttorealmmap"></a>ksetup: delhosttorealmmap



명시 된 호스트와 영역 간의 SPN (서비스 사용자 이름) 매핑을 제거 합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /delhosttorealmmap <HostName> <RealmName>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<HostName >|호스트 이름은 컴퓨터 이름이 며 컴퓨터의 정규화 된 도메인 이름으로 지정할 수 있습니다.|
|@no__t 0RealmName >|영역 이름은 CORP. 같은 대문자는 DNS 이름으로 명시 CONTOSO.COM입니다.|

## <a name="remarks"></a>설명

영역에 대 한 호스트 (또는 영역에 대 한 여러 호스트) 매핑이 있는 경우이 명령은 해당 매핑을 제거 합니다.

매핑은 **HKEY_LOCAL_MACHINE\SYSTEM\CurrentContolSet\Lsa\Kerberos\HostToRealm**의 레지스트리에 기록 됩니다. 이 명령을 사용한 후 레지스트리에서 매핑을 확인 해야 합니다.

## <a name="BKMK_Examples"></a>예와

영역 CONTOSO의 구성을 변경 하 여 호스트 컴퓨터 IPops897의 매핑을 영역으로 삭제 합니다.
```
ksetup /delhosttorealmmap IPops897 CONTOSO
```
이 명령을 실행 한 후 레지스트리에서 매핑을 확인할 수 있습니다.

#### <a name="additional-references"></a>추가 참조

-   [Ksetup:addhosttorealmmap](ksetup-addhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   [명령줄 구문 키](command-line-syntax-key.md)