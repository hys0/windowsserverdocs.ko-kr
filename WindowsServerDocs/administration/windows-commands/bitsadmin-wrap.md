---
title: bitsadmin wrap
description: 명령 창의 가장 오른쪽 가장자리를 벗어나 확장 되는 출력 텍스트 줄을 다음 줄로 래핑하는 bitsadmin wrap 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 14e57522-539d-4621-ad15-09f7a44ccab7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8c1c2c78fd3cc78674ef497526ba236ad058fe83
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707570"
---
# <a name="bitsadmin-wrap"></a>bitsadmin wrap

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

명령 창의 가장 오른쪽 가장자리를 벗어나 확장 되는 출력 텍스트 줄을 다음 줄로 래핑합니다. 다른 스위치 앞에이 스위치를 지정 해야 합니다.

기본적으로 [bitsadmin 모니터](bitsadmin-monitor.md) 스위치를 제외한 모든 스위치는 출력 텍스트를 래핑합니다.

## <a name="syntax"></a>구문

```
bitsadmin /wrap <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ---------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

*Mydownloadjob* 이라는 작업에 대 한 정보를 검색 하 고 출력 텍스트를 래핑합니다.

```
bitsadmin /wrap /info myDownloadJob /verbose
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
