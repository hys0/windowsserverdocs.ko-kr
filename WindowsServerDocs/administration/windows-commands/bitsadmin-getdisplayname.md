---
title: bitsadmin getdisplayname
description: 지정 된 작업의 표시 이름을 검색 하는 bitsadmin getdisplayname 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e5c0e76c-4cc6-42d8-ac30-30bf3dc11b9b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0d47a70d34dbff0249a9d69f1db1deaa879c76c8
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2020
ms.locfileid: "83437068"
---
# <a name="bitsadmin-getdisplayname"></a>bitsadmin getdisplayname

지정 된 작업의 표시 이름을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getdisplayname <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업의 표시 이름을 검색 하려면:

```
bitsadmin /getdisplayname myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
