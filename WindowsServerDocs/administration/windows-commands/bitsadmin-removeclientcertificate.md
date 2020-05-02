---
title: bitsadmin removeclientcertificate
description: 작업에서 클라이언트 인증서를 제거 하는 bitsadmin removeclientcertificate 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b417c3e5-aadd-4fcc-968f-45d8b67ca516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 513830f6048f78aa528fa22cb590571e718452c2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717065"
---
# <a name="bitsadmin-removeclientcertificate"></a>bitsadmin removeclientcertificate

작업에서 클라이언트 인증서를 제거합니다.

## <a name="syntax"></a>구문

```
bitsadmin /removeclientcertificate <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업에서 클라이언트 인증서를 제거 하려면 다음을 수행 합니다.

```
bitsadmin /removeclientcertificate myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
