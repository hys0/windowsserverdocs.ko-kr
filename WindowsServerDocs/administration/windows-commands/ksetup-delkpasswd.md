---
title: ksetup delkpasswd
description: 영역에 대 한 Kerberos 암호 서버 (kpasswd)를 제거 하는 ksetup delkpasswd 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2db0bfcd-bc08-48e3-9f30-65b6411839c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 05002c860575bce84748adc2fc353f0994d559ab
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926135"
---
# <a name="ksetup-delkpasswd"></a>ksetup delkpasswd

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

영역에 대 한 Kerberos 암호 서버 (kpasswd)를 제거 합니다.

## <a name="syntax"></a>구문

```
ksetup /delkpasswd <realmname> <kpasswdname>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<realmname>` |  CORP와 같은 대문자 DNS 이름을 지정 합니다. CONTOSO.COM는 **ksetup** 가 실행 될 때 기본 영역 또는 **영역 =** 으로 나열 됩니다. |
| `<kpasswdname>` | Kerberos 암호 서버를 지정 합니다. Mitkdc.contoso.com과 같은 대/소문자를 구분 하지 않고 정규화 된 도메인 이름으로 명시 됩니다. KDC 이름이 생략 된 경우 Kdc 찾을 DNS는 사용할 수 있습니다. |

### <a name="examples"></a>예

영역 CORP를 확인 합니다. CONTOSO.COM는 비 Windows KDC 서버 mitkdc.contoso.com를 암호 서버로 사용 하 고 다음을 입력 합니다.

```
ksetup /delkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```

영역 CORP를 확인 합니다. CONTOSO.COM가 Kerberos 암호 서버 (KDC 이름)에 매핑되지 않고 `ksetup` Windows 컴퓨터에를 입력 한 다음 출력을 확인 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ksetup 명령](ksetup.md)

- [ksetup delkpasswd 명령](ksetup-delkpasswd.md)
