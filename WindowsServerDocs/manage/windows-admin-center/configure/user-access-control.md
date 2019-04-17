---
title: 사용자 액세스 제어 및 사용 권한 구성
description: 사용자 액세스 제어 및 Active Directory 또는 Azure AD (Project Honolulu)를 사용 하 여 권한을 구성 하는 방법을 알아봅니다
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/19/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: b19657f4ce1a1a2cfb94f7234f07805ba0abd42c
ms.sourcegitcommit: 4961576f2891600ef9a760ca7df650d14332e057
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/09/2019
ms.locfileid: "9152048"
---
# 사용자 액세스 제어 및 사용 권한 구성

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

않은 경우 숙지 [Windows 관리 센터에서 사용자 액세스 제어 옵션](../plan/user-access-options.md)

>[!NOTE]
> 작업 그룹 환경에서 또는 신뢰할 수 없는 도메인 기반 그룹 액세스 Windows 관리 센터에서 지원 되지 않습니다.

## 게이트웨이 액세스 역할 정의

Windows Admin Center 게이트웨이 서비스에 액세스 하기 위한 두 가지 역할을 가지 있습니다.

**게이트웨이 사용자가** 해당 게이트웨이 통해 서버를 관리 하는 Windows Admin Center 게이트웨이 서비스에 연결할 수 있지만 액세스 권한 및 게이트웨이 인증에 사용 되는 인증 메커니즘은 변경할 수 없습니다.

**게이트웨이 관리자** 액세스 권한도 누가 사용자가 게이트웨이 인증 방법을 구성할 수 있습니다. 게이트웨이 관리자만 보고 Windows Admin Center에서 액세스 설정을 구성할 수 있습니다. 게이트웨이 컴퓨터에서 로컬 관리자는 Windows Admin Center 게이트웨이 서비스의 관리자가 항상입니다.

> [!NOTE]
> 게이트웨이에 대 한 액세스 게이트웨이 하 여 표시 관리 되는 서버에 대 한 액세스를 의미 하지 않습니다. 대상 서버를 관리 하려면 연결 하는 사용자 (또는 해당 통해 전달 된 Windows 자격 증명을 통해 **으로 관리** 작업을 사용 하 여 Windows Admin Center 세션에 제공 된 자격 증명을 통해) 하는 자격 증명 관리 권한이 사용 해야 합니다. 해당 대상 서버.

## Active Directory 또는 로컬 컴퓨터 그룹

기본적으로 Active Directory 또는 로컬 컴퓨터 그룹 게이트웨이 액세스 제어 사용 됩니다. 게이트웨이 사용자 및 관리자를 관리할 수 Active Directory 도메인에 있는 경우 Windows Admin Center 인터페이스 내에서 액세스 합니다.

**사용자가** 탭에서 Windows Admin Center 게이트웨이 사용자로 액세스할 수 있는 사용자를 제어할 수 있습니다. 기본적으로 고 보안 그룹을 지정 하지 않으면 게이트웨이 URL에 액세스 하는 모든 사용자에 액세스 합니다. 사용자가 목록에 하나 이상의 보안 그룹을 추가 하 고 나면 액세스는 해당 그룹의 구성원으로 제한 됩니다.

액세스에 의해 제어 됩니다 환경에서 Active Directory 도메인을 사용 하지 않을 경우는 ```Users``` 및 ```Administrators``` Windows Admin Center 게이트웨이 컴퓨터에서 로컬 그룹.

### 스마트 카드 인증

스마트 카드 기반 보안 그룹에 대 한 추가 _필수_ 그룹을 지정 하 여 **스마트 카드 인증** 을 적용할 수 있습니다. 스마트 카드 기반 보안 그룹을 추가 하 고 나면 모든 보안 그룹의 구성원 및 스마트 카드 그룹의 사용자 목록에 포함 된 경우 사용자가 Windows Admin Center 서비스에 액세스할만 수 있습니다.

**관리자** 탭에서 Windows Admin Center 게이트웨이 관리자 권한으로 액세스할 수 있는 사용자를 제어할 수 있습니다. 컴퓨터에서 로컬 관리자 그룹은 항상 전체 관리자 액세스 하 고 목록에서 제거할 수 없습니다. 보안 그룹을 추가 하 여 Windows Admin Center 게이트웨이 설정을 변경 하려면 해당 그룹 권한의 구성원을 제공 합니다. 관리자가 목록 같은 방식으로 사용자가 목록에서 스마트 카드 인증을 지원: 보안 그룹 및 스마트 카드 그룹에 대 한 AND 조건과 합니다.

## Azure Active Directory

조직에서 Azure Active Directory (Azure AD)을 사용 하는 경우 Windows Admin Center에 **추가** 보안 계층도 게이트웨이 액세스 하려면 Azure AD 인증을 요구 하 여 추가할 선택할 수 있습니다. Windows Admin Center에 액세스 하려면 사용자의 **Windows 계정** 도 있어야 게이트웨이 서버에 대 한 액세스 (경우에 Azure AD 인증을 사용). Azure 포털에서 아니라 내에서 Windows Admin Center 사용자 및 관리자 액세스 권한을 관리 합니다 Azure AD를 사용 하면 Windows Admin Center UI 합니다.

### Azure AD 인증을 사용 하는 경우 Windows Admin Center에 액세스

일부 사용자를 Azure AD 인증 구성 된 Windows Admin Center에 대 한 액세스는 추가 프롬프트 받을 **브라우저에서** 자신의 Windows 제공 되어야 하는 컴퓨터에 대 한 자격 증명 계정에 사용 되는 브라우저를 따라 Windows Admin Center 설치 됩니다. 해당 정보를 입력 한 후 사용자는 Azure에서 Azure AD 응용 프로그램에 대 한 액세스 권한이 부여 된 Azure 계정 자격 증명이 필요 하면 추가 Azure Active Directory 인증 메시지를 받게 됩니다.

> [!NOTE]
> 사용자가 사용자의 Windows 계정에 **대 한 관리자 권한** 을 게이트웨이 컴퓨터 는 Azure AD 인증에 대 한 메시지가 표시 되지 않습니다.

### Windows Admin Center 미리 보기에 대 한 Azure Active Directory 인증 구성

Windows Admin Center **설정**으로 이동 > **액세스** 및 켜려면 토글 스위치를 사용 하 여 "사용 하 여 Azure Active Directory 보안 계층 게이트웨이를 추가 하려면". 게이트웨이를 Azure 등록 하지 않은 경우이 시간에 작업을 안내 합니다.

기본적으로 Azure AD 테 넌 트의 모든 구성원에 Windows Admin Center 게이트웨이 서비스에 대 한 사용자 액세스 합니다. 게이트웨이 컴퓨터에서 로컬 관리자만 Windows Admin Center 게이트웨이에 관리자 권한이 있습니다. Note 게이트웨이 컴퓨터에서 로컬 관리자의 권한을 제한 될 수 없습니다-로컬 관리자는 Azure AD 인증을 위해 사용 여부에 상관 없이 아무 작업도 수행할 수 있습니다.

제공 특정 Azure AD 사용자 또는 그룹 게이트웨이 사용자나 게이트웨이 Windows Admin Center 서비스에 대 한 관리자 액세스 하려는 경우 다음을 수행 해야 합니다.

1.  액세스 설정에 있는 하이퍼링크를 사용 하 여 Azure portal에서 Windows Admin Center Azure AD 응용 프로그램으로 이동 합니다. Note Azure Active Directory 인증을 사용 하는 경우이 하이퍼링크는 에서만 사용할 수 있습니다. 
    -   또한 응용 프로그램 Azure portal에서 **Azure Active Directory**로 이동 하 여 찾을 수 있습니다 > **엔터프라이즈 응용 프로그램** > **모든 응용 프로그램** 및 검색 **WindowsAdminCenter** (Azure AD 응용 프로그램 이름은 WindowsAdminCenter-<gateway name>). 모든 검색 결과 얻을 하 고, **표시** 는 **모든 응용 프로그램**으로 설정, **응용 프로그램 상태** 를 **모두** 설정 되어 있는지 확인 하 고, 적용을 클릭 하지, 검색을 하십시오. 응용 프로그램에 도달 하면, **사용자 및 그룹으로** 이동
2.  속성 탭에서 **사용자 할당 필요한** 예로 설정 합니다.
    이 작업을 마쳤으면 되 면 **사용자 및 그룹** 탭에 나열 된 구성원만 Windows Admin Center 게이트웨이 액세스할 수 없게 됩니다.
3.  사용자 및 그룹 탭에서 **사용자 추가**선택 합니다. 게이트웨이 사용자 또는 게이트웨이 추가 된 각 사용자/그룹에 대 한 관리자 역할을 할당 해야 합니다.

Azure AD 인증을 설정한 후 게이트웨이 서비스를 다시 시작 하 고 브라우저를 복구 해야 합니다. 언제 든 지 Azure portal에서 SME Azure AD 응용 프로그램에 대 한 사용자 액세스를 업데이트할 수 있습니다.

Windows Admin Center 게이트웨이 URL에 액세스 하려고 할 때 자신의 Azure Active Directory id를 사용 하 여 로그인 사용자에 게 표시 됩니다. 사용자가 Windows Admin Center에 액세스 하려면 게이트웨이 서버에 로컬 사용자의 구성원도 되도록 해야 합니다.

사용자 및 관리자가 현재 로그인 계정을 볼 수 있고도으로 로그 아웃의 경우이 Azure AD 계정 windows **계정** 탭에서 관리 센터 설정 됩니다.

### Windows Admin Center에 대 한 Azure Active Directory 인증 구성

[Azure AD 인증을 설정 하려면 먼저 Azure와 게이트웨이 등록 해야](azure-integration.md) (만 해야 하는 것이 Windows Admin Center 게이트웨이에 대 한). 이 단계에서는 게이트웨이 사용자 및 관리자 액세스 권한이 게이트웨이 관리할 수 있는 Azure AD 응용 프로그램을 만듭니다.

제공 특정 Azure AD 사용자 또는 그룹 게이트웨이 사용자나 게이트웨이 Windows Admin Center 서비스에 대 한 관리자 액세스 하려는 경우 다음을 수행 해야 합니다.

1.  Azure portal에서 SME Azure AD 응용 프로그램으로 이동 합니다. 
    -   **변경 액세스 제어** 를 클릭 하 고 **Azure Active Directory** Windows 관리 센터 액세스 설정에서 선택한 Azure portal에서 Azure AD 응용 프로그램에 액세스 하려면 UI에 있는 하이퍼링크를 사용할 수 있습니다. 저장을 클릭 하 고 Azure AD 액세스 제어 id 공급자로 선택한 후에이 하이퍼링크 액세스 설정에서 제공 됩니다.
    -   또한 응용 프로그램 Azure portal에서 **Azure Active Directory**로 이동 하 여 찾을 수 있습니다 > **엔터프라이즈 응용 프로그램** > **모든 응용 프로그램** 및 검색 **SME** (Azure AD 응용 프로그램의 이름은 SME-<gateway>). 모든 검색 결과 얻을 하 고, **표시** 는 **모든 응용 프로그램**으로 설정, **응용 프로그램 상태** 를 **모두** 설정 되어 있는지 확인 하 고, 적용을 클릭 하지, 검색을 하십시오. 응용 프로그램에 도달 하면, **사용자 및 그룹으로** 이동
2.  속성 탭에서 **사용자 할당 필요한** 예로 설정 합니다.
    이 작업을 마쳤으면 되 면 **사용자 및 그룹** 탭에 나열 된 구성원만 Windows Admin Center 게이트웨이 액세스할 수 없게 됩니다.
3.  사용자 및 그룹 탭에서 **사용자 추가**선택 합니다. 게이트웨이 사용자 또는 게이트웨이 추가 된 각 사용자/그룹에 대 한 관리자 역할을 할당 해야 합니다.

Azure AD 액세스 제어를 저장 하면 **변경 액세스 제어** 창에서 게이트웨이 서비스를 다시 시작 하 고 새로 고쳐야 브라우저. 언제 든 지 Azure portal에서 Windows Admin Center Azure AD 응용 프로그램에 대 한 사용자 액세스를 업데이트할 수 있습니다. 

Windows Admin Center 게이트웨이 URL에 액세스 하려고 할 때 자신의 Azure Active Directory id를 사용 하 여 로그인 사용자에 게 표시 됩니다. 사용자가 Windows Admin Center에 액세스 하려면 게이트웨이 서버에 로컬 사용자의 구성원도 되도록 해야 합니다. 

Windows Admin Center 일반 설정의 **Azure** 탭에서는 사용자와 관리자가 볼 수은 현재 로그인 계정을이 Azure AD 계정 로그 아웃 합니다.

### 조건부 액세스 및 다단계 인증

추가 보안 계층으로 Azure AD를 사용 하 여 Windows Admin Center 게이트웨이에 대 한 액세스를 제어 하는 이점 중 하나는 다단계 인증 조건부 액세스 등의 Azure AD의 강력한 보안 기능을 사용할 수 있습니다. 

[Azure Active directory 조건부 액세스 구성에 대해 알아봅니다.](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## 대 한 single sign-on 구성

**대 한 single sign-on 배포 하는 Windows Server에서 서비스 하는 경우**

Windows 10에서 Windows Admin Center를 설치한 경우에 대 한 single sign-on 사용할 준비가 되었습니다. 하지만 Windows Server에서 Windows Admin Center를 사용 하려는 경우 대 한 single sign-on 사용 하려면 먼저 일종의 환경에서 Kerberos 위임 설정 해야 합니다. 위임 하는 대상 노드에 위임 시 신뢰할 수 있는으로 게이트웨이 컴퓨터를 구성 합니다. 

사용자 환경에서 [리소스 기반 제한 위임](http://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-1) 구성 하려면 다음 PowerShell cmdlet을 실행 합니다. (이 Windows Server 2012를 실행 하는 도메인 컨트롤러를 위해서는 인식 이상 이어야 합니다.)

```powershell
     $gateway = "WindowsAdminCenterGW" # Machine where Windows Admin Center is installed
     $node = "ManagedNode" # Machine that you want to manage
     $gatewayObject = Get-ADComputer -Identity $gateway
     $nodeObject = Get-ADComputer -Identity $node
     Set-ADComputer -Identity $nodeObject -PrincipalsAllowedToDelegateToAccount $gatewayObject
```

이 예제에서는 Windows Admin Center 게이트웨이 **WindowsAdminCenterGW**서버에 설치 되 고 대상 노드 이름은 **ManagedNode**.

이러한 관계를 제거 하려면 다음 cmdlet을 실행 합니다.

```powershell
Set-ADComputer -Identity $nodeObject -PrincipalsAllowedToDelegateToAccount $null
```

## 역할 기반 액세스 제어

역할 기반 액세스 제어를 사용 하거나 전체 로컬 관리자를 만드는 대신 컴퓨터에 대 한 액세스가 제한 된 사용자를 제공할 수 있습니다.
[역할 기반 액세스 제어 및 사용 가능한 역할에 대해 자세히.](../plan/user-access-options.md#role-based-access-control)

2 단계 RBAC 설정 구성: 대상 컴퓨터에서 지원을 활성화와 관련 된 역할에 사용자 지정 합니다.

> [!TIP]
> 컴퓨터에 대 한 로컬 관리자 권한이 있는지 역할 기반 액세스 제어에 대 한 지원을 구성 한다고 확인 합니다.

### 단일 컴퓨터에 적용 하는 역할 기반 액세스 제어

단일 컴퓨터 배포 모델은 몇 대의 컴퓨터만 관리할 수 있는 간단한 환경에 적합 합니다.
역할 기반 액세스 제어에 대 한 지원을 사용 하 여 컴퓨터를 구성 다음과 같이 변경 될 수 있습니다.
-   아래에서 Windows Admin Center 필요한 기능을 사용 하 여 PowerShell 모듈은 시스템 드라이브에 설치 됩니다 `C:\Program Files\WindowsPowerShell\Modules`. 모든 모듈 **Microsoft.Sme** 부터 시작
-   원하는 상태 구성을 **Microsoft.Sme.PowerShell**라는 컴퓨터에서 Just Enough Administration 끝점을 구성 하는 한 번만 구성을 실행 됩니다. 이 끝점 Windows Admin Center에서 사용 되는 3 가지 역할을 정의 하며 사용자가 연결 하 여 임시 로컬 관리자 권한으로 실행 됩니다.
-   3 개의 새 로컬 그룹 있는 사용자는 어떤 역할에 할당 된 액세스 제어에 생성 됩니다.
    -   Windows Admin Center 관리자
    -   Windows Admin Center Hyper-v 관리자
    -   Windows Admin Center 판독기

단일 컴퓨터에서 역할 기반 액세스 제어에 대 한 지원을 사용 하려면 다음이 단계를 따르세요.

1.  Windows Admin Center를 열고 대상 컴퓨터에서 로컬 관리자 권한이 있는 계정을 사용 하 여 역할 기반 액세스 제어를 사용 하 여 구성 하려는 컴퓨터에 연결 합니다.
2.  **개요** 도구에서 **설정**을 클릭 > **역할 기반 액세스 제어**합니다.
3.  대상 컴퓨터에서 역할 기반 액세스 제어에 대 한 지원을 사용 하도록 설정 페이지의 맨 아래에 **적용** 을 클릭 합니다. 응용 프로그램 프로세스의 대상 컴퓨터에서 PowerShell 스크립트를 복사 하 고 구성 (PowerShell 필요한 상태 구성 사용)를 호출 해야 합니다. 완료 하는 데 최대 10 분이 걸릴 수 있습니다 WinRM을 다시 시작 됩니다. 이 Windows 관리 센터, PowerShell 및 WMI 사용자 일시적으로 끊어집니다.
4.  역할 기반 액세스 제어의 상태를 확인 하는 페이지를 새로 고칩니다. 사용할 준비가 되었을 때 **적용**상태 변경 됩니다.

구성이 적용 되 고 나면 사용자 역할을 할당할 수 있습니다.

1.  **로컬 사용자 및 그룹** 도구를 열고 **그룹** 탭으로 이동 합니다.
2.  **Windows Admin Center 판독기** 그룹을 선택 합니다.
3.  맨 아래에 *세부 정보* 창에서 **사용자 추가** 클릭 하 고 Windows Admin Center를 통해 서버에 대 한 읽기 전용 액세스 해야 하는 사용자 또는 보안 그룹의 이름을 입력 합니다. 사용자와 그룹은 로컬 컴퓨터 또는 Active Directory 도메인에서 가져올 수 있습니다.
4.  **Windows Admin Center에서 Hyper-v 관리자** 와 **Windows 관리 센터 관리자** 그룹에 대해 2-3 단계를 반복 합니다.

또한 채울 수 이러한 그룹 일관 되 게 도메인에서 [제한 된 그룹 정책 설정을](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc756802%28v=ws.10%29)사용 하 여 그룹 정책 개체를 구성 하 여 합니다.

### 역할 기반 액세스 제어 여러 컴퓨터에 적용

대기업 배포에서는 Windows Admin Center 게이트웨이에서 구성 패키지를 다운로드 하 여 역할 기반 액세스 제어 기능으로 컴퓨터를 푸시하기 위해 기존 자동화 도구를 사용할 수 있습니다.
구성 패키지는 PowerShell 필요한 상태 구성에 사용할 설계 되었지만 기본 자동화 솔루션에 맞게 조정할 수 있습니다.

#### 역할 기반 액세스 제어 구성 다운로드

역할 기반 액세스 제어 구성 패키지를 다운로드 하려면 Windows Admin Center 및 PowerShell 프롬프트에 액세스 해야 합니다.

Windows Server에서 Windows Admin Center 게이트웨이 서비스 모드에서 실행 중인, 다음 명령을 사용 하 여 구성 패키지를 다운로드 합니다.
환경에 가장 적합로 게이트웨이 주소를 업데이트 해야 합니다.

```powershell
$WindowsAdminCenterGateway = 'https://windowsadmincenter.contoso.com'
Invoke-RestMethod -Uri "$WindowsAdminCenterGateway/api/nodes/all/features/jea/endpoint/export" -Method POST -UseDefaultCredentials -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Windows 10 컴퓨터에서 Windows Admin Center 게이트웨이 실행 중인 경우 대신 다음 명령을 실행 합니다.

```powershell
$cert = Get-ChildItem Cert:\CurrentUser\My | Where-Object Subject -eq 'CN=Windows Admin Center Client' | Select-Object -First 1
Invoke-RestMethod -Uri "https://localhost:6516/api/nodes/all/features/jea/endpoint/export" -Method POST -Certificate $cert -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Zip 보관 파일을 확장 하 고 다음 폴더 구조를 표시 됩니다.
- InstallJeaFeatures.ps1
- JustEnoughAdministration (디렉터리)
- 모듈 (디렉터리)
    - Microsoft.SME.\* (디렉터리)
    - WindowsAdminCenter.Jea (디렉터리)

노드에 역할 기반 액세스 제어에 대 한 지원을 구성 하려면 다음 작업을 수행 해야 합니다.
1.  대상 컴퓨터에서 PowerShell 모듈 디렉터리에 JustEnoughAdministration, Microsoft.SME.\*, 및 WindowsAdminCenter.Jea 모듈을 복사 합니다. 이 위치는 일반적으로 `C:\Program Files\WindowsPowerShell\Modules`.
2.  RBAC 끝점에 대 한 원하는 구성과 일치 하도록 **InstallJeaFeature.ps1** 파일을 업데이트 합니다.
3.  DSC 리소스를 컴파일하는 데 InstallJeaFeature.ps1를 실행 합니다.
4.  구성을 적용 하려면 컴퓨터의 모든 DSC 구성을 배포 합니다.

다음 섹션에는 PowerShell 원격 기능을 사용 하는 방법을 설명 합니다.

#### 여러 대의 컴퓨터에 배포

여러 대의 컴퓨터에 다운로드 구성을 배포 하려면 사용자 환경에 대 한 적절 한 보안 그룹을 포함 하도록 **InstallJeaFeatures.ps1** 스크립트를 업데이트 하려면 파일을 각 컴퓨터에 복사 합니다 고 해야 함수를 호출 합니다 구성 스크립트입니다.
이 문서에서는 순수 PowerShell 기반 방법을 중점적 되지만이 수행 하 기본 자동화 도구를 사용할 수 있습니다.

기본적으로 구성 스크립트는 각 역할에 대 한 액세스를 제어 하는 컴퓨터에서 로컬 보안 그룹을 만듭니다.
이 작업 그룹에 적합 하 고 도메인 가입 컴퓨터, 하지만 직접 하고자 할 수도 도메인 전용 환경에서 배포 하는 경우 각 역할을 사용 하 여 도메인 보안 그룹에 연결 합니다.
도메인 보안 그룹을 사용 하 여 구성을 업데이트 하려면 **InstallJeaFeatures.ps1** 열고 다음과 같이 변경 합니다.

1.  3 **그룹** 리소스 파일에서 제거 합니다.
    1.  "그룹 MS 판독기 그룹"
    2.  "그룹 MS-하이퍼-V--" 관리자 그룹
    3.  "그룹 MS-관리자가 그룹"
2.  3 그룹 리소스 JeaEndpoint **DependsOn** 속성에서 제거
    1.  "[그룹] MS-판독기-그룹"
    2.  "[그룹] MS-하이퍼-V-관리자-그룹"
    3.  "[그룹] MS-관리자-그룹"
3.  원하는 보안 그룹을 JeaEndpoint **RoleDefinitions** 속성에서 그룹 이름을 변경 합니다. 예를 들어 Windows Admin Center 관리자 역할에 대 한 액세스를 할당 해야 하는 *CONTOSO\MyTrustedAdmins* 보안 그룹을 갖고 변경 `'$env:COMPUTERNAME\Windows Admin Center Administrators'` 를 `'CONTOSO\MyTrustedAdmins'`합니다. 업데이트 해야 하는 세 가지 문자열 다음과 같습니다.
    1.  ' $env: COMPUTERNAME\Windows 관리자 센터 관리자
    2.  ' $env: COMPUTERNAME\Windows Admin Center에서 Hyper-v 관리자
    3.  ' $env: COMPUTERNAME\Windows 관리자 센터 읽는 사람의

> [!NOTE]
> 각 역할에 대 한 고유 보안 그룹을 사용 해야 합니다. 동일한 보안 그룹은 여러 역할 할당 구성 하면 실패 합니다.

다음으로 **InstallJeaFeatures.ps1** 파일의 끝 스크립트 맨 아래에 PowerShell의 다음 줄을 추가 합니다.

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

마지막으로, DSC 리소스 및 각 대상 노드에 구성 모듈을 포함 하는 폴더를 복사 하 고 **InstallJeaFeature.ps1** 스크립트를 실행할 수 있습니다.
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
