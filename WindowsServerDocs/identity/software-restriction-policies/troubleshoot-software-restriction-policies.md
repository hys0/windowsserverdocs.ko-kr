---
title: 소프트웨어 제한 정책 문제 해결
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4fd53736-03e7-4bf9-ba90-d1212d93e19a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: abf592930f5347fa10e83c644671f68f9dc1a3f6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872384"
---
# <a name="troubleshoot-software-restriction-policies"></a>소프트웨어 제한 정책 문제 해결

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 Windows Server 2008 및 Windows Vista의 소프트웨어 제한 정책 (SRP)부터 문제를 해결할 때 일반적인 문제 및 해결 방법 설명.

## <a name="introduction"></a>소개
SRP(소프트웨어 제한 정책)는 도메인의 컴퓨터에서 실행 중인 소프트웨어 프로그램을 식별하고, 실행할 해당 프로그램의 기능을 제어하는 그룹 정책 기반 기능입니다. 소프트웨어 제한 정책을 사용하면 명확하게 식별된 응용 프로그램만 실행할 수 있도록 고도로 제한된 컴퓨터 구성을 만들 수 있습니다. 이러한 Microsoft Active Directory Domain Services 및 그룹 정책과 통합 되어 있지만 독립 실행형 컴퓨터 에서도 구성할 수 있습니다. SRP에 대 한 자세한 내용은 참조는 [소프트웨어 제한 정책](software-restriction-policies.md)합니다.

Windows Server 2008 R2 및 Windows 7 부터는 Windows AppLocker 용도로 사용할 수 있습니다 또는 SRP 함께 대신 응용 프로그램 제어 전략의 일부입니다.

### <a name="windows-cannot-open-a-program"></a>Windows 프로그램을 열 수 없습니다.
"Windows 열 수 없습니다이 프로그램 소프트웨어 제한 정책에 의해 되었기 때문에 한다는 메시지가 사용자. 자세한 내용은 이벤트 뷰어를 열고 하거나 시스템 관리자에 게 문의 합니다. " 또는 명령줄에는 메시지가 표시 되 면 "시스템이 지정된 된 프로그램을 실행할 수 없습니다."

**원인:** 기본 보안 수준을 (또는 규칙을)를 만든 소프트웨어 프로그램으로 설정 되도록 **허용 안 함**, 고 결과적으로 시작 되지 것입니다.

**해결 방법:** 메시지에 자세히 설명에 대 한 이벤트 로그를 확인 합니다. 이벤트 로그 메시지 소프트웨어 프로그램으로 설정 되어 나타냅니다 **허용 안 함** 프로그램에 적용 되는 규칙이 고 합니다.

### <a name="modified-software-restriction-policies-are-not-taking-effect"></a>수정 된 소프트웨어 제한 정책에는 내용이 적용 되지 않습니다.
**원인:** 그룹 정책을 통해 도메인에 지정 된 소프트웨어 제한 정책에는 로컬로 구성 된 모든 정책 설정을 재정의 합니다. 이 정책 설정을 재정의 하는 도메인에서 정책 설정의 임을 의미 수 있습니다.

**원인:** 그룹 정책 수 있는 새로 고쳐지지 해당 정책 설정. 그룹 정책 변경 내용을 적용 정책 설정을 정기적으로; 따라서는 디렉터리에서 만든 정책 변경 내용을 아직 새로 고쳐지지 않았습니다 가능성이 높습니다.

**솔루션:**

1.  네트워크에 대 한 소프트웨어 제한 정책을 수정 하는 컴퓨터는 도메인 컨트롤러에 연결할 수 있어야 합니다. 컴퓨터에 도메인 컨트롤러에 연결할 수 있는지 확인 합니다.

2.  네트워크를 벗어나 로깅 및 다음 네트워크에 다시 로그온 하 여 정책을 새로 고칩니다. 그룹 정책을 통해 모든 정책이 적용 되는 경우 다시 로그인 해당 정책 새로 고침 됩니다.

3.  로그 오프 한 후 다시 컴퓨터에 로그온 하 여 명령줄 유틸리티 gpupdate를 사용 하 여 정책 설정을 새로 고칠 수 있습니다. 최상의 결과 gpupdate를 실행 하 고에서 로그 오프 한 다음 컴퓨터에 다시 로그인 합니다. 일반적으로 보안 설정은 워크스테이션 또는 서버에서 90 분 마다 및 도메인 컨트롤러에서 5 분 마다 새로 고쳐집니다. 또한 보안 설정은 설정이 변경되었는지 여부에 관계없이 16시간마다 새로 고쳐집니다. 이들은 새로 고침 간격 다를 수 있습니다 각 도메인에 있도록 구성 가능한 설정입니다.

4.  어떤 정책이 적용 확인 합니다. 에 대 한 도메인 수준 정책을 확인 하십시오 **No 재정의** 설정 합니다.

5.  그룹 정책을 통해 도메인에 지정 된 소프트웨어 제한 정책에는 로컬로 구성 된 모든 정책을 재정의 합니다. Gpresult 명령줄 도구를 사용 하 여 정책의 최종 결과 결정 합니다. 이 수 로컬 설정을 재정의 하는 도메인에서 정책의 임을 의미 합니다.

6.  SRP 및 AppLocker 정책 설정이 같은 GPO에서 경우 AppLocker 설정이 우선적 Windows 7, Windows Server 2008 R2 이상. 다른 Gpo의 SRP 및 AppLocker 정책 설정을 배치 하는 것이 좋습니다.

### <a name="after-adding-a-rule-through-srp-you-cannot-log-on-to-your-computer"></a>SRP 통해 규칙을 추가한 후 로그온 할 수 없습니다 컴퓨터를
**원인:** 컴퓨터 시작 시 많은 프로그램 및 파일에 액세스 합니다. 설정 했을 수 실수로 이러한 프로그램 또는 파일 중 하나 **허용 안 함**합니다. 컴퓨터 프로그램 또는 파일에 액세스할 수 없는 때문에 제대로 시작할 수 없습니다.

**해결 방법:** 안전 모드에서 컴퓨터를 시작, 로컬 관리자로 로그온 하 고 프로그램 또는 파일을 실행 하도록 허용 하는 데 소프트웨어 제한 정책을 변경 합니다.

### <a name="a-new-policy-setting-is-not-applying-to-a-specific-file-name-extension"></a>특정 파일 이름 확장명에 새 정책 설정이 적용 되지 않습니다.
**원인:** 파일 이름 확장자가 지원 되는 파일 형식 목록이 아닙니다.

**해결 방법:** SRP에서 지 원하는 파일 형식 목록에 파일 이름 확장명을 추가 합니다.

소프트웨어 제한 정책 알 수 없거나 신뢰할 수 없는 코드를 규제 하는 문제를 해결 합니다. 소프트웨어 제한 정책은 소프트웨어를 식별 하 고, 사이트, 도메인 또는 OU에 로컬 컴퓨터에서 실행 하는 기능을 제어 보안 설정 및 GPO를 통해 구현할 수 있습니다.

### <a name="a-default-rule-is-not-restricting-as-expected"></a>기본 규칙이 예상 대로 제한 됩니다.
**원인:** 특정 규칙에 의해 재정의 됩니다 기본 규칙을 일으킬 수 있는 특정 순서로 적용 되는 규칙입니다. SRP 규칙 (가장 구체적인 정보부터 일반) 다음과 같은 순서로 적용 됩니다.

1.  해시 규칙

2.  인증서 규칙

3.  경로 규칙

4.  인터넷 영역 규칙

5.  기본 규칙

**해결 방법:** 응용 프로그램을 제한 하는 규칙을 평가 하 고 해당 하는 경우 기본 규칙을 남기고 모두 제거 합니다.

### <a name="unable-to-discover-which-restrictions-are-applied"></a>어떤 제한이 적용 되는 검색할 수 없습니다.
**원인:** 예기치 않은 동작에 대 한 명백한 원인인 및 GPO 새로 고침 문제 해결 되지 않는 있으므로 추가 조사가 필요 합니다.

**솔루션:**

1.  소프트웨어 제한 정책"."의 원본에 필터링 시스템 이벤트 로그를 조사 합니다. 항목을 명시적으로 규칙은 각 응용 프로그램에 대 한 구현 됩니다.

2.  고급 로깅을 사용 하도록 설정 합니다. 참조 [허용-거부 목록 확인 및 소프트웨어 제한 정책에 대 한 응용 프로그램 인벤토리](software-restriction-policies.md) 자세한 내용은 합니다.


