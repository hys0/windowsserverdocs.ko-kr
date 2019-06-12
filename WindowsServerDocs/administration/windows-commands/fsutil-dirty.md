---
ms.assetid: 385a2a7c-d6bd-4f11-9c18-fca0413f9e97
title: Fsutil 커밋되지 않은 데이터
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: d8a5c4905991203a051fea360ed91c9b372f6993
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439080"
---
# <a name="fsutil-dirty"></a>Fsutil 커밋되지 않은 데이터
>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

쿼리 또는 볼륨의 더티 비트를 설정 합니다. 볼륨의 더티 비트가 설정 됩니다, **않은** 자동으로 오류에 대 한 볼륨을 다음에 컴퓨터를 다시 확인 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
fsutil dirty {query | set} <VolumePath>
```

## <a name="parameters"></a>매개 변수

|   매개 변수   |                                                 설명                                                  |
|---------------|--------------------------------------------------------------------------------------------------------------|
|     쿼리     |                                  지정 된 볼륨의 더티 비트를 쿼리합니다.                                   |
|      집합      |                                    지정 된 볼륨의 더티 비트를 설정합니다.                                    |
| \<VolumePath> | 드라이브 이름을 뒤에 콜론 또는 GUID 다음 형식으로 지정 합니다. **볼륨 {** <em>GUID</em> **}** 합니다. |

## <a name="remarks"></a>설명

-   볼륨의 더티 비트 파일 시스템 일관성이 없는 상태에 있을 수를 나타냅니다. 때문에 더티 비트를 설정할 수 있습니다.

    -   볼륨은 온라인 되어 있으며 처리 중인 변경 내용이 있습니다.

    -   볼륨에 변경 내용이 및 변경 내용이 디스크에 커밋 전에 컴퓨터를 종료 합니다.

    -   볼륨에 파일이 손상 되었습니다.

-   더티 비트가 설정 된 컴퓨터를 다시 시작 하는 경우 **chkdsk** 실행 파일 시스템 무결성을 확인 하 고 볼륨으로 문제를 해결 하려고 합니다.

## <a name="BKMK_examples"></a>예제
C 드라이브에 더티 비트를 쿼리하려면 다음을 입력 합니다.

```
fsutil dirty query c:
```

-   볼륨을 정리, 하는 경우에 다음과 같은 출력이 표시 됩니다.

    `Volume C: is dirty`

-   볼륨 더티가 아닌 경우 다음과 같은 출력이 표시 됩니다.

    `Volume C: is not dirty`

C 드라이브에 더티 비트를 설정 하려면 다음을 입력 합니다.

```
fsutil dirty set C:
```

#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


