---
title: telnet unset
description: 텔넷 설정 해제에 대 한 참조 문서는 이전에 설정 된 옵션을 해제 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da9a0d99-1930-4858-93c7-0e9c3797ee09
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3efbf7d4f2507d16dbe0beb704ab0c80467a56d3
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935295"
---
# <a name="telnet-unset"></a>텔넷: 설정 해제

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이전에 set 옵션을 해제합니다.

## <a name="syntax"></a>구문
```
u[nset] {bsasdel | crlf | delasbs | escape | localecho | logging | ntlm} [?]
```
#### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|bsasdel|보냅니다 **백스페이스** 으로 **백스페이스**합니다.|
|crlf|전송 된 **Enter** CR로 키입니다. 라고도 줄 바꿈 모드입니다.|
|delasbs|**Delete로** **삭제** 를 보냅니다.|
|이스케이프|이스케이프 문자 설정을 제거 합니다.|
|에코|에코를 해제합니다.|
|logging|로깅을 해제합니다.|
|ntlm|NTLM 인증을 해제합니다.|
|?|이 명령에 대 한 도움말을 표시 합니다.|
## <a name="examples"></a>예
로깅을 해제 합니다.
```
u logging
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
