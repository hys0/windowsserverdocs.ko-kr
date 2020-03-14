---
ms.assetid: 3a840b63-78b7-4e62-af7b-497026bfdb93
title: 연습 가이드-조건부 Access Control를 사용 하 여 위험 관리
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: aefcd597a580de526a758c6d026c6c91d02d10c8
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79323045"
---
# <a name="walkthrough-guide-manage-risk-with-conditional-access-control"></a>연습 가이드: 조건부 액세스 제어를 사용한 위험 관리




## <a name="about-this-guide"></a>이 가이드의 내용
이 연습에서는 Windows Server 2012 r 2에서 Active Directory Federation Services (AD FS)의 조건부 액세스 제어 메커니즘을 통해 사용할 수 있는 요소 (사용자 데이터) 중 하나를 사용 하 여 위험을 관리 하기 위한 지침을 제공 합니다. Windows Server 2012 r 2에서 AD FS의 조건부 액세스 제어 및 권한 부여 메커니즘에 대 한 자세한 내용은 [조건부 Access Control를 사용 하 여 위험 관리](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)를 참조 하세요.

이 연습은 다음 섹션으로 구성됩니다.

-   [1 단계: 랩 환경 설정](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [2 단계: 기본 AD FS 액세스 제어 메커니즘 확인](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_2)

-   [3 단계: 사용자 데이터를 기반으로 조건부 액세스 제어 정책 구성](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_3)

-   [4 단계: 조건부 액세스 제어 메커니즘 확인](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_4)

## <a name="BKMK_1"></a>1 단계: 랩 환경 설정
이 연습을 완료하려면 다음 구성 요소로 구성된 환경이 필요합니다.

-   테스트 사용자 및 그룹 계정을 사용 하는 Active Directory 도메인-windows server 2008, Windows Server 2008 R2 또는 windows server 2012의 스키마가 windows server 2012 r 2로 업그레이드 되 고 windows server 2012 r 2에서 실행 되는 Active Directory 도메인

-   Windows Server 2012 r 2에서 실행 하는 페더레이션 서버

-   예제 애플리케이션을 호스팅하는 웹 서버

-   예제 애플리케이션에 액세스할 수 있는 클라이언트 컴퓨터

> [!WARNING]
> 프로덕션 환경과 테스트 환경 모두, 서로 다른 컴퓨터를 페더레이션 서버와 웹 서버로 사용하는 것이 좋습니다.

이 환경에서 페더레이션 서버는 사용자가 예제 애플리케이션에 액세스하는 데 필요한 클레임을 발급합니다. 웹 서버는 페더레이션 서버에서 발급된 클레임을 제공하는 사용자를 신뢰할 예제 애플리케이션을 호스팅합니다.

이 환경을 설정 하는 방법에 대 한 지침을 참조 하십시오. [Windows Server 2012 r 2에서 AD FS에 대 한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

## <a name="BKMK_2"></a>2 단계: 기본 AD FS 액세스 제어 메커니즘 확인
이 단계에서는 사용자가 AD FS 로그인 페이지로 리디렉션된 후 유효한 자격 증명을 제공하면 애플리케이션에 대한 액세스 권한이 부여되는 기본 AD FS 액세스 제어 메커니즘을 확인합니다. 사용할 수는 **Robert Hatley** AD 계정 및 **claimapp** 샘플 애플리케이션에서 구성한 [Windows Server 2012 r 2에서 AD FS에 대 한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

#### <a name="to-verify-the-default-ad-fs-access-control-mechanism"></a>기본 AD FS 액세스 제어 메커니즘을 확인하려면

1.  클라이언트 컴퓨터에서 브라우저 창을 열고 샘플 응용 프로그램: **https://webserv1.contoso.com/claimapp** 로 이동 합니다.

    이 작업을 수행하면 요청이 자동으로 페더레이션 서버로 리디렉션되고 사용자 이름과 암호를 사용하여 로그인하라는 메시지가 표시됩니다.

2.  자격 증명을 입력에서 **Robert Hatley** AD 계정에서 만든 [Windows Server 2012 r 2에서 AD FS에 대 한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

    그러면 애플리케이션에 대한 액세스 권한이 부여됩니다.

## <a name="BKMK_3"></a>3 단계: 사용자 데이터를 기반으로 조건부 액세스 제어 정책 구성
이 단계에서는 사용자 그룹 구성원 자격 데이터를 기반으로 액세스 제어 정책을 설정합니다. 즉, 페더레이션 서버에서 샘플 응용 프로그램 **claimapp**을 나타내는 신뢰 당사자 트러스트를 사용하도록 **발급 권한 부여 규칙**을 구성합니다. 이 규칙의 논리에 따라 **Robert Hatley** AD 사용자는 **재무** 그룹에 속하므로이 응용 프로그램에 액세스 하는 데 필요한 클레임이 발급 됩니다. **Robert Hatley** 계정을 [Windows Server 2012 r 2에서 AD FS에 대 한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)에서 **재무** 그룹에 추가 했습니다.

AD FS 관리 콘솔 또는 Windows PowerShell을 통해 이 작업을 완료할 수 있습니다.

#### <a name="to-configure-conditional-access-control-policy-based-on-user-data-via-the-ad-fs-management-console"></a>AD FS 관리 콘솔을 통해 사용자 데이터에 따라 조건부 액세스 제어 정책을 구성하려면

1.  AD FS 관리 콘솔에서 **Trust Relationships(트러스트 관계)** , **Relying Party Trusts(신뢰 당사자 트러스트)** 로 차례로 이동합니다.

2.  예제 응용 프로그램(**claimapp**)을 나타내는 신뢰 당사자 트러스트를 선택한 다음 **작업** 창에서 또는 이 신뢰 당사자 트러스트를 마우스 오른쪽 단추로 클릭하여 **클레임 규칙 편집**를 선택합니다.

3.  **Edit Claim Rules for claimapp(claimapp에 대한 클레임 규칙 편집)** 창에서 **Issuance Authorization Rules(발급 권한 부여 규칙)** 탭을 클릭하고 **Add Rule(규칙 추가)** 을 클릭합니다.

4.  **Add Issuance Authorization Claim Rule Wizard(발급 권한 부여 클레임 규칙 추가 마법사)** 의 **Select Rule Template(규칙 템플릿 선택)** 페이지에서 **Permit or Deny Users Based on an Incoming Claim(들어오는 클레임에 따라 사용자 허용 또는 거부)** 클레임 규칙 템플릿을 선택하고 **Next(다음)** 를 클릭합니다.

5.  **Configure Rule(규칙 구성)** 페이지에서 다음 작업을 모두 수행하고 **Finish(마침)** 를 클릭합니다.

    1.  클레임 규칙의 이름을 입력합니다(예: **TestRule**).

    2.  **Group SID(그룹 SID)** 를 **Incoming claim type(들어오는 클레임 유형)** 으로 선택합니다.

    3.  **찾아보기**를 클릭하고 AD 테스트 그룹 이름에 **Finance**를 입력한 다음 **들어오는 클레임 값** 필드에 대해 해당 이름을 확인합니다.

    4.  **Deny access to users with this incoming claim(이 들어오는 클레임을 가진 사용자에 대한 액세스 거부)** 옵션을 선택합니다.

6.  **Edit Claim Rules for claimapp(claimapp에 대한 클레임 규칙 편집)** 창에서 이 신뢰 당사자 트러스트를 만들 때 기본적으로 생성된 **Permit Access to All Users(모든 사용자에 대한 액세스 허용)** 규칙을 삭제해야 합니다.

#### <a name="to-configure-conditional-access-control-policy-based-on-user-data-via-windows-powershell"></a>Windows PowerShell을 통해 사용자 데이터에 따라 조건부 액세스 제어 정책을 구성하려면

1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행합니다.


~~~
`$rp = Get-AdfsRelyingPartyTrust -Name claimapp`
~~~


2. 같은 Windows PowerShell 명령 창에서 다음 명령을 실행합니다.


~~~
`$GroupAuthzRule = '@RuleTemplate = "Authorization" @RuleName = "Foo" c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "^(?i)<group_SID>$"] =>issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");'
Set-AdfsRelyingPartyTrust -TargetRelyingParty $rp -IssuanceAuthorizationRules $GroupAuthzRule`
~~~

> [!NOTE]
> <group_SID>를 AD **Finance** 그룹의 SID 값으로 바꿔야 합니다.

## <a name="BKMK_4"></a>4 단계: 조건부 액세스 제어 메커니즘 확인
이 단계에서는 이전 단계에서 설정한 조건부 액세스 제어 정책을 확인합니다. 다음 절차를 사용하여 **Finance** 그룹에 속하는 **Robert Hatley** AD 사용자는 예제 응용 프로그램에 액세스할 수 있고, **Finance** 그룹에 속하지 않는 AD 사용자는 예제 응용 프로그램에 액세스할 수 없는지 확인할 수 있습니다.

1.  클라이언트 컴퓨터에서 브라우저 창을 열고 샘플 응용 프로그램으로 이동 합니다. **https://webserv1.contoso.com/claimapp**

    이 작업을 수행하면 요청이 자동으로 페더레이션 서버로 리디렉션되고 사용자 이름과 암호를 사용하여 로그인하라는 메시지가 표시됩니다.

2.  자격 증명을 입력에서 **Robert Hatley** AD 계정에서 만든 [Windows Server 2012 r 2에서 AD FS에 대 한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

    그러면 애플리케이션에 대한 액세스 권한이 부여됩니다.

3.  **Finance** 그룹에 속하지 않는 다른 AD 사용자의 자격 증명을 입력합니다. AD에서 사용자 계정을 만드는 방법에 대 한 자세한 내용은 [https://technet.microsoft.com/library/cc7833232.aspx](https://technet.microsoft.com/library/cc783323%28v=ws.10%29.aspx)를 참조 하세요.

    이제 이전 단계에서 설정한 액세스 제어 정책으로 인해이 AD 사용자에 대해 **재무** 그룹에 속하지 않은 ' 액세스 거부 ' 메시지가 표시 됩니다. 기본 메시지 텍스트는 **이 사이트에 액세스할 수 있는 권한이 없습니다. 여기를 클릭 하 여 로그 아웃 하 고 다시 로그인 하거나 관리자에 게 권한에 대해 문의 하세요.** (보안상 계정을 확인하기 위해 추가 정보가 필요합니다.)이지만 이 텍스트를 원하는 대로 사용자 지정할 수 있습니다. 로그인 환경을 사용자 지정 하는 방법에 대 한 자세한 내용은 참조 [AD FS 로그인 페이지 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx)합니다.

## <a name="see-also"></a>관련 항목
[조건부 Access Control 사용 하 여 위험 관리](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md) [Windows Server 2012 r 2에서 AD FS에 대 한 랩 환경 설정](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)




