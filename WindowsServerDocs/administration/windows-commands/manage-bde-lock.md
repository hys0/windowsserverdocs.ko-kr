---
title: manage-bde 잠금
description: 잠금 해제 키가 제공 되지 않은 경우 BitLocker로 보호 된 드라이브를 잠가 액세스를 방지 하는 manage-bde lock 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b8858e61-3a7e-4d03-8c98-5c09853f35e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b67342579c827ad195ddf506e529fbfb370a6d94
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931621"
---
# <a name="manage-bde-lock"></a>manage-bde 잠금

BitLocker로 보호 된 드라이브를 잠금 해제 키가 제공 되지 않는 경우에 대 한 액세스를 방지 잠금을 설정 합니다.

## <a name="syntax"></a>구문

```
manage-bde -lock [<drive>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<drive>` | 드라이브 문자를 뒤에 콜론을 나타냅니다. |
| -computername | 다른 컴퓨터에서 BitLocker 보호를 수정 하는 데 manage-bde.exe를 사용 하도록 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다. |
| `<name>` | BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다. |
| -? 또는 /? | 도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다. |
| -help 또는-h | 명령 프롬프트에서 전체 도움말을 표시 합니다. |

### <a name="examples"></a>예

데이터 드라이브 D를 잠그려면 다음을 입력 합니다.

```
manage-bde –lock D:
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [manage-bde 명령](manage-bde.md)
