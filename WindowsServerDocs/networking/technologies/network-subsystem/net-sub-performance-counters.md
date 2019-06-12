---
title: 네트워크 관련 성능 카운터
description: 이 항목은 Windows Server 2016에 대 한 네트워크 하위 시스템 성능 튜닝 지침의 일부입니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 7ebaa271-2557-4c24-a679-c3d863e6bf9e
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bcb0c1c5a08a306fbd9b419d0c458c3bc54e1786
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446200"
---
# <a name="network-related-performance-counters"></a>네트워크 관련 성능 카운터

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 네트워크 성능 관리와 관련 된 다음 섹션이 포함 하는 카운터를 나열 합니다.  
  
-   [리소스 사용률](#bkmk_ru)  
  
-   [잠재적인 네트워크 문제](#bkmk_np)  
  
-   [RSC (수신측) 성능 수신](#bkmk_rsc)  
  
##  <a name="bkmk_ru"></a> 리소스 사용률  

다음 성능 카운터는 네트워크 리소스 사용률에 적용 됩니다.  
  
- IPv4, IPv6  
  
  -   Datagrams Received/sec  
  
  -   Datagrams Sent/sec  
  
- TCPv4, TCPv6  
  
  -   세그먼트 Received/sec  
  
  -   Segments Sent/sec  
  
  -   재전송 세그먼트/sec  
  
- Network Interface(*), Network Adapter(\*)  
  
  - Bytes Received/sec  
  
  - Bytes Sent/sec  
  
  - 수신 된 패킷/초  
  
  - Packets Sent/sec  
  
  - 출력 큐 길이  
  
    이 카운터는 출력 패킷 큐의 길이 \(패킷의\)합니다. 2 자리 보다 긴 경우 지연이 발생 합니다. 병목 지점을 찾아야 하 고 가능한 경우 제거 해야 합니다. NDIS 큐 요청 때문에이 길이 항상 0 이어야 합니다.  
  
- 프로세서 정보  
  
  - % 프로세서 시간  
  
  - Interrupts/sec  
  
  - Dpc 큐에 대기 수/초  
  
    이 카운터는 Dpc 논리 프로세서의 DPC 큐에 추가 된 위치의 평균 비율입니다. 각 논리적 프로세서에는 고유한 DPC 큐를 있습니다. 이 카운터는 큐의 Dpc 수가 아니라 큐에 Dpc가 추가 되는 속도 측정 합니다. 샘플 간격 기간으로 나눈 마지막 두 샘플에서 관찰 된 값 간의 차이 표시 합니다.  
  
##  <a name="bkmk_np"></a> 잠재적인 네트워크 문제  

다음 성능 카운터를 잠재적인 네트워크 문제와 관련이 있습니다.  
  
-   Network Interface(*), Network Adapter(\*)  
  
    -   패킷이 삭제 된 수신  
  
    -   패킷이 수신 오류  
  
    -   삭제 된 아웃 바운드 패킷  
  
    -   아웃 바운드 패킷 오류  
  
-   WFPv4, WFPv6  
  
    -   패킷 삭제 수/초

-   UDPv4, UDPv6

    -   Datagrams Received 오류  
  
-   TCPv4, TCPv6  
  
    -   연결 실패  
  
    -   연결 다시 설정  
  
-   네트워크 QoS 정책  
  
    -   삭제 된 패킷  
  
    -   패킷 삭제 수/초  
  
-   Processor Network Interface Card Activity 당  
  
    -   리소스가 부족 징후 초당 수신  
  
    -   리소스가 부족 받은 패킷/초  
  
-   Microsoft Winsock BSP  
  
    -   데이터 그램 삭제  
  
    -   Dropped Datagrams/sec  
  
    -   Rejected Connections  
  
    -   거부 된 연결/sec  
  
##  <a name="bkmk_rsc"></a> RSC (수신측) 성능 수신  

다음 성능 카운터 RSC 성능에 적용 됩니다.  
  
-   Network Adapter(*)  
  
    -   TCP 활성화 RSC 연결  
  
    -   TCP RSC 평균 패킷 크기  
  
    -   TCP RSC 병합 Packets/sec  
  
    -   TCP RSC Exceptions/sec

이 가이드의 모든 항목에 대 한 링크를 참조 하세요 [네트워크 하위 시스템 성능 튜닝](net-sub-performance-top.md)합니다.