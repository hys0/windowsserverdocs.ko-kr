---
title: 소프트웨어 제한 정책에 대한 허용-거부 목록 및 응용 프로그램 인벤토리 확인
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0abb73b6-b5d8-4505-8ab1-2f29e4bf0411
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 60e78912284715649938567d66ffb90b9890b1b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847294"
---
# <a name="determine-allow-deny-list-and-application-inventory-for-software-restriction-policies"></a>소프트웨어 제한 정책에 대한 허용-거부 목록 및 응용 프로그램 인벤토리 확인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

IT 전문가 위한이 항목에서는 허용을 만들고 거부 목록 소프트웨어 제한 정책 (SRP)부터 Windows Server 2008 및 Windows Vista로 관리 되는 응용 프로그램에 대 한 방법 지침을 제공 합니다.

## <a name="introduction"></a>소개
SRP(소프트웨어 제한 정책)는 도메인의 컴퓨터에서 실행 중인 소프트웨어 프로그램을 식별하고, 실행할 해당 프로그램의 기능을 제어하는 그룹 정책 기반 기능입니다. 소프트웨어 제한 정책을 사용하면 명확하게 식별된 응용 프로그램만 실행할 수 있도록 고도로 제한된 컴퓨터 구성을 만들 수 있습니다. 이러한 Microsoft Active Directory Domain Services 및 그룹 정책과 통합 되어 있지만 독립 실행형 컴퓨터 에서도 구성할 수 있습니다. SRP에 대 한 시작 지점에 대 한 참조를 [소프트웨어 제한 정책](software-restriction-policies.md)합니다.

Windows Server 2008 R2 및 Windows 7 부터는 Windows AppLocker 용도로 사용할 수 있습니다 또는 SRP 함께 대신 응용 프로그램 제어 전략의 일부입니다.

SRP를 사용 하 여 특정 작업을 수행 하는 방법에 대 한 내용은 다음을 참조 합니다.

-   [소프트웨어 제한 정책 규칙을 사용 하 여 작동 합니다.](work-with-software-restriction-policies-rules.md)

-   [전자 메일 바이러스 로부터 컴퓨터를 보호 하기 위해 소프트웨어 제한 정책 사용](use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus.md)

### <a name="what-default-rule-to-choose-allow-or-deny"></a>선택할 수 있는 기본 규칙: 허용 또는 거부
소프트웨어 제한 정책에서 기본 규칙을 기반으로 하는 두 가지 모드 중 하나에 배포할 수 있습니다. 허용 목록 또는 거부 목록입니다. 사용자 환경에서 실행 되는 모든 응용 프로그램을 식별 하는 정책을 만들 수 있습니다. 제한 및 정책 내에서 기본 규칙은 모든 응용 프로그램 실행을 명시적으로 허용 하지 않는 것을 차단 합니다. 실행 되지 않습니다;는 모든 응용 프로그램을 식별 하는 정책을 만들 수 있습니다. 기본 규칙은 Unrestricted 하 고 명시적으로 나열 되어 있는 응용 프로그램만 제한 합니다.

> [!IMPORTANT]
> 거부 목록 모드 응용 프로그램 제어에 대 한 조직에 대 한 높은 유지 관리 전략을 수 있습니다. 만들기 및 모든 맬웨어 및 기타 문제가 있는 응용 프로그램 금지 하는 진화 하는 목록을 유지 관리에 시간이 오래 걸리고 실수에 취약 것입니다.

### <a name="create-an-inventory-of-your-applications-for-the-allow-list"></a>허용 목록에 대 한 응용 프로그램의 인벤토리 생성
허용 기본 규칙을 효과적으로 사용 하려면 조직에서 응용 프로그램은 필요한 정확 하 게 결정 해야 합니다. Microsoft Application Compatibility Toolkit의 인벤토리 수집기와 같은 응용 프로그램 인벤토리를 생성 하도록 설계 하는 도구가 있습니다. 하지만 SRP 고급 로깅 기능을 정확 하 게 새로운 응용 프로그램을 실행 환경에서 이해할 수 있도록 합니다.

##### <a name="to-discover-which-applications-to-allow"></a>검색할 수 있도록 응용 프로그램

1.  테스트 환경에서 소프트웨어 제한 정책을 Unrestricted로 기본 규칙 집합을 사용 하 여 배포 하 고 모든 추가 규칙을 제거 합니다. 모든 응용 프로그램을 제한 하도록 하지 않고도 SRP를 사용 하도록 설정 하면 SPR 새로운 응용 프로그램 되는 실행을 모니터링할 수 됩니다.

2.  고급 로깅 기능을 활성화 하 고 로그 파일을 써야 하는 경로 설정 하기 위해 다음 레지스트리 값을 만듭니다.

    **"HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Safer\ CodeIdentifiers"**

    문자열 값입니다. *NameLogFile NameLogFile 경로*

    로그 파일에 항목이 기록 됩니다 SRP는 모든 응용 프로그램을 실행할 때를 평가 하므로 *NameLogFile* 응용 프로그램이 실행 될 때마다 합니다.

3.  로그 파일을 평가 합니다.

    각 로그 항목 상태:

    -   소프트웨어 제한 정책 및 프로세스는 호출 프로세스의 ID (PID)의 호출자에 게

    -   확인할 대상

    -   해당 응용 프로그램이 실행 하는 동안 발생 하는 SRP 규칙

    -   SRP 규칙에 대 한 식별자입니다.

    로그 파일에 작성 한 출력의 예:

**explorer.exe (PID = 4728) identifiedC:\Windows\system32\onenote.exe 규칙에 따라 무제한 usingpath, Guid = {320bd852-aa7c-4674-82c5-9a80321670a3}** 모든 응용 프로그램 및 관련된 코드 SRP 확인 하 고 차단 하도록 설정 하는 로그에 기록 됩니다 그런 다음 허용 목록에 대해 고려해 야 하는 실행 파일 확인에 사용할 수 있는 파일입니다.


