---
title: bitsadmin getdisplayname
description: 지정 된 작업의 표시 이름을 검색 하는 bitsadmin getdisplayname 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e5c0e76c-4cc6-42d8-ac30-30bf3dc11b9b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4b0e768f377b9faa23eb59645cbecdc129f1e573
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923045"
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
