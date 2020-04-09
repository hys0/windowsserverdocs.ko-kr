---
title: break
description: MS-DOS 시스템에서 확장 된 CTRL + C 검사를 설정 하거나 해제 하는 break_1에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c89b7357-d69e-4141-826e-73c9ba0fc630
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 809a9321b8b4f8b2d201582f767da132076826d4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848366"
---
# <a name="break"></a>break

설정 하거나 MS-DOS 시스템에서 확인 하는 확장 된 CTRL + C를 지웁니다. 매개 변수 없이 사용 하는 경우 **나누기** 현재 설정이 표시 됩니다.

> [!NOTE]
> 이 명령은 더 이상 사용 중입니다. 기존 MS-DOS 파일과의 호환성을 유지하기 위해서만 포함되지만 기능은 자동이므로 명령줄에서는 아무런 영향을 주지 않습니다.

## <a name="syntax"></a>구문

```
break=[on|off]
```

## <a name="remarks"></a>주의

명령 확장을 Windows 플랫폼에서 실행 되 고 활성화 된 경우 삽입 된 **나누기** 명령 배치 파일에는 디버거에서 디버깅 중인 경우 하드 코드 중단점을 입력 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)