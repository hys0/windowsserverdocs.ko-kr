---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Windows 시간 서비스
description: ''
author: shortpatti
ms.author: pashort
manager: dougkim
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: e3dbaa188426ac81073e706db3adc6ab0a655c01
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405186"
---
# <a name="windows-time-service-w32time"></a>W32Time (Windows 시간 서비스)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 이상

W32Time (Windows 시간 서비스)은 Active Directory Domain Services (AD DS)에서 실행 되는 모든 컴퓨터의 날짜와 시간을 동기화 합니다. 시간 동기화는 많은 Windows 서비스 및 LOB (기간 업무) 응용 프로그램의 적절 한 작동에 매우 중요 합니다. Windows 시간 서비스는 NTP (Network Time Protocol)를 사용 하 여 네트워크의 컴퓨터 클럭을 동기화 합니다. NTP를 사용 하면 정확한 클록 값 또는 타임 스탬프를 네트워크 유효성 검사 및 리소스 액세스 요청에 할당할 수 있습니다.

W32Time (Windows 시간 서비스) 항목에서 다음 콘텐츠를 사용할 수 있습니다.
- **[Windows Server 2016 정확한 시간](accurate-time.md)입니다.** 이전 버전과 완전 NTP 이전 Windows 버전과 호환성을 유지 하면서 Windows Server 2016에서 시간 동기화 정확도 크게 향상 되었습니다. 합리적인 운영 조건에서는 Windows Server 2016 및 Windows 10 기념일 업데이트 도메인 구성원에 대 한 UTC 이상에 대해 1 밀리초 정확도를 유지할 수 있습니다.
- **[정확도가 높은 환경에 대 한 경계를 지원](support-boundary.md)합니다.** 이 문서에서는 매우 정확 하 고 안정적인 시스템 시간을 필요로 하는 환경에서 W32Time (Windows 시간 서비스)의 지원 경계를 설명 합니다.
- **[정확도를 높이기 위해 시스템 구성](configuring-systems-for-high-accuracy.md)** Windows 10 및 Windows Server 2016의 시간 동기화는 상당히 향상 되었습니다.  적절 한 운영 조건에서 시스템은 UTC와 관련 하 여 1ms (밀리초) 정확도를 유지 하도록 구성할 수 있습니다.
- **[추적 가능성을 위한 Windows 시간](windows-time-for-traceability.md)입니다.** 많은 섹터의 규정을 준수 하려면 시스템을 UTC로 추적 해야 합니다.  이는 시스템의 오프셋이 UTC와 관련 하 여 증명 된 수 있음을 의미 합니다.  규정 준수 시나리오를 사용 하도록 설정 하기 위해 Windows 10 및 Server 2016는 시스템 클록에서 수행 되는 작업을 이해 하기 위해 운영 체제의 관점에서 그림을 제공 하는 새로운 이벤트 로그를 제공 합니다.  이러한 이벤트 로그는 Windows 시간 서비스에 대해 계속 생성 되며 나중에 분석할 수 있도록 검사 하거나 보관할 수 있습니다.
- **[Windows 시간 서비스 기술 참조](windows-time-service-tech-ref.md)입니다.** W32Time 서비스는 광범위 한 구성이 필요 없는 컴퓨터에 대 한 네트워크 클록 동기화를 제공 합니다. W32Time 서비스는 Kerberos V5 인증을 성공적으로 수행 하는 데 필수적 이며, 따라서 AD DS 기반 인증을 수행 하는 데 필요 합니다.
    - **[Windows 시간 서비스의 작동 방식](How-the-Windows-Time-Service-Works.md)입니다.** Windows 시간 서비스 네트워크 시간 프로토콜 (NTP)의 정확 하 게 구현 하지는 않지만 네트워크 전반에 걸쳐 컴퓨터 시계는 최대한 정확 하 게 있도록 NTP 사양에 정의 된 복잡 한 알고리즘 제품군을 사용 합니다.
    - **[Windows 시간 서비스 도구 및 설정](Windows-Time-Service-Tools-and-Settings.md).** 대부분의 도메인 구성원 컴퓨터에는 시간 클라이언트 유형의 NT5DS가 있습니다. 즉, 도메인 계층에서 시간을 동기화 합니다. 이에 대 한 유일한 일반적인 예외는 포리스트 루트 도메인의 PDC (주 도메인 컨트롤러) 에뮬레이터 작업 마스터 역할을 하는 도메인 컨트롤러입니다 .이는 일반적으로 시간을 외부 시간 원본과 동기화 하도록 구성 됩니다.


## <a name="related-topics"></a>관련 항목
도메인 계층 구조 및 점수 매기기 시스템에 대 한 자세한 내용은 ["Windows 시간 서비스 정의"](https://blogs.msdn.microsoft.com/w32time/2007/07/07/what-is-windows-time-service/) 를 참조 하십시오. 블로그 게시물입니다.

Windows 시간 공급자 플러그 인 모델은 [technet 문서화](https://msdn.microsoft.com/library/windows/desktop/ms725475%28v=vs.85%29.aspx)합니다.

Windows 2016 정확한 시간 문서에서 참조 하는 추 록을 [여기](https://windocs.blob.core.windows.net/windocs/WindowsTimeSyncAccuracy_Addendum.pdf) 에서 다운로드할 수 있습니다.

Windows 시간 서비스에 대 한 간략 한 개요를 보려면 [개략적인 개요 비디오](https://aka.ms/WS2016TimeVideo)를 살펴보세요.
