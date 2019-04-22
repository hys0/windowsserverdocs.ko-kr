---
ms.assetid: 6c6ff819-f349-4aea-b0be-1f637f631736
title: fsutil wim
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: c9186721ce4d3a549964e420cbc16d4893a1859d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826044"
---
# <a name="fsutil-wim"></a>fsutil wim
>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10

검색 지원 Windows 이미지 WIM 파일을 관리 하는 함수를 제공 합니다.

## <a name="syntax"></a>구문

```
fsutil wim [enumfiles] <drive name> <data source>
fsutil wim [enumwims] <drive name>
fsutil wim [queryfile] <filename>
fsutil wim [removewim] <drive name> <data source>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------------|---------------|
|enumfiles|지원 되는 WIM 파일을 열거합니다.|
|\<드라이브 이름 >|드라이브 이름을 지정합니다.|
|\<데이터 소스 >|데이터 소스를 지정합니다.|
|enumwims|백업 WIM 파일을 열거합니다.|
|queryfile|쿼리 파일에서 WIM을 지원 되는 경우 그리고 있다면 WIM 파일에 대 한 세부 정보 표시 합니다.|
|\<filename>|파일 이름을 지정합니다.|
|removewim|백업 파일에서 WIM을 제거 합니다.|




### <a name="examples"></a>예

데이터 원본의 0 c: 드라이브에 대 한 파일을 열거 하려면 다음을 입력 합니다.

```
fsutil wim enumfiles C: 0
```

C: 드라이브에 대 한 백업 WIM 파일을 열거 하려면 다음을 입력 합니다.

```
fsutil wim enumwims C:
```

WIM에서 파일을 지 원하는 경우를 확인 하려면 다음을 입력 합니다.

```
fsutil wim C:\Windows\Notepad.exe
```

C: 볼륨 및 데이터 원본 2에 대 한 파일을 백업에서 WIM을 제거 하려면 다음을 입력 합니다.

```
fsutil wim removewims C: 2
```

### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)