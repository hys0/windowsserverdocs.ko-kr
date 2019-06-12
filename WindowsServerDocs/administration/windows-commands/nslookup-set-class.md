---
title: nslookup set class
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed826400-40da-42b6-b7f0-95db73790723
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7953f450c17afdee849515f8d8945631a30f4b98
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436843"
---
# <a name="nslookup-set-class"></a>nslookup set class



쿼리 클래스를 변경 합니다. 클래스는 프로토콜 그룹 정보를 지정합니다.

## <a name="syntax"></a>구문

```
set class=<Class>
```

## <a name="parameters"></a>매개 변수

| 매개 변수 |                                                                                                                                    설명                                                                                                                                    |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| \<클래스 >  | 기본 클래스는 IN입니다. 다음은이 명령에 대 한 유효한 값을 나열 합니다.</br>-에: 인터넷 클래스를 지정합니다.</br>- CHAOS: 혼돈 클래스를 지정합니다.</br>- HESIOD: Athena Hesiod 클래스를 지정합니다.</br>-모든: 앞에 나열 된 와일드 카드 중 하나를 지정 합니다. |
|   {도움말   |                                                                                                                                        ?}                                                                                                                                         |

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)