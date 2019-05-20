---
title: 텔넷 집합
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 67316b5f-9c6f-43e3-86d5-dcff9ae2ac3e vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 18a49f2e4629b1410a1cec40fe77077c2988dce2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836124"
---
# <a name="telnet-set"></a>텔넷: 설정

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

옵션을 설정합니다.   
## <a name="syntax"></a>구문  
```  
set [bsasdel] [crlf] [delasbs] [escape <Char>] [localecho] [logfile <FileName>] [logging] [mode {console | stream}] [ntlm] [term {ansi | vt100 | vt52 | vtnt}] [?]  
```  
### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|bsasdel|보냅니다 **백스페이스** 으로 **삭제**합니다.|  
|crlf|CR / LF를 보냅니다 (0x0D, 0x0A) 때는 **Enter** 키를 누르면 됩니다. 새 줄 모드 라고합니다.|  
|delasbs|보냅니다 **삭제할** 으로 **백스페이스**합니다.|  
|이스케이프 <Character>|텔넷 클라이언트 프롬프트를 입력 하는 데 이스케이프 문자를 설정 합니다. 이스케이프 문자는 단일 문자 이거나의 조합 수는 **CTRL** 문자 더하기 키입니다. 제어 키 조합을 설정 하려면 키를 누른 채로 **CTRL** 할당 하려는 문자를 입력 하는 동안 키입니다.|  
|에코|로컬 에코를 설정합니다.|  
|logfile <FileName>|로컬 파일에 현재 텔넷 세션을 기록 합니다. 이 옵션을 설정 하면 로깅이 자동으로 시작 합니다.|  
|logging|로깅을 설정합니다. 로그 파일이 설정 되 면 오류 메시지가 나타납니다.|  
|{콘솔 &#124; 화면} 모드|작업 모드를 설정합니다.|  
|ntlm|NTLM 인증을 설정합니다.|  
|{ansi &#124, v t 100 &#124, v t 52 &#124, vtnt} 용어|터미널 유형을 설정합니다.|  
|?|이 명령에 대 한 도움말을 표시 합니다.|  
## <a name="remarks"></a>설명  
1.  사용할 수는 **설정 되지 않은** 명령을 이전에 설정 된 옵션을 해제 합니다.  
2.  텔넷 영어가 아닌 버전에는 **코드** <option> 를 사용할 수 있습니다. **코드 집합** <option> 은 현재 코드를 다음 중 하나를 사용할 수 있는 옵션으로 설정 합니다. **shift JIS**, **일본어 EUC**, **JIS 간지**, **JIS 간지 (78)** 하십시오 **DEC 간지**하십시오 **NEC 간지**합니다. 원격 컴퓨터에서 설정 하는 동일한 코드를 설정 해야 합니다.  
## <a name="BKMK_Examples"></a>예제  
로그 파일을 설정 하 고 로컬 파일 tnlog.txt에 로깅을 시작합니다  
```  
set logfile tnlog.txt  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
