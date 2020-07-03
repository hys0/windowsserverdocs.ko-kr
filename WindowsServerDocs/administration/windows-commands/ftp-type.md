---
title: ftp type
description: 파일 전송 유형을 설정 하거나 표시 하는 ftp 유형 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6e96dcd4-08f8-4e7b-90b7-1e1761fea4c7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ea0b2a319dae65104db8a215e17fa4b579ee6ffa
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931196"
---
# <a name="ftp-type"></a>ftp type

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

설정 하거나 파일 전송 유형을 표시 합니다. **Ftp** 명령은 ASCII (기본) 및 이진 이미지 파일 전송 형식을 모두 지원 합니다.

- 텍스트 파일을 전송할 때 ASCII를 사용 하는 것이 좋습니다. ASCII 모드에서는 네트워크 표준 문자 집합 사이에 문자 변환이 수행 됩니다. 예를 들어, 줄의 끝 문자는 대상 운영 체제에 따라 필요에 따라 변환 됩니다.

- 실행 파일을 전송할 때 이진 파일을 사용 하는 것이 좋습니다. 이진 모드에서 파일은 1 바이트 단위로 전송 됩니다.

## <a name="syntax"></a>구문

```
type [<typename>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `[<typename>]` | 파일 전송 유형을 지정합니다. 이 매개 변수를 지정 하지 않으면 현재 형식이 표시 됩니다.|

### <a name="examples"></a>예

파일 전송 유형을 ASCII로 설정 하려면 다음을 입력 합니다.

```
type ascii
```

전송 파일 형식을 binary로 설정 하려면 다음을 입력 합니다.

```
type binary
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
