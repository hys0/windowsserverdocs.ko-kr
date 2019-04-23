---
ms.assetid: ''
title: Windows Server 2019에 HPN 기능에 대 한 참가자 미리 보기
description: Windows Server 2019의 새로운 고속 네트워킹 기능에 알아봅니다.
manager: dougkim
author: shortpatti
ms.author: pashort
ms.date: 09/12/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 3d3e974472f28c30d093fbd1094ef3693d984d19
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886274"
---
# <a name="insider-preview"></a>Insider Preview


## <a name="dynamic-vrss-and-vmmq"></a>동적 vRSS 및 VMMQ

>적용 대상: Windows Server 2019

과거에는 가상 머신 큐 및 가상 머신 다중 큐 활성화 개별 Vm에 훨씬 높은 처리량 먼저 10GbE 표시에 도달 하는 네트워크 처리량으로 이상. 아쉽게도 계획, 기준 지정, 조정 및 모니터링에 필요한 성공 상태가 매우 힘든 작업이; 종종 소비 하기 위한 보다 IT 관리자입니다. 

Windows Server 2019 동적으로 분산 하 고 필요에 따라 네트워크 워크 로드를 처리 하는 튜닝 하 여 이러한 최적화를 개선 합니다. Windows Server 2019 최대 효율성을 확인 하 고 IT 관리자에 대 한 구성 해야 하는 부담을 제거 합니다.

참조 항목:

-   [공지 블로그](https://blogs.technet.microsoft.com/networking/2018/08/22/netperf4vw/)

-   [유효성 검사 가이드는 IT 전문가](https://aka.ms/DVMMQ-Validation)

## <a name="receive-segment-coalescing-rsc-in-the-vswitch"></a>vSwitch RSC(수신 세그먼트 통합)

>적용 대상: Windows Server 2019 및 Windows 10 버전 1809

수신 세그먼트 (RSC) vSwitch에서 여러 TCP 세그먼트 데이터 vSwitch를 통과 하기 전에 더 큰 세그먼트를 결합 하는 향상 된 기능입니다. 큰 세그먼트에는 가상 워크 로드에 대 한 네트워킹 성능을 향상 시킵니다.

이전에이 NIC에 의해 구현 되는 오프 로드 아쉽게도이 어댑터가 가상 스위치에 연결한 현재 사용할 수 없도록 합니다. Windows Server 2019 및 Windows에서 vSwitch의 RSC 10 년 10 월 2018 업데이트는이 제한을 제거 합니다.

기본적으로 vSwitch의 RSC는 외부 가상 스위치에서 사용 됩니다.

참조 항목:

-  [공지 블로그](https://blogs.technet.microsoft.com/networking/2018/08/22/netperf4vw/)

-  [유효성 검사 가이드는 IT 전문가](https://aka.ms/RSC-Validation)
