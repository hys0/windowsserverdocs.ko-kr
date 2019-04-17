---
title: Azure 통합 구성
description: Azure 통합 Windows Admin Center (Project Honolulu)를 구성 합니다. Windows Admin Center 게이트웨이를 Azure에 연결합니다.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/19/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 38b973680463cdebc1b3168e447abfcf1caba6b5
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296993"
---
# Azure 통합 구성

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center는 Azure 서비스와 통합 하는 여러 가지 선택적 기능을 지원 합니다. [Windows Admin Center를 사용 하 여 사용할 수 있는 Azure 통합 옵션에 알아봅니다.](../plan/azure-integration-options.md)

Windows Admin Center 게이트웨이 Azure를 활용 하는 게이트웨이 액세스를 위해 Azure Active Directory 인증 또는 Azure 리소스 (예: Azure 사이트를 사용 하 여 Windows 관리 센터에서 관리 되는 Vm을 보호 하기 위해 자동으로 만드는 통신할 수 있도록 복구)를 먼저 Windows Admin Center 게이트웨이 Azure로 등록 해야 합니다. 설정이 새 버전으로 게이트웨이 업데이트할 때 Windows Admin Center 게이트웨이-유지 되 면이 작업을 수행 해야 합니다.

## 게이트웨이 Azure로 등록

Windows Admin Center는 Azure 통합 기능을 사용 하려고 하면 처음으로 게이트웨이를 Azure 등록 하 라는 메시지가 표시 됩니다. 또한 Windows Admin Center 설정에서 **Azure** 탭으로 이동 하 여 게이트웨이 등록할 수 있습니다.

제품의 단계를 안내가 Windows Admin Center Azure와 통신할 수 있는 디렉터리에 Azure AD 응용 프로그램을 만듭니다. 자동으로 만들어지는 Azure AD 응용 프로그램을 보려면 Windows Admin Center 설정의 **Azure** 탭으로 이동 합니다. **Azure에서 보기** 하이퍼링크 Azure portal에서 Azure AD 응용 프로그램을 볼 수 있습니다. 

만든 Azure AD 응용 프로그램의 Azure 통합 [게이트웨이를 Azure AD 인증](../configure/user-access-control.md#azure-active-directory)을 포함 하 여 Windows 관리 센터의 모든 요소에 사용 됩니다.