---
title: 'ksetup: 도메인'
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ef766e3-6071-44f2-946b-22ea5b61a508
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f127eaf33e9ef6d597851c31a4167ceaa3516abb
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724681"
---
# <a name="ksetupdomain"></a>ksetup: 도메인



모든 Kerberos 작업에 대 한 도메인 이름을 설정합니다.

## <a name="syntax"></a>구문

```
ksetup /domain <DomainName>
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<DomainName>|연결을 설정 하려는 도메인 이름입니다. 정규화 된 도메인 이름 또는 간단한 형태의 contoso.com 또는 contoso과 같은 이름 사용 합니다.|

## <a name="remarks"></a>설명

없음

## <a name="examples"></a>예

예: Microsoft /mapuser 하위 명령을 사용 하 여 올바른 도메인에 대 한 연결을 설정 합니다.
```
ksetup /mapuser principal@realm domain-user /domain domain-name
```
연결 되 면 새 표시 됩니다 TGT 또는 기존 TGT는 새로 고칠 수 있습니다.

## <a name="additional-references"></a>추가 참조

-   [Ksetup](ksetup.md)
-   - [명령줄 구문 키](command-line-syntax-key.md)