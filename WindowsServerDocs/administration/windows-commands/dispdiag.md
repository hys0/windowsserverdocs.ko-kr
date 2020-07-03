---
title: dispdiag
description: 표시 정보를 파일에 기록 하는 dispdiag 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5079e1dd-b57c-44ed-970f-e6b409369e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d95a53f60aa7e51450a640d5ec9c5a5e6ccb41a6
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931220"
---
# <a name="dispdiag"></a>dispdiag

표시 정보를 파일에 기록 합니다.

## <a name="syntax"></a>구문

```
dispdiag [-testacpi] [-d] [-delay <seconds>] [-out <filepath>]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| -testacpi | 핫키 진단 테스트를 실행 합니다. 테스트 하는 동안 누른 키의 키 이름, 코드 및 검사 코드를 표시 합니다. |
| -d | 테스트 결과를 사용 하 여 덤프 파일을 생성 합니다. |
| -delay`<seconds>` | 지정 된 시간 *(초)* 으로 데이터 컬렉션을 지연 시킵니다. |
| -out`<filepath>`  | 수집 된 데이터를 저장할 경로와 파일 이름을 지정 합니다. 이 매개 변수는 마지막 매개 변수 여야 합니다. |
| -? | 사용 가능한 명령 매개 변수를 표시 하 고 사용 하기 위한 도움말을 제공 합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
