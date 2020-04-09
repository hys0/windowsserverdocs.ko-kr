---
title: 압축
description: NTFS 파티션에서 파일이 나 디렉터리의 압축을 표시 하거나 변경 하는 Windows 명령 항목을 압축 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 429b3752-df0a-43a4-a210-df2f3ad03c3b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e9e6a3ba71ecc0c8e264ac4af8dc1da42d23fdc2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847356"
---
# <a name="compact"></a>압축

NTFS 파티션에서 파일이 나 디렉터리의 압축을 표시 하거나 변경 합니다. 매개 변수 없이 사용 하는 경우 **compact** 는 현재 디렉터리와이 디렉터리에 포함 된 파일의 압축 상태를 표시 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
compact [/c | /u] [/s[:<Dir>]] [/a] [/i] [/f] [/q] [<FileName>[...]]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/c|지정 된 디렉터리 또는 파일을 압축 합니다.|
|/u|지정 된 디렉터리 또는 파일을 Uncompresses 합니다.|
|/s [:\<Dir >]|지정 된 디렉터리 (또는 지정 되지 않은 경우 현재 디렉터리)의 모든 하위 디렉터리에 **compact** 명령을 적용 합니다.|
|/a|숨겨진 또는 시스템 파일을 표시 합니다.|
|/i|오류를 무시합니다.|
|/f|지정 된 디렉터리나 파일의 압축을 강제로 압축 하거나 압축을 해제 합니다. **/f** 는 시스템 작동 중단에 의해 작업이 중단 된 경우 부분적으로 압축 된 파일의 경우에 사용 됩니다. 파일이 전체적으로 압축 되도록 하려면 **/c** 및 **/f** 매개 변수를 사용 하 고 부분적으로 압축 된 파일을 지정 합니다.|
|/q|가장 중요 한 정보만 보고 합니다.|
|\<파일 이름 >|파일이 나 디렉터리를 지정 합니다. 여러 파일 이름을 **&#42;** 사용할 수 있습니다. **?** 와일드 카드 문자.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>주의

-   **Compact** 명령은 NTFS 파일 시스템 압축 기능의 명령줄 버전입니다. 디렉터리의 압축 상태는 파일이 디렉터리에 추가 될 때 자동으로 압축 되는지 여부를 나타냅니다. 디렉터리의 압축 상태를 설정 하는 것은 디렉터리에 이미 있는 파일의 압축 상태를 변경 하지 않아도 됩니다.
-   **압축** 을 사용 하 여 디스크 공간 또는 DoubleSpace로 압축 된 볼륨을 읽거나, 쓰고, 탑재할 수 없습니다.
-   **압축** 을 사용 하 여 FAT (파일 할당 테이블) 또는 FAT32 파티션을 압축할 수 없습니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

현재 디렉터리, 하위 디렉터리 및 기존 파일의 압축 상태를 설정 하려면 다음을 입력 합니다.
```
compact /c /s 
```
현재 디렉터리 자체의 압축 상태를 변경 하지 않고 현재 디렉터리에 있는 파일 및 하위 디렉터리의 압축 상태를 설정 하려면 다음을 입력 합니다.
```
compact /c /s *.*
```
볼륨을 압축 하려면 볼륨의 루트 디렉터리에서 다음을 입력 합니다.
```
compact /c /i /s:\
```

> [!NOTE]
> 이 예에서는 볼륨의 루트 디렉터리를 포함 하 여 모든 디렉터리의 압축 상태를 설정 하 고 볼륨에 있는 모든 파일을 압축 합니다. **/I** 매개 변수는 오류 메시지가 압축 프로세스를 방해 하지 않도록 합니다.

디렉터리의 압축 특성을 수정 하지 않고 \Tmp 디렉터리와 \Tmp의 모든 하위 디렉터리에서 .bmp 파일 이름 확장명을 가진 모든 파일을 압축 하려면 다음을 입력 합니다.
```
compact /c /s:\tmp *.bmp
```
시스템 작동이 중단 되는 동안 부분적으로 압축 된 얼룩말 파일의 전체 압축을 강제로 적용 하려면 다음을 입력 합니다.
```
compact /c /f zebra.bmp
```
해당 디렉터리에 있는 파일의 압축 상태를 변경 하지 않고 C:\Tmp 디렉터리에서 압축 된 특성을 제거 하려면 다음을 입력 합니다.
```
compact /u c:\tmp
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)