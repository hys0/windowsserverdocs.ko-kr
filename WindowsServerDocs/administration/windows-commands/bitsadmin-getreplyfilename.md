---
title: bitsadmin getreplyfilename
description: '**Bitsadmin getreplyfilename**에 대 한 Windows 명령 항목-작업에 대 한 서버 업로드 회신이 들어 있는 파일의 경로를 가져옵니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 85447184-1732-4816-a365-2e3599551bf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 541a6e60d641405b5da2e65fecbbbe87468c8702
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850496"
---
# <a name="bitsadmin-getreplyfilename"></a>bitsadmin getreplyfilename

작업에 대 한 서버 업로드 회신이 들어 있는 파일의 경로를 가져옵니다.

> [!NOTE]
> 이 명령은 BITS 1.2 이전 버전에서는 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /getreplyfilename <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |


## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 upload reply 파일 이름을 검색 *Mydownloadjob*합니다.

```
C:\>bitsadmin /getreplyfilename myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)