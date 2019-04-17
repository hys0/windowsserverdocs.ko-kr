---
ms.assetid: a0f7bb11-47a5-47ff-a70c-9e6353382b39
title: "관련 된 위험 조건부 액세스 제어도 관리"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e2ad7d1467abd6d69077b515b8c69a65f7e70f19
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="manage-risk-with-conditional-access-control"></a>관련 된 위험 조건부 액세스 제어도 관리

>Windows Server 2012 r 2에 적용 됩니다.


-   [Adfs의 주요 개념 조건부 액세스 제어](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [관련 된 위험 조건부 액세스 제어도 관리](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md#BKMK_2)

## <a name="BKMK_1"></a>주요 개념-adfs에서 조건부 액세스 제어
Adfs의 전체 기능은 발급 액세스 토큰 클레임 집합을 포함 하는 것입니다. 어떤 클레임 ADFS 수락 하 고 다음 문제에 대 한 결정 클레임 규칙 적용 됩니다.

Adfs의 액세스 제어 발급 허용 발급 또는 거부 클레임 사용자 있는지 여부를 결정 하는 데 사용 되는 인증 클레임 규칙과 함께 구현 되거나의 사용자 그룹 여부 광고 FS 보안 리소스에 액세스할 수 있습니다. 승인 규칙 신뢰 파티 신뢰 에서만 설정 가능 합니다.

|규칙 옵션|규칙 논리|
|---------------|--------------|
|모든 사용자가 허용|수신 클레임 유형 같으면 *유형 청구* 같음 가치 및 *값*, 문제 값 같음와 주장 다음 *허용*|
|이 들어오는 클레임 있는 사용자에 게 액세스 권한을|수신 클레임 유형 같으면 *클레임 유형 지정* 같음 값 및 *클레임 값 지정 된*, 문제 값 같음와 주장 다음 *허용*|
|액세스를 사용자에 게가 들어오는 클레임 거부|수신 클레임 유형 같으면 *클레임 유형 지정* 같음 값 및 *클레임 값 지정 된*, 문제 값 같음와 주장 다음 *거부*|

이 규칙 옵션과 논리에 대 한 자세한 내용은 참조 [승인 클레임 규칙을 사용 하는 경우](https://technet.microsoft.com/library/ee913560.aspx)합니다.

Windows Server 2012 r 2 ADFS 액세스 제어 사용자, 디바이스, 위치 및 인증 데이터를 포함 한 여러 요인으로 향상 됩니다. 이 의해 가능 더 다양 한 클레임 유형 승인 클레임 규칙에 사용할 수 있습니다.  즉, Windows Server 2012 r 2 Adfs에 적용할 수 있습니다 조건부 액세스 제어 사용자 id 또는 그룹 구성원 네트워크 위치를 디바이스에 따라 (회사에 대 한 자세한 내용은 가입 인지 확인 [SSO 및 원활 하 게 두 번째 요소 인증 간에 회사 응용 프로그램에 모든 디바이스에서 회사에 가입](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md))를 인증 상태 (다중 요소 인증 (MFA) 수행 된 여부) 및 합니다.

Windows Server 2012 r 2에 adfs에서 조건부 액세스 제어 다음 기능을 제공 합니다.

-   허용 하거나 사용자, 디바이스, 네트워크 위치 및 인증 상태에 따라 액세스 거부 수 있는 반면 유연 하 고 표현력이 응용 프로그램 승인 정책

-   파티 응용 프로그램에 대 한 권한 규칙 발급 만들기

-   일반적인 조건부 액세스 제어 시나리오에 대 한 다양 한 UI 환경

-   고급 조건부 액세스 제어 시나리오에 대 한 지원이 Windows PowerShell 및 다양 한 클레임 언어

-   사용자 지정 (의존 당 파티 응용 프로그램) 메시지 액세스 거부 합니다. 자세한 내용은 참조 [AD FS 로그인 페이지 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx)합니다. 이러한 메시지를 사용자 지정할 수 없게 되 고, 여 설명 이유 사용자는 되 고 액세스할 수 있으며도 자체 서비스 개선 경우 가능 하면 등 회사에 프롬프트 사용자가 자신의 디바이스에 참가 용이 하 게 수 있습니다. 자세한 내용은 참조 [SSO 및 원활 하 게 두 번째 요소 인증 간에 회사 응용 프로그램에 모든 디바이스에서 회사에 가입](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)합니다.

다음 표에서 Windows Server 2012 r 2 조건부 액세스 제어 구현 하는 데 사용할 수 Adfs에서 사용할 수 있는 모든 클레임 유형은 포함 합니다.

|클레임 유형|설명|
|--------------|---------------|
|메일 주소|사용자의 메일 주소입니다.|
|이름|사용자의 이름이 합니다.|
|이름|사용자의 고유한 이름|
|UPN|UPN 사용자 계정 이름 () 사용자의 합니다.|
|일반 이름|일반 사용자의 이름입니다.|
|메일 주소 x ADFS 1|ADFS 1.1 또는 ADFS 1.0와 상호 작용할 때 사용자의 메일 주소입니다.|
|그룹|사용자가의 그룹입니다.|
|광고 FS 1 x UPN|ADFS 1.1 또는 ADFS 1.0와 상호 작용할 때 사용자의 UPN 합니다.|
|역할|사용자가 역할입니다.|
|성|사용자의 성과 합니다.|
|PPID|사용자의 개인 식별자입니다.|
|이름 ID|사용자의 SAML 이름 식별자입니다.|
|인증 타임 스탬프|사용자가 인증 날짜와 시간을 표시 하는 데 사용 합니다.|
|인증 방법|사용자 인증 하는 데 사용 하는 방법입니다.|
|만 그룹 SID|거부 전용 그룹 SID 사용자의 합니다.|
|거부 주 SID만|사용자의 거부 전용 기본 SID 합니다.|
|기본 그룹 SID|거부 전용 주 그룹 SID 사용자의 합니다.|
|그룹 SID|사용자의 그룹 SID 합니다.|
|주 그룹 SID|사용자의 기본 그룹 SID 합니다.|
|주 SID|사용자의 기본 SID 합니다.|
|Windows 계정 이름|도메인 계정 도메인 \ 사용자 형태의 사용자의 이름입니다.|
|이 사용자를 등록|이 디바이스를 사용 하 여 사용자가 등록 되어 있습니다.|
|디바이스 식별자입니다.|디바이스 식별자입니다.|
|디바이스 식별자 등록|장치를 등록에 대 한 식별자입니다.|
|디바이스 등록 표시 이름|장치를 등록의 이름을 표시 합니다.|
|디바이스 운영 체제 유형|디바이스의 운영 체제 유형|
|디바이스 운영 체제 버전|디바이스의 운영 체제 버전입니다.|
|이 디바이스 관리|디바이스 관리 서비스에서 관리 합니다.|
|클라이언트 전달 IP|사용자의 IP 주소입니다.|
|클라이언트 응용 프로그램|형식 클라이언트 응용 프로그램입니다.|
|클라이언트 사용자 에이전트|디바이스 유형 클라이언트 응용 프로그램에 액세스에 사용 중입니다.|
|클라이언트 IP|클라이언트의 IP 주소입니다.|
|끝점 경로|수동 하는 클라이언트와 활성 결정 하는 데 사용할 수 있는 절대 끝점 경로입니다.|
|프록시|DNS 요청 전달 federation 서버 프록시의 이름입니다.|
|응용 프로그램 식별자|당사자에 대 한 식별자입니다.|
|정책|인증서의 정책 응용 프로그램입니다.|
|키 식별자 기관|기관 키 식별자 발급된 된 인증서를 서명 인증서의 확장 합니다.|
|기본 제한|기본 제한 인증서의 중 하나입니다.|
|향상 된 키 사용|인증서의 향상 된 키 사용 중 하나에 대해 설명 합니다.|
|발행인이|X.509 인증서를 인증 기관의 이름입니다.|
|발행인이 이름|인증서 발행인이의 고유 하는 이름입니다.|
|키 사용|인증서의 키 사용 중 하나입니다.|
|하지 후|날짜 이후에 인증서를는 더 이상 유효 로컬 시간 합니다.|
|하지 하기 전에|날짜 로컬 시간 인증서 유효 됩니다.|
|인증서 정책|인증서가 발급 되었습니다는 정책입니다.|
|공개 키|인증서의 공개 키입니다.|
|인증서 Raw 데이터|인증서 원시 데이터입니다.|
|주체 다른 이름|다른 이름 인증서의 중 하나입니다.|
|일련 번호|일련 번호 인증서입니다.|
|서명 알고리즘|알고리즘 서명 인증서를 작성 하는 데 사용 합니다.|
|제목|인증서의 제목 합니다.|
|주체 주요 식별자|인증서의 제목 주요 식별자입니다.|
|제목 이름|제목 고유 인증서의 이름입니다.|
|V2 템플릿 이름|버전 2 인증서 템플릿의 이름이 해도 발급 또는 인증서 갱신 사용 합니다. 특정 Microsoft 값입니다.|
|V1 템플릿 이름|발급 또는 인증서 갱신 때 사용 되는 버전 1 인증서 템플릿의 이름입니다. 특정 Microsoft 값입니다.|
|지문|인증서의 지문입니다.|
|509 버전 X|인증서 X.509 형식 버전입니다.|
|회사 네트워크 안쪽|회사의 네트워크 안에 요청에서 발생 하는 경우 나타내는 데 사용 합니다.|
|만료 기간 암호|암호가 만료 되 면 시간을 표시 하는 데 사용 합니다.|
|암호 만료 날짜|비밀 번호 만료를 일 수를 표시 하는 데 합니다.|
|업데이트 암호 URL|업데이트 암호 서비스의 웹 주소를 표시 하는 데 사용 합니다.|
|인증 방법 참조|나타내는 al 인증 방법을 사용자 인증 하는 데 사용 하는 데 사용 합니다.|

## <a name="BKMK_2"></a>관련 된 위험 조건부 액세스 제어도 관리
사용할 수 있는 설정을 사용 하 고 여러 가지 방법으로는 위험 조건부 액세스 제어 구현 하 여 관리할 수 있습니다.

### <a name="common-scenarios"></a>일반적인 시나리오
예를 들어, 특정 응용 프로그램 (신뢰 파티 신뢰)에 대 한 그룹 구성원 데이터는 사용자의 기준 조건부 액세스 제어 구현 하는 간단한 시나리오 할 때 즉, 설정할 수 있습니다 발급 승인 규칙 해당 federation 서버에서 사용자의 광고에 특정 그룹에 속하는 허용 하도록 도메인 Adfs로 보호 된 특정 응용 프로그램에 대 한 액세스 합니다.  자세한 단계별 지침 (UI와 Windows PowerShell 사용)이이 시나리오를 구현에 대 한 설명 [연습 가이드: 위험 액세스 제어 조건으로 관리](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)합니다. 이 연습의 단계를 완료 하기 위해 환경을 설정 하 고 해야 단계에 따라 [랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

### <a name="advanced-scenarios"></a>고급 시나리오
Windows Server 2012 r 2에서 adfs에서 조건부 액세스 제어 구현 하는 기타 예는 다음과 같습니다.

-   이 사용자의이 id를 검증 MFA 된 경우에 Adfs로 보호 응용 프로그램에 대 한 액세스를 허용 합니다.

    다음 코드를 사용할 수 있습니다.

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "PermitAccessWithMFA"
    c:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)https://schemas\.microsoft\.com/claims/multipleauthn$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   ADFS 하 여 사용자에 게 액세스 요청 회사 결합된 장치를 등록 되어에서 발생 하는 경우에 보안을 유지 하는 응용 프로그램에 대 한 액세스를 허용 합니다.

    다음 코드를 사용할 수 있습니다.

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "PermitAccessFromRegisteredWorkplaceJoinedDevice"
    c:[Type == "https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", Value =~ "^(?i)true$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   액세스 요청 MFA와 id를 검증 된 사용자에 게 회사 결합된 장치를 등록 되어에서 발생 하는 경우에 Adfs로 보호 응용 프로그램에 대 한 액세스를 허용 합니다.

    다음 코드를 사용할 수 있습니다.

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "RequireMFAOnRegisteredWorkplaceJoinedDevice"
    c1:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$"] &&
    c2:[Type == "https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", Value =~ "^(?i)true$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   액세스 요청 MFA와 id를 검증 된 사용자에서 발생 하는 경우에 Adfs로 보호 응용 프로그램에 엑스트라넷 액세스할 수 있습니다.

    다음 코드를 사용할 수 있습니다.

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "RequireMFAForExtranetAccess"
    c1:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$"] &&
    c2:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value =~ "^(?i)false$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

## <a name="see-also"></a>참조 하십시오
[연습 가이드: 관련 된 위험 액세스 제어 조건으로 관리](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)<ph x="2">
</ph>[랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



