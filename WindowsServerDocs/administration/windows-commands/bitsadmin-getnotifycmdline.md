---
title: bitsadmin getnotifycmdline
description: '**Bitsadmin getnotifycmdline**에 대 한 Windows 명령 항목-작업에서 데이터 전송을 완료할 때 실행 되는 명령줄 명령을 검색 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90fa33e6-aca5-4a23-82bd-19a9f13f8416
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 24b49b3fa0c2dafb999d8cb9c6e0c13ae68bf6f4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850596"
---
# <a name="bitsadmin-getnotifycmdline"></a>bitsadmin getnotifycmdline

작업에서 데이터 전송을 완료할 때 실행할 명령줄 명령을 검색 합니다.

> [!NOTE]
> 이 명령은 BITS 1.2 이전 버전에서는 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /getnotifycmdline <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 *Mydownloadjob* 이라는 작업이 완료 될 때 서비스에서 사용 하는 명령줄 명령을 검색 합니다.

```
C:\>bitsadmin /getnotifycmdline myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)