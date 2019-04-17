---
title: "소프트웨어 제한 정책 기술 개요"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc7013b0-0efd-40fd-bd6d-75128adbd0b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: d007d55ced9c6a18581eaedb4edb66db9eeccab9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="software-restriction-policies-technical-overview"></a>소프트웨어 제한 정책 기술 개요

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에 설명 소프트웨어 제한 정책을 어떻게 변경 지난 릴리스에서 구현 되었습니다 기능을 사용 하는 방법 및 시기 및 생성 및 Windows Server 2008 및 Windows Vista로 시작 소프트웨어 제한 정책을 배포를 위해 추가 리소스에 대 한 링크를 제공 합니다.

## <a name="introduction"></a>소개
소프트웨어 제한 정책이 소프트웨어를 식별 하 고 로컬 컴퓨터에서 실행 하는 기능을 제어 하는 그룹 정책 기반 메커니즘 관리자에 게 제공 됩니다. 이러한 정책에 대해 알려진된 충돌 Microsoft Windows 운영 체제 (Windows Server 2003 및 Windows XP Professional로 시작)를 실행 하는 컴퓨터를 보호 하 고 컴퓨터 악의적인 바이러스, 트로이 말 프로그램 등 보안 위협 요소 로부터 보호를 사용할 수 있습니다. 또한 매우 제한적 구성을 식별된 응용 프로그램을 실행 하면 컴퓨터에 대 한 제한 정책을 소프트웨어를 사용할 수 있습니다. 그룹 정책 및 Microsoft Active Directory를 제한 정책이 소프트웨어 통합 되어 있습니다. 또한 소프트웨어 제한 정책 독립 실행형 컴퓨터에 만들 수 있습니다.

소프트웨어 제한 정책은 규정 스크립트와 완벽 하 게 실행에서 신뢰할 수 없는 다른 코드를 제한 하려면 관리자 권한으로 설정 되는 보안 정책이 합니다. 로컬 그룹 정책 편집기 소프트웨어 제한 정책 확장 응용 프로그램의 사용을 제한에 대 한 설정을 관리할 수 있는 단일 사용자 인터페이스 도메인 전체 로컬 컴퓨터에서 제공 합니다.

## <a name="procedures"></a>절차

-   [소프트웨어 제한 정책을 관리합니다](administer-software-restriction-policies.md)

    -   [거부 허용 목록 및 응용 프로그램 재고 제한 정책 소프트웨어에 대 한 확인](determine-allow-deny-list-and-application-inventory-for-software-restriction-policies.md)

    -   [소프트웨어 제한 정책 규칙 사용](work-with-software-restriction-policies-rules.md)

    -   [메일 바이러스 로부터 컴퓨터를 보호 하기 위해 제한 정책이 소프트웨어를 사용 하 여](use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus.md)

-   [소프트웨어 제한 정책 문제 해결](troubleshoot-software-restriction-policies.md)

## <a name="software-restriction-policy-usage-scenarios"></a>소프트웨어 제한 정책 사용 시나리오
비즈니스 사용자가 전자 메일, 인스턴트 메시징 및 피어 투 피어 응용 프로그램을 사용 하 여 공동 작업. 특히 비즈니스 컴퓨팅 인터넷 사용 하 여 이러한 공동 작업 증가 웜, 바이러스와 악성 사용자 또는 공격자가 위협와 같은 악성 코드 위협 함 있습니다.

사용자에 게 기본 Windows 실행 파일에서 이르는 다양 한 형태로 악의적인 코드를 받을 수 (.exe files), 매크로 스크립트 (예:.vbs 파일)를 (예:.doc 파일), 문서에 있습니다. 악의적인 사용자가 또는 공격자 사회 공학적 방법 바이러스와 웜 포함 된 코드를 실행 하는 사용자를 흔히 사용 합니다. (사회 공학적 피플을 속여 암호 또는 어떤 형태로 보안 정보에 대 한 용어는.) 해당 코드를 정품 인증 된 경우 서비스 거부 공격이 네트워크에서 생성, 인터넷에 중요 한 개인 데이터를 전송, 컴퓨터의 보안 위험에 노출 하거나 수 하드 디스크 드라이브의 내용을 손상 합니다.

조직의 IT 및 사용자에 게 확인 하는 소프트웨어를 안전 하 게 실행 하도록 하 고 하지 즉 수 있어야 합니다. 이 많은와 악의적인 코드 양식 어려운 작업 됩니다.

조직 으로부터 보호 하기 위해 해당 네트워크 컴퓨터 악의적인 코드 및 알 수 없거나 지원 되지 않는 소프트웨어를 전체 보안 전략 자신의의 일환으로 제한 정책이 소프트웨어를 구현할 수 있습니다.

관리자 다음 작업에 대 한 제한 정책을 소프트웨어를 사용할 수 있습니다.

-   신뢰할 수 있는 코드를 정의합니다

-   스크립트 실행 파일, ActiveX 컨트롤을 조정 유연한 그룹 정책을 디자인합니다

소프트웨어 제한 정책을 준수 하는 응용 프로그램 (예: 스크립팅 응용 프로그램) 및 운영 체제 소프트웨어 제한 정책이 적용 됩니다.

특히, 관리자 다음 목적을 위해 제한 정책을 소프트웨어를 사용할 수 있습니다.

-   지정 클라이언트 컴퓨터에서 실행할 수 있는 소프트웨어 (실행 파일)

-   사용자 공유 컴퓨터에서 특정 프로그램을 실행 하는 것을 방지합니다

-   신뢰할 수 있는 게시자 클라이언트 컴퓨터에 추가할 수 있는 사용자 지정

-   (정책은 모든 사용자에 게 영향을 여부는 클라이언트에서 사용자의 하위 집합 지정) 소프트웨어 제한 정책 범위 설정

-   실행 파일 로컬 컴퓨터, 조직 단위, 사이트 또는 도메인에서 실행 되지 않도록 합니다. 게 되는 경우에서 사용자가 악성 소프트웨어 제한 정책을 잠재적 문제를 해결 하려면 사용 하지 않는 경우 합니다.

## <a name="BKMK_Diffs_Changes"></a>차이점 및 기능 변경
Windows 8 및 Windows Server 2012 용 소매가 기능이 없습니다 변경 사항이 있습니다.

**지원 되는 버전**

소프트웨어 제한 정책만 구성 및 이상 실행 하는 컴퓨터에 적용할 수 있는 Windows Server 2003, Windows Server 2012 및 최소 Windows XP, Windows 8을 포함 하 여 합니다.

> [!NOTE]
> 특정 버전의 Windows Vista로 Windows 클라이언트 운영 체제 시작 하는 소프트웨어 제한을 정책이 필요가 없습니다. 그룹 정책으로 관리 도메인 되지 컴퓨터 분산된 정책 받지 못할 수 있습니다.

**응용 프로그램 제한 정책 소프트웨어 및 AppLocker 제어 기능을 비교**

다음 표에서 특징과 기능 소프트웨어 제한 정책 (소매가) 기능 및 AppLocker 비교합니다.

|응용 프로그램 제어 기능|소매가|AppLocker|
|----------------|----|-------|
|범위|소매가 정책은 일부 터 Windows XP 및 Windows Server 2003 모든 Windows 운영 체제에 적용 수 있습니다.|Windows Server 2008 R2, Windows Server 2012, Windows 7 및 Windows 8에만 AppLocker 정책이 적용 됩니다.|
|정책 만들기|그룹 정책을 통해 소매가 정책은 그대로 유지 됩니다 및 GPO 관리자만 소매가 정책 업데이트할 수 있습니다. 로컬 컴퓨터에서 관리자 로컬 GPO에 정의 된 소매가 정책 수정할 수 있습니다.|그룹 정책을 통해 AppLocker 정책은 그대로 유지 됩니다 및 GPO 관리자만 정책을 업데이트할 수 있습니다. 로컬 컴퓨터에서 관리자 로컬 GPO에 정의 된 AppLocker 정책 수정할 수 있습니다.<br /><br />AppLocker 사용자에 대 한 도움말 웹 페이지를으로 오류 메시지를 사용자 지정할을 수 있습니다.|
|정책 유지 관리|소매가 정책은 그룹 정책 GPMC (관리 콘솔) (정책을 로컬로 만들면) 하는 경우 현지 보안 정책이 스냅인 사용 하 여 업데이트 해야 합니다.|AppLocker 정책에서 보안 정책이 로컬 스냅인 (정책을 로컬로 만들면) 하는 경우, 또는 GPMC 또는 AppLocker Windows PowerShell cmdlet 사용 하 여 업데이트할 수 있습니다.|
|정책 응용 프로그램|그룹 정책을 통해 소매가 정책 배포 됩니다.|그룹 정책을 통해 AppLocker 정책 배포 됩니다.|
|적용 모드|SRP works in the "deny list mode" where administrators can create rules for files that they do not want to allow in this Enterprise whereas the rest of the file are allowed to run by default.<br /><br />SRP can also be configured in the "allow list mode" such that the by default all files are blocked and administrators need to create allow rules for files that they want to allow.|AppLocker by default works in the "allow list mode" where only those files are allowed to run for which there is a matching allow rule.|
|제어할 수 있는 파일 형식|소매가는 다음과 같은 파일 형식 제어할 수 있습니다.<br /><br />-실행<br />-Dll<br />-스크립트<br />Windows 설치 관리자<br /><br />소매가 각 파일 형식 별도로 제어할 수 없습니다. 모든 소매가 규칙 단일 규칙 컬렉션에 됩니다.|AppLocker는 다음과 같은 파일 형식 제어할 수 있습니다.<br /><br />-실행<br />-Dll<br />-스크립트<br />Windows 설치 관리자<br />패키지 앱과 (Windows 8 및 Windows Server 2012) 설치<br /><br />AppLocker 각 5 파일 형식에 대 한 별도 규칙 컬렉션을 유지합니다.|
|지정 된 파일 형식|소매가 extensible 실행 것으로 간주 되는 파일 형식 목록은 지원 합니다. 관리자 확장 실행 고려해 야 하는 파일을 추가할 수 있습니다.|AppLocker이 지원 하지 않습니다. 현재 AppLocker 다음 파일 확장명을 지원합니다.<br /><br />-실행 파일 (.exe,.com)<br />-Dll (.ocx,.dll)<br />-스크립트 (.vbs,.js,.ps1,.cmd,.bat)<br />Windows 설치 관리자 (.msi,.mst,.msp)<br />-설치 관리자 (.appx) 패키지 앱|
|규칙 유형|소매가 4 가지 형식의 규칙을 지원합니다.<br /><br />-해시<br />경로<br />서명<br />-인터넷 영역|AppLocker 규칙의 세 종류를 지원합니다.<br /><br />-해시<br />경로<br />-출판사|
|해시 값 편집|소매가 관리자를 사용자 지정 해시 값을 제공할 수 있습니다.|AppLocker 계산 해시 값 자체 합니다. 내부적으로 SHA1 Authenticode 해시 나머지 SHA1 평평한 파일 콘텐츠의 해시 휴대용 실행 파일 (Exe 및 Dll) 및 Windows 설치 관리자에 대 한 사용합니다.|
|다양 한 보안 수준에 대 한 지원|소매가 관리자 앱을 실행할 수는 권한을 지정할 수 있습니다. 관리자 이러한 규칙 구성할 수, 따라서 해당 메모장은 항상 제한 된 권한 및 절대 관리자 권한으로 실행 합니다.<br /><br />Windows Vista 및 이전 버전 소매가 여러 보안 수준 지원 됩니다. 두 개의 수준으로 제한 된 해당 목록이 Windows 7: 허용 하지 않는 한 무제한 (기본 사용자 변환 허용 안 함).|AppLocker 보안 수준을 지원 하지 않습니다.|
|패키지 된 앱 설치 및 패키지 된 앱 관리|수 없습니다.|.appx는 AppLocker 관리할 수 있는 유효한 파일 형식입니다.|
|규칙의 사용자 그룹 또는 사용자를 대상으로|소매가 규칙 특정 컴퓨터에서 모든 사용자에 게 적용 됩니다.|AppLocker 규칙의 사용자 그룹 또는 특정 사용자 지정할 수 있습니다.|
|규칙 예외에 대 한 지원|소매가 규칙 예외를 지원 하지 않는|AppLocker rules can have exceptions which allow administrators to create rules such as "Allow everything from Windows except for Regedit.exe".|
|감사 모드에 대 한 지원|소매가 감사 모드를 지원 하지 않습니다. 테스트 환경을를 설정 하는 몇 가지 실험 소매가 정책 테스트 하는 유일한 방법은입니다.|AppLocker는 관리자는 사용자 경험에 영향을 주지 않고 실제 생산 환경에서 자신의 정책 영향을 테스트할 수 있도록 해줍니다 감사 모드를 지원 합니다. 결과 했으면 정책을 적용을 시작할 수 있습니다.|
|내보내고 가져오는 정책에 대 한 지원|소매가 정책 내보내기를 지원 하지 않습니다.|AppLocker 가져오고 내보내기 정책 지원 합니다. 이 AppLocker 정책 샘플 컴퓨터에 만들 수 있도록 테스트해 한 다음 해당 정책 내보내고 원하는 GPO에 다시 가져올 합니다.|
|규칙 집행|내부적으로 소매가 규칙 집행 상대적으로 약 해지 인 사용자 모드에서 발생 합니다.|내부적으로 Exe 및 Dll AppLocker 규칙 사용자 모드로 적용 보다 더 안전 하 고 커널 모드에 적용 됩니다.|

## <a name="system-requirements"></a>시스템 요구 사항
소프트웨어 제한 정책만 구성 및 이상 실행 하는 컴퓨터에 적용할 수 있는 Windows Server 2003, 이상 및 Windows XP입니다. 그룹 정책은 제한 정책 소프트웨어를 포함 하는 그룹 정책 개체 배포할 필요 합니다.

## <a name="software-restriction-policies-components-and-architecture"></a>소프트웨어 제한 정책 구성 요소 및 아키텍처
소프트웨어 제한 정책을 운영 체제와 제한 런타임 소프트웨어 프로그램을 실행 하기 위해 소프트웨어 제한 정책을 준수 응용 프로그램에 대 한 장치를 제공 합니다.

높은 수준의 제한 정책이 소프트웨어 구성 요소도 구성 됩니다.

-   소프트웨어 제한 정책 API 합니다. 응용 프로그램 프로그래밍 인터페이스 (Api)를 만들고 구성 규칙 소프트웨어 제한 정책 구성 하는 데 사용 됩니다. 또한는 제한 정책 쿼리, 처리 하기 위한 Api 소프트웨어 및 소프트웨어 제한 정책이 적용 됩니다.

-   소프트웨어 제한 정책 관리 도구입니다. 이 **소프트웨어 제한 정책** 의 확장은 **로컬 그룹 정책 개체 편집기** 스냅인을 만들고 소프트웨어 제한 정책을 편집 하는 관리자 사용 하 여 합니다.

-   운영 체제 Api 일련 및 응용 프로그램 소프트웨어 제한 정책 실행 시 소프트웨어 제한 정책을 적용을 제공 하기 위해 Api를 호출 하는 합니다.

-   Active Directory 및 그룹 정책을 합니다. 소프트웨어 제한 정책이 소프트웨어 제한 정책 Active Directory에서와 범위 필터링 이러한 정책 응용 프로그램을 적절 한 대상 컴퓨터 및 적절 한 클라이언트를 전파 그룹 정책 인프라에 따라 다릅니다.

-   Authenticode 및 WinVerify 신뢰 Api 서명된 실행 파일을 처리 하는 데 사용 되는 합니다.

-   이벤트 뷰어 합니다. 소프트웨어 제한 정책 로그 이벤트 이벤트 뷰어 로그를 사용 하는 기능입니다.

-   결과 설정의 (RSoP)는 정책을 실제 정책 클라이언트에 적용 되는 진단에 도움이 될 수 있습니다.

For more information about SRP architecture, how SRP manages rules, processes and interactions, see [How Software Restriction Policies Work](https://technet.microsoft.com/library/cc786941(v=WS.10).aspx) in the Windows Server 2003 Technical Library.

## <a name="BKMK_Best_Practices"></a>모범 사례

### <a name="do-not-modify-the-default-domain-policy"></a>기본 도메인 정책을 수정 하지 않습니다.

-   기본 도메인 정책을 편집 하면 항상 있는지 정책에 정의 도메인에 문제가 발생 하는 경우 기본 도메인 정책의 다시 적용할 수 있습니다.

### <a name="create-a-separate-group-policy-object-for-software-restriction-policies"></a>그룹 정책 개체 소프트웨어 제한 정책에 대 한 별도 만듭니다.

-   소프트웨어 제한 정책에 대 한 별도 그룹 정책 개체 (GPO)를 만드는 경우 도메인 정책의 나머지 부분을 해제 하지 않고 비상시에 제한 정책을 소프트웨어를 비활성화할 수 있습니다.

### <a name="if-you-experience-problems-with-applied-policy-settings-restart-windows-in-safe-mode"></a>적용된 정책 설정에 문제가 발생 하는 경우를 안전 모드로 Windows를 다시 시작 합니다.

-   안전 모드로 Windows를 시작할 때 소프트웨어 제한 정책이 적용 되지 않습니다. 소프트웨어 제한 정책 워크스테이션 실수로 잠글 경우 안전 모드에서 컴퓨터를 다시 시작, 로컬 관리자 권한으로 로그온, 정책을 수정, 실행 **gpupdate**, 컴퓨터를 다시 정상적으로 로그온 합니다.

### <a name="use-caution-when-defining-a-default-setting-of-disallowed"></a>정의할 허용 안 함의 기본 설정을 때는 주의 해야 합니다.

-   기본 설정의 정의 하는 경우 **허용 안 함**, 모든 소프트웨어가 명시적으로 허용 된 소프트웨어를 제외 하 고 허용 되지 않습니다. 열려는 하는 모든 파일에 열 수 있게 해 주는 정책 규칙 소프트웨어 제한 있어야 합니다.

-   으로부터 보호 하기 위해 관리자 자체 시스템에서 기본 보안 수준이 설정한 경우 잠금 **허용 안 함**, 네 레지스트리 경로 규칙은 자동으로 만들어집니다. 삭제 하거나 이러한 레지스트리 경로 규칙을 수정할 수 있습니다. 그러나이 권장 되지 않습니다.

### <a name="for-best-security-use-access-control-lists-in-conjunction-with-software-restriction-policies"></a>최적의 보안을 위해 액세스 제어 목록을 제한 정책 소프트웨어와 함께에서 사용 합니다.

-   사용자가 우회 무제한 파일 덮어쓰지 하거나 이름 바꾸기 또는 허용 되지 않은 파일을 이동 하 여 소프트웨어 제한 정책을 하려고 할 수 있습니다. 결과적으로, 액세스 제어 (Acl 목록)을 사용 하 여 사용자가 이러한 작업을 수행 하는 데 필요한 액세스 거부 하려면이 좋습니다.

### <a name="test-new-policy-settings-thoroughly-in-test-environments-before-applying-the-policy-settings-to-your-domain"></a>도메인에 정책 설정을 적용 되기 전에 테스트 환경에서 완전히 새로운 정책 설정을 테스트 합니다.

-   새로운 정책 설정을 원래 예상 보다 다르게 작동할 수도 있습니다. 정책 설정을 네트워크를 통해 배포할 때 문제가 발생 하는 기회를 가지게를 줄어듭니다 테스트 합니다.

-   새 정책 설정을 테스트 하는 조직 도메인의 별도 테스트 도메인을 설정할 수 있습니다. 또한 테스트 GPO 만들고 테스트 조직에 연결 하 여 정책 설정 테스트할 수 있습니다. 정책 설정을 테스트 사용자와 철저 하 게 테스트 때 테스트 GPO 도메인에 연결할 수 있습니다.

-   프로그램 또는 파일을 설정 하지 않은 **허용 안 함** 볼 수 있는 영향을 테스트 합니다. 특정 파일에 대 한 제한 심각한 컴퓨터 또는 네트워크의 작동 영향을 줄 수 있습니다.

-   정책 설정을 예상 대로 수행 되지 않는 정보를 잘못 입력 또는 실수로 입력 될 수 있습니다. 새 정책 설정에 적용 하기 전에 테스트 예기치 않은 문제가 되지 않을 수 있습니다.

### <a name="filter-user-policy-settings-based-on-membership-in-security-groups"></a>사용자 정책 설정을 구성원 보안 그룹에 따라를 필터링 합니다.

-   사용자 또는 그룹 정책 설정을 선택 취소 하 여 적용 않을 지정할 수 있는 **그룹 정책을 적용** 및 **읽기** 에 있는 확인란은 **보안** gpo 속성 대화 상자를 탭 합니다.

-   읽기 권한이 거부 되 면 컴퓨터에서 정책 설정을 다운로드 되지 않습니다. 결과적으로, 덜 대역폭 네트워크 더 빠르게 작동할 수 있게 하는 불필요 한 정책 설정을 다운로드 하 여 사용 됩니다. 읽기 자녀가, 선택 **거부** 에 대 한는 **읽기** 에 있는 확인란의 **보안** gpo 속성 대화 상자를 탭 합니다.

### <a name="do-not-link-to-a-gpo-in-another-domain-or-site"></a>다른 도메인 또는 사이트 하 연결 하지 않습니다.

-   다른 도메인 또는 사이트 하 연결 성능이 저하 될 수 있습니다.

## <a name="additional-resources"></a>추가 리소스

|콘텐츠 종류|참조|
|--------|-------|
|**계획**|[소프트웨어 제한 정책 기술 참조](https://technet.microsoft.com/library/cc728085(v=WS.10).aspx)|
|**작업**|[소프트웨어 제한 정책을 관리합니다](administer-software-restriction-policies.md)|
|**문제 해결**|[소프트웨어 제한 정책을 (2003)의 문제 해결](https://technet.microsoft.com/library/cc737011(v=WS.10).aspx)|
|**보안**|[위협과 대책 소프트웨어 제한에 대 한 정책을 (2008)](https://technet.microsoft.com/library/dd349795(v=WS.10).aspx)<br /><br />[위협과 대책 소프트웨어 제한에 대 한 정책을 (2008 r 2)](https://technet.microsoft.com/library/hh125926(v=WS.10).aspx)|
|**도구 및 설정**|[소프트웨어 제한 정책을 도구 및 설정 (2003)](https://technet.microsoft.com/library/cc782454(v=WS.10).aspx)|
|**커뮤니티 리소스**|[소프트웨어 제한 정책 응용 프로그램 잠금](https://technet.microsoft.com/magazine/2008.06.srp.aspx?pr=blog)|


