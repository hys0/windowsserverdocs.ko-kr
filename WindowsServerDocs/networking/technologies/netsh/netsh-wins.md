---
title: 네트워크 셸 (Netsh) 예 배치 파일
description: Netsh Windows Server 2016에 사용 하 여 여러 가지 작업을 수행 하는 배치 파일 만드는 방법을이 항목을 사용할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: c94e37a4-3637-4613-9eb5-ed604e831eca
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b0528cfaef201ba30e00e30f56a763be39a6b828
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="network-shell-netsh-example-batch-file"></a>네트워크 셸 \(Netsh\) 예 배치 파일

Windows Server 2016 적용 됩니다.

Netsh Windows Server 2016에 사용 하 여 여러 가지 작업을 수행 하는 배치 파일 만드는 방법을이 항목을 사용할 수 있습니다. 이 들어 배치 파일에는 **netsh wins** 컨텍스트가 사용 됩니다.

## <a name="example-batch-file-overview"></a>예 배치 파일 개요

Windows Internet 이름 서비스 \(WINS\) 배치 파일에서에 대 한 Netsh 명령 및 기타 스크립트 작업 자동화을 사용할 수 있습니다. 다음 배치 파일 예제 wins Netsh 명령을 사용 하 여 다양 한 관련된 작업을 수행 하는 방법을 보여 줍니다.

이 들어 배치 파일에 WINS\ A 192.168.125.30 IP 주소와 WINS 서버 이며 WINS\ B WINS 서버 192.168.0.189 IP 주소를 사용 합니다.

배치 파일의 예는 다음과 같은 작업을 수행 합니다.

- 동적 이름 레코드 192.168.0.205 IP 주소, MY\_RECORD \[04h\ 추가]에 WINS\ A
- 푸시/방향으로 빼냅니다 복제 파트너 WINS\ a WINS\ B 설정
- WINS\ B에 연결 하 고 다음 설정 WINS\ b 푸시/방향으로 빼냅니다 복제 파트너 WINS\ A
- WINS\ b WINS\ a에서 푸시 복제 시작
- 새 녹음 MY\_RECORD를 성공적으로 복제 확인 하기 위해 WINS\-B에 연결

## <a name="netsh-example-batch-file"></a>Netsh 예 배치 파일

다음 예 배치 파일에서 주석이 포함 된 줄 의견에 대 한 "rem" 앞 됩니다. Netsh 의견 무시합니다.

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

## <a name="netsh-wins-commands-used-in-the-example-batch-file"></a>Netsh WINS 명령 예 배치 파일에 사용

다음 목록 섹션의 **netsh wins** 이 예제 절차에 사용 되는 명령을 합니다.

- **서버**합니다. 서버 이름 또는 IP 주소를 지정 현재 WINS 줄 command\ 컨텍스트가 이동 합니다.
- **이름 추가**합니다. 이름을 WINS 서버에 등록합니다.
- **파트너 추가**합니다. 복제 파트너 WINS 서버에 추가 합니다.
- **초기화 푸시**합니다. 시작 및 푸시 트리거 WINS 서버에 전송 합니다.
- **표시 이름**합니다. WINS 서버 데이터베이스에는 특정 기록에 대 한 자세한 정보를 표시 합니다.  

자세한 내용은 참조 [네트워크 (Netsh) 셸](netsh.md)합니다.
