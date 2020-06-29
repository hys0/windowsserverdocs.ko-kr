---
title: Windows Server Essentials에서 사용자 계정 관리
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 0d115697-532b-48c2-a659-9f889e235326
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 350c9aa4cf4a2e71f3a3b7600ec2acd9016fe50e
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470508"
---
# <a name="manage-user-accounts-in-windows-server-essentials"></a>Windows Server Essentials에서 사용자 계정 관리

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server Essentials 대시보드의 사용자 페이지에서는 소규모 기업 네트워크에서 사용자 계정 관리를 도와주는 정보와 작업을 중앙화합니다. 사용자 대시보드의 개요는 [대시보드 개요](Overview-of-the-Dashboard-in-Windows-Server-Essentials.md)를 참조 하세요.


##  <a name="managing-user-accounts"></a><a name="BKMK_ManageAccounts"></a>사용자 계정 관리
 다음 항목에서는 Windows Server Essentials 대시보드를 사용하여 서버에서 사용자 계정을 관리하는 방법을 설명합니다.

-   [사용자 계정 추가](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage1)

-   [사용자 계정 제거](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Remove)

-   [사용자 계정 보기](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage3)

-   [사용자 계정에 대한 표시 이름 변경](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage4)

-   [사용자 계정 활성화](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage5)

-   [사용자 계정 비활성화](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage6)

-   [사용자 계정 이해](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage7)

-   [대시보드를 사용하여 사용자 계정 관리](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage8)

###  <a name="add-a-user-account"></a><a name="BKMK_Manage1"></a>사용자 계정 추가
 사용자 계정을 추가하면 할당된 사용자가 네트워크에 로그온할 수 있고 사용자에게 공유 폴더 및 원격 웹 액세스 사이트와 같은 네트워크 리소스에 액세스할 권한을 제공할 수 있습니다. Windows Server Essentials에는 다음 작업을 도와주는 사용자 계정 추가 마법사가 포함되어 있습니다.

-   사용자 계정의 이름과 암호를 제공합니다.

-   계정을 관리자 또는 표준 사용자로 정의합니다.

-   사용자 계정이 액세스할 수 있는 공유 폴더를 선택합니다.

-   사용자 계정이 네트워크에 원격으로 액세스할 수 있는지를 지정합니다.

-   해당하는 경우 메일 옵션을 선택합니다.

-   해당 하는 경우 Microsoft Online Services 계정 (Windows Server Essentials에서 Office 365 계정 이라고 함)을 할당 합니다.

-   사용자 그룹을 할당 합니다 (Windows Server Essentials에만 해당).

> [!NOTE]
> - 비 ASCII 문자는 Microsoft Azure Active Directory (Azure AD)에서 지원 되지 않습니다. 서버를 Azure AD와 통합 하는 경우 암호에 ASCII가 아닌 문자를 사용 하지 마세요.
>   -   메일 서비스를 제공하는 추가 기능을 설치하면 메일 옵션만 사용할 수 있습니다.

##### <a name="to-add-a-user-account"></a>사용자 계정을 추가하려면

1.  Windows Server Essentials 대시보드를 엽니다.

2.  탐색 모음에서 **사용자**를 클릭합니다.

3.  **사용자 작업** 창에서 **사용자 계정 추가**를 클릭합니다. 사용자 계정 추가 마법사가 나타납니다.

4.  지시에 따라 마법사를 완료합니다.

###  <a name="remove-a-user-account"></a><a name="BKMK_Remove"></a>사용자 계정 제거
 서버에서 사용자 계정을 제거하도록 선택하면 선택한 계정이 삭제됩니다. 이 때문에 네트워크에 로그온하거나 네트워크 리소스에 액세스하는 데 더 이상 계정을 사용할 수 없습니다. 필요하면 계정을 제거하면서 사용자 계정에 대한 파일을 삭제할 수도 있습니다. 사용자 계정을 영구적으로 제거하지 않으려면 네트워크 리소스에 대한 액세스를 일시 중단하지 않고 사용자 계정을 비활성화할 수 있습니다.

> [!IMPORTANT]
>  사용자 계정에 Microsoft 온라인 계정이 할당 되어 있으면 사용자 계정을 제거할 때 온라인 계정도 Microsoft Online Services에서 제거 되 고 전자 메일을 포함 한 사용자의 데이터에는 Microsoft Online Services의 데이터 보존 정책이 적용 됩니다. 온라인 계정에 대한 사용자 데이터를 유지하려면 사용자 계정을 제거하는 대신 비활성화합니다. 자세한 내용은 [사용자에 대 한 온라인 계정 관리](Manage-Online-Accounts-for-Users.md)를 참조 하세요.

##### <a name="to-remove-a-user-account"></a>사용자 계정을 제거하려면

1.  Windows Server Essentials 대시보드를 엽니다.

2.  탐색 모음에서 **사용자**를 클릭합니다.

3.  사용자 계정 목록에서 제거하려는 사용자 계정을 선택합니다.

4.  **<사용자 계정 \> 작업** 창에서 **사용자 계정 제거**를 클릭 합니다. 사용자 계정 삭제 마법사가 나타납니다.

5.  마법사의 파일 **보관 여부 확인** 페이지에서 사용자 계정에 대 한 파일 히스토리 백업 및 리디렉션된 폴더를 포함 하 여 사용자 파일을 삭제 하도록 선택할 수 있습니다. 사용자의 파일을 유지 하려면 확인란을 비워 둡니다. 선택하고 나서 **다음**을 클릭합니다.

6.  **계정 삭제**를 클릭합니다.

> [!NOTE]
>  사용자 계정을 제거하고 나면 계정이 더 이상 사용자 계정 목록에 나타나지 않습니다. 파일을 삭제 하도록 선택 하면 **사용자 서버 폴더** 및 **파일 히스토리 백업** 서버 폴더에서 사용자 폴더가 영구적으로 삭제 됩니다.
>
>  통합된 메일 공급자가 있으면 사용자 계정에 할당된 메일 계정도 제거됩니다.

###  <a name="view-user-accounts"></a><a name="BKMK_Manage3"></a>사용자 계정 보기
 Windows Server Essentials 대시보드의 **사용자** 섹션에는 네트워크 사용자 계정 목록이 표시됩니다. 목록에서는 각 계정에 대한 추가 정보도 제공합니다.

##### <a name="to-view-a-list-of-user-accounts"></a>사용자 계정 목록을 보려면

1.  Windows Server Essentials 대시보드를 엽니다.

2.  기본 탐색 모음에서 **사용자**를 클릭합니다.

3.  대시보드에는 현재 사용자 계정 목록이 표시됩니다.

##### <a name="to-view-or-change-properties-for-a-user-account"></a>사용자 계정에 대한 속성을 보거나 변경하려면

1.  사용자 계정 목록에서 속성을 보거나 변경할 계정을 선택합니다.

2.  **<사용자 계정 \> 작업** 창에서 **계정 속성 보기**를 클릭 합니다. 사용자 계정에 대한 **속성** 페이지가 나타납니다.

3.  탭을 클릭하여 해당 계정 기능에 대한 속성을 표시합니다.

4.  사용자 계정 속성의 모든 변경 사항을 저장하려면 **적용**을 클릭합니다.

###  <a name="change-the-display-name-for-the-user-account"></a><a name="BKMK_Manage4"></a>사용자 계정에 대 한 표시 이름 변경
 표시 이름은 대시보드 **사용자** 페이지의 **이름** 열에 나타나는 이름입니다. 표시 이름을 변경해도 사용자 계정에 대한 로그온 또는 로그인 이름은 변경되지 않습니다.

##### <a name="to-change-the-display-name-for-a-user-account"></a>사용자 계정에 대한 표시 이름을 변경하려면

1.  Windows Server Essentials 대시보드를 엽니다.

2.  탐색 모음에서 **사용자**를 클릭합니다.

3.  사용자 계정 목록에서 변경하려는 사용자 계정을 선택합니다.

4.  **<사용자 계정 \> 작업** 창에서 **계정 속성 보기**를 클릭 합니다. 사용자 계정에 대한 **속성** 페이지가 나타납니다.

5.  **일반** 탭에서 사용자 계정에 대한 새 **이름** 및 **성**을 입력하고 **확인**을 클릭합니다.

     사용자 계정 목록에 새로운 표시 이름이 나타납니다.

###  <a name="activate-a-user-account"></a><a name="BKMK_Manage5"></a>사용자 계정 활성화
 사용자 계정을 활성화하면 할당된 사용자가 네트워크에 로그온하고 계정에 사용 권한이 있는 공유 폴더 및 원격 웹 액세스 사이트와 같은 네트워크 리소스에 액세스할 수 있습니다.

> [!NOTE]
>  비활성화된 사용자 계정만 활성화할 수 있습니다. 사용자 계정을 서버에서 제거하고 나면 활성화할 수 없습니다.

##### <a name="to-activate-a-user-account"></a>사용자 계정을 활성화하려면

1.  Windows Server Essentials 대시보드를 엽니다.

2.  탐색 모음에서 **사용자**를 클릭합니다.

3.  목록 뷰에서 활성화하려는 사용자 계정을 선택합니다.

4.  **<사용자 계정 \> 작업** 창에서 **사용자 계정 활성화**를 클릭 합니다.

5.  확인 창에서 **예**를 클릭하여 작업을 확인합니다.

> [!NOTE]
>  사용자 계정을 활성화하고 나면 계정에 대한 상태에 **활성**이 표시됩니다. 사용자 계정은 계정이 비활성화되기 전에 할당된 것과 같은 액세스 권한을 다시 얻습니다.
>
>  통합된 메일 공급자가 있으면 사용자 계정에 할당된 메일 계정도 활성화됩니다.

###  <a name="deactivate-a-user-account"></a><a name="BKMK_Manage6"></a>사용자 계정 비활성화
 사용자 계정을 비활성화하면 서버에 대한 계정 액세스가 일시적으로 중단됩니다. 이 때문에 할당된 사용자는 계정을 활성화할 때까지 공유 폴더 또는 원격 웹 액세스 사이트와 같은 네트워크 리소스에 액세스하는 데 해당 계정을 사용할 수 없습니다.

 사용자 계정에 Microsoft 온라인 계정이 할당되어 있으면 온라인 계정도 비활성화됩니다. 사용자는 Office 365의 리소스 및 구독 하는 다른 온라인 서비스를 사용할 수 없지만 전자 메일을 포함 한 사용자 데이터는 Microsoft Online Services에서 유지 됩니다.

> [!NOTE]
>  현재 활성 상태인 사용자 계정만 비활성화할 수 있습니다.

##### <a name="to-deactivate-a-user-account"></a>사용자 계정을 비활성화하려면

1.  Windows Server Essentials 대시보드를 엽니다.

2.  탐색 모음에서 **사용자**를 클릭합니다.

3.  목록 뷰에서 비활성화하려는 사용자 계정을 선택합니다.

4.  **<사용자 계정 \> 작업** 창에서 **사용자 계정 비활성화**를 클릭 합니다.

5.  확인 창에서 **예**를 클릭하여 작업을 확인합니다.

> [!NOTE]
>  사용자 계정을 비활성화하고 나면 계정에 대한 상태에 **비활성**이 표시됩니다.
>
>  통합된 메일 공급자가 있으면 사용자 계정에 할당된 메일 계정도 비활성화됩니다.

###  <a name="understand-user-accounts"></a><a name="BKMK_Manage7"></a>사용자 계정 이해
 사용자 계정은 개별 사용자가 서버에 저장된 정보에 액세스하는 데 사용되는 중요한 정보를 Windows Server Essentials에 제공하고 사용자 계정을 통해 개별 사용자가 파일과 설정을 만들고 관리할 수 있습니다. 사용자는 Windows Server Essentials 사용자 계정이 있고 컴퓨터에 액세스할 권한이 있으면 네트워크의 모든 컴퓨터에 로그온할 수 있습니다. 사용자는 사용자 이름과 암호를 사용하여 사용자 계정에 액세스합니다.

 사용자 계정에는 두 가지 기본 유형이 있습니다. 각 유형은 사용자에게 컴퓨터에 대한 서로 다른 수준의 제어 권한을 부여합니다.

-   **표준** 계정은 일상적인 작업에 사용합니다. 표준 계정을 통해 사용자가 파일 삭제 또는 네트워크 설정 변경 등 다른 사용자에게 영향을 미치는 변경 사항을 적용할 수 없도록 하여 네트워크를 보호할 수 있습니다.

-   **관리자** 계정을 사용하면 컴퓨터 네트워크를 가장 완벽하게 제어할 수 있습니다. 필요한 경우에만 관리자 계정 유형을 할당해야 합니다.

###  <a name="manage-user-accounts-using-the-dashboard"></a><a name="BKMK_Manage8"></a>대시보드를 사용 하 여 사용자 계정 관리
 Windows Server Essentials에서는 Windows Server Essentials 대시보드를 사용하여 일반적인 관리 작업을 수행할 수 있습니다. 기본적으로 대시보드의 **사용자** 페이지에는 **사용자** 및 **사용자 그룹**의 두 탭이 있습니다.

> [!NOTE]
> - Windows Server Essentials를 실행 하는 서버를 Office 365와 통합 하는 경우 **배포 그룹** 이라는 새 탭이 대시보드의 **사용자** 페이지에도 추가 됩니다.
>   -   Windows Server Essentials에서 대시보드의 **사용자** 페이지에는 단일 탭 **사용자**만 포함 됩니다.

 **사용자** 탭에는 다음이 포함됩니다.

- 다음을 표시하는 사용자 계정 목록:

  -   사용자의 이름입니다.

  -   사용자 계정의 로그온 이름.

  -   사용자 계정에 원격 액세스 권한이 있는지 여부. 사용자 계정에 대한 원격 액세스 권한은 **허용됨** 또는 **허용 안 함**입니다.

  -   이 사용자 계정에 대한 파일 히스토리가 Windows Server Essentials를 실행하는 서버에서 관리되는지 여부. 사용자 계정에 대한 파일 히스토리 상태는 **관리됨** 또는 **관리되지 않음**입니다.

  -   사용자 계정에 할당되는 액세스 수준. 사용자 계정에 대한 **표준 사용자** 액세스 또는 **관리자** 액세스 권한을 할당할 수 있습니다.

  -   사용자 계정 상태. 사용자 계정은 **활성**, **비활성** 또는 **완료 안 됨** 상태일 수 있습니다.

  -   Windows Server Essentials에서 서버가 Office 365 또는 Windows Intune과 통합 되어 있으면 Microsoft 온라인 계정이 표시 됩니다.

  -   Windows Server Essentials에서 서버가 Microsoft Office 365와 통합 된 경우 사용자 계정에 대 한 Office 365 계정 (Windows Server Essentials에서 Microsoft 온라인 계정으로 알려짐)의 상태가 표시 됩니다.

- 선택한 사용자 계정에 대한 추가 정보가 있는 세부 정보 창.

- 다음을 포함하는 작업 창:

  -   사용자 계정 보기 및 제거, 암호 변경과 같은 사용자 계정 관리 작업 집합.

  -   네트워크의 모든 사용자 계정에 대한 설정을 전역적으로 설정하거나 변경할 수 있는 작업.

  다음 표에서는 **사용자** 탭에서 사용할 수 있는 다양 한 사용자 계정 작업에 대해 설명 합니다. 일부 작업은 사용자 계정에 따라 달라 지 며, 목록에서 사용자 계정을 선택할 때만 표시 됩니다.

> [!NOTE]
>  Windows Server Essentials와 Office 365을 통합 하는 경우 추가 작업을 사용할 수 있게 됩니다. 자세한 내용은 [사용자에 대 한 온라인 계정 관리](Manage-Online-Accounts-for-Users.md)를 참조 하세요.

### <a name="user-account-tasks-in-the-dashboard"></a>대시보드의 사용자 계정 작업

|작업 이름|설명|
|---------------|-----------------|
|계정 속성 보기|선택한 사용자 계정의 속성을 확인 및 변경하고 계정에 대한 폴더 액세스 권한을 지정할 수 있습니다.|
|사용자 계정 비활성화|비활성화된 사용자 계정은 네트워크에 로그온하거나 공유 폴더 또는 프린터와 같은 네트워크 리소스에 액세스할 수 없습니다.|
|사용자 계정 활성화|활성화된 사용자 계정은 네트워크에 로그온하고 계정 권한에 정의된 대로 네트워크 리소스에 액세스할 수 있습니다.|
|사용자 계정 제거|선택한 사용자 계정을 제거할 수 있습니다.|
|사용자 계정 암호 변경|선택한 사용자 계정에 대한 네트워크 암호를 재설정할 수 있습니다.|
|사용자 계정 추가|표준 액세스 또는 관리자 액세스 권한이 있는 단일 사용자 계정을 새로 만들 수 있는 사용자 계정 추가 마법사를 시작합니다.|
|Microsoft 온라인 계정 할당|선택된 로컬 네트워크 사용자 계정에 Microsoft 온라인 계정을 추가합니다.<br /><br /> 이 작업은 서버가 Office 365와 같은 Microsoft 온라인 서비스와 통합되어 있을 때 표시됩니다.|
|Microsoft 온라인 계정 추가|로컬 네트워크 사용자 계정에 Microsoft 온라인 계정을 추가하고 연결합니다.<br /><br /> 이 작업은 서버가 Office 365와 같은 Microsoft 온라인 서비스와 통합되어 있을 때 표시됩니다.|
|암호 정책 설정|네트워크에 대한 암호 정책의 값을 변경할 수 있습니다.|
|Microsoft 온라인 계정 가져오기|Microsoft 온라인 서비스에서 로컬 네트워크로 계정을 대량으로 가져옵니다.<br /><br /> 이 작업은 서버가 Office 365와 같은 Microsoft 온라인 서비스와 통합되어 있을 때 표시됩니다.|
|새로 고침|사용자 탭을 새로 고칩니다.<br /><br /> 이 작업은 Windows Server Essentials에 적용 됩니다.|
|파일 히스토리 설정 변경|백업 빈도 또는 백업 기간 등의 파일 히스토리 설정을 변경할 수 있습니다.<br /><br /> 이 작업은 Windows Server Essentials에 적용 됩니다.|
|모든 원격 연결 내보내기|최근 30일 동안 발생한 서버에 대한 모든 원격 연결의 .CSV 형식 파일을 만듭니다.|

##  <a name="managing-passwords-and-access"></a><a name="BKMK_ManageAccess"></a>암호 및 액세스 관리
 다음 항목에서는 Windows Server Essentials 대시보드를 사용하여 서버에서 사용자 계정 암호와 공유 폴더에 대한 사용자 액세스 권한을 관리하는 방법을 설명합니다.

-   [사용자 계정에 대한 암호 변경 또는 다시 설정](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access1)

-   [암호 정책에 대해 알고 있어야 하는 내용](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access3)

-   [암호 정책 변경](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access4)

-   [공유 폴더에 대한 액세스 수준](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access5)

-   [제거된 사용자 계정에 대한 파일 액세스 권한 유지 및 관리](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access6)

-   [DSRM 암호를 네트워크 관리자 암호와 동기화](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access7)

-   [사용자 계정에 원격 데스크톱 권한 부여](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access8)

-   [사용자가 서버의 리소스에 액세스할 수 있도록 허용](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access9)

-   [사용자 계정의 원격 액세스 권한 변경](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access10)

-   [사용자 계정에 대한 가상 개인 네트워크 사용 권한 변경](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access11)

-   [사용자 계정에 대한 내부 공유 폴더 액세스 권한 변경](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access12)

-   [사용자 계정이 컴퓨터에 대한 원격 데스크톱 세션을 설정하도록 허용](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Access13)

###  <a name="change-or-reset-the-password-for-a-user-account"></a><a name="BKMK_Access1"></a>사용자 계정에 대 한 암호 변경 또는 다시 설정
 사용자 계정 암호를 변경하거나 다시 설정하려면 다음 단계를 수행합니다.

##### <a name="to-reset-the-password-for-a-user-account"></a>사용자 계정에 대한 암호를 다시 설정하려면

1. Windows Server Essentials 대시보드를 엽니다.

2. 탐색 모음에서 **사용자**를 클릭합니다.

3. 사용자 계정 목록에서 다시 설정하려는 사용자 계정을 선택합니다.

4. **<사용자 계정 \> 작업** 창에서 **사용자 계정 암호 변경**을 클릭 합니다. 사용자 계정 암호 변경 마법사가 나타납니다.

5. 사용자 계정에 대한 새 암호를 입력하고 암호를 다시 입력하여 확인합니다.

6. **암호 변경**을 클릭합니다.

7. 사용자에게 새 암호를 제공합니다.

   > [!IMPORTANT]
   > - 사용자 계정에 대한 암호 정책이 **암호 사용 기간 제한 없음**으로 설정되었으면 암호를 변경할 수 없습니다.
   >   -   비 ASCII 문자는 Azure AD에서 지원 되지 않습니다. 따라서 서버를 Azure AD와 통합 하는 경우 암호에 비 ASCII 문자를 사용 하지 마세요.
   >   -   Microsoft 온라인 계정 (Windows Server Essentials에서 Office 365 계정으로 알려짐)이 사용자에 게 할당 된 경우 암호는 온라인 계정 암호와 동기화 됩니다. 사용자는 새 암호를 사용하여 서버 또는 Office 365에 로그인합니다. 자세한 내용은 [사용자에 대 한 온라인 계정 관리](Manage-Online-Accounts-for-Users.md)를 참조 하세요.

###  <a name="what-you-should-know-about-password-policies"></a><a name="BKMK_Access3"></a>암호 정책에 대해 알아야 할 사항
 암호 정책은 사용자가 암호를 만들고 사용하는 방법을 정의하는 규칙 집합입니다. 정책을 사용하여 서버에 저장된 사용자 데이터와 기타 정보에 대한 무단 액세스를 방지할 수 있습니다. 암호 정책은 네트워크에 액세스하는 모든 사용자 계정에 적용됩니다.

 Windows Server Essentials 암호 정책은 다음과 같이 세 가지 기본 요소로 구성됩니다.

- **암호 길이**.  암호 길이가 길수록 암호가 더 안전합니다. 빈 암호는 안전하지 않습니다.

- **암호 복잡성**.  복잡한 암호에는 혼합된 대문자 및 소문자(a-z, A-Z), 기본 숫자(0-9), 알파벳이 아닌 기호(예: !,@,#,_,-)가 포함됩니다. 복잡한 암호를 사용하면 무단 액세스에 노출될 위험이 훨씬 더 적습니다. 사용자 이름, 생년월일 또는 기타 개인 정보를 포함하는 암호는 적절한 보안을 제공하지 않습니다.

- **암호 사용 기간**.  Windows Server Essentials에서는 사용자가 최소한 180 일에 한 번 암호를 변경해야 합니다. 필요하면 암호가 만료되지 않도록 선택할 수 있습니다.

  컴퓨터 네트워크에서 암호 정책을 더욱 손쉽게 구현할 수 있도록 Windows Server Essentials에서는 다음 4가지 미리 정의된 정책 프로필의 하나로 암호 정책을 설정하거나 변경할 수 있는 간단한 도구를 제공합니다.

- **약함**.  비어 두지만 않는다면 어떤 암호라도 사용자가 지정할 수 있습니다.

- **보통**.  이 암호에는 5자 이상이 포함되어야 합니다. 복잡한 암호는 필수가 아닙니다.

- **약간 강함**.  이 암호에는 문자, 숫자, 기호가 5자 이상 포함되어야 합니다.

- **강함**.  이 암호에는 문자, 숫자, 기호가 7자 이상 포함되어야 합니다. 이 암호는 매우 안전하지만 사용자가 기억하기 어려울 수 있습니다.

  > [!NOTE]
  >  암호는 사용자 이름이나 메일 주소를 포함할 수 없습니다.
  >
  >  Office 365와 통합하면 **강함** 암호 정책이 적용되고 다음 요구 사항을 포함하도록 정책이 업데이트됩니다.
  >
  > - 암호는 8 16 문자를 포함 해야 합니다.
  >   -   암호는 공백 또는 Office 365 메일 이름을 포함할 수 없습니다.

  기본적으로 서버를 설치하면 기본 암호 정책이 **강함** 옵션으로 설정됩니다.

###  <a name="change-the-password-policy"></a><a name="BKMK_Access4"></a>암호 정책 변경
 다음 절차에 따라 암호 정책을 미리 정의된 정책 프로필의 하나로 설정하거나 변경합니다.

##### <a name="to-change-the-password-policy"></a>암호 정책을 변경하려면

1.  Windows Server Essentials 대시보드를 열고 **사용자**를 클릭합니다.

2.  **사용자 작업** 창에서 **암호 정책 설정**을 클릭합니다.

3.  **암호 정책 변경** 화면에서 슬라이더를 이동하여 암호 강도 수준을 설정합니다.

     암호 강도를 **강함**으로 설정하는 것이 좋습니다.

    > [!NOTE]
    >  필요하면 **암호 사용 기간 제한 없음**을 선택할 수도 있습니다. 이 설정은 보안 수준이 낮으므로 권장되지 않습니다.

4.  **정책 변경**을 클릭합니다.

###  <a name="level-of-access-to-shared-folders"></a><a name="BKMK_Access5"></a>공유 폴더에 대 한 액세스 수준
 사용자가 필요한 작업을 수행할 수 있게 하는 가장 제한적인 사용 권한을 할당하는 것이 좋습니다.

 서버의 공유 폴더에 대한 세 가지 액세스 권한 설정을 사용할 수 있습니다.

-   **읽기/쓰기**.  사용자 계정 사용 권한이 공유 폴더에서 파일을 만들고 변경 및 삭제할 수 있게 하려면 이 설정을 선택합니다.

-   **읽기 전용**.  사용자 계정 사용 권한이 공유 폴더에서 파일을 읽을 수만 있게 하려면 이 설정을 선택합니다. 읽기 전용 액세스 권한이 있는 사용자 계정은 공유 폴더에서 파일을 만들거나 변경하거나 삭제할 수 없습니다.

-   **권한 없음**.  사용자 계정이 공유 폴더의 모든 파일에 액세스할 수 없게 하려면 이 설정을 선택합니다.

###  <a name="retain-and-manage-access-to-files-for-removed-user-accounts"></a><a name="BKMK_Access6"></a>제거 되는 사용자 계정에 대 한 파일 액세스 권한 유지 및 관리
 네트워크 관리자는 사용자 계정을 제거 하 고 나중에 사용할 수 있도록 사용자의 파일을 유지 하도록 선택할 수 있습니다. 이 시나리오에서 제거된 사용자 계정은 더 이상 네트워크에 로그인하는 데 사용되지 않지만, 이 사용자에 대한 파일은 공유 폴더에 저장되어 다른 사용자와 공유할 수 있습니다.

> [!IMPORTANT]
>  Microsoft 온라인 계정이 할당된 사용자 계정을 제거하면 온라인 계정도 제거되고 메일을 포함한 사용자 데이터에는 Microsoft Online Services의 데이터 보존 정책이 적용됩니다. 온라인 계정에 대한 사용자 데이터를 유지하려면 사용자 계정을 제거하지 않고 비활성화합니다. 자세한 내용은 [사용자에 대 한 온라인 계정 관리](Manage-Online-Accounts-for-Users.md)를 참조 하세요.

##### <a name="to-remove-a-user-account-but-retain-access-to-the-users-files"></a>사용자 계정을 제거 하지만 사용자 파일에 대 한 액세스 권한을 유지 하려면

1. Windows Server Essentials 대시보드를 엽니다.

2. 탐색 모음에서 **사용자**를 클릭합니다.

3. 사용자 계정 목록에서 제거하려는 사용자 계정을 선택합니다.

4. **<사용자 계정 \> 작업** 창에서 **사용자 계정 제거**를 클릭 합니다. 사용자 계정 삭제 마법사가 나타납니다.

5. **파일 보관 여부 확인** 페이지에서 **이 사용자 계정에 대한 파일 기록 백업 및 리디렉션된 폴더를 포함하는 파일 삭제** 확인란이 선택 취소되어 있는지 확인하고 **다음**을 클릭합니다.

    계정을 삭제하지만 파일이 유지됨을 경고하는 확인 페이지가 나타납니다.

6. **계정 삭제**를 클릭하여 사용자 계정을 제거합니다.

   사용자 계정이 제거되고 나면 관리자가 또 다른 사용자 계정에 공유 폴더에 대한 액세스 권한을 부여할 수 있습니다.

##### <a name="to-give-a-user-account-permission-to-access-a-shared-folder"></a>사용자 계정에 공유 폴더에 액세스할 수 있는 사용 권한을 부여하려면

1.  Windows Server Essentials 대시보드를 엽니다.

2.  탐색 모음에서 **스토리지**, **서버 폴더** 탭을 차례로 클릭합니다.

3.  폴더 목록에서 **사용자** 폴더를 선택합니다.

4.  **사용자 작업** 창에서 **폴더 열기**를 클릭합니다. Windows 탐색기가 열리고 **사용자** 폴더의 콘텐츠가 표시됩니다.

5.  공유할 사용자 계정 폴더를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.

6.  **<사용자 계정 \> 속성**에서 **공유** 탭을 클릭 한 다음 **공유**를 클릭 합니다.

7.  **파일 공유** 창에서 폴더를 함께 공유할 사용자 계정 이름을 입력하거나 선택하고 **추가**를 클릭합니다.

8.  사용자 계정에 포함할 **사용 권한 수준**을 선택하고 **공유**를 클릭합니다.

###  <a name="synchronize-the-dsrm-password-with-the-network-administrator-password"></a><a name="BKMK_Access7"></a>DSRM 암호를 네트워크 관리자 암호와 동기화
 DSRM(디렉터리 서비스 복원 모드)은 Active Directory를 복구하기 위한 특수 부팅 모드입니다. Active Directory가 실패하거나 복원되어야 하면 운영 체제에서는 DSRM을 사용하여 컴퓨터에 로그온합니다. 네트워크 관리자 암호와 DSRM 암호가 다르면 DSRM이 로드되지 않습니다.

 Windows Server Essentials을 처음 새로 설치하는 동안 프로그램에서는 설정 중에 지정하거나 마이그레이션 응답 파일에서 지정한 네트워크 관리자 계정 암호로 DSRM 암호를 설정합니다. (권장된 대로 서버 보안 강화를 위해 일반적으로 60일마다) 네트워크 관리자 암호를 변경해도 암호 변경이 DSRM에 전달되지 않습니다. 이 때문에 암호가 일치하지 않습니다. 이 경우 다음 해결 방법을 사용 하 여 네트워크 관리자 암호를 DSRM 암호와 수동으로 또는 자동으로 동기화 할 수 있습니다.

##### <a name="to-manually-synchronize-the-dsrm-password-to-a-network-administrator-account"></a>DSRM 암호를 네트워크 관리자 계정에 수동으로 동기화하려면

1. 명령 프롬프트에서 `ntdsutil.exe` 를 실행하여 ntdsutil 도구를 엽니다.

2. DSRM 암호를 다시 설정하려면 **set dsrm password**를 입력합니다.

3. 도메인 컨트롤러에서 DSRM 암호를 현재 네트워크 관리자 계정과 동기화 하려면 다음을 입력 합니다.

    **도메인 계정에서 동기화** *<current_network_administrator_account>* 한 다음 enter 키를 누릅니다.

   네트워크 관리자 계정의 암호를 정기적으로 변경하게 되므로 DSRM 암호가 항상 네트워크 관리자의 현재 암호와 동일하게 하려면 매일 DSRM 암호를 네트워크 관리자 암호에 자동으로 동기화하는 일정 작업을 만드는 것이 좋습니다.

##### <a name="to-automatically-synchronize-the-dsrm-password-to-a-network-administrator-account"></a>DSRM 암호를 네트워크 관리자 계정에 자동으로 동기화하려면

1.  서버에서 **관리 도구**를 열고 **작업 Scheduler**를 두 번 클릭합니다.

2.  작업 Scheduler **작업** 창에서 **작업 만들기**를 클릭합니다.

3.  **이름** 텍스트 상자에 작업 이름(예: **AutoSync DSRM Password**)을 입력하고 **가장 높은 수준의 권한으로 실행** 옵션을 선택합니다.

4.  작업 실행 시기를 정의합니다.

    1.  **작업 만들기** 대화 상자에서 **트리거** 탭, **새로 만들기**를 차례로 클릭합니다.

    2.  **새 트리거** 대화 상자에서 되풀이 옵션을 선택하고 되풀이 간격을 지정하고 시작 시간을 선택합니다.

        > [!NOTE]
        >  매일 업무 시간 이외의 시간에 작업을 실행하도록 설정하는 것이 좋습니다.

    3.  **확인**을 클릭하여 변경 내용을 저장하고 **작업 만들기** 대화 상자로 돌아갑니다.

5.  작업 동작을 정의합니다.

    1.  **작업** 탭, **새로 만들기**를 차례로 클릭합니다. **새 작업** 대화 상자가 나타납니다.

    2.  **작업** 목록에서 **프로그램 시작**을 클릭하고 **C:\WINDOWS\SYSTEM32\ntdsutil.exe**로 이동합니다.

    3.  **인수 추가**(선택 사항) 텍스트 상자에 다음을 입력 합니다. (인용 부호를 포함 해야 함) **도메인 계정에서 dsrm 암호 동기화를 설정 SBS_network_administrator_account q q에서** *SBS_network_administrator_account* 현재 네트워크 관리자의 계정 이름입니다.

6.  **확인**을 두 번 클릭하여 작업을 저장하고 **작업 만들기** 대화 상자를 닫습니다. 새 작업이 **작업 일정**의 **활성 작업** 섹션에 나타납니다.

###  <a name="give-user-accounts-remote-desktop-permission"></a><a name="BKMK_Access8"></a>사용자 계정에 원격 데스크톱 권한 부여
 Windows Server Essentials의 기본 설치에서 네트워크 사용자는 네트워크의 컴퓨터 또는 기타 리소스에 대한 원격 연결을 설정할 권한이 없습니다.

 네트워크 사용자가 네트워크 리소스에 대한 원격 연결을 설정할 수 있으려면 먼저 원격 액세스를 설정해야 합니다. 원격 액세스를 설정하고 나면 사용자가 인터넷 연결을 통해 위치에 관계없이 디바이스에서 사무실 네트워크의 파일, 애플리케이션 및 컴퓨터에 액세스할 수 있습니다.

 원격 액세스 설정 마법사에서는 두 가지 방법으로 원격 액세스를 수행할 수 있습니다.

- VPN(가상 프라이빗 네트워크)

- 원격 웹 액세스

  마법사를 실행하면 모든 현재 및 새로 추가된 사용자 계정에 대한 원격 액세스를 허용하도록 선택할 수 있습니다.

  원격 액세스를 설정하려면 대시보드 **홈** 페이지를 열고 **설정**, **원격 액세스 설정**을 차례로 클릭합니다.

  원격 액세스에 대 한 자세한 내용은 [원격 액세스 관리](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)를 참조 하세요.

###  <a name="enable-users-to-access-resources-on-the-server"></a><a name="BKMK_Access9"></a>사용자가 서버의 리소스에 액세스할 수 있도록 설정
  이 섹션은 windows server essentials 또는 Windows Server Essentials를 실행 하는 서버 또는 windows Server Essentials Experience 역할이 설치 된 windows Server 2012 R2 Standard 또는 Windows Server 2012 R2 Datacenter를 실행 하는 서버에 적용 됩니다.

 사용자가 원격 액세스를 사용하고 개별 사용자 계정을 보유하도록 하려면 컴퓨터를 서버에 연결하고 나서 대시보드를 사용하여 서버에서 네트워크로 연결된 컴퓨터 사용자에 대한 새 네트워크 사용자 계정을 만들 수 있습니다. 사용자 계정을 만드는 방법에 대한 자세한 내용은 [사용자 계정 추가](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage1)를 참조하세요. 사용자 계정을 만들고 나서 클라이언트 컴퓨터의 사용자가 실행 패드를 사용하여 서버의 리소스에 액세스할 수 있도록 해당 사용자에게 네트워크 사용자 이름 및 암호 정보를 제공해야 합니다.

 생성된 각 사용자 계정에 대해 사용자 계정 속성을 통해 다음에 대한 액세스 권한을 설정할 수 있습니다.

-   **공유 폴더**.  기본적으로 네트워크 관리자는 모든 공유 폴더에 대한 **읽기/쓰기** 권한을 보유하고 표준 사용자 계정은 회사 폴더에 대한 **읽기 전용** 권한을 보유합니다. 미디어 스트리밍이 사용되면 다음 공유 폴더에 대해 개별 표준 사용자 계정의 폴더 액세스 권한을 할당할 수 있습니다. **음악**, **사진**, **녹화된 TV**및 **동영상**. 사용자 계정 속성의 **공유 폴더** 탭에서 사용자 계정이 공유 폴더에 액세스하는 데 필요한 사용 권한을 설정할 수 있습니다.

-   **원격 액세스**.  기본적으로 네트워크 관리자는 VPN 또는 원격 웹 액세스를 사용하여 서버 리소스에 액세스할 수 있습니다. 표준 사용자 계정의 경우 **원격 액세스** 탭에서 사용자 계정 사용 권한을 설정해야 합니다.

-   **컴퓨터 액세스**.  기본적으로 네트워크 관리자는 네트워크의 모든 컴퓨터에 액세스할 수 있습니다. 그러나 표준 사용자 계정의 경우 사용자 계정 속성의 **컴퓨터 액세스** 탭에서 네트워크의 컴퓨터에 액세스하는 데 필요한 개별 사용자 계정 사용 권한을 설정할 수 있습니다.

##### <a name="to-edit-user-account-properties-in-windows-server-essentials-2012-r2"></a>Windows Server Essentials 2012 R2에서 사용자 계정 속성을 편집하려면

1.  Windows Server Essentials 대시보드를 엽니다.

2.  탐색 모음에서 **사용자**를 클릭합니다.

3.  사용자 계정 목록에서 편집하려는 사용자 계정을 선택합니다.

4.  **<사용자 계정 \> 작업** 창에서 **계정 속성 보기**를 클릭 합니다.

5.  **<사용자 계정 \> 속성**에서 다음을 수행 합니다.

    1.  **공유 폴더** 탭에서 필요에 따라 각 공유 폴더에 대한 적절한 폴더 사용 권한을 설정합니다.

    2.  **원격 액세스** 탭에서:

        1.  사용자가 VPN을 사용하여 서버에 연결할 수 있게 하려면 **VPN(가상 사설망) 허용** 확인란을 선택합니다.

        2.  사용자가 원격 웹 액세스를 사용하여 서버에 연결할 수 있게 하려면 **원격 웹 액세스 허용 및 웹 서비스 응용 프로그램에 액세스** 확인란을 선택합니다.

    3.  **컴퓨터 액세스** 탭에서 사용자에게 액세스를 허용할 네트워크 컴퓨터를 선택합니다.

##### <a name="to-edit-user-account-properties-in-windows-server-essentials-2012"></a>Windows Server Essentials 2012에서 사용자 계정 속성을 편집하려면

1.  Windows Server Essentials 대시보드를 엽니다.

2.  탐색 모음에서 **사용자**를 클릭합니다.

3.  사용자 계정 목록에서 편집하려는 사용자 계정을 선택합니다.

4.  **사용자 계정 \> 작업<** 창에서 **속성**을 클릭 합니다.

5.  **<사용자 계정 \> 속성**에서 다음을 수행 합니다.

    1.  사용자 계정이 네트워크 상태 보고서에 액세스해야 하면 **일반** 탭에서 **네트워크 상태 경고를 볼 수 있음**을 선택합니다.

    2.  **공유 폴더** 탭에서 필요에 따라 각 공유 폴더에 대한 적절한 폴더 사용 권한을 설정합니다.

    3.  **원격 액세스** 탭에서:

        1.  사용자가 VPN을 사용하여 서버에 연결할 수 있게 하려면 **VPN(가상 사설망) 허용** 확인란을 선택합니다.

        2.  사용자가 원격 웹 액세스를 사용하여 서버에 연결할 수 있게 하려면 **원격 웹 액세스 허용 및 웹 서비스 응용 프로그램에 액세스** 확인란을 선택합니다.

    4.  **컴퓨터 액세스** 탭에서 사용자에게 액세스를 허용할 네트워크 컴퓨터를 선택합니다.

###  <a name="change-remote-access-permissions-for-a-user-account"></a><a name="BKMK_Access10"></a>사용자 계정에 대 한 원격 액세스 권한 변경
 사용자는 VPN(가상 사설망), 원격 웹 액세스 또는 기타 웹 서비스 애플리케이션을 사용하여 원격 위치에서 서버에 있는 리소스에 액세스할 수 있습니다. 기본적으로 원격 액세스 권한은 대시보드를 사용하여 Windows Server Essentials에서 원격 액세스를 구성할 때 네트워크 사용자에 대해 켜집니다.

##### <a name="to-change-remote-access-permissions-for-a-user-account"></a>사용자 계정에 대한 원격 액세스 권한을 변경하려면

1.  Windows Server Essentials 대시보드를 엽니다.

2.  탐색 모음에서 **사용자**를 클릭합니다.

3.  사용자 계정 목록에서 변경하려는 사용자 계정을 선택합니다.

4.  **<사용자 계정 \> 작업** 창에서 **계정 속성 보기**를 클릭 합니다. 사용자 계정에 대한 **속성** 페이지가 나타납니다.

5.  **원격 액세스** 탭에서 다음을 수행합니다.

    -   **VPN(가상 사설망) 허용** 확인란을 선택하여 사용자가 VPN을 사용하여 서버에 연결할 수 있도록 합니다.

    -   **원격 웹 액세스 허용 및 웹 서비스 응용 프로그램에 액세스** 확인란을 선택하여 사용자가 원격 웹 액세스를 사용하여 서버에 연결할 수 있도록 합니다.

6.  **적용**, **확인**을 차례로 클릭합니다.

###  <a name="change-virtual-private-network-permissions-for-a-user-account"></a><a name="BKMK_Access11"></a>사용자 계정에 대 한 가상 개인 네트워크 사용 권한 변경
 VPN(가상 사설망)을 사용하여 Windows Server Essentials에 연결하고 서버에 저장된 모든 리소스에 액세스할 수 있습니다. 이 기능은 특히 VPN 연결을 통해 호스트된 Windows Server Essentials 서버에 연결하는 데 사용할 수 있는 네트워크 계정으로 설정되는 클라이언트 컴퓨터가 있는 경우 유용합니다. 호스트된 Windows Server Essentials 서버에서 새로 만든 모든 사용자 계정은 처음에 VPN을 사용하여 클라이언트 컴퓨터에 로그온해야 합니다.

##### <a name="to-change-vpn-permissions-for-network-users"></a>네트워크 사용자에 대한 VPN 사용 권한을 변경하려면

1.  Windows Server Essentials 대시보드를 엽니다.

2.  탐색 모음에서 **사용자**를 클릭합니다.

3.  사용자 계정 목록에서 데스크톱에 원격으로 액세스할 수 있는 사용 권한을 부여할 사용자 계정을 선택합니다.

4.  **사용자 계정 \> 작업<** 창에서 **속성**을 클릭 합니다.

5.  **<사용자 계정 \> 속성**에서 **원격 액세스** 탭을 클릭 합니다.

6.  **원격 액세스** 탭에서 사용자가 VPN을 사용하여 서버에 연결할 수 있게 하려면 **VPN(가상 사설망) 허용** 확인란을 선택합니다.

7.  **적용**, **확인**을 차례로 클릭합니다.

###  <a name="change-access-to-internal-shared-folders-for-a-user-account"></a><a name="BKMK_Access12"></a>사용자 계정에 대 한 내부 공유 폴더에 대 한 액세스 변경
 대시보드의 **서버 폴더** 탭에 있는 작업을 사용하여 서버에 있는 모든 공유 폴더에 대한 액세스 권한을 관리할 수 있습니다. 기본적으로 Windows Server Essentials를 설치할 때 다음 서버 폴더가 생성됩니다.

-   **클라이언트 컴퓨터 백업**.  Windows Server 백업에서 생성된 클라이언트 컴퓨터 백업을 저장하는 데 사용됩니다. 이 서버 폴더는 공유되지 않습니다.

-   **회사**.  네트워크 사용자가 조직에 관련된 문서를 저장하고 액세스하는 데 사용됩니다.

-   **파일 히스토리 백업**.  기본적으로 Windows Server Essentials에서는 파일 히스토리를 사용하여 생성된 파일 백업을 저장합니다. 이 서버 폴더는 공유되지 않습니다.

-   **폴더 리디렉션**.  네트워크 사용자가 폴더 리디렉션을 위해 설정된 폴더를 저장하고 액세스하는 데 사용됩니다. 이 서버 폴더는 공유되지 않습니다.

-   **음악**.  네트워크 사용자가 음악 파일을 저장하고 액세스하는 데 사용됩니다. 이 폴더는 미디어 공유를 켤 때 생성됩니다.

-   **사진**.  네트워크 사용자가 사진을 저장하고 액세스하는 데 사용됩니다. 이 폴더는 미디어 공유를 켤 때 생성됩니다.

-   **녹화된 TV**.  네트워크 사용자가 녹화된 TV 프로그램을 저장하고 액세스하는 데 사용됩니다. 이 폴더는 미디어 공유를 켤 때 생성됩니다.

-   **동영상**.  네트워크 사용자가 동영상을 저장하고 액세스하는 데 사용됩니다. 이 폴더는 미디어 공유를 켤 때 생성됩니다.

-   **사용자**.  네트워크 사용자가 파일을 저장하고 액세스하는 데 사용됩니다. 사용자 특정 폴더는 관리자가 만드는 모든 네트워크 사용자 계정에 대한 **사용자** 서버 폴더에서 자동으로 생성됩니다.

##### <a name="to-change-access-to-a-shared-folder-for-a-user-account"></a>사용자 계정에 대한 공유 폴더 액세스 권한을 변경하려면

1.  Windows Server Essentials 대시보드를 엽니다.

2.  **저장소**, **서버 폴더**를 차례로 클릭합니다.

3.  사용 권한을 수정할 서버 폴더로 이동하여 폴더를 선택합니다.

4.  작업 창에서 **폴더 속성 보기**를 클릭합니다.

5.  **<FolderName \> 속성**에서 **공유**를 클릭 하 고 나열 된 사용자 계정에 대 한 적절 한 사용자 액세스 수준을 선택한 다음 **적용**을 클릭 합니다.

    > [!NOTE]
    >  **파일 히스토리 백업**, **폴더 리디렉션** 및 **사용자** 서버 폴더에 대한 공유 권한은 수정할 수 없습니다. 또한 이러한 서버 폴더의 폴더 속성에는 **공유** 탭이 포함되지 않습니다.

###  <a name="allow-user-accounts-to-establish-a-remote-desktop-session-to-their-computer"></a><a name="BKMK_Access13"></a>사용자 계정이 컴퓨터에 대 한 원격 데스크톱 세션을 설정 하도록 허용
  이 섹션은 windows server essentials 또는 Windows Server Essentials를 실행 하는 서버 또는 windows Server Essentials Experience 역할이 설치 된 windows Server 2012 R2 Standard 또는 Windows Server 2012 R2 Datacenter를 실행 하는 서버에 적용 됩니다.

 네트워크 관리자는 원격 위치에서 네트워크 컴퓨터에 액세스할 수 있게 하는 사용 권한을 네트워크 사용자에게 부여할 수 있습니다.

##### <a name="to-enable-users-to-access-their-network-computers-from-a-remote-location"></a>사용자가 원격 위치에서 네트워크 컴퓨터에 액세스할 수 있게 하려면

1.  Windows Server Essentials 대시보드를 엽니다.

2.  탐색 모음에서 **사용자**를 클릭합니다.

3.  사용자 계정 목록에서 데스크톱에 원격으로 액세스할 수 있는 사용 권한을 부여할 사용자 계정을 선택합니다.

4.  **사용자 계정 \> 작업<** 창에서 **속성**을 클릭 합니다.

5.  **<사용자 계정 \> 속성**에서 **컴퓨터 액세스** 탭을 클릭 합니다.

6.  이 사용자 계정으로 원격으로 액세스할 컴퓨터를 선택하고 **확인**을 클릭합니다.

## <a name="additional-references"></a>추가 참조

-   [사용자에 대한 온라인 계정 관리](Manage-Online-Accounts-for-Users.md)

-   [연결](../use/Get-Connected-in-Windows-Server-Essentials.md)

-   [Windows Server Essentials 사용](../use/Use-Windows-Server-Essentials.md)

-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)
