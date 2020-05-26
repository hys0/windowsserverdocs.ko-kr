---
title: ksetup delhosttorealmmap
description: Ksetup delhosttorealmmap 명령에 대 한 참조 항목으로, 명시 된 호스트와 영역 간에 SPN (서비스 사용자 이름) 매핑을 제거 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3faee482-a96c-4614-86fd-aaa446643ec4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 17fc30e76247c570c653d5ec38501a2199435c7f
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817863"
---
# <a name="ksetup-delhosttorealmmap"></a>ksetup delhosttorealmmap

명시 된 호스트와 영역 간의 SPN (서비스 사용자 이름) 매핑을 제거 합니다. 또한이 명령은 호스트 간 (또는 영역에 대 한 여러 호스트) 간의 매핑을 제거 합니다.

매핑은 레지스트리에 저장 됩니다 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentContolSet\Lsa\Kerberos\HostToRealm` . 이 명령을 실행 한 후 매핑이 레지스트리에 표시 되도록 하는 것이 좋습니다.

## <a name="syntax"></a>구문

```
ksetup /delhosttorealmmap <hostname> <realmname>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<hostname>` | 컴퓨터의 정규화 된 도메인 이름을 지정 합니다. |
| `<realmname>` | CORP와 같은 대문자 DNS 이름을 지정 합니다. CONTOSO.COM. |

### <a name="examples"></a>예

영역 CONTOSO의 구성을 변경 하 고 호스트 컴퓨터 IPops897의 매핑을 영역에 삭제 하려면 다음을 입력 합니다.

```
ksetup /delhosttorealmmap IPops897 CONTOSO
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ksetup 명령](ksetup.md)

- [ksetup addhosttorealmmap 명령](ksetup-addhosttorealmmap.md)
