---
title: 소프트웨어 제한 정책 기술 개요
description: Windows Server 보안
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830854"
---
# <a name="software-restriction-policies-technical-overview"></a>소프트웨어 제한 정책 기술 개요

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 소프트웨어 제한 정책 설명 내용을 이전 릴리스에서 구현한 및 Windows로 시작 하는 소프트웨어 제한 정책을 만들고 배포 하는 데 추가 리소스 링크를 제공 시기와 기능을 사용 하는 방법 Server 2008 및 Windows Vista입니다.

## <a name="introduction"></a>소개
소프트웨어 제한 정책은 소프트웨어를 식별 하 고 로컬 컴퓨터에서 실행 하는 기능을 제어 하는 그룹 정책 기반 메커니즘을 사용 하 여 관리자를 제공 합니다. 이러한 정책은 알려진된 충돌에 대 한 Microsoft Windows 운영 체제 (Windows Server 2003 및 Windows XP Professional을 사용 하 여 시작)를 실행 하는 컴퓨터를 보호 하기 위한 악의적인 바이러스와 같은 보안 위협 으로부터 컴퓨터를 사용할 수 있는 및 트로이 목마 프로그램을 추가 합니다. 또한 소프트웨어 제한 정책을 사용하여 명확하게 식별된 응용 프로그램만 실행할 수 있도록 고도로 제한된 컴퓨터 구성을 만들 수 있습니다. 소프트웨어 제한 정책은 Microsoft Active Directory 및 그룹 정책에 통합되어 있습니다. 독립 실행형 컴퓨터에 소프트웨어 제한 정책을 만들 수도 있습니다.

소프트웨어 제한 정책은 완전히 신뢰할 수 없는 스크립트와 기타 코드를 실행하지 못하도록 제한하기 위해 관리자가 만든 규정으로 구성된 신뢰할 수 있는 정책입니다. 소프트웨어 제한 정책 확장 로컬 그룹 정책 편집기를 로컬 컴퓨터 또는 도메인 전체에서 응용 프로그램의 사용을 제한 하는 것에 대 한 설정을 관리할 수 있는 단일 사용자 인터페이스를 제공 합니다.

## <a name="procedures"></a>절차

-   [소프트웨어 제한 정책 관리](administer-software-restriction-policies.md)

    -   [소프트웨어 제한 정책에 대 한 허용-거부 목록 및 응용 프로그램 인벤토리 확인](determine-allow-deny-list-and-application-inventory-for-software-restriction-policies.md)

    -   [소프트웨어 제한 정책 규칙을 사용 하 여 작동 합니다.](work-with-software-restriction-policies-rules.md)

    -   [전자 메일 바이러스 로부터 컴퓨터를 보호 하기 위해 소프트웨어 제한 정책 사용](use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus.md)

-   [소프트웨어 제한 정책 문제 해결](troubleshoot-software-restriction-policies.md)

## <a name="software-restriction-policy-usage-scenarios"></a>소프트웨어 제한 정책 사용 시나리오
비즈니스 사용자에 게 전자 메일, 인스턴트 메시징 및 피어-투-피어 응용 프로그램을 사용 하 여 공동 작업을 수행 합니다. 이러한 공동 작업 커질수록 컴퓨팅 비즈니스에 인터넷 사용 하 여 특히 웜, 바이러스, 악의적인 사용자나 공격자가 위협을 같은 악성 코드 로부터 위협 그렇게 합니다.

사용자 (예:.vbs) 스크립트에 악의적인 코드에서 네이티브 Windows 실행 파일 (.exe 파일) (예:.doc 파일), 문서에서 매크로에 이르기까지 다양 한 형태로 나타날 수 있습니다. 악의적인 사용자 또는 공격자가 소셜 엔지니어링 메서드 종종 바이러스와 웜 포함 하는 코드를 실행 하는 사용자를 사용 합니다. (소셜 엔지니어링 사람들을 속여 해당 암호 또는 일종의 보안 정보에 대 한 용어입니다.) 이러한 코드를 활성화 하는 경우 네트워크에 대 한 서비스 거부 공격을 생성, 중요 한 정보나 개인 데이터 인터넷, 컴퓨터의 보안 위험에 처하게 보내거나 있습니다 하드 디스크 드라이브의 내용이 손상입니다.

IT 조직과 사용자는 소프트웨어를 실행 하기에 안전 하 고 없는 결정할 수 있어야 합니다. 많은 수 및 악의적인 코드는 폼을 사용 하 여 까다로운 작업이이 됩니다.

알 수 없거나 지원 되지 않는 소프트웨어 및 악의적인 코드에서 해당 네트워크 컴퓨터를 보호 하기 위해, 조직 전체 보안 전략의 일환으로 소프트웨어 제한 정책을 구현할 수 있습니다.

관리자는 소프트웨어 제한 정책을 사용하여 다음과 같은 작업을 수행할 수 있습니다.

-   신뢰할 수 있는 코드 정의

-   스크립트, 실행 파일 및 ActiveX 컨트롤을 규제할 수 있는 유연한 그룹 정책 설계

소프트웨어 제한 정책은 소프트웨어 제한 정책을 준수하는 응용 프로그램(예: 스크립팅 응용 프로그램) 및 운영 체제에서 강제 적용됩니다.

관리자는 특히 다음과 같은 목적으로 소프트웨어 제한 정책을 사용할 수 있습니다.

-   클라이언트 컴퓨터에서 실행 가능한 소프트웨어 (실행 파일)를 지정 합니다.

-   사용자가 공유 컴퓨터에서 특정 프로그램을 실행할 수 없도록 지정

-   클라이언트 컴퓨터에 신뢰할 수 있는 게시자를 추가할 수 있는 사람 지정

-   (지정 정책은 모든 사용자에 게 영향을 줍니다 나 클라이언트 컴퓨터에서 사용자의 하위 집합) 소프트웨어 제한 정책의 범위 설정

-   실행 파일이 로컬 컴퓨터, OU(조직 구성 단위), 사이트 또는 도메인에서 실행될 수 없도록 방지합니다. 이는 악성 사용자의 잠재적인 문제점을 해결하는 데 소프트웨어 제한 정책을 사용하지 않는 경우에 적절합니다.

## <a name="BKMK_Diffs_Changes"></a>차이점 및의 기능 변경 사항
SRP for Windows Server 2012 및 Windows 8의 기능에는 변경 하지 않고 있습니다.

**지원 되는 버전**

소프트웨어 제한 정책만 구성 및 이상에서 실행 중인 컴퓨터에 적용할 수 있습니다 Windows Server 2003, Windows Server 2012 이상 Windows XP, Windows 8을 포함 합니다.

> [!NOTE]
> 특정 버전의 Windows 클라이언트 운영 체제부터 Windows Vista의 소프트웨어 제한 정책 필요는 없습니다. 그룹 정책을 통해 도메인에서 관리 되지 않는 컴퓨터에 분산된 정책을 받지 못할 수 있습니다.

**소프트웨어 제한 정책과 AppLocker의 응용 프로그램 제어 기능을 비교**

다음 표에서 소프트웨어 제한 정책 (SRP) 기능 및 AppLocker의 특징과 기능을 비교 합니다.

|응용 프로그램 제어 기능|SRP|AppLocker|
|----------------|----|-------|
|범위|SRP 정책은 Windows XP 및 Windows Server 2003부터 모든 Windows 운영 체제에 적용할 수 있습니다.|AppLocker 정책은 Windows Server 2008 R2, Windows Server 2012, Windows 7 및 Windows 8에만 적용 됩니다.|
|정책 만들기|SRP 정책은 그룹 정책을 통해 유지 됩니다 및 관리자만 GPO의 SRP 정책을 업데이트할 수 있습니다. 로컬 컴퓨터의 관리자에는 로컬 GPO에 정의 된 SRP 정책은 수정할 수 있습니다.|AppLocker 정책은 그룹 정책을 통해 유지 됩니다 및 GPO의 관리자만 정책을 업데이트할 수 있습니다. 로컬 컴퓨터의 관리자에는 로컬 GPO에 정의 된 AppLocker 정책을 수정할 수 있습니다.<br /><br />AppLocker를 사용할 경우 사용자를 지원 웹 페이지로 안내하기 위해 오류 메시지를 사용자 지정할 수 있습니다.|
|정책 유지 관리|SRP 정책은 그룹 정책 관리 콘솔 (GPMC) 또는 (로컬 정책을 만들면) 하는 경우 로컬 보안 정책 스냅인을 사용 하 여 업데이트 해야 합니다.|AppLocker 정책은 로컬 보안 정책 스냅인 (정책을 만들면 로컬로) 하는 경우, GPMC 또는 Windows PowerShell AppLocker cmdlet을 사용 하 여 업데이트할 수 있습니다.|
|정책 적용|SRP 정책은 그룹 정책을 통해 배포 됩니다.|AppLocker 정책은 그룹 정책을 통해 배포 됩니다.|
|적용 모드|SRP는 "거부 목록 모드" 관리자는 기본적으로 파일의 나머지를 실행할 수 있습니다 하는 반면이 엔터프라이즈에서 허용 하지 않으려는 이러한 파일에 대 한 규칙을 만들 수 있습니다 위치에서 작동 합니다.<br /><br />"허용 목록 모드"에서 SRP를 구성할 수도 있습니다는 기본적으로 모든 파일 차단 되 고 관리자를 만들 필요가 허용 하려는 파일에 대 한 규칙을 허용 합니다.|AppLocker는 "허용 목록 모드" 파일만를 가지는 일치 하는 허용 규칙을 실행할 수 있는 위치에서 작동 하는 기본으로 합니다.|
|제어할 수 있는 파일 형식|SRP에는 다음 파일 형식을 제어할 수 있습니다.<br /><br />실행 파일<br />-Dll<br />-스크립트<br />-Windows 설치 관리자<br /><br />SRP에는 개별적으로 각 파일 형식을 제어할 수 없습니다. 단일 규칙 컬렉션의 모든 SRP 규칙은입니다.|AppLocker에는 다음 파일 형식을 제어할 수 있습니다.<br /><br />실행 파일<br />-Dll<br />-스크립트<br />-Windows 설치 관리자<br />패키지 앱 및 설치 관리자 (Windows Server 2012 및 Windows 8)<br /><br />AppLocker 5 개 파일 형식 마다 별도 규칙 컬렉션을 유지합니다.|
|지정 된 파일 형식|SRP를 확장할 수 있는 실행으로 간주 되는 파일 형식 목록을 지원 합니다. 관리자는 실행 고려해 야 하는 파일의 확장명을 추가할 수 있습니다.|AppLocker이를 지원 하지 않습니다. AppLocker는 현재 다음 파일 확장명을 지원합니다.<br /><br />실행 파일 (.exe,.com)<br />-   Dlls (.ocx, .dll)<br />-스크립트 (.vbs,.js,. ps1,.cmd,.bat)<br />-Windows 설치 관리자 (.msi,.mst,.msp)<br />-패키지 된 앱 설치 관리자 (.appx)|
|규칙 유형|SRP는 네 가지 유형의 규칙을 지원합니다.<br /><br />-   Hash<br />-   Path<br />서명<br />인터넷 영역|AppLocker는 세 가지 유형의 규칙을 지원합니다.<br /><br />-   Hash<br />-   Path<br />-   Publisher|
|해시 값을 편집합니다.|SRP에 사용자 지정 해시 값을 제공 하는 작업을 할당할 수 있습니다.|AppLocker에는 자체 해시 값을 계산 합니다. 내부적으로 이식 가능한 실행 파일 (Exe 및 Dll) 및 Windows 설치 관리자 및 나머지 SHA1 플랫 파일 해시를 Authenticode SHA1 해시를 사용합니다.|
|다른 보안 수준에 대 한 지원|SRP를 사용 하 여 관리자 권한이 있는 앱을 실행할 수를 지정할 수 있습니다. 관리자가 이러한 규칙을 구성할 수 있습니다 따라서 제한 된 권한 및 관리자 권한으로 하지는 메모장은 항상 실행 됩니다.<br /><br />SRP 및 이전 버전 Windows Vista에서 여러 보안 수준을 지원 합니다. Windows 7에서 해당 목록이 두 수준으로 제한 합니다. 허용 되지 않습니다 및 무제한 (기본 사용자 변환 허용 안 함).|AppLocker에는 보안 수준을 지원 하지 않습니다.|
|패키지 된 앱 및 패키지 된 앱 설치 관리자를 관리 합니다.|없습니다.|.appx는 AppLocker를 관리할 수 있는 올바른 파일 형식입니다.|
|사용자 또는 사용자 그룹에 규칙을 대상으로|SRP 규칙은 특정 컴퓨터의 모든 사용자에 게 적용 됩니다.|특정 사용자 또는 사용자 그룹에 AppLocker 규칙을 지정할 수 있습니다.|
|규칙 예외에 대 한 지원|SRP 규칙 예외를 지원 하지 않습니다.|AppLocker 규칙 "허용 모두에서 Windows 제외 하 고 Regedit.exe" 같은 규칙을 만드는 관리자가 허용 하는 예외를 가질 수 있습니다.|
|감사 모드에 대 한 지원|SRP는 감사 모드를 지원 하지 않습니다. SRP 정책을 테스트 하는 유일한 방법은 테스트 환경 설정 및 몇 가지 실험을 실행 하는 경우|AppLocker는 관리자가 사용자 환경에 영향을 주지 않고 실제 프로덕션 환경에서 해당 정책의 효과 테스트를 허용 하는 감사 모드를 지원 합니다. 결과 만족 했으면 정책 적용을 시작할 수 있습니다.|
|정책 내보내기 및 가져오기에 대 한 지원|SRP는 정책 가져오기/내보내기를 지원 하지 않습니다.|AppLocker는 가져오기 및 내보내기 정책을 지원 합니다. 이 샘플 컴퓨터에 AppLocker 정책을 만들 수 있습니다 테스트 하 고 해당 정책을 내보내고 원하는 GPO로 다시 합니다.|
|규칙 적용|내부적으로, SRP 규칙 적용을 더 어렵게 하는 사용자 모드에서 발생 합니다.|내부적으로 Exe 및 Dll에 대 한 AppLocker 규칙은 사용자 모드에서이 적용 하는 것 보다 안전 하 게 연결 되는 커널 모드에서 적용 됩니다.|

## <a name="system-requirements"></a>시스템 요구 사항
소프트웨어 제한 정책만 구성 및 이상에서 실행 중인 컴퓨터에 적용할 수 있습니다 Windows Server 2003 이상 Windows XP 합니다. 그룹 정책 소프트웨어 제한 정책을 포함 하는 그룹 정책 개체를 배포 해야 합니다.

## <a name="software-restriction-policies-components-and-architecture"></a>소프트웨어 제한 정책 구성 요소 및 아키텍처
소프트웨어 제한 정책은 운영 체제 및 소프트웨어 프로그램의 런타임 실행을 제한 하려면 소프트웨어 제한 정책을 호환 응용 프로그램에 대 한 메커니즘을 제공 합니다.

높은 수준에서 소프트웨어 제한 정책을 다음 구성 요소로 구성 됩니다.

-   소프트웨어 제한 정책 API입니다. 만들고 소프트웨어 제한 정책을 구성 하는 규칙을 구성 하는 Api (응용 프로그래밍 인터페이스) 사용 됩니다. 또한 가지 소프트웨어 제한 정책 쿼리, 처리에 대 한 Api 및 소프트웨어 제한 정책을 적용 합니다.

-   소프트웨어 제한 정책 관리 도구입니다. 이루어져이 **소프트웨어 제한 정책** 의 확장을 **로컬 그룹 정책 개체 편집기** 스냅인을 만들고 소프트웨어 제한 정책을 편집 하는 관리자를 사용 합니다.

-   응용 프로그램 및 운영 체제 Api 집합이 소프트웨어 제한 정책이 런타임 시 소프트웨어 제한 정책의 적용을 제공 하기 위한 Api를 호출 하는 합니다.

-   Active Directory 및 그룹 정책 소프트웨어 제한 정책은 소프트웨어 제한 정책을 Active Directory에서 범위 지정 및 적절 한 이러한 정책의 응용 프로그램을 필터링 한 적절 한 클라이언트에 전파 하는 그룹 정책 인프라에 따라 다릅니다. 대상 컴퓨터입니다.

-   Authenticode 및 WinVerify 신뢰 Api는 서명 된 실행 파일을 처리 하는 데 사용 됩니다.

-   이벤트 뷰어에서 그렇습니다. 소프트웨어 제한 정책 로그 이벤트는 이벤트 뷰어 로그를 사용 하는 함수입니다.

-   결과 집합의 정책 rsop (정책) 클라이언트에 적용 될 실제 정책의 진단에 도움이 될 수 있습니다.

SRP 아키텍처에 대 한 자세한 내용은 SRP에서 규칙, 프로세스 및 상호 작용을 관리 하는 방법 참조 [소프트웨어 제한 정책 작동 방법](https://technet.microsoft.com/library/cc786941(v=WS.10).aspx) Windows Server 2003 기술 라이브러리에서.

## <a name="BKMK_Best_Practices"></a>모범 사례

### <a name="do-not-modify-the-default-domain-policy"></a>기본 도메인 정책을 수정 하지 마십시오.

-   기본 도메인 정책을 편집 하지 않는 것을 항상 있으면 사용자 지정된 도메인 정책에 따라 사용 하 여 문제가 있는 경우에 기본 도메인 정책을 다시 적용할 수입니다.

### <a name="create-a-separate-group-policy-object-for-software-restriction-policies"></a>소프트웨어 제한 정책에 대 한 별도 그룹 정책 개체를 만듭니다.

-   소프트웨어 제한 정책에 대 한 별도 그룹 정책 개체 (GPO)를 만드는 경우 도메인 정책에 따라의 나머지 부분을 사용 하지 않도록 설정 하지 않고 비상 시에서 소프트웨어 제한 정책을 비활성화할 수 있습니다.

### <a name="if-you-experience-problems-with-applied-policy-settings-restart-windows-in-safe-mode"></a>적용 된 정책 설정 사용 하 여 문제가 있으면 Windows 안전 모드에서 다시 시작 합니다.

-   소프트웨어 제한 정책에는 Windows 안전 모드에서 시작 될 때 적용 되지 않습니다. 소프트웨어 제한 정책 사용 하 여 워크스테이션에서 실수로 잠글 경우 안전 모드에서 컴퓨터를 다시 시작, 로컬 관리자로 로그온, 정책을 수정, 실행 **gpupdate**, 컴퓨터를 다시 시작 하 고 정상적으로 로그온 합니다.

### <a name="use-caution-when-defining-a-default-setting-of-disallowed"></a>허용 안 함의 기본 설정을 정의 하는 경우에 주의 해야 합니다.

-   기본 설정을 정의 하는 경우 **허용 안 함**를 명시적으로 허용 되는 소프트웨어를 제외 하 고 소프트웨어를 모두 허용 되지 않습니다. 열려고 하는 모든 파일에 열 수 있는 소프트웨어 제한 정책 규칙 있어야 합니다.

-   로부터 보호 하기 위해 관리자는 기본 보안 수준이 설정 된 경우 시스템 잠그게 **허용 안 함**, 네 레지스트리 경로 규칙을 자동으로 만들어집니다. 삭제 하거나 이러한 레지스트리 경로 규칙을 수정할 수 있습니다. 그러나이 권장 되지 않습니다.

### <a name="for-best-security-use-access-control-lists-in-conjunction-with-software-restriction-policies"></a>최상의 보안을 위해 액세스 제어 목록 소프트웨어 제한 정책과 함께에서 사용 합니다.

-   사용자가 허용 되지 않는 파일을 이동 하거나 이름을 변경 하거나 무제한 파일을 덮어쓰는 방법으로 소프트웨어 제한 정책을 우회 하려고 할 수 있습니다. 결과적으로, 액세스 제어 목록 (Acl)를 사용 하 여 사용자가 이러한 작업을 수행 하는 데 필요한 액세스를 거부 하는 것이 좋습니다.

### <a name="test-new-policy-settings-thoroughly-in-test-environments-before-applying-the-policy-settings-to-your-domain"></a>도메인 정책 설정을 적용 하기 전에 테스트 환경에서 새 정책 설정의 철저히 테스트 합니다.

-   새 정책 설정을 원래 예상 하는 것과 다르게 작동 될 수 있습니다. 테스트 네트워크를 통해 정책 설정을 배포할 때 문제가 발생할 가능성이 감소 합니다.

-   새 정책 설정을 테스트 하는 조직의 도메인에서 별도 테스트 도메인을 설정할 수 있습니다. 또한 테스트 GPO를 만들고 테스트 조직 구성 단위에 연결 하 여 정책 설정을 테스트할 수 있습니다. 테스트 사용자를 사용 하 여 정책 설정에서 철저히 테스트 하는 경우에 도메인에 테스트 GPO를 연결할 수 있습니다.

-   프로그램 또는 파일을 설정 하지 마십시오 **허용 안 함** 테스트 수 있는 효과 확인 하지 않고 있습니다. 특정 파일에 대 한 제한 컴퓨터나 네트워크의 작업에 심각한 영향을 줄 수 있습니다.

-   예상 대로 수행 되지 않는 정책 설정을 잘못 입력 된 정보 또는 실수 입력 될 수 있습니다. 새 정책 설정을 적용 하기 전에 테스트 예기치 않은 동작을 방지할 수 있습니다.

### <a name="filter-user-policy-settings-based-on-membership-in-security-groups"></a>보안 그룹의 멤버 자격에 따라 사용자 정책 설정을 필터링 합니다.

-   사용자 또는 그룹을 하지 않으려면 선택을 취소 하 여 적용할 정책 설정을 지정할 수 있습니다 합니다 **그룹 정책 적용** 및 **읽기** 에 있는 확인란을 **보안**GPO에 대 한 속성 대화 상자의 탭 합니다.

-   읽기 권한이 거부 되는 컴퓨터에서 정책 설정을 다운로드 되지 않습니다. 결과적으로 더 적은 대역폭 네트워크 보다 신속 하 게 함수를 통해 불필요 한 정책 설정을 다운로드 하 여 사용 됩니다. 읽기 권한을 거부 하려면 선택 **거부** 에 대 한 합니다 **읽기** 에 있는 확인란을 **보안** GPO에 대 한 속성 대화 상자의 탭 합니다.

### <a name="do-not-link-to-a-gpo-in-another-domain-or-site"></a>다른 도메인 또는 사이트에서 GPO를 연결 하지 않습니다.

-   GPO에 연결 하면 다른 도메인 또는 사이트의 성능이 저하 될 수 있습니다.

## <a name="additional-resources"></a>추가 자료

|콘텐츠 형식|참조|
|--------|-------|
|**계획**|[소프트웨어 제한 정책 기술 참조](https://technet.microsoft.com/library/cc728085(v=WS.10).aspx)|
|**작업**|[소프트웨어 제한 정책 관리](administer-software-restriction-policies.md)|
|**문제 해결**|[소프트웨어 제한 정책 (2003)를 문제 해결](https://technet.microsoft.com/library/cc737011(v=WS.10).aspx)|
|**보안**|[위협 및 대책 소프트웨어 제한 정책 (2008)](https://technet.microsoft.com/library/dd349795(v=WS.10).aspx)<br /><br />[위협 및 대책 소프트웨어 제한 정책 (2008 R2)](https://technet.microsoft.com/library/hh125926(v=WS.10).aspx)|
|**도구 및 설정**|[소프트웨어 제한 정책 도구 및 설정 (2003)](https://technet.microsoft.com/library/cc782454(v=WS.10).aspx)|
|**커뮤니티 리소스**|[소프트웨어 제한 정책 사용 하 여 응용 프로그램 잠금](https://technet.microsoft.com/magazine/2008.06.srp.aspx?pr=blog)|


