---
title: ksetup 도메인
description: 모든 Kerberos 작업에 대해 도메인 이름을 설정 하는 ksetup 도메인 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ef766e3-6071-44f2-946b-22ea5b61a508
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1d497f2bc76bae8a95b077658c661e0fdc1e93f3
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817803"
---
# <a name="ksetup-domain"></a>ksetup 도메인

모든 Kerberos 작업에 대 한 도메인 이름을 설정합니다.

## <a name="syntax"></a>구문

```
ksetup /domain <domainname>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<domainname>` | 연결을 설정 하려는 도메인 이름입니다. 정규화 된 도메인 이름 또는 contoso.com 또는 contoso와 같은 간단한 형식의 이름을 사용 합니다.|

### <a name="examples"></a>예

하위 명령을 사용 하 여 Microsoft와 같은 유효한 도메인에 연결 하려면 `ksetup /mapuser` 다음을 입력 합니다.

```
ksetup /mapuser principal@realm domain-user /domain domain-name
```

성공적으로 연결 되 면 새 TGT를 받거나 기존 TGT를 새로 고칩니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ksetup 명령](ksetup.md)

- [ksetup mapuser 명령](ksetup-mapuser.md)