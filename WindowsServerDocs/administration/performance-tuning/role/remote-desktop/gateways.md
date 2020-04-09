---
title: 원격 데스크톱 게이트웨이 성능 조정
description: 원격 데스크톱 게이트웨이에 대 한 성능 조정 권장 사항
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: hammadbu; vladmis
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 3794b47e7226a905944495dd7c31f3196a33d0d5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851736"
---
# <a name="performance-tuning-remote-desktop-gateways"></a>원격 데스크톱 게이트웨이 성능 조정

> [!NOTE]
> Windows 8 + 및 Windows Server 2012 R2 이상에서 원격 데스크톱 게이트웨이 (RD 게이트웨이)은 TCP, UDP 및 레거시 RPC 전송을 지원 합니다. 다음 데이터는 대부분 레거시 RPC 전송과 관련 됩니다. 레거시 RPC 전송이 사용 되지 않는 경우에는이 섹션을 적용할 수 없습니다.

이 항목에서는 고객 배포의 성능과 고객의 네트워크 사용 패턴을 사용 하는 tunings을 개선 하는 데 도움이 되는 성능 관련 매개 변수를 설명 합니다.

코어 RD 게이트웨이는 원격 데스크톱 연결 인스턴스와 고객 네트워크 내의 RD 세션 호스트 서버 인스턴스 간에 많은 패킷 전달 작업을 수행 합니다.

> [!NOTE]
> 다음 매개 변수는 RPC 전송에만 적용 됩니다.

인터넷 정보 서비스 (IIS) 및를 RD 게이트웨이 하 여 RD 게이트웨이에서 시스템 성능을 향상 시킬 수 있도록 다음 레지스트리 매개 변수를 내보냅니다.

**스레드 tunings**

-   **Maxiothreads**

    ``` syntax
    HKLM\Software\Microsoft\Terminal Server Gateway\Maxiothreads (REG_DWORD)
    ```

    이 앱 특정 스레드 풀은 RD 게이트웨이 들어오는 요청을 처리 하기 위해 만들 수 있는 스레드 수를 지정 합니다. 이 레지스트리 설정이 있으면 적용 됩니다. 스레드 수는 논리적 프로세스 수와 같습니다. 논리 프로세서 수가 5 보다 작은 경우 기본값은 5 개의 스레드입니다.

-   **MaxPoolThreads**

    ``` syntax
    HKLM\System\CurrentControlSet\Services\InetInfo\Parameters\MaxPoolThreads (REG_DWORD)
    ```

    이 매개 변수는 논리적 프로세서당 만들 IIS 풀 스레드 수를 지정 합니다. IIS 풀 스레드는 네트워크에서 요청을 감시 하 고 들어오는 모든 요청을 처리 합니다. **Maxpoolthreads** 수에는 RD 게이트웨이 사용 하는 스레드가 포함 되지 않습니다. 기본값은 4입니다.

**RD 게이트웨이에 대 한 원격 프로시저 호출 tunings**

다음 매개 변수는 원격 데스크톱 연결 및 RD 게이트웨이 컴퓨터에서 수신 하는 RPC (원격 프로시저 호출)를 조정 하는 데 도움이 될 수 있습니다. Windows를 변경 하면 각 연결을 통해 전송 되는 데이터의 양을 제한 하 고 RPC over HTTP v2 시나리오에 대 한 성능을 향상 시킬 수 있습니다.

-   **ServerReceiveWindow**

    ``` syntax
    HKLM\Software\Microsoft\Rpc\ServerReceiveWindow (REG_DWORD)
    ```

    기본값은 64입니다. 이 값은 서버가 RPC 프록시에서 수신 하는 데이터에 대해 사용 하는 창을 지정 합니다. 최 솟 값은 8kb로 설정 되 고 최대값은 1gb로 설정 됩니다. 값이 없는 경우 기본값이 사용 됩니다. 이 값이 변경 되 면 IIS를 다시 시작 해야 변경 내용이 적용 됩니다.

-   **ServerReceiveWindow**

    ``` syntax
    HKLM\Software\Microsoft\Rpc\ServerReceiveWindow (REG_DWORD)
    ```

    기본값은 64입니다. 이 값은 클라이언트가 RPC 프록시에서 받은 데이터에 사용 하는 창을 지정 합니다. 최 솟 값은 8kb 이며 최대값은 1gb입니다. 값이 없는 경우 기본값이 사용 됩니다.

## <a name="monitoring-and-data-collection"></a>모니터링 및 데이터 수집

다음 성능 카운터 목록은 RD 게이트웨이에서 리소스 사용량을 모니터링할 때 기본 카운터 집합으로 간주 됩니다.

-   터미널 서비스 게이트웨이\\\\\*

-   \\RPC/HTTP 프록시\\\*

-   서버당 RPC/HTTP 프록시를 \\\\\*

-   웹 서비스\\\\\*

-   W3SVC\_w3wp.exe\\\\\*

-   \\IPv4\\\*

-   메모리\\\\\*

-   \*(\\Network Interface)\\\*

-   \\프로세스 (\*)\\\*

-   \\Processor Information (\*)\\\*

-   \\동기화 (\*)\\\*

-   \\System\\\*

-   \\TCPv4\\\*

다음 성능 카운터는 레거시 RPC 전송에만 적용 됩니다.

-   rpc \\RPC/HTTP 프록시\\\* RPC

-   서버당 RPC/HTTP 프록시를 \\\\\* RPC

-   \\웹 서비스\\\* RPC

-   \\W3SVC\_w3wp.exe\\\* RPC

> [!NOTE]
> 해당 하는 경우 \\IPv6\\\* 및 \\TCPv6\\개체를 추가 합니다. ReplaceThisText\*

