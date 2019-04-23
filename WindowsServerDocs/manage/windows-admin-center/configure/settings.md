---
title: 설정
description: Windows Admin Center (프로젝트 브라 티)에서 설정을 알아봅니다. 사용자 설정 사용 사용자가 자신의 언어/지역 및 기타 기본 설정을 변경할 수 있습니다. 게이트웨이 설정을 게이트웨이 구성 관리자를 사용 합니다.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/19/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 1e1231500733f70ddfcbd4f8a847047b73f24a00
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882384"
---
# <a name="settings"></a>설정

> 적용 대상: Windows Admin Center

Windows Admin Center 설정-사용자 수준 및 게이트웨이 수준 설정을 구성합니다. 사용자 수준 설정에 대 한 변경만 게이트웨이 수준 설정에 대 한 변경의 모든 사용자에 해당 Windows Admin Center 게이트웨이에 영향을 줍니다 하지만 현재 사용자의 프로필을 영향을 줍니다.

## <a name="user-settings"></a>사용자 설정

다음 섹션의 사용자 수준 설정은 구성 됩니다.

- 계정
- 언어/지역
- 제안

에 **계정** 탭, 사용자가 있었던 인증 Windows Admin Center 자격 증명을 검토할 수 있습니다. Azure AD는 id 공급자를 구성 하는 경우 사용자는이 탭에서 Azure AD 계정에서 기록할 수 있습니다.

에 **언어/지역** 탭 사용자 Windows Admin Center 하 여 표시 언어 및 지역 형식을 변경할 수 있습니다.

에 **제안** 탭, 사용자는 Azure 서비스 및 새 기능에 대 한 제안을 전환할 수 있습니다.

### <a name="dark-theme"></a>어두운 테마

> 적용 대상: Windows Admin Center 미리 보기

Windows Admin Center 미리 보기에서 잠금을 해제할 수 있습니다 추가로 **개인 설정** 어두운 UI 테마에 설정/해제 하는 옵션을 포함 하는 섹션입니다. 사용 하도록 설정 합니다 **개인 설정** 섹션에서 입력 ```msft.sme.shell.personalization``` 실험 키로 합니다.

>[!IMPORTANT]
> 어두운 테마는 진행 중인 작업,이 이번에 버그를 보고를 수행 하세요.

## <a name="gateway-settings"></a>게이트웨이 설정

다음 섹션의 게이트웨이 수준 설정은 구성 됩니다.

- Extensions
- 액세스 권한
- Azure

게이트웨이 관리자만 이러한 설정을 보거나 변경할 수 있습니다. 게이트웨이의 구성을 변경 하 고 Windows Admin Center 게이트웨이의 모든 사용자에 게 적용 하는 이러한 설정 변경 합니다.

에 **확장** 탭 관리자 수를 설치, 제거 또는 게이트웨이 확장을 업데이트 합니다. [확장에 대해 알아봅니다.](using-extensions.md)

합니다 **액세스** 탭에서는 사용자를 인증 하는 데 사용 하는 id 공급자 뿐만 아니라 Windows Admin Center 게이트웨이에 액세스할 수 있는 사용자를 구성 하는 관리자가 있습니다. [게이트웨이에 대 한 액세스를 제어 하는 방법에 대 한 자세히 알아봅니다.](user-access-control.md)

**Azure** 탭, 관리자 수 있도록 Azure를 사용 하 여 게이트웨이 등록할 수 있습니다 [Azure 통합 기능](azure-integration.md) Windows Admin Center.