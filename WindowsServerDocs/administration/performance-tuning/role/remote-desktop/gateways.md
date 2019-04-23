---
title: 원격 데스크톱 게이트웨이 튜닝 하는 성능
description: 성능 튜닝 권장 사항에 대 한 원격 데스크톱 게이트웨이
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: HammadBu; VladmiS
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 7619d2e2ce394c7f06826d6ebe36bccfa43344ad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842574"
---
# <a name="performance-tuning-remote-desktop-gateways"></a>원격 데스크톱 게이트웨이 튜닝 하는 성능

**참고**    Windows 8 이상 및 Windows Server 2012 R2 이상에서 원격 데스크톱 게이트웨이 (RD 게이트웨이) TCP, UDP 및 레거시 RPC 전송을 지원 합니다. 다음의 데이터 대부분은 레거시 RPC 전송을 관련입니다. 레거시 RPC 전송 사용 하지 않는 경우이 섹션에서는 적용 되지 않습니다.

이 항목에서는 고객 배포의 성능을 향상 하는 데 도움이 되는 성능 관련 매개 변수 및 고객의 네트워크 사용 패턴을 사용 하는 tunings를 설명 합니다.

RD 게이트웨이 본질적으로 원격 데스크톱 연결 인스턴스 및 고객의 네트워크 내에서 RD 세션 호스트 서버 인스턴스 간에 작업을 전달 하는 많은 패킷을 수행 합니다.

**참고**    RPC 전송만에 다음 매개 변수를 적용 합니다.

인터넷 정보 서비스 (IIS) 및 RD 게이트웨이 RD 게이트웨이에서 시스템 성능 향상을 위해 다음 레지스트리 매개 변수를 내보냅니다.

**Tunings 스레드**

-   **Maxiothreads**

    ``` syntax
    HKLM\Software\Microsoft\Terminal Server Gateway\Maxiothreads (REG_DWORD)
    ```

    이 앱 특정 스레드 풀 RD 게이트웨이 만듭니다 들어오는 요청을 처리 하는 스레드의 수를 지정 합니다. 이 레지스트리 설정이 있는 경우에 적용이 됩니다. 스레드 수가 논리 프로세스의 수를 같습니다. 논리 프로세서 수가 5 보다 작을 경우 기본값은 5 개 스레드입니다.

-   **MaxPoolThreads**

    ``` syntax
    HKLM\System\CurrentControlSet\Services\InetInfo\Parameters\MaxPoolThreads (REG_DWORD)
    ```

    이 매개 변수는 논리적 프로세서당 만들려면 IIS 풀 스레드 수를 지정 합니다. IIS 풀 스레드 요청에 대 한 네트워크를 시청 하 고 들어오는 모든 요청을 처리 합니다. 합니다 **MaxPoolThreads** RD 게이트웨이 사용 하는 스레드는 포함 되지 않습니다. 기본값은 4입니다.

**RD 게이트웨이에 대 한 원격 프로시저 호출 tunings**

다음 매개 변수는 원격 데스크톱 연결 및 RD 게이트웨이 컴퓨터에서 수신 되는 원격 프로시저 호출 (RPC)을 조정할 수 있습니다. Windows 변경 데이터의 양을 각 연결을 통해 전달 되 고 RPC over HTTP v2 시나리오 성능을 향상 시킬 수를 제한 하는 데 도움이 됩니다.

-   **ServerReceiveWindow**

    ``` syntax
    HKLM\Software\Microsoft\Rpc\ServerReceiveWindow (REG_DWORD)
    ```

    기본값은 64KB입니다. 이 값 RPC 프록시에서 수신 되는 데이터에 대 한 서버를 사용 하는 기간을 지정 합니다. 8kb, 최 솟 값 집합과 최 댓 값 1로 설정 되어 있습니다. 값이 없는 경우 기본값이 사용 됩니다. 이 값이 변경 되 면 변경 내용을 적용 하려면 IIS는 다시 시작 해야 합니다.

-   **ServerReceiveWindow**

    ``` syntax
    HKLM\Software\Microsoft\Rpc\ServerReceiveWindow (REG_DWORD)
    ```

    기본값은 64KB입니다. 이 값에는 RPC 프록시에서 수신 되는 데이터에 대 한 클라이언트를 사용 하는 창을 지정 합니다. 최소값은 8KB 및 최 댓 값은 1GB입니다. 값이 없는 경우 기본값이 사용 됩니다.

## <a name="monitoring-and-data-collection"></a>모니터링 및 데이터 수집


다음과 같은 성능 카운터는 RD 게이트웨이에서 리소스 사용량을 모니터링 하는 경우 기본 카운터 집합으로 간주 됩니다.

-   \\터미널 서비스 게이트웨이\\\*

-   \\RPC/HTTP 프록시\\\*

-   \\서버당 RPC/HTTP 프록시\\\*

-   \\웹 서비스\\\*

-   \\W3SVC\_W3WP\\\*

-   \\IPv4\\\*

-   \\메모리\\\*

-   \\Network Interface(\*)\\\*

-   \\Process(\*)\\\*

-   \\Processor Information(\*)\\\*

-   \\Synchronization(\*)\\\*

-   \\시스템\\\*

-   \\TCPv4\\\*

다음 성능 카운터 레거시 RPC 전송에 대해서만 적용 됩니다.

-   \\RPC/HTTP 프록시\\ \* RPC

-   \\RPC/HTTP 프록시 서버당\\ \* RPC

-   \\웹 서비스\\ \* RPC

-   \\W3SVC\_W3WP\\\* RPC

**참고**    해당 하는 경우 추가 합니다 \\IPv6\\ \* 하 고 \\TCPv6\\ \* 개체입니다. ReplaceThisText

 
