---
title: 그림자를 삭제 합니다.
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1a0945477bc4fce907b5ec4a697c7a2ec2f59557
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436114"
---
# <a name="delete-shadows"></a>그림자를 삭제 합니다.



섀도 복사본을 삭제 합니다.

## <a name="syntax"></a>구문

```
delete shadows [all | volume <Volume> | oldest <Volume> | set <SetID> | id <ShadowID> | exposed {<Drive> | <MountPoint>}]
```

## <a name="parameters"></a>매개 변수

|     매개 변수     |                                                                             설명                                                                              |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        모든        |                                                                      모든 섀도 복사본을 삭제합니다.                                                                      |
| 볼륨 \<볼륨 >  |                                                            지정 된 볼륨의 모든 섀도 복사본을 삭제합니다.                                                            |
| 가장 오래 된 \<볼륨 >  |                                                         지정 된 볼륨의 가장 오래 된 섀도 복사본을 삭제합니다.                                                          |
|   set \<SetID>    | 지정 된 ID의 섀도 복사본 집합에 대 한 섀도 복사본을 삭제 사용 하 여 별칭을 지정할 수는 **%** 별칭 현재 환경에 있는 경우 기호입니다. |
|  id \<ShadowID>   |              지정 된 ID의 섀도 복사본을 삭제합니다. 사용 하 여 별칭을 지정할 수는 **%** 별칭 현재 환경에 있는 경우 기호입니다.               |
| 노출 {\<드라이브 > |                                                                            <MountPoint>}                                                                             |

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)