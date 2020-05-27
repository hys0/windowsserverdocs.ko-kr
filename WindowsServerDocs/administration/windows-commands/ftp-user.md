---
title: ftp 사용자
description: 원격 컴퓨터에 대 한 사용자를 지정 하는 ftp 사용자 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0a77bfeb-27a9-4f2f-a3c4-2fef529fb569
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f0773084ee718db37d6c79009d66d754283f94c8
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820263"
---
# <a name="ftp-user"></a>ftp 사용자

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 컴퓨터에 사용자를 지정합니다.

## <a name="syntax"></a>구문

```
user <username> [<password>] [<account>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<username>` | 원격 컴퓨터에 로그온 하는 데 사용할 사용자 이름을 지정 합니다. |
| `[<password>]` | *사용자 이름의*암호를 지정 합니다. 암호를 지정 하지 않은 경우 암호를 입력 하 라는 **ftp** 메시지가 표시 됩니다. |
| `[<account>]` | 원격 컴퓨터에 로그온 하는 데 사용할 계정을 지정 합니다. *계정이* 지정 되지 않지만 필요한 경우 **ftp** 명령에서 해당 계정을 확인 합니다. |

### <a name="examples"></a>예

암호 *Password1*를 사용 하 여 *User1* 을 지정 하려면 다음을 입력 합니다.

```
user User1 Password1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
