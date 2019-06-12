---
ms.assetid: ''
title: Active Directory Federation Services 2.0에서 클라이언트 액세스 제어 정책
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 036d6d0543687e7f82caf3dfd2c3bb0b4a981181
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445054"
---
# <a name="client-access-control-policies-in-ad-fs-20"></a>AD FS 2.0에서에서 클라이언트 액세스 제어 정책
Active Directory Federation Services 2.0에서 클라이언트 액세스 정책 제한 하거나 리소스에 대 한 사용자 액세스 권한을 부여 할 수 있습니다.  이 문서에는 AD FS 2.0에서에서 클라이언트 액세스 정책을 사용 하도록 설정 하는 방법 및 가장 일반적인 시나리오를 구성 하는 방법을 설명 합니다.

## <a name="enabling-client-access-policy-in-ad-fs-20"></a>AD FS 2.0에서에서 클라이언트 액세스 정책 사용

클라이언트 액세스 정책을 사용 하려면 다음 단계를 수행 합니다.

### <a name="step-1-install-the-update-rollup-2-for-ad-fs-20-package-on-your-ad-fs-servers"></a>1단계: AD FS 서버에서 AD FS 2.0에 대 한 업데이트 롤업 2 패키지 설치

다운로드 합니다 [Active Directory Federation Services (AD FS)에 대 한 업데이트 롤업 2 2.0](https://support.microsoft.com/en-us/help/2681584/description-of-update-rollup-2-for-active-directory-federation-services-ad-fs-2.0) 패키지 하 고 모든 페더레이션 서버 및 페더레이션 서버 프록시에 설치 합니다.

### <a name="step-2-add-five-claim-rules-to-the-active-directory-claims-provider-trust"></a>2단계: 5 개의 클레임 규칙 Active Directory 클레임 공급자 트러스트 추가

모든 프록시 및 AD FS 서버에서 업데이트 롤업 2를 설치한 후 새 클레임 형식을 정책 엔진을 사용할 수 있도록 클레임 규칙의 집합을 추가 하려면 다음 절차를 따르십시오.

이렇게 하려면 추가 5 수용 변환 규칙 다음 절차를 사용 하 여 새 요청 컨텍스트 클레임 유형 각각에 대 한 합니다.

Active Directory 클레임 공급자 트러스트에서 각 새 요청 컨텍스트 클레임 유형 통과 하도록 새 수용 변환 규칙을 만듭니다.

#### <a name="to-add-a-claim-rule-to-the-active-directory-claims-provider-trust-for-each-of-the-five-context-claim-types"></a>Active Directory에 클레임 규칙을 추가 하려면 5 컨텍스트의 각 클레임 공급자 트러스트에 클레임 유형:


1. 시작, 프로그램, 관리 도구를 누르고 다음 AD FS 2.0 관리 합니다.
2. AD FS 2.0\Trust Relationships 아래 콘솔 트리에서 클레임 공급자 트러스트를 클릭 하 고 Active Directory를 마우스 오른쪽 단추로 클릭 클레임 규칙 편집을 클릭 합니다.
3. 클레임 규칙 편집 대화 상자에서 수용 변환 규칙 탭을 선택 하 고 규칙 마법사를 시작 하려면 규칙 추가 클릭 합니다.
4. 클레임 규칙 템플릿 아래 규칙 템플릿 선택 페이지에서 통과 선택 또는 목록에서 들어오는 클레임을 필터링 하 고 클릭 합니다.
5. 규칙 구성 페이지에서 클레임 규칙 이름 아래의;이 규칙에 대 한 표시 이름 입력 들어오는 클레임 유형, 다음 클레임 형식 URL을 입력 하 고 모든 클레임 값 통과 선택 합니다.</br>
        `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`</br>
6. 규칙을 확인 하려면 목록에서 선택 하 고 규칙 편집 후 규칙 언어 보기를 클릭 합니다. 클레임 규칙 언어는 다음과 같이 표시 됩니다. `c:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip"] => issue(claim = c);`
7. 마침을 클릭 합니다.
8. 클레임 규칙 편집 대화 상자에서 규칙을 저장 하려면 확인을 클릭 합니다.
9. 2 단계에서 만든 모든 5 개 규칙이 될 때까지 아래 나머지 4 개의 클레임 형식 중 각각에 대해 추가 클레임 규칙을 만들려면 6 단계를 반복 합니다.

    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`


~~~
`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`
~~~

### <a name="step-3-update-the-microsoft-office-365-identity-platform-relying-party-trust"></a>3단계: Microsoft Office 365 Id 플랫폼 신뢰 당사자 트러스트를 업데이트 합니다.

예제 시나리오에서는 신뢰 당사자 트러스트는 조직의 요구에 가장 부합 하는 Microsoft Office 365 Id 플랫폼에 클레임 규칙을 구성 하려면 다음 중 하나를 선택 합니다.

## <a name="client-access-policy-scenarios-for-ad-fs-20"></a>AD FS 2.0에 대 한 클라이언트 액세스 정책 시나리오
다음 섹션에서는 AD FS 2.0에 대 한 존재 하는 시나리오를 설명 하는

### <a name="scenario-1-block-all-external-access-to-office-365"></a>시나리오 1: Office 365에 대 한 모든 외부 액세스를 차단 합니다.

이 클라이언트 액세스 정책 시나리오는 외부 클라이언트의 IP 주소를 기반으로 하는 모든 외부 클라이언트가 모든 내부 클라이언트 및 블록에서 액세스를 허용 합니다. 규칙 집합을 모든 사용자에 게 액세스 허용 기본 발급 권한 부여 규칙을 기반으로 합니다. Office 365 신뢰 당사자 트러스트에 발급 권한 부여 규칙을 추가 하려면 다음 절차를 사용할 수 있습니다.

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365"></a>Office 365에 대 한 모든 외부 액세스를 차단 하는 규칙을 만들려면



1. 시작, 프로그램, 관리 도구를 누르고 다음 AD FS 2.0 관리 합니다.
2. AD FS 2.0\Trust Relationships 아래 콘솔 트리에서 신뢰 당사자 트러스트를 클릭 하 고 Microsoft Office 365 Id 플랫폼 신뢰를 마우스 오른쪽 단추로 클릭 클레임 규칙 편집을 클릭 합니다. 
3. 클레임 규칙 편집 대화 상자에서 발급 권한 부여 규칙 탭을 선택한 다음 클레임 규칙 마법사를 시작 하려면 규칙 추가 클릭 합니다.
4. 클레임 규칙 템플릿 아래 규칙 템플릿 선택 페이지에서 사용자 지정 규칙을 클레임으로 보내기 선택 하 고 클릭 합니다.
5. 클레임 규칙 이름 아래에 있는 규칙 구성 페이지에서이 규칙에 대 한 표시 이름을 입력 합니다. 사용자 지정 규칙을 입력 하거나 다음 클레임 규칙 언어 구문을 붙여넣습니다. `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");` 
6. 마침을 클릭 합니다. 액세스 허용 발급 권한 부여 규칙 목록에 있는 모든 사용자 규칙 아래 새 규칙이 즉시 표시 되는지 확인 합니다.
7. 클레임 규칙 편집 대화 상자에서 규칙을 저장 하려면 확인을 클릭 합니다.

>[!NOTE]
>유효한 IP 식; "공용 ip 주소 regex"에 대 한 위의 값으로 대체 해야 합니다. 자세한 정보에 대 한 IP 주소 범위 식 작성을 참조 하세요.


### <a name="scenario-2-block-all-external-access-to-office-365-except-exchange-activesync"></a>시나리오 2: Exchange ActiveSync를 제외 하 고 Office 365에 대 한 모든 외부 액세스를 차단 합니다.

다음 예제에는 Outlook을 비롯 한 내부 클라이언트에서 Exchange Online을 비롯 한 모든 Office 365 응용 프로그램에 액세스할 수 있습니다. 클라이언트 IP 주소를 제외 하 고 스마트폰 등의 Exchange ActiveSync 클라이언트에 표시 된 대로 회사 네트워크 외부에 상주 하는 클라이언트에서 액세스를 차단 합니다. 규칙 집합을 모든 사용자에 게 액세스 허용 이라는 기본 발급 권한 부여 규칙을 기반으로 합니다. 신뢰 당사자 트러스트 클레임 규칙 마법사를 사용 하 여 Office 365에 발급 권한 부여 규칙을 추가 하려면 다음 단계를 사용 합니다.

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365"></a>Office 365에 대 한 모든 외부 액세스를 차단 하는 규칙을 만들려면



1. 시작, 프로그램, 관리 도구를 누르고 다음 AD FS 2.0 관리 합니다.
2. AD FS 2.0\Trust Relationships 아래 콘솔 트리에서 신뢰 당사자 트러스트를 클릭 하 고 Microsoft Office 365 Id 플랫폼 신뢰를 마우스 오른쪽 단추로 클릭 클레임 규칙 편집을 클릭 합니다. 
3. 클레임 규칙 편집 대화 상자에서 발급 권한 부여 규칙 탭을 선택한 다음 클레임 규칙 마법사를 시작 하려면 규칙 추가 클릭 합니다.
4. 클레임 규칙 템플릿 아래 규칙 템플릿 선택 페이지에서 사용자 지정 규칙을 클레임으로 보내기 선택 하 고 클릭 합니다.
5. 클레임 규칙 이름 아래에 있는 규칙 구성 페이지에서이 규칙에 대 한 표시 이름을 입력 합니다. 사용자 지정 규칙을 입력 하거나 다음 클레임 규칙 언어 구문을 붙여넣습니다. `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application",
    Value=="Microsoft.Exchange.Autodiscover"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application",
    Value=="Microsoft.Exchange.ActiveSync"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. 마침을 클릭 합니다. 액세스 허용 발급 권한 부여 규칙 목록에 있는 모든 사용자 규칙 아래 새 규칙이 즉시 표시 되는지 확인 합니다.
7. 클레임 규칙 편집 대화 상자에서 규칙을 저장 하려면 확인을 클릭 합니다.

>[!NOTE]
>유효한 IP 식; "공용 ip 주소 regex"에 대 한 위의 값으로 대체 해야 합니다. 자세한 정보에 대 한 IP 주소 범위 식 작성을 참조 하세요.

### <a name="scenario-3-block-all-external-access-to-office-365-except-browser-based-applications"></a>시나리오 3: 브라우저 기반 응용 프로그램을 제외한 Office 365에 모든 외부 액세스를 차단 합니다.

규칙 집합을 모든 사용자에 게 액세스 허용 이라는 기본 발급 권한 부여 규칙을 기반으로 합니다. 신뢰 당사자 트러스트 클레임 규칙 마법사를 사용 하 여 Microsoft Office 365 Id 플랫폼에 발급 권한 부여 규칙을 추가 하려면 다음 단계를 사용 합니다.

>[!NOTE]
>이 시나리오는 제 3 자 프록시를 사용 하 여 수동 (웹 기반) 요청을 사용 하 여 클라이언트 액세스 정책 헤더에 대 한 제한으로 인해 지원 되지 않습니다.

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>브라우저 기반 응용 프로그램을 제외한 Office 365에 모든 외부 액세스를 차단 하는 규칙을 만들려면



1. 시작, 프로그램, 관리 도구를 누르고 다음 AD FS 2.0 관리 합니다.
2. AD FS 2.0\Trust Relationships 아래 콘솔 트리에서 신뢰 당사자 트러스트를 클릭 하 고 Microsoft Office 365 Id 플랫폼 신뢰를 마우스 오른쪽 단추로 클릭 클레임 규칙 편집을 클릭 합니다. 
3. 클레임 규칙 편집 대화 상자에서 발급 권한 부여 규칙 탭을 선택한 다음 클레임 규칙 마법사를 시작 하려면 규칙 추가 클릭 합니다.
4. 클레임 규칙 템플릿 아래 규칙 템플릿 선택 페이지에서 사용자 지정 규칙을 클레임으로 보내기 선택 하 고 클릭 합니다.
5. 클레임 규칙 이름 아래에 있는 규칙 구성 페이지에서이 규칙에 대 한 표시 이름을 입력 합니다. 사용자 지정 규칙을 입력 하거나 다음 클레임 규칙 언어 구문을 붙여넣습니다. `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value == "/adfs/ls/"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. 마침을 클릭 합니다. 액세스 허용 발급 권한 부여 규칙 목록에 있는 모든 사용자 규칙 아래 새 규칙이 즉시 표시 되는지 확인 합니다.
7. 클레임 규칙 편집 대화 상자에서 규칙을 저장 하려면 확인을 클릭 합니다.

### <a name="scenario-4-block-all-external-access-to-office-365-for-designated-active-directory-groups"></a>시나리오 4: 지정 된 Active Directory 그룹에 대 한 Office 365에 모든 외부 액세스를 차단 합니다.

다음 예제에서는 IP 주소를 기반으로 하는 내부 클라이언트에서 액세스할 수 있도록 합니다. 외부 클라이언트 IP 주소를 포함 하는 회사 네트워크 외부에 상주 하는 클라이언트에서 액세스를 차단, 지정된 된 Active Directory 그룹 규칙에는 개인 제외 하 고 집합 기반에 대 한 액세스 허용 이라는 기본 발급 권한 부여 규칙 모든 사용자입니다. 신뢰 당사자 트러스트 클레임 규칙 마법사를 사용 하 여 Microsoft Office 365 Id 플랫폼에 발급 권한 부여 규칙을 추가 하려면 다음 단계를 사용 합니다.

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365-for-designated-active-directory-groups"></a>지정 된 Active Directory 그룹에 대 한 Office 365에 모든 외부 액세스를 차단 하는 규칙을 만들려면



1. 시작, 프로그램, 관리 도구를 누르고 다음 AD FS 2.0 관리 합니다.
2. AD FS 2.0\Trust Relationships 아래 콘솔 트리에서 신뢰 당사자 트러스트를 클릭 하 고 Microsoft Office 365 Id 플랫폼 신뢰를 마우스 오른쪽 단추로 클릭 클레임 규칙 편집을 클릭 합니다. 
3. 클레임 규칙 편집 대화 상자에서 발급 권한 부여 규칙 탭을 선택한 다음 클레임 규칙 마법사를 시작 하려면 규칙 추가 클릭 합니다.
4. 클레임 규칙 템플릿 아래 규칙 템플릿 선택 페이지에서 사용자 지정 규칙을 클레임으로 보내기 선택 하 고 클릭 합니다.
5. 클레임 규칙 이름 아래에 있는 규칙 구성 페이지에서이 규칙에 대 한 표시 이름을 입력 합니다. 사용자 지정 규칙을 입력 하거나 다음 클레임 규칙 언어 구문을 붙여넣습니다. `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "Group SID value of allowed AD group"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. 마침을 클릭 합니다. 액세스 허용 발급 권한 부여 규칙 목록에 있는 모든 사용자 규칙 아래 새 규칙이 즉시 표시 되는지 확인 합니다.
7. 클레임 규칙 편집 대화 상자에서 규칙을 저장 하려면 확인을 클릭 합니다.


### <a name="descriptions-of-the-claim-rule-language-syntax-used-in-the-above-scenarios"></a>위의 시나리오에 사용 되는 클레임 규칙 언어 구문 설명

|                                                                                                   설명                                                                                                   |                                                                     클레임 규칙 언어 구문                                                                     |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              기본 AD FS 규칙을 모든 사용자에 게 액세스를 허용 합니다. 이 규칙 Microsoft Office 365 Id 플랫폼 신뢰 당사자 트러스트에 발급 권한 부여 규칙 목록에에서 이미 있어야 합니다.              |                                  => issue(Type = "<https://schemas.microsoft.com/authorization/claims/permit>", Value = "true");                                   |
|                               페더레이션 서버 프록시에서 요청에 나오도록 지정이 절이 새, 사용자 지정 규칙을 추가 (즉,이 x-ms-프록시 헤더 있음)                                |                                                                                                                                                                    |
|                                                                                 모든 규칙을 포함 하는 것이 좋습니다.                                                                                  |                                    exists([Type == "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy>"])                                    |
|                                                         요청 허용 되는 정의 된 범위에서 IP 사용 하 여 클라이언트에서 설정 하는 데 사용 합니다.                                                         | 없음 ([유형 = = "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip>", 값 = ~ "고객이 제공한 공용 ip 주소 regex"]) |
|                                    이 절을 사용 하 여 액세스 하는 응용 프로그램 Microsoft.Exchange.ActiveSync 없는 경우 요청은 거부 될 할지 지정 하려면.                                     |       NOT exists([Type == "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application>", Value=="Microsoft.Exchange.ActiveSync"])        |
|                                                      이 규칙을 사용 하면 호출 된 웹 브라우저를 통해 거부 되지 됩니다 있는지 여부를 확인 하는 수 있습니다.                                                      |              NOT exists([Type == "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path>", Value == "/adfs/ls/"])               |
| 이 규칙에 따르면 (SID 값에 따라)를 사용 하 여 특정 Active Directory 그룹의 사용자만을 거부 하도록 해야 합니다. 이 문은 필요가 추가 위치에 관계 없이 사용자 그룹을 허용 하는 것을 의미 합니다. |             exists([Type == "<https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid>", Value =~ "{Group SID value of allowed AD group}"])              |
|                                                                이 모든 이전 조건이 충족 되 면 deny를 실행할 필요는 절.                                                                 |                                   => issue(Type = "<https://schemas.microsoft.com/authorization/claims/deny>", Value = "true");                                    |

### <a name="building-the-ip-address-range-expression"></a>IP 주소 범위 식 작성

클레임 x-ms-전달-클라이언트-ip는 현재 Exchange Online을 AD fs 인증 요청을 전달 하는 경우 헤더를 채우는 의해서만 설정 된 HTTP 헤더에서 채워집니다. 클레임의 값 중 하나일 수 있습니다.

>[!Note] 
>현재 Exchange Online는 IPV4 및 IPV6 하지 주소만 지원합니다.

단일 IP 주소: Exchange Online에 직접 연결 된 클라이언트의 IP 주소

>[!Note] 
>회사 네트워크에서 클라이언트의 IP 주소는 조직의 아웃 바운드 프록시 또는 게이트웨이의 외부 인터페이스 IP 주소로 표시 됩니다.

클라이언트는 VPN을 통해 또는에서 Microsoft DA (DirectAccess) 회사 네트워크에 연결 된 VPN 또는 da. 구성에 따라 외부 클라이언트 또는 내부 회사 클라이언트로 나타날 수 있습니다.

하나 이상의 IP 주소: Exchange Online는 연결 중인 클라이언트의 IP 주소를 확인할 수 없습니다, 하는 경우 x-전달 기능에 대 한 헤더의 HTTP 기반 요청에 포함 될 수 있으며 많은 클라이언트에 부하 분산 장치에서 사용할 수 있는 비표준 헤더 값을 기반으로 하는 값 설정 및 시장에서 프록시입니다.

>[!Note]
>클라이언트 IP 주소 및 요청을 전달 하는 각 프록시 주소를 나타내는 여러 IP 주소를 쉼표로 구분 됩니다.

Exchange Online 인프라와 관련 된 IP 주소 목록에 나타나지 않습니다.


#### <a name="regular-expressions"></a>정규식

범위의 IP 주소와 일치 하는 경우에 비교를 수행 하는 정규식을 생성 하는 데 필요한 됩니다. 다음 일련의 단계에서 다음 주소 범위 (공용 IP 범위를 일치 하도록 이러한 예제를 변경 해야 하는 참고)에 맞게 이러한 식을 구성 하는 방법에 대 한 예제가 제공 됩니다.


- 192.168.1.1 – 192.168.1.25
- 10.0.0.1 – 10.0.0.14

먼저 단일 IP 주소를 일치 하는 기본적인 패턴은 다음과 같습니다: \b###\.###\.###\.# # # \b

이 확장을 일치 시킬 수는 OR 식으로 서로 다른 두 IP 주소 같이: \b###\.###\.###\.# # # \b|\b###\. ### \. ### \.# # # \b

따라서 두 주소 (예: 192.168.1.1 또는 10.0.0.1)와 일치 하는 예제는 것: \b192\.168\.1\.1\b | \b10\.0\.0\.1\b

이는 임의 개수의 주소를 입력할 수 있습니다 하는 기술을 제공 합니다. 주소 범위 예: 192.168.1.1 – 192.168.1.25를 허용 해야 하는 경우 일치 하는 수행 해야 문자로 문자: \b192\.168\.1\.([1-9] | [0-9] 1 | 2 [0-5]) \b

>[!Note] 
>IP 주소 문자열 및 숫자가 아닌로 처리 됩니다.


규칙은 다음과 같이 세분화: \b192\.168\.1\.

이 모든 값부터 192.168.1 일치합니다.

다음은 마지막 소수점 뒤의 주소 부분에 필요한 범위 일치 합니다.


- 1-9로 끝나는 ([1-9] 일치 주소
- | [0-9] 1 개의 10-19로 끝나는 주소와 일치
- 20-25 끝나는 |2[0-5]) 일치 주소

>[!Note]
>괄호 올바르게 배치 해야, 일치 하는 다른 부분 IP 주소를 시작 하지 않습니다.

일치 하는 192 블록을 사용 하 여 10 개 블록에 대 한 유사한 식을 작성할 수 있습니다: \b10\.0\.0\.([1-9] | [0-4] 1) \b

와 함께 배치 하, 다음 식은 같아야 "192.168.1.1~25" 및 "10.0.0.1~14"에 대 한 모든 주소: \b192\.168\.1\.([1-9] | [0-9] 1 | 2 [0-5]) \b|\b10\.0\.0\. ([1-9] | [0-4] 1) \b

#### <a name="testing-the-expression"></a>식 테스트

Regex 식을 상당히 까다로운 될 수 있으므로 regex 확인 도구를 사용 하는 것이 좋습니다. "온라인 regex 식 작성기"에 대 한 인터넷을 검색 하면 샘플 데이터에 대 한 식을 실행 해 볼 수 있도록 몇 가지 좋은 온라인 유틸리티를 찾을 수 있습니다.

식을 테스트 하는 경우는 일치 하는 데 예상 되는 상황을 파악 하는 것입니다. Exchange 온라인 시스템에는 쉼표로 구분 하 여 여러 IP 주소를 보낼 수 있습니다. 위에 제공 된 식이이 작동 합니다. 그러나 regex 식을 테스트 하는 경우이 대해 생각 하는 것이 반드시 합니다. 예를 들어 위의 예제를 확인 하려면 입력 다음 샘플을 사용할 수 있습니다 하나. 

192.168.1.1, 192.168.1.2, 192.169.1.1. 192.168.12.1, 192.168.1.10, 192.168.1.25, 192.168.1.26, 192.168.1.30, 1192.168.1.20 

10.0.0.1, 10.0.0.5, 10.0.0.10, 10.0.1.0, 10.0.1.1, 110.0.0.1, 10.0.0.14, 10.0.0.15, 10.0.0.10, 10,0.0.1 











## <a name="validating-the-deployment"></a>배포 유효성 검사

### <a name="security-audit-logs"></a>보안 감사 로그

새 요청 컨텍스트 클레임 전송 되 고 AD FS를 사용할 수 있는 클레임 처리 파이프라인 있는지를 확인 하려면 AD FS 서버에 로그온 하는 감사를 사용 하도록 설정 합니다. 그런 다음 표준 보안 감사 로그 항목에 몇 가지 인증 요청 및 클레임 값에 대 한 검사를 보냅니다. 

AD FS 서버에서 보안 이벤트 로그에 기록 하는 감사 로깅을 사용 하려면 AD FS 2.0에 대 한 감사 구성에 단계를 수행 합니다.

### <a name="event-logging"></a>이벤트 로깅

기본적으로 실패 한 요청은 응용 프로그램 및 서비스 로그 아래에 있는 응용 프로그램 이벤트 로그에 기록 됩니다 \ AD FS 2.0 \ Admin.For AD FS에 대 한 이벤트 로깅에 대 한 자세한 내용은 참조 하십시오 [AD 설정 FS 2.0 이벤트 로깅](https://technet.microsoft.com/library/adfs2-troubleshooting-configuring-computers.aspx)합니다.

### <a name="configuring-verbose-ad-fs-tracing-logs"></a>자세한 정보 표시 AD FS 추적 로그를 구성 합니다.

AD FS 추적 이벤트는 AD FS 2.0 디버그 로그에 기록 됩니다. 추적을 사용 하려면 참조 [AD FS 2.0에 대 한 디버그 추적 구성](https://technet.microsoft.com/library/adfs2-troubleshooting-configuring-computers.aspx)합니다.

추적을 사용 하도록 설정 하면 자세한 로깅 수준을 사용 하도록 설정 하려면 다음 명령줄 구문을 사용 합니다: wevtutil.exe sl "AD FS 2.0 추적/디버그" /l:5  

## <a name="related"></a>관련 항목
새 클레임 유형에 대 한 자세한 내용은 참조 하세요 [AD FS 클레임 유형](AD-FS-Claims-Types.md)합니다.

