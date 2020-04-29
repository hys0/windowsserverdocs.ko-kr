---
title: Settings
description: Windows Admin Center(Project Honolulu)의 설정에 대해 알아봅니다. 사용자 설정을 사용하여 언어/지역 및 기타 기본 설정을 변경할 수 있습니다. 관리자는 게이트웨이 설정을 사용하여 게이트웨이를 구성할 수 있습니다.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 04/12/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: e0fd6618f275058d4e22fe9abb9e484d4752ac9a
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "71407056"
---
# <a name="windows-admin-center-settings"></a>Windows Admin Center 설정

> 적용 대상: Windows Admin Center

Windows Admin Center 설정은 사용자 수준 설정과 게이트웨이 수준 설정으로 구성되어 있습니다. 사용자 수준 설정을 변경하면 현재 사용자의 프로필에만 영향을 주는 반면, 게이트웨이 수준 설정을 변경하면 해당 Windows Admin Center 게이트웨이의 모든 사용자에게 영향을 미칩니다.

## <a name="user-settings"></a>사용자 설정

사용자 수준 설정은 다음 섹션으로 구성됩니다.

- 계정
- 개인 설정
- 언어/지역
- 제안
- 고급

**계정** 탭에서 사용자는 Windows Admin Center 인증에 사용한 자격 증명을 검토할 수 있습니다. Azure AD가 자격 증명 공급자가 되도록 구성된 경우, 사용자는 이 탭에서 Azure AD 계정에서 로그아웃할 수 있습니다.

**개인 설정** 탭에서 사용자는 어두운 UI 테마로 전환할 수 있습니다.

**언어/지역** 탭에서 사용자는 Windows Admin Center에 표시되는 언어 및 지역 형식을 변경할 수 있습니다.

**제안** 탭에서 사용자는 Azure 서비스 및 새로운 기능에 대한 제안을 토글할 수 있습니다.

**고급** 탭은 Windows Admin Center 확장 개발자에게 추가 기능을 제공합니다.

## <a name="gateway-settings"></a>게이트웨이 설정

게이트웨이 수준 설정은 다음 섹션으로 구성됩니다.

- 확장
- 액세스
- Azure
- 공유 연결

게이트웨이 관리자만 이러한 설정을 보고 변경할 수 있습니다. 이러한 설정을 변경하면 게이트웨이 구성이 변경되고 Windows Admin Center 게이트웨이의 모든 사용자에게 영향을 줍니다.

**확장** 탭에서 관리자는 게이트웨이 확장을 설치, 제거 또는 업데이트할 수 있습니다. [확장 프로그램에 대해 자세히 알아보세요.](using-extensions.md)

관리자는 **액세스** 탭을 통해 Windows Admin Center 게이트웨이에 액세스할 수 있는 사람과 사용자를 인증하는 데 사용되는 자격 증명 공급자를 구성할 수 있습니다. [게이트웨이에 대한 액세스 제어에 대해 자세히 알아보세요.](user-access-control.md)

**Azure** 탭에서 관리자는 Windows Admin Center에서 [Azure 통합 기능](azure-integration.md)을 사용하도록 Azure에 게이트웨이를 등록할 수 있습니다.

관리자는 **공유 연결** 탭을 사용하여 단일 연결 목록을 Windows Admin Center 게이트웨이의 모든 사용자가 공유하도록 구성할 수 있습니다. [게이트웨이의 모든 사용자를 위한 연결 구성에 대해 자세히 알아보세요.](shared-connections.md)