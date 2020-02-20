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
ms.openlocfilehash: d8758342752ac71c5b700682d4c0f4317dc4cb4e
ms.sourcegitcommit: e817a130c2ed9caaddd1def1b2edac0c798a6aa2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/09/2019
ms.locfileid: "74945218"
---
# <a name="configuring-azure-integration"></a>Azure 통합 구성

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows 관리 센터는 Azure 서비스와 통합 되는 여러 가지 선택적 기능을 지원 합니다. [Windows 관리 센터에서 사용할 수 있는 Azure 통합 옵션에 대해 알아봅니다.](../plan/azure-integration-options.md)

Azure 사이트를 사용 하 여 windows 관리 센터에서 관리 되는 Vm을 보호 하는 등의 방법으로 Windows 관리 센터 게이트웨이에서 Azure와 통신 하 여 게이트웨이 액세스를 위한 Azure Active Directory 인증을 활용 하거나 사용자 대신 Azure 리소스를 만들 수 있습니다. 복구)를 사용 하려면 먼저 Azure에 Windows 관리 센터 게이트웨이를 등록 해야 합니다. Windows 관리 센터 게이트웨이에 대해이 작업을 한 번만 수행 하면 됩니다. 게이트웨이를 최신 버전으로 업데이트 하는 경우에는 설정이 유지 됩니다.

## <a name="register-your-gateway-with-azure"></a>Azure를 사용 하 여 게이트웨이 등록

Windows 관리 센터에서 처음으로 Azure 통합 기능을 사용 하려고 할 때 게이트웨이를 Azure에 등록 하 라는 메시지가 표시 됩니다. Windows 관리 센터 설정에서 **Azure** 탭으로 이동 하 여 게이트웨이를 등록할 수도 있습니다. Windows 관리 센터 게이트웨이 관리자만 Azure에 Windows 관리 센터 게이트웨이를 등록할 수 있습니다. [Windows 관리 센터 사용자 및 관리자 권한에 대해 자세히 알아보세요](../configure/user-access-control.md#gateway-access-role-definitions).

단계별 제품 단계에서는 Windows 관리 센터가 Azure와 통신할 수 있도록 하는 Azure AD 앱을 디렉터리에 만듭니다. 자동으로 만들어진 Azure AD 앱을 보려면 Windows 관리 센터 설정의 **azure** 탭으로 이동 합니다. **Azure의 보기** 하이퍼링크를 사용 하 여 Azure Portal에서 azure AD 앱을 볼 수 있습니다. 

만든 Azure AD 앱은 게이트웨이에 대 한 [AZURE ad 인증](../configure/user-access-control.md#azure-active-directory)을 포함 하 여 Windows 관리 센터의 모든 azure 통합 지점에 사용 됩니다. Windows 관리 센터는 사용자를 대신 하 여 Azure 리소스를 만들고 관리 하는 데 필요한 권한을 자동으로 구성 합니다.

- Azure Active Directory 그래프
    - 디렉터리. AccessAsUser. 모두
    - User.Read
- Azure 서비스 관리
    - user_impersonation

### <a name="manual-azure-ad-app-configuration"></a>Azure AD 앱 수동 구성

게이트웨이 등록 프로세스 중에 Windows 관리 센터에서 자동으로 만든 Azure AD 앱을 사용 하지 않고 Azure AD 앱을 수동으로 구성 하려는 경우 다음을 수행 해야 합니다.

1. 위에 나열 된 필수 API 권한을 Azure AD 앱에 부여 합니다. Azure Portal에서 Azure AD 앱으로 이동 하 여이 작업을 수행할 수 있습니다. Azure Portal > **Azure Active Directory** > **앱 등록** 으로 이동한 > 사용할 Azure AD 앱을 선택 합니다. 그런 다음 **api 권한** 탭으로가 서 위에 나열 된 api 권한을 추가 합니다.
2. Windows 관리 센터 게이트웨이 URL을 회신 Url (리디렉션 Uri 라고도 함)에 추가 합니다. Azure AD 앱으로 이동한 다음 **매니페스트**로 이동 합니다. 매니페스트에서 "replyUrlsWithType" 키를 찾습니다. 키 내에서 "url" 및 "type"의 두 키를 포함 하는 개체를 추가 합니다. "Url" 키에는 Windows 관리 센터 게이트웨이 URL의 값이 있어야 합니다. 끝에 와일드 카드를 추가 합니다. 키 "type" 키는 "Web" 값을 가져야 합니다. 예를 들면 다음과 같습니다.

    ```json
    "replyUrlsWithType": [
            {
                    "url": "http://localhost:6516/*",
                    "type": "Web"
            }
    ],
    ```
