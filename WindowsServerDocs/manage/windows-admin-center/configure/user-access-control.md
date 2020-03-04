---
title: 사용자 액세스 제어 및 권한 구성
description: Active Directory 또는 Azure AD(Project Honolulu)를 사용하여 사용자 액세스 제어 및 권한을 구성하는 방법을 알아봅니다.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 39af45506ff7023cebe437992e90f6d4ec051333
ms.sourcegitcommit: da6c4fa55a6a72924ac363753d04c5b682cee55b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/26/2020
ms.locfileid: "77624897"
---
# <a name="configure-user-access-control-and-permissions"></a>사용자 액세스 제어 및 권한 구성

> 적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

아직 익숙하지 않은 경우 [Windows Admin Center의 사용자 액세스 제어 옵션](../plan/user-access-options.md)을 숙지하세요.

> [!NOTE]
> Windows Admin Center의 그룹 기반 액세스는 작업 그룹 환경 또는 신뢰할 수 없는 도메인에서 지원되지 않습니다.

## <a name="gateway-access-role-definitions"></a>게이트웨이 액세스 역할 정의

Windows Admin Center 게이트웨이 서비스에 액세스할 수 있는 두 가지 역할은 다음과 같습니다.

**게이트웨이 사용자**는 Windows Admin Center 게이트웨이 서비스에 연결하여 해당 게이트웨이를 통해 서버를 관리할 수 있지만, 액세스 권한 또는 게이트웨이에 인증하는 데 사용되는 인증 메커니즘은 변경할 수 없습니다.

**게이트웨이 관리자**는 액세스 권한을 부여받을 수 있는 사용자와 해당 사용자가 게이트웨이를 인증하는 방법을 구성할 수 있습니다. 게이트웨이 관리자만 Windows Admin Center에서 액세스 설정을 보고 구성할 수 있습니다. 게이트웨이 머신의 로컬 관리자는 항상 Windows Admin Center 게이트웨이 서비스의 관리자입니다.

> [!NOTE]
> 게이트웨이에 대한 액세스는 게이트웨이에서 볼 수 있는 관리 서버에 대한 액세스를 암시하지 않습니다. 대상 서버를 관리하려면 연결하는 사용자가 해당 대상 서버에 대한 관리자 권한이 있는 자격 증명(통과된 Windows 자격 증명 또는 **다음으로 관리** 작업을 사용하여 Windows Admin Center 세션에서 제공되는 자격 증명)을 사용해야 합니다.

## <a name="active-directory-or-local-machine-groups"></a>Active Directory 또는 로컬 머신 그룹

Active Directory 또는 로컬 머신 그룹은 기본적으로 게이트웨이 액세스를 제어하는 데 사용됩니다. Active Directory 도메인을 사용하는 경우 Windows Admin Center 인터페이스 내에서 게이트웨이 사용자와 관리자의 액세스를 관리할 수 있습니다.

게이트웨이 사용자는 **사용자** 탭에서 Windows Admin Center에 액세스할 수 있는 사용자를 제어할 수 있습니다. 기본적으로 보안 그룹을 지정하지 않으면 게이트웨이 URL에 액세스하는 모든 사용자에게 액세스 권한이 있습니다. 하나 이상의 보안 그룹을 사용자 목록에 추가하는 경우 액세스는 해당 그룹의 멤버로 제한됩니다.

사용자 환경에서 Active Directory 도메인을 사용하지 않는 경우 액세스는 Windows Admin Center 게이트웨이 머신의 `Users` 및 `Administrators` 로컬 그룹을 통해 제어됩니다.

### <a name="smartcard-authentication"></a>스마트 카드 인증

스마트 카드 기반 보안 그룹에 _필요한_ 추가 그룹을 지정하여 **스마트 카드 인증**을 적용할 수 있습니다. 스마트 카드 기반 보안 그룹이 추가되면 사용자가 보안 그룹 및 사용자 목록에 포함된 스마트 카드 그룹 모두의 멤버인 경우에만 Windows Admin Center 서비스에 액세스할 수 있습니다.

게이트웨이 관리자는 **관리자** 탭에서 Windows Admin Center에 액세스할 수 있는 사용자를 제어할 수 있습니다. 컴퓨터의 로컬 관리자 그룹은 항상 모든 관리자 액세스 권한을 가지고 있으며, 목록에서 제거할 수 없습니다. 보안 그룹이 추가되면 해당 그룹의 멤버에게 Windows Admin Center 게이트웨이 설정을 변경할 수 있는 권한을 부여합니다. 관리자 목록은 보안 그룹 및 스마트 카드 그룹에 대한 AND 조건을 사용하여 사용자 목록과 동일한 방식으로 스마트 카드 인증을 지원합니다.

## <a name="azure-active-directory"></a>Azure Active Directory

조직에서 Azure AD(Azure Active Directory)를 사용하는 경우 게이트웨이에 액세스하기 위해 Azure AD를 요구하여 **추가** 보안 계층을 Windows Admin Center에 추가하도록 선택할 수 있습니다. Windows Admin Center에 액세스하려면 사용자의 **Windows 계정**에도 게이트웨이 서버에 대한 액세스 권한이 있어야 합니다(Azure AD 인증이 사용되는 경우에도). Azure AD를 사용하면 Windows Admin Center UI 내에서가 아니라 Azure Portal에서 Windows Admin Center 사용자 및 관리자 액세스 권한을 관리할 수 있습니다.

### <a name="accessing-windows-admin-center-when-azure-ad-authentication-is-enabled"></a>Azure AD 인증을 사용하도록 설정된 경우의 Windows Admin Center 액세스

사용되는 브라우저에 따라 Azure AD 인증이 구성된 Windows Admin Center에 액세스하는 일부 사용자는 **브라우저에서** Windows Admin Center가 설치된 머신에 대한 Windows 계정 자격 증명을 제공하도록 요구하는 추가 메시지를 받습니다. 해당 정보가 입력되면 사용자는 추가 Azure Active Directory 인증을 요구하는 메시지를 받습니다. 이 메시지는 Azure의 Azure AD 애플리케이션에서 액세스 권한을 부여받은 Azure 계정의 자격 증명을 요구합니다.

> [!NOTE]
> 게이트웨이 머신에 대한 **관리자 권한**이 있는 Windows 계정의 사용자에게는 Azure AD 인증을 요구하는 메시지가 표시되지 않습니다.

### <a name="configuring-azure-active-directory-authentication-for-windows-admin-center-preview"></a>Windows Admin Center 미리 보기에 대한 Azure Active Directory 인증 구성

Windows Admin Center **설정** > **액세스**로 차례로 이동하고, 토글 스위치를 사용하여 "Azure Active Directory를 사용하여 게이트웨이에 보안 계층 추가"를 설정합니다. 게이트웨이를 Azure에 등록하지 않은 경우 지금 이 작업을 수행하는 방법을 안내합니다.

기본적으로 Azure AD 테넌트의 모든 멤버는 Windows Admin Center 게이트웨이 서비스에 대한 사용자 액세스 권한을 갖습니다. 게이트웨이 머신의 로컬 관리자만 Windows Admin Center 게이트웨이에 대한 관리자 액세스 권한을 갖습니다. 게이트웨이 머신에 대한 로컬 관리자의 권한은 제한할 수 없습니다. Azure AD가 인증에 사용되는지 여부에 관계없이 로컬 관리자는 모든 작업을 수행할 수 있습니다.

특정 Azure AD 사용자, 그룹 게이트웨이 사용자 또는 게이트웨이 관리자에게 Windows Admin Center 서비스에 대한 액세스 권한을 부여하려면 다음을 수행해야 합니다.

1.  [액세스 설정]에 제공된 하이퍼링크를 사용하여 Azure Portal의 Windows Admin Center Azure AD 애플리케이션으로 이동합니다. 이 하이퍼링크는 Azure Active Directory 인증을 사용하도록 설정된 경우에만 사용할 수 있습니다. 
    -   Azure Portal에서 **Azure Active Directory** > **엔터프라이즈 애플리케이션** > **모든 애플리케이션**으로 차례로 이동하고 **WindowsAdminCenter**를 검색하여 애플리케이션을 찾을 수도 있습니다(Azure AD 앱의 이름은 WindowsAdminCenter-<gateway name>임). 검색 결과를 가져올 수 없으면 **표시**가 **모든 애플리케이션**으로 설정되어 있고 **애플리케이션 상태**가 **모두**로 설정되어 있는지 확인하고, [적용]을 클릭한 다음, 검색을 시도합니다. 애플리케이션을 찾았으면 **사용자 및 그룹**으로 이동합니다.
2.  [속성] 탭에서 필요한 **사용자 할당 필요**를 [예]로 설정합니다.
    이 작업이 완료되면 **사용자 및 그룹** 탭에 나열된 멤버만 Windows Admin Center 게이트웨이에 액세스할 수 있습니다.
3.  [사용자 및 그룹] 탭에서 **사용자 추가**를 선택합니다. 추가된 각 사용자/그룹에 대해 게이트웨이 사용자 또는 게이트웨이 관리자 역할을 할당해야 합니다.

Azure AD 인증이 설정되면 게이트웨이 서비스가 다시 시작되고 브라우저를 새로 고쳐야 합니다. SME Azure AD 애플리케이션에 대한 사용자 액세스는 언제든지 Azure Portal에서 업데이트할 수 있습니다.

Windows Admin Center 게이트웨이 URL에 액세스하려고 하면 Azure Active Directory ID를 사용하여 로그인하라는 메시지가 표시됩니다. Windows Admin Center에 액세스하려면 게이트웨이 서버에서 로컬 사용자의 멤버여야 합니다.

사용자와 관리자는 Windows Admin Center 설정의 **계정** 탭에서 현재 로그인한 계정뿐만 아니라 이 Azure AD 계정의 로그아웃도 볼 수 있습니다.

### <a name="configuring-azure-active-directory-authentication-for-windows-admin-center"></a>Windows Admin Center에 대한 Azure Active Directory 인증 구성

[Azure AD 인증을 설정하려면 먼저 게이트웨이를 Azure에 등록해야 합니다](azure-integration.md)(이 작업은 Windows Admin Center 게이트웨이에 대해 한 번만 수행해야 함). 이 단계에서는 게이트웨이 사용자 및 게이트웨이 관리자 액세스를 관리할 수 있는 Azure AD 애플리케이션을 만듭니다.

특정 Azure AD 사용자, 그룹 게이트웨이 사용자 또는 게이트웨이 관리자에게 Windows Admin Center 서비스에 대한 액세스 권한을 부여하려면 다음을 수행해야 합니다.

1.  Azure Portal에서 SME Azure AD 애플리케이션으로 이동합니다. 
    -   **액세스 제어 변경**을 클릭한 다음, Windows Admin Center 액세스 설정에서 **Azure Active Directory**를 선택하면 UI에 제공된 하이퍼링크를 사용하여 Azure Portal의 Azure AD 애플리케이션에 액세스할 수 있습니다. 또한 이 하이퍼링크는 저장을 클릭하고 액세스 제어 ID 공급자로 Azure AD를 선택한 후에 [액세스 설정]에서 사용할 수 있습니다.
    -   **Azure Active Directory** > **엔터프라이즈 애플리케이션** > **모든 애플리케이션**으로 차례로 이동하고 **SME**를 검색하여 Azure Portal에서 애플리케이션을 찾을 수도 있습니다(Azure AD 앱의 이름은 SME-<gateway>임). 검색 결과를 가져올 수 없으면 **표시**가 **모든 애플리케이션**으로 설정되어 있고 **애플리케이션 상태**가 **모두**로 설정되어 있는지 확인하고, [적용]을 클릭한 다음, 검색을 시도합니다. 애플리케이션을 찾았으면 **사용자 및 그룹**으로 이동합니다.
2.  [속성] 탭에서 필요한 **사용자 할당 필요**를 [예]로 설정합니다.
    이 작업이 완료되면 **사용자 및 그룹** 탭에 나열된 멤버만 Windows Admin Center 게이트웨이에 액세스할 수 있습니다.
3.  [사용자 및 그룹] 탭에서 **사용자 추가**를 선택합니다. 추가된 각 사용자/그룹에 대해 게이트웨이 사용자 또는 게이트웨이 관리자 역할을 할당해야 합니다.

**액세스 제어 변경** 창에서 Azure AD 액세스 제어가 저장되면 게이트웨이 서비스가 다시 시작되고 브라우저를 새로 고쳐야 합니다. Windows Admin Center Azure AD 애플리케이션에 대한 사용자 액세스는 언제든지 Azure Portal에서 업데이트할 수 있습니다. 

Windows Admin Center 게이트웨이 URL에 액세스하려고 하면 Azure Active Directory ID를 사용하여 로그인하라는 메시지가 표시됩니다. Windows Admin Center에 액세스하려면 게이트웨이 서버에서 로컬 사용자의 멤버여야 합니다. 

Windows Admin Center 일반 설정의 **Azure** 탭을 사용하면 현재 로그인한 계정뿐만 아니라 이 Azure AD 계정의 로그아웃도 볼 수 있습니다.

### <a name="conditional-access-and-multi-factor-authentication"></a>조건부 액세스 및 다단계 인증

추가 보안 계층으로 Azure AD를 사용하여 Windows Admin Center 게이트웨이에 대한 액세스를 제어하는 이점 중 하나는 조건부 액세스 및 다단계 인증과 같은 Azure AD의 강력한 보안 기능을 활용할 수 있다는 것입니다. 

[Azure Active Directory를 사용하여 조건부 액세스를 구성하는 방법에 대해 자세히 알아보세요.](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## <a name="configure-single-sign-on"></a>Single Sign-On 구성

**Windows Server에 서비스로 배포된 경우의 Single Sign-On**

Windows Admin Center를 Windows 10에 설치하면 Single Sign-On을 사용할 수 있습니다. 그러나 Windows Server에서 Windows Admin Center를 사용하려면 Single Sign-On을 사용하기 전에 먼저 사용자 환경에서 특정 형태의 Kerberos 위임을 설정해야 합니다. 위임은 게이트웨이 컴퓨터를 대상 노드에 위임하도록 신뢰할 수 있는 것으로 구성합니다. 

사용자 환경에서 [리소스 기반 제한 위임](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview)을 구성하려면 다음 PowerShell 예제를 사용합니다. 이 예제에서는 contoso.com 도메인의 Windows Admin Center 게이트웨이 [wac.contoso.com]에서 위임을 수락하도록 Windows Server [node01.contoso.com]을 구성하는 방법을 보여줍니다.

```powershell
Set-ADComputer -Identity (Get-ADComputer node01) -PrincipalsAllowedToDelegateToAccount (Get-ADComputer wac)
```

이 관계를 제거하려면 다음 cmdlet을 실행합니다.

```powershell
Set-ADComputer -Identity (Get-ADComputer node01) -PrincipalsAllowedToDelegateToAccount $null
```

## <a name="role-based-access-control"></a>역할 기반 액세스 제어

역할 기반 액세스 제어를 사용하도록 설정하면 사용자에게 모든 로컬 관리자 권한을 설정하는 대신 머신에 대한 제한된 액세스 권한을 제공할 수 있습니다.
[역할 기반 액세스 제어 및 사용 가능한 역할에 대해 자세히 알아보세요.](../plan/user-access-options.md#role-based-access-control)

RBAC 설정은 대상 컴퓨터에서 지원을 사용하도록 설정하고 사용자를 관련 역할에 할당하는 두 단계로 구성됩니다.

> [!TIP]
> 역할 기반 액세스 제어를 지원하도록 구성하는 머신에 대한 로컬 관리자 권한이 있는지 확인하세요.

### <a name="apply-role-based-access-control-to-a-single-machine"></a>단일 머신에 역할 기반 액세스 제어 적용

단일 머신 배포 모델은 몇 개의 컴퓨터만 관리하는 간단한 환경에 적합합니다.
역할 기반 액세스 제어를 지원하는 머신을 구성하면 다음과 같이 변경됩니다.

-   Windows Admin Center에 필요한 기능이 있는 PowerShell 모듈이 시스템 드라이브의 `C:\Program Files\WindowsPowerShell\Modules` 아래에 설치됩니다. 모든 모듈은 **Microsoft.Sme**로 시작합니다.
-   Desired State Configuration에서 일회성 구성을 실행하여 **Microsoft.Sme.PowerShell**이라는 Just Enough Administration 엔드포인트를 머신에 구성합니다. 이 엔드포인트는 Windows Admin Center에서 사용하는 세 가지 역할을 정의하며, 사용자가 이 역할에 연결할 때 임시 로컬 관리자로 실행됩니다.
-   특정 역할에 대한 액세스 권한이 할당된 사용자를 제어하기 위해 다음 3개의 로컬 그룹이 새로 만들어집니다.
    -   Windows Admin Center 관리자
    -   Windows Admin Center Hyper-V 관리자
    -   Windows Admin Center 읽기 권한자

단일 머신에서 역할 기반 액세스 제어를 지원하도록 설정하려면 다음 단계를 수행합니다.

1.  Windows Admin Center를 열고, 대상 머신에 대한 로컬 관리자 권한이 있는 계정을 사용하여 역할 기반 액세스를 제어하도록 구성하려는 머신에 연결합니다.
2.  **개요** 도구에서 **설정** > **역할 기반 액세스 제어**를 차례로 클릭합니다.
3.  페이지 아래쪽에서 **적용**을 클릭하여 대상 컴퓨터에서 역할 기반 액세스 제어를 지원하도록 설정합니다. 애플리케이션 프로세스에는 PowerShell 스크립트를 복사하고 대상 머신에서 PowerShell Desired State Configuration을 사용하여 구성을 호출하는 작업이 포함됩니다. 완료하는 데 최대 10분이 걸릴 수 있으며, WinRM이 다시 시작됩니다. 이 경우 Windows Admin Center, PowerShell 및 WMI 사용자의 연결이 일시적으로 끊어집니다.
4.  페이지를 새로 고쳐 역할 기반 액세스 제어의 상태를 확인합니다. 사용할 준비가 되면 상태가 **적용됨**으로 변경됩니다.

구성이 적용되면 사용자를 역할에 할당할 수 있습니다.

1.  **로컬 사용자 및 그룹** 도구를 열고, **그룹** 탭으로 이동합니다.
2.  **Windows Admin Center 읽기 권한자** 그룹을 선택합니다.
3.  아래쪽의 *세부 정보* 창에서 **사용자 추가**를 클릭하고, Windows Admin Center를 통해 서버에 대한 읽기 전용 액세스 권한이 있어야 하는 사용자 또는 보안 그룹의 이름을 입력합니다. 사용자 및 그룹은 로컬 머신 또는 Active Directory 도메인에서 가져올 수 있습니다.
4.  **Windows Admin Center Hyper-V 관리자** 및 **Windows Admin Center 관리자** 그룹에 대해 2-3단계를 반복합니다.

또한 [제한된 그룹 정책 설정](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc756802%28v=ws.10%29)에서 그룹 정책 개체를 구성하여 이러한 그룹을 도메인 전체에서 일관되게 채울 수도 있습니다.

### <a name="apply-role-based-access-control-to-multiple-machines"></a>여러 머신에 역할 기반 액세스 제어 적용

대규모 엔터프라이즈 배포에서는 기존 자동화 도구를 통해 Windows Admin Center 게이트웨이에서 구성 패키지를 다운로드하여 역할 기반 액세스 제어 기능을 컴퓨터로 푸시할 수 있습니다.
구성 패키지는 PowerShell Desired State Configuration에서 사용하도록 설계되었지만 기본 설정 자동화 솔루션을 사용하도록 조정할 수 있습니다.

#### <a name="download-the-role-based-access-control-configuration"></a>역할 기반 액세스 제어 구성 다운로드

역할 기반 액세스 제어 구성 패키지를 다운로드하려면 Windows Admin Center 및 PowerShell 프롬프트에 액세스해야 합니다.

Windows Server에서 Windows Admin Center 게이트웨이를 서비스 모드로 실행하는 경우 다음 명령을 사용하여 구성 패키지를 다운로드합니다.
게이트웨이 주소를 사용자 환경에 맞는 올바른 주소로 업데이트해야 합니다.

```powershell
$WindowsAdminCenterGateway = 'https://windowsadmincenter.contoso.com'
Invoke-RestMethod -Uri "$WindowsAdminCenterGateway/api/nodes/all/features/jea/endpoint/export" -Method POST -UseDefaultCredentials -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Windows 10 머신에서 Windows Admin Center 게이트웨이를 실행하는 경우 다음 명령을 대신 실행합니다.

```powershell
$cert = Get-ChildItem Cert:\CurrentUser\My | Where-Object Subject -eq 'CN=Windows Admin Center Client' | Select-Object -First 1
Invoke-RestMethod -Uri "https://localhost:6516/api/nodes/all/features/jea/endpoint/export" -Method POST -Certificate $cert -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

zip 보관 파일을 확장하면 다음과 같은 폴더 구조가 표시됩니다.

- InstallJeaFeatures.ps1
- JustEnoughAdministration(단일 디렉터리)
- Modules(단일 디렉터리)
    - Microsoft.SME.\*(다중 디렉터리)
    - WindowsAdminCenter.Jea(단일 디렉터리)

노드에서 역할 기반 액세스 제어를 지원하도록 구성하려면 다음 작업을 수행해야 합니다.

1.  JustEnoughAdministration, Microsoft.SME.\* 및 WindowsAdminCenter.Jea 모듈을 대상 머신의 PowerShell 모듈 디렉터리에 복사합니다. 일반적으로 이 위치는 `C:\Program Files\WindowsPowerShell\Modules`입니다.
2.  RBAC 엔드포인트에 원하는 구성과 일치하도록 **InstallJeaFeature.ps1** 파일을 업데이트합니다.
3.  InstallJeaFeature.ps1을 실행하여 DSC 리소스를 컴파일합니다.
4.  DSC 구성을 모든 머신에 배포하여 해당 구성을 적용합니다.

다음 섹션에서는 PowerShell 원격을 사용하여 이 작업을 수행하는 방법에 대해 설명합니다.

#### <a name="deploy-on-multiple-machines"></a>여러 머신에 배포

다운로드한 구성을 여러 머신에 배포하려면 사용자 환경에 적합한 보안 그룹을 포함하도록 **InstallJeaFeatures.ps1** 스크립트를 업데이트하고, 해당 파일을 각 컴퓨터에 복사하고, 구성 스크립트를 호출해야 합니다.
이 작업은 기본 설정 자동화 도구를 사용하여 수행할 수 있지만, 이 문서에서는 순수한 PowerShell 기반 접근 방식에 중점을 둡니다.

구성 스크립트는 기본적으로 각 역할에 대한 액세스를 제어하기 위해 로컬 보안 그룹을 머신에 만듭니다.
이는 작업 그룹 및 도메인 조인 머신에 적합하지만, 도메인 전용 환경에서 배포하는 경우 도메인 보안 그룹을 각 역할에 직접 연결하는 것이 좋습니다.
도메인 보안 그룹을 사용하도록 구성을 업데이트하려면 **InstallJeaFeatures.ps1**을 열고 다음과 같이 변경합니다.

1.  파일에서 다음 세 개의 **그룹** 리소스를 제거합니다.
    1.  "Group MS-Readers-Group"
    2.  "Group MS-Hyper-V-Administrators-Group"
    3.  "Group MS-Administrators-Group"
2.  JeaEndpoint **DependsOn** 속성에서 다음 세 개의 그룹 리소스를 제거합니다.
    1.  "[Group]MS-Readers-Group"
    2.  "[Group]MS-Hyper-V-Administrators-Group"
    3.  "[Group]MS-Administrators-Group"
3.  JeaEndpoint **RoleDefinitions** 속성의 그룹 이름을 원하는 보안 그룹으로 변경합니다. 예를 들어 Windows Admin Center 관리자 역할에 대한 액세스 권한을 할당해야 하는 *CONTOSO\MyTrustedAdmins* 보안 그룹이 있는 경우 `'$env:COMPUTERNAME\Windows Admin Center Administrators'`를 `'CONTOSO\MyTrustedAdmins'`로 변경합니다. 업데이트해야 하는 세 개의 문자열은 다음과 같습니다.
    1.  '$env:COMPUTERNAME\Windows Admin Center Administrators'
    2.  '$env:COMPUTERNAME\Windows Admin Center Hyper-V Administrators'
    3.  '$env:COMPUTERNAME\Windows Admin Center Readers'

> [!NOTE]
> 각 역할에 대해 고유한 보안 그룹을 사용해야 합니다. 동일한 보안 그룹이 여러 역할에 할당되면 구성이 실패합니다.

다음으로, **InstallJeaFeatures.ps1** 파일의 끝에 있는 스크립트의 아래쪽에 다음 PowerShell 줄을 추가합니다.

```powershell
Copy-Item "$PSScriptRoot\JustEnoughAdministration" "$env:ProgramFiles\WindowsPowerShell\Modules" -Recurse -Force
$ConfigData = @{
    AllNodes = @()
    ModuleBasePath = @{
        Source = "$PSScriptRoot\Modules"
        Destination = "$env:ProgramFiles\WindowsPowerShell\Modules"
    }
}
InstallJeaFeature -ConfigurationData $ConfigData | Out-Null
Start-DscConfiguration -Path "$PSScriptRoot\InstallJeaFeature" -JobName "Installing JEA for Windows Admin Center" -Force
```

마지막으로, 모듈, DSC 리소스 및 구성이 포함된 폴더를 각 대상 노드에 복사하고, **InstallJeaFeature.ps1** 스크립트를 실행할 수 있습니다.
관리자 워크스테이션에서 원격으로 이 작업을 수행하려면 다음 명령을 실행할 수 있습니다.

```powershell
$ComputersToConfigure = 'MyServer01', 'MyServer02'

$ComputersToConfigure | ForEach-Object {
    $session = New-PSSession -ComputerName $_ -ErrorAction Stop
    Copy-Item -Path "~\Desktop\WindowsAdminCenter_RBAC\JustEnoughAdministration\" -Destination "$env:ProgramFiles\WindowsPowerShell\Modules\" -ToSession $session -Recurse -Force
    Copy-Item -Path "~\Desktop\WindowsAdminCenter_RBAC" -Destination "$env:TEMP\WindowsAdminCenter_RBAC" -ToSession $session -Recurse -Force
    Invoke-Command -Session $session -ScriptBlock { Import-Module JustEnoughAdministration; & "$env:TEMP\WindowsAdminCenter_RBAC\InstallJeaFeature.ps1" } -AsJob
    Disconnect-PSSession $session
}
```
