---
title: chkntfs
description: 컴퓨터를 시작할 때 자동 디스크 검사를 표시 하거나 수정 하는 chkntfs 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 93eca810-8699-4716-8e9d-aecd54f704be
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4d2a19a479ec3b00bda83ecded91f5fbb7941ca0
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930710"
---
# <a name="chkntfs"></a>chkntfs

표시 하거나 컴퓨터를 시작할 때 검사 자동 디스크를 수정 합니다. 옵션 없이 사용 하는 경우 **chkntfs** 지정된 된 볼륨의 파일 시스템을 표시 합니다. 자동 파일 검사를 실행 하도록 예약 하는 경우 **chkntfs** 표시 합니다. 지정된 된 볼륨 커밋되지 않았는지 여부 될 예정입니다 다음에 컴퓨터를 검사 시작 됩니다.

> [!NOTE]
> 실행 하려면 **chkntfs**, Administrators 그룹의 구성원 이어야 합니다.

## <a name="syntax"></a>구문

```
chkntfs <volume> [...]
chkntfs [/d]
chkntfs [/t[:<time>]]
chkntfs [/x <volume> [...]]
chkntfs [/c <volume> [...]]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<volume>` [...] | 컴퓨터를 시작할 때를 확인 하려면 하나 이상의 볼륨을 지정 합니다. (콜론) 드라이브 문자를 포함 하는 유효한 볼륨 탑재 지점 또는 볼륨 이름입니다. |
| /d | 모든 복원 **chkntfs** 기본 카운트다운 검사의 시간을 자동으로 파일을 제외 하 고 설정 합니다. 모든 볼륨은 컴퓨터를 시작할 때 기본적으로 검사 하 고 **chkdsk** 커밋되지 않은에서 실행 됩니다. |
| /t [ `:<time>` ] | Autochk.exe 시작 카운트다운 시간 (초)에 지정 된 시간을 변경 합니다. 한 번 입력 하지 않으면 **/t** 현재 카운트 다운 시간을 표시 합니다. |
| /x `<volume>` [...] | 볼륨은 필요한 것으로 표시 하는 경우에 컴퓨터를 시작할 때 검사에서 제외할 볼륨을 하나 이상 지정 **chkdsk**합니다. |
| /c `<volume>` [...] | 컴퓨터가 시작 되 고 실행 하는 경우 검사할 볼륨을 하나 이상 예약 **chkdsk** 에 커밋되지 않은 데이터입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="examples"></a>예

C 드라이브에 대 한 파일 시스템의 종류를 표시 하려면 다음을 입력 합니다.

```
chkntfs c:
```

> [!NOTE]
> 자동 파일 검사를 실행 하도록 예약 하는 경우 추가 출력에 표시 됩니다, 그리고 선택 여부를 나타내는 드라이브 변경 하거나 수동으로 했으면 예약 되도록 다음에 컴퓨터가 시작 됩니다.

Autochk.exe 시작 카운트다운 시간을 표시 하려면 다음을 입력 합니다.

```
chkntfs /t
```

Autochk.exe 시작 카운트다운 시간을 30 초로 변경 하려면 다음을 입력 합니다.

```
chkntfs /t:30
```

> [!NOTE]
> Autochk.exe 시작 카운트다운 시간 0을 설정할 수 있지만 차단 하면에서 걸리는 자동 파일 확인을 취소 합니다.

여러 볼륨을 검사에서 제외 하려면 단일 명령에서 각각의 나열 해야 합니다. 예를 들어, D 및 E 모두 볼륨을 제외 하려면 다음을 입력 합니다.

```
chkntfs /x d: e:
```

> [!IMPORTANT]
> **/X** 명령줄 옵션은 누적이 아닙니다. 두 번 이상 입력 하는 경우 가장 최근 항목이 이전 항목을 덮어씁니다.

D 볼륨에서 자동 파일 검사를 예약 하지만 C 또는 E 볼륨은 예약 하지 않으려면 다음 명령을 순서 대로 입력 합니다.

```
chkntfs /d
chkntfs /x c: d: e:
chkntfs /c d:
```

> [!IMPORTANT]
> **/c** 명령줄 옵션은 누적 되지 않습니다. 입력 하는 경우 **/c** 두 번 이상 각 항목 상태를 유지 합니다. 특정 볼륨에만 선택 되어 있는지을 보장 하려면 모든 볼륨을 검사에서 제외할 모든 이전 명령이 선택 취소 하는 기본값을 재설정 하 고 원하는 볼륨의 자동 파일 검사를 예약 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
