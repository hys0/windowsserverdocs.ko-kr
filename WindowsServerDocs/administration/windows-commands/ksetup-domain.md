---
title: 'ksetup: 도메인'
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2ef766e3-6071-44f2-946b-22ea5b61a508
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0a4d9f09def32c7518046c25887f4154020c5d7e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375120"
---
# <a name="ksetupdomain"></a>ksetup: 도메인



모든 Kerberos 작업에 대 한 도메인 이름을 설정합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /domain <DomainName>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<DomainName >|연결을 설정 하려는 도메인 이름입니다. 정규화 된 도메인 이름 또는 간단한 형태의 contoso.com 또는 contoso과 같은 이름 사용 합니다.|

## <a name="remarks"></a>설명

없음

## <a name="BKMK_Examples"></a>예와

예: Microsoft /mapuser 하위 명령을 사용 하 여 올바른 도메인에 대 한 연결을 설정 합니다.
```
ksetup /mapuser principal@realm domain-user /domain domain-name
```
연결 되 면 새 표시 됩니다 TGT 또는 기존 TGT는 새로 고칠 수 있습니다.

#### <a name="additional-references"></a>추가 참조

-   [Ksetup](ksetup.md)
-   [명령줄 구문 키](command-line-syntax-key.md)