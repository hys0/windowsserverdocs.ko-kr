---
title: ksetup addrealmflags
description: 지정 된 영역에 영역 플래그를 추가 하는 ksetup addrealmflags 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 80ca1e16-8871-494b-b9be-6bc9d63de860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c0862462f47189f4904421943e4d3de55c856ace
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818033"
---
# <a name="ksetup-addrealmflags"></a>ksetup addrealmflags

지정 된 영역에 영역 플래그를 추가 합니다.

## <a name="syntax"></a>구문

```
ksetup /addrealmflags <realmname> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<realmname>` | CORP와 같은 대문자 DNS 이름을 지정 합니다. CONTOSO.COM. |

#### <a name="remarks"></a>설명

- 영역 플래그는 Windows Server 운영 체제를 기반으로 하지 않는 Kerberos 영역의 추가 기능을 지정 합니다. Windows Server를 실행 하는 컴퓨터는 Windows Server 운영 체제를 실행 하는 도메인을 사용 하는 대신 Kerberos 서버를 사용 하 여 Kerberos 영역에서 인증을 관리할 수 있습니다. 이 항목은 다음과 같이 영역 기능을 설정 합니다.

| 값 | 영역 플래그 | 설명 |
| ----- | ---------- | ----------- |
| 0xF를 지정합니다. | 모두 | 모든 영역 플래그를 설정 합니다. |
| 0x00 | None | 영역 플래그는 설정 되지 않으며 추가 기능을 사용할 수 없습니다. |
| 0x01 | sendaddress | IP 주소는 티켓 부여 티켓에 포함 됩니다. |
| 0x02 | tcpsupported | 이 영역에서는 TCP (전송 제어 프로토콜)와 UDP (사용자 데이터 그램 프로토콜)가 모두 지원 됩니다. |
| 0x04 | 대리자(delegate) | 이 영역에 있는 모든 사용자는 위임용으로 트러스트 됩니다. |
| 0x08 | ncsupported | 이 영역은 DNS 및 영역 명명 표준을 허용 하는 이름 정규화를 지원 합니다. |
| 0x80 | rc4 | 이 영역 TLS 사용에 대 한 수 있는 상호 영역 트러스트를 사용 하도록 설정 하려면 RC4 암호화를 지원 합니다. |

- 영역 플래그는의 레지스트리에 저장 됩니다 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\Kerberos\Domains\<realmname>` . 이 항목은 기본적으로 레지스트리에 없습니다. [Ksetup addrealmflags](ksetup-addrealmflags.md) 명령을 사용 하 여 레지스트리를 채울 수 있습니다.

- **Ksetup** 또는의 출력을 확인 하 여 사용 가능한 영역 플래그 및 설정 영역 플래그를 볼 수 있습니다 `ksetup /dumpstate` .

### <a name="examples"></a>예

CONTOSO 영역에 사용할 수 있는 영역 플래그를 나열 하려면 다음을 입력 합니다.

```
ksetup /listrealmflags
```

CONTOSO 영역에 두 개의 플래그를 설정 하려면 다음을 입력 합니다.

```
ksetup /setrealmflags CONTOSO ncsupported delegate
```

현재 집합에 없는 플래그를 하나 더 추가 하려면 다음을 입력 합니다.

```
ksetup /addrealmflags CONTOSO SendAddress
```

영역 플래그가 설정 되었는지 확인 하려면를 입력 하 `ksetup` 고 출력을 확인 하 여 텍스트, **영역 플래그 =** 를 찾습니다. 텍스트가 표시 되지 않으면 플래그가 설정 되지 않았음을 의미 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ksetup 명령](ksetup.md)

- [ksetup listrealmflags 명령](ksetup-listrealmflags.md)

- [ksetup setrealmflags 명령](ksetup-setrealmflags.md)

- [ksetup delrealmflags 명령](ksetup-delrealmflags.md)

- [ksetup ffstate 명령](ksetup-dumpstate.md)
