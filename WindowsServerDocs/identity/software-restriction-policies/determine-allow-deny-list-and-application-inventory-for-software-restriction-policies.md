---
title: 소프트웨어 제한 정책에 대한 허용-거부 목록 및 응용 프로그램 인벤토리 확인
description: Windows Server 보안
ms.prod: windows-server
ms.technology: security-software-restriction-policies
ms.topic: article
ms.assetid: 0abb73b6-b5d8-4505-8ab1-2f29e4bf0411
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: c0fdb5c1d7c4b03610a173c6cd0575d39646a7d0
ms.sourcegitcommit: af1cf89632d62a94943d3ad9f6b5234b88499278
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81524908"
---
# <a name="determine-allow-deny-list-and-application-inventory-for-software-restriction-policies"></a>소프트웨어 제한 정책에 대한 허용-거부 목록 및 응용 프로그램 인벤토리 확인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

IT 전문가를 위한이 항목에서는 Windows Server 2008 및 Windows Vista부터 응용 프로그램에 대 한 허용 및 거부 목록을 SRP (소프트웨어 제한 정책)로 관리 하는 방법에 대 한 지침을 제공 합니다.

## <a name="introduction"></a>소개
SRP(소프트웨어 제한 정책)는 도메인의 컴퓨터에서 실행 중인 소프트웨어 프로그램을 식별하고, 실행할 해당 프로그램의 기능을 제어하는 그룹 정책 기반 기능입니다. 소프트웨어 제한 정책을 사용하면 명확하게 식별된 애플리케이션만 실행할 수 있도록 고도로 제한된 컴퓨터 구성을 만들 수 있습니다. 이러한 기능은 Microsoft Active Directory Domain Services 및 그룹 정책와 통합 되어 있지만 독립 실행형 컴퓨터 에서도 구성할 수 있습니다. SRP에 대 한 시작 지점은 [소프트웨어 제한 정책](software-restriction-policies.md)을 참조 하세요.

Windows Server 2008 R2 및 Windows 7 부터는 응용 프로그램 제어 전략의 일부에 대 한 SRP를 사용 하거나 사용 하지 않고 Windows AppLocker를 사용할 수 있습니다.

SRP를 사용 하 여 특정 작업을 수행 하는 방법에 대 한 자세한 내용은 다음을 참조 하세요.

-   [소프트웨어 제한 정책 규칙 사용](work-with-software-restriction-policies-rules.md)

-   [소프트웨어 제한 정책을 사용 하 여 전자 메일 바이러스 로부터 컴퓨터를 보호 합니다.](use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus.md)

### <a name="what-default-rule-to-choose-allow-or-deny"></a>선택할 기본 규칙: 허용 또는 거부
소프트웨어 제한 정책은 기본 규칙의 기본 인 허용 목록 또는 거부 목록 중 하나로 배포할 수 있습니다. 사용자 환경에서 실행할 수 있는 모든 응용 프로그램을 식별 하는 정책을 만들 수 있습니다. 정책 내의 기본 규칙은 제한 되며 명시적으로 실행을 허용 하지 않는 모든 응용 프로그램을 차단 합니다. 또는 실행할 수 없는 모든 응용 프로그램을 식별 하는 정책을 만들 수 있습니다. 기본 규칙은 무제한 이며 명시적으로 나열 된 응용 프로그램만 제한 합니다.

> [!IMPORTANT]
> 거부 목록 모드는 응용 프로그램 제어와 관련 하 여 조직에 대 한 높은 유지 관리 전략 일 수 있습니다. 모든 맬웨어 및 기타 문제가 있는 응용 프로그램을 차단 하는 진화 하는 목록을 만들고 유지 관리 하는 데는 시간이 많이 걸리고 실수에 취약 합니다.

### <a name="create-an-inventory-of-your-applications-for-the-allow-list"></a>허용 목록에 사용할 응용 프로그램의 인벤토리를 만듭니다.
기본 허용 규칙을 효과적으로 사용 하려면 조직에 필요한 응용 프로그램을 정확 하 게 결정 해야 합니다. Microsoft 응용 프로그램 호환성 도구 키트의 인벤토리 수집기와 같은 응용 프로그램 인벤토리를 생성 하도록 설계 된 도구가 있습니다. 그러나 SRP에는 사용자 환경에서 실행 중인 응용 프로그램을 정확 하 게 이해 하는 데 도움이 되는 고급 로깅 기능이 있습니다.

##### <a name="to-discover-which-applications-to-allow"></a>허용할 응용 프로그램을 검색 하려면

1.  테스트 환경에서 기본 규칙이 무제한으로 설정 된 소프트웨어 제한 정책을 배포 하 고 추가 규칙을 제거 합니다. 응용 프로그램을 제한 하지 않고 SRP를 사용 하도록 설정 하는 경우 SPR는 실행 중인 응용 프로그램을 모니터링할 수 있습니다.

2.  고급 로깅 기능을 사용 하도록 설정 하 고 로그 파일을 쓸 경로를 설정 하려면 다음 레지스트리 값을 만듭니다.

    **"HKEY_LOCAL_MACHINE \SOFTWARE\Policies\Microsoft\Windows\Safer\CodeIdentifiers"**

    문자열 값: *LogFileName path To LogFileName*

    SRP는 실행 될 때 모든 응용 프로그램을 평가 하므로 응용 프로그램이 실행 될 때마다 로그 파일 *Namelogfile* 에 항목이 기록 됩니다.

3.  로그 파일 평가

    각 로그 항목의 상태는 다음과 같습니다.

    -   소프트웨어 제한 정책의 호출자와 호출 프로세스의 PID (프로세스 ID)

    -   평가할 대상입니다.

    -   해당 응용 프로그램이 실행 될 때 발생 한 SRP 규칙입니다.

    -   SRP 규칙의 식별자입니다.

    로그 파일에 기록 되는 출력의 예는 다음과 같습니다.

**explorer.exe (PID = 4728) identifiedC: \ Windows\system32\onenote.exe As 무제한 usingpath rule, Guid = {320bd852-aa7c-4674-82c5-9a80321670a3}**    SRP를 확인 하 고 차단 하도록 설정 하는 모든 응용 프로그램 및 관련 코드는 로그 파일에 기록 되며,이 파일을 사용 하 여 허용 된 목록에 대해 고려해 야 하는 실행 파일을 확인할 수 있습니다.

