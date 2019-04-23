---
ms.assetid: 155abe09-6360-4913-8dd9-7392d71ea4e6
title: 문제 해결을 위한 컴퓨터 구성
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1acb5f7d309d58ed4a5a3aca6bb89f01c0cbf933
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854124"
---
# <a name="configuring-a-computer-for-troubleshooting"></a>문제 해결을 위한 컴퓨터 구성

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

고급 문제 해결 기술을 식별 하 고 Active Directory 문제 해결을 사용 하기 전에 문제 해결을 위해 컴퓨터를 구성 합니다. 또한 개념, 절차 및 도구 문제 해결에 대 한 기본적인 지식이 있어야 합니다.

Windows Server에 대 한 모니터링 도구에 대 한 내용은 대 한 단계별 지침을 참조 하세요. [의 성능 및 안정성 모니터링 Windows Server](https://go.microsoft.com/fwlink/?LinkId=123737)

## <a name="configuration-tasks-for-troubleshooting"></a>문제 해결에 대 한 구성 작업

Active Directory Domain Services (AD DS) 문제 해결을 위해 컴퓨터를 구성 하려면 다음 작업을 수행 합니다.

### <a name="install-remote-server-administration-tools-for-ad-ds"></a>AD DS 용 원격 서버 관리 도구 설치

도메인 컨트롤러를 만들려면 AD DS를 설치할 때 AD DS 관리를 사용 하는 관리 도구는 자동으로 설치 됩니다. 도메인 컨트롤러가 아닌 컴퓨터에서 도메인 컨트롤러를 원격으로 관리 하려는 경우에 구성원 서버 또는 워크스테이션 지원 되는 Windows 버전을 실행 하는 원격 서버 관리 도구 (RSAT)를 설치할 수 있습니다. RSAT는 Windows Server 2003에서 Windows 지원 도구를 대체합니다.

RSAT를 설치 하는 것에 대 한 자세한 문서를 참조 [원격 서버 관리 도구](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)합니다.

### <a name="configure-reliability-and-performance-monitor"></a>안정성 및 성능 모니터 구성

Windows 안정성 및 성능 로그 및 경고, Server Performance Advisor, 등 이전 독립 실행형 도구를의 기능을 결합 하는 Microsoft Management Console (MMC) 스냅인에 성능 모니터를 포함 하는 Windows Server 및 시스템 모니터입니다. 이 스냅인에서 데이터 수집기 집합 및 이벤트 추적 세션을 사용자 지정 하기 위한 그래픽 사용자 인터페이스 (GUI)를 제공 합니다.

안정성 및 성능 모니터 안정성 모니터 시스템의 변경 내용을 추적 및 시스템 안정성에 변경 내용을 비교 하는 MMC 스냅인 관계의 그래픽 뷰가 제공 포함 됩니다.

### <a name="set-logging-levels"></a>로깅 수준 설정

이벤트 뷰어에서 디렉터리 서비스 로그에서 수신 하는 정보를 문제 해결을 위해 충분 하지 않으면 적절 한 레지스트리 항목을 사용 하 여 로깅 수준을 발생 **HKEY_LOCAL_ MACHINESYSTEMCurrentControlSetServicesNTDSDiagnostics**합니다.

기본적으로 모든 항목에 대 한 로깅 수준 설정이 **0**, 최소한의 정보만 제공 합니다. 가장 높은 로깅 수준이 **5**합니다. 디렉터리 서비스 이벤트 로그에 기록할 이벤트를 추가 하면 항목에 대 한 수준을 증가 합니다.

진단 항목에 대 한 로깅 수준을 변경 하려면 다음 절차를 따르십시오. **Domain Admins**의 구성원이거나 이에 준하는 자격이 있어야 이 절차를 완료할 수 있습니다.

> [!WARNING]
> 다른 대안이 없는 경우가 아니면 레지스트리를 직접 편집하지 않는 것이 좋습니다. 레지스트리를 수정 하지 전에 유효성을 검사 나 Windows 레지스트리 편집기에서 적용 되 고 결과적으로, 잘못 된 값을 저장할 수 있습니다. 이 시스템에 복구할 수 없는 오류가 발생할 수 있습니다. 가능 하면 레지스트리를 직접 편집 하는 것이 아니라 작업을 수행 하려면 그룹 정책 또는 MMC 스냅인과 같이 다른 Windows 도구를 사용 합니다. 레지스트리를 편집해야 하는 경우 각별히 주의하세요.
>

진단 항목에 대 한 로깅 수준을 변경 하려면

1. 클릭 **시작** > **실행** > 형식 **regedit** > 클릭 **확인**합니다.
2. 로그인을 설정 하려면 원하는 항목으로 이동 합니다.
   * 예: HKEY_LOCAL_MACHINESYSTEMCurrentControlSetServicesNTDSDiagnostics
3. 항목을 두 번 클릭 하 고 **자료**, 클릭 **10 진수**합니다.
4. **값**에서 정수를 입력 **0** 를 통해 **5**를 클릭 하 고 **확인**합니다.
