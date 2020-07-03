---
title: bitsadmin getnotifycmdline
description: 작업에서 데이터 전송을 완료할 때 실행 되는 명령줄 명령을 검색 하는 bitsadmin getnotifycmdline 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90fa33e6-aca5-4a23-82bd-19a9f13f8416
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 233186edcdb10d98e1d1139ebd63943647b84ae4
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926996"
---
# <a name="bitsadmin-getnotifycmdline"></a>bitsadmin getnotifycmdline

지정 된 작업에서 데이터 전송을 완료 한 후 실행 되는 명령줄 명령을 검색 합니다.

> [!NOTE]
> 이 명령은 BITS 1.2 이전 버전에서는 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /getnotifycmdline <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

*Mydownloadjob* 이라는 작업이 완료 될 때 서비스에서 사용 하는 명령줄 명령을 검색 합니다.

```
bitsadmin /getnotifycmdline myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
