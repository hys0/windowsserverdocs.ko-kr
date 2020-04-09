---
title: bitsadmin getreplydata
description: '**Bitsadmin getreplydata**에 대 한 Windows 명령 항목-작업에 대 한 16 진수 형식으로 서버의 업로드 응답 데이터를 검색 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 819f97d5-b255-4b2d-9f63-0daa73915434
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fb83ca93f8e73445788d926e0d5e6db4c774d759
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850506"
---
# <a name="bitsadmin-getreplydata"></a>bitsadmin getreplydata

작업에 대 한 16 진수 형식의 서버 업로드 응답 데이터를 검색 합니다.

> [!NOTE]
> 이 명령은 BITS 1.2 이전 버전에서는 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /getreplydata <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 업로드 회신 데이터를 검색 *Mydownloadjob*합니다.

```
C:\>bitsadmin /getreplydata myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)