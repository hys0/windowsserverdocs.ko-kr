---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Windows 시간 서비스
description: ''
author: shortpatti
ms.author: pashort
manager: brianlic
ms.date: 02/01/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b997d1f26e8da82e0d595b1ce13763e0a87d6d03
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="windows-time-service-w32time"></a>Windows 시간 (W32Time) 서비스

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

(W32Time) Windows 시간 서비스의 날짜 및 시간 Active Directory DS (도메인 서비스 AD)를 실행 하는 모든 컴퓨터에 대 한 동기화 합니다. 시간 동기화가 제대로 작동 많은 Windows 서비스 및 비즈니스 줄 (lob 기간 업무) 응용 프로그램에 대 한 중요 합니다. Windows 시간 서비스 네트워크 시간 Protocol (NTP)를 사용 하 여 네트워크에서 컴퓨터 시계 동기화 합니다. NTP 정확한 시간 값 또는 타임 스탬프 네트워크 리소스를 유효성 검사 액세스 요청에 할당 될 수 있는지 확인 합니다.

Windows 시간 (W32Time) 서비스 항목에서 다음과 같은 콘텐츠를 사용할 수 있습니다.
- **[Windows 2016 정확한 시간](accurate-time.md)합니다.** 전체 이전 버전과 호환성이 NTP 오래 된 Windows 버전과 호환성을 유지 하면서 시간 동기화 정확도 Windows Server 2016에 크게 향상 되었습니다.  합리적인 작동 조건 1를 유지할 수 UTC 또는 Windows Server 2016 및 Windows 10 1 주년 업데이트 도메인 구성원에 대해 더와 관련 하 여 ms 정확도 합니다.
- **[Windows 시간 서비스 기술 참조](windows-time-service-tech-ref.md)합니다.** W32Time 서비스는 다양 한 구성에 대 한 필요 없이 컴퓨터에 대 한 네트워크 시계 동기화를 제공합니다. W32Time 서비스 Kerberos v 5 인증 성공적으로 작동 하 고, 따라서 광고 DS 기반 인증을 필수입니다.
    - **[Windows 시간 서비스의 작동 방식](How-the-Windows-Time-Service-Works.md)합니다.** Windows 시간 서비스 정확한 구현 네트워크 시간 Protocol (NTP)의 하지는 않지만 네트워크를 통해 컴퓨터에 시계 최대한 정확 하 게 되도록 NTP 사양에 정의 된 알고리즘 복잡 한 제품군을 사용 합니다.
    - **[Windows 시간 서비스 도구 및 설정](Windows-Time-Service-Tools-and-Settings.md)합니다.** 대부분의 도메인 회원 컴퓨터 NT5DS 도메인 계층에서 시간을 동기화 하는 것을 의미 하는 시간 클라이언트 유형이 있습니다. 이만 일반적인 예외 주 도메인 컨트롤러 (PDC) 에뮬레이터가 작업 마스터 시간 외부 시간 원본을와 동기화 하도록 일반적으로 구성 된 숲 루트 도메인의로 작동 하는 도메인 컨트롤러입니다.

## <a name="related-topics"></a>관련된 항목
도메인 계층 및 득점 시스템에 대 한 자세한 내용은 참조는 ["시간 서비스 Windows 란?"](https://blogs.msdn.microsoft.com/w32time/2007/07/07/what-is-windows-time-service/) 블로그 게시물 합니다.

Windows 시간 공급자 플러그 인 모델은 [technet 설명](https://msdn.microsoft.com/en-us/library/windows/desktop/ms725475%28v=vs.85%29.aspx)합니다.

Windows 2016 정확성 시간 문서에서 참조 되는 addendum 다운로드할 수 [여기](http://windocs.blob.core.windows.net/windocs/WindowsTimeSyncAccuracy_Addendum.pdf)

Windows 시간 서비스의 빠른 개요를 살펴보세요이 [비디오 고급 개요](https://aka.ms/WS2016TimeVideo)합니다.

<!-- In this guide
In this guide:
Windows Accurate Time
High Accuracy
Support Boundary
Configuration for High Accuracy
Traceability for Compliance
Best Practices
Technical Reference
How the Windows Time Service Works
Windows Time Service Tools and Settings
-->

