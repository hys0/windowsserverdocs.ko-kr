---
title: 네트워크 작업에 대 한 성능 도구
description: 이 항목은 Windows Server 2016 용 네트워크 하위 시스템 성능 조정 가이드의 일부입니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: c7789781-87e8-464e-981b-af887d01badd
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 81c31871b3dfa4644690fe074ae15eaaa680d7f2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="performance-tools-for-network-workloads"></a>네트워크 작업에 대 한 성능 도구

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

성능 도구에 대 한 자세한 내용은이 항목을 사용할 수 있습니다.

이 항목 클라이언트 서버 교통 도구, TCP/IP 창 크기 및 Microsoft 서버 성능 관리자에 대 한 부분을 포함합니다.

##  <a name="bkmk_tuning"></a>서버 교통 도구에 대 한 클라이언트

클라이언트 서버 교통 \(ctsTraffic\) 도구를 만들고 네트워크 교통량을 확인 하는 기능을 제공 합니다.

표시 되는 자세한 정보 및 도구를 다운로드 하려면 [ctsTraffic (클라이언트 서버 교통)](http://ctstraffic.codeplex.com/)합니다.
  
##  <a name="bkmk_size"></a>TCP/IP 창 크기

1 g B 어댑터를 이전 표에 있는 설정을 제공 해야 좋은 처리량 NTttcp 특정 논리 프로세서를 통해 기본 TCP 창 크기를 64 K 설정 때문에 옵션 \(SO_RCVBUF\) 연결 합니다. 낮은 대기 네트워크 뛰어난 성능을 제공합니다.  

반면,와 대기 네트워크 또는 10GB 어댑터에 대 한는 TCP 창 크기에 대 한 기본값 NTttcp 최적의 성능을 보다 작음 생성합니다. 두 경우 모두 큰 대역폭 지연 제품에 대 한 수 있도록 TCP 창 크기를 조정 해야 합니다.  

정적 TCP 하는 창 크기가 큰 금액을 사용 하 여 설정할 수 있습니다는 **-rb** 옵션이 있습니다. 이 옵션 비활성화 TCP 창 자동 조정 하 고 사용자의 TCP/IP 동작 결과 변경 완벽 하 게 것을 이해 하는 경우에 사용 하는 것이 좋습니다. 기본적으로 TCP 하는 창 크기가 충분 한 값으로 설정 하 고만 부하가 또는 대기 링크를 통해 조정 합니다.  

##  <a name="bkmk_advisor"></a>Microsoft 서버 성능 관리자

Microsoft 서버 성능 관리자 \(SPA\) IT 관리자 수집 메트릭 식별 비교 하 고 Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008 배포에서 성능 문제를 진단 하는 데 도움이 됩니다. 

진단 보고서가 포괄적인 및 차트, SPA 생성 하 고 신속 하 게 하는 데 도움이 되도록 권장 문제를 분석 하 고 조치를 개발을 제공 합니다.  
  
 표시 되는 자세한 정보 및 도우미를 다운로드 하려면 [Microsoft 서버 성능 관리자](https://msdn.microsoft.com/library/windows/hardware/dn481522.aspx) 하드웨어 Windows 개발자 센터에서 합니다.

이 가이드의 모든 항목에 대 한 링크를 참조 하세요. [네트워크 하위 시스템 성능 조정](net-sub-performance-top.md)합니다.