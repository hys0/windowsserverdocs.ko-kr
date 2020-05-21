---
title: extract
description: 원본 위치에서 파일을 추출 하는 extract 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 20dab03e-f6e1-4eb8-b8a1-fd6f1d97ee83
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dbadcc555fc9bb0b02e568b1126a317a9d59d336
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2020
ms.locfileid: "83437188"
---
# <a name="extract"></a>extract

캐비닛이 나 원본에서 파일을 추출 합니다.

## <a name="syntax"></a>구문

```
extract [/y] [/a] [/d | /e] [/l dir] cabinet [filename ...]
extract [/y] source [newname]
extract [/y] /c source destination
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 캐비닛 | 두 개 이상의 파일을 추출 하려면를 사용 합니다. |
| filename | 캐비닛에서 추출 하는 파일의 이름입니다. 여러 파일 이름 (공백으로 구분) 및 와일드 카드를 사용할 수 있습니다. |
| 원본 | 압축된 파일 (하나의 파일 캐비닛)입니다. |
| 새 이름 | 추출 된 파일에 새 파일 이름입니다. 을 제공 하지 않으면 원래 이름이 사용 됩니다. |
| /a | 모든 캐비닛을 처리 합니다. 언급 한 첫 번째 캐비닛에 시작 해 서 캐비닛 체인을 따릅니다. |
| /C | 대상 (DMF 디스크에서 복사)을 소스 파일을 복사 합니다. |
| /d | 캐비닛 디렉터리 (압축 해제를 방지 하려면 파일 이름으로 사용)을 표시 합니다. |
| /e | Extract (대신를 사용 *합니다.* 파일을 추출 하려면 모든). |
| /l 디렉터리 | (기본값은 현재 디렉터리)는 압축 푼된 파일을 배치할 위치입니다. |
| /y | 기존 파일을 덮어쓰기 전에 메시지를 표시 하지 않습니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
