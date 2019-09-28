---
ms.assetid: a0f7bb11-47a5-47ff-a70c-9e6353382b39
title: 조건부 액세스 제어를 사용한 위험 관리
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e73cf77e9590496f0ff3f881fd8ac4556450b5f0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357764"
---
# <a name="manage-risk-with-conditional-access-control"></a>조건부 액세스 제어를 사용한 위험 관리




-   [주요 개념-AD FS의 조건부 액세스 제어](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [조건부 Access Control로 위험 관리](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md#BKMK_2)

## <a name="BKMK_1"></a>주요 개념-AD FS의 조건부 액세스 제어
AD FS의 전반적인 기능은 클레임 집합이 포함 된 액세스 토큰을 발급 하는 것입니다. AD FS 수락 하 고 실행 한 다음 클레임에 대 한 결정은 클레임 규칙에 따라 적용 됩니다.

AD FS의 액세스 제어는 사용자 또는 사용자 그룹이 AD FS 보안 리소스에 액세스할 수 있는지 여부를 결정 하는 허용 또는 거부 클레임을 발급 하는 데 사용 되는 발급 권한 부여 클레임 규칙을 사용 하 여 구현 됩니다. 권한 부여 규칙은 신뢰 당사자 트러스트에만 설정할 수 있습니다.

|규칙 옵션|규칙 논리|
|---------------|--------------|
|모든 사용자 허용|들어오는 클레임 유형이 *임의의 클레임 유형* 이고 값이 *임의의 값*이면 값이 있는 클레임 발급이 *허용*됩니다.|
|이 들어오는 클레임의 사용자에 대한 액세스 허용|들어오는 클레임 유형이 *지정된 클레임 유형* 이고 값이 *지정된 값*이면 값이 있는 클레임 발급이 *허용*됩니다.|
|이 들어오는 클레임의 사용자에 대한 액세스 거부|들어오는 클레임 유형이 *지정된 클레임 유형* 이고 값이 *지정된 값*이면 값이 있는 클레임 발급이 *거부*됩니다.|

이러한 규칙 옵션과 논리에 대한 자세한 내용은 [When to Use an Authorization Claim Rule](https://technet.microsoft.com/library/ee913560.aspx)를 참조하세요.

Windows Server 2012 r 2의 AD FS에서는 사용자, 장치, 위치, 인증 데이터 등의 여러 요소로 액세스 제어가 향상 되었습니다. 이는 권한 부여 클레임 규칙에 다양한 클레임 유형을 사용할 수 있기 때문입니다.  즉, Windows Server 2012 r 2의 AD FS에서는 사용자 id 또는 그룹 구성원 자격, 네트워크 위치, 장치 (작업 공간에 연결 되어 있는지 여부)를 기반으로 조건부 액세스 제어를 적용할 수 있습니다. 자세한 내용은 [SSO를 위해 모든 장치에서 작업 공간에 연결을 참조 하세요. 그리고 회사 응용 프로그램 전체에서 원활한 두 번째 단계 인증](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)) 및 인증 상태 (MFA (다단계 인증)가 수행 되었는지 여부)

Windows Server 2012 r 2에서 AD FS의 조건부 액세스 제어는 다음과 같은 이점을 제공 합니다.

-   사용자, 장치, 네트워크 위치 및 인증 상태에 따라 액세스를 허용하거나 거부할 수 있는 유연하고 명확한 응용 프로그램별 권한 부여 규칙

-   신뢰 당사자 응용 프로그램에 대한 발급 권한 부여 규칙 만들기

-   일반적인 조건부 액세스 제어 시나리오에 사용되는 다양한 기능의 UI 환경

-   고급 조건부 액세스 제어 시나리오에 대한 다양한 클레임 언어 및 Windows PowerShell 지원

-   사용자 지정 (신뢰 당사자 응용 프로그램별) ' 액세스 거부 ' 메시지 자세한 내용은 [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx)를 참조하세요. 이러한 메시지를 사용자 지정할 수 있으면 사용자의 액세스가 거부된 이유를 설명할 수 있으며, 가능한 경우 장치를 작업 공간에 연결하라는 메시지를 표시하는 등의 방법으로 셀프 서비스 업데이트 관리를 지원할 수도 있습니다. 자세한 내용은 [Join to Workplace from Any Device for SSO and Seamless Second Factor Authentication Across Company Applications](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)를 참조하세요.

다음 표에는 조건부 액세스 제어를 구현 하는 데 사용 되는 Windows Server 2012 r 2의 AD FS에서 사용할 수 있는 모든 클레임 유형이 나와 있습니다.

|클레임 형식|설명|
|--------------|---------------|
|Email Address|사용자의 메일 주소입니다.|
|지정된 이름|사용자의 지정된 이름입니다.|
|이름|사용자의 고유한 이름입니다.|
|UPN|사용자의 UPN(사용자 계정 이름)입니다.|
|일반 이름|사용자의 일반 이름입니다.|
|AD FS 1 x 메일 주소|AD FS 1.1 또는 AD FS 1.0과 상호 운용할 때 사용되는 사용자의 메일 주소입니다.|
|그룹|사용자가 구성원으로 속해 있는 그룹입니다.|
|AD FS 1 x UPN|AD FS 1.1 또는 AD FS 1.0과 상호 운용할 때 사용되는 사용자의 UPN입니다.|
|역할|사용자의 역할입니다.|
|성|사용자의 성입니다.|
|PPID|사용자의 프라이빗 식별자입니다.|
|이름 ID|사용자의 SAML 이름 식별자입니다.|
|인증 타임스탬프|사용자가 인증된 시간 및 날짜를 표시하는 데 사용됩니다.|
|인증 방법|사용자를 인증하는 데 사용되는 방법입니다.|
|거부 전용 그룹 SID|사용자의 거부 전용 그룹 SID입니다.|
|거부 전용 주 SID|사용자의 거부 전용 주 SID입니다.|
|거부 전용 주 그룹 SID|사용자의 거부 전용 주 그룹 SID입니다.|
|그룹 SID|사용자의 그룹 SID입니다.|
|주 그룹 SID|사용자의 주 그룹 SID입니다.|
|주 SID|사용자의 주 SID입니다.|
|Windows 계정 이름|도메인\사용자 형식으로 된 사용자의 도메인 계정 이름입니다.|
|등록된 사용자|사용자가 이 장치를 사용하도록 등록되어 있습니다.|
|장치 식별자|장치의 식별자입니다.|
|장치 등록 식별자|장치 등록 식별자입니다.|
|장치 등록 표시 이름|장치 등록 표시 이름입니다.|
|장치 OS 유형|장치의 운영 체제 유형입니다.|
|장치 OS 버전|장치의 운영 체제 버전입니다.|
|관리되는 장치|장치가 관리 서비스를 통해 관리됩니다.|
|전달된 클라이언트 IP|사용자의 IP 주소입니다.|
|클라이언트 응용 프로그램|클라이언트 응용 프로그램의 유형입니다.|
|클라이언트 사용자 에이전트|클라이언트에서 응용 프로그램에 액세스하는 데 사용하는 장치 유형입니다.|
|클라이언트 IP|클라이언트의 IP 주소입니다.|
|끝점 경로|활성 클라이언트와 수동 클라이언트를 확인하는 데 사용할 수 있는 끝점의 절대 경로입니다.|
|Proxy (프록시)|요청을 전달한 페더레이션 서버 프록시의 DNS 이름입니다.|
|응용 프로그램 식별자|신뢰 당사자의 식별자입니다.|
|응용 프로그램 정책|인증서의 응용 프로그램 정책입니다.|
|기관 키 식별자|발급된 인증서를 서명한 인증서의 기관 키 식별자 확장입니다.|
|기본 제한|인증서의 기본 제한 중 하나입니다.|
|확장된 키 사용|인증서의 확장된 키 사용 중 하나를 설명합니다.|
|발급자|해당 Authenticode X.509 v.3 인증서를 발급한 인증 기관의 이름입니다.|
|발급자 이름|인증서 발급자의 고유 이름입니다.|
|키 사용|인증서의 키 사용 중 하나입니다.|
|다음 날짜까지|이 날짜(현지 시간) 이후에는 인증서가 더 이상 유효하지 않습니다.|
|다음 날짜부터|이 날짜(현지 시간)부터 인증서가 유효합니다.|
|인증서 정책|인증서가 발급된 정책입니다.|
|공개 키|인증서의 공개 키입니다.|
|인증서 원시 데이터|인증서의 원시 데이터입니다.|
|주체 대체 이름|인증서의 대체 이름 중 하나입니다.|
|일련 번호|인증서의 일련 번호입니다.|
|서명 알고리즘|인증서의 서명을 만드는 데 사용된 알고리즘입니다.|
|Subject|인증서의 주체입니다.|
|주체 키 식별자|인증서의 주체 키 식별자입니다.|
|주체 이름|인증서의 주체 고유 이름입니다.|
|V2 템플릿 이름|인증서를 발급하거나 갱신할 때 사용된 버전 2 인증서 템플릿의 이름입니다. 이는 Microsoft의 특정 값입니다.|
|V1 템플릿 이름|인증서를 발급하거나 갱신할 때 사용된 버전 1 인증서 템플릿의 이름입니다. 이는 Microsoft의 특정 값입니다.|
|지문|인증서의 지문입니다.|
|X 509 버전|인증서의 X.509 형식 버전입니다.|
|회사 네트워크 내부|요청이 회사 네트워크 내부에서 시작된 경우를 나타내는 데 사용됩니다.|
|암호 만료 시간|암호가 만료되는 시간을 표시하는 데 사용됩니다.|
|암호 만료 일 수|암호 만료 일 수를 표시하는 데 사용됩니다.|
|암호 URL 업데이트|업데이트 암호 서비스의 웹 주소를 표시하는 데 사용됩니다.|
|인증 방법 참조|사용자를 인증하는 데 사용되는 모든 인증 방법을 나타내는 데 사용됩니다.|

## <a name="BKMK_2"></a>조건부 Access Control로 위험 관리
사용 가능한 설정을 통해 조건부 액세스 제어를 구현하여 위험을 관리할 수 있는 여러 가지 방법이 있습니다.

### <a name="common-scenarios"></a>일반적인 시나리오
예를 들어 특정 응용 프로그램 (신뢰 당사자 트러스트)에 대 한 사용자의 그룹 구성원 자격 데이터를 기반으로 조건부 액세스 제어를 구현 하는 간단한 시나리오를 가정해 보겠습니다. 즉, AD 도메인의 특정 그룹에 속한 사용자가 AD FS으로 보안이 유지 되는 특정 응용 프로그램에 액세스할 수 있도록 페더레이션 서버에서 발급 권한 부여 규칙을 설정할 수 있습니다.  이 시나리오를 구현 하는 방법에 대 한 자세한 단계별 지침 (UI 및 Windows PowerShell 사용)은 [ 연습 가이드에서 설명 합니다. 조건 Access Control @ no__t를 사용 하 여 위험 관리-0. 이 연습의 단계를 완료 하려면 랩 환경을 설정 하 고 [Windows Server 2012 r 2에서 AD FS에 대 한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)의 단계를 수행 해야 합니다.

### <a name="advanced-scenarios"></a>고급 시나리오
Windows Server 2012 r 2에서 AD FS의 조건부 액세스 제어를 구현 하는 다른 예를 들면 다음과 같습니다.

-   MFA를 사용 하 여이 사용자의 id의 유효성을 검사 한 경우에만 AD FS로 보호 되는 응용 프로그램에 대 한 액세스

    다음 코드를 사용할 수 있습니다.

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "PermitAccessWithMFA"
    c:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)https://schemas\.microsoft\.com/claims/multipleauthn$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   사용자에 게 등록 된 작업 공간 연결 장치에서 액세스 요청이 발생 하는 경우에만 AD FS 하 여 보안이 유지 되는 응용 프로그램에 대 한 액세스를 허용 합니다.

    다음 코드를 사용할 수 있습니다.

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "PermitAccessFromRegisteredWorkplaceJoinedDevice"
    c:[Type == "https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", Value =~ "^(?i)true$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   MFA를 사용 하 여 id의 유효성을 검사 한 사용자에 게 등록 된 작업 공간 연결 장치에서 액세스 요청이 발생 하는 경우에만 AD FS으로 보안이 유지 되는 응용 프로그램에 대 한 액세스를 허용 합니다.

    다음 코드를 사용할 수 있습니다.

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "RequireMFAOnRegisteredWorkplaceJoinedDevice"
    c1:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$"] &&
    c2:[Type == "https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", Value =~ "^(?i)true$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   MFA를 사용 하 여 id의 유효성을 검사 한 사용자가 액세스를 요청 하는 경우에만 AD FS 하 여 보안이 유지 되는 응용 프로그램에 대 한 엑스트라넷 액세스를 허용 합니다.

    다음 코드를 사용할 수 있습니다.

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "RequireMFAForExtranetAccess"
    c1:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$"] &&
    c2:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value =~ "^(?i)false$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

## <a name="see-also"></a>관련 항목
[연습 가이드: 조건부 Access Control 사용 하 여 위험 관리 @ no__t-0 @ no__t-1[Windows Server 2012 r 2의 AD FS에 대 한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



