---
title: telnet
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6439a91d82d6d199666629e333d8130bf65a384b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858564"
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
|/ a|자동 로그온을 시도 합니다. /L 옵션와 동일 사용을 제외 하 고 현재 로그온 한 사용자가의 이름에 있습니다.|
|/e \<EscapeChar>|텔넷 클라이언트 프롬프트를 입력 하는 데 사용 되는 문자를 이스케이프 합니다.|
|/f \<FileName>|클라이언트 쪽 로깅에 사용 되는 파일 이름입니다.|
|/l \<사용자 이름 >|원격 컴퓨터에서 사용 하 여 로그온 사용자 이름을 지정 합니다.|
|/t {v t 100 &#124; v t 52 &#124; ansi 및 &#124; vtnt}|터미널 유형을 지정합니다. 지원 되는 터미널 유형은 v t 100, v t 52, ansi 및 vtnt입니다.|
|\<호스트 > [\<포트 >]|호스트 이름 또는 원격 컴퓨터에 연결 하 고 선택적으로 사용 하 여 TCP 포트의 IP 주소를 지정 합니다 (기본값은 TCP 포트 23).|
|/?|명령 프롬프트에 도움말을 표시합니다. 또는 /h를 입력할 수 있습니다.|

## <a name="remarks"></a>설명
-   이 명령은 실행 하기 전에 텔넷 클라이언트 소프트웨어를 설치 해야 합니다. 자세한 내용은 [텔넷 설치](https://technet.microsoft.com/library/cc754293(v=ws.10).aspx)합니다.
-   텔넷 텔넷 프롬프트로 텔넷 컨텍스트를 입력 매개 변수 없이 실행할 수 있습니다 (**Microsoft 텔넷 >** ). 텔넷 프롬프트에서 텔넷 클라이언트를 실행 하는 컴퓨터를 관리 하는 텔넷 명령을 사용할 수 있습니다.

## <a name="BKMK_Examples"></a>예제
텔넷을 사용 하 여 telnet.microsoft.com에 텔넷 서버 서비스를 실행 하는 컴퓨터에 연결 합니다.
```
telnet telnet.microsoft.com
```
텔넷을 사용 하 여 TCP 포트 44에서 telnet.microsoft.com에 텔넷 서버 서비스를 실행 중인 컴퓨터에 연결 하 고 telnetlog.txt 라는 로컬 파일에서 세션 활동을 기록 합니다.
```
telnet /f telnetlog.txt telnet.microsoft.com 44
```

## <a name="additional-references"></a>추가 참조
-   [텔넷 설치](https://technet.microsoft.com/library/cc754293(v=ws.10).aspx)
-   [텔넷 기술 참조](https://technet.microsoft.com/library/cc754987(v=ws.10).aspx)
-   [명령줄 구문 키](command-line-syntax-key.md)
