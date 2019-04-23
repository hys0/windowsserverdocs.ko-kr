---
ms.assetid: e5f55f3e-8d2a-4526-8d67-36a539126c22
title: Fsutil 계층화
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: dcb69e4e9c71a723bfd735eb7915472f1232a92b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859254"
---
# <a name="fsutil-tiering"></a>Fsutil 계층화
>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10

설정 및 플래그를 사용 하지 않도록 설정 하 고 계층 목록 같은 저장소 계층 함수를 관리할 수 있습니다.

## <a name="syntax"></a>구문

```
fsutil tiering [clearflags] <volume> <flags>
fsutil tiering [queryflags] <volume>
fsutil tiering [regionlist] <volume>
fsutil tiering [setflags] <volume> <flags>
fsutil tiering [tierlist] <volume>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------------|---------------|
|clearflags|볼륨의 계층화 동작 플래그를 사용 하지 않도록 설정 합니다.|
|\<volume>|볼륨을 지정합니다.|
|/TrNH|계층화 된 저장소를 사용 하 여 볼륨의 경우 수집을 사용할 수 없게 하는 열을 하면 됩니다.<br /><br>NTFS 및 ReFS에만 적용 됩니다.|
|queryflags|볼륨의 계층화 동작 플래그를 쿼리합니다.|
|regionlist|볼륨 및 해당 개별 저장소 계층의 계층화 된 영역을 나열합니다.|
|setflags|볼륨의 계층화 동작 플래그를 사용 하도록 설정 합니다.|
|tierlist|볼륨과 연결 된 저장소 tieres를 나열 합니다.|


### <a name="examples"></a>예

볼륨 C에 플래그를 쿼리하려면 다음을 입력 합니다.

```
fsutil tiering clearflags C:
```

볼륨 C에 플래그를 설정 하려면 다음을 입력 합니다.

```
fsutil tiering setflags C: /TrNH
```

볼륨 C에 플래그를 지우려면 다음을 입력 합니다.

```
fsutil tiering clearflags C: /TrNH
```

C 볼륨과 해당 개별 저장소 계층의 영역을 나열 하려면 다음을 입력 합니다.

```
fsutil tiering regionlist C:
```

볼륨 C의 계층을 나열 하려면 다음을 입력 합니다.

```
fsutil tiering tierlist C:
```



### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

