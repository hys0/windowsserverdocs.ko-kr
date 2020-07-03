---
title: bitsadmin getproxybypasslist
description: 지정 된 작업에 대 한 프록시 바이패스 목록을 검색 하는 bitsadmin getproxybypasslist 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 50959be3-7014-4bc9-9a7b-68f1ff94a94a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 67e6e4a54bb8c4929acbbaa47c78e33bab95a283
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926833"
---
# <a name="bitsadmin-getproxybypasslist"></a>bitsadmin getproxybypasslist

지정된 된 작업에 대 한 프록시 무시 목록을 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getproxybypasslist <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

### <a name="remarks"></a>설명

바이패스 목록에는 호스트 이름 또는 IP 주소 또는 둘 다 포함 한 프록시를 통과 하지 않을 하 합니다. 이 목록에는 `<local>` 동일한 LAN에 있는 모든 서버를 참조 하는가 포함 될 수 있습니다. 목록은 세미콜론 (;) 또는 공백으로 구분 됩니다.

## <a name="examples"></a>예

이름이 *Mydownloadjob*인 작업에 대 한 프록시 무시 목록을 검색 하려면:

```
bitsadmin /getproxybypasslist myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
