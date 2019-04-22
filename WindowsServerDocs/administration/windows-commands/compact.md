---
title: compact
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 429b3752-df0a-43a4-a210-df2f3ad03c3b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 068111b293a3eb3987b14744a1bfcf2fde26bced
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826034"
---
# <a name="compact"></a>compact



표시 하거나 파일 또는 디렉터리가 NTFS 파티션에 대해 압축을 변경 합니다. 매개 변수 없이 사용 하는 경우 **compact** 현재 디렉터리와 포함 된 파일의 압축 상태를 표시 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
compact [/c | /u] [/s[:<Dir>]] [/a] [/i] [/f] [/q] [<FileName>[...]]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/c|지정 된 디렉터리 또는 파일을 압축합니다.|
|/u|지정 된 디렉터리 또는 파일의 압축을 해제 합니다.|
|/s[:\<Dir>]|적용 된 **compact** 모든 하위 디렉터리에 지정된 된 디렉터리 (또는 지정 되지 않은 경우 현재 디렉터리의) 명령을 합니다.|
|/ a|숨김 표시 또는 시스템 파일입니다.|
|/i|오류를 무시합니다.|
|/f|강제로 압축 또는 지정 된 디렉터리 또는 파일의 압축 해제 합니다. **/f** 시스템 충돌로 인해 작업이 중단 되었습니다. 부분적으로 압축 된 파일의 경우 사용 됩니다. 전체에서 압축 파일을 강제로 사용 합니다 **/c** 및 **/f** 매개 변수 부분적으로 압축 된 파일을 지정 합니다.|
|/q|가장 중요 한 정보만을 보고합니다.|
|\<FileName>|파일 또는 디렉터리를 지정합니다. 여러 파일 이름을 사용할 수 있습니다 및 **&#42;** 하 고 **?** 와일드 카드 문자입니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   합니다 **compact** 명령 명령줄 버전을 NTFS 파일 시스템 압축 기능입니다. 압축 상태 디렉터리의 디렉터리에 추가 될 때 파일이 자동으로 압축할지 여부를 나타냅니다. 디렉터리의 압축 상태를 설정 해도 이미 디렉터리에 있는 파일의 압축 상태 반드시 변경 되지 않습니다.
-   사용할 수 없습니다 **compact** 읽기, 쓰기 또는 디스크 공간 늘림 또는 DoubleSpace를 사용 하 여 압축 된 볼륨을 탑재 합니다.
-   사용할 수 없습니다 **compact** 파일 할당 테이블 (FAT) 또는 FAT32 파티션이 압축 합니다.

## <a name="BKMK_examples"></a>예제

현재 디렉터리, 하위 디렉터리 및 기존 파일의 압축 상태를 설정 하려면 다음을 입력 합니다.
```
compact /c /s 
```
현재 디렉터리 자체의 압축 상태를 변경 하지 않고 파일 및 현재 디렉터리 내의 하위 디렉터리의 압축 상태를 설정 하려면 다음을 입력 합니다.
```
compact /c /s *.*
```
볼륨의 루트 디렉터리에서 볼륨을 압축 하려면 다음을 입력 합니다.
```
compact /c /i /s:\
```

> [!NOTE]
> 볼륨의 루트 디렉터리 등 모든 디렉터리의 압축 상태를 설정 하 고 볼륨의 모든 파일을 압축 하는이 예제입니다. 합니다 **/i** 매개 변수는 중단 압축 프로세스에서 오류 메시지를 방지 합니다.

\Tmp 디렉터리에서.bmp 파일 이름 확장명을 사용 하 여 모든 파일 및 \Tmp의 모든 하위 디렉터리의 압축 된 특성을 수정 하지 않고를 압축 하려면 다음을 입력 합니다.
```
compact /c /s:\tmp *.bmp
```
Zebra.bmp 시스템 중단 시 부분적으로 압축 된 파일의 압축을 완료 하도록 다음을 입력 합니다.
```
compact /c /f zebra.bmp
```
압축 된 특성 C:\Tmp 디렉터리에서 해당 디렉터리에 있는 파일의 압축 상태를 변경 하지 않고를 제거 하려면 다음을 입력 합니다.
```
compact /u c:\tmp
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)