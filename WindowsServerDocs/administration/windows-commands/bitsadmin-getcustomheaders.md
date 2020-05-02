---
title: bitsadmin getcustomheaders
description: 작업에서 사용자 지정 HTTP 헤더를 검색 하는 bitsadmin getcustomheaders 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f0d38d3-e865-4474-81e8-773d65c3d1cc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7fe839cd0e629af88b3ee3642abcce339442d03a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718095"
---
# <a name="bitsadmin-getcustomheaders"></a>bitsadmin getcustomheaders

작업에서 사용자 지정 HTTP 헤더를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getcustomheaders <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

명명 된 작업에 대 한 사용자 지정 헤더를 가져오려면 *Mydownloadjob*:

```
bitsadmin /getcustomheaders myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
