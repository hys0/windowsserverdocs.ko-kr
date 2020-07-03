---
title: ksetup setrealm
description: Kerberos 영역의 이름을 설정 하는 ksetup setrealm 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ab268c40-276b-46ef-ab16-d5ce7667fbed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c6fa5573322237dfee5909d9afc2e99696ac82b3
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933130"
---
# <a name="ksetup-setrealm"></a>ksetup setrealm

Kerberos 영역의 이름을 설정합니다.

> [!IMPORTANT]
> 도메인 컨트롤러에서 Kerberos 영역을 설정 하는 것은 지원 되지 않습니다. 이렇게 하려고 하면 경고와 명령 오류가 발생 합니다.

## <a name="syntax"></a>구문

```
ksetup /setrealm <DNSdomainname>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<DNSdomainname>` | CORP와 같은 대문자 DNS 이름을 지정 합니다. CONTOSO.COM. 정규화 된 도메인 이름 또는 간단한 형식의 이름을 사용할 수 있습니다. DNS 이름에 대문자를 사용 하지 않는 경우 계속 하려면 확인을 요청 하는 메시지가 표시 됩니다. |

### <a name="examples"></a>예

이 컴퓨터의 영역을 특정 도메인 이름으로 설정 하 고 비 도메인 컨트롤러에서 CONTOSO Kerberos 영역 으로만 액세스를 제한 하려면 다음을 입력 합니다.

```
ksetup /setrealm CONTOSO
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ksetup 명령](ksetup.md)

- [ksetup removerealm](ksetup-removerealm.md)
