---
ms.assetid: 
title: "클라이언트 Active Directory Federation Services 2.0에 대 한 액세스를 제어 정책"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 00b9cd17c7a5c206e06bea12fd90762adb336715
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="client-access-control-policies-in-ad-fs-20"></a>ADFS 2.0에에서 대 한 액세스를 제어 정책 클라이언트
Active Directory Federation Services 2.0에 클라이언트 액세스 정책을 사용을 제한 하거나 리소스를 사용자에 게 액세스 권한을 부여할 수 있습니다.  이 문서는 ADFS 2.0에에서 대 한 액세스 정책 클라이언트를 사용 하는 방법 및 일반적인 가장 시나리오를 구성 하는 방법을 설명 합니다.

## <a name="enabling-client-access-policy-in-ad-fs-20"></a>ADFS 2.0에에서 대 한 액세스 정책을 클라이언트

액세스 정책 클라이언트를 사용 하려면 다음 단계를 수행 합니다.

### <a name="step-1-install-the-update-rollup-2-for-ad-fs-20-package-on-your-ad-fs-servers"></a>ADFS 서버에 설치 ADFS 2.0에 대 한 업데이트 롤업 2 패키지 1 단계:

다운로드는 [Active Directory Federation Services (ADFS)에 대 한 업데이트 롤업 2 2.0](https://support.microsoft.com/en-us/help/2681584/description-of-update-rollup-2-for-active-directory-federation-services-ad-fs-2.0) 패키지 및 모든 federation 서버와 federation 서버 프록시 설치 합니다.

### <a name="step-2-add-five-claim-rules-to-the-active-directory-claims-provider-trust"></a>2 단계: Active Directory 클레임 공급자 신뢰 하는 규칙 주장 5 추가

ADFS 서버 및 프록시의 모든 업데이트 롤업 2를 설치을 추가 하려면 클레임 규칙의 새로운 클레임 유형 정책 엔진을 사용할 수 있게 하는 다음과 같이 합니다.

이렇게 하려면 추가할 것 5 수용 변환 규칙 각 다음 절차에 따라 새 요청 상황에 맞는 클레임 유형에 대 한 합니다.

Active Directory 클레임 공급자 신뢰 각각의 새로운 요청 상황에 맞는 클레임 유형 통과 하는 새 수용 변환을 규칙을 만듭니다.

#### <a name="to-add-a-claim-rule-to-the-active-directory-claims-provider-trust-for-each-of-the-five-context-claim-types"></a>청구 규칙 Active Directory을 추가 하려면 클레임 공급자 신뢰 5 컨텍스트의 각각에 대 한 주장 유형:


1. 시작, 프로그램, 관리 도구 및 광고를 클릭 한 다음 FS 2.0 관리 합니다.
2. 광고 FS 2.0\Trust 관계에서 콘솔 트리에서 클레임 공급자 신뢰, Active Directory를 마우스 오른쪽 단추로 클릭 및 편집 클레임 규칙을 클릭 한 다음 합니다.
3. 편집 클레임 규칙 대화 상자에서 수용 변환 규칙 탭을 선택한 규칙 마법사를 시작 규칙 추가 클릭 합니다.
4. 규칙 템플릿 선택 페이지 청구 규칙 서식 파일 아래에서 통과 선택 하거나 목록에서 수신 클레임 필터링 하 고을 클릭 합니다.
5. 구성 규칙 페이지 클레임 규칙 이름 아래에서이 규칙; 표시 이름을 입력합니다 들어오는 클레임 유형, 다음 청구 유형 URL을 입력 하 고 모든 클레임 값을 통해 전달을 선택 합니다.</br>
        `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`</br>
6. 규칙을 확인 하려면 규칙 편집 목록에서 선택 클릭 보기 규칙 언어를 클릭 합니다. 클레임은 규칙 언어 다음과 같이 나타납니다. `c:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip"] => issue(claim = c);`
7. 마침 클릭 합니다.
8. 편집 클레임 규칙 대화 상자에서 저장 규칙은 확인을 클릭 합니다.
9. 2 단계-각 아래에 표시 된 모든 5 규칙 생성 된 때까지 남은 네 클레임 유형에 대 한 추가 클레임 규칙을 만드는 데 6 단계를 반복 합니다.

    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`


    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`

### <a name="step-3-update-the-microsoft-office-365-identity-platform-relying-party-trust"></a>3 단계: Microsoft Office 365 Id 플랫폼 필요로 하 파티 보안 업데이트

조직의 요구에 가장 잘 맞는 파티 신뢰를 사용 하지 않고 Microsoft Office 365 Id 플랫폼에서 클레임 규칙 구성 하려면 아래의 예제 시나리오 중 하나를 선택 합니다.

## <a name="client-access-policy-scenarios-for-ad-fs-20"></a>ADFS 2.0에 대 한 클라이언트 액세스 정책 시나리오
다음은 ADFS 2.0에 대 한 존재 하는 시나리오 설명

### <a name="scenario-1-block-all-external-access-to-office-365"></a>차단 외부 Office 365에 대 한 모든 시나리오 1:

이 클라이언트 액세스 정책 시나리오 외부 클라이언트의 IP 주소를 기초로 모든 외부 클라이언트 모든 내부 클라이언트 및 블록에서 액세스할 수 있습니다. 기본 발급 승인 규칙 모든 사용자에 액세스 허용에서 빌드를 규칙 설정 합니다. 다음 절차에 의존 파티 신뢰 Office 365 발급 승인 규칙을 추가 하려면 사용할 수 있습니다.

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365"></a>Office 365에 대 한 모든 외부 차단 규칙을 만들려면



1. 시작, 프로그램, 관리 도구 및 광고를 클릭 한 다음 FS 2.0 관리 합니다.
2. 콘솔 트리에서 광고 FS 2.0\Trust 관계에서 자 신뢰를 사용 하지 않고, Microsoft Office 365 Id 플랫폼 신뢰를 마우스 오른쪽 단추로 클릭 및 편집 클레임 규칙을 클릭 한 다음 합니다. 
3. 편집 클레임 규칙 대화 상자에서 발급 승인 규칙 탭을 선택한 클레임 규칙 마법사를 시작 규칙 추가 클릭 합니다.
4. 청구 규칙 템플릿에서 규칙 템플릿 선택 페이지에서 사용자 지정 규칙 보내기 클레임 사용 하 여 선택 하 고을 클릭 합니다.
5. 구성 규칙 페이지 클레임 규칙 이름 아래에서이 규칙의 표시 이름을 입력 합니다. 사용자 지정 규칙 입력 하거나 붙여 다음 청구 규칙 언어 구문을 다음과 같습니다. `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");` 
6. 마침 클릭 합니다. 새 규칙 발급 승인 규칙 목록에서 모든 사용자에 게 규칙에 허용 액세스할 아래 즉시 표시 되는지 확인 합니다.
7. 편집 클레임 규칙 대화 상자에서 규칙을 절약 하기 위해 확인을 클릭 합니다.

>[!NOTE]
>유효한 IP 식;와 위의 "공개 ip 주소 regex"에 대 한 값을 교체 해야 할는 자세한 내용은 IP 주소 범위 식 빌드 참조 합니다.


### <a name="scenario-2-block-all-external-access-to-office-365-except-exchange-activesync"></a>차단 외부 Exchange ActiveSync 제외 하 고 Office 365에 대 한 모든 시나리오 2:

다음 예제 Outlook 등 내부 클라이언트에서 Exchange Online을 비롯 한 모든 Office 365 응용 프로그램에 액세스할 수 있습니다. 회사 네트워크에서 벗어나 있는 거주 하는 클라이언트에서 액세스 클라이언트 IP 주소 같은 스마트폰 Exchange ActiveSync 클라이언트를 제외 하 고에 표시 된 대로 차단 됩니다. 모든 사용자에 액세스 허용 기본 발급 승인 규칙에 빌드 규칙 집합입니다. 다음 단계를 사용 하 여 발급 승인 규칙을 필요로 하 파티 신뢰 클레임 규칙 마법사를 사용 하 여 Office 365를 추가 하려면:

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365"></a>Office 365에 대 한 모든 외부 차단 규칙을 만들려면



1. 시작, 프로그램, 관리 도구 및 광고를 클릭 한 다음 FS 2.0 관리 합니다.
2. 콘솔 트리에서 광고 FS 2.0\Trust 관계에서 자 신뢰를 사용 하지 않고, Microsoft Office 365 Id 플랫폼 신뢰를 마우스 오른쪽 단추로 클릭 및 편집 클레임 규칙을 클릭 한 다음 합니다. 
3. 편집 클레임 규칙 대화 상자에서 발급 승인 규칙 탭을 선택한 클레임 규칙 마법사를 시작 규칙 추가 클릭 합니다.
4. 청구 규칙 템플릿에서 규칙 템플릿 선택 페이지에서 사용자 지정 규칙 보내기 클레임 사용 하 여 선택 하 고을 클릭 합니다.
5. 구성 규칙 페이지 클레임 규칙 이름 아래에서이 규칙의 표시 이름을 입력 합니다. 사용자 지정 규칙 입력 하거나 붙여 다음 청구 규칙 언어 구문을 다음과 같습니다. `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application",
    Value=="Microsoft.Exchange.Autodiscover"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application",
    Value=="Microsoft.Exchange.ActiveSync"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. 마침 클릭 합니다. 새 규칙 발급 승인 규칙 목록에서 모든 사용자에 게 규칙에 허용 액세스할 아래 즉시 표시 되는지 확인 합니다.
7. 편집 클레임 규칙 대화 상자에서 규칙을 절약 하기 위해 확인을 클릭 합니다.

>[!NOTE]
>유효한 IP 식;와 위의 "공개 ip 주소 regex"에 대 한 값을 교체 해야 할는 자세한 내용은 IP 주소 범위 식 빌드 참조 합니다.

### <a name="scenario-3-block-all-external-access-to-office-365-except-browser-based-applications"></a>브라우저 기반 응용 프로그램을 제외 하 고에 Office 365 외부 모든 액세스를 차단 하는 시나리오 3:

모든 사용자에 액세스 허용 기본 발급 승인 규칙에 빌드 규칙 집합입니다. 다음 단계를 사용 하 여 발급 승인 규칙 클레임 규칙 마법사를 사용 하 여 자 신뢰를 사용 하지 않고 Microsoft Office 365 Id 플랫폼에 추가 하려면:

>[!NOTE]
>이 시나리오를 제 3 자 프록시 수동 (웹 기반) 요청 클라이언트 액세스 정책 헤더에 대 한 제한으로 인해 지원 되지 않습니다.

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>브라우저 기반 응용 프로그램을 제외 하 고 모든 외부 액세스 Office 365를 차단 하려면 규칙을 만들려면



1. 시작, 프로그램, 관리 도구 및 광고를 클릭 한 다음 FS 2.0 관리 합니다.
2. 콘솔 트리에서 광고 FS 2.0\Trust 관계에서 자 신뢰를 사용 하지 않고, Microsoft Office 365 Id 플랫폼 신뢰를 마우스 오른쪽 단추로 클릭 및 편집 클레임 규칙을 클릭 한 다음 합니다. 
3. 편집 클레임 규칙 대화 상자에서 발급 승인 규칙 탭을 선택한 클레임 규칙 마법사를 시작 규칙 추가 클릭 합니다.
4. 청구 규칙 템플릿에서 규칙 템플릿 선택 페이지에서 사용자 지정 규칙 보내기 클레임 사용 하 여 선택 하 고을 클릭 합니다.
5. 구성 규칙 페이지 클레임 규칙 이름 아래에서이 규칙의 표시 이름을 입력 합니다. 사용자 지정 규칙 입력 하거나 붙여 다음 청구 규칙 언어 구문을 다음과 같습니다. `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value == "/adfs/ls/"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. 마침 클릭 합니다. 새 규칙 발급 승인 규칙 목록에서 모든 사용자에 게 규칙에 허용 액세스할 아래 즉시 표시 되는지 확인 합니다.
7. 편집 클레임 규칙 대화 상자에서 규칙을 절약 하기 위해 확인을 클릭 합니다.

### <a name="scenario-4-block-all-external-access-to-office-365-for-designated-active-directory-groups"></a>4 시나리오: 지정 된 Active Directory 그룹에 대 한 모든 외부 액세스 Office 365를 차단

이때에는 IP 주소를 기초로 내부 클라이언트에서 액세스할을 수 있습니다. IP 주소가 외부 클라이언트 회사 네트워크에서 벗어나 있는 상주 하는 클라이언트에서 액세스 차단, 사람이 지정된 된 Active Directory Group.The 규칙의 제외한 모든 사용자에 액세스 허용 기본 발급 승인 규칙에서 빌드를 설정 합니다. 다음 단계를 사용 하 여 발급 승인 규칙 클레임 규칙 마법사를 사용 하 여 자 신뢰를 사용 하지 않고 Microsoft Office 365 Id 플랫폼에 추가 하려면:

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365-for-designated-active-directory-groups"></a>지정 된 Active Directory 그룹에 대 한 모든 외부 액세스 Office 365를 차단 하려면 규칙을 만들려면



1. 시작, 프로그램, 관리 도구 및 광고를 클릭 한 다음 FS 2.0 관리 합니다.
2. 콘솔 트리에서 광고 FS 2.0\Trust 관계에서 자 신뢰를 사용 하지 않고, Microsoft Office 365 Id 플랫폼 신뢰를 마우스 오른쪽 단추로 클릭 및 편집 클레임 규칙을 클릭 한 다음 합니다. 
3. 편집 클레임 규칙 대화 상자에서 발급 승인 규칙 탭을 선택한 클레임 규칙 마법사를 시작 규칙 추가 클릭 합니다.
4. 청구 규칙 템플릿에서 규칙 템플릿 선택 페이지에서 사용자 지정 규칙 보내기 클레임 사용 하 여 선택 하 고을 클릭 합니다.
5. 구성 규칙 페이지 클레임 규칙 이름 아래에서이 규칙의 표시 이름을 입력 합니다. 사용자 지정 규칙 입력 하거나 붙여 다음 청구 규칙 언어 구문을 다음과 같습니다. `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "Group SID value of allowed AD group"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. 마침 클릭 합니다. 새 규칙 발급 승인 규칙 목록에서 모든 사용자에 게 규칙에 허용 액세스할 아래 즉시 표시 되는지 확인 합니다.
7. 편집 클레임 규칙 대화 상자에서 규칙을 절약 하기 위해 확인을 클릭 합니다.


### <a name="descriptions-of-the-claim-rule-language-syntax-used-in-the-above-scenarios"></a>청구에 대 한 설명을 위의 시나리오에서 사용 되는 언어 구문 내 마음 대로 사용

|설명|규칙 언어 구문 주장|
|-----|-----| 
|광고 기본 FS 규칙 모든 사용자에 대 한 액세스를 허용 합니다. 이 규칙 파티 신뢰 발급 승인 규칙 목록 의존 Microsoft Office 365 Id 플랫폼에 이미 있어야 합니다.|= > 문제 (유형 값 "https://schemas.microsoft.com/authorization/claims/permit" = = "true").| 
|요청이 federation 서버 프록시에서 제공에 지정 새로운 사용자 지정 규칙에이 여기서 추가 (즉, x ms 프록시 헤더가)
모든 규칙이 포함 되어 있는 것이 좋습니다.|존재 ([유형 = = "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"])| 
|요청이 IP 정의 허용 범위에 사용 하는 클라이언트에서 임을 설정 하는 데 사용 합니다.|이 (가) ([유형 값 "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip" = = = ~ "사용자가 제공한 공용 ip 주소 regex"])| 
|이 여기서는 액세스 하 고 응용 프로그램이 Microsoft.Exchange.ActiveSync 경우 요청이 거부 되어야 지정 하는 데 사용 됩니다.|이 (가) ([유형 "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application" = =, Value=="Microsoft.Exchange.ActiveSync"])| 
|이 규칙 통화가 웹 브라우저를 통해 했으며 거부 되지 있는지 여부를 확인할 수 있습니다.|이 (가) ([유형 값 "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path" = = = = "/ adfs /! /"])| 
|이 규칙 거부할 특정 Active Directory 그룹 (SID 값에 따라)에 사용자를 설명 합니다. 이 정책에 하지 추가의 사용자 그룹 허용 됩니다 위치와 관계 없이 하는 것을 의미 합니다.|존재 ([유형 값 "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid" = = = ~ "{그룹 허용된 광고 그룹의 SID 값}"])| 
|이 필요한 조항을 모두 이전 조건을 충족 하는 경우 거부 발급입니다.|= > 문제 (유형 값 "https://schemas.microsoft.com/authorization/claims/deny" = = "true").|

### <a name="building-the-ip-address-range-expression"></a>IP 주소 범위 식 빌드

현재만 Exchange Online에서는 인증 요청 Adfs에 전달 하는 경우 헤더를 채웁니다으로 설정 되어 있는 HTTP 머리글에서 x ms-전달-클라이언트-ip 클레임이 채워집니다. 클레임 값 다음 중 하나를 수 있습니다.

>[!Note] 
>Exchange Online IPV4 및 하지 IPV6 주소 현재 지원합니다.

단일 IP 주소: Exchange Online에 직접 연결 하는 클라이언트의 IP 주소

>[!Note] 
>회사 네트워크에 대 한 클라이언트의 IP 주소 조직의 아웃 바운드 프록시 또는 게이트웨이 외부 인터페이스 IP 주소가 표시 됩니다.

VPN 또는 Microsoft DirectAccess (DA) 하 여 회사 네트워크에 연결 하는 클라이언트 기업 클라이언트 내부 또는 외부 클라이언트 VPN 또는 da. 구성에 따라으로 표시 될 수 있습니다.

하나 이상의 IP 주소: 연결 클라이언트의 IP 주소를 확인할 수 없는 경우 Exchange Online을 x-전달 기능에 대 한 머리글, HTTP 기반 요청에 포함 될 수 있는 많은 클라이언트, 부하 분산와 프록시 시장에서 지원 되는 사용할 수 없는 헤더 값에 따라 값 설정 됩니다.

>[!Note]
>클라이언트 IP 주소와 요청을 전달 각 프록시의 주소가 표시 여러 IP 주소가 쉼표로 구분 됩니다.

Exchange Online 인프라와 관련 된 IP 주소 목록에 표시 되지 않습니다.


#### <a name="regular-expressions"></a>일반 표현

IP 주소와 일치 해야 할 때 수행 비교 문자를 생성 하는 데 필요한 됩니다. 다음 일련의 단계를 우리는 예 다음 주소 범위 (공용 IP 범위 내에 맞게 이러한 예 변경 하는 주)에 맞게 식 생성 하는 방법에 대 한 제공 합니다.


- 192.168.1.1 – 192.168.1.25
- 10.0.0.1 – 10.0.0.14

먼저은 단일 IP 주소와 일치 하는 기본 패턴은 다음과 같습니다: \b###\.###\.###\.###\b

를 확장 우리 수 일치 OR 식으로 두 가지 IP 주소 다음과 같은: \b###\.###\.###\.###\b|\b###\.###\.###\.###\b

(예: 192.168.1.1 또는 10.0.0.1) 두 주소와 일치 하도록 예로 들 수 있으므로,: \b192\.168\.1\.1\b|\b10\.0\.0\.1\b

이 주소의 수에 관계 없이 입력할 수 있는 방법을 제공 합니다. 예를 들어 192.168.1.1 – 192.168.1.25을 허용 해야 할 다양 한 주소 나타나는 일치 하는 수행 해야 문자별으로 문자: \b192\.168\.1\ 합니다. ([1-9] | [0-9] 1 | [0 5] 2) \b

>[!Note] 
>IP 주소가 문자열 및 숫자가 아니라으로 간주 됩니다.


규칙 다음과 같은 분할 됩니다. \b192\.168\.1\ 합니다.

192.168.1로 시작을 하는 가치를 찾습니다.

다음 문자 최종 소수점 주소의 부분에 필요한 범위를 찾습니다.


- 1-9로 끝나는 ([1-9] 일치 주소
- | 1 [0-9] 10-19로 끝나는 주소를 찾습니다.
- 20 25로 끝나는 |2[0-5]) 일치 주소

>[!Note]
>괄호 올바르게 위치 해야, 다른 일부는 IP 주소와 일치 하는 시작 하지 않도록 합니다.

일치 하는 192 블록으로 10 블록에 대 한 유사 식 작성할 수 있습니다: \b10\.0\.0\ 합니다. ([1-9] | 1 [0 4]) \b

결합 하, 다음 식 일치 해야 "192.168.1.1~25" 및 "10.0.0.1~14"에 대 한 모든 주소 및: \b192\.168\.1\ 합니다. ([1-9]|1[0-9]|2[0-5])\b|\b10\.0\.0\ 합니다. ([1-9] | 1 [0 4]) \b

#### <a name="testing-the-expression"></a>식 테스트

Regex 확인 도구를 사용 하는 것이 좋습니다 하므로 Regex 식 매우 하기가 될 수 있습니다. "온라인 regex 식"에 대해 인터넷 검색을 수행 하면 샘플 데이터에 대 한 식 사용해 볼 수 있는 몇 가지 좋은 온라인 유틸리티를 찾을 수 있습니다.

식 테스트 때와 일치 하는 데 발생할 수 있는 문제를 이해 하는 것이 중요 합니다. Exchange online 시스템 쉼표로 많은 IP 주소를 보낼 수 있습니다. 위의 표현이 작동 합니다. 그러나는 regex 식 테스트 하는이 대해 생각 하는 것이 중요 합니다. 예를 들어, 위 예제 확인 입력 다음 샘플을 사용할 수 하나. 

192.168.1.1, 192.168.1.2, 192.169.1.1. 192.168.12.1, 192.168.1.10, 192.168.1.25, 192.168.1.26, 192.168.1.30, 1192.168.1.20 

10.0.0.1, 10.0.0.5, 10.0.0.10, 10.0.1.0, 10.0.1.1, 110.0.0.1, 10.0.0.14, 10.0.0.15, 10.0.0.10, 10,0.0.1 











## <a name="validating-the-deployment"></a>배포의 유효성 검사

### <a name="security-audit-logs"></a>보안 감사 로그

클레임 전송 되는 및는 Adfs에 사용할 수 있는 새로운 요청 컨텍스트 처리 파이프라인 주장 있는지를 확인 하려면 ADFS 서버에 기록 감사를 사용 하도록 설정 합니다. 그런 다음 일부 인증 요청 및 청구 값 확인 표준 보안 감사 로그 항목에 보냅니다. 

보안 이벤트 ADFS 서버에 기록 감사의 로깅 사용 하려면 ADFS 2.0에 대 한 감사 구성에서 단계를 따르세요.

### <a name="event-logging"></a>이벤트 로깅에서

기본적으로 실패 요청 응용 프로그램 및 서비스 로그 아래에 있는 응용 프로그램 이벤트 로그에 기록 \ ADFS 2.0 \ Admin.For 이벤트 로깅에서 ADFS에 대 한 자세한 내용은 참조 [AD 설정 FS 2.0 이벤트 로깅에서](https://technet.microsoft.com/library/adfs2-troubleshooting-configuring-computers.aspx)합니다.

### <a name="configuring-verbose-ad-fs-tracing-logs"></a>세부 정보 표시 ADFS 추적 로그 구성

ADFS 추적 이벤트 ADFS 2.0 디버그 로그에 기록 됩니다. 추적을 사용 하려면 참조 [구성 ADFS 2.0에 대 한 추적 디버깅](https://technet.microsoft.com/en-us/library/adfs2-troubleshooting-configuring-computers.aspx)합니다.

추적을 활성화 한 후 다음 명령줄 구문을 로깅 세부 정보 표시 수준을 사용 하려면 사용: wevtutil.exe sl "ADFS 2.0 추적/디버그" /l:5  

## <a name="related"></a>관련
새 클레임 유형에 대 한 자세한 내용은 참조 [광고 FS 클레임 종류](AD-FS-Claims-Types.md)합니다.
 
