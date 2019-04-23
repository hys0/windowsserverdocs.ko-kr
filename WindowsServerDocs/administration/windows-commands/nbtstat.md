---
title: nbtstat
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d2ea99e-72f1-471f-9525-d2c49bf3be82
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0193152674dc934aa4f2d3be4dec54afc3066951
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867704"
---
# <a name="nbtstat"></a>nbtstat

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

TCP/IP (NetBT) 프로토콜 통계, 로컬 컴퓨터와 원격 컴퓨터에 대 한 NetBIOS 이름 테이블에서 NetBIOS를 표시 및 NetBIOS 이름을 캐시 합니다. **nbtstat** 등록 된 Windows 인터넷 이름 서비스 WINS () 이름과 NetBIOS 이름 캐시를 새로 고칠 수 있습니다. 매개 변수 없이 사용 **nbtstat** 도움말을 표시 합니다. 

## <a name="syntax"></a>구문

```
nbtstat [/a <remoteName>] [/A <IPaddress>] [/c] [/n] [/r] [/R] [/RR] [/s] [/S] [<Interval>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|/a <remoteName>|원격 컴퓨터의 NetBIOS 이름 테이블을 표시 합니다. 여기서 *로그인* 원격 컴퓨터의 NetBIOS 컴퓨터 이름입니다. NetBIOS 이름 테이블에는 해당 컴퓨터에서 실행 되는 NetBIOS 응용 프로그램에 해당 하는 NetBIOS 이름 목록입니다.|
|/A <IPaddress>|원격 컴퓨터의 점으로 구분 된 10 진수 표기법으로 IP 주소 지정 하는 원격 컴퓨터의 NetBIOS 이름 테이블을 표시 합니다.|
|/c|캐시, NetBIOS 이름 중 테이블 및 확인 된 IP 주소 이름을 NetBIOS의 내용의 표시 합니다.|
|/n|로컬 컴퓨터의 NetBIOS 이름 테이블을 표시합니다. 상태의 **등록** 이름을 브로드캐스트 또는 WINS 서버를 등록 했음을 나타냅니다.|
|/r|NetBIOS 이름 확인 통계가 표시 됩니다. 에 Windows XP 또는 WINS를 사용 하도록 구성 된 Windows Server 2003을 실행 하는 컴퓨터를이 매개 변수 확인 된 이름 수를 반환 및 브로드캐스트 및 WINS 등록 하 고 사용 하 여 합니다.|
|/R|NetBIOS 이름 캐시의 콘텐츠를 제거 하 고 다음 다시 로드 하는 # 사전에서 항목을 tagged는 **Lmhosts** 파일입니다.|
|/RR|해제 하 고에 등록 된 WINS 서버는 로컬 컴퓨터에 대 한 NetBIOS 이름을 새로 고칩니다.|
|/s|대상 IP 주소를 이름으로 변환 하려고 NetBIOS 클라이언트와 서버 세션을 표시 합니다.|
|/S|대상 IP 주소만으로 원격 컴퓨터 목록을 NetBIOS 클라이언트와 서버 세션을 표시 합니다.|
|<Interval>|선택한 통계를 다시에 지정 된 초 수를 다시 표시 *간격* 표시 합니다. 통계 표시를 중지 하려면 CTRL + C 키를 누릅니다. 이 매개 변수를 생략 하면 **nbtstat** 현재 구성 정보를 한 번만 출력 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   **nbtstat** 명령줄 매개 변수는 대/소문자 구분 합니다.

-   다음 표에서 설명 하 여 생성 되는 열 머리글 **nbtstat**:

    |제목|설명|
    |------|--------|
    |입력|받은 바이트 수입니다.|
    |출력|보낸 바이트 수입니다.|
    |입/출력|연결 인지 여부 (아웃 바운드) 컴퓨터에서 로컬 컴퓨터에 다른 컴퓨터에서 (인바운드).|
    |수명|제거 되는 이름 테이블 캐시 항목을 지우기 전까지 남은 시간입니다.|
    |로컬 이름|연결과 관련 된 로컬 NetBIOS 이름입니다.|
    |원격 호스트|이름 또는 원격 컴퓨터와 연결 된 IP 주소.|
    |<03>|NetBIOS 이름이의 마지막 바이트를 16 진수로 변환 합니다. 각 NetBIOS 이름에는 16 자입니다. 이 마지막 바이트는 특별 한 의미 하므로 이름이 같은 여러 번 마지막 바이트만 다르고 동일한 컴퓨터에 있을 수 있습니다. 예를 들어, < 20 > ASCII 텍스트에 공백이 있습니다.|
    |type|형식 이름입니다. 이름을 고유한 이름 또는 그룹 이름 수 있습니다.|
    |상태|여부를 원격 컴퓨터의 NetBIOS 서비스 실행 (등록 된) 또는 중복 된 컴퓨터 이름과 같은 서비스 (충돌)가 등록 합니다.|
    |State|NetBIOS 연결의 상태입니다.|

-   다음 표에서 가능한 NetBIOS 연결 상태를 설명 합니다.

    |State|설명|
    |-----|--------|
    |연결됨|세션 설정 되었습니다.|
    |연결 된|연결 끝점을 만들어야 IP 주소와 연결 합니다.|
    |수신 대기|이 끝점은 인바운드 연결에 사용할 수 있습니다.|
    |Idle|이 끝점 열려 있지만 연결을 수신할 수 없습니다.|
    |Connecting|세션이 연결 단계에 있으며 대상의 이름-IP 주소 매핑을 확인 하 고 있습니다.|
    |수락|인바운드 세션이 현재 허용 되 고 곧 연결 됩니다.|
    |다시 연결|세션 (첫 번째 시도에서 연결 하지 못했습니다 it)를 다시 연결 하려고 합니다.|
    |아웃바운드|세션이 연결 단계에 있으며 현재 TCP 연결이 생성 됩니다.|
    |인바운드|인바운드 세션이 연결 단계를 수 있습니다.|
    |연결 끊기|세션 연결을 끊는 중입니다.|
    |Disconnected|로컬 컴퓨터의 연결이 해제 하 고 원격 시스템에서 확인을 위해 대기 합니다.|

-   이 명령은 네트워크 연결에서 네트워크 어댑터의 속성에 구성 요소로 인터넷 프로토콜 (TCP/IP) 프로토콜을 설치 하는 경우에 사용할 수입니다.

## <a name="BKMK_Examples"></a>예제
CORP07의 NetBIOS 컴퓨터 이름 사용 하는 원격 컴퓨터의 NetBIOS 이름 테이블을 표시 하려면 다음을 입력 합니다.

```
nbtstat /a CORP07
```

10.0.0.99의 IP 주소를 지정 하는 원격 컴퓨터의 NetBIOS 이름 테이블을 표시 하려면 다음을 입력 합니다.

```
nbtstat /A 10.0.0.99
```

로컬 컴퓨터의 NetBIOS 이름 테이블을 표시 하려면 다음을 입력 합니다.

```
nbtstat /n
```

로컬 컴퓨터 NetBIOS 이름 캐시의 콘텐츠를 표시 하려면 다음을 입력 합니다.

```
nbtstat /c
```

NetBIOS 이름 캐시를 제거 하 고 다시 로드 하는 # 미리 tagged 로컬 Lmhosts 파일의 항목을 입력 합니다.

```
nbtstat /R
```

WINS 서버에 등록 된 NetBIOS 이름을 해제 하는 컬렉션을 다시 등록을 입력 합니다.

```
nbtstat /RR
```

5 초 마다 IP 주소를 통해 NetBIOS 세션 통계 표시를 하려면 다음을 입력 합니다.

```
nbtstat /S 5
```

## <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)


