---
title: "클레임을 생성할 수 id_token에서 FS 2016 ad OAuth 또는 OpenID 연결을 사용 하는 경우 사용자 지정"
description: "기술 광고 FS 2016에 사용자 지정 id 토큰 conecpts 개요"
author: anandyadavmsft
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.reviewer: anandy
ms.technology: identity-adfs
ms.openlocfilehash: c17d50bb6d90726eafc3e585f16a7a8189a68392
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2018
---
# <a name="customize-claims-to-be-emitted-in-idtoken-when-using-openid-connect-or-oauth-with-ad-fs-2016"></a>클레임을 생성할 수 id_token에서 FS 2016 ad OAuth 또는 OpenID 연결을 사용 하는 경우 사용자 지정

## <a name="overview"></a>개요
The article [here](enabling-openId-connect-with-ad-fs.md) shows how to build an app that uses AD FS for OpenID Connect sign on. 그러나 기본적으로 여러 가지 고정된 집합이 클레임은 id_token에서 사용할 수 있습니다. 광고 FS 2016에 OpenID 연결 시나리오에서 id_token 사용자 지정할 수 있는 기능입니다.

## <a name="when-are-custom-id-token-used"></a>사용자 지정 ID 되 면 사용 되는 토큰?
특정 상황에서 것 같습니다 리소스에 액세스 하려고 하는 클라이언트 응용 프로그램은 없습니다. 따라서 액세스 토큰이 필요 정말 하지 않습니다. 이러한 경우 클라이언트 응용 프로그램 기본적으로는 ID 토큰 하지만 일부 추가 클레임 기능을 지원 하기 필요 합니다.

## <a name="what-are-the-restrictions-on-getting-custom-claims-in-id-token"></a>사용자 지정 클레임 id에서 토큰 받기에 대 한 제한 이란 무엇 인가요?

### <a name="scenario-1"></a>1 시나리오

![제한](media/Custom-Id-Tokens-in-AD-FS/res1.png)

1.  response_mode는 form_post으로 설정 된
2.  공용 클라이언트만 로그인 수 사용자 지정 클레임 ID 토큰
3.  신뢰 파티 식별자 클라이언트 식별자와 동일 해야 합니다.

### <a name="scenario-2"></a>시나리오 2

![제한](media/Custom-Id-Tokens-in-AD-FS/restrict2.png)

와 [KB4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) ADFS 서버에 설치
1.  response_mode는 form_post으로 설정 된
2.  범위 allatclaims 클라이언트-RP 페어링을 할당 합니다.
아래의 예제 표시 된 대로 Grant-ADFSApplicationPermission cmdlet 사용 하 여 범위를 지정할 수 있습니다.

``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "https://my/privateclient" -ServerRoleIdentifier "https://rp/fedpassive" -ScopeNames "allatclaims","openid"
```

## <a name="creating-an-oauth-application-to-handle-custom-claims-in-id-token"></a>ID 토큰에 사용자 지정 클레임 처리 하기 위한 작업이 OAuth 응용 프로그램을 만들기
문서를 사용 하 여 [여기](Enabling-OpenId-Connect-with-AD-FS-2016.md) 로그인 ADFS OpenID 연결에 대 한 사용 하는 응용 프로그램 앱을 만들 수 있습니다. 다음 Adfs의 응용 프로그램을 사용자 지정 클레임 토큰 ID를 받기 위해 구성 하려면 아래 단계를 따릅니다.

### <a name="create-the-application-group-in-ad-fs-2016"></a>Adfs 2016 응용 그룹 만들기

1.  라는 CustomTokenClient 응용 프로그램, 아래에 표시 된 새로운 템플릿으로에 따라 그룹을 만듭니다.

![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap1.png)

2. 이 서식 기밀 클라이언트를 만듭니다. 식별자 기록한 반환 URI VS 프로젝트 SSL URL으로 지정 합니다.

![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap2.png)

3.  다음 단계를 선택 **공유 암호를 생성** 클라이언트 자격 증명을 만들을 생성 클라이언트 자격 증명을 복사 합니다.

![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap3.png)

4. 클릭 **다음** 마법사를 완료 하려면 진행 하 고 있습니다.

![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap4.png)

### <a name="create-the-relying-party"></a>당사자 만들기
ID를 사용자 지정 클레임 추가 하기 위해 토큰 해야 클레임 소유자 ID 토큰에 추가 될 것 RP 만들 수 있습니다. 의존 파티 신뢰 추가 마법사를 사용 하 여 다음과 같이 새 당사자를 만들려면 다음과 같습니다.
 
![당사자에](media/Custom-Id-Tokens-in-AD-FS/rpsnap1.png)

당사자에를 만든 후 신뢰 파티 항목을 마우스 오른쪽 단추로 클릭 하 고 선택 **편집 주장 발급 정책** 클레임 발급 규칙을 추가 해야 합니다. 다음과 같이 ID 토큰 요구 사용자 지정 청구 추가:

![당사자에](media/Custom-Id-Tokens-in-AD-FS/rpsnap2.png)

### <a name="assign-allatclaims-scope-to-the-pair-of-client-and-relying-party"></a>"Allatclaims" 범위를 클라이언트 및 당사자 페어링할 지정
아래의 예제에 지정 된 새 allatclaims 범위 PowerShell ADFS 서버에 사용 하 여 지정 (clientID 및 서버를 변경 합니다.

``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "5db77ce4-cedf-4319-85f7-cc230b7022e0" -ServerRoleIdentifier "https://customidrp1/" -ScopeNames "allatclaims","openid"
```

>[!NOTE]
>응용 프로그램 설정을 따라 ClientRoleIdentifier 및 ServerRoleIdentifier 변경

## <a name="test-the-custom-claims-in-id-token"></a>ID 토큰에 사용자 지정 클레임 테스트

그런 다음 동일한 약간의 클레임 액세스 하는 데 항상 한 코드를 사용 하 여 id_token 일부가 됩니다 추가 클레임은 볼 수 있습니다.
예를 들어.NET MVC 샘플 앱에서 중 하나 컨트롤러 파일 열고 같은 코드를 입력 하 고 아래:


``` code
    [Authorize]
    public ActionResult About()
    {

        ClaimsPrincipal cp = ClaimsPrincipal.Current;

        string userName = cp.FindFirst(ClaimTypes.GivenName).Value;
        ViewBag.Message = String.Format("Hello {0}!", userName);
        return View();

    }

```

>[!NOTE]
>Please be aware that the resource parameter is required in the Oauth2 request.
>
>Bad example:
>
>**https&#58;//sts.contoso.com/adfs/oauth2/authorize?response_type=id_token&scope=openid&redirect_uri=https&#58;//myportal/auth&nonce=b3ceb943fc756d927777&client_id=6db3ec2a-075a-4c72-9b22-ca7ab60cb4e7&state=42c2c156aef47e8d0870&resource=6db3ec2a-075a-4c72-9b22-ca7ab60cb4e7**
>
>Good example:
>
>**https&#58;//sts.contoso.com/adfs/oauth2/authorize?response_type=id_token&scope=openid&redirect_uri=https&#58;//myportal/auth&nonce=b3ceb943fc756d927777&client_id=6db3ec2a-075a-4c72-9b22-ca7ab60cb4e7&state=42c2c156aef47e8d0870&resource=https&#58;//customidrp1/**
>
>If the resource parameter is not in the request you may recieve an error or a token without any custom claims.

## <a name="next-steps"></a>다음 단계
[광고 FS 개발](../../ad-fs/AD-FS-Development.md)  