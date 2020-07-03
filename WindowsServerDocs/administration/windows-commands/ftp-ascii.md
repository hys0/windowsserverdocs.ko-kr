---
title: ftp ascii
description: Ftp ascii 명령에 대 한 참조 문서로, 파일 전송 형식을 ASCII로 설정 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 523be48e-eab0-4237-8fb5-ca222824f0b6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e3ba10ba6498b48a19aacf6235c84a890c7db63a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933320"
---
# <a name="ftp-ascii"></a>ftp ascii

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ASCII 파일 전송 유형을 설정합니다. **Ftp** 명령은 ascii (기본) 및 이진 이미지 파일 전송 유형을 모두 지원 하지만 텍스트 파일을 전송할 때 ascii를 사용 하는 것이 좋습니다. ASCII 모드에서는 네트워크 표준 문자 집합 사이에 문자 변환이 수행 됩니다. 예를 들어, 줄의 끝 문자는 대상 운영 체제에 따라 필요에 따라 변환 됩니다.

## <a name="syntax"></a>구문

```
ascii
```

### <a name="examples"></a>예

파일 전송 유형을 ASCII로 설정 하려면 다음을 입력 합니다.

```
ascii
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ftp 이진 명령](ftp-binary.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
