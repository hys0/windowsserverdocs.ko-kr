---
title: telnet send
description: 텔넷 서버에 텔넷 명령을 보내는 텔넷 송신에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c217abc-1182-466e-914c-1ff16755021b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 44a0415a3516fcb15cd292c9e4c9c0a4a18e5ad9
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85937374"
---
# <a name="telnet-send"></a>텔넷: 송신

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

텔넷 서버에 텔넷 명령을 보냅니다.

## <a name="syntax"></a>구문
```
sen[d] {ao | ayt | brk | esc | ip | synch | <string>} [?]
```
#### <a name="parameters"></a>매개 변수

| 매개 변수 |                     설명                      |
|-----------|------------------------------------------------------|
|    ao     |       텔넷 명령 중단 출력을 보냅니다.        |
|    ayt    |       텔넷 명령을 보냅니다.       |
|    brk    |            텔넷 명령 brk를 보냅니다.            |
|    esc    |      현재 텔넷 이스케이프 문자를 보냅니다.      |
|    ip     |     텔넷 명령 인터럽트 프로세스를 보냅니다.     |
|   동기화   |           텔넷 명령 동기화를 보냅니다.           |
| <string>  | 텔넷 서버에 입력 하는 모든 문자열을 보냅니다. |
|     ?     |     이 명령과 관련 된 도움말을 표시 합니다.      |

## <a name="examples"></a>예
그러면 텔넷 서버에 전송 됩니다.
```
sen ayt
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
