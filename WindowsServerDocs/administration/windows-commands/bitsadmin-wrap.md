---
title: bitsadmin wrap
description: '**Bitsadmin 줄 바꿈**에 대 한 Windows 명령 항목으로, 명령 창의 가장 오른쪽 가장자리를 벗어나 확장 되는 출력 텍스트 줄을 다음 줄로 래핑합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 14e57522-539d-4621-ad15-09f7a44ccab7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e754a765d94661baf24190431b455584d29991ec
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122561"
---
# <a name="bitsadmin-wrap"></a>bitsadmin wrap

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

명령 창의 가장 오른쪽 가장자리를 벗어나 확장 되는 출력 텍스트 줄을 다음 줄로 래핑합니다. 다른 스위치 앞에이 스위치를 지정 해야 합니다.

기본적으로 [bitsadmin 모니터](bitsadmin-monitor.md) 스위치를 제외한 모든 스위치는 출력 텍스트를 래핑합니다.

## <a name="syntax"></a>구문

```
bitsadmin /wrap <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ---------- |
| 작업 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

다음 예제에서는 이름이 *Mydownloadjob* 인 작업에 대 한 정보를 검색 하 고 출력을 래핑합니다.

```
C:\>bitsadmin /wrap /info myDownloadJob /verbose
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
