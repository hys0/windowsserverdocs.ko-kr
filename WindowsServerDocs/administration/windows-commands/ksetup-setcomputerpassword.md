---
title: ksetup setcomputerpassword
description: 로컬 컴퓨터의 암호를 설정 하는 ksetup setcomputerpassword 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e307d8f6-3b93-4c24-ac04-f31549f7dc7d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 70af854838e439532e49d6159b010e453d339244
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922612"
---
# <a name="ksetup-setcomputerpassword"></a>ksetup setcomputerpassword

로컬 컴퓨터에 대 한 암호를 설정합니다. 이 명령은 컴퓨터 계정에만 영향을 주고 암호 변경을 적용 하려면 다시 시작 해야 합니다.

> [!IMPORTANT]
> 컴퓨터 계정 암호가 레지스트리에 표시 되지 않거나 **ksetup** 명령의 출력으로 표시 되지 않습니다.

## <a name="syntax"></a>구문

```
ksetup /setcomputerpassword <password>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<password>` | 로컬 컴퓨터의 컴퓨터 계정을 설정 하기 위해 제공 된 암호를 지정 합니다. 암호는 관리자 권한이 있는 계정을 사용 하 여 설정할 수 있으며 암호는 1 ~ 156 영숫자 또는 특수 문자 여야 합니다. |

### <a name="examples"></a>예

로컬 컴퓨터의 컴퓨터 계정 암호를 *IPops897* 에서 *ipop $897!* 로 변경 하려면 다음을 입력 합니다.

```
ksetup /setcomputerpassword IPop$897!
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ksetup 명령](ksetup.md)
