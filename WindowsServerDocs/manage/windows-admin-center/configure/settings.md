---
title: 설정
description: Windows Admin Center (Project Honolulu)의 설정에 알아봅니다. 사용자 설정을 통해 사용자가 자신의 언어/지역 및 기타 기본 설정을 변경할 수 있습니다. 게이트웨이 설정을 게이트웨이 구성 관리자를 사용 합니다.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 04/12/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: d67a2c743900792353141186112cd09dbf780309
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296625"
---
# Windows Admin Center 설정

> 적용 대상: Windows Admin Center

Windows Admin Center 설정 사용자 수준 및 게이트웨이 수준 설정을 구성합니다. 사용자 액세스 제어 설정에 대 한 변경만 게이트웨이 수준 설정에 대 한 변경 해당 Windows Admin Center 게이트웨이의 모든 사용자를 적용 하는 동안 현재 사용자의 프로필을 영향을 줍니다.

## 사용자 설정

사용자 수준 설정의 다음 섹션으로 구성 됩니다.

- 계정
- Personalization
- 언어/지역
- 제안
- 고급

**계정** 탭에서 사용자는 Windows Admin Center를 인증을 사용 하는 자격 증명을 검토할 수 있습니다. Azure AD를 id 공급자를 구성 하는 경우 사용자가 자신의 Azure AD 계정을이 탭에서 기록할 수 있습니다.

**개인 설정** 탭에서 사용자가 UI 어두운 테마로 전환할 수 있습니다.

**언어/지역** 탭에서 사용자가 Windows Admin Center에서 표시 언어 및 지역 형식을 변경할 수 있습니다.

**제안** 탭에서 사용자가 Azure 서비스 및 새로운 기능에 대 한 제안 전환할 수 있습니다.

**고급** 탭 Windows Admin Center 확장 개발자가 추가 기능을 제공합니다.

## 게이트웨이 설정

게이트웨이 수준 설정의 다음 섹션으로 구성 됩니다.

- 확장
- Access
- Azure
- 공유 연결

게이트웨이 관리자만 이러한 설정을 보거나 변경할 수 있습니다. 이러한 설정 변경 사항 게이트웨이의 구성을 변경 하 고 Windows Admin Center 게이트웨이의 모든 사용자에 게 적용 합니다.

**확장** 탭에서 관리자 수 설치, 제거 또는 업데이트 게이트웨이 확장 합니다. [확장에 대해 알아봅니다.](using-extensions.md)

**액세스** 탭 관리자가 Windows Admin Center 게이트웨이 뿐만 아니라 사용자를 인증 하는 데 사용 되는 id 공급자에 액세스할 수 있는 사용자를 구성할 수 있습니다. [게이트웨이에 대 한 액세스를 제어 하는 방법에 대 한 자세히 알아보세요.](user-access-control.md)

**Azure** 탭에서 관리자가 Windows 관리 센터에서 [Azure 통합 기능](azure-integration.md) 활성화 하는 Azure와 게이트웨이 등록할 수 있습니다.

**공유 연결** 탭을 사용 하 여 관리자가 Windows Admin Center 게이트웨이의 모든 사용자가 공유에 대 한 연결 단일 목록을 구성할 수 있습니다. [게이트웨이의 모든 사용자가 한 번에 대 한 연결을 구성 하는 방법에 대 한 자세한 내용은 합니다.](shared-connections.md)