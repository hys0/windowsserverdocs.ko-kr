---
title: bitsadmin getclientcertificate
description: 작업에서 클라이언트 인증서를 검색 하는 bitsadmin getclientcertificate 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fc8f408-085e-43a0-9fa8-3d798ef107b1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5113214f106aea21b1b13f08cc08002237730daf
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928515"
---
# <a name="bitsadmin-getclientcertificate"></a>bitsadmin getclientcertificate

작업에서 클라이언트 인증서를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getclientcertificate <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

이름이 *Mydownloadjob*인 작업에 대 한 클라이언트 인증서를 검색 하려면:

```
bitsadmin /getclientcertificate myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
