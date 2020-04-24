---
title: Windows Admin Center를 사용하는 사용자 액세스 옵션
description: Windows Admin Center(Project Honolulu)를 사용하는 사용자 액세스 옵션 및 ID 공급자
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 084cdae0bf8ca0eb3aff1f4679d30978b860efef
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "71356922"
---
# <a name="user-access-options-with-windows-admin-center"></a>Windows Admin Center를 사용하는 사용자 액세스 옵션

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Server에서 배포하는 경우 Windows Admin Center는 서버 환경을 위한 중앙 집중식 관리 지점을 제공합니다. Windows Admin Center에 대한 액세스를 제어하면 관리 환경에서의 보안을 강화할 수 있습니다.

## <a name="gateway-access-roles"></a>게이트웨이 액세스 역할

Windows Admin Center는 게이트웨이 서비스에 액세스하기 위해 게이트웨이 사용자 및 게이트웨이 관리자라는 두 가지 역할을 정의합니다.

> [!NOTE]
> 게이트웨이에 대한 액세스는 게이트웨이에서 볼 수 있는 관리 서버에 대한 액세스를 암시하지 않습니다. 대상 서버를 관리하려면 사용자는 대상 서버에 대한 관리 권한이 있는 자격 증명을 사용하여 연결해야 합니다.

**게이트웨이 사용자**는 해당 게이트웨이를 통해 서버를 관리하도록 Windows Admin Center 게이트웨이 서비스에 연결할 수 있지만, 액세스 권한 또는 게이트웨이에 인증하는 데 사용되는 인증 메커니즘은 변경할 수 없습니다.

**게이트웨이 관리자**는 액세스 권한을 부여받을 수 있는 사용자와 해당 사용자가 게이트웨이를 인증하는 방법을 구성할 수 있습니다.

>[!NOTE]
> Windows Admin Center에 정의된 액세스 그룹이 없는 경우 역할에는 게이트웨이 서버에 대 한 Windows 계정 액세스가 반영됩니다. 

[Windows Admin Center에서 게이트웨이 사용자 및 관리자 액세스를 구성합니다.](../configure/user-access-control.md)

## <a name="identity-provider-options"></a>ID 공급자 옵션

게이트웨이 관리자는 다음 중 하나를 선택할 수 있습니다.

 - [Active Directory/로컬 머신 그룹](../configure/user-access-control.md#active-directory-or-local-machine-groups)
 - [Windows Admin Center에서 ID 공급자로의 Azure Active Directory](../configure/user-access-control.md#azure-active-directory)


### <a name="smartcard-authentication"></a>스마트 카드 인증

Active Directory 또는 로컬 머신 그룹을 ID 공급자로 사용하는 경우 Windows Admin Center에 액세스하는 사용자에게 추가 스마트 카드 기반 보안 그룹의 구성원이 되도록 요구하면 스마트 카드 인증을 적용할 수 있습니다. [Windows Admin Center에서 스마트 카드 인증을 구성합니다.](../configure/user-access-control.md#active-directory-or-local-machine-groups)

### <a name="conditional-access-and-multi-factor-authentication"></a>조건부 액세스 및 다단계 인증

게이트웨이에 대한 Azure AD 인증을 요구하면 Azure AD에서 제공하는 조건부 액세스 및 다단계 인증과 같은 추가 보안 기능을 활용할 수 있습니다. [Azure Active Directory를 사용하여 조건부 액세스를 구성하는 방법에 대해 자세히 알아보세요.](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## <a name="role-based-access-control"></a>역할 기반 액세스 제어

기본적으로 사용자는 Windows Admin Center를 사용하여 관리하려는 머신에 대해 전체 로컬 관리자 권한이 있어야 합니다.
그러면 머신에 원격으로 연결할 수 있으며, 시스템 설정을 보고 수정할 수 있는 충분한 권한이 있는지 확인할 수 있습니다.
그러나 일부 사용자는 작업을 수행하는 데 머신에 대한 무제한 액세스가 필요하지 않을 수 있습니다.
Windows Admin Center에서 **역할 기반 액세스 제어**를 사용하여 전체 로컬 관리자 권한 대신 머신에 대한 제한적인 액세스 권한을 사용자에게 제공할 수 있습니다.

Windows Admin Center의 역할 기반 액세스 제어는 PowerShell [Just Enough Administration](https://aka.ms/jeadocs) 엔드포인트를 사용하여 각 관리형 서버를 구성하여 작동됩니다.
이 엔드포인트는 각 역할이 관리할 수 있는 시스템의 측면과 역할에 할당된 사용자를 비롯한 역할을 정의합니다.
사용자가 제한된 엔드포인트에 연결하면 임시 로컬 관리자 계정이 생성되어 시스템을 대신 관리합니다.
그러면 자체 위임 모델이 없는 도구도 Windows Admin Center에서 계속 관리할 수 있습니다.
사용자가 Windows Admin Center를 통한 머신 관리를 중지하면 임시 계정이 자동으로 제거됩니다.

사용자가 역할 기반 액세스 제어를 사용하여 구성된 머신에 연결하는 경우 Windows Admin Center는 먼저 사용자가 로컬 관리자인지 확인합니다.
해당하는 경우 제한이 없는 전체 Windows Admin Center 환경을 사용할 수 있습니다.
그렇지 않은 경우 Windows Admin Center는 사용자가 미리 정의된 역할에 속하는지 여부를 확인합니다.
사용자가 Windows Admin Center 역할에 속하지만 전체 관리자가 아닌 경우에는 *제한적인 액세스*가 부여됩니다.
마지막으로, 사용자가 관리자 또는 역할의 구성원이 아닌 경우 머신을 관리하기 위한 액세스가 거부됩니다.

역할 기반 액세스 제어는 서버 관리자 및 장애 조치(Failover) 클러스터 솔루션에 사용할 수 있습니다.

### <a name="available-roles"></a>사용 가능한 역할

Windows Admin Center는 다음과 같은 최종 사용자 역할을 지원합니다.

역할 이름 | 올바른 사용법
----------|-------------
Administrators | 사용자에게 원격 데스크톱 또는 PowerShell에 대한 액세스 권한을 부여하지 않고도 Windows Admin Center에서 대부분의 기능을 사용할 수 있도록 허용합니다. 이 역할은 머신에서 관리 진입점을 제한하려는 “점프 서버” 시나리오에 적합합니다.
Readers | 사용자가 서버에서 정보 및 설정을 볼 수 있지만 변경할 수는 없습니다.
Hyper-V 관리자 | 사용자가 Hyper-V 가상 머신 및 스위치를 변경할 수 있지만 다른 기능은 읽기 전용 액세스로 제한할 수 있습니다.

사용자가 제한된 액세스로 연결하는 경우 다음과 같은 기본 제공 확장 기능이 제한됩니다.

- 파일(파일 업로드 또는 다운로드 없음)
- PowerShell(사용할 수 없음)
- 원격 데스크톱(사용할 수 없음)
- 스토리지 복제본(사용할 수 없음)

지금은 조직에 대한 사용자 지정 역할을 만들 수 없지만 각 역할에 대한 액세스 권한이 부여된 사용자를 선택할 수 있습니다.

### <a name="preparing-for-role-based-access-control"></a>역할 기반 액세스 제어 준비

임시 로컬 계정을 활용하려면 Windows Admin Center에서 역할 기반 액세스 제어를 지원하도록 각 대상 머신을 구성해야 합니다.
구성 프로세스에는 Desired State Configuration을 사용하여 머신에 PowerShell 스크립트와 Just Enough Administration 엔드포인트를 설치하는 작업이 포함됩니다.

컴퓨터 수가 많지 않은 경우에는 Windows Admin Center의 역할 기반 액세스 제어 페이지를 사용하여 각 컴퓨터에 개별적으로 구성을 적용할 수 있습니다.
개별 컴퓨터에서 역할 기반 액세스 제어를 설정하면 각 역할에 대한 액세스를 제어하는 로컬 보안 그룹이 만들어집니다.
사용자 또는 다른 보안 그룹을 역할 보안 그룹의 구성원으로 추가하여 액세스 권한을 부여할 수 있습니다.

여러 머신에 대한 엔터프라이즈급 배포의 경우 게이트웨이에서 구성 스크립트를 다운로드하고 Desired State Configuration 끌어오기 서버, Azure Automation 또는 선호하는 관리 도구를 사용하여 컴퓨터에 배포할 수 있습니다.
