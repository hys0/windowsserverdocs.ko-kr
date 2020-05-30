---
title: manage-bde 꺼짐
description: 드라이브의 암호를 해독 하 고 BitLocker를 끄는 manage-bde off 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0a27c119-d385-45e5-89fe-e311d4429876
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cbcec0cadba870a5f416af50f12e0b2c5eed6d95
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222862"
---
# <a name="manage-bde-off"></a>manage-bde 꺼짐

드라이브를 해독 하 고 BitLocker를 해제 합니다. 암호 해독 완료 되 면 모든 키 보호기 제거 됩니다.

## <a name="syntax"></a>구문

```
manage-bde -off [<volume>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<volume>` | 드라이브 문자 뒤에 콜론, 볼륨 GUID 경로 또는 탑재 된 볼륨을 지정 합니다. |
| -computername | 다른 컴퓨터에서 BitLocker 보호를 수정 하는 데 manage-bde.exe를 사용 하도록 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다. |
| `<name>` | BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다. |
| -? 또는 /? | 도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다. |
| -help 또는-h | 명령 프롬프트에서 전체 도움말을 표시 합니다. |

### <a name="examples"></a>예

C 드라이브에서 BitLocker를 해제 하려면 다음을 입력 합니다.

```
manage-bde –off C:
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [manage-bde on 명령](manage-bde-on.md)

- [manage-bde 일시 중지 명령](manage-bde-pause.md)

- [manage-bde resume 명령](manage-bde-resume.md)

- [manage-bde 명령](manage-bde.md)
