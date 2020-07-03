---
title: nslookup set class
description: 쿼리 클래스를 변경 하는 nslookup set 클래스 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ed826400-40da-42b6-b7f0-95db73790723
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 073f27f6f10721b11e6d0889d1cb8c16f15db283
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934419"
---
# <a name="nslookup-set-class"></a>nslookup set class

쿼리 클래스를 변경 합니다. 클래스는 프로토콜 그룹 정보를 지정합니다.

## <a name="syntax"></a>구문

```
set class=<class>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<class>` | 유효한 값은 다음과 같습니다.<ul><li>**에서:** 인터넷 클래스를 지정 합니다. 기본값입니다.</li><li>비정상 상황 **:** 비정상 클래스를 지정 합니다.</li><li>**HESIOD:** MIT 아테나 Hesiod 클래스를 지정 합니다.</li><li>**ANY:** 이전에 나열 된 값을 사용 하도록 지정 합니다.</li></ul> |
| /? | 명령 프롬프트에 도움말을 표시합니다. |
| /help | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
