---
title: telnet
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b70a6156-9413-4300-84ce-a34c467e2b4e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b1621a10b9b445e87eb6bc16a8d7f52a64c146a3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385147"
---
# <a name="telnet"></a>telnet

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

텔넷 서버 서비스를 실행 하는 컴퓨터와 통신 합니다. 
## <a name="syntax"></a>구문
```
telnet [/a] [/e <EscapeChar>] [/f <FileName>] [/l <UserName>] [/t {vt100 | vt52 | ansi | vtnt}] [<Host> [<Port>]] [/?]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/ a|자동 로그온을 시도 합니다. 제외 하 고/l 옵션과 동일는 현재 로그온 된 사용자 이름을 사용 합니다.|
|/e \<EscapeChar >|텔넷 클라이언트 프롬프트를 입력 하는 데 사용 되는 이스케이프 문자입니다.|
|/f \< 파일 이름 >|클라이언트 쪽 로깅에 사용 되는 파일 이름입니다.|
|/l \< 사용자 이름 >|원격 컴퓨터에서 사용 하 여 로그온 사용자 이름을 지정 합니다.|
|/t {v t 100 &#124; v t 52 &#124; ansi 및 &#124; vtnt}|터미널 유형을 지정합니다. 지원 되는 터미널 유형은 v t 100, v t 52, ansi 및 vtnt입니다.|
|\<Host > [\<Port >]|호스트 이름 또는 원격 컴퓨터에 연결 하 고 선택적으로 사용 하 여 TCP 포트의 IP 주소를 지정 합니다 (기본값은 TCP 포트 23).|
|/?|명령 프롬프트에 도움말을 표시합니다. 또는 /h를 입력할 수 있습니다.|

## <a name="remarks"></a>설명
-   이 명령을 실행 하려면 먼저 텔넷 클라이언트 소프트웨어를 설치 해야 합니다. 자세한 내용은 [Telnet 설치](https://technet.microsoft.com/library/cc754293(v=ws.10).aspx)를 참조 하세요.
-   텔넷 프롬프트 (**Microsoft telnet >** )로 표시 되는 텔넷 컨텍스트를 입력 하는 매개 변수 없이 텔넷을 실행할 수 있습니다. 텔넷 프롬프트에서 텔넷 명령을 사용 하 여 텔넷 클라이언트를 실행 하는 컴퓨터를 관리할 수 있습니다.

## <a name="BKMK_Examples"></a>예와
Telnet을 사용 하 여 telnet.microsoft.com에서 텔넷 서버 서비스를 실행 하는 컴퓨터에 연결 합니다.
```
telnet telnet.microsoft.com
```
Telnet을 사용 하 여 TCP 포트 44에서 telnet.microsoft.com의 텔넷 서버 서비스를 실행 하는 컴퓨터에 연결 하 고 telnetlog 라는 로컬 파일에 세션 작업을 기록 합니다.
```
telnet /f telnetlog.txt telnet.microsoft.com 44
```

## <a name="additional-references"></a>추가 참조
-   [텔넷 설치](https://technet.microsoft.com/library/cc754293(v=ws.10).aspx)
-   [텔넷 기술 참조](https://technet.microsoft.com/library/cc754987(v=ws.10).aspx)
-   [명령줄 구문 키](command-line-syntax-key.md)
