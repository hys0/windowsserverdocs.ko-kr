---
ms.assetid: 3a840b63-78b7-4e62-af7b-497026bfdb93
title: "연습 가이드-관련 된 위험 조건부 액세스 제어도 관리"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 11d2d567f9264dca53a3426263a172649d7d7c11
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="walkthrough-guide-manage-risk-with-conditional-access-control"></a>연습 가이드: 관련 된 위험 조건부 액세스 제어도 관리

>Windows Server 2012 r 2에 적용 됩니다.


## <a name="about-this-guide"></a>이 가이드 정보
이 연습 Active Directory Federation Services (ADFS) Windows Server 2012 r 2에서에 조건부 액세스 제어 메커니즘을 통해 요인 중 하나에서 (사용자 데이터) 사용할 수 있는 위험 관리 하기 위한 지침을 제공 합니다. 조건부 액세스를 제어 하 고 승인 메커니즘 adfs Windows Server 2012 r 2에서에 대 한 자세한 내용은 참조 [액세스 제어 조건으로 관리 위험](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)합니다.

이 연습 다음 섹션으로 구성 됩니다.

-   [1 단계: 랩 환경 설정](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [2 단계: 기본 ADFS 액세스 제어 메커니즘 확인](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_2)

-   [3 단계: 구성 조건부 액세스 제어 정책 기반으로 사용자 데이터](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_3)

-   [4 단계: 조건부 액세스 제어 메커니즘 확인](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_4)

## <a name="BKMK_1"></a>1 단계: 랩 환경 설정
이 연습을 완료 하기 위해 다음과 같은 구성 요소도 구성 된 환경을 할 수 있습니다.

-   테스트 사용자와 해당 스키마 Windows Server 2012 R2 또는 Windows Server 2012 r 2 실행 Active Directory 도메인으로 업그레이드와 Windows Server 2008, Windows Server 2008 R2 또는 Windows Server 2012에서 실행 중인 그룹 계정, Active Directory 도메인

-   Windows Server 2012 r 2에 실행 하는 federation 서버

-   샘플 신청서 호스트 하는 웹 서버

-   클라이언트 컴퓨터 샘플 응용 프로그램 액세스할 수 있습니다

> [!WARNING]
> 권장 (프로덕션 또는 테스트 환경에서 둘 다)를 해당 federation 서버 하 고 웹 서버 동일한 컴퓨터를 사용 하지 마십시오.

이 환경에서 federation 서버는 사용자에 게 샘플 응용 프로그램에 액세스할 수 있도록 클레임 발행 합니다. 클레임은를 제공 하는 사용자가 신뢰 하는 샘플 응용 프로그램 federation 서버 문제 호스트 하는 웹 서버 합니다.

이 환경을 설정 하는 방법에 관한 참조 [랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

## <a name="BKMK_2"></a>2 단계: 기본 ADFS 액세스 제어 메커니즘 확인
이 단계에서 사용자 확인 ADFS 액세스 제어 메커니즘, 여기서 사용자가 ADFS 로그인 페이지로 리디렉션됩니다, 기본 유효한 자격 증명을 제공 하며 응용 프로그램에 대 한 액세스 권한이 부여 됩니다. 사용할 수 있는 **로버트 Hatley** AD 계정이 및 **claimapp** 샘플으로 구성 된 응용 프로그램 [랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

#### <a name="to-verify-the-default-ad-fs-access-control-mechanism"></a>ADFS 액세스 제어 메커니즘 기본 확인 하려면

1.  클라이언트 컴퓨터에 브라우저 창을 열고 샘플 응용 프로그램으로 이동: **https://webserv1.contoso.com/claimapp**합니다.

    이 작업은 federation 서버에 요청을 자동으로 리디렉션합니다 및 사용자 이름 및 암호를 사용 하 여 로그인 하 라는 메시지가 표시 됩니다.

2.  자격 증명 입력은 **로버트 Hatley** 광고 계정에서 만든 [랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

    응용 프로그램에 대 한 액세스를 부여 하 고 됩니다.

## <a name="BKMK_3"></a>3 단계: 구성 조건부 액세스 제어 정책 기반으로 사용자 데이터
이 단계를 기반으로 사용자 그룹 구성원 데이터 액세스를 제어 정책을 설정 합니다. 즉, 구성 된 **발급 승인 규칙** 샘플 응용 프로그램-나타내는 신뢰 파티 보안에 대 한 federation 서버에 **claimapp**합니다. 이 규칙 논리가 **로버트 Hatley** 광고를 사용자에 속하는 그 하기 때문에이 응용 프로그램에 액세스 하는 데 필요한 청구 발생 합니다는 **금융** 그룹입니다. 추가한는 **로버트 Hatley** 계정에 **금융** 그룹에서 [랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

AD FS Management Console 중 하나를 사용 하 여이 작업을 완료할 수 또는 Windows PowerShell 통해 합니다.

#### <a name="to-configure-conditional-access-control-policy-based-on-user-data-via-the-ad-fs-management-console"></a>구성 조건부 액세스 제어 정책 기반으로 광고 FS Management Console을 통해 사용자 데이터

1.  AD FS Management Console에서 이동 **관계 신뢰**, 다음 **파티 신뢰 의존**합니다.

2.  샘플 응용 프로그램을 나타내는 신뢰 파티 신뢰 선택 (**claimapp**)와에서 다음 중 하나는 **작업** 창이 신뢰 파티 신뢰를 마우스 오른쪽 단추로 클릭, 선택 또는 **편집 클레임 규칙**합니다.

3.  에 **claimapp 클레임 규칙 편집** 창을 선택 하 고 **발급 승인 규칙** 탭 및 클릭 **규칙 추가**합니다.

4.  **발급 승인 규칙 주장 마법사 추가**에 **규칙 템플릿 선택 페이지**선택 **허용 또는 거부 들어오는 요구에 따라 사용자에 게** 규칙 템플릿 주장와 클릭 한 다음 **다음**합니다.

5.  에 **구성 규칙** 페이지를 다음 수행 클릭 한 다음 **완료**:

    1.  예를 들어 클레임 규칙의 이름을 입력 **TestRule**합니다.

    2.  선택 **그룹 SID** 으로 **수신 클레임 유형**합니다.

    3.  클릭 **검색**에 입력 **금융** 광고 이름에 대 한 그룹을 테스트 하 고 해결에 대 한 것은 **클레임 값을 수신** 필드 합니다.

    4.  선택는 **액세스를 사용자에 게가 들어오는 클레임 거부** 옵션입니다.

6.  에 **claimapp 클레임 규칙 편집** 창, 삭제 되었는지 확인은 **모든 사용자에 액세스 허용** 이 신뢰 파티 신뢰를 만들 때 기본적으로 만들어진 규칙을 합니다.

#### <a name="to-configure-conditional-access-control-policy-based-on-user-data-via-windows-powershell"></a>구성 조건부 액세스 제어 정책 기반으로 사용자 데이터를 통해 Windows PowerShell 하려면

1.  해당 federation 서버를 Windows PowerShell 명령 창 열고 다음 명령을 실행 합니다.


    `$rp = Get-AdfsRelyingPartyTrust -Name claimapp`


2.  동일한 Windows PowerShell 명령 창에서 다음 명령을 실행 합니다.


    `$GroupAuthzRule = '@RuleTemplate = "Authorization" @RuleName = "Foo" c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "^(?i)<group_SID>$"] =>issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");'
    Set-AdfsRelyingPartyTrust -TargetRelyingParty $rp -IssuanceAuthorizationRules $GroupAuthzRule`

> [!NOTE]
> < Group_SID > 광고 sid 값으로 대체 하 않도록 **금융** 그룹입니다.

## <a name="BKMK_4"></a>4 단계: 조건부 액세스 제어 메커니즘 확인
이 단계에서 이전 단계에서를 설정 하는 조건 액세스 제어 정책을 확인 합니다. 다음 절차 여부를 확인할 수 있습니다 **로버트 Hatley** 광고 사용자에 속하는 그 하기 때문에 샘플 응용 프로그램에 액세스할 수 있는 **금융** 에 속하지 않는 광고 사용자 및 그룹은 **금융** 그룹 샘플 응용 프로그램에 액세스할 수 없습니다.

1.  클라이언트 컴퓨터에 브라우저 창을 열고 샘플 응용 프로그램으로 이동: **https://webserv1.contoso.com/claimapp**

    이 작업은 federation 서버에 요청을 자동으로 리디렉션합니다 및 사용자 이름 및 암호를 사용 하 여 로그인 하 라는 메시지가 표시 됩니다.

2.  자격 증명 입력은 **로버트 Hatley** 광고 계정에서 만든 [랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

    응용 프로그램에 대 한 액세스를 부여 하 고 됩니다.

3.  자격 증명에 속하지 않는 다른 광고 사용자의 입력에서 **금융** 그룹입니다. (사용자 계정 광고에 만드는 방법에 대 한 자세한 내용은 참조 [https://technet.microsoft.com/library/cc7833232.aspx](https://technet.microsoft.com/library/cc783323%28v=ws.10%29.aspx)합니다.

    이 시점 액세스 제어 정책 이전 단계에서 설정으로 인해 '액세스 거부' 메시지가 표시 되에 속하지 않는이 광고 사용자는 **금융** 그룹입니다. 가 기본 메시지 텍스트 **권한이이 사이트에 액세스할 수 없습니다. 로그 아웃 하 고 다시 로그인 나 권한을 관리자에 게 문의 하려면 여기를 클릭 합니다.** 그러나이 텍스트는 완전히 사용자 지정할 수 있습니다. 로그인 환경을 사용자 지정 하는 방법에 대 한 자세한 내용은 참조 [FS 로그인 페이지 광고를 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx)합니다.

## <a name="see-also"></a>참조 하십시오
[관련 된 위험 액세스 제어 조건으로 관리](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)
[랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



