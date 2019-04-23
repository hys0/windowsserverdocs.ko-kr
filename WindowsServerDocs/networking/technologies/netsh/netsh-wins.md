---
title: Netsh(네트워크 셸) 배치 파일 예
description: Windows Server 2016에서 Netsh를 사용 하 여 여러 작업을 수행 하는 배치 파일을 만드는 방법에 알아보려면이 항목에서는 사용할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: c94e37a4-3637-4613-9eb5-ed604e831eca
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b0528cfaef201ba30e00e30f56a763be39a6b828
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880174"
---
# <a name="network-shell-netsh-example-batch-file"></a>네트워크 셸 \(Netsh\) 배치 파일 예

적용 대상: Windows Server 2016

Windows Server 2016에서 Netsh를 사용 하 여 여러 작업을 수행 하는 배치 파일을 만드는 방법에 알아보려면이 항목에서는 사용할 수 있습니다. 이 예제 배치 파일에는 **netsh wins** 컨텍스트가 사용 됩니다.

## <a name="example-batch-file-overview"></a>예제에서는 일괄 처리 파일 개요

Windows Internet Name Service에 대 한 Netsh 명령을 사용할 수 있습니다 \(WINS\) 배치 파일에 작업을 자동화 하는 다른 스크립트입니다. 다음 배치 파일 예제 WINS에 대 한 Netsh 명령을 사용 하 여 다양 한 관련된 작업을 수행 하는 방법에 설명 합니다.

이 예제 배치 파일에서 WINS\-A 192.168.125.30 IP 주소 및 WINS를 사용 하 여 WINS 서버는\-B는 192.168.0.189 IP 주소를 사용 하 여 WINS 서버.

배치 파일 예는 다음과 같은 작업을 수행합니다.

- 레코드를 추가 동적 이름을 IP 주소로 192.168.0.205, MY\_레코드 \[04 h\], wins\-는
- WINS 설정\-WINS의 푸시/끌어오기 복제 파트너로 B\-는
- WINS 연결할\-B 및 집합 WINS\-WINS의 푸시/끌어오기 복제 파트너는\-B
- Wins에서 밀어넣기 복제를 시작\-wins는\-B
- WINS 연결할\-되어 있는지 확인 하기 위해 B 새 레코드를 내\_레코드를 성공적으로 복제 된

## <a name="netsh-example-batch-file"></a>Netsh 배치 파일 예

다음 예제에서는 배치 파일에서 주석을 포함 하는 줄 앞에 "rem" 묶어 표시에 대 한 합니다. Netsh는 주석을 무시합니다.

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

## <a name="netsh-wins-commands-used-in-the-example-batch-file"></a>예제에서는 배치 파일에서 사용 되는 WINS Netsh 명령

다음 섹션 나열 된 **netsh wins** 이 예제 절차에서 사용 되는 명령입니다.

- **서버**합니다. 현재 WINS 명령 이동\-줄 컨텍스트 이름 또는 IP 주소에서 지정한 서버를 합니다.
- **이름을 추가**합니다. WINS 서버의 이름을 등록합니다.
- **파트너 추가**합니다. WINS 서버에서 복제 파트너를 추가합니다.
- **init push**. 시작 하 고 밀어넣기 트리거 WINS 서버에 보냅니다.
- **이름 표시**합니다. WINS 서버 데이터베이스에 있는 특정 레코드에 대 한 자세한 정보를 표시 합니다.  

자세한 내용은 [네트워크 셸 (Netsh)](netsh.md)합니다.
