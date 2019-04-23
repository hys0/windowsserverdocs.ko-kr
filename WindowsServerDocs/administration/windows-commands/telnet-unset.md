---
title: telnet unset
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da9a0d99-1930-4858-93c7-0e9c3797ee09 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 37c4d84d1664fdc13ea7ffec60bf981b264dba00
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853894"
---
# <a name="telnet-unset"></a>telnet: unset

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이전에 set 옵션을 해제합니다.   
## <a name="syntax"></a>구문  
```  
u[nset] {bsasdel | crlf | delasbs | escape | localecho | logging | ntlm} [?]  
```  
### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|bsasdel|보냅니다 **백스페이스** 으로 **백스페이스**합니다.|  
|crlf|전송 된 **Enter** CR로 키입니다. 라고도 줄 바꿈 모드입니다.|  
|delasbs|보냅니다 **삭제할** 으로 **삭제**합니다.|  
|이스케이프|이스케이프 문자 설정을 제거합니다.|  
|에코|에코를 해제합니다.|  
|logging|로깅을 해제합니다.|  
|ntlm|NTLM 인증을 해제합니다.|  
|?|이 명령에 대 한 도움말을 표시 합니다.|  
## <a name="BKMK_Examples"></a>예제  
로깅을 해제 합니다.  
```  
u logging  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
