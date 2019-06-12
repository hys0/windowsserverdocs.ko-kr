---
title: 사용자 access control 및 권한 구성
description: 사용자 액세스 제어 및 Active Directory 또는 Azure AD (프로젝트 브라 티)를 사용 하 여 권한을 구성 하는 방법 알아보기
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 96d09b25ddb2f473fb4fe22c0cf716bfcf8becaa
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811931"
---
# <a name="configure-user-access-control-and-permissions"></a>사용자 Access Control 및 권한 구성

> 적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

이미 않았다면 숙지 합니다 [Windows Admin Center 사용자 액세스 제어 옵션](../plan/user-access-options.md)

> [!NOTE]
> 트러스트 되지 않은 도메인 또는 작업 그룹 환경에서는 그룹 기반 액세스 Windows Admin Center 지원 되지 않습니다.

## <a name="gateway-access-role-definitions"></a>게이트웨이 액세스 역할 정의

Windows Admin Center 게이트웨이 서비스에 액세스 하기 위한 두 가지 역할이 있습니다.

**게이트웨이 사용자** 해당 게이트웨이 통해 서버를 관리 하기 위해 Windows Admin Center 게이트웨이 서비스에 연결할 수 있지만 게이트웨이 인증에 사용 하는 인증 메커니즘 또는 액세스 권한을 변경할 수 없습니다.

**게이트웨이 관리자** 게이트웨이에 사용자를 인증 방법과 누가 액세스도 구성할 수 있습니다. 게이트웨이 관리자만 볼 수 있으며 Windows Admin Center 액세스 설정을 구성 됩니다. 게이트웨이 컴퓨터의 로컬 관리자는 항상 Windows Admin Center 게이트웨이 서비스의 관리자입니다.

> [!NOTE]
> 게이트웨이에 액세스할 수는 게이트웨이에 의해 표시 되는 관리 되는 서버에 대 한 액세스를 의미 하지 않습니다. 연결 하는 사용자를 대상 서버를 관리 하려면 자격 증명을 사용 해야 합니다 (해당 통과 Windows 자격 증명을 통해 또는 사용 하 여 Windows Admin Center 세션에 제공 된 자격 증명을 통해 합니다 **로 관리** 작업)는 해당 대상 서버에 대 한 액세스를 관리 합니다.

## <a name="active-directory-or-local-machine-groups"></a>Active Directory 또는 로컬 컴퓨터 그룹

기본적으로 Active Directory 또는 로컬 컴퓨터 그룹은 게이트웨이 액세스를 제어 하도록 사용 됩니다. Active Directory 도메인에 있는 게이트웨이 사용자 및 관리자가 관리할 수 있습니다 Windows Admin Center 인터페이스 내에서 액세스 합니다.

에 **사용자** 게이트웨이 사용자로 Windows Admin Center 액세스할 수 있는 탭을 제어할 수 있습니다. 기본적으로 게이트웨이 URL에 액세스 하는 모든 사용자가 액세스 하는 보안 그룹을 지정 하지 않으면, 및입니다. 사용자 목록에 하나 이상의 보안 그룹을 추가한 후 액세스 해당 그룹의 멤버 에게만 부여 됩니다.

으로 액세스가 제어 됩니다 Active Directory 도메인 환경에서를 사용 하지 않는 경우는 `Users` 고 `Administrators` Windows Admin Center 게이트웨이 컴퓨터의 로컬 그룹입니다.

### <a name="smartcard-authentication"></a>스마트 카드 인증

적용할 수 있습니다 **스마트 카드 인증** 추가로 지정 하 여 _필수_ 스마트 카드 기반 보안 그룹에 대 한 그룹입니다. 스마트 카드 기반 보안 그룹을 추가한 후 사용자만 액세스할 수 있습니다 Windows Admin Center 서비스 보안 그룹의 멤버인 경우 스마트 카드 그룹 사용자 목록에 포함 합니다.

에 **관리자** 게이트웨이 관리자로 Windows Admin Center 액세스할 수 있는 탭을 제어할 수 있습니다. 컴퓨터의 로컬 관리자 그룹은 항상 전체 관리자 액세스 권한 및 목록에서 제거할 수 없습니다. 보안 그룹에 추가 하 여 Windows Admin Center 게이트웨이 설정을 변경 하려면 해당 그룹 권한의 멤버를 제공 합니다. 동일한 방식으로 사용자 목록에 스마트 카드 인증에서는 관리자 목록: 보안 그룹 및 스마트 카드 그룹에 대해 AND 조건을 사용 하 여 합니다.

## <a name="azure-active-directory"></a>Azure Active Directory

조직 Azure Active Directory (Azure AD)를 사용 하는 경우 추가할 수도 있습니다는 **추가** 게이트웨이에 액세스 하려면 Azure AD 인증을 요구 하 여 Windows Admin Center 보안 계층입니다. Windows Admin Center, 사용자의 액세스 하기 위해 **Windows 계정** (경우에 Azure AD 인증이 사용 됨) 게이트웨이 서버에 액세스할 수 있어야 합니다. Azure AD를 사용 하면 관리 하려는 Windows Admin Center 사용자 및 관리자 액세스 권한 내에서 아니라 Azure Portal에서 Windows Admin Center UI입니다.

### <a name="accessing-windows-admin-center-when-azure-ad-authentication-is-enabled"></a>Azure AD 인증을 사용 하는 경우 Windows Admin Center 액세스

구성 된 Azure AD 인증을 사용 하 여 Windows Admin Center 액세스 하는 일부 사용자는 추가 프롬프트를을 수신 하는 데 사용 되는 브라우저에 따라 **브라우저에서** 에 대 한 Windows 계정 자격 증명을 제공 하기 위해 필요한 위치 Windows Admin Center 설치 된 컴퓨터. 해당 정보를 입력 한 후 사용자가 Azure에서 Azure AD 응용 프로그램에 대 한 액세스 권한이 있는 Azure 계정 자격 증명을 요구 하는 추가 Azure Active Directory 인증 프롬프트를 받습니다.

> [!NOTE]
> Windows 사용자 계정에 **관리자 권한** 게이트웨이에서 컴퓨터 하지 않게 됩니다에 대 한 Azure AD 인증.

### <a name="configuring-azure-active-directory-authentication-for-windows-admin-center-preview"></a>Windows Admin Center 미리 보기에 대 한 Azure Active Directory 인증 구성

Windows Admin Center 이동 **설정을** > **액세스** 토글 스위치를 사용 하 여 설정 하 고 "사용 하 여 게이트웨이에 보안 계층을 추가 하려면 Azure Active Directory"입니다. Azure 게이트웨이 등록 하지 않은 경우이 이번에 이렇게 하려면 안내 합니다.

기본적으로 Azure AD 테 넌 트의 모든 멤버는 Windows Admin Center 게이트웨이 서비스에 대 한 사용자 액세스를 갖습니다. Windows Admin Center 게이트웨이 관리자 액세스 권한을 보유 하는 게이트웨이 컴퓨터의 로컬 관리자만 합니다. 게이트웨이 컴퓨터의 로컬 관리자의 권한을 제한할 수 없습니다-로컬 관리자는 Azure AD 인증에 사용 되는 여부에 관계 없이 수행할 수는 note 합니다.

사용자에 게 특정 Azure AD 그룹 게이트웨이 사용자 또는 Windows Admin Center 서비스에 대 한 게이트웨이 관리자가 액세스 하려는 경우 다음을 수행 해야 합니다.

1.  액세스 설정에 제공 된 하이퍼링크를 사용 하 여 Azure portal에서 Azure AD Windows Admin Center 응용 프로그램으로 이동 합니다. 이 하이퍼링크 Azure Active Directory 인증을 사용 하는 경우에 사용할 수는 note 합니다. 
    -   으로 이동 하 여 Azure portal에서 응용 프로그램을 찾을 수도 있습니다 **Azure Active Directory** > **엔터프라이즈 응용 프로그램** > **모든응용프로그램** 검색과 **WindowsAdminCenter** (Azure AD 앱 이름은 WindowsAdminCenter-<gateway name>). 검색 결과 얻지 못한 경우 확인 **표시** 로 설정 된 **모든 응용 프로그램**합니다 **응용 프로그램 상태** 로 설정 되어 **모든** 적용을 클릭 하 고 검색을 시도 합니다. 로 이동 하는 응용 프로그램을 찾았으면 **사용자 및 그룹**
2.  속성 탭에서 설정할 **사용자 할당 필요** ' 예 '로 합니다.
    이 작업을 수행한에 멤버만 표시는 **사용자 및 그룹** 탭 Windows Admin Center 게이트웨이에 액세스할 수 있게 됩니다.
3.  사용자 및 그룹 탭에서 선택 **사용자 추가**합니다. 게이트웨이 사용자 또는 각 사용자/그룹 추가 대 한 게이트웨이 관리자 역할을 할당 해야 합니다.

Azure AD 인증을 설정한 후 게이트웨이 서비스를 다시 시작 하 고 해야 브라우저를 새로 고치십시오. 언제 든 지 Azure portal에서 Azure AD SME 응용 프로그램에 대 한 사용자 액세스를 업데이트할 수 있습니다.

사용자는 Windows Admin Center 게이트웨이 URL에 액세스 하려고 할 때 자신의 Azure Active Directory id를 사용 하 여 로그인 해야 합니다. 사용자가 Windows Admin Center 액세스 하려면 게이트웨이 서버에서 로컬 사용자의 구성원도 되도록 해야 합니다.

사용자와 관리자가 현재 로그인 한 계정을 볼 수 있습니다 및도이 Azure AD 계정에서 로그 아웃 합니다 **계정** Windows Admin Center 설정 탭입니다.

### <a name="configuring-azure-active-directory-authentication-for-windows-admin-center"></a>Windows Admin Center 대 한 Azure Active Directory 인증 구성

[Azure AD 인증을 설정 하려면 먼저 등록 해야 게이트웨이가 Azure를 사용 하 여](azure-integration.md) (만 Windows Admin Center 게이트웨이에 대 한 번만 수행 해야 함). 이 단계는 게이트웨이 사용자와 게이트웨이 관리자 액세스 권한을 관리할 수 있습니다 Azure AD 응용 프로그램을 만듭니다.

사용자에 게 특정 Azure AD 그룹 게이트웨이 사용자 또는 Windows Admin Center 서비스에 대 한 게이트웨이 관리자가 액세스 하려는 경우 다음을 수행 해야 합니다.

1.  Azure portal에서 Azure AD SME 응용 프로그램으로 이동 합니다. 
    -   클릭 하면 **변경 액세스 제어** 선택한 후 **Azure Active Directory** Windows Admin Center 액세스 설정에서 Azure AD에 액세스 하려면 UI에 있는 하이퍼링크를 사용할 수 있습니다 Azure portal에서 응용 프로그램입니다. 저장을 클릭 하 고 액세스 제어 id 공급자로 Azure AD를 선택한 후에이 하이퍼링크 액세스 설정에서 제공 됩니다.
    -   으로 이동 하 여 Azure portal에서 응용 프로그램을 찾을 수도 있습니다 **Azure Active Directory** > **엔터프라이즈 응용 프로그램** > **모든응용프로그램** 검색과 **SME** (Azure AD 앱 이름은 SME-<gateway>). 검색 결과 얻지 못한 경우 확인 **표시** 로 설정 된 **모든 응용 프로그램**합니다 **응용 프로그램 상태** 로 설정 되어 **모든** 적용을 클릭 하 고 검색을 시도 합니다. 로 이동 하는 응용 프로그램을 찾았으면 **사용자 및 그룹**
2.  속성 탭에서 설정할 **사용자 할당 필요** ' 예 '로 합니다.
    이 작업을 수행한에 멤버만 표시는 **사용자 및 그룹** 탭 Windows Admin Center 게이트웨이에 액세스할 수 있게 됩니다.
3.  사용자 및 그룹 탭에서 선택 **사용자 추가**합니다. 게이트웨이 사용자 또는 각 사용자/그룹 추가 대 한 게이트웨이 관리자 역할을 할당 해야 합니다.

Azure AD에 저장 한 후의 액세스 제어를 **변경 액세스 제어** 창 게이트웨이 서비스를 다시 시작 하 고 브라우저를 새로 고쳐야 합니다. 언제 든 지 Azure portal에서 Azure AD Windows Admin Center 응용 프로그램에 대 한 사용자 액세스를 업데이트할 수 있습니다. 

사용자는 Windows Admin Center 게이트웨이 URL에 액세스 하려고 할 때 자신의 Azure Active Directory id를 사용 하 여 로그인 해야 합니다. 사용자가 Windows Admin Center 액세스 하려면 게이트웨이 서버에서 로컬 사용자의 구성원도 되도록 해야 합니다. 

사용 하는 **Azure** Windows Admin Center 일반 설정, 사용자 및 관리자의 탭에 현재 로그인 한 계정에 볼 수 있습니다 및이 Azure AD 계정으로 로그 아웃도 합니다.

### <a name="conditional-access-and-multi-factor-authentication"></a>조건부 액세스 및 multi-factor authentication

추가 보안 계층으로 Azure AD를 사용 하 여 Windows Admin Center 게이트웨이에 대 한 액세스 제어의 이점 중 하나는 조건부 액세스 및 multi-factor authentication과 같은 Azure AD의 강력한 보안 기능을 활용할 수 있습니다. 

[Azure Active Directory를 사용 하 여 조건부 액세스를 구성 하는 방법에 대 한 자세히 알아봅니다.](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## <a name="configure-single-sign-on"></a>Single Sign-On 구성

**Single sign on Windows Server에 서비스로 배포 하는 경우**

Windows 10에서 Windows Admin Center 설치할 때 single sign-on을 사용할 준비가 됩니다. 하지만 Windows Server에서 Windows Admin Center 사용 하려는 경우에 single sign on 사용 하기 전에 특정 형태의 사용자 환경에서 Kerberos 위임 설정 해야 합니다. 위임으로 대상 노드에 대 한 대리자로 신뢰를 게이트웨이 컴퓨터를 구성 합니다. 

구성 하려면 [리소스 기반의 제한 위임](http://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-1) 사용자 환경에서 다음 PowerShell cmdlet을 실행 합니다. (이 Windows Server 2012를 실행 하는 도메인 컨트롤러를 위해서는 인식 이상을 수).

```powershell
     $gateway = "WindowsAdminCenterGW" # Machine where Windows Admin Center is installed
     $node = "ManagedNode" # Machine that you want to manage
     $gatewayObject = Get-ADComputer -Identity $gateway
     $nodeObject = Get-ADComputer -Identity $node
     Set-ADComputer -Identity $nodeObject -PrincipalsAllowedToDelegateToAccount $gatewayObject
```

이 예제에서는 Windows Admin Center 게이트웨이 서버에 설치 되어 **WindowsAdminCenterGW**, 대상 노드 이름은 **ManagedNode**합니다.

이 관계를 제거 하려면 다음 cmdlet을 실행 합니다.

```powershell
Set-ADComputer -Identity $nodeObject -PrincipalsAllowedToDelegateToAccount $null
```

## <a name="role-based-access-control"></a>역할 기반 액세스 제어

역할 기반 액세스 제어를 사용 하면 전체 로컬 관리자가 하는 대신 컴퓨터에 대 한 액세스가 제한 된 사용자를 제공할 수 있습니다.
[역할 기반 액세스 제어 및 사용 가능한 역할에 대해 읽어보세요.](../plan/user-access-options.md#role-based-access-control)

2 단계로 이루어져 있습니다 RBAC를 설정 합니다: 대상 컴퓨터에 대 한 지원을 사용 하도록 설정 하 고 관련 역할에 사용자를 할당 합니다.

> [!TIP]
> 컴퓨터에 대 한 로컬 관리자 권한이 있는지는 역할 기반 액세스 제어에 대 한 지원을 구성 하는 확인 합니다.

### <a name="apply-role-based-access-control-to-a-single-machine"></a>단일 컴퓨터에 역할 기반 액세스 제어 적용

단일 컴퓨터 배포 모델을 관리 하는 몇 가지 컴퓨터만을 사용 하 여 간단한 환경에 적합 합니다.
역할 기반 액세스 제어에 대 한 지원을 사용 하 여 컴퓨터를 구성 하면 다음과 같이 변경 합니다.

-   아래 Windows Admin Center 필요한 함수를 사용 하 여 PowerShell 모듈은 시스템 드라이브에 설치 됩니다 `C:\Program Files\WindowsPowerShell\Modules`합니다. 모든 모듈 시작 **Microsoft.Sme**
-   Desired State Configuration 라는 컴퓨터에서 Just Enough Administration 끝점을 구성 하는 일회성 구성이 실행될지 **Microsoft.Sme.PowerShell**합니다. 이 끝점 Windows Admin Center 사용 하는 3 가지 역할을 정의 하 고 사용자를 연결 하는 경우 임시 로컬 관리자 권한으로 실행 됩니다.
-   액세스는 역할에 할당 된 사용자 컨트롤에 3 개의 새 로컬 그룹을 만듭니다.
    -   Windows Admin Center 관리자
    -   Windows Admin Center Hyper-v 관리자
    -   Windows Admin Center 판독기

단일 컴퓨터에서 역할 기반 액세스 제어에 대 한 지원을 사용 하려면 다음이 단계를 수행 합니다.

1.  Windows Admin Center 열고 대상 컴퓨터의 로컬 관리자 권한이 있는 계정을 사용 하 여 역할 기반 액세스 제어를 사용 하 여 구성 하려는 컴퓨터에 연결 합니다.
2.  에 **개요** 도구를 클릭 **설정** > **역할 기반 액세스 제어**입니다.
3.  클릭 **적용** 대상 컴퓨터의 역할 기반 액세스 제어에 대 한 지원을 사용 하도록 설정 페이지의 맨 아래에 있습니다. 응용 프로그램 프로세스에 대상 컴퓨터에서 PowerShell 스크립트를 복사 하 고 (사용 하 여 PowerShell Desired State Configuration) 하는 구성을 호출 포함 됩니다. 를 완료 하려면 최대 10 분이 걸릴 수 있습니다 및 WinRM을 다시 시작 됩니다. 이 Windows Admin Center, PowerShell 및 WMI 사용자가 일시적으로 끊어집니다.
4.  역할 기반 access control의 상태를 확인 하려면 페이지를 새로 고칩니다. 사용할 준비가 되었는지, 상태가 변경 됩니다 **적용**합니다.

구성이 적용 되 면 역할에 사용자를 할당할 수 있습니다.

1.  열기는 **로컬 사용자 및 그룹** 도구를 이동 합니다 **그룹** 탭 합니다.
2.  선택 된 **Windows Admin Center 판독기** 그룹입니다.
3.  에 *세부 정보* 창의 아래쪽에서 클릭 **사용자 추가** Windows Admin Center 통해 서버에 대 한 읽기 전용 액세스를 포함 해야 하는 사용자 또는 보안 그룹의 이름을 입력 합니다. 사용자 및 그룹을 로컬 컴퓨터 또는 Active Directory 도메인에서 가져올 수 있습니다.
4.  에 대 한 2-3 단계를 반복 합니다 **Windows Admin Center Hyper-v 관리자** 하 고 **Windows Admin Center 관리자** 그룹.

채울 수도 있습니다 이러한 그룹 일관 되 게 도메인 전체에서 사용 하 여 그룹 정책 개체를 구성 하 여 합니다 [제한 된 그룹 정책 설정을](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc756802%28v=ws.10%29)합니다.

### <a name="apply-role-based-access-control-to-multiple-machines"></a>여러 컴퓨터에 역할 기반 액세스 제어를 적용 합니다.

대규모 엔터프라이즈 배포에서 Windows Admin Center 게이트웨이에서 구성 패키지를 다운로드 하 여 역할 기반 액세스 제어 기능이 컴퓨터를 강제 기존 자동화 도구를 사용할 수 있습니다.
구성 패키지는 PowerShell Desired State Configuration 사용 하 여 사용할 만들어졌지만 기본 automation 솔루션이 사용 하도록 조정할 수 있습니다.

#### <a name="download-the-role-based-access-control-configuration"></a>역할 기반 액세스 제어 구성 다운로드

역할 기반 액세스 제어 구성 패키지를 다운로드 하려면 Windows Admin Center 및 PowerShell 프롬프트에 액세스할 수 있도록 해야 합니다.

Windows 서버에서 Windows Admin Center 게이트웨이 서비스 모드에서 실행 중인 경우 구성 패키지를 다운로드 하려면 다음 명령을 사용 합니다.
사용자 환경에 적절 한을 사용 하 여 게이트웨이 주소를 업데이트 해야 합니다.

```powershell
$WindowsAdminCenterGateway = 'https://windowsadmincenter.contoso.com'
Invoke-RestMethod -Uri "$WindowsAdminCenterGateway/api/nodes/all/features/jea/endpoint/export" -Method POST -UseDefaultCredentials -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Windows 10 컴퓨터에 Windows Admin Center 게이트웨이 실행 하는 경우 대신 다음 명령을 실행 합니다.

```powershell
$cert = Get-ChildItem Cert:\CurrentUser\My | Where-Object Subject -eq 'CN=Windows Admin Center Client' | Select-Object -First 1
Invoke-RestMethod -Uri "https://localhost:6516/api/nodes/all/features/jea/endpoint/export" -Method POST -Certificate $cert -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Zip 보관 파일을 확장 하면 다음 폴더 구조가 표시 됩니다.

- InstallJeaFeatures.ps1
- JustEnoughAdministration (디렉터리)
- 모듈 (디렉터리)
    - Microsoft.SME 합니다. \* (디렉터리)
    - WindowsAdminCenter.Jea (directory)

노드에서 역할 기반 액세스 제어에 대 한 지원을 구성 하려면 다음 작업을 수행 해야 합니다.

1.  Microsoft.SME JustEnoughAdministration를 복사 합니다. \*, 및 대상 컴퓨터에서 PowerShell 모듈 디렉터리로 WindowsAdminCenter.Jea 모듈입니다. 이 위치는 일반적으로 `C:\Program Files\WindowsPowerShell\Modules`입니다.
2.  업데이트 **InstallJeaFeature.ps1** RBAC 끝점에 대 한 원하는 구성과 일치 하도록 파일입니다.
3.  DSC 리소스를 컴파일하는 데 InstallJeaFeature.ps1를 실행 합니다.
4.  구성을 적용 하려면 컴퓨터의 모든 DSC 구성을 배포 합니다.

다음 섹션에서는 PowerShell 원격을 사용 하 여 이렇게 하는 방법에 설명 합니다.

#### <a name="deploy-on-multiple-machines"></a>여러 컴퓨터에 배포

여러 컴퓨터에 다운로드 한 구성을 배포를 업데이트 해야 합니다 **InstallJeaFeatures.ps1** 사용자 환경에 대 한 적절 한 보안 그룹, 각 컴퓨터에 파일을 복사 하는 스크립트 및 구성 스크립트를 호출 합니다.
하지만이 문서는 순수 PowerShell 기반 접근 방식을 중점적이 수행 하 여 기본 자동화 도구를 사용할 수 있습니다.

기본적으로 구성 스크립트를 각 역할에 대 한 액세스를 제어할 컴퓨터에서 로컬 보안 그룹이 만들어집니다.
이 작업 그룹에 적합 하며 도메인에 가입 된 컴퓨터에 있지만 직접 하려는 경우가 있습니다 도메인 전용 환경에서 구축 하는 경우 각 역할을 사용 하 여 도메인 보안 그룹을 연결 합니다.
도메인 보안 그룹을 사용 하도록 구성을 업데이트 하려면 엽니다 **InstallJeaFeatures.ps1** 다음과 같이 변경 하 고 있습니다.

1.  3 제거 **그룹** 파일에서 리소스:
    1.  "그룹 MS Readers 그룹"
    2.  "그룹 MS-하이퍼-V--" 관리자 그룹
    3.  "그룹 MS 관리자 그룹"
2.  JeaEndpoint에서 3 개의 그룹 리소스를 제거 **DependsOn** 속성
    1.  "[Group]MS-Readers-Group"
    2.  "[Group]MS-Hyper-V-Administrators-Group"
    3.  "[Group]MS-Administrators-Group"
3.  JeaEndpoint에서 그룹 이름을 변경할 **RoleDefinitions** 원하는 보안 그룹에는 속성입니다. 예를 들어 보안 그룹이 *CONTOSO\MyTrustedAdmins* 해야에 할당할 수 있는 액세스 Windows Admin Center 관리자 역할을 변경 `'$env:COMPUTERNAME\Windows Admin Center Administrators'` 하려면 `'CONTOSO\MyTrustedAdmins'`합니다. 업데이트 해야 하는 세 가지 문자열이 있습니다.
    1.  ' $env: COMPUTERNAME\Windows 관리자 센터 관리자 '
    2.  ' $env: COMPUTERNAME\Windows 관리 센터에서 Hyper-v 관리자
    3.  ' $env: COMPUTERNAME\Windows Admin Center Readers'

> [!NOTE]
> 각 역할에 대 한 고유한 보안 그룹을 사용 해야 합니다. 동일한 보안 그룹은 여러 역할에 할당 되 면 구성이 실패 합니다.

끝에 다음 합니다 **InstallJeaFeatures.ps1** 파일, 스크립트의 아래쪽에 PowerShell의 다음 줄을 추가 합니다.

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

마지막으로, 모듈, DSC 리소스 및 각 대상 노드에 구성을 포함 하는 폴더를 복사 하 수 실행 합니다 **InstallJeaFeature.ps1** 스크립트입니다.
이렇게 하려면 원격으로 관리 워크스테이션에서 다음 명령을 실행할 수 있습니다.

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
