---
title: 네트워크 작업에 대한 성능 도구
description: 이 항목은 Windows Server 2016에 대 한 네트워크 하위 시스템 성능 튜닝 지침의 일부입니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: c7789781-87e8-464e-981b-af887d01badd
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 07/16/2018
ms.openlocfilehash: e71c5f34041145907c30b279dc91a94c03c2abed
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824934"
---
# <a name="performance-tools-for-network-workloads"></a>네트워크 작업에 대한 성능 도구

>적용 대상: Windows Server (반기 채널), Windows Server 2016

성능 도구에 대해 자세히 알아보려면이 항목에서는 사용할 수 있습니다.

이 항목에서는 서버 트래픽을 도구, TCP/IP 창 크기 및 Microsoft Server Performance Advisor를 클라이언트에 대 한 섹션을 포함합니다.

##  <a name="bkmk_tuning"></a> 서버 트래픽을 도구에 대 한 클라이언트

클라이언트를 서버 트래픽을 \(ctsTraffic\) 도구 만들기 및 네트워크 트래픽을 확인 하는 기능을 사용 하면 메시지를 표시 합니다.

자세한 내용은 및 도구를 다운로드 하려면 [ctsTraffic (클라이언트와 서버 간 트래픽)](https://github.com/Microsoft/ctsTraffic)합니다.
  
##  <a name="bkmk_size"></a> TCP/IP 창 크기

1GB 어댑터의 경우 위의 표에 표시 된 설정을 NTttcp 특정 논리 프로세서 옵션을 통해 기본 TCP 창 크기를 64k로 설정 하기 때문에 적절 한 처리량을 제공 해야 \(SO_RCVBUF\) 연결 합니다. 지연율이 낮은 네트워크에 좋은 성능을 제공합니다.  

반면, 대기 시간이 긴 네트워크 또는 10GB 어댑터에 대 한 기본 TCP 창 크기 값 NTttcp에 대 한 최상의 성능 보다 낮습니다 생성합니다. 두 경우 모두에서 더 큰 대역폭 지연 제품에 대 한 허용 하도록 TCP 창 크기를 조정 해야 합니다.  

사용 하 여 TCP 창 크기를 큰 값으로 정적으로 설정할 수 있습니다 합니다 **-rb** 옵션입니다. TCP 창 자동 조정 하는이 옵션이 사용 하지 않도록 설정 하 고 TCP/IP 동작의 결과 변화를 완벽 하 게 이해 하는 경우에 사용 하는 것이 좋습니다. 기본적으로 TCP 창 크기를 충분 한 값으로 설정 되 고 부하가 또는 대기 시간이 긴 연결을 통해 조정.  

##  <a name="bkmk_advisor"></a> Microsoft Server Performance Advisor

Microsoft Server Performance Advisor \(SPA\) 비교 하 고 Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows에서 잠재적인 성능 문제를 진단 하는 IT 관리자를 식별 하는 메트릭을 수집 하는 데 도움이 됩니다. Server 2008 R2 또는 Windows Server 2008 배포 합니다. 

SPA는 종합 진단 보고서와 차트를 생성 하 고 제공 하기 위한 권장 사항을 신속 하 게 문제를 분석 하 고 수정 작업을 개발 합니다.  
  
 자세한 내용은 다운로드 관리자를 참조 하십시오 [Microsoft Server Performance Advisor](https://msdn.microsoft.com/library/windows/hardware/dn481522.aspx) Windows 하드웨어 개발자 센터에서.

이 가이드의 모든 항목에 대 한 링크를 참조 하세요 [네트워크 하위 시스템 성능 튜닝](net-sub-performance-top.md)합니다.