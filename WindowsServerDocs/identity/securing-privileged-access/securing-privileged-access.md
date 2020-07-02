---
title: 권한 있는 액세스 보안
description: 권한 있는 액세스를 보호하는 단계별 방법
ms.prod: windows-server
ms.topic: conceptual
ms.assetid: f5dec0c2-06fe-4c91-9bdc-67cc6a3ede60
ms.date: 02/25/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: mas
ms.openlocfilehash: 806a2aced95421bd469ba885d4a81c219ae1b651
ms.sourcegitcommit: 457e88e5aa6be13a2bffdb8e434a8efc3698678f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548837"
---
# <a name="securing-privileged-access"></a>권한 있는 액세스 보안

>적용 대상: Windows Server

권한 있는 액세스 보안은 오늘날의 조직에서 비즈니스 자산에 대한 보안 보증을 설정하는 중요한 첫 단계입니다. IT 조직이 보유한 대부분의 또는 모든 비즈니스 자산에 대한 보안은 자산의 관리 및 개발에 사용되는 권한 있는 계정의 무결성에 따라 달라집니다. 사이버 공격자는 종종 이러한 계정 및 기타 권한 있는 액세스 요소를 목표로 삼아 [Pass-the-Hash 및 Pass-the-Ticket](https://www.microsoft.com/pth)과 같은 자격 증명 도난 공격을 사용하여 데이터 및 시스템에 대한 액세스 권한을 탈취합니다.

확인된 악의적 사용자로부터 권한 있는 액세스를 보호하려면 이러한 시스템을 위험으로부터 격리하기 위한 완전하고 신중한 접근 방식을 취해야 합니다.

## <a name="what-are-privileged-accounts"></a>권한 있는 계정이란?

권한 있는 계정을 보호하는 방법을 설명하기 전에, 권한 있는 계정이 무엇인지 정의하겠습니다.

Active Directory Domain Services 관리자와 같은 권한 있는 계정은 IT 조직이 보유한 대부분의 또는 모든 자산에 직접 또는 간접적으로 액세스할 수 있으므로, 이러한 계정이 노출되면 엄청난 비즈니스 위험이 발생합니다.

## <a name="why-securing-privileged-access-is-important"></a>권한 있는 액세스를 보호해야 하는 이유

사이버 공격자는 조직의 모든 대상 데이터에 대한 액세스 권한을 신속하게 얻기 위해 AD(Active Directory) 같은 시스템에 대한 권한 있는 액세스를 집중 공격합니다. 기존의 보안 접근 방식에서는 네트워크 및 방화벽을 주요 보안 경계로 사용하는 데 중점을 두었지만, 다음 두 가지 추세로 인해 네트워크 보안 효과가 크게 감소했습니다.

* 조직에서는 모바일 엔터프라이즈 PC, 휴대폰 및 태블릿과 같은 디바이스, 클라우드 서비스 및 BYOD 디바이스에서 기존 네트워크 경계 외부의 데이터 및 리소스를 호스트합니다.
* 악의적 사용자는 피싱 및 기타 웹 및 전자 메일 공격을 통해 네트워크 경계 내의 워크스테이션에 대한 액세스 권한을 지속적으로 획득할 수 있는 능력을 보여 주었습니다.

이러한 이유로 기존의 네트워크 경계 전략 외에도 인증 및 권한 부여 ID 제어를 기반으로 최신 보안 경계를 구축해야 합니다. 여기서 보안 경계는 자산과 자산에 대한 위협 사이의 일관적인 컨트롤 세트로 정의됩니다. 권한 있는 계정은 이 새로운 보안 경계를 제어하는 데 효과적이므로 권한 있는 액세스를 보호하는 데 있어서 매우 중요합니다.

![조직의 ID 계층을 보여 주는 다이어그램](../media/securing-privileged-access/PAW_LP_Fig2.JPG)

관리 계정에 대한 제어권을 탈취한 공격자는 아래와 같이 탈취한 권한을 사용하여 대상 조직에 미치는 영향력을 높일 수 있습니다.

![관리 계정에 대한 제어 권한이 있는 악의적 사용자가 이러한 권한을 사용하여 대상 조직의 비용으로 어떻게 이득을 추구할 수 있는지 보여 주는 다이어그램](../media/securing-privileged-access/PAW_LP_Fig3.JPG)

아래 그림은 다음 두 가지 경로를 보여줍니다.

* 표준 사용자 계정을 사용하여 이메일 같은 리소스에 권한 없이 액세스하고, 웹 검색 및 일상적인 작업이 완료되는 "파란색" 경로

   > [!NOTE]
   > 뒷부분에서 설명하는 파란색 경로 항목은 관리 계정 범위를 넘어서 확장되는 광범위한 환경 보호를 나타냅니다.

* 피싱과 기타 웹 및 이메일 공격의 위험을 줄이기 위해 강화된 디바이스에서 권한 있는 액세스가 발생하는 "빨간색" 경로

![웹 검색 및 이메일 액세스와 같은 높은 위험의 표준 사용자 작업으로부터 권한 있는 액세스 작업을 격리하기 위해 로드맵에서 설정하는 별도의 관리 "경로"를 보여주는 다이어그램](../media/securing-privileged-access/PAW_LP_Fig4.JPG)

## <a name="securing-privileged-access-roadmap"></a>권한 있는 액세스 보안 로드맵

이 로드맵은 이미 배포된 Microsoft 기술의 사용을 극대화하고, 클라우드 기술을 활용하여 보안을 강화하고, 이미 배포된 타사 보안 도구를 통합하기 위해 설계되었습니다.

Microsoft 권장 로드맵은 다음과 같은 3단계로 구성됩니다.

* [1단계: 처음 30일](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/securing-privileged-access#phase-1-quick-wins-with-minimal-operational-complexity)
   * 의미 있는 긍정적인 효과를 통해 빠르게 성공
* [2단계: 90일](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/securing-privileged-access#phase-2-significant-incremental-improvements)
   * 대폭 향상
* [3단계: 지속](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/securing-privileged-access#phase-3-security-improvement-and-sustainment)
   * 보안 향상 및 지속

로드맵은 이러한 공격 및 솔루션 구현에 대한 Microsoft의 경험을 바탕으로 가장 효과적이고 신속한 구현부터 우선적으로 수행하도록 지정되었습니다. 

이 로드맵에 따라 확인된 악의적 사용자로부터 권한 있는 액세스의 보안을 유지하는 것이 좋습니다. 조직의 기존 기능 및 특정 요구 사항을 수용하도록 이 로드맵을 조정할 수 있습니다.

> [!NOTE]
> 권한 있는 액세스 보안에는 기술적 구성 요소(호스트 방어, 계정 보호, ID 관리 등)뿐만 아니라 프로세스 변경과 관리 방식 및 지식 등 광범위한 요소가 필요합니다. 로드맵의 타임라인은 대략적이며 고객 구현에 대한 Microsoft의 경험을 바탕으로 합니다. 기간은 사용자 환경의 복잡성 및 변경 관리 프로세스에 따라 다릅니다.

## <a name="phase-1-quick-wins-with-minimal-operational-complexity"></a>1단계: 운영 복잡성을 최소화하면서 빠르게 성공

로드맵의 1단계는 가장 자주 사용되는 자격 증명 도난 및 남용 공격 기술의 위험을 신속하게 완화하는 데 중점을 둡니다. 1단계는 다음 다이어그램에 설명된 것처럼 약 30일 동안 구현되도록 설계되었습니다.

![1단계 다이어그램: 1. 관리자 계정과 사용자 계정의 분리 2. Just-in-time 로컬 관리자 암호 3. 관리 워크스테이션 스테이지 1 4. ID 공격 탐지](../media/securing-privileged-access/PAW_LP_Fig6.JPG)

### <a name="1-separate-accounts"></a>1. 개별 분리

권한 있는 액세스 계정으로부터 인터넷 위험(피싱 공격, 웹 검색)을 분리하기 위해, 권한 있는 액세스가 가능한 모든 직원의 전용 계정을 만듭니다. 관리자는 높은 권한이 있는 계정을 사용하여 웹을 탐색하거나, 이메일을 확인하거나, 일상적인 생산성 작업을 수행하면 안 됩니다. 이에 대한 자세한 내용은 참조 문서의 [별도의 관리 계정](securing-privileged-access-reference-material.md#separate-administrative-accounts) 섹션에서 찾을 수 있습니다.

온-프레미스 AD 및 Azure AD 환경에서 관리자 권한을 영구적으로 할당하여 두 개 이상의 응급 액세스 계정을 만들려면 [Azure AD에서 응급 액세스 계정 관리](/azure/active-directory/users-groups-roles/directory-emergency-access) 문서의 지침을 따르세요. 이러한 계정은 재해가 발생한 경우처럼 기존 관리자 계정이 필수 작업을 수행할 수 없는 경우에만 사용됩니다.

### <a name="2-just-in-time-local-admin-passwords"></a>2. Just-in-time 로컬 관리자 암호

공격자가 로컬 SAM 데이터베이스에서 로컬 관리자 계정 암호 해시를 훔쳐서 다른 컴퓨터를 공격하는 데 사용하는 위험을 완화하기 위해, 조직에서는 모든 머신에 고유한 로컬 관리자 암호가 있는지 확인해야 합니다. LAPS(로컬 관리자 암호 솔루션) 도구는 각 워크스테이션과 서버에서 고유한 임의의 암호를 구성하여 ACL로 보호되는 AD(Active Directory)에 저장할 수 있습니다. 권한 있는 적격 사용자만이 이러한 로컬 관리자 계정 암호를 읽거나 재설정을 요청할 수 있습니다. 워크스테이션 및 서버에 사용할 LAPS는 [Microsoft 다운로드 센터](https://aka.ms/LAPS)에서 받을 수 있습니다.

LAPS 및 PAW를 사용하여 환경을 운영하는 방법에 대한 추가 지침은 [클린 소스 원칙을 기반으로 하는 운영 표준](securing-privileged-access-reference-material.md#operational-standards-based-on-clean-source-principle) 섹션에서 찾을 수 있습니다.

### <a name="3-administrative-workstations"></a>3. 관리 워크스테이션

Azure Active Directory 및 기존 온-프레미스 Active Directory 관리 권한이 있는 사용자에 대한 초기 보안 조치로, 이들이 [안전한 Windows 10 디바이스를 위한 표준](/windows-hardware/design/device-experiences/oem-highly-secure)에 따라 구성된 Windows 10 디바이스를 사용하도록 해야 합니다. 권한 있는 관리자 계정은 관리 워크스테이션의 로컬 관리자 그룹 구성원이 아니어야 합니다.  워크스테이션 구성을 변경해야 하는 경우 UAC(사용자 액세스 제어)를 통한 권한 상승을 활용할 수 있습니다.  또한 Windows 10 보안 기준을 워크스테이션에 적용하여 디바이스 보안을 강화해야 합니다.

### <a name="4-identity-attack-detection"></a>4. ID 공격 탐지

[Azure ATP(Azure Advanced Threat Protection)](/azure-advanced-threat-protection/what-is-atp)는 온-프레미스 Active Directory 환경을 노리는 지능형 위협, 손상된 ID 및 악의적인 내부자 작업을 식별, 탐지, 조사하도록 도와주는 클라우드 기반 보안 솔루션입니다.

## <a name="phase-2-significant-incremental-improvements"></a>2단계: 대폭 향상

2단계는 1단계에서 수행한 작업을 기반으로 하며, 약 90일 동안 완료하도록 설계되었습니다. 이 단계는 다음 다이어그램에 나와 있습니다.

![2단계 다이어그램: 1. 비즈니스용 Windows Hello/MFA 2. PAW 롤아웃 3. Just-in-time 권한 4. Credential Guard 5. 유출된 자격 증명 6. 횡이동 취약성 탐지](../media/securing-privileged-access/PAW_LP_Fig7.JPG)

### <a name="1-require-windows-hello-for-business-and-mfa"></a>1. 비즈니스용 Windows Hello 및 MFA 필요

관리자는 비즈니스용 Windows Hello와 관련된 사용 편의성을 활용할 수 있습니다. 관리자는 자신의 PC에서 복잡한 암호를 강력한 2단계 인증으로 바꿀 수 있습니다. 공격자는 디바이스와 생체 인식 정보나 PIN을 모두 확보해야 하므로, 직원 모르게 액세스하는 것이 훨씬 더 어렵습니다. 비즈니스용 Windows Hello 및 롤아웃 경로에 대한 자세한 내용은 [비즈니스용 Windows Hello 개요](/windows/security/identity-protection/hello-for-business/hello-overview) 문서에서 찾을 수 있습니다.

Azure AD에서 Azure MFA를 사용하여 관리자 계정에 MFA(다단계 인증)를 사용하도록 설정합니다. 적어도 [기준 보호 조건부 액세스 정책](/azure/active-directory/conditional-access/baseline-protection#require-mfa-for-admins)을 사용하도록 설정해야 합니다. Azure Multi-Factor Authentication에 대한 자세한 내용은 [클라우드 기반 Azure Multi-Factor Authentication 배포](/azure/active-directory/authentication/howto-mfa-getstarted) 문서에서 확인할 수 있습니다.

### <a name="2-deploy-paw-to-all-privileged-identity-access-account-holders"></a>2. 모든 권한 있는 ID 액세스 계정 소유자에게 PAW 배포

권한 있는 계정을 이메일, 웹 검색 및 기타 비 관리 작업에서 발견된 위협으로부터 분리하는 프로세스를 계속 진행하려면 조직의 정보 시스템에 대한 권한 있는 액세스가 가능한 모든 직원의 전용 PAW(Privileged Access Workstation)를 구현해야 합니다. PAW 배포에 대한 추가 지침은 [Privileged Access Workstation](privileged-access-workstations.md#paw-phased-implementation) 문서에서 찾을 수 있습니다.

### <a name="3-just-in-time-privileges"></a>3. Just-in-time 권한

권한 노출 시간을 줄이고 권한 사용에 대한 가시성을 높이기 위해, 아래의 적절한 솔루션 또는 타사 솔루션을 사용하여 적시에(JIT) 권한을 제공합니다.

* AD DS(Active Directory 도메인 서비스)의 경우 MIM(Microsoft Identity Manager)의 [PAM(Privileged Access Manager)](/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) 기능을 사용합니다.
* Azure Active Directory의 경우 [Azure AD PIM(Privileged Identity Management)](/azure/active-directory/privileged-identity-management/pim-deployment-plan) 기능을 사용합니다.

### <a name="4-enable-windows-defender-credential-guard"></a>4. Windows Defender Credential Guard 사용

Credential Guard를 사용하면 NTLM 암호 해시, Kerberos 허용 티켓 및 애플리케이션에 도메인 자격 증명으로 저장된 자격 증명을 보호할 수 있습니다. 이 기능은 훔친 자격 증명으로 환경에서 피벗하기 어렵게 만들어서 Pass-the-Hash 또는 Pass-The-Ticket 같은 자격 증명 도난 공격을 방지할 수 있습니다. Credential Guard의 작동 원리 및 배포 방법에 대한 자세한 내용은 [Windows Defender Credential Guard를 사용하여 파생된 도메인 자격 증명 보호](/windows/security/identity-protection/credential-guard/credential-guard) 문서에서 찾을 수 있습니다.

### <a name="5-leaked-credentials-reporting"></a>5. 유출된 자격 증명 보고

"Microsoft는 새로운 위협을 식별하고 고객을 보호하기 위해 매일 6.5조 개의 신호를 분석합니다." - [Microsoft By the Numbers](https://news.microsoft.com/bythenumbers/cyber-attacks)

손실된 자격 증명을 수정할 수 있도록, Microsoft Azure AD ID 보호를 사용하도록 설정하여 자격 증명이 손실된 사용자를 보고합니다. [Azure AD ID 보호](/azure/active-directory/identity-protection/index)를 활용하면 조직에서는 클라우드 및 하이브리드 환경을 위협으로부터 보호할 수 있습니다.

### <a name="6-azure-atp-lateral-movement-paths"></a>6. Azure ATP 횡적 이동 경로

권한 없는 손상된 계정이 Pass-the-Hash 또는 Pass-The-Ticket 같은 자격 증명 도난 공격을 통해 권한 있는 계정에 대한 액세스 권한을 얻을 수 없도록, 권한 있는 액세스 계정 소유자가 자신의 PAW를 관리 용도로만 사용하게 합니다. [Azure ATP LMP(횡적 이동 경로)](/azure-advanced-threat-protection/use-case-lateral-movement-path)는 권한 있는 계정이 손상될 가능성이 있는 위치를 파악할 수 있는 알기 쉬운 보고서를 제공합니다.

## <a name="phase-3-security-improvement-and-sustainment"></a>3단계: 보안 향상 및 지속

로드맵의 3단계는 1단계 및 2단계에서 수행된 단계를 기반으로 보안 태세를 강화합니다. 3단계는 다음 다이어그램에 시각적으로 설명되어 있습니다.

![3단계: 1. RBAC 검토 2. 공격 노출 영역 축소 3. SEIM과 로그 통합 4. 유출된 자격 증명 자동화](../media/securing-privileged-access/PAW_LP_Fig8.JPG)

이러한 기능은 이전 단계의 작업을 기반으로 하며 보다 사전 예방적인 방어 태세로 전환합니다. 이 단계에는 구체적인 타임라인이 없으며 조직에 따라 구현 시간이 오래 걸릴 수 있습니다.

### <a name="1-review-role-based-access-control"></a>1. 역할 기반 액세스 제어 검토

[Active Directory 관리 계층 모델](securing-privileged-access-reference-material.md) 문서에 설명된 3계층 모델을 사용하여 하위 계층 관리자가 상위 계층 리소스에 대한 관리 액세스 권한(그룹 구성원, 사용자 계정에 대한 ACL 등)을 갖는 일이 없도록 검토 및 확인합니다.

### <a name="2-reduce-attack-surfaces"></a>2. 공격 노출 영역 축소

도메인, 도메인 컨트롤러, ADFS 및 Azure AD Connect를 비롯한 ID 워크로드 보안을 강화합니다. 이러한 시스템 중 하나가 손상되면 조직의 다른 시스템도 손상될 수 있습니다. [Active Directory 공격에 대한 취약성 줄이기](../ad-ds/plan/security-best-practices/reducing-the-active-directory-attack-surface.md) 및 [ID 인프라를 보호하기 위한 5단계](/azure/security/azure-ad-secure-steps) 문서에서는 온-프레미스 및 하이브리드 ID 환경을 보호하는 방법에 대한 지침을 제공합니다.

### <a name="3-integrate-logs-with-siem"></a>3. SIEM과 로그 통합

중앙의 SIEM 도구에 로깅을 통합하면 조직에서 보안 이벤트를 분석, 탐지 및 대응하는 데 도움이 됩니다. [손상 징후에 대한 Active Directory 모니터링](../ad-ds/plan/security-best-practices/monitoring-active-directory-for-signs-of-compromise.md) 및 [부록 L: 모니터링할 이벤트](../ad-ds/plan/appendix-l--events-to-monitor.md) 문서에서는 환경에서 모니터링해야 하는 이벤트에 대한 지침을 제공합니다.

기본 경고가 제공되는 30일 플랜의 Azure ATP와는 다르게 SIEM(보안 정보 및 이벤트 관리)에서 경고를 집계, 생성 및 조정하려면 숙련된 분석가가 필요하기 때문에 이 부분은 플랜의 범위를 벗어납니다.

### <a name="4-leaked-credentials---force-password-reset"></a>4. 유출된 자격 증명 - 강제 암호 재설정

암호가 손상된 것으로 의심되면 자동으로 암호 재설정을 강제하도록 Azure AD ID 보호를 설정하여 보안 태세를 계속 강화합니다. [위험 이벤트를 사용하여 Multi-Factor Authentication 및 암호 변경 트리거](/azure/active-directory/authentication/tutorial-risk-based-sspr-mfa) 문서의 지침에서는 조건부 액세스 정책을 사용하여 강제 암호 재설정을 사용하는 방법을 설명합니다.

## <a name="am-i-done"></a>작업 완료

결론만 말하면 그렇지 않습니다.

나쁜 사람들은 결코 멈추지 않으므로, 여러분도 멈추면 안 됩니다. 공격자들은 지속적으로 진화하고 변화하고 있으며, 이 로드맵은 조직에서 현재 알려진 위협을 방어하는 데 도움이 될 것입니다. 보안이란 사용자 환경을 목표로 삼는 악의적 사용자의 비용을 증가시키고 공격 성공률을 낮추는 데 집중하는 지속적인 프로세스라고 생각하셔야 합니다.

조직의 보안 프로그램에는 권한 있는 액세스 보호 외에도 여러 가지가 더 있겠지만, 권한 있는 액세스 보호는 보안 전략의 중요한 구성 요소입니다.
