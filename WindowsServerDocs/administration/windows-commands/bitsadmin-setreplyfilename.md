---
title: bitsadmin setreplyfilename
description: 서버 업로드-회신이 포함 된 파일의 경로를 지정 하는 bitsadmin setreplyfilename 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c26d3342-0533-40b1-a13e-e09678232b25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2f0bd184db274dc915817ff3e26ae2c686190c27
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720485"
---
# <a name="bitsadmin-setreplyfilename"></a>bitsadmin setreplyfilename

서버 업로드-회신이 들어 있는 파일의 경로를 지정 합니다.

> [!NOTE]
> 이 명령은 BITS 1.2 이전 버전에서는 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /setreplyfilename <job> <file_path>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| file_path | 서버 업로드-회신이 배치 될 위치입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업의 업로드-회신 파일 이름 파일 경로를 설정 하려면 다음을 수행 합니다.

```
bitsadmin /setreplyfilename myDownloadJob c:\upload-reply
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
