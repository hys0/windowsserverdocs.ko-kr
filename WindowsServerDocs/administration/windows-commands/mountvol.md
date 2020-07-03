---
title: mountvol
description: 볼륨 탑재 지점을 만들거나 삭제 하거나 나열 하는 mountvol 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fea8ad4d-f04a-4aaa-a3e5-75931e867b39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1617149fac677069d97b5b7c1353e85b4e1fea14
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936325"
---
# <a name="mountvol"></a>mountvol

만들고, 삭제 또는 볼륨 탑재 지점을 나열 합니다. 드라이브 문자를 요구 하지 않고 볼륨을 연결할 수도 있습니다.

## <a name="syntax"></a>구문

```
mountvol [<drive>:]<path volumename>
mountvol [<drive>:]<path> /d
mountvol [<drive>:]<path> /l
mountvol [<drive>:]<path> /p
mountvol /r
mountvol [/n|/e]
mountvol <drive>: /s
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `[<drive>:]<path>` | 탑재 지점이 있는 기존 NTFS 디렉터리를 지정 합니다. |
| `<volumename>` | 탑재 지점의 대상인 볼륨 이름을 지정 합니다. 볼륨 이름은 다음 구문을 사용 합니다. 여기서 *GUID* 는 전역 고유 식별자 `\\?\volume\{GUID}\` 입니다. 대괄호가 `{ }` 필요 합니다. |
| /d | 지정된 된 폴더의 볼륨 탑재 지점을 제거합니다. |
| /l | 지정된 된 폴더에 탑재 된 볼륨 이름을 나열합니다. |
| /p | 지정된 된 디렉터리에서 볼륨 탑재 지점을 제거 하 고 기본 볼륨을 분리는 기본 볼륨을 오프 라인을 탑재할 수 없게 만드는 합니다. 다른 프로세스에서 볼륨을 사용 하는 경우 **mountvol** 에서 볼륨을 분리 하기 전에 열린 핸들을 닫습니다. |
| /r | 볼륨 탑재 지점 디렉터리와 볼륨을 더 이상 자동으로를 방지 하는 시스템, 및 볼륨에 이전 볼륨 탑재 지점을 시스템에 다시 추가 하는 경우에 대 한 레지스트리 설정을 제거 합니다. |
| /n | 새 기본 볼륨의 자동 탑재를 사용 하지 않도록 설정 합니다. 새 볼륨은 시스템에 추가 될 때 자동으로 탑재 되지 않습니다. |
| /e | 새 기본 볼륨의 자동 탑재를 다시 설정합니다. |
| /s | 지정 된 드라이브에 EFI 시스템 파티션을 탑재합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="remarks"></a>설명

- **/P** 매개 변수를 사용 하는 동안 볼륨을 분리 하는 경우 볼륨 목록에 볼륨 탑재 지점을 만들 때까지 볼륨이 탑재 되지 않음으로 표시 됩니다.

- 볼륨에 둘 이상의 탑재 지점이 있는 경우에는 **/d** 를 사용 하 여 **/p**를 사용 하기 전에 추가 탑재 지점을 제거 합니다. 다시 만들 수 있습니다 기본 볼륨 탑재 가능한 볼륨 탑재 지점을 할당 합니다.

- 를 다시 포맷 하거나 하드 드라이브의 교체 하지 않고 볼륨 공간을 확장 해야 하는 경우 다른 볼륨을 탑재 경로 추가할 수 있습니다. 여러 탑재 경로 볼륨 하나를 사용 하는 이점은 하나의 드라이브 문자를 사용 하 여 모든 로컬 볼륨에 액세스할 수 있는지 (예: `C:`). 여전히 로컬 볼륨을 탑재 하 고 드라이브 문자를 할당할 수 있지만 드라이브 문자에 해당 하는 볼륨을 기억할 필요는 없습니다.

## <a name="examples"></a>예

탑재 지점을 만들려면 다음을 입력 합니다.

```
mountvol \sysmount \\?\volume\{2eca078d-5cbc-43d3-aff8-7e8511f60d0e}\
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
