---
title: "소프트웨어 제한 정책 문제 해결"
description: "Windows Server 보안"
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-software-restriction-policies"></a>소프트웨어 제한 정책 문제 해결

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 Windows Server 2008 및 Windows Vista로 시작 하는 소프트웨어 제한 정책 (소매가) 문제를 해결할 때 관련 된 일반적인 문제 및 해결 방법 설명 합니다.

## <a name="introduction"></a>소개
소프트웨어 제한 정책 (소매가)은 도메인에 있는 컴퓨터에서 실행 중인 소프트웨어 프로그램으로 식별 하 고 이러한 프로그램을 실행 하는 기능을 제어 하는 그룹 정책 기반 기능입니다. 제한 정책이 소프트웨어를 사용 하 여 매우 제한적된 구성을 식별된 응용 프로그램을 실행 하면 컴퓨터에 대 한 만들 수 있습니다. 이러한 그룹 정책을 Microsoft Active Directory Domain Services와 통합만 독립 실행형 컴퓨터에를 구성할 수도 있습니다. 소매가 대 한 자세한 내용은 참조는 [소프트웨어 제한 정책](software-restriction-policies.md)합니다.

Windows Server 2008 R2 및 Windows 7부터, Windows AppLocker에 사용할 수 대신 또는 소매가 협력 제어 전략 응용 프로그램의 일부입니다.

### <a name="windows-cannot-open-a-program"></a>프로그램을 열 수 없는 Windows
사용자가 메시지가 "Windows 열 수 없는이 프로그램 소프트웨어가 제한 정책에 따라 되었기 때문입니다. 자세한 내용은 이벤트 뷰어 열거나 시스템 관리자에 게 문의 합니다. " 또는 명령줄 메시지에 "시스템에서 지정된 된 프로그램을 실행할 수 없습니다."

**원인:** 기본 보안 수준이 (또는 규칙) 소프트웨어 프로그램으로 설정 되어 수 있도록 생성 되었습니다 **허용 안 함**, 시작 되지 않으면 따라서 하 고 있습니다.

**해결 방법:** 메시지에 대 한 자세한 내용과 이벤트 로그에서 찾습니다. 이벤트 메시지는 어떤 소프트웨어 프로그램으로 설정 된 나타냅니다 **허용 안 함** 어떤 규칙 프로그램에 적용 됩니다.

### <a name="modified-software-restriction-policies-are-not-taking-effect"></a>수정 된 소프트웨어 제한 정책을 적용을 사용 하지 않는
**원인:** 그룹 정책을 통해 도메인에 지정 된 소프트웨어 제한 정책이 로컬 구성 되어 있는 한 정책 설정을 재정의 합니다. 이 정책 설정을 재정의 도메인에서 정책 설정의 임을 의미 될 수 있습니다.

**원인:** 그룹 정책 정책 설정을 새로 되지 않을 수 있습니다. 그룹 정책을 적용 됩니다 변경 정책 설정에 주기적으로; 따라서 디렉터리에 수행 된 정책 변경 아직 새로 하지 있을 가능성이입니다.

**해결 방법**

1.  네트워크에 대 한 제한 정책을 소프트웨어를 수정 하는 컴퓨터가 도메인 컨트롤러에 연결할 수 있어야 합니다. 컴퓨터가 도메인 컨트롤러에 연결할 수 있는지 확인 합니다.

2.  네트워크에서 로그인 한 후는 네트워크에 다시 여 정책을 새로 고칩니다. 그룹 정책을 통해 어떤 정책이 적용 되는 경우 다시 로그인 고쳐집니다 정책을입니다.

3.  정책 설정을 명령줄 유틸리티 gpupdate 또는에서 로그 오프 한 다음 컴퓨터가 다시 로그온 복구할 수 있습니다. 최상의 결과 gpupdate을 실행 하 고에서 로그 오프 한 다음 컴퓨터가 다시 로그온 합니다. 일반적으로 워크스테이션 나 서버에서 90 분 마다 및 5 분 마다 도메인 컨트롤러에 보안 설정은 고쳐집니다. 설정은 변경 내용이 여부 16 시간 마다 옵션도 있습니다. 이들은 설정을 구성할 수 있으므로 새로 고침 간격으로 각 도메인에 있는 다른 될 수 있습니다.

4.  검사는 정책이 적용 됩니다. 도메인에 대 한 수준 정책을 확인 **무시 안** 설정 합니다.

5.  그룹 정책을 통해 도메인에 지정 된 소프트웨어 제한 정책이 로컬 구성 되어 있는 모든 정책을 보다 우선 합니다. Gpresult 명령줄 도구를 사용 하 여 정책 효과가 인지 확인 합니다. 이 수 로컬 설정을 재정의 도메인 정책 임을 의미 합니다.

6.  정책 설정을 소매가 및 AppLocker 같은 GPO 인 AppLocker 설정 우선 Windows 7, Windows Server 2008 R2 이상 합니다. 다른 Gpo의 소매가 및 AppLocker 정책 설정을 저장 하는 것이 좋습니다.

### <a name="after-adding-a-rule-through-srp-you-cannot-log-on-to-your-computer"></a>소매가 통해 규칙을 추가한 후 수 없는에 로그온 할 컴퓨터
**원인:** 시작 되 면 컴퓨터 많은 프로그램 및 파일 액세스 합니다. 실수로 페이지 설정 이러한 프로그램 또는 파일을 **허용 안 함**합니다. 컴퓨터의 프로그램 또는 파일에 액세스할 수 없는 때문에 제대로 시작할 수 없습니다.

**해결 방법:** 안전 모드로 컴퓨터 시작, 로컬 관리자로 로그온 한 다음 프로그램 또는 파일을 실행할 수 있도록 제한 정책을 소프트웨어를 변경 합니다.

### <a name="a-new-policy-setting-is-not-applying-to-a-specific-file-name-extension"></a>특정 파일 이름 확장명에 새 정책 설정을 적용 되지 않습니다.
**원인:** 파일 이름 확장명은 지원 되는 파일 형식 목록에 없습니다.

**해결 방법:** 파일 이름 확장명 소매가에서 지원 되는 파일 형식 목록에 추가 합니다.

소프트웨어 제한 정책을 규제 코드 알 수 없거나 신뢰할 수 없는 문제를 해결 합니다. 소프트웨어 제한 소프트웨어를 식별 하 고 사이트나 도메인 OU에서 로컬 컴퓨터에서 실행 하는 기능을 제어 보안 설정이 정책과 GPO를 통해 구현할 수 있습니다.

### <a name="a-default-rule-is-not-restricting-as-expected"></a>기본 규칙 예상 대로 제한 됩니다.
**원인:** 특정 규칙 재정의 기본 규칙 발생할 수 있는 특정 주문에 적용 되는 규칙 합니다. 소매가 (가장 관련 일반) 다음 순서 대로 규칙 적용 됩니다.

1.  Hash 규칙

2.  인증서 규칙

3.  경로 규칙

4.  인터넷 시간대 규칙

5.  기본 규칙

**해결 방법:** 응용 프로그램 제한 규칙 평가 하 고, 해당 되는 경우 기본 규칙 제외 하 고 모두 제거 합니다.

### <a name="unable-to-discover-which-restrictions-are-applied"></a>어떤 제한이 적용 되는 검색 수 없습니다.
**원인:** 예기치 않은 동작에 대 한 명확 원인인 및 새로 고침 GPO 문제가 해결 되지 않는 추가 조사 있으므로 필요 합니다.

**해결 방법**

1.  Investigate the System Event Log, filtering on source of "Software Restriction Policy." 항목 규칙 각 응용 프로그램에 대해 구현 명시적으로 합니다.

2.  고급 로깅 사용. 참조 [결정 허용 거부 목록 및 응용 프로그램 재고 제한 정책 소프트웨어에 대 한](software-restriction-policies.md) 에 대 한 자세한 내용은 합니다.


