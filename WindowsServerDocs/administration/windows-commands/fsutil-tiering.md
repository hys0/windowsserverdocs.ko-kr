---
title: fsutil tiering
description: 플래그 및 계층 목록 설정/해제와 같은 저장소 계층 기능을 관리할 수 있도록 하는 fsutil 계층화 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: e5f55f3e-8d2a-4526-8d67-36a539126c22
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 1463a6c50d2f735456e0675bdeef235cb5484b3e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932097"
---
# <a name="fsutil-tiering"></a>fsutil tiering

> 적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016, Windows 10

플래그 설정/해제, 계층 목록 등의 저장소 계층 기능을 관리할 수 있습니다.

## <a name="syntax"></a>구문

```
fsutil tiering [clearflags] <volume> <flags>
fsutil tiering [queryflags] <volume>
fsutil tiering [regionlist] <volume>
fsutil tiering [setflags] <volume> <flags>
fsutil tiering [tierlist] <volume>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| clearflags | 볼륨의 계층화 동작 플래그를 사용 하지 않도록 설정 합니다. |
| `<volume>` | 볼륨을 지정 합니다. |
| /trnh | 계층화 된 저장소가 있는 볼륨의 경우에는 열 수집을 사용 하지 않도록 설정 합니다.<p>NTFS 및 ReFS에만 적용 됩니다. |
| queryflags | 볼륨의 계층화 동작 플래그를 쿼리 합니다. |
| regionlist | 볼륨 및 해당 저장소 계층의 계층화 된 영역을 나열 합니다. |
| setflags | 볼륨의 계층화 동작 플래그를 사용 하도록 설정 합니다. |
| tierlist | 볼륨에 연결 된 저장소 계층을 나열 합니다. |

### <a name="examples"></a>예

C 볼륨에서 플래그를 쿼리하려면 다음을 입력 합니다.

```
fsutil tiering queryflags C:
```

C 볼륨에 플래그를 설정 하려면 다음을 입력 합니다.

```
fsutil tiering setflags C: /trnh
```

C 볼륨에서 플래그를 지우려면 다음과 같이 입력 합니다.

```
fsutil tiering clearflags C: /trnh
```

볼륨 C의 지역과 해당 하는 저장소 계층을 나열 하려면 다음을 입력 합니다.

```
fsutil tiering regionlist C:
```

볼륨 C의 계층을 나열 하려면 다음을 입력 합니다.

```
fsutil tiering tierlist C:
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [fsutil](fsutil.md)
