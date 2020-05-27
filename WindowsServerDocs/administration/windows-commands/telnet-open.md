---
title: 텔넷 열기
description: 텔넷 서버에 연결 하는 텔넷 열기에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
s.topic: article
ms.assetid: e30ad68c-2366-4754-ac36-311a2392902a vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ed2c00b44143942ba1ccb77eec17ca975f23b498
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821323"
---
# <a name="telnet-open"></a>텔넷: 열기

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

텔넷 서버에 연결 합니다.

## <a name="syntax"></a>구문
```
o[pen] <hostname> [<Port>]
```
#### <a name="parameters"></a>매개 변수

| 매개 변수  |                                        설명                                         |
|------------|--------------------------------------------------------------------------------------------|
| <hostname> |                         컴퓨터 이름 또는 IP 주소를 지정합니다.                         |
|  [<Port>]  | 텔넷 서버가 수신 대기 하는 TCP 포트를 지정 합니다. 기본값은 23 TCP 포트. |

## <a name="examples"></a>예
Telnet.microsoft.com에서 텔넷 서버에 연결 합니다.
```
o telnet.microsoft.com
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
