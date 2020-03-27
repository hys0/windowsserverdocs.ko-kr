---
title: 네트워크 관련 성능 카운터
description: 이 항목은 Windows Server 2016에 대 한 네트워크 하위 시스템 성능 조정 가이드의 일부입니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 7ebaa271-2557-4c24-a679-c3d863e6bf9e
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: e62b92fbb78dc267dbd9cd09927bf54c62d8245f
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316608"
---
# <a name="network-related-performance-counters"></a>네트워크 관련 성능 카운터

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 네트워크 성능 관리와 관련 된 카운터를 나열 하 고 다음 섹션을 포함 합니다.  
  
-   [리소스 사용률](#bkmk_ru)  
  
-   [잠재적인 네트워크 문제](#bkmk_np)  
  
-   [RSC (수신측 통합) 성능](#bkmk_rsc)  
  
##  <a name="resource-utilization"></a><a name="bkmk_ru"></a>리소스 사용률  

다음 성능 카운터는 네트워크 리소스 사용량과 관련이 있습니다.  
  
- IPv4, IPv6  
  
  -   받은 데이터 그램/초  
  
  -   초당 전송 되는 데이터 그램  
  
- TCPv4, TCPv6  
  
  -   받은 세그먼트/초  
  
  -   전송 되는 세그먼트/초  
  
  -   재전송 한 세그먼트/초  
  
- 네트워크 인터페이스 (*), 네트워크 어댑터 (\*)  
  
  - Bytes Received/sec  
  
  - 보낸 바이트/초  
  
  - 받은 패킷/초  
  
  - 보낸 패킷/초  
  
  - 출력 큐 길이  
  
    이 카운터는 패킷\)\(출력 패킷 큐의 길이입니다. 2 보다 길면 지연이 발생 합니다. 가능 하면 병목 상태를 확인 하 고 제거 해야 합니다. NDIS에서 요청을 큐에 대기 하므로이 길이는 항상 0 이어야 합니다.  
  
- 프로세서 정보  
  
  - % Processor Time  
  
  - 인터럽트/초  
  
  - 큐에 대기 된 Dpc/초  
  
    이 카운터는 Dpc가 논리 프로세서의 DPC 큐에 추가 되는 평균 비율입니다. 각 논리 프로세서에는 자체 DPC 큐가 있습니다. 이 카운터는 큐의 Dpc 수가 아니라 Dpc가 큐에 추가 되는 속도를 측정 합니다. 마지막 두 샘플에서 관찰 된 값의 차이를 샘플 간격 기간으로 나눈 값을 표시 합니다.  
  
##  <a name="potential-network-problems"></a><a name="bkmk_np"></a>잠재적인 네트워크 문제  

다음 성능 카운터는 잠재적인 네트워크 문제와 관련 됩니다.  
  
-   네트워크 인터페이스 (*), 네트워크 어댑터 (\*)  
  
    -   받은 패킷 삭제 됨  
  
    -   수신 되는 패킷 오류  
  
    -   아웃 바운드 패킷 삭제 됨  
  
    -   패킷 아웃 바운드 오류  
  
-   WFPv4, WFPv6  
  
    -   삭제 된 패킷/초

-   UDPv4, UDPv6

    -   데이터 그램 수신 오류  
  
-   TCPv4, TCPv6  
  
    -   연결 실패  
  
    -   연결 다시 설정  
  
-   네트워크 QoS 정책  
  
    -   삭제 된 패킷  
  
    -   초당 삭제 된 패킷  
  
-   프로세서당 네트워크 인터페이스 카드 활동  
  
    -   낮은 리소스 수신 표시/초  
  
    -   낮은 리소스 수신 패킷/초  
  
-   Microsoft Winsock BSP  
  
    -   삭제 된 데이터 그램  
  
    -   삭제 된 데이터 그램/초  
  
    -   Rejected Connections  
  
    -   거부 된 연결/초  
  
##  <a name="receive-side-coalescing-rsc-performance"></a><a name="bkmk_rsc"></a>RSC (수신측 통합) 성능  

다음 성능 카운터는 RSC 성능과 관련 됩니다.  
  
-   네트워크 어댑터 (*)  
  
    -   TCP 활성 RSC 연결  
  
    -   TCP RSC 평균 패킷 크기  
  
    -   TCP RSC 병합 패킷/초  
  
    -   TCP RSC 예외/초

이 가이드의 모든 항목에 대 한 링크는 [네트워크 하위 시스템 성능 튜닝](net-sub-performance-top.md)을 참조 하세요.