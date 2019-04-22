---
title: Windows Admin Center 사용 하 여 사용자 액세스 옵션
description: 사용자 액세스 옵션 및 Windows Admin Center (프로젝트 브라 티)를 사용 하 여 id 공급자
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 9adea736d6e7ae181bdfe50289564083146f5b30
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825894"
---
# <a name="user-access-options-with-windows-admin-center"></a>Windows Admin Center 사용 하 여 사용자 액세스 옵션

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows 서버에 배포 하는 경우 Windows Admin Center 중앙 집중식된 서버 환경에 관리 지점을 제공 합니다. Windows Admin Center 대 한 액세스 제어 관리 환경의의 보안을 향상 시킬 수 있습니다.

## <a name="gateway-access-roles"></a>게이트웨이 액세스 역할

게이트웨이 서비스에 액세스를 위한 두 가지 역할을 정의 하는 Windows Admin Center: 게이트웨이 사용자와 게이트웨이 관리자입니다.

> [!NOTE]
> 게이트웨이에 액세스 게이트웨이에서 표시 대상 서버에 대 한 액세스를 의미 하지 않습니다. 대상 서버를 관리 하려면 사용자는 대상 서버에 대 한 관리 권한이 있는 자격 증명을 사용 하 여 연결 해야 합니다.

**게이트웨이 사용자** 해당 게이트웨이 통해 서버를 관리 하기 위해 Windows Admin Center 게이트웨이 서비스에 연결할 수 있지만 게이트웨이 인증에 사용 하는 인증 메커니즘 또는 액세스 권한을 변경할 수 없습니다.

**게이트웨이 관리자** 게이트웨이에 사용자가 인증 방법과 누가 액세스도 구성할 수 있습니다.

>[!NOTE]
> Windows Admin Center 정의 된 액세스 그룹이 없는 경우 게이트웨이 서버에 대 한 Windows 계정 액세스는 역할에 반영 됩니다. 

[Windows Admin Center 게이트웨이 사용자 및 관리자 액세스를 구성 합니다.](../configure/user-access-control.md)

## <a name="identity-provider-options"></a>Id 공급자 옵션

게이트웨이 관리자는 다음 중 하나를 선택할 수 있습니다.

 - [Active Directory/로컬 컴퓨터 그룹](../configure/user-access-control.md#active-directory-or-local-machine-groups)
 - [Windows Admin Center 대 한 id 공급자로 azure Active Directory](../configure/user-access-control.md#azure-active-directory)


### <a name="smartcard-authentication"></a>스마트 카드 인증

Active Directory 또는 로컬 컴퓨터 그룹 id 공급자로 사용 하는 경우에 Windows Admin Center 추가 스마트 카드 기반 보안 그룹의 구성원으로 액세스 하는 사용자를 요구 하 여 스마트 카드 인증을 적용할 수 있습니다. [Windows Admin Center 스마트 카드 인증을 구성 합니다.](../configure/user-access-control.md#active-directory-or-local-machine-groups)

### <a name="conditional-access-and-multi-factor-authentication"></a>조건부 액세스 및 multi-factor authentication

게이트웨이에 대 한 Azure AD 인증을 요구 하 여 조건부 액세스 및 Azure AD에서 제공 하는 multi-factor authentication과 같은 추가 보안 기능을 활용할 수 있습니다. [Azure Active Directory를 사용 하 여 조건부 액세스를 구성 하는 방법에 대 한 자세히 알아봅니다.](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## <a name="role-based-access-control"></a>역할 기반 액세스 제어

기본적으로 사용자가 Windows Admin Center 사용 하 여 관리 하려는 컴퓨터에서 전체 로컬 관리자 권한이 필요 합니다.
이 컴퓨터에 원격으로 연결할 수 있도록 하 고 시스템 설정 보기 및 수정에 충분 한 권한이 있는 확인 합니다.
그러나 일부 사용자에 해당 작업을 수행 하려면 컴퓨터에 대 한 무제한 액세스가 필요는 없습니다.
사용할 수 있습니다 **역할 기반 액세스 제어** 하 전체 로컬 관리자를 설정 하는 대신 컴퓨터에 대 한 제한 된 액세스를 사용 하 여 이러한 사용자에 게 제공 하려면 Windows Admin Center.

PowerShell을 사용 하 여 관리 되는 각 서버를 구성 하 여 Windows Admin Center 역할 기반 액세스 제어 작동 [Just Enough Administration](https://aka.ms/jeadocs) 끝점입니다.
이 끝점에는 시스템의 어떤 측면 역할별로 관리 하도록 허용 하 고 역할에 할당 된 사용자를 포함 하 여 역할을 정의 합니다.
사용자가 제한 된 끝점에 연결할 때 본인을 대신해 시스템을 관리 하는 임시 로컬 관리자 계정 생성 됩니다.
이렇게 하면 자신의 위임 모델 없는 도구 Windows Admin Center 사용 하 여 계속 관리할 수 있습니다.
임시 계정은 사용자가 Windows Admin Center 통해 컴퓨터를 관리 하는 경우에 자동으로 제거 됩니다.

사용자 역할 기반 액세스 제어를 사용 하 여 구성 된 컴퓨터에 연결할 때 Windows Admin Center 로컬 관리자 인지 확인 먼저 합니다.
이러한 경우 제한 없는 전체 Windows Admin Center 환경을 받게 됩니다.
그렇지 않은 경우 Windows Admin Center 사용자가 미리 정의 된 역할 중 하나에 속한 경우 확인 합니다.
사용자가 이라고 *제한 된 액세스* Windows Admin Center 역할에 속해 있지만 전체 관리자가 아닌 경우.
마지막으로, 사용자 관리자도 아니고 역할의 멤버인 경우는 거부 됩니다 컴퓨터를 관리에 대 한 액세스.

역할 기반 액세스 제어는 서버 관리자 및 장애 조치 클러스터 솔루션에 대해 사용할 수 있습니다.

### <a name="available-roles"></a>사용 가능한 역할

Windows Admin Center에서는 다음 최종 사용자 역할을 지원합니다.

역할 이름 | 올바른 사용법
----------|-------------
Administrators | 원격 데스크톱 또는 PowerShell에 대 한 액세스 권한을 부여 하지 않고 Windows Admin Center 대부분의 기능을 사용할 수 있습니다. 이 역할은 컴퓨터에서 관리 진입점을 제한 하려는 "점프 서버" 시나리오에 적합 합니다.
Readers | 서버에서 정보 및 설정을 볼 수 있지만을 변경 하지 않고 있습니다.
Hyper-V 관리자 | Hyper-v virtual machines 및 스위치를 변경할 수 있습니다 하지만 읽기 전용으로 액세스 하는 기타 기능으로 제한 합니다.

사용자가 제한 된 액세스를 사용 하 여 다음 기본 제공 확장 기능이 감소 합니다.

- 파일 (파일 업로드 또는 다운로드)
- PowerShell (사용할 수 없음)
- 원격 데스크톱 (사용할 수 없음)
- 저장소 복제본 (사용할 수 없음)

이때 조직에 대 한 사용자 지정 역할을 만들 수는 없지만 각 역할에 대 한 액세스 부여 될 사용자를 선택할 수 있습니다.

### <a name="preparing-for-role-based-access-control"></a>역할 기반 액세스 제어에 대 한 준비

임시 로컬 계정을 활용 하려면 각 대상 컴퓨터를 Windows Admin Center 역할 기반 액세스 제어를 지원 하도록 구성 해야 합니다.
구성 과정 Desired State Configuration을 사용 하 여 컴퓨터에 PowerShell 스크립트 및 Just Enough Administration 끝점을 설치 합니다.

몇 대의 컴퓨터만 있는 경우 손쉽게 적용할 수 있습니다 구성을 개별적으로 Windows Admin Center 역할 기반 액세스 제어 페이지를 사용 하 여 각 컴퓨터에 있습니다.
개별 컴퓨터에서 역할 기반 액세스 제어를 설정 하는 경우 각 역할에 대 한 액세스를 제어 하도록 로컬 보안 그룹이 만들어집니다.
역할 보안 그룹의 구성원으로 추가 하 여 사용자 또는 다른 보안 그룹에 대 한 액세스를 부여할 수 있습니다.

여러 컴퓨터에서 엔터프라이즈 수준의 배포를 게이트웨이에서 구성 스크립트를 다운로드할 수 있으며 Desired State Configuration 끌어오기 서버, Azure Automation 또는 사용자 기본 설정된 관리 도구를 사용 하 여 컴퓨터에 배포할 수 있습니다.
