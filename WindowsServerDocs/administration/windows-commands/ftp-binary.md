---
title: ftp binary
description: 파일 전송 형식을 이진으로 설정 하는 ftp 이진 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ee925b4d-85d2-47b1-b7d6-3832b7ec5505
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: daf300598f8a31fc35d5702b5bd42507dd9e8211
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925957"
---
# <a name="ftp-binary"></a>ftp binary

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

파일 전송 형식을 이진으로 설정 합니다. **Ftp** 명령은 ASCII (기본) 및 이진 이미지 파일 전송 유형을 모두 지원 하지만 실행 파일을 전송할 때는 이진을 사용 하는 것이 좋습니다. 이진 모드에서 파일은 1 바이트 단위로 전송 됩니다.

## <a name="syntax"></a>구문

```
binary
```

### <a name="examples"></a>예

파일 전송 유형을 binary로 설정 하려면 다음을 입력 합니다.

```
binary
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ftp ascii 명령](ftp-ascii.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
