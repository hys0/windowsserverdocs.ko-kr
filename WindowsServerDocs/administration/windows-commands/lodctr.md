---
title: lodctr
description: 파일에서 성능 카운터 이름 및 레지스트리 설정을 등록 하거나 저장 하 고 신뢰할 수 있는 서비스를 지정 하는 데 사용할 수 있는 lodctr 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5a849abd-6b31-4833-bc8a-306c05eca29a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 221737d68280dabf34c270fccff02071ebf9b5a2
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820183"
---
# <a name="lodctr"></a>lodctr

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

등록 성능 카운터 이름 및 레지스트리 설정을 파일에 저장 하 고, 신뢰할 수 있는 서비스를 지정할 수 있습니다.

## <a name="syntax"></a>구문

```
lodctr <filename> [/s:<filename>] [/r:<filename>] [/t:<servicename>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<filename>` | 성능 카운터 이름 설정 및 설명 텍스트를 등록 하는 초기화 파일의 이름을 지정 합니다. |
| /s`<filename>` | 성능 카운터 레지스트리 설정 및 설명 텍스트가 저장 되는 파일의 이름을 지정 합니다. |
| /r | 현재 레지스트리 설정 및 레지스트리와 관련 된 캐시 된 성능 파일에서 카운터 레지스트리 설정 및 설명 텍스트를 복원 합니다. |
| /r`<filename>` | 성능 카운터 레지스트리 설정 및 설명 텍스트를 복원 하는 파일의 이름을 지정 합니다.<p>**경고:** 이 명령을 사용 하는 경우 모든 성능 카운터 레지스트리 설정 및 설명 텍스트를 덮어써서 지정 된 파일에 정의 된 구성으로 바꿉니다. |
| /t:`<servicename>` | 해당 서비스를 나타내는 `<servicename>` 신뢰할 수 있습니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 제공 하는 정보에 공백이 포함 된 경우 텍스트에 따옴표를 사용 합니다 (예: "파일 이름 1").

### <a name="examples"></a>예

현재 성능 레지스트리 설정 및 설명 텍스트를 파일 *성능 백업 1*에 저장 하려면 다음을 입력 합니다.

```
lodctr /s:perf backup1.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
