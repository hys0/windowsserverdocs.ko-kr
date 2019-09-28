---
title: 권한 있는 액세스 보안
description: 권한 있는 액세스를 보호 하는 단계별 방법
ms.prod: windows-server
ms.topic: conceptual
ms.assetid: f5dec0c2-06fe-4c91-9bdc-67cc6a3ede60
ms.date: 02/25/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: mas
ms.openlocfilehash: e6ff22d0563fa11aa633004966b2cd2648ba5877
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357697"
---
# <a name="securing-privileged-access"></a>권한 있는 액세스 보안

>적용 대상: Windows Server

권한 있는 액세스 보안은 오늘날의 조직에서 비즈니스 자산에 대한 보안 보증을 설정하는 중요한 첫 단계입니다. IT 조직에서 대부분 또는 모든 비즈니스 자산의 보안은 관리, 관리 및 개발에 사용 되는 권한 있는 계정의 무결성에 따라 달라 집니다. 사이버 공격자는 종종 이러한 계정 및 권한 있는 액세스의 다른 요소를 대상으로 하 여 [해시 패스 및 티켓 전달](https://www.microsoft.com/pth)같은 자격 증명 도난 공격을 통해 데이터 및 시스템에 액세스할 수 있습니다.

결정 된 악의적 사용자에 대해 권한 있는 액세스를 보호 하려면 이러한 시스템을 위험 으로부터 격리 하는 완전 하 고 해결 방법을 수행 해야 합니다.

## <a name="what-are-privileged-accounts"></a>권한 있는 계정 이란?

보안을 설정 하는 방법에 대해 설명 하기 전에 권한 있는 계정을 정의 합니다.

Active Directory Domain Services 관리자와 같은 권한 있는 계정은 IT 조직의 대부분 또는 모든 자산에 직접 또는 간접적으로 액세스할 수 있으므로 이러한 계정을 손상 시킬 경우 상당한 비즈니스 위험이 있습니다.

## <a name="why-securing-privileged-access-is-important"></a>권한 있는 액세스 보안이 중요 한 이유는 무엇 인가요?

사이버 공격자는 AD (Active Directory)와 같은 시스템에 대 한 권한 있는 액세스에 초점을 맞춘 모든 조직에서 대상으로 지정 된 모든 데이터에 대 한 액세스를 빠르게 얻습니다. 기존 보안 접근 방식은 네트워크 및 방화벽에 기본 보안 경계를 집중 하지만 네트워크 보안의 효율성은 다음 두 가지 추세에 의해 크게 저하 되었습니다.

* 조직에서 모바일 엔터프라이즈 Pc의 기존 네트워크 경계 외부에 있는 데이터 및 리소스를 호스팅하고 있습니다. 모바일 휴대폰 및 태블릿, 클라우드 서비스와 같은 장치 및 사용자 고유의 장치 (BYOD)를 가져옵니다.
* 악의적 사용자는 피싱 및 기타 웹 및 전자 메일 공격을 통해 네트워크 경계 내의 워크스테이션에 대한 액세스 권한을 지속적으로 획득할 수 있는 능력을 보여 주었습니다.

이러한 요인은 기존 네트워크 경계 전략 외에도 최신 보안 경계를 인증 및 권한 부여 id 제어로 구축 해야 합니다. 여기에 있는 보안 경계는 자산과 자산의 위협 간에 일관 된 컨트롤 집합으로 정의 됩니다. 권한 있는 계정은이 새로운 보안 경계를 효과적으로 제어할 수 있으므로 권한 있는 액세스를 보호 하는 것이 중요 합니다.

![조직의 ID 계층을 보여 주는 다이어그램](../media/securing-privileged-access/PAW_LP_Fig2.JPG)

관리 계정에 대 한 제어 권한을 획득 하는 공격자는 아래와 같이 해당 권한을 사용 하 여 대상 조직에 미치는 영향을 높일 수 있습니다.

![관리 계정에 대한 제어 권한이 있는 악의적 사용자가 이러한 권한을 사용하여 대상 조직의 비용으로 어떻게 이득을 추구할 수 있는지 보여 주는 다이어그램](../media/securing-privileged-access/PAW_LP_Fig3.JPG)

아래 그림에서는 두 개의 경로를 보여 줍니다.

* 표준 사용자 계정을 사용 하 여 전자 메일, 웹 검색, 일상적인 작업을 완료 하는 것과 같은 리소스에 대 한 권한이 없는 액세스에 사용 되는 "blue" 경로입니다.

   > [!NOTE]
   > 뒷부분에서 설명 하는 파란색 경로 항목은 관리 계정 이상으로 확장 되는 광범위 한 환경 보호를 표시 합니다.

* 피싱 및 기타 웹 및 전자 메일 공격의 위험을 줄이기 위해 권한 있는 액세스가 강화 된 장치에서 발생 하는 "red" 경로입니다.

![웹 검색 및 전자 메일 액세스와 같은 높은 위험 표준 사용자 작업 으로부터 권한 있는 액세스 작업을 격리 하기 위해 로드맵에서 설정 하는 관리에 대 한 별도의 "경로"를 보여 주는 다이어그램](../media/securing-privileged-access/PAW_LP_Fig4.JPG)

## <a name="securing-privileged-access-roadmap"></a>권한 있는 액세스 보안 로드맵

이 로드맵은 이미 배포 된 Microsoft 기술의 사용을 최대화 하 고, 클라우드 기술을 활용 하 여 보안을 강화 하 고, 이미 배포 했을 수 있는 타사 보안 도구를 통합 하도록 설계 되었습니다.

Microsoft 권장 로드맵은 3 단계로 나뉩니다.

* [1 단계: 처음 30 일]()
   * 의미 있는 긍정적인 영향을 받는 빠른 wins
* [2 단계: 90 일]()
   * 상당한 증분 향상.
* [3 단계: 진행]()
   * 보안 향상 및 sustainment.

로드맵은 이러한 공격 및 솔루션 구현에 대한 Microsoft의 경험을 바탕으로 가장 효과적이고 신속한 구현부터 우선적으로 수행하도록 지정되었습니다. 

이 로드맵에 따라 확인된 악의적 사용자로부터 권한 있는 액세스의 보안을 유지하는 것이 좋습니다. 조직의 기존 기능 및 특정 요구 사항을 수용하도록 이 로드맵을 조정할 수 있습니다.

> [!NOTE]
> 권한 있는 액세스 보안에는 기술적 구성 요소(호스트 방어, 계정 보호, ID 관리 등)뿐만 아니라 프로세스 변경과 관리 방식 및 지식 등 광범위한 요소가 필요합니다. 로드맵의 타임라인은 대략적이며 고객 구현에 대한 Microsoft의 경험을 바탕으로 합니다. 기간은 사용자 환경의 복잡성 및 변경 관리 프로세스에 따라 다릅니다.

## <a name="phase-1-quick-wins-with-minimal-operational-complexity"></a>1단계: 운영 복잡성을 최소화 하면서 빠른 wins

로드맵의 1 단계는 자격 증명 도난 및 남용의 가장 자주 사용 되는 공격 기법을 신속 하 게 완화 하는 데 중점을 두었습니다. 1 단계는 약 30 일 이내에 구현 되도록 설계 되었으며이 다이어그램에 표시 됩니다.

![1 단계 다이어그램: 1. 별도의 관리자 및 사용자 계정 2. Just-in-time 로컬 관리자 암호, 3. 관리 워크스테이션 1, 4 단계. Id 공격 검색](../media/securing-privileged-access/PAW_LP_Fig6.JPG)

### <a name="1-separate-accounts"></a>1. 개별 계정

권한 있는 액세스 계정에서 인터넷 위험 (피싱 공격, 웹 검색)을 분리 하는 데 도움이 되도록 권한 있는 액세스 권한이 있는 모든 직원에 대 한 전용 계정을 만듭니다. 관리자는 웹을 탐색 하 고, 전자 메일을 확인 하 고, 높은 권한의 계정을 사용 하 여 일상적인 생산성 작업을 수행 하지 않아야 합니다. 이에 대 한 자세한 내용은 참조 문서의 [개별 관리 계정](securing-privileged-access-reference-material.md#separate-administrative-accounts) 섹션에서 찾을 수 있습니다.

온-프레미스 AD 및 Azure AD 환경에서 관리자 권한을 영구적으로 할당 하 여 두 개 이상의 응급 액세스 계정을 만들려면 [AZURE ad의 응급 액세스 계정 관리](/azure/active-directory/users-groups-roles/directory-emergency-access) 문서에 있는 지침을 따르세요. 이러한 계정은 기존 관리자 계정이 재해가 발생 한 경우와 같은 필수 작업을 수행할 수 없는 경우에만 사용할 수 있습니다.

### <a name="2-just-in-time-local-admin-passwords"></a>2. Just-in-time 로컬 관리자 암호

공격자가 로컬 SAM 데이터베이스에서 로컬 관리자 계정 암호 해시를 도용 하 고 다른 컴퓨터를 공격 하는 데 사용 하는 위험을 완화 하기 위해 조직에서는 모든 컴퓨터에 고유한 로컬 관리자 암호가 있는지 확인 해야 합니다. LAPS (로컬 관리자 암호 솔루션) 도구는 각 워크스테이션과 서버에서 고유한 임의의 암호를 구성 하 여 ACL로 보호 되는 Active Directory (AD)에 저장할 수 있습니다. 자격이 있는 권한 있는 사용자만 이러한 로컬 관리자 계정 암호의 재설정을 읽거나 요청할 수 있습니다. [Microsoft 다운로드 센터](http://Aka.ms/LAPS)에서 워크스테이션 및 서버에 사용할 LAPS를 가져올 수 있습니다.

LAPS 및 Paw를 사용 하 여 환경을 운영 하는 방법에 대 한 추가 지침은 [클린 소스 원칙을 기반으로 하는 운영 표준](securing-privileged-access-reference-material.md#operational-standards-based-on-clean-source-principle)섹션에서 찾을 수 있습니다.

### <a name="3-administrative-workstations"></a>3. 관리 워크스테이션

Azure Active Directory 및 기존 온-프레미스 Active Directory 관리 권한이 있는 사용자에 대 한 초기 보안 조치로, windows 10 장치를 사용 하 여 [보안 수준이 높은 windows 10 장치에 대 한 표준으로 구성 된 windows 10 장치를 사용 하 고 있는지 확인 ](/windows-hardware/design/device-experiences/oem-highly-secure). 권한 있는 관리자 계정은 관리 워크스테이션의 로컬 관리자 그룹의 구성원이 아니어야 합니다.  워크스테이션에 대 한 구성이 변경 되어야 하는 경우 UAC (사용자 Access Control)를 통한 권한 상승을 활용할 수 있습니다.  또한 장치를 강화 하기 위해 Windows 10 보안 기준을 워크스테이션에 적용 해야 합니다.

### <a name="4-identity-attack-detection"></a>4. Id 공격 검색

[AZURE ATP (Advanced Threat Protection)](/azure-advanced-threat-protection/what-is-atp) 는 온-프레미스에서 전달 되는 고급 위협, 손상 된 id 및 악의적인 참가자 작업을 식별 하 고, 검색 하 고, 조사 하는 데 도움이 되는 클라우드 기반 보안 솔루션입니다 Active Directory 개발.

## <a name="phase-2-significant-incremental-improvements"></a>2 단계: 상당한 증분 향상

2 단계는 1 단계에서 수행한 작업을 기반으로 하며 약 90 일 이내에 완료 되도록 설계 되었습니다. 이 단계는 다음 다이어그램에 나와 있습니다.

![2 단계 다이어그램: 1. 비즈니스용 Windows Hello/MFA, 2. PAW 롤아웃, 3. Just-in-time 권한, 4. Credential Guard, 5. 자격 증명이 유출 되었습니다. 6. 측면 이동 취약성 검색](../media/securing-privileged-access/PAW_LP_Fig7.JPG)

### <a name="1-require-windows-hello-for-business-and-mfa"></a>1. 비즈니스용 Windows Hello 및 MFA 필요

관리자는 비즈니스용 Windows Hello와 관련 된 사용 편의성을 활용할 수 있습니다. 관리자는 자신의 Pc에서 복잡 한 암호를 강력한 2 단계 인증으로 바꿀 수 있습니다. 공격자가 장치와 생체 인식 정보를 모두가지고 있어야 하며 직원의 지식 없이도 액세스를 얻는 것이 훨씬 어렵습니다. 비즈니스용 Windows Hello 및 롤아웃할 경로에 대 한 자세한 내용은 [비즈니스용 Windows Hello 개요](/windows/security/identity-protection/hello-for-business/hello-overview) 를 참조 하세요.

Azure MFA를 사용 하 여 Azure AD에서 관리자 계정에 대해 MFA (multi-factor authentication)를 사용 하도록 설정 합니다. 최소 사용 [기준 보호 조건부 액세스 정책](/azure/active-directory/conditional-access/baseline-protection#require-mfa-for-admins) azure Multi-Factor Authentication에 대 한 자세한 내용은 [클라우드 기반 azure 배포](/azure/active-directory/authentication/howto-mfa-getstarted) 문서에서 찾을 수 있습니다 Multi-Factor Authentication

### <a name="2-deploy-paw-to-all-privileged-identity-access-account-holders"></a>2. 모든 권한 있는 id 액세스 계정 소유자에 PAW 배포

권한 있는 계정을 전자 메일, 웹 검색 및 기타 비 관리 작업에서 발견 된 위협 으로부터 분리 하는 프로세스를 계속 진행 하려면,에 대 한 권한 있는 액세스 권한이 있는 모든 직원에 대해 전용 권한 있는 액세스 워크스테이션 (PAW)을 구현 해야 합니다. 조직의 정보 시스템. PAW 배포에 대 한 추가 지침은 [권한 있는 액세스 워크스테이션](privileged-access-workstations.md#paw-phased-implementation)문서에서 찾을 수 있습니다.

### <a name="3-just-in-time-privileges"></a>3. Just-in-time 권한

권한 노출 시간을 낮추고 사용에 대 한 가시성을 높이기 위해, 아래와 같은 적절 한 솔루션을 사용 하 여 JIT (just-in-time)를 제공 합니다.

* AD DS(Active Directory 도메인 서비스)의 경우 MIM(Microsoft Identity Manager)의 [PAM(Privileged Access Manager)](/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) 기능을 사용합니다.
* Azure Active Directory의 경우 [Azure AD PIM(Privileged Identity Management)](/azure/active-directory/privileged-identity-management/pim-deployment-plan) 기능을 사용합니다.

### <a name="4-enable-windows-defender-credential-guard"></a>4. Windows Defender Credential Guard 사용

Credential Guard를 사용 하면 도메인 자격 증명으로 응용 프로그램에 의해 저장 되는 NTLM 암호 해시, Kerberos 티켓 및 자격 증명을 보호 하는 데 도움이 됩니다. 이 기능을 사용 하면 도난당 한 자격 증명을 사용 하 여 환경에서 피벗 하는 어려움을 높여 해시 전달 또는 티켓 통과와 같은 자격 증명 도난 공격을 방지할 수 있습니다. Credential Guard의 작동 방식 및 배포 방법에 대 한 정보는 [Windows Defender Credential Guard를 사용 하 여 파생 된 도메인 자격 증명 보호](/windows/security/identity-protection/credential-guard/credential-guard)문서에서 찾을 수 있습니다.

### <a name="5-leaked-credentials-reporting"></a>5. 누출 자격 증명 보고

"매일 microsoft는 새로운 위협을 식별 하 고 고객을 보호 하기 위해 6조5000억 신호를 분석 [합니다](https://news.microsoft.com/bythenumbers/cyber-attacks) .

Microsoft Azure AD Id 보호를 사용 하도록 설정 하 여 누출 된 자격 증명이 있는 사용자에 게 보고 하 여 수정할 수 있도록 합니다. 조직에서 위협 으로부터 클라우드 및 하이브리드 환경을 보호 하는 데 도움이 되는 [Azure AD ID 보호](/azure/active-directory/identity-protection/index) 활용할 수 있습니다.

### <a name="6-azure-atp-lateral-movement-paths"></a>6. Azure ATP 측면 이동 경로

권한 있는 액세스 계정 소유자가 관리를 위해 해당 PAW를 사용 하 고 있는지 확인 합니다. 권한이 없는 손상 된 계정이 자격 증명 도난 공격을 통해 권한 있는 계정에 대 한 액세스 권한을 얻을 수 없도록 합니다. [AZURE ATP LMPs (측면 이동 경로)](/azure-advanced-threat-protection/use-case-lateral-movement-path) 는 권한 있는 계정이 손상 될 수 있는 위치를 식별 하는 보고를 이해 하기 쉽게 해줍니다.

## <a name="phase-3-security-improvement-and-sustainment"></a>3 단계: 보안 향상 및 sustainment

로드맵의 3 단계는 보안 상태를 강화 하기 위해 1 단계 및 2 단계에서 수행 된 단계를 빌드합니다. 이 다이어그램에서 3 단계가 시각적으로 표시 됩니다.

![3 단계: 1. RBAC, 2를 검토 합니다. 공격 노출 영역을 줄입니다. 3. 로그를 SEIM, 4와 통합 합니다. 누출 자격 증명 자동화](../media/securing-privileged-access/PAW_LP_Fig8.JPG)

이러한 기능은 이전 단계의 단계를 기반으로 하 고 방어를 보다 적극적인 상태로 전환 합니다. 이 단계에는 특정 타임 라인이 없으며 개별 조직에 따라 구현 하는 데 더 많은 시간이 걸릴 수 있습니다.

### <a name="1-review-role-based-access-control"></a>1. 역할 기반 액세스 제어 검토

[관리 계층 모델 Active Directory](securing-privileged-access-reference-material.md)문서에 설명 된 3 계층 모델을 사용 하 여 하위 계층 관리자에 게 더 높은 계층 리소스 (그룹 멤버 자격, 사용자 계정에 대 한 acl 등)에 대 한 관리 권한이 없는지 확인 하 고 확인 합니다.

### <a name="2-reduce-attack-surfaces"></a>2. 공격 노출 영역 감소

도메인, 도메인 컨트롤러, ADFS 및 Azure AD Connect을 포함 하 여 이러한 시스템 중 하나를 손상 시킬 경우 조직의 다른 시스템이 손상 될 수 있으므로 id 작업을 강화 하세요. [Active Directory 공격 노출 영역을 줄이는](../ad-ds/plan/security-best-practices/reducing-the-active-directory-attack-surface.md) 문서와 [id 인프라를 보호 하는 5 단계](/azure/security/azure-ad-secure-steps) 는 온-프레미스 및 하이브리드 id 환경을 보호 하기 위한 지침을 제공 합니다.

### <a name="3-integrate-logs-with-siem"></a>3. SIEM과 로그 통합

로그인을 중앙의 SIEM 도구에 통합 하면 조직에서 보안 이벤트를 분석, 검색 및 대응 하는 데 도움이 됩니다. 다음 문서에서는 손상 및 [부록 L [의 서명을 위한 Active Directory 모니터링](../ad-ds/plan/security-best-practices/monitoring-active-directory-for-signs-of-compromise.md) 합니다. 모니터링할](../ad-ds/plan/appendix-l--events-to-monitor.md) 이벤트는 사용자 환경에서 모니터링 해야 하는 이벤트에 대 한 지침을 제공 합니다.

이는 SIEM (보안 정보 및 이벤트 관리)에서 경고를 집계, 생성 및 조정 하는 데 숙련 된 분석가가 필요 하기 때문에 더 이상 계획의 일부입니다 (기본 제공 되는 30 일 요금제의 Azure ATP와 다름).

### <a name="4-leaked-credentials---force-password-reset"></a>4. 누출 자격 증명-암호 재설정 강제

암호가 손상 된 것으로 의심 되는 경우 자동으로 암호 재설정을 사용 하도록 Azure AD ID 보호 설정 하 여 보안 상태를 계속 향상할 수 있습니다. [위험 이벤트를 사용 하 여 Multi-Factor Authentication 및 암호 변경을 트리거하](/azure/active-directory/authentication/tutorial-risk-based-sspr-mfa) 는 문서에 있는 지침은 조건부 액세스 정책을 사용 하 여이 기능을 사용 하도록 설정 하는 방법을 설명 합니다.

## <a name="am-i-done"></a>작업 완료

짧은 대답은 아니요입니다.

잘못 된 사람들은 중단 되지 않으므로 가능 하지 않습니다. 이 로드맵은 공격자가 지속적으로 진화 하 고 변화 하는 현재 알려진 위협을 조직에서 보호 하는 데 도움이 됩니다. 사용자 환경을 대상으로 하는 악의적 사용자의 성공률을 높이고 비용을 절감 하는 데 초점을 맞춘 지속적인 프로세스로 보안을 확인 하는 것이 좋습니다.

조직 보안 프로그램의 유일한 부분은 아니지만 권한 있는 액세스를 보호 하는 것은 보안 전략의 중요 한 구성 요소입니다.
