---
title: Windows Server 2019의 HPN 기능에 대 한 Insider Preview
description: Windows Server 2019의 새로운 고성능 네트워킹 기능에 대해 알아봅니다.
manager: dougkim
author: eross-msft
ms.author: lizross
ms.date: 09/12/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: f6403cd9787ccdd4f50eb08ebd7723d2de789ebb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819646"
---
# <a name="new-hpn-features-in-windows-server-2019"></a>Windows Server 2019의 새로운 HPN 기능


## <a name="dynamic-vrss-and-vmmq"></a>동적 vRSS 및 VMMQ

>적용 대상: Windows Server 2019

이전에는 네트워크 처리량이 먼저 10GbE 표시 이상에 도달 하 여 가상 머신 큐와 가상 머신 다중 큐에서 개별 Vm에 대 한 처리량을 훨씬 더 높게 설정 했습니다. 아쉽게도 성공에 필요한 계획, 기준 조정, 조정 및 모니터링이 많은 작업이 되었습니다. 일반적으로 IT 관리자가 지출 하려고 합니다. 

Windows Server 2019에서는 필요에 따라 네트워크 작업의 처리를 동적으로 분산 하 고 조정 하 여 이러한 최적화를 개선 합니다. Windows Server 2019는 최고 효율성을 보장 하 고 IT 관리자의 구성 부담을 제거 합니다.

참조 항목:

-   [발표 블로그](https://blogs.technet.microsoft.com/networking/2018/08/22/netperf4vw/)

-   [IT 전문가를 위한 유효성 검사 가이드](https://aka.ms/DVMMQ-Validation)

## <a name="receive-segment-coalescing-rsc-in-the-vswitch"></a>vSwitch RSC(수신 세그먼트 통합)

>적용 대상: Windows Server 2019 및 Windows 10, 버전 1809

VSwitch의 RSC (수신 세그먼트 통합)는 vSwitch를 통과 하는 데이터 보다 큰 세그먼트로 여러 TCP 세그먼트를 결합 하는 향상 된 기능입니다. 대량 세그먼트는 가상 워크 로드에 대 한 네트워킹 성능을 향상 시킵니다.

이전에는 NIC에서 구현 된 오프 로드 였습니다. 안타깝게도 어댑터를 가상 스위치에 연결 하는 순간에는이 기능을 사용할 수 없습니다. Windows Server 2019 및 Windows 10 10 2018 월 업데이트의 vSwitch에서 RSC는 이러한 제한을 제거 합니다.

기본적으로 vSwitch의 RSC는 외부 가상 스위치에서 사용 하도록 설정 됩니다.

참조 항목:

-  [발표 블로그](https://blogs.technet.microsoft.com/networking/2018/08/22/netperf4vw/)

-  [IT 전문가를 위한 유효성 검사 가이드](https://aka.ms/RSC-Validation)
