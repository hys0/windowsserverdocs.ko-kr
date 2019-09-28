---
title: 설정
description: Windows 관리 센터 (Project Honolulu)의 설정에 대해 알아봅니다. 사용자 설정을 통해 사용자는 자신의 언어/지역 및 기타 기본 설정을 변경할 수 있습니다. 관리자는 게이트웨이 설정을 사용 하 여 게이트웨이를 구성할 수 있습니다.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 04/12/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: e0fd6618f275058d4e22fe9abb9e484d4752ac9a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407056"
---
# <a name="windows-admin-center-settings"></a>Windows 관리 센터 설정

> 적용 대상: Windows Admin Center

Windows 관리 센터 설정은 사용자 수준 및 게이트웨이 수준 설정으로 구성 됩니다. 사용자 수준 설정에 대 한 변경 내용은 현재 사용자의 프로필에만 영향을 주지만 게이트웨이 수준 설정이 변경 되 면 해당 Windows 관리 센터 게이트웨이의 모든 사용자에 게 영향을 줍니다.

## <a name="user-settings"></a>사용자 설정

사용자 수준 설정은 다음 섹션으로 구성 됩니다.

- 계정
- Personalization
- 언어/지역
- 제안
- 고급

**계정** 탭에서 사용자는 Windows 관리 센터에 인증 하는 데 사용한 자격 증명을 검토할 수 있습니다. Azure AD가 id 공급자로 구성 된 경우 사용자는이 탭에서 해당 Azure AD 계정에서 로그 아웃할 수 있습니다.

**개인 설정** 탭에서 사용자는 어두운 UI 테마를 전환할 수 있습니다.

**언어/지역** 탭에서 사용자는 Windows 관리 센터에서 표시 하는 언어 및 지역 형식을 변경할 수 있습니다.

**제안** 탭에서 사용자는 Azure 서비스 및 새로운 기능에 대 한 제안을 전환할 수 있습니다.

**고급** 탭에서는 Windows 관리 센터 확장 개발자에 게 추가 기능을 제공 합니다.

## <a name="gateway-settings"></a>게이트웨이 설정

게이트웨이 수준 설정은 다음 섹션으로 구성 됩니다.

- Extensions
- 액세스 권한
- Azure
- 공유 연결

게이트웨이 관리자만 이러한 설정을 보고 변경할 수 있습니다. 이러한 설정을 변경 하면 게이트웨이의 구성이 변경 되 고 Windows 관리 센터 게이트웨이의 모든 사용자에 게 영향을 줍니다.

관리자는 **확장** 탭에서 게이트웨이 확장을 설치, 제거 또는 업데이트할 수 있습니다. [확장에 대해 자세히 알아보세요.](using-extensions.md)

관리자는 **액세스** 탭을 사용 하 여 Windows 관리 센터 게이트웨이에 액세스할 수 있는 사용자와 사용자를 인증 하는 데 사용 되는 id 공급자를 구성할 수 있습니다. [게이트웨이에 대 한 액세스 제어에 대해 자세히 알아보세요.](user-access-control.md)

관리자는 **azure** 탭에서 azure에 게이트웨이를 등록 하 여 Windows 관리 센터에서 [azure 통합 기능](azure-integration.md) 을 사용 하도록 설정할 수 있습니다.

관리자는 **공유 연결** 탭을 사용 하 여 Windows 관리 센터 게이트웨이의 모든 사용자에서 공유할 단일 연결 목록을 구성할 수 있습니다. [게이트웨이의 모든 사용자에 대해 한 번 연결을 구성 하는 방법에 대해 자세히 알아보세요.](shared-connections.md)