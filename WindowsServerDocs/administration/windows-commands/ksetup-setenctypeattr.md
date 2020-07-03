---
title: ksetup setenctypeattr
description: 도메인에 대 한 암호화 유형 특성을 설정 하는 ksetup setenctypeattr 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 88fb913e-6b57-48d9-8c16-a035ab2977ac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8bb8411a795d0167af1fc921fdf1c19febcb8527
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933915"
---
# <a name="ksetup-setenctypeattr"></a>ksetup setenctypeattr

도메인에 대 한 암호화 유형 특성을 설정합니다. 성공 또는 실패 완료 시 상태 메시지가 표시 됩니다.

**Klist** 명령을 실행 하 고 출력을 확인 하 여 Kerberos TGT (티켓 허용 티켓) 및 세션 키의 암호화 유형을 볼 수 있습니다. 명령을 실행 하 여 도메인을 연결 하 고 사용 하도록 설정할 수 있습니다 `ksetup /domain <domainname>` .

## <a name="syntax"></a>구문

```
ksetup /setenctypeattr <domainname> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<domainname>` | 연결을 설정 하려는 도메인 이름입니다. 정규화 된 도메인 이름 또는 corp.contoso.com 또는 contoso와 같은 간단한 형식의 이름을 사용 합니다. |
| 암호화 유형 | 다음 지원 되는 암호화 유형 중 하나 여야 합니다.<ul><li>DES---CRC</li><li>DES-MD5</li><li>RC4-HMAC-MD5</li><li>AES128-HMAC-SHA1</li><li>AES256-HMAC-SHA1</li></ul> |

#### <a name="remarks"></a>설명

- 명령의 암호화 유형을 공백으로 구분 하 여 여러 암호화 유형을 설정 하거나 추가할 수 있습니다. 그러나 한 번에 하나의 도메인에 대해서만이 작업을 수행할 수 있습니다.

### <a name="examples"></a>예

Kerberos TGT (티켓 허용 티켓) 및 세션 키의 암호화 유형을 보려면 다음을 입력 합니다.

```
klist
```

도메인을 corp.contoso.com로 설정 하려면 다음을 입력 합니다.

```
ksetup /domain corp.contoso.com
```

암호화 유형 특성을 corp.contoso.com 도메인에 대 한 AES-256-c a s-s h a-96로 설정 하려면 다음을 입력 합니다.

```
ksetup /setenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```

암호화 유형 특성이 도메인에 대해 의도 한 대로 설정 되었는지 확인 하려면 다음을 입력 합니다.

```
ksetup /getenctypeattr corp.contoso.com
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [klist 명령](klist.md)

- [ksetup 명령](ksetup.md)

- [ksetup 도메인 명령](ksetup-domain.md)

- [ksetup addenctypeattr 명령](ksetup-addenctypeattr.md)

- [ksetup getenctypeattr 명령](ksetup-getenctypeattr.md)

- [ksetup delenctypeattr 명령](ksetup-delenctypeattr.md)
