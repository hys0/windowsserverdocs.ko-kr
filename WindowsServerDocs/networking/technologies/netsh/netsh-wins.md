---
title: Netsh(네트워크 셸) 예제 배치 파일
description: 이 항목을 사용하여 Windows Server 2016에서 Netsh를 사용하여 여러 작업을 수행하는 배치 파일을 만드는 방법을 배울 수 있습니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: c94e37a4-3637-4613-9eb5-ed604e831eca
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 73798ff4c8af11cc5cfb6461245ba7873f5d6f36
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316719"
---
# <a name="network-shell-netsh-example-batch-file"></a>네트워크 셸 \(Netsh\) 예제 배치 파일

적용 대상: Windows Server 2016

이 항목을 사용하여 Windows Server 2016에서 Netsh를 사용하여 여러 작업을 수행하는 배치 파일을 만드는 방법을 배울 수 있습니다. 이 예제 배치 파일에서는 **netsh wins** 컨텍스트가 사용됩니다.

## <a name="example-batch-file-overview"></a>예제 배치 파일 개요

배치 파일 및 기타 스크립트에서 Windows Internet Name Service \(WINS\)에 대해 Netsh 명령을 사용하여 작업을 자동화할 수 있습니다. 다음 배치 파일 예제에서는 WINS에 대해 Netsh 명령을 사용하여 다양한 관련 작업을 수행하는 방법을 보여 줍니다.

이 예제 배치 파일에서 WINS\-A는 IP 주소가 192.168.125.30인 WINS 서버이며 WINS\-B는 IP 주소가 192.168.0.189인 WINS 서버입니다.

예제 배치 파일은 다음 작업을 수행합니다.

- IP 주소가 192.168.0.205, 내\_레코드 \[04h\]인 동적 이름 레코드를 WINS\-A에 추가
- WINS\-B를 WINS\-A의 밀어넣기/끌어오기 복제 파트너로 설정
- WINS\-B에 연결한 다음, WINS\-A를 WINS\-B의 밀어넣기/끌어오기 복제 파트너로 설정
- WINS\-A에서 WINS\-B로 푸시 복제 시작
- WINS\-B에 연결하여 새 레코드, 내\_레코드가 성공적으로 복제되었는지 확인

## <a name="netsh-example-batch-file"></a>Netsh 예제 배치 파일

다음 예제 배치 파일에서 주석이 포함된 줄 앞에는 설명을 위해 "rem"이 붙습니다. Netsh는 주석을 무시합니다.

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

## <a name="netsh-wins-commands-used-in-the-example-batch-file"></a>예제 배치 파일에 사용된 Netsh WINS 명령

다음 섹션에는 이 예제 절차에서 사용되는 **netsh wins** 명령이 나열되어 있습니다.

- **서버** 현재 WINS 명령\-줄 컨텍스트를 해당 이름 또는 IP 주소로 지정된 서버로 이동합니다.
- **이름 추가** WINS 서버에 이름을 등록합니다.
- **파트너 추가** WINS 서버에 복제 파트너를 추가합니다.
- **밀어넣기 초기화** 밀어넣기 트리거를 시작하고 WINS 서버에 보냅니다.
- **이름 표시** WINS 서버 데이터베이스에 특정 레코드에 대한 자세한 정보를 표시합니다.  

자세한 내용은 참조 [Netsh(네트워크 셸)](netsh.md)를 참조하세요.
