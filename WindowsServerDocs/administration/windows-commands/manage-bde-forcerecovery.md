---
title: manage-bde forcerecovery
description: Forcerecovery 명령에 대 한 참조 항목으로, 다시 시작 시 BitLocker로 보호 된 드라이브를 복구 모드로 강제로 적용 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eecae37c-c9a3-46c5-b615-a0ace1f1d778
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e152a18137925bd197e672531ccef47e7b2a7119
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222898"
---
# <a name="manage-bde-forcerecovery"></a>manage-bde forcerecovery

BitLocker로 보호 된 드라이브를 복구 모드로 다시 시작 되도록합니다. 이 명령은 드라이브에서 모든 신뢰할 수 있는 플랫폼 모듈 TPM 관련 키 보호기를 삭제합니다. 컴퓨터 다시 시작 되 면 복구 암호 또는 복구 키만 데 사용할 수 드라이브의 잠금을 해제 합니다.

## <a name="syntax"></a>구문

```
manage-bde –forcerecovery <drive> [-computername <name>] [{-?|/?}] [{-help|-h}]
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

C 드라이브의 복구 모드에서 BitLocker를 시작 하려면 다음을 입력 합니다.

```
manage-bde –forcerecovery C:
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [manage-bde 명령](manage-bde.md)
