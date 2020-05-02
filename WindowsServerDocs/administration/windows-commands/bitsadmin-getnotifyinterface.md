---
title: bitsadmin getnotifyinterface
description: 다른 프로그램에서 지정 된 작업에 대 한 COM 콜백 인터페이스를 등록 했는지 여부를 확인 하는 bitsadmin getnotifyinterface 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 40bf9dd8-b167-406a-80a6-a5a6f1b8cf7f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2158759067010292ca213f97014857354247b9c7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717735"
---
# <a name="bitsadmin-getnotifyinterface"></a>bitsadmin getnotifyinterface

다른 프로그램에서 지정 된 작업에 대 한 COM 콜백 인터페이스 (알림 인터페이스)를 등록 했는지 여부를 확인 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getnotifyinterface <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

#### <a name="output"></a>출력

이 명령의 출력은, **등록** 됨 또는 등록 **취소**됨을 표시 합니다.

> [!NOTE]
> 콜백 인터페이스를 등록 한 프로그램은 확인할 수 없습니다.

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업에 대 한 알림 인터페이스를 검색 하려면:

```
bitsadmin /getnotifyinterface myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
