---
ms.assetid: 155abe09-6360-4913-8dd9-7392d71ea4e6
title: 문제 해결을 위한 컴퓨터 구성
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 8e11883de9f89d0b95ed0fc35b4f5f3941ef82a3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71368901"
---
# <a name="configuring-a-computer-for-troubleshooting"></a>문제 해결을 위한 컴퓨터 구성

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

고급 문제 해결 기술을 사용 하 여 Active Directory 문제를 식별 하 고 해결 하기 전에 문제 해결을 위해 컴퓨터를 구성 합니다. 또한 개념, 절차 및 도구 문제 해결에 대 한 기본적인 지식이 있어야 합니다.

Windows Server 용 모니터링 도구에 대 한 자세한 내용은 [Windows server의 성능 및 안정성 모니터링](https://go.microsoft.com/fwlink/?LinkId=123737) 에 대 한 단계별 가이드를 참조 하세요.

## <a name="configuration-tasks-for-troubleshooting"></a>문제 해결을 위한 구성 작업

Active Directory Domain Services (AD DS) 문제 해결을 위해 컴퓨터를 구성 하려면 다음 작업을 수행 합니다.

### <a name="install-remote-server-administration-tools-for-ad-ds"></a>AD DS에 대 한 원격 서버 관리 도구 설치

AD DS를 설치 하 여 도메인 컨트롤러를 만들 때 AD DS를 관리 하는 데 사용 하는 관리 도구가 자동으로 설치 됩니다. 도메인 컨트롤러가 아닌 컴퓨터에서 도메인 컨트롤러를 원격으로 관리 하려면 지원 되는 Windows 버전을 실행 하는 워크스테이션 또는 구성원 서버에 원격 서버 관리 도구 (RSAT)를 설치 하면 됩니다. RSAT는 windows Server 2003에서 Windows 지원 도구를 대체 합니다.

RSAT를 설치 하는 방법에 대 한 자세한 내용은 [원격 서버 관리 도구](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)문서를 참조 하세요.

### <a name="configure-reliability-and-performance-monitor"></a>안정성 및 성능 모니터 구성

Windows Server에는 성능 로그 및 경고, Server Performance Advisor를 비롯 하 여 이전 독립 실행형 도구의 기능을 결합 한 MMC (Microsoft Management Console) 스냅인 인 Windows 안정성 및 성능 모니터가 포함 되어 있습니다. 및 시스템 모니터. 이 스냅인은 데이터 수집기 집합과 이벤트 추적 세션을 사용자 지정 하는 GUI (그래픽 사용자 인터페이스)를 제공 합니다.

안정성 및 성능 모니터에는 시스템의 변경 내용을 추적 하 고 시스템 안정성의 변경과 비교 하 여 해당 관계에 대 한 그래픽 보기를 제공 하는 MMC 스냅인 인 안정성 모니터도 포함 됩니다.

### <a name="set-logging-levels"></a>로깅 수준 설정

이벤트 뷰어 디렉터리 서비스 로그에서 수신 하는 정보가 문제를 해결 하기에 충분 하지 않은 경우 HKEY_LOCAL_의 적절 한 레지스트리 항목을 사용 하 여 로깅 수준을 올립니다.  **MACHINESYSTEMCurrentControlSetServicesNTDSDiagnostics**.

기본적으로 모든 항목에 대 한 로깅 수준은 **0**으로 설정 되며, 최소 정보를 제공 합니다. 가장 높은 로깅 수준은 **5**입니다. 항목에 대 한 수준을 높이면 디렉터리 서비스 이벤트 로그에 추가 이벤트가 기록 됩니다.

진단 항목에 대 한 로깅 수준을 변경 하려면 다음 절차를 따르십시오. **Domain Admins**의 구성원이거나 이에 준하는 자격이 있어야 이 절차를 완료할 수 있습니다.

> [!WARNING]
> 다른 대안이 없는 경우가 아니면 레지스트리를 직접 편집하지 않는 것이 좋습니다. 레지스트리를 수정 하지 전에 유효성을 검사 나 Windows 레지스트리 편집기에서 적용 되 고 결과적으로, 잘못 된 값을 저장할 수 있습니다. 이 시스템에 복구할 수 없는 오류가 발생할 수 있습니다. 가능 하면 레지스트리를 직접 편집 하는 대신 그룹 정책 또는 다른 Windows 도구 (예: MMC 스냅인)를 사용 하 여 작업을 수행 합니다. 레지스트리를 편집해야 하는 경우 각별히 주의하세요.
>

진단 항목에 대 한 로깅 수준을 변경 하려면

1. **시작** > **실행** > 클릭 하 > **Regedit** 를 입력 하 고 **확인을**클릭 합니다.
2. 로그인을 설정 하려는 항목으로 이동 합니다.
   * 예: HKEY_LOCAL_MACHINESYSTEMCurrentControlSetServicesNTDSDiagnostics
3. 항목을 두 번 클릭 하 고 **기준**에서 **10 진수**를 클릭 합니다.
4. **값**에 **0** 에서 **5**사이의 정수를 입력 한 다음 **확인**을 클릭 합니다.
