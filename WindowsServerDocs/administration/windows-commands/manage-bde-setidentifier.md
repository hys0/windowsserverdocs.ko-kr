---
title: manage-bde setidentifier
description: Manage-bde setidentifier command에 대 한 참조 문서-드라이브의 드라이브 식별자 필드를 조직에 대 한 고유 식별자 제공 그룹 정책 설정에 지정 된 값으로 설정 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7092d18f-4ac9-4c73-a20f-1246ca60e75e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d20120bf4c6ec76fa6ba040141afadea2a748d5
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922251"
---
# <a name="manage-bde-setidentifier"></a>manage-bde setidentifier

드라이브 식별자 필드에 지정 된 값을 드라이브에 설정 된 **조직에 대 한 고유 식별자를 제공** 그룹 정책 설정.

## <a name="syntax"></a>구문

```
manage-bde –setidentifier <drive> [-computername <name>] [{-?|/?}] [{-help|-h}]
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

C에 대 한 BitLocker 드라이브 식별자 필드를 설정 하려면 다음을 입력 합니다.

```
manage-bde –setidentifier C:
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [manage-bde 명령](manage-bde.md)

- [BitLocker 복구 가이드](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-recovery-guide-plan)
