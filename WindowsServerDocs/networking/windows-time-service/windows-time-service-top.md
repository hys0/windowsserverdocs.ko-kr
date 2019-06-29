---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Windows 시간 서비스
description: ''
author: shortpatti
ms.author: pashort
manager: dougkim
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 3233434403594ef9e2555c0329c4791d1fb99709
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469585"
---
# <a name="windows-time-service-w32time"></a>Windows 시간 서비스 (w32time))

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 이상

Windows 시간 서비스 (w32time)) Active Directory Domain Services (AD DS)에서 실행 하는 모든 컴퓨터에 대 한 시간과 날짜를 동기화 합니다. 시간 동기화는 여러 Windows 서비스 및-업무용 (LOB) 응용 프로그램의 올바른 작동에 중요 합니다. Windows 시간 서비스 (NTP (Network Time Protocol)를 사용 하 여 네트워크의 컴퓨터 시계 동기화. NTP 네트워크 유효성 검사 및 리소스 액세스 요청에는 정확한 시간 값 또는 타임 스탬프를 할당할 수 있도록 보장 합니다.

Windows 시간 서비스 (w32time)) 항목에 다음 콘텐츠는 사용할 수 있습니다.
- **[Windows Server 2016 정확한 시간](accurate-time.md)합니다.** 이전 버전과 완전 NTP 이전 Windows 버전과 호환성을 유지 하면서 Windows Server 2016에서 시간 동기화 정확도 크게 향상 되었습니다. 적절 한 작업 상태에 1을 유지할 수 있습니다 UTC 또는 Windows Server 2016 및 Windows 10 1 주년 업데이트에 해당 하는 도메인의 구성원에 대 한 관련 하 여 ms 정확도입니다.
- **[정확도 높은 환경에 대 한 지원 경계](support-boundary.md)합니다.** 이 문서에서는 매우 정확 하 고 안정적인 시스템 시간을 필요로 하는 환경에서 Windows 시간 서비스 (w32time))에 대 한 지원 범위를 설명 합니다.
- **[높은 정확도 대 한 시스템 구성](configuring-systems-for-high-accuracy.md)합니다.** Windows 10 및 Windows Server 2016에서 시간 동기화 크게 향상 되었습니다.  적절 한 작동 조건 시스템이 1ms (밀리초)을 유지 하기 위해 구성 수 (UTC)에 대해 정확도 이상.
- **[추적 기능에 대 한 Windows 시간](windows-time-for-traceability.md)합니다.** 많은 섹터의 규정 시스템을 UTC로 추적 가능 해야 합니다.  즉, UTC와 관련 하 여 시스템의 오프셋을 증명할 수 있습니다.  규정 준수 시나리오를 사용 하려면 Windows 10 및 Server 2016 시스템 클록에서 수행 된 작업의 이해를 운영 체제의 관점에서 그림을 제공 하는 새 이벤트 로그를 제공 합니다.  이러한 이벤트 로그 Windows 시간 서비스에 대해 지속적으로 생성 된 검사 또는 보관 나중에 분석할 수 있습니다.
- **[Windows 시간 서비스에 대 한 기술 참조](windows-time-service-tech-ref.md)합니다.** W32Time 서비스는 광범위 한 구성이 필요 없이 컴퓨터에 대 한 네트워크 시계 동기화를 제공합니다. Kerberos V5 인증 작업을 성공적으로 실행 하 고 따라서 AD DS 기반 인증으로 W32Time 서비스 반드시 필요 합니다.
    - **[Windows 시간 서비스의 작동 원리](How-the-Windows-Time-Service-Works.md)합니다.** Windows 시간 서비스 네트워크 시간 프로토콜 (NTP)의 정확 하 게 구현 하지는 않지만 네트워크 전반에 걸쳐 컴퓨터 시계는 최대한 정확 하 게 있도록 NTP 사양에 정의 된 복잡 한 알고리즘 제품군을 사용 합니다.
    - **[Windows 시간 서비스 도구 및 설정](Windows-Time-Service-Tools-and-Settings.md)합니다.** 대부분의 도메인 구성원 컴퓨터 형식이 시간 클라이언트 NT5DS 도메인 계층 구조에서 시간을 동기화 하는 것을 의미 합니다. 만 일반적인 예외는 일반적으로 외부 시간 원본을 사용 하 여 시간을 동기화 하도록 구성 된 포리스트 루트 도메인의 주 도메인 컨트롤러 (PDC) 에뮬레이터 작업 마스터로 작동 하는 도메인 컨트롤러입니다.


## <a name="related-topics"></a>관련 항목
도메인 계층 구조 및 점수 매기기에 대 한 자세한 내용은 참조는 ["Windows 시간 서비스 무엇입니까?"](https://blogs.msdn.microsoft.com/w32time/2007/07/07/what-is-windows-time-service/) 블로그 게시물입니다.

Windows 시간 공급자 플러그 인 모델은 [technet 문서화](https://msdn.microsoft.com/library/windows/desktop/ms725475%28v=vs.85%29.aspx)합니다.

Windows 2016 정확한 내용 시간 문서에서 참조 하는 추 록을 다운로드할 수 있습니다 [여기](https://windocs.blob.core.windows.net/windocs/WindowsTimeSyncAccuracy_Addendum.pdf)

Windows 시간 서비스의 간략 한 개요를 위해이 살펴보겠습니다 [높은 수준의 개요 비디오](https://aka.ms/WS2016TimeVideo)합니다.
