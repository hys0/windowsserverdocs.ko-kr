---
title: Netsh(네트워크 셸) 배치 파일 예
description: 이 항목을 사용 하 여 Windows Server 2016의 Netsh를 사용 하 여 여러 작업을 수행 하는 배치 파일을 만드는 방법을 배울 수 있습니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: c94e37a4-3637-4613-9eb5-ed604e831eca
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 86fbe66978f7c09a332bba16a27a13fa029cb5a6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401915"
---
# <a name="network-shell-netsh-example-batch-file"></a>네트워크 셸 \(Netsh\) 예제 배치 파일

적용 대상: Windows Server 2016

이 항목을 사용 하 여 Windows Server 2016의 Netsh를 사용 하 여 여러 작업을 수행 하는 배치 파일을 만드는 방법을 배울 수 있습니다. 이 예제 배치 파일에서는 **netsh wins** 컨텍스트가 사용 됩니다.

## <a name="example-batch-file-overview"></a>배치 파일의 예 개요

Windows 인터넷 이름 서비스에 대 한 Netsh 명령을 사용 하 여 배치 파일 및 기타 스크립트에서 작업을 자동화 하는 \(WINS\)를 사용할 수 있습니다. 다음 배치 파일 예제에서는 WINS에 대해 Netsh 명령을 사용 하 여 다양 한 관련 작업을 수행 하는 방법을 보여 줍니다.

이 예제 배치 파일에서 WINS\-는 IP 주소가 192.168.125.30이 고 WINS\-B가 IP 주소가 192.168.0.189 인 wins 서버입니다.

예제 배치 파일은 다음 작업을 수행 합니다.

- IP 주소가 192.168.0.205, 내\_레코드 \[04h\]인 동적 이름 레코드를 WINS\-에 추가 합니다.
- Wins\-B를 WINS\-밀어넣기/끌어오기 복제 파트너로 설정 합니다.
- Wins\-B에 연결한 다음 wins\-A를 WINS의 밀어넣기/끌어오기 복제 파트너로 설정\-B
- WINS\-에서 WINS\-B로의 푸시 복제를 시작 합니다.
- WINS\-B에 연결 하 여 새 레코드, 내\_레코드가 성공적으로 복제 되었는지 확인 합니다.

## <a name="netsh-example-batch-file"></a>Netsh 예제 배치 파일

다음 예제 배치 파일에서 주석이 포함 된 줄 앞에는 "rem"이 붙습니다. Netsh는 주석을 무시 합니다.

    rem: Begin example batch file.
    
    rem two WINS servers:
    
    rem (WINS-A) 192.168.125.30
    
    rem (WINS-B) 192.168.0.189
    
    rem 1. Connect to (WINS-A), and add the dynamic name MY\_RECORD \[04h\] to the (WINS-A) database.
    
    netsh wins server 192.168.125.30 add name Name=MY\_RECORD EndChar=04 IP={192.168.0.205}
    
    rem 2. Connect to (WINS-A), and set (WINS-B) as a push/pull replication partner of (WINS-A).
    
    netsh wins server 192.168.125.30 add partner Server=192.168.0.189 Type=2
    
    rem 3. Connect to (WINS-B), and set (WINS-A) as a push/pull replication partner of (WINS-B).
    
    netsh wins server 192.168.0.189 add partner Server=192.168.125.30 Type=2
    
    rem 4. Connect back to (WINS-A), and initiate a push replication to (WINS-B).
    
    netsh wins server 192.168.125.30 init push Server=192.168.0.189 PropReq=0
    
    rem 5. Connect to (WINS-B), and check that the record MY\_RECORD \[04h\] was replicated successfully.
    
    netsh wins server 192.168.0.189 show name Name=MY\_RECORD EndChar=04
    
    rem 6. End example batch file.

## <a name="netsh-wins-commands-used-in-the-example-batch-file"></a>예제 배치 파일에 사용 된 Netsh WINS 명령

다음 섹션에는이 예제 절차에서 사용 되는 **netsh wins** 명령이 나열 되어 있습니다.

- **서버**. 현재 WINS 명령\-줄 컨텍스트를 이름 또는 IP 주소로 지정 된 서버로 이동 합니다.
- **이름을 추가**합니다. WINS 서버에 이름을 등록 합니다.
- **파트너를 추가**합니다. WINS 서버에 복제 파트너를 추가 합니다.
- **푸시를 초기화**합니다. 밀어넣기 트리거를 시작 하 고 WINS 서버에 보냅니다.
- **이름을 표시**합니다. WINS 서버 데이터베이스의 특정 레코드에 대 한 자세한 정보를 표시 합니다.  

자세한 내용은 [Netsh (네트워크 셸)](netsh.md)를 참조 하세요.
