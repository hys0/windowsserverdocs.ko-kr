---
title: attributes volume
description: 볼륨의 특성을 표시, 설정 또는 삭제 하는 특성 볼륨 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e40e8284-3d57-4de8-a46c-e4ade34a0d53
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aae7cc7fe26fac5ef03e40610eb46389eb274c94
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923877"
---
# <a name="attributes-volume"></a>attributes volume

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

표시 설정 하거나 볼륨의 특성을 지웁니다.

## <a name="syntax"></a>구문

```
attributes volume [{set | clear}] [{hidden | readonly | nodefaultdriveletter | shadowcopy}] [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ------- | -------- |
| set | 포커스가 있는 볼륨의 지정된 된 특성을 설정합니다. |
| 지우기 | 포커스가 있는 볼륨의 지정된 된 특성을 지웁니다. |
| readonly | 볼륨이 읽기 전용인 지 여부를 지정 합니다. |
| hidden | 볼륨 숨겨지는지를 지정 합니다. |
| nodefaultdriveletter | 볼륨 기본적으로 드라이브 문자를 할당 하지 않는 것을 지정 합니다. |
| 섀도 복사본 | 볼륨 섀도 복사본 볼륨 임을 지정 합니다. |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

### <a name="remarks"></a>설명

- 기본 MBR (마스터 부트 레코드) 디스크에서 **hidden**, **readonly**및 **nodefaultdriveletter** 매개 변수는 디스크의 모든 볼륨에 적용 됩니다.

- 기본 GPT (GUID 파티션 테이블) 디스크 및 동적 MBR 및 GPT 디스크에서 **hidden**, **readonly**및 **nodefaultdriveletter** 매개 변수는 선택한 볼륨에만 적용 됩니다.

- 볼륨을 선택 해야는 **볼륨 특성** 명령을 성공적으로 합니다. 사용 하 여는 **볼륨 선택** 볼륨을 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="examples"></a>예

선택된 된 볼륨의 현재 속성을 표시 하려면 다음을 입력 합니다.

```
attributes volume
```

선택한 볼륨을 숨겨진 읽기 전용으로 설정 하려면 다음을 입력 합니다.

```
attributes volume set hidden readonly
```

선택한 볼륨의 숨겨진 및 읽기 전용 특성을 제거 하려면 다음을 입력 합니다.

```
attributes volume clear hidden readonly
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [볼륨 선택 명령](select-volume.md)
