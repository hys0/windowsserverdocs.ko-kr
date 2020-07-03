---
title: ftp mdelete
description: 원격 컴퓨터에서 파일을 삭제 하는 ftp mdelete 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8a80a8f5-e880-40a8-abc9-29a41836844f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 720ae8b5ebb0ef380f6547a85913cd84c6d98c7e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931174"
---
# <a name="ftp-mdelete"></a>ftp mdelete

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 컴퓨터에서 파일을 삭제 합니다.

## <a name="syntax"></a>구문
```
mdelete <remotefile>[...]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<remotefile>` | 삭제할 원격 파일을 지정 합니다. |

### <a name="examples"></a>예

원격 파일 *a.exe* 및 *b.exe*를 삭제 하려면 다음을 입력 합니다.

```
mdelete a.exe b.exe
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
