---
title: 추가
description: 프로그램이 현재 디렉터리에 있는 것 처럼 지정 된 디렉터리의 데이터 파일을 열 수 있도록 하는 추가 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9c3fea20-9502-40ad-a442-7a927aad88eb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 562a13c6b1a47e43bb66548902f0b8e57e789a34
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718992"
---
# <a name="append"></a>추가

지정 된 디렉터리에 데이터 파일을 현재 디렉터리에 있는 것 처럼 열을 수 있습니다. 매개 변수 없이 사용 하는 경우 **추가** 추가 디렉터리 목록을 표시 합니다.

> [!NOTE]
> 이 명령은 Windows 10에서 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
append [[<drive>:]<path>[;...]] [/x[:on|:off]] [/path:[:on|:off] [/e]
append ;
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `[\<drive>:]<path>` | 드라이브와 추가할 디렉터리를 지정 합니다. |
| / x:에 | 파일 검색 및 시작 애플리케이션에 추가 된 디렉터리를 적용합니다. |
| /x: 해제 | 추가 된 디렉터리 요청 파일을 열에 적용 됩니다. **/X: off** 옵션이 기본 설정입니다. |
| /path:에 | 이미 경로 지정 하는 파일 요청에 추가 된 디렉터리를 적용 합니다. **/path:에** 기본 설정입니다. |
| /path: 해제 | 효과 해제 **/path:에**합니다. |
| /e | Append 환경 변수에 추가 디렉터리 목록의 복사본을 저장 합니다. **/e** 처음에 사용할 때만 사용할 수 있습니다 **추가** 시스템을 시작한 후입니다. |
| ; | 추가 디렉터리 목록을 지웁니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="examples"></a>예

추가 디렉터리 목록을 지우려면 다음을 입력 합니다.

```
append ;
```

*Append*라는 환경 변수에 추가 된 디렉터리의 복사본을 저장 하려면 다음을 입력 합니다.

```
append /e
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
