---
title: expand
description: 하나 이상의 압축 된 파일을 확장 하는 확장 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 66de0488-a0c4-40c2-9b03-e40c107ba343
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1204f3db338f835b47db03eab3d178544a6acc85
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83819123"
---
# <a name="expand"></a>expand

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

하나 이상의 압축 된 파일을 확장합니다. 이 명령을 사용 하 여 배포 디스크에서 압축 된 파일을 검색할 수도 있습니다.

다른 매개 변수를 사용 하 여 Windows 복구 콘솔에서 **확장** 명령을 실행할 수도 있습니다. 자세한 내용은 [WinRE (Windows 복구 환경)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference)를 참조 하세요.

## <a name="syntax"></a>구문

```
expand [/r] <source> <destination>
expand /r <source> [<destination>]
expand /i <source> [<destination>]
expand /d <source>.cab [/f:<files>]
expand <source>.cab /f:<files> <destination>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| /r | 압축을 푼 파일입니다. |
| 원본 | 압축을 풀 파일을 지정 합니다. *소스* 드라이브 문자 및 콜론, 디렉터리 이름, 파일 이름, 또는 이들의 조합으로 구성 될 수 있습니다. 와일드 카드 (**&#42;** 또는 **?**)를 사용할 수 있습니다. |
| destination | 확장 하는 파일의 위치를 지정 합니다.<p>*원본이* 여러 파일로 구성 되어 있고 **/r**을 지정 하지 않은 경우 *대상은* 디렉터리 여야 합니다. *대상* 드라이브 문자 및 콜론, 디렉터리 이름, 파일 이름, 또는 이들의 조합으로 구성 될 수 있습니다. 대상 `file | path` 사양입니다. |
| /i | 확장 된 파일의 이름을 바꿉니다 하 하지만 디렉터리 구조를 무시 합니다. |
| /d | 원본 위치에서 파일 목록을 표시합니다. 는 파일을 확장 하거나 추출 하지 않습니다. |
| /f`<files>` | 확장 하려는 캐비닛 (.cab) 파일에 파일을 지정 합니다. 와일드 카드 (**&#42;** 또는 **?**)를 사용할 수 있습니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
