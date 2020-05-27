---
title: ksetup addhosttorealmmap
description: Ksetup addhosttorealmmap 명령에 대 한 참조 항목으로, 명시 된 호스트와 영역 사이에 SPN (서비스 사용자 이름) 매핑을 추가 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 237742d5-fa68-466c-b97e-636f489248ea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ee2639a5bb071bdd3d6ac3f6373e881c18f3bf9a
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818113"
---
# <a name="ksetup-addhosttorealmmap"></a>ksetup addhosttorealmmap

명시 된 호스트와 영역 사이에 SPN (서비스 사용자 이름) 매핑을 추가 합니다. 이 명령을 사용 하면 동일한 DNS 접미사를 공유 하는 여러 호스트 또는 호스트를 영역에 매핑할 수도 있습니다.

매핑은 **HKEY_LOCAL_MACHINE \system\currentcontolset\lsa\kerberos\hosttorealm**의 레지스트리에 저장 됩니다.

## <a name="syntax"></a>구문

```
ksetup /addhosttorealmmap <hostname> <realmname>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- |------------ |
| `<hostname>` | 호스트 이름은 컴퓨터 이름이 며 컴퓨터의 정규화 된 도메인 이름으로 지정할 수 있습니다. |
| `<realmname>` | 영역 이름은 CORP. 같은 대문자는 DNS 이름으로 명시 CONTOSO.COM입니다. |

### <a name="examples"></a>예

*IPops897* 호스트 컴퓨터를 *CONTOSO* 영역에 매핑하려면 다음을 입력 합니다.

```
ksetup /addhosttorealmmap IPops897 CONTOSO
```

레지스트리를 확인 하 여 매핑이 의도 한 대로 발생 했는지 확인 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ksetup 명령](ksetup.md)

- [ksetup delhosttorealmmap 명령](ksetup-delhosttorealmmap.md)
