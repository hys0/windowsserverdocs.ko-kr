---
title: bitsadmin setreplyfilename
description: '**Bitsadmin setreplyfilename**에 대 한 Windows 명령 항목으로, 서버 업로드-회신이 포함 된 파일의 경로를 지정 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c26d3342-0533-40b1-a13e-e09678232b25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6c476073cb22ff66bcefc75a45fcd0526cdf3d25
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122733"
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
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| file_path | 서버 업로드-회신이 배치 될 위치입니다. |

## <a name="examples"></a>예

다음 예에서는 이름이 *Mydownloadjob*인 작업에 대 한 upload-reply 파일 이름 파일 경로를 설정 합니다.

```
C:\>bitsadmin /setreplyfilename myDownloadJob c:\upload-reply
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)