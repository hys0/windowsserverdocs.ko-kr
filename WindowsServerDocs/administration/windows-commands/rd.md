---
title: rd
description: 디렉터리를 삭제 하는 rd 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 42e672f6-5bc2-4c16-af25-18e7ed2dd555
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 21f2828466bd8b41583ed4400856654cd53f4b49
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931985"
---
# <a name="rd"></a>rd

디렉터리를 삭제합니다.

다른 매개 변수를 사용 하 여 Windows 복구 콘솔에서 **rd** 명령을 실행할 수도 있습니다. 자세한 내용은 [WinRE (Windows 복구 환경)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference)를 참조 하세요.

> [!NOTE]
> 이 명령은 [rmdir 명령과](rmdir.md)같습니다.

## <a name="syntax"></a>구문

```
rd [<drive>:]<path> [/s [/q]]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| `[<drive>:]<path>` | 삭제 하려는 디렉터리의 이름과 위치를 지정 합니다. *경로* 가 필요 합니다. 지정 된 경로의 시작 부분에 백슬래시를 포함 하는 경우 \) *경로* 는 현재 디렉터리에 관계 없이 루트 디렉터리에서 시작 됩니다. *path* |
| /s | (지정된 된 디렉터리 및 모든 파일을 비롯 한 모든 하위) 디렉터리 트리를 삭제 합니다. |
| /q | 자동 모드를 지정합니다. 디렉터리 트리를 삭제할 때 확인 표시 하지 않습니다. **/Q** 매개 변수는 **/s** 도 지정 된 경우에만 작동 합니다.<p>**주의:** 자동 모드에서 실행 하는 경우 확인 없이 전체 디렉터리 트리가 삭제 됩니다. **/Q** 명령줄 옵션을 사용 하기 전에 중요 한 파일이 이동 되거나 백업 되었는지 확인 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 숨겨진 파일 또는 시스템 파일을 포함 하 여 파일이 포함 된 디렉터리는 삭제할 수 없습니다. 이렇게 하려고 하면 다음과 같은 메시지가 나타납니다.

    `The directory is not empty`

    모든 파일 (숨겨진 파일 및 시스템 파일 포함)을 나열 하려면 **dir/a** 명령을 사용 합니다. 다음 사용 하 여는 **attrib** 명령과 **-h** 숨겨진된 파일 특성을 제거 하려면 **-s** 시스템 파일 특성을 제거 하려면 또는 **-h-s** 모두 분리 숨김 및 시스템 파일 특성을 합니다. 숨겨진 후 및 파일 특성을 제거한, 파일을 삭제할 수 있습니다.

- **Rd** 명령을 사용 하 여 현재 디렉터리를 삭제할 수 없습니다. 현재 디렉터리를 삭제 하려고 하면 다음과 같은 오류 메시지가 나타납니다.

    `The process can't access the file because it is being used by another process.`

    이 오류 메시지가 표시 되 면 다른 디렉터리 (현재 디렉터리의 하위 디렉터리 아님)로 변경한 후 다시 시도 하십시오.

### <a name="examples"></a>예

원하는 디렉터리를 안전 하 게 제거할 수 있도록 부모 디렉터리를 변경 하려면 다음을 입력 합니다.

```
cd ..
```

현재 디렉터리에서 *test* (및 모든 하위 디렉터리 및 파일) 라는 디렉터리를 제거 하려면 다음을 입력 합니다.

```
rd /s test
```

자동 모드에서 앞의 예제를 실행 하려면 다음을 입력 합니다.

```
rd /s /q test
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
