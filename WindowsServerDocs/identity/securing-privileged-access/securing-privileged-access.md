---
title: 권한 있는 액세스 보안
description: 권한 있는 액세스 보안 유지를 위한 단계적된 접근
ms.prod: windows-server-threshold
ms.topic: conceptual
ms.assetid: f5dec0c2-06fe-4c91-9bdc-67cc6a3ede60
ms.date: 02/25/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: mas
ms.openlocfilehash: 0d54a94d51a4d1e0a1d28f78ec39bf16bc3d9100
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822014"
---
# <a name="securing-privileged-access"></a>권한 있는 액세스 보안

>적용 대상: Windows Server

권한 있는 액세스 보안은 오늘날의 조직에서 비즈니스 자산에 대한 보안 보증을 설정하는 중요한 첫 단계입니다. IT 조직에서 대부분 또는 모든 비즈니스 자산의 보안을 관리, 관리 및 개발 하는 데 사용 하는 권한 있는 계정의 무결성에 따라 달라 집니다. 사이버 공격자는 종종 이러한 계정 및 다른 요소의 데이터와 같은 자격 증명 도난 공격을 사용 하 여 시스템에 액세스할 수 있는 권한 있는 액세스 대상 [-Pass-the-hash 및 통과-티켓](https://www.microsoft.com/pth)합니다.

확인된 된 악의적 사용자 로부터 권한 있는 액세스를 보호 하려면 이러한 시스템을 위험 으로부터 격리를 완전 하 고 신중한 접근 해야 합니다.

## <a name="what-are-privileged-accounts"></a>권한 있는 계정 이란?

보안을 유지 하는 방법에 대 한 이야기 하기 전에 권한 있는 계정을 정의할 수 있습니다.

Active Directory Domain Services의 관리자와 같은 권한 있는 계정에 있는 IT 조직에서 중요 한 비즈니스 위험을 이러한 계정 손상 하기 대부분 또는 모든 자산에 대 한 직접 또는 간접 액세스 합니다.

## <a name="why-securing-privileged-access-is-important"></a>권한 있는 액세스 보안 중요 한 이유는?

Active Directory (AD) 신속 하 게 액세스 하는 조직의 모든 대상 데이터와 같은 시스템에 대 한 권한 있는 액세스에 사이버 공격자 집중 합니다. 기본 보안 경계로 서 기존의 보안 접근 방식은 네트워크 및 방화벽에 집중 하지만 두 가지 추세로 인해 네트워크 보안의 효과 크게 감소 했습니다.

* 조직 데이터를 호스팅하는 하 고 모바일 엔터프라이즈 Pc, 휴대폰 및 태블릿, 같은 장치에서 기존 네트워크 경계 외부 리소스 클라우드 서비스, 사용자 고유의 장치 (BYOD)
* 악의적 사용자는 피싱 및 기타 웹 및 전자 메일 공격을 통해 네트워크 경계 내의 워크스테이션에 대한 액세스 권한을 지속적으로 획득할 수 있는 능력을 보여 주었습니다.

이러한 요소 인증 및 권한 부여에서 최신 보안 경계를 기존의 네트워크 경계 전략 외에도 id 컨트롤을 작성 해야 합니다. 보안 경계를 일관 된 자산을 위협 사이의 컨트롤 집합으로 정의 됩니다. 권한 있는 계정을 효과적으로 제어가 새로운 보안 경계 것이 권한 있는 액세스를 보호 하기 위해 중요 합니다.

![조직의 ID 계층을 보여 주는 다이어그램](../media/securing-privileged-access/PAW_LP_Fig2.JPG)

관리자 계정에 대 한 제어는 공격자는 해당 권한을 사용 하 여 아래와 같이 대상 조직에 해당 효과 더욱 높일 수 있습니다.

![관리 계정에 대한 제어 권한이 있는 악의적 사용자가 이러한 권한을 사용하여 대상 조직의 비용으로 어떻게 이득을 추구할 수 있는지 보여 주는 다이어그램](../media/securing-privileged-access/PAW_LP_Fig3.JPG)

아래 그림에서는 두 개의 경로 보여 줍니다.

* 전자 메일 및 웹 검색 및 일상적인 작업 등의 리소스에 대 한 액세스 권한이 없는 표준 사용자 계정 위치는 "blue" 경로 완료할 수 있습니다.

   > [!NOTE]
   > 파란색 경로 항목을 나중에 설명 된 관리 계정을 이상으로 확장 하는 광범위 한 환경 보호를 나타냅니다.

* 권한 있는 액세스 피싱 및 기타 웹 및 전자 메일 공격 위험을 줄이기 위해 강화 된 장치에서 발생 하는 "red" 경로입니다.

![웹 검색 및 전자 메일 액세스와 같은 높은 위험의 표준 사용자 작업 으로부터 권한 있는 액세스 작업을 격리 하기 로드맵에서 설정 하는 관리에 대 한 별도 "경로" 보여 주는 다이어그램](../media/securing-privileged-access/PAW_LP_Fig4.JPG)

## <a name="securing-privileged-access-roadmap"></a>보안 권한 있는 액세스 로드맵

로드맵의 최대한 활용 하기 위해 이미 배포한 경우 Microsoft 기술 보안을 강화 하 고 모든 타사 보안 도구를 이미 배포 했을 수를 통합 하는 클라우드 기술 활용 하도록 설계 되었습니다.

Microsoft 권장 로드맵은 3 단계로 나뉩니다.

* [1 단계: 처음 30 일]()
   * 의미 있는 긍정적인 영향을 줄을 사용 하 여 빠른 승리 합니다.
* [2 단계: 90 일]()
   * 증분 향상 합니다.
* [3 단계: 진행 중인]()
   * 보안 향상 및 sustainment 합니다.

로드맵은 이러한 공격 및 솔루션 구현에 대한 Microsoft의 경험을 바탕으로 가장 효과적이고 신속한 구현부터 우선적으로 수행하도록 지정되었습니다. 

이 로드맵에 따라 확인된 악의적 사용자로부터 권한 있는 액세스의 보안을 유지하는 것이 좋습니다. 조직의 기존 기능 및 특정 요구 사항을 수용하도록 이 로드맵을 조정할 수 있습니다.

> [!NOTE]
> 권한 있는 액세스 보안에는 기술적 구성 요소(호스트 방어, 계정 보호, ID 관리 등)뿐만 아니라 프로세스 변경과 관리 방식 및 지식 등 광범위한 요소가 필요합니다. 로드맵의 타임라인은 대략적이며 고객 구현에 대한 Microsoft의 경험을 바탕으로 합니다. 기간은 사용자 환경의 복잡성 및 변경 관리 프로세스에 따라 다릅니다.

## <a name="phase-1-quick-wins-with-minimal-operational-complexity"></a>1단계: 최소 운영 복잡성을 사용 하 여 빠른 wins

로드맵의 1 단계는 자격 증명 도난 및 남용 하는 가장 자주 사용 되는 공격 기술을 신속 하 게 완화에 집중 됩니다. 1 단계는 약 30 일에 구현 되도록 설계 되었습니다 및이 다이어그램에 표시 됩니다.

![1 단계 다이어그램: 1. 별도 관리자 및 사용자 계정 2입니다. 시간 로컬 관리자 암호를 3에만 관리 워크스테이션 1, 4 단계입니다. Identity 공격 감지](../media/securing-privileged-access/PAW_LP_Fig6.JPG)

### <a name="1-separate-accounts"></a>1. 별도 계정

인터넷 위험을 분리 하는 데 (피싱 공격, 웹 검색)에서 권한 있는 계정에 액세스, 권한 있는 액세스를 사용 하 여 모든 직원에 대 한 전용된 계정을 만듭니다. 관리자 전자 메일을 확인 하 고 매우 강력한 권한의 계정 사용 하 여 일상적인 생산성 작업을 수행, 웹을 검색 수 해야 합니다. 자세한 내용은이 섹션에서 찾을 수 있습니다 [관리 계정을 분리](securing-privileged-access-reference-material.md#separate-administrative-accounts) 참조 문서입니다.

문서의 지침을 따릅니다 [Azure AD에서 응급 액세스 계정을 관리할](/azure/active-directory/users-groups-roles/directory-emergency-access) 두 개 이상의 응급 액세스 계정을 만들려면를 영구적으로 할당 된 관리자 권한이 모두 온-프레미스에서 AD와 Azure AD 환경 . 이러한 계정은 기존 관리자 계정에서와 같이 이러한 필요한 작업을 수행할 수 없는 경우에 사용 되는 재해의 경우.

### <a name="2-just-in-time-local-admin-passwords"></a>2. 시간 로컬 관리자 암호에만

다른 컴퓨터를 공격 하는 로컬 SAM 데이터베이스에서 로컬 관리자 계정 암호 해시를 도용 하 고이 남용 하 악의적 사용자의 위험을 완화 하려면 조직의 모든 컴퓨터의 고유한 로컬 관리자 암호를 확인 해야 합니다. 로컬 관리자 암호 솔루션 (랩) 도구 각 워크스테이션에서 고유한 임의 암호를 구성할 수 있습니다 하 고 해당 서버에서 Active Directory (AD)는 ACL에 의해 보호를 제공 하는 저장 합니다. 적합 한 권한이 있는 사용자만 읽거나 이러한 로컬 관리자 계정 암호 재설정을 요청할 수 있습니다. 워크스테이션 및 서버에서 사용 하기 위해 LAPS를 가져올 수 있습니다 [Microsoft 다운로드 센터](http://Aka.ms/LAPS)합니다.

LAPS 및 Paw를 사용 하 여 환경을 운영 하기 위한 추가 지침 섹션에서 찾을 수 있습니다 [클린 소스 원칙을 기반으로 운영 표준](securing-privileged-access-reference-material.md#operational-standards-based-on-clean-source-principle)합니다.

### <a name="3-administrative-workstations"></a>3. 관리 워크스테이션

Azure Active Directory와 기존의 온-프레미스 Active Directory에 대 한 관리자 권한이 있는 사용자에 대 한 초기 보안 조치로 사용 하 여 구성 하는 Windows 10 장치를 사용 하는 것을 확인 합니다 [매우 안전한 Windows에 대 한 표준 10 개의 장치](/windows-hardware/design/device-experiences/oem-highly-secure)합니다. 

### <a name="4-identity-attack-detection"></a>4. Identity 공격 감지

[Azure 고급 위협 보호 (ATP)](/azure-advanced-threat-protection/what-is-atp) 하 식별 하 고, 감지 하는 데 도움이 보안 클라우드 기반 솔루션을 조사 고급 위협, 손상 된 id 및 온-프레미스 활성 노린 악의적인 내부자 작업은 디렉터리 환경입니다.

## <a name="phase-2-significant-incremental-improvements"></a>2 단계: 증분 향상

2 단계 1 단계에서 수행 된 작업 기반으로 하 고 90 일 정도에 완료할 수 있도록 설계 되었습니다. 이 단계는 다음 다이어그램에 나와 있습니다.

![2 단계 다이어그램: 1. 비즈니스용 Windows Hello / MFA, 2입니다. PAW 출시를 3입니다. 에 4 시간 권한. Credential Guard 5입니다. 유출 된 자격 증명, 6입니다. 횡 적 이동 취약성 검색](../media/securing-privileged-access/PAW_LP_Fig7.JPG)

### <a name="1-require-windows-hello-for-business-and-mfa"></a>1. Windows Hello 비즈니스에 MFA 필요

관리자는 Windows Hello for Business와 연결 된 사용 편의성에서 이용할 수 있습니다. 관리자 자신의 Pc에서 강력한 2 단계 인증을 사용 하 여 복잡 한 암호를 바꿀 수 있습니다. 공격자는 장치 및 정보 생체 인식 또는 PIN 모두 있어야 합니다., 직원의 지식 없이 액세스 하기가 훨씬 더 어렵습니다. 에 대 한 Windows Hello 비즈니스 및 배포에 대 한 경로 대 한 자세한 내용은 문서에서 찾을 수 있습니다 [Windows Hello 비즈니스 개요](/windows/security/identity-protection/hello-for-business/hello-overview)

Azure MFA를 사용 하 여 Azure AD에서 관리자 계정에 대해 multi-factor authentication (MFA)를 사용 합니다. 최소 사용에는 [초기 보호 조건부 액세스 정책을](/azure/active-directory/conditional-access/baseline-protection#require-mfa-for-admins) 문서에서 Azure Multi-factor Authentication에 대 한 자세한 정보를 찾을 수 있습니다 [Azure Multi-factor Authentication 클라우드 기반 배포](/azure/active-directory/authentication/howto-mfa-getstarted)

### <a name="2-deploy-paw-to-all-privileged-identity-access-account-holders"></a>2. 모든 권한 있는 id 액세스 계정 소유자에 PAW 배포

전자 메일, 웹 검색 및 기타 비 관리 작업에서 발견 한 위협에서 권한 있는 계정을 분리 하는 과정을 계속를 구현 해야 전용된 워크스테이션 PAW (Privileged Access)에 대 한 권한 있는 액세스를 사용 하 여 모든 직원에 대 한 사용자 조직 정보 시스템입니다. PAW 배포 하기 위한 추가 지침 문서에서 찾을 수 있습니다 [Privileged Access Workstation](privileged-access-workstations.md#paw-phased-implementation)합니다.

### <a name="3-just-in-time-privileges"></a>3. 에 시간 권한

용도에 대 한 가시성을 높이고 권한의 노출 시간을 줄이고, just-in-time (JIT) 아래와 같은 적절 한 솔루션 또는 기타 타사 솔루션을 사용 하 여 권한을 제공 합니다.

* AD DS(Active Directory 도메인 서비스)의 경우 MIM(Microsoft Identity Manager)의 [PAM(Privileged Access Manager)](/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) 기능을 사용합니다.
* Azure Active Directory의 경우 [Azure AD PIM(Privileged Identity Management)](/azure/active-directory/privileged-identity-management/pim-deployment-plan) 기능을 사용합니다.

### <a name="4-enable-windows-defender-credential-guard"></a>4. Windows Defender Credential Guard 사용

Credential Guard 사용 하도록 설정 하면 NTLM 암호 해시, Kerberos 티켓 부여 티켓 및 도메인 자격 증명으로 응용 프로그램에서 저장 된 자격 증명을 보호할 수 있습니다. 이 기능은-Pass-the-hash 또는 Pass 티켓 도난된 된 자격 증명을 사용 하 여 환경에서 피벗의 어려움을 늘려 같은 자격 증명 도난 공격을 방지할 수 있습니다. Credential Guard 작동 원리 및 배포 하는 방법에 대 한 정보를 문서에서 찾을 수 있습니다 [보호는 Windows Defender Credential Guard 사용 하 여 도메인 자격 증명 파생](/windows/security/identity-protection/credential-guard/credential-guard)합니다.

### <a name="5-leaked-credentials-reporting"></a>5. 보고 유출 된 자격 증명

"매일 Microsoft 분석 하 여 새로운 위협 요소를 식별 하 고 고객을 보호 하기 위해 6.5 조 개 신호"- [the 숫자에서 Microsoft](https://news.microsoft.com/bythenumbers/cyber-attacks)

이러한 문제를 해결할 수 있습니다 있도록 유출 된 자격 증명을 사용 하 여 사용자에 게 보고 하는 Microsoft Azure AD Id 보호를 사용 하도록 설정 합니다. [Azure AD Id 보호](/azure/active-directory/identity-protection/index) 조직의 클라우드 및 하이브리드 환경을 위협 으로부터 보호 하는 데 활용할 수 있습니다.

### <a name="6-azure-atp-lateral-movement-paths"></a>6. Azure ATP 횡 적 이동 경로

권한 확인 된 손상 된 권한이 없는 계정-Pass-the-hash 통과-티켓 등의 자격 증명 도난 공격을 통해 권한 있는 계정에 액세스할 수 있도록만 소유자 관리에 대 한 해당 PAW 사용 중인 계정에 액세스 합니다. [Azure ATP 횡 적 이동 경로 (LMPs)](/azure-advanced-threat-protection/use-case-lateral-movement-path) 쉽게 권한 있는 계정을 손상 시킬 열려 있을 수 있습니다 위치를 식별 하려면 보고 이해를 제공 합니다.

## <a name="phase-3-security-improvement-and-sustainment"></a>3 단계: 보안 향상 및 sustainment

로드맵의 3 단계 보안 태세를 강화 하는 데 걸린 단계 1 및 2 단계를 기반으로 합니다. 이 다이어그램에서 3 단계를 시각적으로 설명 합니다.

![3 단계: 1. RBAC를 2를 검토 합니다. 공격 노출 영역, 3을 축소 합니다. SEIM, 4 사용 하 여 로그를 통합 합니다. 유출 된 자격 증명 자동화](../media/securing-privileged-access/PAW_LP_Fig8.JPG)

이러한 기능은 이전 단계의 단계에서 빌드를 보다 사전 예방적인 상태에 기반을 이동 합니다. 이 단계는 특정 타임 라인이 없습니다 있으며 오래 걸릴 수 없습니다 구현 하려면 개별 조직에 따라 합니다.

### <a name="1-review-role-based-access-control"></a>1. 역할 기반 액세스 제어를 검토 합니다.

문서에 설명 된 세 개의 계층화 된 모델을 사용 하 여 [Active Directory 관리 계층 모델](securing-privileged-access-reference-material.md)를 검토 하 고 더 낮은 계층 관리자 상위 계층의 리소스 (그룹 멤버 자격에 대 한 Acl에 대 한 관리 액세스에 있지 않은 확인 합니다. 사용자 계정, 등...).

### <a name="2-reduce-attack-surfaces"></a>2. 공격 노출 영역 축소

도메인을 포함 하 여 identity 워크 로드를 강화, 도메인 컨트롤러, ADFS 및 이러한 시스템 중 하나를 손상 시 키 지와 Azure AD Connect 조직 내에서 다른 시스템의 손상 시킬 수 있습니다. 문서 [Active Directory 공격 가능성을 줄일](../ad-ds/plan/security-best-practices/reducing-the-active-directory-attack-surface.md) 하 고 [보안 id 인프라에 다섯 단계](/azure/security/azure-ad-secure-steps) 온-프레미스 및 하이브리드 보안에 대 한 지침을 제공 identity 환경입니다.

### <a name="3-integrate-logs-with-siem"></a>3. 로그를 SIEM과 통합

로깅 중앙 집중식된 SIEM 도구에 통합 하면 분석, 검색 및 보안 이벤트에 대응 하기 위해 조직을 수 있습니다. 아티클이 [손상의 기호에 대 한 Active Directory 모니터링](../ad-ds/plan/security-best-practices/monitoring-active-directory-for-signs-of-compromise.md) 고 [부록 l: 모니터링할 이벤트](../ad-ds/plan/appendix-l--events-to-monitor.md) 환경에서 모니터링 해야 하는 이벤트에 지침을 제공 합니다.

기능 이외에 일부인이 만들기를 집계 하기 때문에 계획 하 고 (달리 경고 상자에서 포함 하는 30 일 계획에 Azure ATP) 숙련 된 분석가 필요한 보안 정보 및 이벤트 관리 (SIEM)에 대 한 경고 조정

### <a name="4-leaked-credentials---force-password-reset"></a>4. 유출 된 자격 증명-Force 암호 재설정

암호는 손상 될 것으로 의심 되는 경우 암호 재설정을 자동으로 실행 하려면 Azure AD Id 보호를 사용 하 여 보안 태세를 향상 시키기 위해 계속 합니다. 지침 문서에 나오는 [트리거 Multi-factor Authentication 및 암호 변경에 대 한 위험 이벤트를 사용 하 여](/azure/active-directory/authentication/tutorial-risk-based-sspr-mfa) 조건부 액세스 정책을 사용 하 여이 사용 하도록 설정 하는 방법에 설명 합니다.

## <a name="am-i-done"></a>작업 완료

답은 없습니다.

악의적인 사용자를 차단 하지 중지 되므로 둘 다를 수 있습니다. 이 로드맵에서 방지 조직을 보호할 수 있는 현재 라고 위협은 공격자가 지속적으로 발전 하 고 이동 합니다. 환경을 대상으로 하는 악의적 사용자의 성공률을 줄이고 비용을 발생 시키는에 초점을 맞춘 지속적인 프로세스로 보안을 확인 하는 것이 좋습니다.

아니지만 권한 있는 액세스 보안 조직의 보안 프로그램의 일부만 보안 전략의 중요 한 구성이 됩니다.
