---
title: Windows 관리 센터를 사용 하는 사용자 액세스 옵션
description: Windows 관리 센터 (Project Honolulu)를 사용 하는 사용자 액세스 옵션 및 id 공급자
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 084cdae0bf8ca0eb3aff1f4679d30978b860efef
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356922"
---
# <a name="user-access-options-with-windows-admin-center"></a>Windows 관리 센터를 사용 하는 사용자 액세스 옵션

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Server에 배포 하는 경우 Windows 관리 센터에서 서버 환경을 위한 중앙 집중식 관리 지점을 제공 합니다. Windows 관리 센터에 대 한 액세스를 제어 하 여 관리 환경에 대 한 보안을 향상 시킬 수 있습니다.

## <a name="gateway-access-roles"></a>게이트웨이 액세스 역할

Windows 관리 센터는 게이트웨이 서비스에 액세스 하기 위해 게이트웨이 사용자 및 게이트웨이 관리자의 두 가지 역할을 정의 합니다.

> [!NOTE]
> 게이트웨이에 대 한 액세스는 게이트웨이에서 표시 하는 대상 서버에 대 한 액세스를 암시 하지 않습니다. 대상 서버를 관리 하려면 사용자는 대상 서버에 대 한 관리 권한이 있는 자격 증명을 사용 하 여 연결 해야 합니다.

게이트웨이 **사용자** 는 해당 게이트웨이를 통해 서버를 관리 하기 위해 Windows 관리 센터 게이트웨이 서비스에 연결할 수 있지만, 게이트웨이를 인증 하는 데 사용 되는 액세스 권한 또는 인증 메커니즘은 변경할 수 없습니다.

**게이트웨이 관리자** 는 액세스 권한을 받는 사용자 및 사용자가 게이트웨이에 인증 하는 방법을 구성할 수 있습니다.

>[!NOTE]
> Windows 관리 센터에 정의 된 액세스 그룹이 없는 경우 역할에는 게이트웨이 서버에 대 한 Windows 계정 액세스 권한이 반영 됩니다. 

[Windows 관리 센터에서 게이트웨이 사용자 및 관리자 액세스를 구성 합니다.](../configure/user-access-control.md)

## <a name="identity-provider-options"></a>Id 공급자 옵션

게이트웨이 관리자는 다음 중 하나를 선택할 수 있습니다.

 - [Active Directory/로컬 컴퓨터 그룹](../configure/user-access-control.md#active-directory-or-local-machine-groups)
 - [Windows 관리 센터에 대 한 id 공급자 Azure Active Directory](../configure/user-access-control.md#azure-active-directory)


### <a name="smartcard-authentication"></a>스마트 카드 인증

Active Directory 또는 로컬 컴퓨터 그룹을 id 공급자로 사용 하는 경우 Windows 관리 센터에 액세스 하는 사용자가 추가 스마트 카드 기반 보안 그룹의 구성원이 되도록 요구 하 여 스마트 카드 인증을 적용할 수 있습니다. [Windows 관리 센터에서 스마트 카드 인증을 구성 합니다.](../configure/user-access-control.md#active-directory-or-local-machine-groups)

### <a name="conditional-access-and-multi-factor-authentication"></a>조건부 액세스 및 multi-factor authentication

게이트웨이에 대 한 Azure AD 인증을 요구 하 여 Azure AD에서 제공 하는 조건부 액세스 및 multi-factor authentication과 같은 추가 보안 기능을 활용할 수 있습니다. [Azure Active Directory를 사용 하 여 조건부 액세스 구성에 대해 자세히 알아보세요.](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## <a name="role-based-access-control"></a>역할 기반 액세스 제어

기본적으로 사용자에 게는 Windows 관리 센터를 사용 하 여 관리 하려는 컴퓨터에 대 한 전체 로컬 관리자 권한이 있어야 합니다.
이렇게 하면 원격 컴퓨터에 원격으로 연결 하 여 시스템 설정을 보고 수정할 수 있는 충분 한 권한이 있는지 확인할 수 있습니다.
그러나 일부 사용자는 작업을 수행 하기 위해 컴퓨터에 대 한 무제한 액세스가 필요 하지 않을 수 있습니다.
Windows 관리 센터에서 **역할 기반 액세스 제어** 를 사용 하 여 이러한 사용자에 게 전체 로컬 관리자가 아닌 컴퓨터에 대 한 제한 된 액세스 권한을 제공할 수 있습니다.

Windows 관리 센터의 역할 기반 access control은 PowerShell을 사용 하 여 [각 관리 되](https://aka.ms/jeadocs) 는 서버를 구성 하는 방식으로 작동 합니다.
이 끝점은 각 역할이 관리할 수 있는 시스템의 측면과 역할에 할당 된 사용자를 포함 하 여 역할을 정의 합니다.
사용자가 제한 된 끝점에 연결 하면 시스템을 대신 하 여 시스템을 관리 하기 위해 임시 로컬 관리자 계정이 만들어집니다.
이렇게 하면 자체 위임 모델이 없는 도구도 Windows 관리 센터에서 계속 관리할 수 있습니다.
사용자가 Windows 관리 센터를 통해 컴퓨터 관리를 중지 하면 임시 계정이 자동으로 제거 됩니다.

사용자가 역할 기반 액세스 제어를 사용 하 여 구성 된 컴퓨터에 연결 하는 경우 Windows 관리 센터는 먼저 로컬 관리자 인지 확인 합니다.
그러한 경우에는 모든 제한 없이 전체 Windows 관리 센터 환경을 받게 됩니다.
그렇지 않으면 Windows 관리 센터에서 사용자가 미리 정의 된 역할에 속하는지 여부를 확인 합니다.
사용자가 Windows 관리 센터 역할에 속하지만 전체 관리자가 아닌 경우에는 *제한 된 액세스* 권한이 있다고 합니다.
마지막으로 사용자가 관리자 또는 역할의 멤버가 아닌 경우 컴퓨터를 관리 하기 위한 액세스가 거부 됩니다.

역할 기반 액세스 제어는 서버 관리자 및 장애 조치 (Failover) 클러스터 솔루션에 사용할 수 있습니다.

### <a name="available-roles"></a>사용 가능한 역할

Windows 관리 센터는 다음과 같은 최종 사용자 역할을 지원 합니다.

역할 이름 | 올바른 사용법
----------|-------------
Administrators | 사용자가 원격 데스크톱 또는 PowerShell에 대 한 액세스 권한을 부여 하지 않고 Windows 관리 센터에서 대부분의 기능을 사용할 수 있습니다. 이 역할은 컴퓨터에서 관리 진입점을 제한 하려는 "점프 서버" 시나리오에 적합 합니다.
Readers | 사용자가 서버에서 정보 및 설정을 볼 수 있지만 변경할 수는 없습니다.
Hyper-V 관리자 | 사용자가 Hyper-v 가상 컴퓨터 및 스위치를 변경할 수 있지만 다른 기능을 읽기 전용 액세스로 제한할 수 있습니다.

사용자가 제한 된 액세스로 연결 하는 경우 다음과 같은 기본 제공 확장 기능이 제한 됩니다.

- 파일 (파일 업로드 또는 다운로드 없음)
- PowerShell (사용할 수 없음)
- 원격 데스크톱 (사용할 수 없음)
- 저장소 복제본 (사용할 수 없음)

지금은 조직에 대 한 사용자 지정 역할을 만들 수 없지만 각 역할에 대 한 액세스 권한이 부여 된 사용자를 선택할 수 있습니다.

### <a name="preparing-for-role-based-access-control"></a>역할 기반 액세스 제어 준비

임시 로컬 계정을 활용 하려면 Windows 관리 센터에서 역할 기반 액세스 제어를 지원 하도록 각 대상 컴퓨터를 구성 해야 합니다.
구성 프로세스에는 필요한 상태 구성을 사용 하 여 컴퓨터에 PowerShell 스크립트와 충분 한 관리 끝점을 설치 하는 작업이 포함 됩니다.

컴퓨터 수가 많지 않은 경우에는 Windows 관리 센터의 역할 기반 액세스 제어 페이지를 사용 하 여 각 컴퓨터에 구성을 개별적으로 적용할 수 있습니다.
개별 컴퓨터에서 역할 기반 액세스 제어를 설정 하면 각 역할에 대 한 액세스를 제어 하는 로컬 보안 그룹이 만들어집니다.
사용자 또는 다른 보안 그룹을 역할 보안 그룹의 구성원으로 추가 하 여 액세스 권한을 부여할 수 있습니다.

여러 컴퓨터에 대 한 엔터프라이즈급 배포의 경우 게이트웨이에서 구성 스크립트를 다운로드 하 고 원하는 상태 구성 끌어오기 서버, Azure Automation 또는 선호 하는 관리 도구를 사용 하 여 컴퓨터에 배포할 수 있습니다.
