---
title: Azure 통합 구성
description: Azure 통합 Windows 관리 센터 (Project Honolulu)를 구성 합니다. Windows 관리 센터 게이트웨이를 Azure에 연결 합니다.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/19/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 448a8fb3e4340752b673b06f86d5d49211b6b147
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357361"
---
# <a name="configuring-azure-integration"></a>Azure 통합 구성

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows 관리 센터는 Azure 서비스와 통합 되는 여러 가지 선택적 기능을 지원 합니다. [Windows 관리 센터에서 사용할 수 있는 Azure 통합 옵션에 대해 알아봅니다.](../plan/azure-integration-options.md)

Azure 사이트를 사용 하 여 windows 관리 센터에서 관리 되는 Vm을 보호 하는 등의 방법으로 Windows 관리 센터 게이트웨이에서 Azure와 통신 하 여 게이트웨이 액세스를 위한 Azure Active Directory 인증을 활용 하거나 사용자 대신 Azure 리소스를 만들 수 있습니다. 복구)를 사용 하려면 먼저 Azure에 Windows 관리 센터 게이트웨이를 등록 해야 합니다. Windows 관리 센터 게이트웨이에 대해이 작업을 한 번만 수행 하면 됩니다. 게이트웨이를 최신 버전으로 업데이트 하는 경우에는 설정이 유지 됩니다.

## <a name="register-your-gateway-with-azure"></a>Azure를 사용 하 여 게이트웨이 등록

Windows 관리 센터에서 처음으로 Azure 통합 기능을 사용 하려고 할 때 게이트웨이를 Azure에 등록 하 라는 메시지가 표시 됩니다. Windows 관리 센터 설정에서 **Azure** 탭으로 이동 하 여 게이트웨이를 등록할 수도 있습니다.

단계별 제품 단계에서는 Windows 관리 센터가 Azure와 통신할 수 있도록 하는 Azure AD 앱을 디렉터리에 만듭니다. 자동으로 만들어진 Azure AD 앱을 보려면 Windows 관리 센터 설정의 **azure** 탭으로 이동 합니다. **Azure의 보기** 하이퍼링크를 사용 하 여 Azure Portal에서 azure AD 앱을 볼 수 있습니다. 

만든 Azure AD 앱은 게이트웨이에 대 한 [AZURE ad 인증](../configure/user-access-control.md#azure-active-directory)을 포함 하 여 Windows 관리 센터의 모든 azure 통합 지점에 사용 됩니다.