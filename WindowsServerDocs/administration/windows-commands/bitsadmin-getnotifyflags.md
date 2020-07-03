---
title: bitsadmin getnotifyflags
description: 지정 된 작업에 대 한 알림 플래그를 검색 하는 bitsadmin getnotifyflags 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d4657e6c-8959-4db7-a4af-e73d3f80ecf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0ea97c039f372a2211b1e2a6c640c4499a38dfe4
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926922"
---
# <a name="bitsadmin-getnotifyflags"></a>bitsadmin getnotifyflags

지정 된 작업에 대 한 알림 플래그를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getnotifyflags <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="remarks"></a>설명

작업은 다음 알림 플래그 중 하나 이상을 포함할 수 있습니다.

| 플래그 | 설명 |
| ----- | ----- |
| 0x001 | 작업의 모든 파일 전송 된 경우 이벤트를 생성 합니다. |
| 0x002 | 오류가 발생 하면 이벤트를 생성 합니다. |
| 0x004 | 알림을 사용 하지 않도록 설정 합니다. |
| 0x008 | 작업을 수정 하거나 진행 중인 전송 작업을 수행할 때 이벤트를 생성 합니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업에 대 한 알림 플래그를 검색 하려면:

```
bitsadmin /getnotifyflags myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
