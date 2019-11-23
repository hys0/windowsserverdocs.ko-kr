---
ms.assetid: ''
title: Active Directory Federation Services 2.0의 클라이언트 Access Control 정책
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b0d6133a6fb43b8624dc1329db632fb5dd4aa070
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358446"
---
# <a name="client-access-control-policies-in-ad-fs-20"></a>AD FS 2.0의 클라이언트 Access Control 정책
Active Directory Federation Services 2.0의 클라이언트 액세스 정책을 사용 하 여 리소스에 대 한 액세스를 제한 하거나 사용자에 게 부여할 수 있습니다.  이 문서에서는 AD FS 2.0에서 클라이언트 액세스 정책을 사용 하도록 설정 하는 방법 및 가장 일반적인 시나리오를 구성 하는 방법을 설명 합니다.

## <a name="enabling-client-access-policy-in-ad-fs-20"></a>AD FS 2.0에서 클라이언트 액세스 정책 사용

클라이언트 액세스 정책을 사용 하도록 설정 하려면 다음 단계를 수행 합니다.

### <a name="step-1-install-the-update-rollup-2-for-ad-fs-20-package-on-your-ad-fs-servers"></a>1 단계: AD FS 서버에 AD FS 2.0 패키지에 대 한 업데이트 롤업 2 설치

[Active Directory Federation Services (AD FS) 2.0 용 업데이트 롤업 2](https://support.microsoft.com/en-us/help/2681584/description-of-update-rollup-2-for-active-directory-federation-services-ad-fs-2.0) 패키지를 다운로드 하 고 모든 페더레이션 서버 및 페더레이션 서버 프록시에 설치 합니다.

### <a name="step-2-add-five-claim-rules-to-the-active-directory-claims-provider-trust"></a>2 단계: 클레임 공급자 트러스트 Active Directory 5 개 클레임 규칙 추가

모든 AD FS 서버 및 프록시에 업데이트 롤업 2를 설치한 후에는 다음 절차를 사용 하 여 새 클레임 유형을 정책 엔진에 사용할 수 있도록 하는 클레임 규칙 집합을 추가 합니다.

이렇게 하려면 다음 절차를 사용 하 여 새로운 각 요청 컨텍스트 클레임 유형에 대해 5 개의 수락 변환 규칙을 추가 합니다.

Active Directory 된 클레임 공급자 트러스트에서 새로운 각 요청 컨텍스트 클레임 유형을 통과 하는 새 승인 변환 규칙을 만듭니다.

#### <a name="to-add-a-claim-rule-to-the-active-directory-claims-provider-trust-for-each-of-the-five-context-claim-types"></a>5 가지 컨텍스트 클레임 유형에 대 한 클레임 규칙을 Active Directory 클레임 공급자 트러스트에 추가 하려면 다음을 수행 합니다.


1. 시작을 클릭 하 고 프로그램, 관리 도구를 차례로 가리킨 다음 AD FS 2.0 관리를 클릭 합니다.
2. 콘솔 트리의 AD FS 2.0 \ 트러스트 관계에서 클레임 공급자 트러스트를 클릭 하 고 Active Directory을 마우스 오른쪽 단추로 클릭 한 다음 클레임 규칙 편집을 클릭 합니다.
3. 클레임 규칙 편집 대화 상자에서 수용 변환 규칙 탭을 선택한 다음 규칙 추가를 클릭 하 여 규칙 마법사를 시작 합니다.
4. 규칙 템플릿 선택 페이지의 클레임 규칙 템플릿에서 들어오는 클레임 통과 또는 필터링을 선택 하 고 다음을 클릭 합니다.
5. 규칙 구성 페이지의 클레임 규칙 이름에이 규칙에 대 한 표시 이름을 입력 합니다. 들어오는 클레임 형식에 다음 클레임 유형 URL을 입력 하 고 모든 클레임 값 통과를 선택 합니다.</br>
        `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`</br>
6. 규칙을 확인 하려면 목록에서 규칙을 선택 하 고 규칙 편집을 클릭 한 다음 규칙 언어 보기를 클릭 합니다. 클레임 규칙 언어는 다음과 같이 표시 되어야 합니다. `c:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip"] => issue(claim = c);`
7. 마침을 클릭 합니다.
8. 클레임 규칙 편집 대화 상자에서 확인을 클릭 하 여 규칙을 저장 합니다.
9. 2 ~ 6 단계를 반복 하 여 5 개의 규칙을 모두 만들 때까지 아래에 표시 된 나머지 4 개의 클레임 유형에 대해 추가 클레임 규칙을 만듭니다.

    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`


~~~
`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`
~~~

### <a name="step-3-update-the-microsoft-office-365-identity-platform-relying-party-trust"></a>3 단계: Microsoft Office 365 Id 플랫폼 신뢰 당사자 트러스트 업데이트

조직의 요구에 가장 부합 하는 Microsoft Office 365 Id 플랫폼 신뢰 당사자 트러스트에 대 한 클레임 규칙을 구성 하려면 아래 예제 시나리오 중 하나를 선택 합니다.

## <a name="client-access-policy-scenarios-for-ad-fs-20"></a>AD FS 2.0에 대 한 클라이언트 액세스 정책 시나리오
다음 섹션에서는 AD FS 2.0에 대해 존재 하는 시나리오를 설명 합니다.

### <a name="scenario-1-block-all-external-access-to-office-365"></a>시나리오 1: Office 365에 대 한 모든 외부 액세스 차단

이 클라이언트 액세스 정책 시나리오에서는 모든 내부 클라이언트의 액세스를 허용 하 고 외부 클라이언트의 IP 주소에 따라 모든 외부 클라이언트를 차단 합니다. 기본 발급 권한 부여 규칙을 기반으로 하는 규칙 집합은 모든 사용자에 대 한 액세스를 허용 합니다. 다음 절차를 사용 하 여 Office 365 신뢰 당사자 트러스트에 발급 권한 부여 규칙을 추가할 수 있습니다.

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365"></a>Office 365에 대 한 모든 외부 액세스를 차단 하는 규칙을 만들려면



1. 시작을 클릭 하 고 프로그램, 관리 도구를 차례로 가리킨 다음 AD FS 2.0 관리를 클릭 합니다.
2. 콘솔 트리의 AD FS 2.0 \ 트러스트 관계에서 신뢰 당사자 트러스트를 클릭 하 고 Microsoft Office 365 Id 플랫폼 트러스트를 마우스 오른쪽 단추로 클릭 한 다음 클레임 규칙 편집을 클릭 합니다. 
3. 클레임 규칙 편집 대화 상자에서 발급 권한 부여 규칙 탭을 선택한 다음 규칙 추가를 클릭 하 여 클레임 규칙 마법사를 시작 합니다.
4. 규칙 템플릿 선택 페이지의 클레임 규칙 템플릿에서 사용자 지정 규칙을 사용 하 여 클레임 보내기를 선택 하 고 다음을 클릭 합니다.
5. 규칙 구성 페이지의 클레임 규칙 이름에이 규칙에 대 한 표시 이름을 입력 합니다. 사용자 지정 규칙에서 다음 클레임 규칙 언어 구문을 입력 하거나 붙여 넣습니다. `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");` 
6. 마침을 클릭 합니다. 새 규칙이 발급 권한 부여 규칙 목록의 모든 사용자에 게 액세스 허용 규칙 바로 아래에 표시 되는지 확인 합니다.
7. 규칙을 저장 하려면 클레임 규칙 편집 대화 상자에서 확인을 클릭 합니다.

>[!NOTE]
>"공용 ip 주소 regex"에 대해 위의 값을 유효한 IP 식으로 바꿔야 합니다. 자세한 내용은 IP 주소 범위 식 작성을 참조 하세요.


### <a name="scenario-2-block-all-external-access-to-office-365-except-exchange-activesync"></a>시나리오 2: Exchange ActiveSync를 제외 하 고 Office 365에 대 한 모든 외부 액세스 차단

다음 예에서는 Outlook을 포함 하 여 내부 클라이언트에서 Exchange Online을 비롯 한 모든 Office 365 응용 프로그램에 액세스할 수 있습니다. 클라이언트 IP 주소에 표시 되는 것 처럼 회사 네트워크 외부에 있는 클라이언트의 액세스를 차단 합니다. 단, 스마트 휴대폰과 같은 Exchange ActiveSync 클라이언트의 경우는 예외입니다. 규칙 집합은 모든 사용자에 대 한 액세스 허용 이라는 기본 발급 권한 부여 규칙을 기반으로 합니다. 클레임 규칙 마법사를 사용 하 여 Office 365 신뢰 당사자 트러스트에 발급 권한 부여 규칙을 추가 하려면 다음 단계를 수행 합니다.

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365"></a>Office 365에 대 한 모든 외부 액세스를 차단 하는 규칙을 만들려면



1. 시작을 클릭 하 고 프로그램, 관리 도구를 차례로 가리킨 다음 AD FS 2.0 관리를 클릭 합니다.
2. 콘솔 트리의 AD FS 2.0 \ 트러스트 관계에서 신뢰 당사자 트러스트를 클릭 하 고 Microsoft Office 365 Id 플랫폼 트러스트를 마우스 오른쪽 단추로 클릭 한 다음 클레임 규칙 편집을 클릭 합니다. 
3. 클레임 규칙 편집 대화 상자에서 발급 권한 부여 규칙 탭을 선택한 다음 규칙 추가를 클릭 하 여 클레임 규칙 마법사를 시작 합니다.
4. 규칙 템플릿 선택 페이지의 클레임 규칙 템플릿에서 사용자 지정 규칙을 사용 하 여 클레임 보내기를 선택 하 고 다음을 클릭 합니다.
5. 규칙 구성 페이지의 클레임 규칙 이름에이 규칙에 대 한 표시 이름을 입력 합니다. 사용자 지정 규칙에서 다음 클레임 규칙 언어 구문을 입력 하거나 붙여 넣습니다. `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application",
    Value=="Microsoft.Exchange.Autodiscover"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application",
    Value=="Microsoft.Exchange.ActiveSync"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. 마침을 클릭 합니다. 새 규칙이 발급 권한 부여 규칙 목록의 모든 사용자에 게 액세스 허용 규칙 바로 아래에 표시 되는지 확인 합니다.
7. 규칙을 저장 하려면 클레임 규칙 편집 대화 상자에서 확인을 클릭 합니다.

>[!NOTE]
>"공용 ip 주소 regex"에 대해 위의 값을 유효한 IP 식으로 바꿔야 합니다. 자세한 내용은 IP 주소 범위 식 작성을 참조 하세요.

### <a name="scenario-3-block-all-external-access-to-office-365-except-browser-based-applications"></a>시나리오 3: 브라우저 기반 응용 프로그램을 제외한 Office 365에 대 한 모든 외부 액세스 차단

규칙 집합은 모든 사용자에 대 한 액세스 허용 이라는 기본 발급 권한 부여 규칙을 기반으로 합니다. 클레임 규칙 마법사를 사용 하 여 Microsoft Office 365 Id 플랫폼 신뢰 당사자 트러스트에 발급 권한 부여 규칙을 추가 하려면 다음 단계를 수행 합니다.

>[!NOTE]
>이 시나리오는 수동 (웹 기반) 요청을 사용 하는 클라이언트 액세스 정책 헤더의 제한 사항으로 인해 타사 프록시에서 지원 되지 않습니다.

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>브라우저 기반 응용 프로그램을 제외한 Office 365에 대 한 모든 외부 액세스를 차단 하는 규칙을 만들려면



1. 시작을 클릭 하 고 프로그램, 관리 도구를 차례로 가리킨 다음 AD FS 2.0 관리를 클릭 합니다.
2. 콘솔 트리의 AD FS 2.0 \ 트러스트 관계에서 신뢰 당사자 트러스트를 클릭 하 고 Microsoft Office 365 Id 플랫폼 트러스트를 마우스 오른쪽 단추로 클릭 한 다음 클레임 규칙 편집을 클릭 합니다. 
3. 클레임 규칙 편집 대화 상자에서 발급 권한 부여 규칙 탭을 선택한 다음 규칙 추가를 클릭 하 여 클레임 규칙 마법사를 시작 합니다.
4. 규칙 템플릿 선택 페이지의 클레임 규칙 템플릿에서 사용자 지정 규칙을 사용 하 여 클레임 보내기를 선택 하 고 다음을 클릭 합니다.
5. 규칙 구성 페이지의 클레임 규칙 이름에이 규칙에 대 한 표시 이름을 입력 합니다. 사용자 지정 규칙에서 다음 클레임 규칙 언어 구문을 입력 하거나 붙여 넣습니다. `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value == "/adfs/ls/"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. 마침을 클릭 합니다. 새 규칙이 발급 권한 부여 규칙 목록의 모든 사용자에 게 액세스 허용 규칙 바로 아래에 표시 되는지 확인 합니다.
7. 규칙을 저장 하려면 클레임 규칙 편집 대화 상자에서 확인을 클릭 합니다.

### <a name="scenario-4-block-all-external-access-to-office-365-for-designated-active-directory-groups"></a>시나리오 4: 지정 된 Active Directory 그룹에 대해 Office 365에 대 한 모든 외부 액세스 차단

다음 예제에서는 IP 주소를 기반으로 하는 내부 클라이언트에서 액세스할 수 있도록 합니다. 지정 된 Active Directory 그룹의 개인을 제외 하 고 외부 클라이언트 IP 주소가 있는 회사 네트워크 외부에 있는 클라이언트의 액세스를 차단 합니다. 규칙 집합은 다음에 대 한 액세스 허용 이라는 제목의 기본 발급 권한 부여 규칙을 기반으로 합니다. 모든 사용자입니다. 클레임 규칙 마법사를 사용 하 여 Microsoft Office 365 Id 플랫폼 신뢰 당사자 트러스트에 발급 권한 부여 규칙을 추가 하려면 다음 단계를 수행 합니다.

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365-for-designated-active-directory-groups"></a>지정 된 Active Directory 그룹에 대해 Office 365에 대 한 모든 외부 액세스를 차단 하는 규칙을 만들려면



1. 시작을 클릭 하 고 프로그램, 관리 도구를 차례로 가리킨 다음 AD FS 2.0 관리를 클릭 합니다.
2. 콘솔 트리의 AD FS 2.0 \ 트러스트 관계에서 신뢰 당사자 트러스트를 클릭 하 고 Microsoft Office 365 Id 플랫폼 트러스트를 마우스 오른쪽 단추로 클릭 한 다음 클레임 규칙 편집을 클릭 합니다. 
3. 클레임 규칙 편집 대화 상자에서 발급 권한 부여 규칙 탭을 선택한 다음 규칙 추가를 클릭 하 여 클레임 규칙 마법사를 시작 합니다.
4. 규칙 템플릿 선택 페이지의 클레임 규칙 템플릿에서 사용자 지정 규칙을 사용 하 여 클레임 보내기를 선택 하 고 다음을 클릭 합니다.
5. 규칙 구성 페이지의 클레임 규칙 이름에이 규칙에 대 한 표시 이름을 입력 합니다. 사용자 지정 규칙에서 다음 클레임 규칙 언어 구문을 입력 하거나 붙여 넣습니다. `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "Group SID value of allowed AD group"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. 마침을 클릭 합니다. 새 규칙이 발급 권한 부여 규칙 목록의 모든 사용자에 게 액세스 허용 규칙 바로 아래에 표시 되는지 확인 합니다.
7. 규칙을 저장 하려면 클레임 규칙 편집 대화 상자에서 확인을 클릭 합니다.


### <a name="descriptions-of-the-claim-rule-language-syntax-used-in-the-above-scenarios"></a>위의 시나리오에서 사용 된 클레임 규칙 언어 구문에 대 한 설명

|                                                                                                   설명                                                                                                   |                                                                     클레임 규칙 언어 구문                                                                     |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              모든 사용자에 대 한 액세스를 허용 하는 기본 AD FS 규칙입니다. 이 규칙은 Microsoft Office 365 Id 플랫폼 신뢰 당사자 트러스트 발급 권한 부여 규칙 목록에 이미 있어야 합니다.              |                                  = > issue (Type = "<https://schemas.microsoft.com/authorization/claims/permit>", Value = "true");                                   |
|                               이 절을 새로운 사용자 지정 규칙에 추가 하면 요청이 페더레이션 서버 프록시에서 온 것으로 지정 됩니다. 즉, x-m 프록시 헤더를 포함 합니다.                                |                                                                                                                                                                    |
|                                                                                 모든 규칙에이를 포함 하는 것이 좋습니다.                                                                                  |                                    exists ([Type = = "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy>"])                                    |
|                                                         지정 된 허용 범위 내에 IP가 있는 클라이언트에서 요청을 하는 것을 설정 하는 데 사용 됩니다.                                                         | 존재 하지 않음 ([Type = = "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip>", 값 = ~ "고객이 제공한 공용 ip 주소 regex"]) |
|                                    이 절을 사용 하 여 액세스 하는 응용 프로그램이 Microsoft. Exchange.                                     |       존재 하지 않음 ([Type = = "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application>", 값 = = "Microsoft. Exchange. ActiveSync"])        |
|                                                      이 규칙을 사용 하면 호출이 웹 브라우저를 통해 발생 했는지 여부를 확인할 수 있으며,이는 거부 되지 않습니다.                                                      |              존재 하지 않음 ([Type = = "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path>", 값 = = "/adfs/ls/"])               |
| 이 규칙은 특정 Active Directory 그룹 (SID 값 기반)의 유일한 사용자를 거부 해야 함을 설명 합니다. 이 문에 NOT을 추가 하면 위치에 관계 없이 사용자 그룹이 허용 됩니다. |             exists ([Type = = "<https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid>", 값 = ~ "{그룹 SID 값이 허용 된 AD 그룹}"])              |
|                                                                위의 조건이 모두 충족 될 때 거부를 발급 하는 필수 절입니다.                                                                 |                                   = > issue (Type = "<https://schemas.microsoft.com/authorization/claims/deny>", Value = "true");                                    |

### <a name="building-the-ip-address-range-expression"></a>IP 주소 범위 식 작성

X AD FS--------------------------------------------------- 클레임의 값은 다음 중 하나일 수 있습니다.

>[!Note] 
>Exchange Online은 현재 IPV4 및 IPV6 주소만 지원 합니다.

단일 IP 주소: Exchange Online에 직접 연결 되는 클라이언트의 IP 주소

>[!Note] 
>회사 네트워크에 있는 클라이언트의 IP 주소는 조직의 아웃 바운드 프록시 또는 게이트웨이의 외부 인터페이스 IP 주소로 표시 됩니다.

Vpn 또는 da의 구성에 따라 VPN 또는 Microsoft DirectAccess (DA)를 통해 회사 네트워크에 연결 된 클라이언트는 내부 회사 클라이언트나 외부 클라이언트로 표시 될 수 있습니다.

하나 이상의 IP 주소: Exchange Online에서 연결 하는 클라이언트의 IP 주소를 확인할 수 없는 경우, HTTP 기반 요청에 포함할 수 있는 비표준 헤더 인 x 전달 된 헤더의 값을 기반으로 값을 설정 합니다. 클라이언트, 부하 분산 장치 및 시장의 프록시.

>[!Note]
>클라이언트 IP 주소와 요청을 전달한 각 프록시의 주소를 나타내는 여러 IP 주소가 쉼표로 구분 됩니다.

Exchange Online 인프라와 관련 된 IP 주소가 목록에 표시 되지 않습니다.


#### <a name="regular-expressions"></a>정규식

IP 주소 범위와 일치 해야 하는 경우 비교를 수행 하는 정규식을 생성 해야 합니다. 다음 일련의 단계에서는 다음 주소 범위와 일치 하도록 이러한 식을 구성 하는 방법에 대 한 예제를 제공 합니다. 공용 IP 범위와 일치 하도록 이러한 예제를 변경 해야 합니다.


- 192.168.1.1 – 192.168.1.25
- 10.0.0.1 – 10.0.0.14

첫째, 단일 IP 주소와 일치 하는 기본 패턴은 다음과 같습니다. \b # # #\.###\.###\.# # # \b

이를 확장 하 여 다음과 같이 두 개의 서로 다른 IP 주소를 또는 식과 일치 시킬 수 있습니다. \b # # #\.###\.###\.# # # \b | \b # # #\.###\.###\.# # # \b

따라서 두 개의 주소 (예: 192.168.1.1 또는 10.0.0.1)만 일치 시키는 예는 \b192\.168\.1\.1 \ b | \b10\.0\.0\.1 \ b입니다.

이렇게 하면 원하는 수의 주소를 입력할 수 있는 방법이 제공 됩니다. 주소 범위 (예: 192.168.1.1 – 192.168.1.25)를 허용 해야 하는 경우 일치 하는 문자: \b192\.168\.1\.([1-9] | 1 [0-9] | 2 [0-5]) \b

>[!Note] 
>IP 주소는 숫자가 아니라 문자열로 처리 됩니다.


이 규칙은 \b192\.168\.1\.와 같이 세분화 됩니다.

이 값은 192.168.1로 시작 하는 모든 값과 일치 합니다.

다음은 마지막 소수점 뒤의 주소 부분에 필요한 범위와 일치 합니다.


- ([1-9] 1-9로 끝나는 주소와 일치
- | 1 [0-9]는 10-19로 끝나는 주소와 일치 합니다.
- | 2 [0-5]) 20-25로 끝나는 주소와 일치 합니다.

>[!Note]
>IP 주소의 다른 부분과 일치 하지 않도록 괄호를 올바르게 배치 해야 합니다.

192 블록 일치를 사용 하 여 10 개의 블록에 대 한 유사한 식을 작성할 수 있습니다. \b10\.0\.0\.([1-9] | 1 [0-4]) \b

그리고 다음 식은 "192.168.1.1 ~ 25" 및 "10.0.0.1 ~ 14"의 모든 주소와 일치 해야 합니다. \b192\.168\.1\.([1-9] | 1 [0-9] | 2 [0-5]) \b | \b10\.0\.0\.([1-9] | 1 [0-4]) \b

#### <a name="testing-the-expression"></a>식 테스트

Regex 식이 매우 복잡할 수 있으므로 regex 확인 도구를 사용 하는 것이 좋습니다. "온라인 regex 식 작성기"에 대해 인터넷 검색을 수행 하는 경우 샘플 데이터에 대해 식을 사용해 볼 수 있도록 하는 몇 가지 좋은 온라인 유틸리티를 찾을 수 있습니다.

식을 테스트할 때 일치 해야 할 것으로 예측 해야 하는 사항을 이해 하는 것이 중요 합니다. Exchange online 시스템은 쉼표로 구분 된 많은 IP 주소를 보낼 수 있습니다. 위에서 제공한 식이이 작업에 대해 작동 합니다. 그러나 regex 식을 테스트할 때이에 대해 생각 하는 것이 중요 합니다. 예를 들어 다음 샘플 입력을 사용 하 여 위의 예제를 확인할 수 있습니다. 

192.168.1.1, 192.168.1.2, 192.169.1.1. 192.168.12.1, 192.168.1.10, 192.168.1.25, 192.168.1.26, 192.168.1.30, 1192.168.1.20 

10.0.0.1, 10.0.0.5, 10.0.0.10, 10.0.1.0, 10.0.1.1, 110.0.0.1, 10.0.0.14, 10.0.0.15, 10.0.0.10, 10, 0.0.1 











## <a name="validating-the-deployment"></a>배포 유효성 검사

### <a name="security-audit-logs"></a>보안 감사 로그

새 요청 컨텍스트 클레임을 보내고 AD FS 클레임 처리 파이프라인에서 사용할 수 있는지 확인 하려면 AD FS 서버에서 감사 로깅을 사용 하도록 설정 합니다. 그런 다음 몇 가지 인증 요청을 보내고 표준 보안 감사 로그 항목에서 클레임 값을 확인 합니다. 

AD FS 서버에서 보안 로그에 감사 이벤트 로깅을 사용 하도록 설정 하려면 AD FS 2.0에 대 한 감사 구성의 단계를 수행 합니다.

### <a name="event-logging"></a>이벤트 로깅

실패 한 요청은 기본적으로 응용 프로그램 및 서비스 로그 \ AD FS 2.0 \ 관리자 아래에 있는 응용 프로그램 이벤트 로그에 기록 됩니다. AD FS에 대 한 이벤트 로깅에 대 한 자세한 내용은 [AD FS 2.0 이벤트 로깅 설정](https://technet.microsoft.com/library/adfs2-troubleshooting-configuring-computers.aspx)을 참조 하세요.

### <a name="configuring-verbose-ad-fs-tracing-logs"></a>자세한 AD FS 추적 로그 구성

AD FS 추적 이벤트는 AD FS 2.0 디버그 로그에 기록 됩니다. 추적을 사용 하도록 설정 하려면 [AD FS 2.0에 대 한 디버그 추적 구성](https://technet.microsoft.com/library/adfs2-troubleshooting-configuring-computers.aspx)을 참조 하세요.

추적을 사용 하도록 설정한 후 다음 명령줄 구문을 사용 하 여 자세한 로깅 수준을 사용 하도록 설정 합니다. wevtutil sl "AD FS 2.0 추적/디버그"/l: 5  

## <a name="related"></a>관련 항목
새 클레임 유형에 대 한 자세한 내용은 [AD FS 클레임 유형](AD-FS-Claims-Types.md)을 참조 하세요.

