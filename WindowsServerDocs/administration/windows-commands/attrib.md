---
title: attrib
description: 파일 또는 디렉터리에 할당 된 특성을 표시, 설정 또는 제거 하 **는 특성에 대 한**Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5e763ca5-21a2-45d2-b26d-a9c44c99091a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 94a6f307450b06dff81180b70f864bd9e1ed5885
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851256"
---
# <a name="attrib"></a>attrib

표시 설정 하거나 파일 또는 디렉터리에 할당 된 특성을 제거 합니다. 매개 변수 없이 사용 하는 경우 **attrib** 현재 디렉터리에 있는 모든 파일의 속성을 표시 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
attrib [{+|-}r] [{+|-}a] [{+|-}s] [{+|-}h] [{+|-}i] [<Drive>:][<Path>][<FileName>] [/s [/d] [/l]]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{+|-}r` | 집합 ( **+** )을 선택 하거나 취소 ( **-** ) 읽기 전용 파일 특성입니다. |
| `{+\|-}a` | 집합 ( **+** )을 선택 하거나 취소 ( **-** ) 보관 파일 특성입니다. |
| `{+\|-}s` | 집합 ( **+** )을 선택 하거나 취소 ( **-** ) 시스템 파일 특성입니다. |
| `{+\|-}h` | 집합 ( **+** )을 선택 하거나 취소 ( **-** ) 숨김 파일 특성입니다. |
| `{+\|-}i` | 집합 ( **+** )을 선택 하거나 취소 ( **-** ) 콘텐츠 인덱싱되지 파일 특성입니다. |
| `[<Drive>:][<Path>][<FileName>]` | 디렉터리, 파일 또는 파일을 표시 하거나 특성을 변경 하려면 원하는 그룹의 이름과 위치를 지정 합니다. 사용할 수는 **?** 파일 **&#42;** 그룹에 대 한 특성을 표시 하거나 변경 하기 위해 *FileName* 매개 변수에 와일드 카드 문자를 사용할 수 있습니다. |
| /s | 적용 대상 **attrib** 현재 디렉터리에 일치 하는 파일에 명령줄 옵션 및 모든 하위 디렉터리 및입니다. |
| /d | 적용 대상 **attrib** 와 디렉터리에 명령줄 옵션입니다. |
| /l | 적용 대상 **attrib** 와 기호화 된 링크의 대상이 아닌 기호화 된 링크에 명령줄 옵션입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="remarks"></a>주의

- 와일드 카드 문자를 사용할 수 있습니다 ( **?** 및 **&#42;** )를 파일 그룹에 대 한 특성을 표시 하거나 변경 하는 *FileName* 매개 변수를 사용 합니다.

- 파일에 있는 경우 시스템 (**s**) 또는 숨김 (**h**) 특성 집합을 해제 해야 특성 해당 파일에 대 한 다른 특성을 변경할 수 있습니다.

- Archive 특성 (**는**) 마지막으로 백업한 이후 변경 된 파일을 표시 합니다. **Xcopy** 명령은 보관 특성을 사용 합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

현재 디렉터리에 있는 News86 라는 파일의 특성을 표시 하려면 다음을 입력 합니다.

```
attrib news86 
```

Report.txt 라는 파일에 읽기 전용 특성을 할당 하려면 다음을 입력 합니다.

```
attrib +r report.txt 
```

B 드라이브의 디스크에서 공용 디렉터리 및 하위 디렉터리에 있는 파일에서 읽기 전용 특성을 제거 하려면 다음을 입력 합니다.

```
attrib -r b:\public\*.* /s 
```

A, 드라이브에 있는 모든 파일에 대 한 기록 속성을 설정 하 고 확장명이.bak 인 파일에 대 한 보관 특성을 해제 하십시오, 다음을 입력 합니다.

```
attrib +a a:*.* & attrib -a a:*.bak 
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)