---
title: manage-bde autounlock
description: BitLocker로 보호 되는 데이터 드라이브의 자동 잠금 해제를 관리 하는 manage-bde autounlock command에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 063528bf-d235-4b44-887a-52a7d983e01a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a214ba868e04a81e6282dc919c93ab626ef26725
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223009"
---
# <a name="manage-bde-autounlock"></a>manage-bde autounlock

BitLocker로 보호 된 데이터 드라이브 자동 잠금 해제를 관리 합니다.

## <a name="syntax"></a>구문

```
manage-bde -autounlock [{-enable|-disable|-clearallkeys}] <drive> [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| -사용 하도록 설정 | 데이터 드라이브 자동 잠금 해제 수 있습니다. |
| -사용 하지 않도록 설정 | 데이터 드라이브 자동 잠금 해제 하는 사용 하지 않도록 설정 합니다. |
| -clearallkeys | 운영 체제 드라이브에 저장 된 모든 외부 키를 제거합니다. |
| `<drive>` | 드라이브 문자를 뒤에 콜론을 나타냅니다. |
| -computername | 다른 컴퓨터에서 BitLocker 보호를 수정 하는 데 manage-bde.exe를 사용 하도록 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다. |
| `<name>` | BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다. |
| -? 또는 /? | 도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다. |
| -help 또는-h | 명령 프롬프트에서 전체 도움말을 표시 합니다. |

## <a name="examples"></a>예

데이터 드라이브 E의 자동 잠금 해제를 사용 하려면 다음을 입력 합니다.

```
manage-bde –autounlock -enable E:
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [manage-bde 명령](manage-bde.md)