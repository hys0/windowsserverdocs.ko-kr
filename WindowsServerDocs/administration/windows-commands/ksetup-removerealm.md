---
title: ksetup removerealm
description: Ksetup removerealm 명령에 대 한 참조 항목으로, 레지스트리에서 지정 된 영역에 대 한 모든 정보를 삭제 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 39f0c6f0-4c50-4781-941e-0893495405e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5da1be77a3b585e566bfd3b051b2fb391b326f32
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817613"
---
# <a name="ksetup-removerealm"></a>ksetup removerealm

레지스트리에서 지정한 영역에 대 한 모든 정보를 삭제합니다.

영역 이름은 및 아래의 레지스트리에 저장 됩니다 `HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001` `\CurrentControlSet\Control\Lsa\Kerberos` . 이 항목은 기본적으로 레지스트리에 없습니다. [Ksetup addrealmflags](ksetup-addrealmflags.md) 명령을 사용 하 여 레지스트리를 채울 수 있습니다.

> [!IMPORTANT]
> 도메인 컨트롤러에서 기본 영역 이름을 제거할 수 없습니다. DNS 정보를 다시 설정 하 고 제거 하면 도메인 컨트롤러를 사용할 수 없게 될 수 있습니다.

## <a name="syntax"></a>구문

```
ksetup /removerealm <realmname>
```
### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<realmname>` | CORP와 같은 대문자 DNS 이름을 지정 합니다. CONTOSO.COM는 **ksetup** 가 실행 될 때 기본 영역 또는 **영역 =** 으로 나열 됩니다. |

### <a name="examples"></a>예

잘못 된 영역 이름을 제거 하려면 (. 로컬 컴퓨터에서 .COM 대신 CON을 입력 하 고 다음을 입력 합니다.
```
ksetup /removerealm CORP.CONTOSO.CON
```

제거를 확인 하려면 **ksetup** 명령을 실행 하 고 출력을 검토 하면 됩니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ksetup 명령](ksetup.md)

- [ksetup setrealm 명령](ksetup-setrealm.md)
