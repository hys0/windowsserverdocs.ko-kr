---
title: 네트워크 작업에 대한 성능 도구
description: 이 항목은 Windows Server 2016에 대 한 네트워크 하위 시스템 성능 조정 가이드의 일부입니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: c7789781-87e8-464e-981b-af887d01badd
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 07/16/2018
ms.openlocfilehash: 09e775bfe956d67adbd70cf4ce3f9461e1c37cf5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405513"
---
# <a name="performance-tools-for-network-workloads"></a>네트워크 작업에 대한 성능 도구

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 성능 도구에 대해 알아볼 수 있습니다.

이 항목에는 클라이언트-서버 트래픽 도구, TCP/IP 창 크기 및 Microsoft Server Performance Advisor에 대 한 섹션이 포함 되어 있습니다.

##  <a name="bkmk_tuning"></a>클라이언트-서버 트래픽 도구

클라이언트와 서버 간 트래픽 \(ctsTraffic\) 도구는 네트워크 트래픽을 만들고 확인 하는 기능을 제공 합니다.

자세한 내용 및 도구를 다운로드 하려면 [ctsTraffic (클라이언트-서버 트래픽)](https://github.com/Microsoft/ctsTraffic)를 참조 하세요.
  
##  <a name="bkmk_size"></a>TCP/IP 창 크기

어댑터 어댑터의 경우에는 NTttcp가 연결에 대 한 SO_RCVBUF\) \(특정 논리 프로세서 옵션을 통해 기본 TCP 창 크기를 64 K로 설정 하기 때문에 이전 표에 나와 있는 설정이 적절 한 처리량을 제공 해야 합니다. 이는 대기 시간이 짧은 네트워크에서 좋은 성능을 제공 합니다.  

이와 대조적으로 대기 시간이 긴 네트워크 또는 10gb 어댑터의 경우에는 NTttcp의 기본 TCP 창 크기 값이 최적의 성능 보다 낮습니다. 두 경우 모두, 더 큰 대역폭 지연 제품을 허용 하도록 TCP 창 크기를 조정 해야 합니다.  

**-Rb** 옵션을 사용 하 여 TCP 창 크기를 큰 값으로 정적으로 설정할 수 있습니다. 이 옵션은 TCP 창 자동 조정을 사용 하지 않도록 설정 하며, 사용자가 TCP/IP 동작의 결과 변경을 완전히 이해 하는 경우에만 사용 하는 것이 좋습니다. 기본적으로 TCP 창 크기는 충분 한 값으로 설정 되며 과도 한 부하가 나 대기 시간이 긴 링크 에서만 조정 됩니다.  

##  <a name="bkmk_advisor"></a>Microsoft Server Performance Advisor

Microsoft Server Performance Advisor \(SPA\)를 사용 하면 IT 관리자가 Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008 배포에서 잠재적 성능 문제를 식별, 비교 및 진단 하는 메트릭을 수집할 수 있습니다. 

SPA는 포괄적인 진단 보고서 및 차트를 생성 하 고, 문제를 신속 하 게 분석 하 고 정정 작업을 개발 하는 데 유용한 권장 사항을 제공 합니다.  
  
 자세한 내용 및 advisor를 다운로드 하려면 Windows 하드웨어 개발자 센터에서 [Microsoft Server Performance advisor](https://msdn.microsoft.com/library/windows/hardware/dn481522.aspx) 를 참조 하세요.

이 가이드의 모든 항목에 대 한 링크는 [네트워크 하위 시스템 성능 튜닝](net-sub-performance-top.md)을 참조 하세요.