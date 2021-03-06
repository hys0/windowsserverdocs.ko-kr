---
title: telnet open
description: 텔넷 서버에 연결 하는 텔넷 열기에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
s.topic: article
ms.assetid: e30ad68c-2366-4754-ac36-311a2392902a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f3b27088d464e62b24479eaa87f44b91f7d95d12
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935330"
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
