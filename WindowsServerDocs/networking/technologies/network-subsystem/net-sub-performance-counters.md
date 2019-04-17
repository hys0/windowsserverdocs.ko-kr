---
title: 네트워크 관련 된 성능 카운터
description: 이 항목은 Windows Server 2016 용 네트워크 하위 시스템 성능 조정 가이드의 일부입니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 7ebaa271-2557-4c24-a679-c3d863e6bf9e
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 33551dfd4f76bc13ba69863b782ddae279e0ad16
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="network-related-performance-counters"></a>네트워크 관련 된 성능 카운터

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목에서는 카운터 네트워크 성능을 관리 관련 된는 다음 섹션에 포함 되어 있습니다.  
  
-   [리소스 사용](#bkmk_ru)  
  
-   [네트워크 문제](#bkmk_np)  
  
-   [측면 결합 (RSC) 성능 받기](#bkmk_rsc)  
  
##  <a name="bkmk_ru"></a>리소스 사용  

다음과 같은 성능 카운터 네트워크 리소스 사용량 관련이 있습니다.  
  
-   I p v 4을 IPv6  
  
    -   받은 데이터 그램/초  
  
    -   보낸 데이터 그램/초  
  
-   TCPv6 TCPv4  
  
    -   받은 초 나누어  
  
    -   보낸 초 나누어  
  
    -   다시 전송 초 나누어  
  
-   네트워크 Interface(*), Adapter(\*) 네트워크  
  
    -   받은 바이트 월 초  
  
    -   보낸 바이트 월 초  
  
    -   초당 받은 패킷  
  
    -   초당 전송 패킷  
  
    -   출력 대기  
  
     이 카운터 길이 출력 패킷 큐 \(in packets\)입니다. 2 보다 더 길게 만들면를 지연 발생 합니다. 장애가 찾아 가능 하면 제거할 해야 합니다. NDIS 큐에 요청을 하기 때문에이 길이 항상 0 해야 합니다.  
  
-   프로세서 정보  
  
    -   프로세서 시간  
  
    -   인터럽트 월 초  
  
    -   초당 대기 Dpc  
  
     이 카운터 Dpc 논리 프로세서 DPC 대기열에 추가 된 평균 속도입니다. 각 논리 프로세서 자체 DPC 큐를 있습니다. Dpc 큐에 Dpc 수가 하지 대기열에 추가 하는 빈도 측정 하 여이 카운터 합니다. 샘플 기간 기간 나눈 마지막 두 샘플에서 발견 된 값 간의 차이점을 표시 합니다.  
  
##  <a name="bkmk_np"></a>네트워크 문제  

다음과 같은 성능 카운터 잠재적인 네트워크 문제 관련이 있습니다.  
  
-   네트워크 Interface(*), Adapter(\*) 네트워크  
  
    -   패킷 받은 삭제  
  
    -   패킷 받은 오류  
  
    -   패킷을 아웃 바운드 삭제  
  
    -   패킷 아웃 바운드 오류  
  
-   WFPv6 WFPv4  
  
    -   초당 무시 패킷

-   UDPv6 UDPv4

    -   데이터 그램 받은 오류  
  
-   TCPv6 TCPv4  
  
    -   연결이 실패  
  
    -   연결 초기화  
  
-   네트워크 QoS 정책  
  
    -   핀 패킷  
  
    -   초당 핀 패킷  
  
-   프로세서 네트워크 인터페이스 카드 활동 마다  
  
    -   낮은 리소스 표시/초 받기  
  
    -   낮은 리소스 초당 패킷 받은  
  
-   Microsoft Winsock BSP  
  
    -   데이터 삭제 그램  
  
    -   장식된 데이터 그램 초당  
  
    -   거부 연결  
  
    -   거부 연결 초당  
  
##  <a name="bkmk_rsc"></a>측면 결합 (RSC) 성능 받기  

다음과 같은 성능 카운터 RSC 성능 관련이 있습니다.  
  
-   네트워크 Adapter(*)  
  
    -   현재 RSC TCP 연결  
  
    -   TCP RSC 평균 패킷 크기  
  
    -   초당 패킷 결합 됩니다 TCP RSC  
  
    -   초당 TCP RSC 예외

이 가이드의 모든 항목에 대 한 링크를 참조 하세요. [네트워크 하위 시스템 성능 조정](net-sub-performance-top.md)합니다.