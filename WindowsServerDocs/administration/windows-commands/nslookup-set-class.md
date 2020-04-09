---
title: nslookup set class
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ed826400-40da-42b6-b7f0-95db73790723
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc3bb4e36582f01584c0b89a12d43874322c3190
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838586"
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
| \<클래스 >  | 기본 클래스는 IN입니다. 다음은이 명령에 대 한 유효한 값을 나열 합니다.</br>-IN: 인터넷 클래스를 지정 합니다.</br>-비정상: 비정상 클래스를 지정 합니다.</br>-HESIOD: MIT 아테나 Hesiod 클래스를 지정 합니다.</br>-ANY: 이전에 나열 된 와일드 카드를 지정 합니다. |
|   {도움말   |                                                                                                                                        ?}                                                                                                                                         |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)