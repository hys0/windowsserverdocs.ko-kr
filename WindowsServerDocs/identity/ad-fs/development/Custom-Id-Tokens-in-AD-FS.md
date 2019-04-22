---
title: Ad FS 2016 OpenID Connect 또는 OAuth를 사용 하는 경우 id_token에 내보내지는 클레임을 사용자 지정
description: AD FS 2016에서에서 사용자 지정 id 토큰 conecpts 기술 개요
author: anandyadavmsft
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.reviewer: anandy
ms.technology: identity-adfs
ms.openlocfilehash: 8c8e14f22a4bca5b6d32e841814a58a4b4ddca01
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820644"
---
# <a name="customize-claims-to-be-emitted-in-idtoken-when-using-openid-connect-or-oauth-with-ad-fs-2016"></a>Ad FS 2016 OpenID Connect 또는 OAuth를 사용 하는 경우 id_token에 내보내지는 클레임을 사용자 지정

## <a name="overview"></a>개요
이 문서 [여기](enabling-openId-connect-with-ad-fs.md) 로그온 OpenID Connect에 대 한 AD FS를 사용 하는 앱을 빌드하는 방법을 보여 줍니다. 그러나 기본적으로 가지 고정된 된 집합의 클레임은 id_token에서 사용할 수 있습니다. AD FS 2016 OpenID Connect 시나리오의 id_token을 사용자 지정 하는 기능을 있습니다.

## <a name="when-are-custom-id-token-used"></a>사용자 지정 ID를 때 사용 되는 토큰?
특정 시나리오에서 클라이언트 응용 프로그램 액세스를 시도 하는 리소스 없이 됩니다. 따라서 액세스 토큰이 필요 실제로 하지 않습니다. 이러한 경우 클라이언트 응용 프로그램 에서만 ID 토큰 하지만 기능을 돕는 몇 가지 추가 클레임을 사용 하 여 기본적으로 해야 합니다.

## <a name="what-are-the-restrictions-on-getting-custom-claims-in-id-token"></a>토큰을 가져오는 데 사용자 지정 클레임 id에서에 대 한 제한 이란?

### <a name="scenario-1"></a>시나리오 1

![제한](media/Custom-Id-Tokens-in-AD-FS/res1.png)

1.  response_mode는 form_post로 설정
2.  공용 클라이언트만 수는 사용자 지정 클레임 ID에서 토큰 가져오기
3.  신뢰 당사자 식별자는 클라이언트 식별자와 동일 해야 합니다.

### <a name="scenario-2"></a>시나리오 2

![제한](media/Custom-Id-Tokens-in-AD-FS/restrict2.png)

사용 하 여 [KB4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) AD FS 서버에 설치
1.  response_mode는 form_post로 설정
2.  클라이언트-RP 쌍에 범위 allatclaims를 할당 합니다.
아래 예제에 표시 된 대로 권한 부여 ADFSApplicationPermission cmdlet을 사용 하 여 범위를 할당할 수 있습니다.

``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "https://my/privateclient" -ServerRoleIdentifier "https://rp/fedpassive" -ScopeNames "allatclaims","openid"
```

## <a name="creating-an-oauth-application-to-handle-custom-claims-in-id-token"></a>ID 토큰의 사용자 지정 클레임을 처리 하는 OAuth 응용 프로그램 만들기
문서를 사용 하 여 [여기](Enabling-OpenId-Connect-with-AD-FS-2016.md) 를 사용 하는 응용 프로그램 앱을 만드는 데 OpenID connect의 AD FS에 로그인 합니다. 그런 다음 사용자 지정 클레임을 사용 하 여 ID 토큰을 수신 하기 위한 AD FS에서 응용 프로그램을 구성 하려면 다음 단계를 따릅니다.

### <a name="create-the-application-group-in-ad-fs-2016"></a>AD FS 2016에서에서 응용 프로그램 그룹 만들기

1.  CustomTokenClient 호출 아래에 표시 된, 새 템플릿을 기반으로 응용 프로그램 그룹을 만듭니다.

![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap1.png)

2. 이 템플릿은 기밀 클라이언트를 만듭니다. 식별자를 확인 하 고 VS 프로젝트의 SSL URL로 반환 된 URI를 지정 합니다.

![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap2.png)

3.  다음 단계에서 선택 **공유 암호 생성** 클라이언트 자격 증명을 만들고 생성 된 클라이언트 자격 증명을 복사 합니다.

![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap3.png)

4. 클릭 **다음** 하 고 마법사를 완료 하려면 진행 합니다.

![클라이언트](media/Custom-Id-Tokens-in-AD-FS/clientsnap4.png)

### <a name="create-the-relying-party"></a>신뢰 당사자 만들기
ID에서 사용자 지정 클레임을 추가 하려면 토큰을 만들려는 RP ID 토큰에 해당 클레임 추가 됩니다. 신뢰 당사자 트러스트 추가 마법사를 사용 하 여 아래와 같이 새 신뢰 당사자를 만듭니다.
 
![신뢰 당사자](media/Custom-Id-Tokens-in-AD-FS/rpsnap1.png)

신뢰 당사자를 만든 후 신뢰 당사자 항목을 마우스 오른쪽 단추로 클릭 하 고 선택 **편집 클레임 발급 정책** 클레임 발급 규칙을 추가 합니다. 아래 표시 된 것과 같이 ID 토큰에 대 한 필수 사용자 지정 클레임을 추가 합니다.

![신뢰 당사자](media/Custom-Id-Tokens-in-AD-FS/rpsnap2.png)

### <a name="assign-allatclaims-scope-to-the-pair-of-client-and-relying-party"></a>클라이언트 및 신뢰 당사자에 "allatclaims" 범위를 할당
아래 예제에서는 지정 된 대로 새 allatclaims 범위 할당 AD FS 서버에서 PowerShell을 사용 하 여 (clientID 및 서버를 변경 합니다.

``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "5db77ce4-cedf-4319-85f7-cc230b7022e0" -ServerRoleIdentifier "https://customidrp1/" -ScopeNames "allatclaims","openid"
```

>[!NOTE]
>응용 프로그램 설정에 따라 ClientRoleIdentifier 및 ServerRoleIdentifier 변경

## <a name="test-the-custom-claims-in-id-token"></a>ID 토큰에서 사용자 지정 클레임을 테스트 합니다.

그런 다음 동일한 약간의 항상 사용 하 여 클레임에 액세스 하는 코드를 사용 하 여 id_token의 일부가 됩니다 하는 추가 클레임 볼 수 있습니다.
예를 들어.NET MVC 샘플 앱에서 컨트롤러 파일 중 하나를 열고 다음과 같은 코드를 입력 합니다 아래:


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
>리소스 매개 변수는 Oauth2 요청에 필요 하다는 점에 주의 하십시오입니다.
>
>잘못 된 예제:
>
>**https&#58;//sts.contoso.com/adfs/oauth2/authorize?response_type=id_token & 범위 = openid redirect_uri = https&#58;//myportal/auth & nonce = b3ceb943fc756d927777 client_id 6db3ec2a-075a-4c 72 9b22 ca7ab60cb4e7 = & 상태 = 42c2c156aef47e8d0870 리소스 6db3ec2a-075a-4c 72 9b22 ca7ab60cb4e7 =**
>
>좋은 예:
>
>**https&#58;//sts.contoso.com/adfs/oauth2/authorize?response_type=id_token & 범위 = openid redirect_uri = https&#58;//myportal/auth & nonce = b3ceb943fc756d927777 client_id 6db3ec2a-075a-4c 72 9b22 ca7ab60cb4e7 = & 상태 = 42c2c156aef47e8d0870 resource = https&#58;//customidrp1/ & response_mode form_post =**
>
>리소스 매개 변수가 요청에 없는 경우에 오류 또는 없이 모든 사용자 지정 클레임 토큰을 나타날 수 있습니다.

## <a name="next-steps"></a>다음 단계
[AD FS 개발](../../ad-fs/AD-FS-Development.md)  
