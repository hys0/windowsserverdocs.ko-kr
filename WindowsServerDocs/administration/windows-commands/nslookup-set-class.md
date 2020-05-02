---
title: nslookup set class
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ed826400-40da-42b6-b7f0-95db73790723
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b1ae3a5336815a5273aafa976b1dcad8b60fac9b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723652"
---
# <a name="nslookup-set-class"></a>nslookup set class



쿼리 클래스를 변경 합니다. 클래스는 프로토콜 그룹 정보를 지정합니다.

## <a name="syntax"></a>구문

```
set class=<Class>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 |                                                                                                                                    설명                                                                                                                                    |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| \<Class>  | 기본 클래스는 IN입니다. 다음은이 명령에 대 한 유효한 값을 나열 합니다.</br>-IN: 인터넷 클래스를 지정 합니다.</br>-비정상: 비정상 클래스를 지정 합니다.</br>-HESIOD: MIT 아테나 Hesiod 클래스를 지정 합니다.</br>-ANY: 이전에 나열 된 와일드 카드를 지정 합니다. |
|   {도움말   |                                                                                                                                        ?}                                                                                                                                         |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)