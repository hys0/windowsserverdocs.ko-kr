---
title: bitsadmin removeclientcertificate
description: '**Bitsadmin removeclientcertificate**에 대 한 Windows 명령 항목-작업에서 클라이언트 인증서를 제거 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b417c3e5-aadd-4fcc-968f-45d8b67ca516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 312226b73b91385436e15c4afbb49df161258768
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123104"
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
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

다음 예에서는 *Mydownloadjob*이라는 작업에서 클라이언트 인증서를 제거 합니다.

```
C:\>bitsadmin /removeclientcertificate myDownloadJob 
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)