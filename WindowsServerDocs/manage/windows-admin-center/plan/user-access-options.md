---
title: Windows Admin Center를 사용 하 여 사용자 액세스 옵션
description: Windows Admin Center (Project Honolulu)를 사용 하 여 id 공급자 및 사용자 액세스 옵션
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 9adea736d6e7ae181bdfe50289564083146f5b30
ms.sourcegitcommit: 4961576f2891600ef9a760ca7df650d14332e057
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/09/2019
ms.locfileid: "9151998"
---
# Windows Admin Center를 사용 하 여 사용자 액세스 옵션

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Server를 배포할 때 Windows Admin Center 서버 환경에 대 한 관리의 중앙된 지점을 제공 합니다. Windows Admin Center에 대 한 액세스를 제어 관리 가로의 보안을 향상 시킬 수 있습니다.

## 게이트웨이 액세스 역할

Windows Admin Center 게이트웨이 서비스에 대 한 액세스에 대 한 두 가지 역할을 정의: 게이트웨이 사용자와 게이트웨이 관리자.

> [!NOTE]
> 게이트웨이에 액세스 게이트웨이 하 여 표시 되는 대상 서버에 대 한 액세스를 의미 하지 않습니다. 대상 서버를 관리 하려면 사용자는 대상 서버에 대 한 관리자 권한이 있는 자격 증명으로 연결 해야 합니다.

**게이트웨이 사용자가** 해당 게이트웨이 통해 서버를 관리 하기 위해 Windows Admin Center 게이트웨이 서비스에 연결할 수 있지만 액세스 권한 및 게이트웨이 인증에 사용 되는 인증 메커니즘은 변경할 수 없습니다.

**게이트웨이 관리자** 액세스 권한도 누가 사용자 인증 게이트웨이 하는 방법과 구성할 수 있습니다.

>[!NOTE]
> Windows Admin Center에 정의 된 액세스 그룹이 인 경우 게이트웨이 서버에 대 한 Windows 계정 액세스는 역할에 반영 됩니다. 

[Windows Admin Center에서 사용자 및 관리자 액세스 게이트웨이 구성 합니다.](../configure/user-access-control.md)

## Identity 공급자 옵션

게이트웨이 관리자는 다음 중 하나를 선택할 수 있습니다.

 - [Active Directory/로컬 컴퓨터 그룹](../configure/user-access-control.md#active-directory-or-local-machine-groups)
 - [Windows Admin Center에 대 한 id 공급자로 azure Active Directory](../configure/user-access-control.md#azure-active-directory)


### 스마트 카드 인증

Active Directory 또는 로컬 컴퓨터 그룹을 사용 하 여 id 공급자 역할을 하는 경우 추가 스마트 카드 기반 보안 그룹의 구성원으로 Windows Admin Center에 액세스 하는 사용자에 게 요청 하 여 스마트 카드 인증을 적용할 수 있습니다. [Windows Admin Center에서 스마트 카드 인증을 구성 합니다.](../configure/user-access-control.md#active-directory-or-local-machine-groups)

### 조건부 액세스 및 다단계 인증

게이트웨이에 대 한 Azure AD 인증을 요구 함으로써 조건부 액세스 및 Azure AD에서 제공 하는 다단계 인증 같은 추가적인 보안 기능을 활용할 수 있습니다. [Azure Active directory 조건부 액세스 구성에 대해 알아봅니다.](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## 역할 기반 액세스 제어

기본적으로 사용자가 Windows Admin Center를 사용 하 여 관리 하려는 컴퓨터에서 전체 로컬 관리자 권한이 필요 합니다.
이 컴퓨터에 원격으로 연결을 허용 하 고 충분 한 수 있는 권한이 있는지 확인 하 고 수정할 시스템 설정 되도록 합니다.
하지만 일부 사용자 작업을 수행할 컴퓨터에 제한 없이 액세스할이 필요 하지 않을 수 있습니다.
이러한 전체 로컬 관리자를 만드는 대신 컴퓨터에 대 한 액세스가 제한 된 이러한 사용자에 게 제공 하기 위해 Windows Admin Center의 **역할 기반 액세스 제어** 를 사용할 수 있습니다.

Windows Admin Center의 역할 기반 액세스 제어 PowerShell [Just Enough Administration](https://aka.ms/jeadocs) 끝점을 사용 하 여 각 관리 되는 서버를 구성 하 여 작동 합니다.
이 끝점을 포함 하 여 시스템의 측면 각 역할 관리 하도록 허용 하 고 있는 사용자 역할에 할당 된 역할을 정의 합니다.
사용자가 제한 된 끝점에 연결할 때 대신 하 여 시스템을 관리 하는 임시 로컬 관리자 계정을 만들어집니다.
이렇게 하면 자신의 위임 모델 없는 도구에도 Windows Admin Center를 사용 하 여 계속 관리할 수 있습니다.
임시 계정 사용자가 Windows Admin Center를 통해 컴퓨터를 관리 하는 경우 자동으로 제거 됩니다.

사용자 역할 기반 액세스 제어를 사용 하 여 구성 하는 컴퓨터에 연결할 때 Windows Admin Center는 로컬 관리자 인지 확인 먼저 합니다.
이러한 경우 제한 없이 Windows Admin Center 환경 전체 받게 됩니다.
그렇지 않은 경우 Windows Admin Center는 경우 사용자가 속한 미리 정의 된 역할을 확인 합니다.
Windows Admin Center 역할에 속해 않지만 전체 관리자가 아닌 경우 *제한* 액세스할 수 있도록 사용자 라고 합니다.
마지막으로, 사용자 관리자 지도 역할의 구성원 인 경우은 거부 됩니다 컴퓨터 관리에 대 한 액세스 합니다.

역할 기반 액세스 제어는 서버 관리자 및 장애 조치 클러스터 솔루션에 사용할 수 있습니다.

### 사용 가능한 역할

Windows Admin Center는 다음 최종 사용자 역할을 지원합니다.

역할 이름 | 올바른 사용법
----------|-------------
관리자 | 사용자가 원격 데스크톱 또는 PowerShell에 대 한 액세스 권한을 부여 하 없이 Windows Admin Center의 대부분의 기능을 사용할 수 있습니다. 이 역할은 컴퓨터에 관리 진입점을 제한 하려는 "서버 이동" 시나리오에 적합 합니다.
판독기 | 변경 하지 하지만 서버에서 설정 및 정보를 볼 수 있습니다.
Hyper-v 관리자 | Hyper-v 가상 컴퓨터와 스위치를 변경할 수 있도록 하지만 다른 기능을 읽기 전용 액세스를 제한 합니다.

다음 기본 제공 확장 제한 된 액세스 사용자가 연결 기능이 감소 합니다.

- 파일 (파일 업로드 또는 다운로드 없음)
- PowerShell (사용할 수 없음)
- 원격 데스크톱 (사용할 수 없음)
- 저장소 복제본 (사용할 수 없음)

이때 사용자가 조직에 대 한 역할 사용자 지정을 만들 수는 없지만 있는 사용자는 각 역할에 대 한 액세스를 부여 선택할 수 있습니다.

### 역할 기반 액세스 제어 하기 위한 준비

임시 로컬 계정을 활용 하려면 각 대상 컴퓨터를 Windows Admin Center의 역할 기반 액세스 제어를 지원 하도록 구성 해야 합니다.
구성 프로세스는 PowerShell 스크립트 및 Just Enough Administration 끝점 필요한 상태 구성 사용 하 여 컴퓨터에 설치 해야 합니다.

몇 대의 컴퓨터만 있으면 쉽게 적용할 수 구성을 개별적으로 역할 기반 액세스 제어 페이지를 사용 하 여 Windows 관리 센터에서 각 컴퓨터.
개별 컴퓨터에 역할 기반 액세스 제어를 설정할 때 각 역할에 대 한 액세스를 제어 하려면 로컬 보안 그룹이 만들어집니다.
역할 보안 그룹의 구성원으로 추가 하 여 사용자 또는 다른 보안 그룹에 대 한 액세스 권한을 부여할 수 있습니다.

여러 대의 컴퓨터에는 엔터프라이즈 배포에 대 한 구성 스크립트 게이트웨이에서 다운로드할 수 있으며 필요한 상태 구성 끌어오기 서버, Azure 자동화 또는 기본 설정된 관리 도구를 사용 하 여 컴퓨터에 배포할 수 있습니다.
