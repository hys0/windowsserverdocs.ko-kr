---
title: bitsadmin setdisplayname
description: 지정 된 작업의 표시 이름을 설정 하는 bitsadmin setdisplayname 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 382cb2f20f0374c2d2787c4c3d88670b4f7260cd
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719383"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname

지정 된 작업에 대 한 표시 이름을 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setdisplayname <job> <display_name>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| display_name | 특정 작업에 대해 표시 된 이름으로 사용 되는 텍스트입니다. |

## <a name="examples"></a>예

작업의 표시 이름을 *Mydownloadjob*로 설정 하려면 다음을 수행 합니다.

```
bitsadmin /setdisplayname myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
