---
title: 사용자 액세스 제어 및 권한 구성
description: Active Directory 또는 Azure AD (Project Honolulu)를 사용 하 여 사용자 액세스 제어 및 사용 권한을 구성 하는 방법을 알아봅니다.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 20b311e9330880c2b26e2494aabe27bb04891868
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407030"
---
# <a name="configure-user-access-control-and-permissions"></a>사용자 Access Control 및 사용 권한 구성

> 적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

아직 사용 하지 않은 경우 [Windows 관리 센터에서 사용자 액세스 제어 옵션](../plan/user-access-options.md) 을 숙지 하세요.

> [!NOTE]
> Windows 관리 센터의 그룹 기반 액세스는 작업 그룹 환경이 나 트러스트 되지 않은 도메인에서 지원 되지 않습니다.

## <a name="gateway-access-role-definitions"></a>게이트웨이 액세스 역할 정의

Windows 관리 센터 게이트웨이 서비스에 액세스 하기 위한 두 가지 역할은 다음과 같습니다.

**게이트웨이 사용자** 는 Windows 관리 센터 게이트웨이 서비스에 연결 하 여 해당 게이트웨이를 통해 서버를 관리할 수 있지만 액세스 권한 또는 게이트웨이 인증에 사용 되는 인증 메커니즘을 변경할 수는 없습니다.

**게이트웨이 관리자** 는 액세스 권한을 받는 사용자 및 사용자가 게이트웨이에 인증 하는 방법을 구성할 수 있습니다. 게이트웨이 관리자만 Windows 관리 센터에서 액세스 설정을 보고 구성할 수 있습니다. 게이트웨이 컴퓨터의 로컬 관리자는 항상 Windows 관리 센터 게이트웨이 서비스의 관리자입니다.

> [!NOTE]
> 게이트웨이에 대 한 액세스는 게이트웨이에서 볼 수 있는 관리 되는 서버에 대 한 액세스를 암시 하지 않습니다. 대상 서버를 관리 하려면 연결 하는 사용자가 관리 액세스 권한이 있는 전달 된 Windows 자격 증명 또는 **관리** 작업을 사용 하 여 Windows 관리 센터 세션에 제공 된 자격 증명을 통해 자격 증명을 사용 해야 합니다. 대상 서버에 연결할 수 있습니다.

## <a name="active-directory-or-local-machine-groups"></a>Active Directory 또는 로컬 컴퓨터 그룹

기본적으로 Active Directory 또는 로컬 컴퓨터 그룹은 게이트웨이 액세스를 제어 하는 데 사용 됩니다. Active Directory 도메인을 사용 하는 경우 Windows 관리 센터 인터페이스 내에서 게이트웨이 사용자 및 관리자 액세스를 관리할 수 있습니다.

**사용자** 탭에서 게이트웨이 사용자로 Windows 관리 센터에 액세스할 수 있는 사용자를 제어할 수 있습니다. 기본적으로 보안 그룹을 지정 하지 않으면 게이트웨이 URL에 액세스 하는 모든 사용자에 게 액세스 권한이 있습니다. 하나 이상의 보안 그룹을 사용자 목록에 추가 하면 해당 그룹의 멤버로 액세스가 제한 됩니다.

사용자 환경에서 Active Directory 도메인을 사용 하지 않는 경우 액세스는 Windows 관리 센터 게이트웨이 컴퓨터의 `Users` 및 @no__t 1 로컬 그룹에 의해 제어 됩니다.

### <a name="smartcard-authentication"></a>스마트 카드 인증

스마트 카드 기반 보안 그룹에 _필요한_ 추가 그룹을 지정 하 여 **스마트 카드 인증** 을 적용할 수 있습니다. 스마트 카드 기반 보안 그룹을 추가 하면 사용자가 사용자 목록에 포함 된 보안 그룹 및 스마트 카드 그룹의 멤버인 경우에만 Windows 관리 센터 서비스에 액세스할 수 있습니다.

**관리자** 탭에서 게이트웨이 관리자로 Windows 관리 센터에 액세스할 수 있는 사용자를 제어할 수 있습니다. 컴퓨터의 로컬 관리자 그룹은 항상 모든 관리자 액세스 권한을 가지 며 목록에서 제거할 수 없습니다. 보안 그룹을 추가 하 여 해당 그룹의 구성원에 게 Windows 관리 센터 게이트웨이 설정을 변경할 수 있는 권한을 부여 합니다. 관리자 목록은 사용자 목록과 동일한 방식으로 스마트 카드 인증을 지원 합니다. 보안 그룹 및 스마트 카드 그룹에 대 한 AND 조건이 사용 됩니다.

## <a name="azure-active-directory"></a>Azure Active Directory

조직에서 Azure Active Directory (Azure AD)를 사용 하는 경우 Azure AD 인증을 사용 하 여 게이트웨이에 액세스 하도록 요구 하 여 Windows 관리 센터에 **추가** 보안 계층을 추가 하도록 선택할 수 있습니다. Windows 관리 센터에 액세스 하려면 사용자의 **windows 계정** 에도 게이트웨이 서버에 대 한 액세스 권한이 있어야 합니다 (Azure AD 인증을 사용 하는 경우에도). Azure AD를 사용 하는 경우 Windows 관리 센터 UI 내에서가 아니라 Azure Portal에서 Windows 관리 센터 사용자 및 관리자 액세스 권한을 관리 합니다.

### <a name="accessing-windows-admin-center-when-azure-ad-authentication-is-enabled"></a>Azure AD 인증을 사용 하는 경우 Windows 관리 센터에 액세스

사용 되는 브라우저에 따라, Azure AD 인증을 사용 하 여 Windows 관리 센터에 액세스 하는 일부 사용자는 **브라우저에서** 추가 프롬프트를 받게 됩니다. 여기에서 컴퓨터에 대 한 windows 계정 자격 증명을 제공 해야 합니다. Windows 관리 센터가 설치 되어 있습니다. 해당 정보를 입력 한 후에는 azure에서 azure AD 응용 프로그램에 대 한 액세스 권한이 부여 된 Azure 계정의 자격 증명이 필요한 추가 Azure Active Directory 인증 프롬프트가 표시 됩니다.

> [!NOTE]
> Windows 계정에는 게이트웨이 컴퓨터에 대 한 **관리자 권한이** 있는 사용자에 게는 Azure AD 인증에 대 한 메시지가 표시 되지 않습니다.

### <a name="configuring-azure-active-directory-authentication-for-windows-admin-center-preview"></a>Windows 관리 센터 미리 보기에 대 한 Azure Active Directory 인증 구성

Windows 관리 센터 **설정** > **액세스** 로 이동 하 고 설정/해제 스위치를 사용 하 여 "Azure Active Directory 사용 하 여 게이트웨이에 보안 계층 추가"를 설정 합니다. Azure에 게이트웨이를 등록 하지 않은 경우 지금이 작업을 수행 하는 방법을 안내 합니다.

기본적으로 Azure AD 테 넌 트의 모든 구성원은 Windows 관리 센터 게이트웨이 서비스에 대 한 사용자 액세스 권한을 보유 합니다. 게이트웨이 컴퓨터의 로컬 관리자만 Windows 관리 센터 게이트웨이에 대 한 관리자 액세스 권한을 보유 합니다. 게이트웨이 컴퓨터에서 로컬 관리자의 권한은 제한할 수 없습니다. 로컬 관리자는 인증에 Azure AD를 사용 하는지 여부에 관계 없이 모든 작업을 수행할 수 있습니다.

특정 Azure AD 사용자 또는 그룹에 Windows 관리 센터 서비스에 대 한 액세스 권한을 부여 하려면 다음을 수행 해야 합니다.

1.  액세스 설정에 제공 된 하이퍼링크를 사용 하 여 Azure Portal의 Windows 관리 센터 Azure AD 응용 프로그램으로 이동 합니다. 참고이 하이퍼링크는 Azure Active Directory 인증을 사용 하는 경우에만 사용할 수 있습니다. 
    -   또한 **Azure Active Directory** > **엔터프라이즈 응용**프로그램  > **모든 응용 프로그램** 을 검색 하 고 **windowsadmincenter** 를 검색 하 여 Azure Portal에서 응용 프로그램을 찾을 수 있습니다. Azure AD 앱은 다음과 같이 이름이 지정 됩니다. WindowsAdminCenter-<gateway name>). 검색 결과를 얻지 못한 경우 **Show** 가 **모든 응용 프로그램**으로 설정 되 고 **응용 프로그램 상태** 가 **any** 로 설정 되 고 적용을 클릭 한 다음 검색을 시도 합니다. 응용 프로그램을 찾았으면 **사용자 및 그룹** 으로 이동 합니다.
2.  속성 탭에서 **사용자 할당 필요** 를 예로 설정 합니다.
    이 작업을 완료 한 후에는 **사용자 및 그룹** 탭에 나열 된 멤버만 Windows 관리 센터 게이트웨이에 액세스할 수 있습니다.
3.  사용자 및 그룹 탭에서 **사용자 추가**를 선택 합니다. 추가 된 각 사용자/그룹에 대해 게이트웨이 사용자 또는 게이트웨이 관리자 역할을 할당 해야 합니다.

Azure AD 인증을 켜면 게이트웨이 서비스가 다시 시작 되 고 브라우저를 새로 고쳐야 합니다. 언제 든 지 Azure Portal에서 SME Azure AD 응용 프로그램에 대 한 사용자 액세스를 업데이트할 수 있습니다.

사용자가 Windows 관리 센터 게이트웨이 URL에 액세스 하려고 할 때 Azure Active Directory id를 사용 하 여 로그인 하 라는 메시지가 표시 됩니다. Windows 관리 센터에 액세스 하려면 사용자도 게이트웨이 서버에서 로컬 사용자의 구성원 이어야 합니다.

사용자와 관리자는 현재 로그인 된 계정을 볼 수 있을 뿐만 아니라 Windows 관리 센터 설정의 **계정** 탭에서이 Azure AD 계정에 대 한 로그 아웃을 볼 수 있습니다.

### <a name="configuring-azure-active-directory-authentication-for-windows-admin-center"></a>Windows 관리 센터에 대 한 Azure Active Directory 인증 구성

[AZURE AD 인증을 설정 하려면 먼저 azure에 게이트웨이를 등록 해야](azure-integration.md) 합니다 (Windows 관리 센터 게이트웨이에 대해이 작업을 한 번만 수행 해야 함). 이 단계에서는 게이트웨이 사용자 및 게이트웨이 관리자 액세스를 관리할 수 있는 Azure AD 응용 프로그램을 만듭니다.

특정 Azure AD 사용자 또는 그룹에 Windows 관리 센터 서비스에 대 한 액세스 권한을 부여 하려면 다음을 수행 해야 합니다.

1.  Azure Portal에서 SME Azure AD 응용 프로그램으로 이동 합니다. 
    -   **액세스 제어 변경** 을 클릭 하 고 Windows 관리 센터 액세스 설정에서 **Azure Active Directory** 를 선택 하는 경우 UI에 제공 된 하이퍼링크를 사용 하 여 Azure Portal에서 Azure AD 응용 프로그램에 액세스할 수 있습니다. 저장을 클릭 하 고 액세스 제어 id 공급자로 Azure AD를 선택한 후에도 액세스 설정에서이 하이퍼링크를 사용할 수 있습니다.
    -   또한 **Azure Active Directory** > **엔터프라이즈 응용**프로그램  > **모든 응용 프로그램** 및 **SME** 검색으로 이동 하 여 Azure Portal에서 응용 프로그램을 찾을 수 있습니다 (Azure AD 앱의 이름은 @no__t SME-6). 검색 결과를 얻지 못한 경우 **Show** 가 **모든 응용 프로그램**으로 설정 되 고 **응용 프로그램 상태** 가 **any** 로 설정 되 고 적용을 클릭 한 다음 검색을 시도 합니다. 응용 프로그램을 찾았으면 **사용자 및 그룹** 으로 이동 합니다.
2.  속성 탭에서 **사용자 할당 필요** 를 예로 설정 합니다.
    이 작업을 완료 한 후에는 **사용자 및 그룹** 탭에 나열 된 멤버만 Windows 관리 센터 게이트웨이에 액세스할 수 있습니다.
3.  사용자 및 그룹 탭에서 **사용자 추가**를 선택 합니다. 추가 된 각 사용자/그룹에 대해 게이트웨이 사용자 또는 게이트웨이 관리자 역할을 할당 해야 합니다.

**액세스 제어 변경** 창에서 Azure AD 액세스 제어를 저장 하면 게이트웨이 서비스가 다시 시작 되 고 브라우저를 새로 고쳐야 합니다. 언제 든 지 Azure Portal에서 Windows 관리 센터 Azure AD 응용 프로그램에 대 한 사용자 액세스를 업데이트할 수 있습니다. 

사용자가 Windows 관리 센터 게이트웨이 URL에 액세스 하려고 할 때 Azure Active Directory id를 사용 하 여 로그인 하 라는 메시지가 표시 됩니다. Windows 관리 센터에 액세스 하려면 사용자도 게이트웨이 서버에서 로컬 사용자의 구성원 이어야 합니다. 

Windows 관리 센터 일반 설정의 **Azure** 탭을 사용 하 여 사용자와 관리자는 현재 로그인 된 계정을 볼 수 있을 뿐 아니라이 azure AD 계정에 대 한 로그 아웃도 볼 수 있습니다.

### <a name="conditional-access-and-multi-factor-authentication"></a>조건부 액세스 및 multi-factor authentication

Azure AD를 추가 보안 계층으로 사용 하 여 Windows 관리 센터 게이트웨이에 대 한 액세스를 제어 하는 이점 중 하나는 조건부 액세스 및 multi-factor authentication과 같은 Azure AD의 강력한 보안 기능을 활용할 수 있다는 것입니다. 

[Azure Active Directory를 사용 하 여 조건부 액세스 구성에 대해 자세히 알아보세요.](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## <a name="configure-single-sign-on"></a>Single Sign-On 구성

**Windows Server에 서비스로 배포 된 경우 Single sign-on**

Windows 10에서 Windows 관리 센터를 설치 하는 경우 Single Sign-On를 사용할 준비가 된 것입니다. 그러나 windows Server에서 Windows 관리 센터를 사용 하려는 경우에는 Single Sign-On를 사용 하기 전에 사용자 환경에서 특정 형태의 Kerberos 위임을 설정 해야 합니다. 위임은 대상 노드에 위임할 수 있도록 신뢰할 수 있는 게이트웨이 컴퓨터를 구성 합니다. 

사용자 환경에서 [리소스 기반 제한 위임을](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview) 구성 하려면 다음 PowerShell cmdlet을 실행 합니다. (이 경우 Windows Server 2012 이상을 실행 하는 도메인 컨트롤러가 필요 합니다.)

```powershell
     $gateway = "WindowsAdminCenterGW" # Machine where Windows Admin Center is installed
     $node = "ManagedNode" # Machine that you want to manage
     $gatewayObject = Get-ADComputer -Identity $gateway
     $nodeObject = Get-ADComputer -Identity $node
     Set-ADComputer -Identity $nodeObject -PrincipalsAllowedToDelegateToAccount $gatewayObject
```

이 예제에서는 Windows 관리 센터 게이트웨이가 서버 **WindowsAdminCenterGW**에 설치 되 고 대상 노드 이름은 **managednode**입니다.

이 관계를 제거 하려면 다음 cmdlet을 실행 합니다.

```powershell
Set-ADComputer -Identity $nodeObject -PrincipalsAllowedToDelegateToAccount $null
```

## <a name="role-based-access-control"></a>역할 기반 액세스 제어

역할 기반 액세스 제어를 사용 하면 전체 로컬 관리자를 만드는 대신 사용자에 게 컴퓨터에 대 한 제한 된 액세스 권한을 제공할 수 있습니다.
[역할 기반 액세스 제어 및 사용 가능한 역할에 대해 자세히 알아보세요.](../plan/user-access-options.md#role-based-access-control)

RBAC를 설정 하는 작업은 대상 컴퓨터에 대 한 지원을 사용 하도록 설정 하 고 사용자를 관련 역할에 할당 하는 두 단계로 구성 됩니다.

> [!TIP]
> 역할 기반 액세스 제어에 대 한 지원을 구성 하는 컴퓨터에 대 한 로컬 관리자 권한이 있는지 확인 합니다.

### <a name="apply-role-based-access-control-to-a-single-machine"></a>단일 컴퓨터에 역할 기반 액세스 제어 적용

단일 컴퓨터 배포 모델은 관리할 컴퓨터가 많지 않은 간단한 환경에 적합 합니다.
역할 기반 액세스 제어를 지 원하는 컴퓨터를 구성 하면 다음과 같이 변경 됩니다.

-   Windows 관리 센터에 필요한 기능을 포함 하는 PowerShell 모듈은 `C:\Program Files\WindowsPowerShell\Modules`에서 시스템 드라이브에 설치 됩니다. 모든 모듈은 **Microsoft. Sme로 시작 합니다.**
-   필요한 상태 구성에서는 **Sme**라는 컴퓨터에서 충분 한 관리 끝점을 구성 하는 일회성 구성을 실행 합니다. 이 끝점은 Windows 관리 센터에서 사용 되는 3 개의 역할을 정의 하 고 사용자가 연결할 때 임시 로컬 관리자로 실행 됩니다.
-   3 새 로컬 그룹이 만들어지고 역할에 대 한 액세스 권한이 할당 된 사용자를 제어 합니다.
    -   Windows 관리 센터 관리자
    -   Windows 관리 센터 Hyper-v 관리자
    -   Windows 관리 센터 독자

단일 컴퓨터에서 역할 기반 액세스 제어를 지원 하도록 설정 하려면 다음 단계를 수행 합니다.

1.  Windows 관리 센터를 열고 대상 컴퓨터에 대 한 로컬 관리자 권한이 있는 계정을 사용 하 여 역할 기반 액세스 제어를 사용 하 여 구성 하려는 컴퓨터에 연결 합니다.
2.  **개요** 도구에서 **설정** > **역할 기반 액세스 제어**를 클릭 합니다.
3.  페이지 아래쪽에서 **적용** 을 클릭 하 여 대상 컴퓨터의 역할 기반 액세스 제어를 지원할 수 있습니다. 응용 프로그램 프로세스에는 PowerShell 스크립트를 복사 하 고 대상 컴퓨터에서 구성 (PowerShell 필요한 상태 구성을 사용 하 여)을 호출 하는 작업이 포함 됩니다. 완료 하는 데 최대 10 분이 걸릴 수 있으며 WinRM이 다시 시작 됩니다. 이렇게 하면 Windows 관리 센터, PowerShell 및 WMI 사용자의 연결이 일시적으로 끊어집니다.
4.  페이지를 새로 고쳐 역할 기반 액세스 제어의 상태를 확인 합니다. 사용할 준비가 되 면 상태가 **적용**됨으로 변경 됩니다.

구성이 적용 되 면 사용자를 역할에 할당할 수 있습니다.

1.  **로컬 사용자 및 그룹** 도구를 열고 **그룹** 탭으로 이동 합니다.
2.  **Windows 관리 센터 구독자** 그룹을 선택 합니다.
3.  아래쪽의 *세부 정보* 창에서 **사용자 추가** 를 클릭 하 고 Windows 관리 센터를 통해 서버에 대 한 읽기 전용 액세스 권한이 있어야 하는 사용자 또는 보안 그룹의 이름을 입력 합니다. 사용자 및 그룹은 로컬 컴퓨터 또는 Active Directory 도메인에서 가져올 수 있습니다.
4.  **Windows 관리 센터 Hyper-v 관리자** 및 **Windows 관리 센터 관리자** 그룹에 대해 2-3 단계를 반복 합니다.

또한 [제한 된 그룹 정책 설정을](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc756802%28v=ws.10%29)사용 하 여 그룹 정책 개체를 구성 하 여 도메인 전체에서 이러한 그룹을 일관 되 게 채울 수 있습니다.

### <a name="apply-role-based-access-control-to-multiple-machines"></a>여러 컴퓨터에 역할 기반 액세스 제어 적용

대기업 배포에서는 Windows 관리 센터 게이트웨이에서 구성 패키지를 다운로드 하 여 기존 자동화 도구를 사용 하 여 역할 기반 액세스 제어 기능을 컴퓨터에 푸시할 수 있습니다.
구성 패키지는 PowerShell 필요한 상태 구성에서 사용 하도록 설계 되었지만 선호 하는 자동화 솔루션을 사용 하도록 조정할 수 있습니다.

#### <a name="download-the-role-based-access-control-configuration"></a>역할 기반 액세스 제어 구성 다운로드

역할 기반 access control 구성 패키지를 다운로드 하려면 Windows 관리 센터 및 PowerShell 프롬프트에 대 한 액세스 권한이 있어야 합니다.

Windows Server의 서비스 모드에서 Windows 관리 센터 게이트웨이를 실행 하는 경우 다음 명령을 사용 하 여 구성 패키지를 다운로드 합니다.
사용자 환경에 맞는 게이트웨이 주소를 사용 하 여 게이트웨이 주소를 업데이트 해야 합니다.

```powershell
$WindowsAdminCenterGateway = 'https://windowsadmincenter.contoso.com'
Invoke-RestMethod -Uri "$WindowsAdminCenterGateway/api/nodes/all/features/jea/endpoint/export" -Method POST -UseDefaultCredentials -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Windows 10 컴퓨터에서 Windows 관리 센터 게이트웨이를 실행 하는 경우 대신 다음 명령을 실행 합니다.

```powershell
$cert = Get-ChildItem Cert:\CurrentUser\My | Where-Object Subject -eq 'CN=Windows Admin Center Client' | Select-Object -First 1
Invoke-RestMethod -Uri "https://localhost:6516/api/nodes/all/features/jea/endpoint/export" -Method POST -Certificate $cert -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Zip 보관 파일을 확장 하면 다음과 같은 폴더 구조가 표시 됩니다.

- InstallJeaFeatures
- JustEnoughAdministration (디렉터리)
- 모듈 (디렉터리)
    - SME \* (디렉터리)
    - WindowsAdminCenter. Jea (디렉터리)

노드에 대 한 역할 기반 액세스 제어 지원을 구성 하려면 다음 작업을 수행 해야 합니다.

1.  JustEnoughAdministration, @no__t SME 및 WindowsAdminCenter. Jea 모듈을 대상 컴퓨터의 PowerShell 모듈 디렉터리에 복사 합니다. 일반적으로이는 `C:\Program Files\WindowsPowerShell\Modules`에 있습니다.
2.  **InstallJeaFeature** 파일을 업데이트 하 여 RBAC 끝점의 원하는 구성과 일치 시킵니다.
3.  InstallJeaFeature를 실행 하 여 DSC 리소스를 컴파일합니다.
4.  모든 컴퓨터에 DSC 구성을 배포 하 여 구성을 적용 합니다.

다음 섹션에서는 PowerShell 원격을 사용 하 여이 작업을 수행 하는 방법을 설명 합니다.

#### <a name="deploy-on-multiple-machines"></a>여러 컴퓨터에 배포

여러 컴퓨터에 다운로드 한 구성을 배포 하려면 사용자 환경에 적절 한 보안 그룹을 포함 하도록 InstallJeaFeatures 스크립트를 업데이트 하 고, 각 컴퓨터에 파일을 복사 하 고,를 호출 합니다 **.** 구성 스크립트.
선호 하는 자동화 도구를 사용 하 여이를 수행할 수 있지만이 문서에서는 순수한 PowerShell 기반 접근 방식에 중점을 둡니다.

기본적으로 구성 스크립트는 컴퓨터에 각 역할에 대 한 액세스를 제어 하는 로컬 보안 그룹을 만듭니다.
이는 작업 그룹 및 도메인에 가입 된 컴퓨터에 적합 하지만 도메인 전용 환경에서 배포 하는 경우 도메인 보안 그룹을 각 역할과 직접 연결 하는 것이 좋습니다.
도메인 보안 그룹을 사용 하도록 구성을 업데이트 하려면 **InstallJeaFeatures** 을 열고 다음과 같이 변경 합니다.

1.  파일에서 3 개의 **그룹** 리소스를 제거 합니다.
    1.  "그룹-독자-그룹"
    2.  "그룹-Hyper-v-관리자-그룹"
    3.  "그룹-관리자-그룹"
2.  JeaEndpoint **DependsOn** 속성에서 3 그룹 리소스를 제거 합니다.
    1.  "[Group] MS Readers-Group"
    2.  "[그룹] MS-hyper-v-관리자-그룹"
    3.  "[Group] MS-Administrators-Group"
3.  JeaEndpoint **Roledefinitions** 속성의 그룹 이름을 원하는 보안 그룹으로 변경 합니다. 예를 들어 Windows 관리 센터 관리자 역할에 대 한 액세스 권한을 할당 해야 하는 보안 그룹 *CONTOSO\MyTrustedAdmins* 있는 경우 `'$env:COMPUTERNAME\Windows Admin Center Administrators'`을 `'CONTOSO\MyTrustedAdmins'`로 변경 합니다. 업데이트 해야 하는 세 가지 문자열은 다음과 같습니다.
    1.  ' $env: COMPUTERNAME\Windows 관리 센터 관리자 '
    2.  ' $env: COMPUTERNAME\Windows 관리 센터 Hyper-v 관리자 '
    3.  ' $env: COMPUTERNAME\Windows 관리 센터 독자 '

> [!NOTE]
> 각 역할에 고유한 보안 그룹을 사용 해야 합니다. 동일한 보안 그룹을 여러 역할에 할당 하면 구성이 실패 합니다.

그런 다음 **InstallJeaFeatures** 파일의 끝에 다음 PowerShell 줄을 스크립트의 맨 아래에 추가 합니다.

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

마지막으로, 모듈, DSC 리소스 및 구성이 포함 된 폴더를 각 대상 노드에 복사 하 고 **InstallJeaFeature** 스크립트를 실행할 수 있습니다.
관리자 워크스테이션에서 원격으로이 작업을 수행 하려면 다음 명령을 실행할 수 있습니다.

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
