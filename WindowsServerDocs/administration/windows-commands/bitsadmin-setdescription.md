---
title: bitsadmin setdescription
description: Bitsadmin setdescription 명령에 대 한 참조 항목으로, 지정 된 작업에 대 한 설명을 설정 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1e46a5dd-4637-4a2e-b88f-d3f85b177db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc76da7cbe348461a79984b8061767711e090da7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719304"
---
# <a name="bitsadmin-setdescription"></a>bitsadmin setdescription

지정 된 작업에 대 한 설명을 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setdescription <job> <description>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| description | 작업에 설명 하는 데 사용 하는 텍스트입니다. |

## <a name="examples"></a>예

이름이 *Mydownloadjob*인 작업에 대 한 설명을 검색 하려면:

```
bitsadmin /setdescription myDownloadJob music_downloads
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
