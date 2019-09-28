---
title: 그림자 삭제
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: c965af8b045c5ab3a110542d148b255f382a95c3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378635"
---
# <a name="delete-shadows"></a>그림자 삭제



섀도 복사본을 삭제 합니다.

## <a name="syntax"></a>구문

```
delete shadows [all | volume <Volume> | oldest <Volume> | set <SetID> | id <ShadowID> | exposed {<Drive> | <MountPoint>}]
```

## <a name="parameters"></a>매개 변수

|     매개 변수     |                                                                             설명                                                                              |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        모두        |                                                                      모든 섀도 복사본을 삭제합니다.                                                                      |
| 볼륨 \<Volume >  |                                                            지정 된 볼륨의 모든 섀도 복사본을 삭제합니다.                                                            |
| 가장 오래 된 \<Volume >  |                                                         지정 된 볼륨의 가장 오래 된 섀도 복사본을 삭제합니다.                                                          |
|   \<SetID > 설정    | 지정 된 ID의 섀도 복사본 집합에 대 한 섀도 복사본을 삭제 사용 하 여 별칭을 지정할 수는 **%** 별칭 현재 환경에 있는 경우 기호입니다. |
|  id \<ShadowID >   |              지정 된 ID의 섀도 복사본을 삭제합니다. 사용 하 여 별칭을 지정할 수는 **%** 별칭 현재 환경에 있는 경우 기호입니다.               |
| {\<Drive > 노출 됨 |                                                                            <MountPoint>}                                                                             |

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)