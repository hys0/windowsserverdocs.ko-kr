---
title: bitsadmin getsecurityflags
description: Bitsadmin getsecurityflags 명령에 대 한 참조 항목으로, 전송 하는 동안 서버 인증서에서 수행 되는 URL 리디렉션과 검사에 대 한 HTTP 보안 플래그를 보고 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c2e73519-34f4-487b-af11-97d5d08ef9bb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 41b710f9897f24eb4161d9379dc3b1f89b141472
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717548"
---
# <a name="bitsadmin-getsecurityflags"></a>bitsadmin getsecurityflags

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

URL 리디렉션 및 검사에 대 한 보안 플래그 보고서 HTTP 전송 하는 동안 서버 인증서에서 수행 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getsecurityflags <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업에서 보안 플래그를 검색 하려면 다음을 수행 합니다.

```
bitsadmin /getsecurityflags myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
