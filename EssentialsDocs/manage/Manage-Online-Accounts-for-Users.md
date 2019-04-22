---
title: Windows Server Essentials 사용자에 대한 온라인 계정 관리
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c09f4cf6-4d12-49fe-9ae4-e6cb14027b9d
8author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 95f401bbec9bb503d19e2d9918a05851c04f7ef4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824094"
---
# <a name="manage-online-accounts-for-windows-server-essentials-users"></a>Windows Server Essentials 사용자에 대한 온라인 계정 관리

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server Essentials 서버에 Microsoft Office 365와 통합 하면 대시보드에서 온라인 계정과 사용자 계정 함께 관리할 수 있습니다. 이 항목에서는 초보 대시보드에서 사용자가 Microsoft Online Services 계정을 관리 하 여 얻을 수 있는 이점, 만들기 및 대시보드에서 온라인 계정을 관리 하는 방법 및 Exchange Online에 대 한 전자 메일 주소 및 메일 그룹을 관리 하는 방법 확인 대시보드로 돌아갑니다.  

  
> [!NOTE]
>  Windows Server Essentials에서 Microsoft Online Services 계정 관리, Office 365를 사용 하 여 서버를 통합 해야 합니다. 자세한 내용은 [Office 365 관리](Manage-Office-365-in-Windows-Server-Essentials.md)합니다.  
  
> [!IMPORTANT]
>  경우를 Windows Server Essentials에서 온라인 계정을 관리 하에 익숙해져 라고 Microsoft Online Services 계정을 보는 *Office 365 계정*합니다. In Windows Server Essentials 대시보드에서 레이블을 하도록 변경 되었습니다 *Microsoft Online Services 계정을*, 또는 *Microsoft 온라인 계정* 짧은 이름입니다. 계정 및 절차는 동일하고 레이블만 변경되었습니다. 이 항목의 대부분 절차에서는 *온라인 계정*이라는 용어를 사용합니다.  
  
## <a name="in-this-topic"></a>이 항목의 내용  
  
-   [대시보드에서 온라인 계정을 관리 해야는 이유](#BKMK_WhyManageOnlineAccounts)  
  
-   [온라인 계정 만들기](#BKMK_SECTION_CreateOnlineAccounts)  
  
-   [온라인 계정 관리](#BKMK_SECTION_ManageOnlineAccounts)  
  
-   [Exchange Online에 대 한 전자 메일 주소를 관리 합니다.](#BKMK_SECTION_ManageEmailAddresses)  
  
-   [Exchange Online에 대 한 메일 그룹 관리](#BKMK_SECTION_ManageDistributionGroups)  
  
##  <a name="BKMK_WhyManageOnlineAccounts"></a> 대시보드에서 온라인 계정을 관리 해야는 이유  
 대시보드를 사용 하 여 Microsoft Online Services 계정을 사용자 계정에 할당 하려면 계정 암호를 자동으로 동기화 된 시간과 함께 사용자 계정 s 수명 주기 내내 두 계정을 유지 관리할 수 있습니다.  
  
 이 s 서버 및 Office 365 리소스에 액세스할 때도 동일한 암호를 사용할 수 있는 사용자에 게 편리한 기능입니다. 있으며 사내 리소스에 필요한 Office 365의 리소스는 액세스를 위해 동일한 암호 요구 사항을 적용할 수 있습니다.  
  
### <a name="how-does-password-synchronization-work"></a>암호 동기화의 작동 원리  
 Microsoft Online Services 계정을 사용자 계정에 할당 하려면 대시보드를 사용 하는 경우 사용자 계정 암호를 사용자가 온라인 계정으로 자동으로 동기화 됩니다. 이 사용자는 서버 및 Office 365에서 두 리소스에 액세스 하는 데 단일 암호만 필요 함을 의미 합니다. 사용자 계정 및 사용자가 온라인 ID에 동일한 이름을 사용할 수는 또한  
  
 도메인에 연결된 컴퓨터나 원격 웹 액세스를 사용하여 사용자 계정의 암호를 변경하면 암호가 즉시 자동으로 동기화됩니다.  
  
> [!IMPORTANT]
>  Windows Server Essentials와 Office 365와 통합 하는 경우 사용자는 Office 365 포털에서 해당 Microsoft 온라인 계정의 암호를 변경 하지 않아야. 암호를 변경하면 암호 동기화가 중단됩니다.  
  
### <a name="simplified-account-creation"></a>간단한 계정 만들기  
 여기가 또 다른 이점은 대시보드에서 초기 온라인 계정을 만들 때. 단일 작업으로 모든 사용자에 대한 온라인 계정을 만들 수 있습니다. 반면, 직원 들에 게 Office 365를 이미 사용 중인를 새 Windows Server Essentials 서버를 설정 하면 만들 수 있습니다 사용자 계정의 모든 단일 작업으로 온라인 계정에서. 자세한 내용은 [온라인 계정 만들기](#BKMK_SECTION_CreateOnlineAccounts)를 참조하세요.  
  
### <a name="manage-email-addresses-and-distribution-groups-from-the-dashboard"></a>대시보드에서 메일 주소 및 메일 그룹 관리  
 대시보드에서 Exchange Online에 대한 전자 메일 주소 및 메일 그룹을 관리할 수 있습니다. 및 전자 메일 주소에서 조직의의 인터넷 도메인을 사용할 수 있습니다. 없이 수행할 수 있습니다이 모든 대시보드에서 Office 365에 로그인 합니다. (Windows Server Essentials 대시보드에서 메일 그룹 관리를 사용 하면 ll 필요 합니다. 이 기능은 지원 되지 않습니다 Windows Server Essentials에서.) 자세한 내용은 [Exchange Online에 대한 전자 메일 주소 관리](#BKMK_SECTION_ManageEmailAddresses) 및 [Exchange Online에 대한 메일 그룹 관리](#BKMK_SECTION_ManageDistributionGroups)를 참조하세요.  
  
### <a name="manage-the-user-account-and-online-account-together"></a>사용자 계정 및 온라인 계정을 함께 관리  
 및 계정 s 수명 주기 내내 사용자 계정과 함께 온라인 계정을 관리할 수 있습니다. 사용자 계정을 비활성화하면 Microsoft Online Services에서 온라인 계정도 비활성화됩니다. 사용자 계정을 제거하면 온라인 계정도 제거됩니다. 자세한 내용은 [온라인 계정 관리](#BKMK_SECTION_ManageOnlineAccounts)를 참조하세요.  
  
##  <a name="BKMK_SECTION_CreateOnlineAccounts"></a> 온라인 계정 만들기  
 Office 365와 서버를 통합 한 후이 대시보드에서 사용자에 대 한 Microsoft Online Services 만들려면 이점이 s 계정. 초보 온라인 계정 만들기의 다양 한 경우 새 Office 365 구독을 사용 하는 경우 대량으로 만들 수 있습니다 온라인 계정의 모든 사용자에 대 한 합니다. Office 365에서 온라인 계정을 이미 만든 경우 걱정 하지. 새 서버를 설정, 있습니다 만들 수 있는 경우 사용자 계정을 서버에서 온라인 계정을 가져와서 합니다. 및는 개별 사용자 계정을 만들 때 또는 기존 사용자 계정에 온라인 계정을 추가 하는 경우 새 또는 기존 온라인 계정을 할당할 수 있습니다.  
  
 **라이선스 요구 사항** 는 사용자가 만든 각 온라인 계정에 대 한 사용자 라이선스가 필요 합니다. 확인 합니다 **Office 365** Office 365 구독을 통해 사용할 수 있는 사용자 라이선스 수를 확인 하려면 대시보드에서 페이지입니다. 사용자 라이선스를 더 추가 해야 할 경우 초보 수 작업을 수행 하는 Office 365의 Office 365 구독을 엽니다.  
  
 **사용자에 대 한 후속** 사용자 계정에 대 한 온라인 계정에 추가한 후 사용자는 다음에 로그인 할 때 사용자 계정의 암호를 변경 하려면 필요 합니다. 새 암호는 즉시 온라인 계정과 동기화됩니다. 그 후 온라인 ID 사용 하 여 Office 365에 로그인 할 암호를 사용할 수 있습니다.  
  
> [!IMPORTANT]
>  Office 365에서 온라인 계정 암호가 변경 되지 해야 사용자에 게 강조 합니다. 이 암호는 사용자 계정의 암호를 변경할 때마다 자동으로 변경됩니다. Office 365에서 온라인 암호를 변경 하면 암호 동기화가 중단 됩니다.  
  
 이 섹션의 절차를 사용하여 다음을 수행합니다.  
  
-   [기존 사용자 계정에 대 한 온라인 계정을 일괄적으로 만들](#BKMK_ToBulkCreateOnlineAccounts)  
  
-   [Microsoft Online Services 계정에서 사용자 계정 가져오기](#BKMK_ToImportUserAccounts)  
  
-   [온라인 계정이 할당 된 새 사용자 계정 만들기](#BKMK_ToCreateaNewUserAccount)  
  
-   [사용자 계정에 온라인 계정을 할당합니다](#BKMK_ToAssignAnOnlineAccount)  
  
> [!NOTE]
>  표시를 Windows Server Essentials를 사용 하 여 *Office 365 계정* of *Microsoft Online Services 계정* 이러한 절차에서 내내 합니다. 프로세스는 동일 하지만 Windows Server Essentials에서 용어가 변경 되었습니다.  
  
###  <a name="BKMK_ToBulkCreateOnlineAccounts"></a> 기존 사용자 계정에 대 한 온라인 계정을 일괄적으로 만들려면  
  
1.  관리자로 서버에 로그인 하 고 Windows Server Essentials 대시보드를 엽니다.  
  
2.  대시보드에서 **사용자** 페이지를 엽니다.  
  
3.  **사용자 작업**에서 **Microsoft 온라인 계정 추가**를 클릭합니다.  
  
     마법사의 **Microsoft Online Services 계정 추가** 페이지에는 Microsoft 온라인 계정이 없는 모든 사용자 계정이 표시됩니다. 모든 계정이 기본적으로 선택되고 Microsoft 온라인 ID에 대한 사용자 이름이 제안됩니다. Office 365 구독에 사용자 지정 인터넷 도메인을 연결한 경우 해당 도메인이 기본적으로 사용 됩니다.  
  
4.  **Microsoft Online Services 계정 추가** 페이지에서 만들어질 계정을 검토합니다. 예를 들어 다른 온라인 ID가 포함된 온라인 계정을 보유한 사용자가 있는지 확인하고 메일 주소에서 사용할 도메인이 선택되었는지 확인합니다. 필요한 변경 작업을 마치면 **다음**을 클릭합니다.  
  
5.  에 **할당 Microsoft Online Services 라이선스** 페이지, 사용자가 사용 하 여 Office 365 서비스를 선택 합니다. **다음**을 클릭하면 계정 만들기가 시작됩니다.  
  
    > [!NOTE]
    >  각 온라인 계정에 대 한 Office 365에서 서비스 라이선스가 있어야 합니다. 사용할 수 있는 라이선스를 확인하고 필요하면 대시보드의 **Office 365** 페이지에서 구독을 열어 라이선스를 추가합니다.  
  
6.  이제 사용자에게 Microsoft 온라인 계정을 보유하게 되었음을 알립니다. Office 365에 로그인 할 수 전에 네트워크 사용자 계정 암호를 변경 해야 있습니다. 자세한 내용은 [새 Microsoft 온라인 계정 사용을 시작하려면](#BKMK_ToBeginUsingAnOnlineAccount)을 참조하세요.  
  
###  <a name="BKMK_ToBeginUsingAnOnlineAccount"></a> 새 Microsoft 온라인 계정 사용을 시작 하려면  
  
1.  네트워크 사용자 계정으로 컴퓨터에 로그인합니다.  
  
2.  사용자 계정의 암호를 변경합니다. 시작하려면 Ctrl+Alt+Delete를 누르고 **암호 변경**을 클릭합니다.  
  
     암호를 변경하면 암호가 새 온라인 계정과 동기화됩니다. 이제 Office 365에 로그인 하려면 동일한 암호를 사용할 수 있습니다.  
  
3.  새 온라인 ID 및 사용자 계정 암호를 사용하여[Office 365에 로그인](https://login.microsoftonline.com/login.srf?wa=wsignin1.0&rpsnv=3&ct=1398981834&rver=6.1.6206.0&wp=MBI_SSL&wreply=https:%2F%2Foutlook.office365.com%2Fowa%2F&id=260563&CBCXT=out) 합니다.  
  
    > [!IMPORTANT]
    >  Office 365에서 온라인 계정 암호를 변경 하지 마십시오. 온라인 암호를 변경하면 암호 동기화가 중단됩니다. 온라인 암호는 네트워크 사용자 계정의 암호를 변경할 때마다 업데이트됩니다.  
  
###  <a name="BKMK_ToImportUserAccounts"></a> 기존 온라인 계정에서 사용자 계정을 가져오려면  
  
1.  대시보드에서 **사용자** 페이지를 엽니다.  
  
2.  **사용자 작업**에서 **Office 365에서 계정 가져오기**를 클릭합니다.  
  
     다음 페이지에는 서버에 사용자 계정이 없는 Office 365 구독에 대 한 모든 온라인 계정이 표시 됩니다. 모든 계정이 기본적으로 선택되고 사용자 이름에 대한 온라인 ID가 제안됩니다.  
  
3.  사용자 계정을 만들려면:  
  
    1.  제안된 사용자 계정에 필요한 내용을 변경합니다.  
  
    2.  선택적으로 링크를 클릭하여 사용자 계정에 할당될 임시 암호를 확인합니다. 사용자에게 새 계정 이름과 함께 임시 암호를 제공해야 합니다.  
  
         (초보가이 파일에 나열 된 이러한 암호를 찾을 계정을 만들면: *SystemDrive*\Users\\*Office365admin*\\*NewServerUser*.txt 여기서 *Office365admin* 계정인 네트워크 서버에 Office 365를 관리 하는 데 사용 되는 및 *NewServerUser* 새 사용자 계정 이름입니다.)  
  
    3.  **다음** 을 클릭하여 사용자 계정을 만듭니다.  
  
4.  사용자를 게 알립니다 해당 새 사용자 계정 및 임시 암호를 사용 하 여 첫 번째 시간 œ 서버에서 로그인 및 로그인 암호를 변경 해야 합니다. 사용자를 위한 지침은 [새 Microsoft 온라인 계정 사용을 시작하려면](#BKMK_ToBeginUsingAnOnlineAccount)을 참조하세요.  
  
     앞으로 사용자 계정으로 온라인 계정에 대 한 암호 동기화 됩니다 하 고 Office 365에서 온라인 암호 변경 되지 않아야 알고 있어야 합니다.  
  
###  <a name="BKMK_ToCreateaNewUserAccount"></a> 온라인 계정이 할당 된 새 사용자 계정을 만들려면  
  
1.  대시보드에서 **사용자**를 클릭합니다.  
  
2.  **사용자 작업**에서 **사용자 계정 추가**를 클릭합니다. 사용자 계정 추가 마법사가 나타납니다.  
  
3.  지침에 따라 사용자 계정을 만듭니다.  
  
4.  **Microsoft Online Services 계정 할당** 페이지에서 사용자에 대한 새 온라인 계정을 만들거나 기존 온라인 계정을 할당합니다.  
  
    -   새 온라인 계정을 만들려면 **새 Microsoft Online Services 계정 만들기 및 이 사용자 계정에 할당**을 클릭하고 Microsoft Online Services 계정의 이름을 입력합니다(기본적으로 사용자 이름이 온라인 ID에 사용됨). 그리고 **다음**을 클릭합니다.  
  
    -   기존 Microsoft 온라인 계정을 할당하려면 **이 사용자 계정에 기존 Microsoft Online Services 계정 할당**을 클릭하고 드롭다운 목록에서 기존 계정을 선택합니다. 그리고 **다음**을 클릭합니다.  
  
    > [!NOTE]
    >  Windows Server Essentials에서 Microsoft Online Services 계정을 마법사와 대시보드 레이블에서 Office 365 계정 이라고 합니다.  
  
5.  지시에 따라 마법사를 완료합니다.  
  
6.  사용자에게 새 온라인 계정으로 Office 365에 로그인하기 전에 사용자 계정 암호를 변경해야 함을 알립니다. 자세한 내용은 [새 Microsoft 온라인 계정 사용을 시작하려면](#BKMK_ToBeginUsingAnOnlineAccount)을 참조하세요.  
  
#### <a name="BKMK_ToAssignAnOnlineAccount"></a>사용자 계정에 온라인 계정을 할당 하려면  
  
1.  대시보드에서 **사용자**를 클릭합니다.  
  
2.  목록에서 사용자 계정을 마우스 오른쪽 단추로 클릭하고 **Microsoft 온라인 계정 할당**을 클릭합니다. Microsoft Online Services 계정 할당 마법사가 나타납니다.  
  
3.  기존 온라인 계정을 할당하거나 사용자에 대한 새 온라인 계정을 만듭니다. 새 계정의 기본 온라인 ID는 사용자 이름입니다. 그리고 **다음** 을 클릭하여 사용자 계정에 온라인 계정을 추가합니다.  
  
4.  마법사의 마지막 페이지에서 정보를 검토하고 **닫기**를 클릭합니다.  
  
5.  사용자에게 새 온라인 계정으로 Office 365에 로그인하기 전에 사용자 계정 암호를 변경해야 함을 알립니다. 자세한 내용은 [새 Microsoft 온라인 계정 사용을 시작하려면](#BKMK_ToBeginUsingAnOnlineAccount)을 참조하세요.  
  
##  <a name="BKMK_SECTION_ManageOnlineAccounts"></a> 온라인 계정 관리  
 Windows Server Essentials에서 사용자 계정에 온라인 계정을 추가할 때 s 계정 수명 주기 내내 두 계정 모두를 함께 관리할 수 있습니다.  
  
###  <a name="BKMK_UnderstandingAccountStatus"></a> 온라인 계정 상태 이해  
 사용자 계정이 Microsoft Online Services 계정을 할당하면 계정의 메일 주소가 대시보드 **사용자** 페이지의 **Microsoft 온라인 계정** 열에 표시됩니다. (열 레이블의 Windows Server Essentials **Office 365 계정**.)  
  
-   메일 주소 옆의 파란색 아이콘은 온라인 계정이 활성 상태임을 나타냅니다. 즉, 계정 현재 Office 365 라이선스가 있고 사용자는 온라인 ID를 사용 하 여 Office 365에 로그인 할 수 있습니다.  
  
-   전자 메일 주소 옆에 있는 음영 처리 된 아이콘을 나타내는 온라인 계정 이므로 비활성 œ 하거나 라이선스가 더 이상 활성 상태가 또는 온라인 계정 할당 해제 되었습니다. 사용자가 온라인 계정 할당을 취소 하면 라이선스가 제거 되 고 사용자 계정을 사용 하는 Office 365에 로그인에서 차단 됩니다. 그러나 서버에는 사용자 계정 이름 및 Office 365 전자 메일 주소 사이의 매핑을 유지 합니다.  
  
###  <a name="BKMK_UnassignOnlineAccount"></a> 온라인 계정에 대 한 액세스 제한  
 사용자를 퇴사 하거나 Office 365 서비스에 대 한 사용자가의 액세스를 제한 하려는 경우 어떤 해야 할까요? Windows Server Essentials에서 계정 사용자와 함께 사용자가 온라인 계정을 관리 하는 경우 세 가지 옵션이 있습니다.  
  
-   **온라인 계정 할당 해제** ? 서버의 리소스에 대 한 액세스를 방지 하지 않고 Office 365를 사용 하 여 사용자를 유지 하려는 경우 온라인 계정 할당 해제 해야 합니다. Office 365 라이선스를 해제 하 고 사용자가 Office 365에 로그인에서 차단 됩니다. 그러나 서버에는 사용자 계정 이름 및 Office 365 전자 메일 주소 사이의 매핑을 유지 합니다. 자세한 내용은 [사용자 계정에서 온라인 계정을 할당 해제 하려면](#BKMK_ToUnassignAnOnlineAccount)합니다.  
  
-   **사용자 계정 비활성화** ? 일시적 또는 영구적으로 직원을 유지 하기 때문에 사용자 계정을 비활성화 하는 경우 사용자가 온라인 계정도 비활성화 됩니다. 온라인 계정을 사용할 수 없지만 메일을 비롯한 사용자 데이터는 Microsoft Online Services에서 유지됩니다. 자세한 내용은 [사용자 계정을 비활성화](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage6) 에 [Manage User Accounts](Manage-User-Accounts-in-Windows-Server-Essentials.md)합니다.  
  
-   **사용자 계정을 제거** ? 사용자 계정을 제거 하면 온라인 계정도 Microsoft Online Services도 제거 됩니다. 자세한 내용은 [사용자 계정을 제거](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Remove) 에 [Manage User Accounts](Manage-User-Accounts-in-Windows-Server-Essentials.md)합니다.  
  
    > [!WARNING]
    >  온라인 계정이 제거되면 사용자 데이터에는 Microsoft Online Services의 데이터 보존 정책이 적용됩니다. 직원이 퇴직 사용자가의 사용자 데이터를 유지 해야 할 경우에 사용자 계정을 제거 하는 대신 비활성화 합니다.  
  
####  <a name="BKMK_ToUnassignAnOnlineAccount"></a> 사용자 계정에서 온라인 계정을 할당 해제 하려면  
  
1.  대시보드에서 **사용자**를 클릭합니다.  
  
2.  목록에서 사용자 계정을 마우스 오른쪽 단추로 누른 **Microsoft 온라인 계정 할당 해제** (Windows Server Essentials에서 클릭 **Office 365 계정 할당 해제**).  
  
3.  확인 프롬프트에서 **예**를 클릭합니다.  
  
##  <a name="BKMK_SECTION_ManageEmailAddresses"></a> Exchange Online에 대 한 전자 메일 주소를 관리 합니다.  
 Windows Server Essentials에서 사용자가 온라인 계정에 전자 메일 주소에 추가 하 여 사용자가 Exchange Online 여러 전자 메일 주소로 전자 메일을 받을 수 있습니다.  
  
###  <a name="BKMK_PROC_AddEmailAliases"></a> 사용자가 Microsoft 온라인 계정 추가 전자 메일 주소를 추가 하려면  
  
1.  Windows Server Essentials 대시보드를 클릭 **사용자**합니다.  
  
2.  목록에서 사용자 계정을 마우스 오른쪽 단추로 클릭하고 **계정 속성 보기**를 클릭합니다.  
  
3.  에 **Microsoft online** 계정 속성 탭 (또는 **Office 365** Windows Server Essentials에서 탭)를 클릭 **추가**합니다.  
  
4.  새 메일 별칭을 입력하고 메일 도메인을 선택합니다.  
  
5.  **확인** 을 두 번 클릭합니다.  
  
##  <a name="BKMK_SECTION_ManageDistributionGroups"></a> Exchange Online (Windows Server Essentials에만 해당)에 대 한 메일 그룹 관리  
 Office 365를 사용 하 여 Windows Server Essentials 서버를 통합 하면 수 만들고 Windows Server Essentials 대시보드에서 Exchange Online에 대 한 배포 그룹을 관리 합니다. 초보에서 이렇게 합니다 **배포 그룹** 탭에 추가 되는 합니다 **사용자** 페이지. Exchange Online 구독이 있는 경우에만 이 탭이 표시됩니다. 이 기능은 Windows Server Essentials에서 사용할 수 없습니다.  
  
 다음 절차에 따라 수행할 수 있는 작업:  
  
-   [메일 그룹 추가](#BKMK_PROCEDURE_AddDistGroup)  
  
-   [배포 그룹의 구성원을 변경](#BKMK_ChangeGroupMembers)  
  
-   [사용자가의 메일 그룹 구성원 변경](#BKMK_EditUserMemberships)  
  
-   [배포 그룹 제거](#BKMK_RemoveDistributionGroup)  
  
###  <a name="BKMK_PROCEDURE_AddDistGroup"></a> 배포 그룹을 추가 하려면  
  
1.  Windows Server Essentials의 대시보드, 클릭 **사용자**, 클릭 하 고는 **배포 그룹** 탭 합니다.  
  
2.  **메일 그룹 작업**에서 **메일 그룹 추가**를 클릭합니다.  
  
     새 메일 그룹 추가 마법사가 표시됩니다.  
  
3.  **새 메일 그룹 추가** 페이지에서 다음 정보를 입력하고 **다음**을 클릭합니다.  
  
    -   새 메일 그룹에 대한 그룹 이름, 선택적 설명 및 메일 별칭을 입력합니다.  
  
    -   기본적으로 메일 그룹은 조직 외부 사용자로부터 메일을 받을 수 있습니다. 이 기능을 허용하지 않으려면 해당 옵션을 선택 취소합니다.  
  
4.  **그룹 구성원 추가** 페이지에서 **추가** 단추를 사용하여 온라인 계정이 할당된 활성 사용자 계정 및 기타 메일 그룹을 새 메일 그룹에 추가합니다. 그리고 **다음**을 클릭합니다.  
  
     새 메일 그룹이 Exchange Online에서 만들어집니다.  
  
###  <a name="BKMK_ChangeGroupMembers"></a> 배포 그룹의 구성원을 변경 하려면  
  
1.  대시보드에서 **사용자**, **메일 그룹** 탭을 차례로 클릭합니다.  
  
2.  목록에서 메일 그룹을 마우스 오른쪽 단추로 클릭하고 **그룹 구성원 변경**을 클릭합니다.  
  
3.  **추가** 및 **제거** 단추를 사용하여 메일 그룹에서 활성 온라인 계정을 추가하거나 제거합니다. 그리고 나서 **다음**을 클릭하여 Exchange Online에서 메일 그룹 구성원을 업데이트합니다.  
  
###  <a name="BKMK_EditUserMemberships"></a> 사용자가의 메일 그룹 구성원을 변경 하려면  
  
1.  대시보드에서 **사용자**를 클릭합니다.  
  
2.  목록에서 사용자 계정을 마우스 오른쪽 단추로 클릭하고 **계정 속성 보기**를 클릭합니다.  
  
3.  사용자 계정 속성에서 **메일 그룹** 탭, **편집**을 차례로 클릭합니다.  
  
4.  **그룹 구성원 편집** 상자에서 **추가** 및 **제거** 단추를 사용하여 사용자 계정에 대한 메일 그룹을 추가하거나 제거하고 **닫기**를 클릭합니다.  
  
5.  **확인**을 클릭하여 업데이트된 사용자 계정 속성을 저장합니다.  
  
###  <a name="BKMK_RemoveDistributionGroup"></a> 배포 그룹을 제거 하려면  
  
1.  대시보드에서 **사용자**, **메일 그룹** 탭을 차례로 클릭합니다.  
  
2.  목록에서 메일 그룹을 마우스 오른쪽 단추로 클릭하고 **그룹 제거**를 클릭합니다.  
  
3.  확인 프롬프트에서 **그룹 삭제**를 클릭합니다.  
  
     메일 그룹이 Exchange Online에서 제거됩니다.  
  
## <a name="see-also"></a>참조  
  
-   [사용자 계정 관리](Manage-User-Accounts-in-Windows-Server-Essentials.md)  
  
-   [Office 365 관리](Manage-Office-365-in-Windows-Server-Essentials.md)  
  
-   [Microsoft Online Services 관리](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)
