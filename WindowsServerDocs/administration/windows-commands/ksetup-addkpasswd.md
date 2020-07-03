---
title: ksetup addkpasswd
description: 영역에 대 한 Kerberos 암호 (kpasswd) 서버 주소를 추가 하는 ksetup addkpasswd 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d3196995-1b38-48ff-ba08-911cfab77317
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2db728684e713df35a39995c8ca95196f0b745ed
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925555"
---
# <a name="ksetup-addkpasswd"></a>ksetup addkpasswd

영역에 대 한 Kerberos 암호 (kpasswd) 서버 주소를 추가 합니다.

## <a name="syntax"></a>구문

```
ksetup /addkpasswd <realmname> [<kpasswdname>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<realmname>` | CORP와 같은 대문자 DNS 이름을 지정 합니다. CONTOSO.COM는 **ksetup** 가 실행 될 때 기본 영역 또는 **영역 =** 으로 나열 됩니다. |
| `<kpasswdname>` | Kerberos 암호 서버를 지정 합니다. Mitkdc.contoso.com과 같은 대/소문자를 구분 하지 않고 정규화 된 도메인 이름으로 명시 됩니다. KDC 이름이 생략 된 경우 Kdc 찾을 DNS는 사용할 수 있습니다. |

#### <a name="remarks"></a>설명

- 워크스테이션 됩니다 인증 하는 수를 지 원하는 Kerberos Kerberos 영역 암호 프로토콜을 변경 하는 경우에 Kerberos 암호 서버를 사용 하 여 Windows 운영 체제를 실행 하는 클라이언트 컴퓨터를 구성할 수 있습니다.

- 한 번에 하나씩 추가 KDC 이름에 추가할 수 있습니다.

### <a name="examples"></a>예

CORP를 구성 합니다. CONTOSO.COM 영역-비 Windows KDC 서버 mitkdc.contoso.com를 암호 서버로 사용 하려면 다음을 입력 합니다.

```
ksetup /addkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```

KDC 이름이 설정 되었는지 확인 하려면를 입력 한 `ksetup` 다음, **kpasswd =** 텍스트를 검색 하 여 출력을 봅니다. 텍스트가 표시 되지 않는 경우 매핑이 구성 되지 않았음을 의미 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ksetup 명령](ksetup.md)

- [ksetup delkpasswd 명령](ksetup-delkpasswd.md)
