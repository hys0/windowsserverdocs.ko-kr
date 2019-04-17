---
ms.assetid: 934ac796-e2ee-490d-8265-6a818be5ee79
title: "추가 다단계 인증 민감한 응용 프로그램에 대 한 위험을 관리"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e9ee275e6fe38005394cd071e9cfe9a7999350e8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="manage-risk-with-additional-multi-factor-authentication-for-sensitive-applications"></a>추가 다단계 인증 민감한 응용 프로그램에 대 한 위험을 관리

>Windows Server 2012 r 2에 적용 됩니다.


-   [Windows Server 2012 r 2에서 adfs 랩 환경을 설정합니다](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)

-   [연습 가이드: 추가 다단계 인증 민감한 응용 프로그램에 대 한 위험을 관리](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

-   [추가 인증 방법을 adfs 구성](../../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)

## <a name="in-this-guide"></a>이 가이드
이 가이드는 다음과 같은 정보를 제공합니다.

-   [Adfs의 인증 메커니즘](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_1) -Windows Server 2012 r 2에서 AD FS(Active Directory Federation Services) 사용할 수 있는 인증 방법에 대 한

-   [시나리오 개요](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_2) -다단계 인증 MFA ()를 사용 하도록 설정 하려면 AD FS(Active Directory Federation Services)를 사용 하는 시나리오에 대 한 설명을 사용자의 그룹 구성원에 따라 합니다.

    > [!NOTE]
    > Windows Server 2012 r 2에서 ADFS MFA 네트워크 위치, 디바이스 id 및 사용자 id 또는 그룹 구성원에 따라 하도록 설정할 수 있습니다.

    이 시나리오를 확인 하 고 구성에 대 한 자세한 단계별 지침을 참조 하세요. [연습 가이드: 민감한 응용 프로그램에 대 한 추가 다단계 인증 관리 위험](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)합니다.

## <a name="BKMK_1"></a>Adfs의 인증 메커니즘 주요 개념-

### <a name="benefits-of-authentication-mechanisms-in-ad---fs"></a>Adfs의 인증 메커니즘의 이점
Windows Server 2012 r 2에서 AD FS(Active Directory Federation Services) 풍부 하 고 더 유연한 일련의 도구와 IT 관리자가 사용자가 회사 리소스에 액세스 하려고 인증할 제공 합니다. 추가 인증 방법을 주를 통해 유연한 컨트롤의 관리자는 인증 구성에 풍부한 관리 경험 (모두 Windows PowerShell 및 사용자 인터페이스를 통해) 정책, 및 응용 프로그램 및 Adfs로 보호 되는 서비스에 액세스 하는 최종 사용자의 환경을 강화를 제공 합니다. 다음은 일부의 이점이 응용 프로그램 및 서비스와 Windows Server 2012 r 2에서 ADFS 보호:

-   글로벌 인증 정책-중앙 관리 기능을에서 IT 관리자는 인증 방법을 하는 데 보호 리소스에 액세스 하는 네트워크 위치에 따라 사용자가 인증 선택할 수 있습니다. 다음을 수행 하려면 관리자가 있습니다.

    -   엑스트라넷에서 액세스 요청에 대 한 보안을 강화 인증 방법의 사용을 요구 합니다.

    -   원활 하 게 번째 단계 인증을 위한 디바이스 인증을 설정 합니다. 이 사용자의 신원을 보호 리소스에 액세스 하기 전에 복합 id를 더 안전 하 게 확인 따라서 제공 리소스에 액세스 하는 데 사용 되는 등록 된 디바이스에 연결 합니다.

        > [!NOTE]
        > 원활 하 게 번째 단계 인증은 및 SSO 장치 개체, 디바이스 등록 서비스, Workplace Join, 및 디바이스에 대 한 자세한 내용은 참조 [SSO 및 원활 하 게 두 번째 요소 인증 간에 회사 응용 프로그램에 모든 디바이스에서 회사에 가입](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)합니다.

    -   MFA 요구 사항을 엑스트라넷 대 한 모든 액세스를 설정 하거나 조건에 따라 사용자의 id, 네트워크 위치 또는 보호 리소스에 액세스 하는 데 사용 하는 디바이스에 따라 합니다.

-   보다 유연 하 게 인증 정책 구성: 광고 FS 보안 리소스에 대 한 사용자 지정 인증 정책을 비즈니스 값 다양 한으로 구성할 수 있습니다. 예를 들어, MFA 업무에 큰 영향을 주는 응용 프로그램에 대 한 필요할 수 있습니다.

-   사용 편의성: 등 AD FS 관리 MMC GUI 기반 스냅인 Windows PowerShell cmdlet 간단 하 고 직관적 관리 도구 사용 IT 관리자 상대 쉽게 인증 정책을 구성할 수 있습니다. Windows PowerShell에서 사용할 배율와 관리 일상적인 작업을 자동화 솔루션 스크립트 수 있습니다.

-   세밀 기업 자산: Adfs을 사용 하 여 특정 리소스에 적용 되는 인증 정책을 구성 관리자 권한으로 향상 해야 제어 어떻게 기업 리소스를 통해 보호 됩니다. 응용 프로그램 IT 관리자가 지정 된 인증 정책 무시할 수 없습니다. 중요 한 응용 프로그램 및 서비스에 대 한 리소스에 액세스 때마다 MFA 요구 사항, 디바이스, 인증과 필요에 따라 새 인증 사용할 수 있습니다.

-   사용자 지정 MFA 공급자에 대 한 지원: ADFS 활용 하는 제 3 자 MFA 방법 조직에 대 한 통합이 인증 방법을 원활 하 게 사용 하는 기능을 제공 합니다.

### <a name="authentication-scope"></a>인증 범위
ADFS Windows Server 2012 r 2에서에 모든 응용 프로그램 및 Adfs로 보호 된 서비스에 해당 하는 세계적인 범위에 인증 정책을 지정할 수 있습니다.  특정 응용 프로그램과 Adfs로 보호 된 (파티 신뢰 의존) 서비스에 대 한 정책을 인증 설정할 수 있습니다. 특정 응용 프로그램에 대 한 인증 정책 지정 (의존 당 파티 신뢰) 글로벌 인증 정책 아니며 합니다. 글로벌 또는 의존 당 경우이 신뢰 파티 보안 인증을 열려고 할 때 인증 정책에 따라 MFA MFA 파티 신뢰는 트리거되지 합니다.  특정 인증 정책 구성 되지 않은 신뢰 파티 신뢰 (응용 프로그램과 서비스)를 대체 하는 세계적인 인증 정책은 합니다.

Adfs로 보호 된 모든 신뢰 당사자에 글로벌 인증 정책이 적용 됩니다. 글로벌 인증 정책의 일부로 다음 설정을 구성할 수 있습니다.

-   주 인증에 사용 되는 인증 방법

-   설정과 MFA 방법

-   디바이스 인증을 사용 하는지 여부. 자세한 내용은 참조 [SSO 및 원활 하 게 두 번째 요소 인증 간에 회사 응용 프로그램에 모든 디바이스에서 회사에 가입](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)합니다.

파티 신뢰 인증 정책에 따라 사용 신뢰 파티 신뢰 (응용 프로그램 또는 서비스)에 액세스 하려고에만 적용 됩니다. 다음 설정을 파티 신뢰 인증 의존 당 정책의 일환으로 구성할 수 있습니다.

-   사용자가 로그인 시 때마다 자격 증명을 제공 하는 데 필요한 여부

-   위치 데이터는 사용자/그룹, 장치 등록 및 액세스 요청에 따라 MFA 설정

### <a name="primary-and-additional-authentication-methods"></a>기본 및 추가 인증 방법
주 인증 메커니즘 뿐만 아니라 Windows Server 2012 r 2에 ADFS 관리자 추가 인증 방법을 구성할 수 있습니다. 기본 인증 기본 제공 되는 방법과 사용자의 id를 확인 하기 위한 것입니다. 사용자의 신원에 대 한 자세한 정보는 제공를 요청 하려면 추가 인증 요인 구성할 수 있으며 따라서 강력한 인증 있는지 확인 합니다.

Adfs Windows Server 2012 r 2에서 주 인증을 다음 옵션을 사용할 수 있습니다.

-   회사 네트워크에서 벗어나 있는 액세스할 수를 게시 리소스에 대 한 기본적으로 인증 서비스를 선택 합니다. 또한 (즉, 스마트 카드 기반 인증 또는 AD DS 함께 작업 하는 사용자 클라이언트 인증서 인증) 인증서를 사용할 수 있습니다.

-   Windows 인증 인트라넷 리소스에 대 한 기본적으로 선택 됩니다. 또한 양식 및/또는 인증 인증서도 사용할 수 있습니다.

개 이상의 인증 방법을 선택 하 여 사용자가 해당 응용 프로그램 또는 서비스에 대 한 로그인 페이지에서 인증 하는 데 어떤 방법 선택할 사용할 수 있습니다.

원활 하 게 번째 단계 인증을 위한 장치 인증을 사용할 수 있습니다. 이 사용자의 신원을 보호 리소스에 액세스 하기 전에 복합 id를 더 안전 하 게 확인 따라서 제공 리소스에 액세스 하는 데 사용 되는 등록 된 디바이스에 연결 합니다.

> [!NOTE]
> 원활 하 게 번째 단계 인증은 및 SSO 장치 개체, 디바이스 등록 서비스, Workplace Join, 및 디바이스에 대 한 자세한 내용은 참조 [SSO 및 원활 하 게 두 번째 요소 인증 간에 회사 응용 프로그램에 모든 디바이스에서 회사에 가입](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)합니다.

Windows 인증 방법 (기본 옵션) 인트라넷 리소스에 대 한 지정 하면 인증 요청을 지 원하는 Windows 인증 브라우저에서 원활 하 게이 방법을 거쳐.

> [!NOTE]
> Windows 인증 모든 브라우저에서 지원 되지 않습니다. Windows Server 2012 r 2에서 adfs에서 인증 메커니즘 사용자의 브라우저 사용자 에이전트 검색 하 고 구성할 수 있는 설정을 사용 하 여 해당 사용자 에이전트 Windows 인증을 지원 하는지 확인 하려면. 관리자는 사용자 에이전트가이 목록에 추가할 수 있습니다 (Windows PowerShell 통해 `Set-AdfsProperties -WIASupportedUserAgents`명령을 지 원하는 Windows 인증 브라우저 에이전트 문자열을 대체 사용자 지정할 수 있도록 합니다. 클라이언트의 사용자 에이전트 Windows 인증을 지원 하지 않는 경우 기본 대체 방법은 폼 인증 합니다.

### <a name="configuring-mfa"></a>MFA 구성
Windows Server 2012 r 2에서 adfs에서 MFA 구성 하는 방법은 두 가지: MFA, 조건을를 지정 하 고 추가 인증 방법을 선택 합니다. 추가 인증 방법에 대 한 자세한 내용은 참조 [adfs 추가 인증 방법을 구성](../../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)합니다.

**MFA 설정**

다음 옵션을 MFA 설정에 사용할 수 있습니다 (을 조건을 MFA 필요).

-   특정 사용자와 해당 federation 서버에 가입한 광고 도메인에 있는 그룹에 대 한 MFA 필요할 수 있습니다.

-   (가입 회사)을 등록 하거나 (하지 가입 회사) 등록에 대 한 MFA 필요할 수 있는 디바이스입니다.

    Windows Server 2012 r 2 장치 개체 자식 관계 최신 디바이스에는 사용자 중심 방법을 걸립니다 user@device와 회사입니다. 디바이스 개체 새 클래스 광고 응용 프로그램 및 서비스에 대 한 액세스를 제공 하는 경우 겹 id를 제공 하는 데 사용 될 수 있는 Windows Server 2012 r 2에는 있습니다. ADFS-디바이스 등록 서비스 (DRS)-의 새 구성 Active Directory에 디바이스 id를 제공 하 고 디바이스 id를 나타내는 데 사용 될 소비자 디바이스에는 인증서를 설정 합니다. 이 디바이스를 사용 하 여 있습니다 id 회사를 Active directory 회사의 개인 장치를 연결할 즉, 디바이스에 참여 합니다. 회사 계정에 개인 디바이스를 연결할 때 알려진된 장치 되 고 응용 프로그램 보호 리소스를 원활 하 게 번째 단계 인증을 제공 합니다. 즉, 디바이스를 회사 가입 되 면 사용자의 id이이 장치에 연결 및 보호 리소스에 액세스 하기 전에 원활 하 게 복합 신원 확인 하기 위해 사용할 수 있습니다.

    에 대 한 자세한 내용은 회사 참여 하 고 남겨, [SSO와 원활 하 게 두 번째 요소 인증 간에 회사 응용 프로그램에 대 한 모든 장치에서 회사에 가입](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)합니다.

-   보호 리소스에 대 한 액세스 요청 엑스트라넷 또는 인트라넷 되 면 MFA 필요할 수 있습니다.

## <a name="BKMK_2"></a>시나리오 개요
이 경우에 특정 응용 프로그램에 대 한 그룹 구성원 데이터는 사용자의 기준 MFA 사용할 수 있습니다. 즉,을 설정 합니다 인증 정책 해당 federation 서버에 사용자가 특정 그룹에 속하는 웹 서버에서 호스트 하는 특정 응용 프로그램에 대 한 액세스를 요청 MFA을 요구 하도록 합니다.

라는 테스트 클레임 기반 응용 프로그램에 대 한 인증 정책의 사용이 경우에 특히 **claimapp**반면, 광고 사용자 **로버트 Hatley** 을 광고 그룹에 속해 그 이후로 MFA 거치지 해야 **금융**합니다.

설정 하 고이 시나리오를 확인 하 여 단계 단계별 지침에 제공 된 [연습 가이드: 민감한 응용 프로그램에 대 한 추가 다단계 인증 관리 위험](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)합니다. 이 연습의 단계를 완료 하기 위해 환경을 설정 하 고 해야 단계에 따라 [랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

Adfs에서 MFA를 설정한 다른 시나리오는 다음과 같습니다.

-   액세스 요청 엑스트라넷에서 가져온 경우, MFA 사용 하도록 설정 합니다. "MFA 정책 설정" 섹션에서 코드를 수정할 수 [연습 가이드: 민감한 응용 프로그램에 대 한 추가 다단계 인증 관리 위험](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md) 다음과 같은 다음과 같습니다.

    ```
    'c:[type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn" );'
    ```

-   액세스 요청 아닌 공간 결합된 장치에서 가져온 경우, MFA 사용 하도록 설정 합니다.  "MFA 정책 설정" 섹션에서 코드를 수정할 수 [연습 가이드: 민감한 응용 프로그램에 대 한 추가 다단계 인증 관리 위험](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md) 다음과 같은 다음과 같습니다.

    ```
    'NOT EXISTS([type=="https://schemas.microsoft.com/2012/01/devicecontext/claims/registrationid"]) => issue (type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn");'

    ```

-   액세스 가입 있지만이 사용자에 게 등록 되어 있지 않으면 회사는 장치가 있는 사용자 로부터 예정입니다 MFA를 사용할 수 있습니다. "MFA 정책 설정" 섹션에서 코드를 수정할 수 [연습 가이드: 민감한 응용 프로그램에 대 한 추가 다단계 인증 관리 위험](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md) 다음과 같은 다음과 같습니다.

    ```
    'c:[type=="https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", value == "false"] => issue (type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn");'

    ```

## <a name="see-also"></a>참조 하십시오
[연습 가이드: 관리 민감한 응용 프로그램에 대 한 추가 다단계 인증 위험](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)<ph x="2">
</ph>[랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



