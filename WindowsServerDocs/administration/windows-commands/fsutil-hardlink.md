---
ms.assetid: 835fc6f1-cc84-4189-b29a-dde90792469e
title: Fsutil hardlink
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 69474bd1817471176598afba508cd80c8fa1df8a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840054"
---
# <a name="fsutil-hardlink"></a>Fsutil hardlink
>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

기존 파일 및 새 파일 간에 하드 링크를 만듭니다.

## <a name="syntax"></a>구문

```
fsutil hardlink create <NewFileName> <ExistingFileName>
fsutil hardlink list <Filename>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------------|---------------|
|만들기|기존 파일 및 새 파일 사이 NTFS 하드 링크를 설정합니다. (NTFS 하드 링크는 POSIX 하드 링크를 비슷합니다.)|
|\<NewFileName>|하드 링크를 만들려면 원하는 파일을 지정 합니다.|
|\<ExistingFileName>|하드 링크를 만들 파일을 지정 합니다.|
|목록|목록에 하드 *Filename*합니다.<br /><br />이 매개 변수가 적용 됩니다.  Windows Server 2008 R2 및 Windows 7입니다.|

## <a name="remarks"></a>설명

-   하드 링크는 파일에 대 한 디렉터리 항목입니다. 모든 파일을 하나 이상의 하드 링크 간주할 수 있습니다. NTFS 볼륨에 단일 파일 많은 디렉터리에 (또는 다른 이름의 같은 디렉터리에도) 표시 될 수 있도록 각 파일 여러 하드 링크가 있을 수 있습니다. 동일한 파일을 참조 하는 모든 링크가 하므로 프로그램 링크 연 파일을 수정 합니다. 에 대 한 모든 링크를 삭제 한 후에 파일을 파일 시스템에서 삭제 됩니다. 하드 링크를 만든 후 프로그램에서 다른 파일 이름 처럼 사용할 수 있습니다.

#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


