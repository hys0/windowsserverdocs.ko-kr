---
title: "거부 허용 목록 및 응용 프로그램 재고 제한 정책 소프트웨어에 대 한 확인"
description: "Windows Server 보안"
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="determine-allow-deny-list-and-application-inventory-for-software-restriction-policies"></a>거부 허용 목록 및 응용 프로그램 재고 제한 정책 소프트웨어에 대 한 확인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

IT 전문가 위한이 항목 허용 만들고 거부 목록 관리 Windows Server 2008 및 Windows Vista로 시작 하는 소프트웨어 제한 정책 (소매가) 하는 응용 프로그램에 대 한 방법 지침을 제공 합니다.

## <a name="introduction"></a>소개
소프트웨어 제한 정책 (소매가)은 도메인에 있는 컴퓨터에서 실행 중인 소프트웨어 프로그램으로 식별 하 고 이러한 프로그램을 실행 하는 기능을 제어 하는 그룹 정책 기반 기능입니다. 제한 정책이 소프트웨어를 사용 하 여 매우 제한적된 구성을 식별된 응용 프로그램을 실행 하면 컴퓨터에 대 한 만들 수 있습니다. 이러한 그룹 정책을 Microsoft Active Directory Domain Services와 통합만 독립 실행형 컴퓨터에를 구성할 수도 있습니다. 소매가, 출발점 참조는 [소프트웨어 제한 정책](software-restriction-policies.md)합니다.

Windows Server 2008 R2 및 Windows 7부터, Windows AppLocker에 사용할 수 대신 또는 소매가 협력 제어 전략 응용 프로그램의 일부입니다.

소매가 사용 하 여 특정 작업을 수행 하는 방법에 대 한 정보를 참조 하십시오.

-   [소프트웨어 제한 정책 규칙 사용](work-with-software-restriction-policies-rules.md)

-   [메일 바이러스 로부터 컴퓨터를 보호 하기 위해 제한 정책이 소프트웨어를 사용 하 여](use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus.md)

### <a name="what-default-rule-to-choose-allow-or-deny"></a>선택할 수 있는 기본 규칙: 허용
소프트웨어 제한 정책을 두 가지 모드 기본 규칙을 기반으로 하는 중 하나에 배포할 수 있습니다: 허용 목록 또는 거부 목록입니다. 귀하의 환경;에서 실행 하도록 허용 하는 모든 응용 프로그램을 식별 하는 정책 만들 수 있습니다. 정책에 따라 기본 규칙은 제한 하 고 실행 하려면 명시적으로 허용 하지 않는 모든 응용 프로그램을 차단 합니다. 또는 모든 응용 프로그램을 실행할 수 없다면; 식별 하는 정책 만들 수 있습니다. 기본 규칙은 제한 없음만 응용 프로그램을 명시적으로 나열 된을 제한 하 고 있습니다.

> [!IMPORTANT]
> 거부 목록 모드 응용 프로그램 컨트롤에 대 한 조직에 대 한 높은 유지 전략 될 수도 있습니다. 만들고 모든 맬웨어 및 기타 문제를 일으키는 응용 프로그램 하지 못하도록 하는 발전 목록을 유지 관리 하는 시간과 실수에 취약 것입니다.

### <a name="create-an-inventory-of-your-applications-for-the-allow-list"></a>허용 목록에 대 한 응용 프로그램의 인벤토리 만들기
허용 기본 규칙 사용할 효과적으로 조직에서 어떤 응용 프로그램이 필요한 정확 하 게 확인 해야 합니다. Microsoft Application Compatibility Toolkit의에서 인벤토리 컬렉터에 등 응용 프로그램 인벤토리 생성 하기 위해 설계 도구가 있습니다. 하지만 소매가 있는 고급 로깅 기능이 정확 하 게 무엇 응용 프로그램에서에서 실행 중인 사용자 환경을 이해할 수 있습니다.

##### <a name="to-discover-which-applications-to-allow"></a>응용 프로그램을 허용 검색

1.  테스트 환경에서 제한 없음 규칙 기본 설정 된 소프트웨어 제한 정책의 배포 하 고 모든 추가 규칙 제거 합니다. 응용 프로그램 제한 하기 위한를 않고도 소매가 사용 하면 SPR 무엇 응용 프로그램은 되 고 실행 모니터링할 수 됩니다.

2.  고급 로깅 기능을 활성화 하 고 로그 파일은 쓸 경로 설정 하기 위해 다음 레지스트리 값을 만듭니다.

    **"HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Safer\ CodeIdentifiers"**

    문자열 값: *NameLogFile 경로를 NameLogFile*

    항목이 로그 파일에 기록 됩니다 소매가 실행 될 때 응용 프로그램을 모두 평가 하기 때문에 *NameLogFile* 응용 프로그램이 실행 되는 때마다 합니다.

3.  평가 로그 파일

    각 로그 항목 상태:

    -   소프트웨어 제한 정책 및 PID (ID) 호출 하는 프로세스의 프로세스의 발신자

    -   평가 대상

    -   해당 응용 프로그램을 실행 하는 경우 만났습니다 소매가 규칙

    -   소매가 규칙에 대 한 식별자입니다.

    파일을 로그에 기록 출력의 예:

**explorer.exe (PID 4728 =) Guid 무제한 usingpath 일반적으로 identifiedC:\Windows\system32\onenote.exe {320bd852-aa7c-4674-82c5-9a80321670a3} =** 다음 결정 허용 목록에 대 한 것으로 간주 어떤 실행 해야 하는 데 사용할 수 있는 로그 파일에는 모든 응용 프로그램과 관련된 코드 소매가 확인 하 고 차단으로 설정 된 기록 됩니다.


