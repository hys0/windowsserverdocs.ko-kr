---
title: Windows Server Essentials 사용자에 대한 온라인 계정 관리
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.topic: article
ms.assetid: c09f4cf6-4d12-49fe-9ae4-e6cb14027b9d
author: nnamuhcs
ms.author: daveba
ms.openlocfilehash: dc3170c7d5267eef6f339dc229b1b9daaf9ac9ec
ms.sourcegitcommit: 2082335e1260826fcbc3dccc208870d2d9be9306
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69980275"
---
# <a name="manage-online-accounts-for-windows-server-essentials-users"></a>Windows Server Essentials 사용자에 대한 온라인 계정 관리

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Microsoft Office 365를 사용 하 여 Windows Server Essentials 서버를 통합 하는 경우 대시보드의 사용자 계정과 함께 온라인 계정을 관리할 수 있습니다. 이 항목에서는 대시보드에서 사용자 Microsoft Online Services 계정을 관리 하 여 얻을 수 있는 작업, 대시보드에서 온라인 계정을 만들고 관리 하는 방법, Exchange Online에 대 한 메일 주소 및 메일 그룹을 관리 하는 방법에 대해 알아봅니다. 대시보드에서.  

  
> [!NOTE]
>  Windows Server Essentials에서 Microsoft Online Services 계정을 관리 하려면 서버를 Office 365에 통합 해야 합니다. 지침은 [Office 365 관리](Manage-Office-365-in-Windows-Server-Essentials.md)를 참조 하세요.  
  
> [!IMPORTANT]
>  Windows Server Essentials에서 온라인 계정을 관리 하는 경우 *Office 365 계정*이라고 하는 Microsoft online Services 계정을 확인 하는 데 익숙할 것입니다. Windows Server Essentials의 대시보드에서는 레이블이 *Microsoft Online Services 계정*또는 *microsoft 온라인 계정* (short)으로 변경 되었습니다. 계정 및 절차는 동일하고 레이블만 변경되었습니다. 이 항목의 대부분 절차에서는 *온라인 계정*이라는 용어를 사용합니다.  
  
## <a name="in-this-topic"></a>항목 내용  
  
-   [대시보드에서 온라인 계정을 관리 해야 하는 이유는 무엇 인가요?](#BKMK_WhyManageOnlineAccounts)  
  
-   [온라인 계정 만들기](#BKMK_SECTION_CreateOnlineAccounts)  
  
-   [온라인 계정 관리](#BKMK_SECTION_ManageOnlineAccounts)  
  
-   [Exchange Online에 대 한 전자 메일 주소 관리](#BKMK_SECTION_ManageEmailAddresses)  
  
-   [Exchange Online에 대 한 메일 그룹 관리](#BKMK_SECTION_ManageDistributionGroups)  
  
##  <a name="BKMK_WhyManageOnlineAccounts"></a>대시보드에서 온라인 계정을 관리 해야 하는 이유는 무엇 인가요?  
 대시보드를 사용 하 여 Microsoft Online Services 계정을 사용자 계정에 할당 하면 계정 암호가 자동으로 동기화 되 고 사용자 계정의 수명 주기 내내 두 계정을 함께 유지 관리할 수 있습니다.  
  
 사용자는 동일한 암호를 사용 하 여 서버 및 Office 365의 리소스에 액세스할 수 있는 사용자에 게 편리 합니다. 사내 리소스에 대해 요구 하는 Office 365의 리소스에 대 한 액세스에 동일한 암호 요구 사항을 적용할 수 있습니다.  
  
### <a name="how-does-password-synchronization-work"></a>암호 동기화의 작동 원리  
 대시보드를 사용 하 여 Microsoft Online Services 계정을 사용자 계정에 할당 하면 사용자 계정 암호가 자동으로 사용자의 온라인 계정과 동기화 됩니다. 이는 사용자가 서버 및 Office 365의 리소스 모두에 액세스 하는 데 단일 암호만 필요 함을 의미 합니다. 또한 사용자 계정 및 사용자의 온라인 ID에 동일한 이름을 사용할 수 있습니다.  
  
 도메인에 연결된 컴퓨터나 원격 웹 액세스를 사용하여 사용자 계정의 암호를 변경하면 암호가 즉시 자동으로 동기화됩니다.  
  
> [!IMPORTANT]
>  Office 365가 Windows Server Essentials와 통합 된 경우 사용자는 Office 365 포털에서 Microsoft 온라인 계정의 암호를 변경 하면 안 됩니다. 암호를 변경하면 암호 동기화가 중단됩니다.  
  
### <a name="simplified-account-creation"></a>간단한 계정 만들기  
 대시보드에서 초기 온라인 계정을 만들면 또 다른 이점이 있습니다. 단일 작업으로 모든 사용자에 대한 온라인 계정을 만들 수 있습니다. 반면, 직원 들이 이미 Office 365를 사용 하 고 있는 경우 새 Windows Server Essentials 서버를 설정 하면 단일 작업으로 온라인 계정에서 모든 사용자 계정을 만들 수 있습니다. 자세한 내용은 [온라인 계정 만들기](#BKMK_SECTION_CreateOnlineAccounts)를 참조하세요.  
  
### <a name="manage-email-addresses-and-distribution-groups-from-the-dashboard"></a>대시보드에서 메일 주소 및 메일 그룹 관리  
 대시보드에서 Exchange Online에 대한 전자 메일 주소 및 메일 그룹을 관리할 수 있습니다. 그리고 메일 주소에서 조직의 인터넷 도메인을 사용할 수 있습니다. Office 365에 로그인 하지 않고 대시보드에서이 모든 작업을 수행할 수 있습니다. 대시보드에서 배포 그룹을 관리 하려면 Windows Server Essentials를 사용 해야 합니다. 이 기능은 Windows Server Essentials에서 지원 되지 않습니다.) 자세한 내용은 [Exchange Online에 대한 전자 메일 주소 관리](#BKMK_SECTION_ManageEmailAddresses) 및 [Exchange Online에 대한 메일 그룹 관리](#BKMK_SECTION_ManageDistributionGroups)를 참조하세요.  
  
### <a name="manage-the-user-account-and-online-account-together"></a>사용자 계정 및 온라인 계정을 함께 관리  
 그리고 계정 수명 주기 내내 사용자 계정과 함께 온라인 계정을 관리할 수 있습니다. 사용자 계정을 비활성화하면 Microsoft Online Services에서 온라인 계정도 비활성화됩니다. 사용자 계정을 제거하면 온라인 계정도 제거됩니다. 자세한 내용은 [온라인 계정 관리](#BKMK_SECTION_ManageOnlineAccounts)를 참조하세요.  
  
##  <a name="BKMK_SECTION_CreateOnlineAccounts"></a>온라인 계정 만들기  
 서버를 Office 365와 통합 하 고 나면 대시보드에서 사용자에 대 한 Microsoft Online Services 계정을 만드는 이점이 있습니다. 온라인 계정을 만드는 데 많은 유연성이 있습니다. 새 Office 365 구독이 있는 경우 모든 사용자에 대 한 온라인 계정을 일괄적으로 만들 수 있습니다. Office 365에서 온라인 계정을 이미 만든 경우에는 걱정할 필요가 없습니다. 새 서버를 설정 하는 경우 온라인 계정을 가져와서 서버에서 사용자 계정을 만들 수 있습니다. 그리고 개별 사용자 계정을 만들거나 기존 사용자 계정에 온라인 계정을 추가할 때 새로운 또는 기존 온라인 계정을 할당할 수 있습니다.  
  
 **라이선스 요구 사항** 사용자가 만드는 각 온라인 계정에 대 한 사용자 라이선스가 필요 합니다. 대시보드의 **office 365** 페이지를 확인 하 여 office 365 구독을 통해 사용할 수 있는 사용자 라이선스 수를 확인 합니다. 사용자 라이선스를 더 추가 해야 하는 경우 Office 365에서 Office 365 구독을 열어이 작업을 수행할 수 있습니다.  
  
 **사용자를 위한 후속 작업** 사용자 계정에 대 한 온라인 계정을 추가한 후에는 사용자가 다음 번에 로그인 할 때 사용자 계정에 대 한 암호를 변경 해야 합니다. 새 암호는 즉시 온라인 계정과 동기화됩니다. 그런 다음 암호를 사용 하 여 온라인 ID로 Office 365에 로그인 할 수 있습니다.  
  
> [!IMPORTANT]
>  Office 365에서 온라인 계정 암호를 변경 하면 안 된다는 점을 사용자에 게 강조 합니다. 이 암호는 사용자 계정의 암호를 변경할 때마다 자동으로 변경됩니다. Office 365에서 온라인 암호를 변경 하면 암호 동기화가 중단 됩니다.  
  
 이 섹션의 절차를 사용하여 다음을 수행합니다.  
  
-   [기존 사용자 계정에 대 한 온라인 계정 대량 생성](#BKMK_ToBulkCreateOnlineAccounts)  
  
-   [Microsoft Online Services 계정에서 사용자 계정 가져오기](#BKMK_ToImportUserAccounts)  
  
-   [온라인 계정이 할당 된 새 사용자 계정 만들기](#BKMK_ToCreateaNewUserAccount)  
  
-   [사용자 계정에 온라인 계정 할당](#BKMK_ToAssignAnOnlineAccount)  
  
> [!NOTE]
>  Windows Server Essentials를 사용 하는 경우 이러한 절차를 통해 *Microsoft Online Services 계정* 대신 *Office 365 계정이* 표시 됩니다. 프로세스는 동일 하지만 Windows Server Essentials에서 용어가 변경 되었습니다.  
  
###  <a name="BKMK_ToBulkCreateOnlineAccounts"></a>기존 사용자 계정에 대 한 온라인 계정을 대량으로 만들려면  
  
1.  관리자 권한으로 서버에 로그인 하 고 Windows Server Essentials 대시보드를 엽니다.  
  
2.  대시보드에서 **사용자** 페이지를 엽니다.  
  
3.  **사용자 작업**에서 **Microsoft 온라인 계정 추가**를 클릭합니다.  
  
     마법사의 **Microsoft Online Services 계정 추가** 페이지에는 Microsoft 온라인 계정이 없는 모든 사용자 계정이 표시됩니다. 모든 계정이 기본적으로 선택되고 Microsoft 온라인 ID에 대한 사용자 이름이 제안됩니다. Office 365 구독에 사용자 지정 인터넷 도메인을 연결 하면 해당 도메인이 기본적으로 사용 됩니다.  
  
4.  **Microsoft Online Services 계정 추가** 페이지에서 만들어질 계정을 검토합니다. 예를 들어 다른 온라인 ID가 포함된 온라인 계정을 보유한 사용자가 있는지 확인하고 메일 주소에서 사용할 도메인이 선택되었는지 확인합니다. 필요한 변경 작업을 마치면 **다음**을 클릭합니다.  
  
5.  **Microsoft Online services 라이선스 할당** 페이지에서 사용자가 사용할 Office 365 서비스를 선택 합니다. **다음**을 클릭하면 계정 만들기가 시작됩니다.  
  
    > [!NOTE]
    >  각 온라인 계정에 대해 Office 365에 서비스 라이선스가 있어야 합니다. 사용할 수 있는 라이선스를 확인하고 필요하면 대시보드의 **Office 365** 페이지에서 구독을 열어 라이선스를 추가합니다.  
  
6.  이제 사용자에게 Microsoft 온라인 계정을 보유하게 되었음을 알립니다. Office 365에 로그인 하려면 먼저 네트워크 사용자 계정 암호를 변경 해야 합니다. 자세한 내용은 [새 Microsoft 온라인 계정 사용을 시작하려면](#BKMK_ToBeginUsingAnOnlineAccount)을 참조하세요.  
  
###  <a name="BKMK_ToBeginUsingAnOnlineAccount"></a>새 Microsoft 온라인 계정 사용을 시작 하려면  
  
1.  네트워크 사용자 계정으로 컴퓨터에 로그인합니다.  
  
2.  사용자 계정의 암호를 변경합니다. 시작하려면 Ctrl+Alt+Delete를 누르고 **암호 변경**을 클릭합니다.  
  
     암호를 변경하면 암호가 새 온라인 계정과 동기화됩니다. 이제 동일한 암호를 사용 하 여 Office 365에 로그인 할 수 있습니다.  
  
3.  새 온라인 ID 및 사용자 계정 암호를 사용하여[Office 365에 로그인](https://login.microsoftonline.com/login.srf?wa=wsignin1.0&rpsnv=3&ct=1398981834&rver=6.1.6206.0&wp=MBI_SSL&wreply=https:%2F%2Foutlook.office365.com%2Fowa%2F&id=260563&CBCXT=out) 합니다.  
  
    > [!IMPORTANT]
    >  Office 365에서 온라인 계정 암호를 변경 하지 마세요. 온라인 암호를 변경하면 암호 동기화가 중단됩니다. 온라인 암호는 네트워크 사용자 계정의 암호를 변경할 때마다 업데이트됩니다.  
  
###  <a name="BKMK_ToImportUserAccounts"></a>기존 온라인 계정에서 사용자 계정을 가져오려면  
  
1.  대시보드에서 **사용자** 페이지를 엽니다.  
  
2.  **사용자 작업**에서 **Office 365에서 계정 가져오기**를 클릭합니다.  
  
     다음 페이지에는 서버에 사용자 계정이 없는 Office 365 구독의 모든 온라인 계정이 표시 됩니다. 모든 계정이 기본적으로 선택되고 사용자 이름에 대한 온라인 ID가 제안됩니다.  
  
3.  사용자 계정을 만들려면:  
  
    1.  제안된 사용자 계정에 필요한 내용을 변경합니다.  
  
    2.  선택적으로 링크를 클릭하여 사용자 계정에 할당될 임시 암호를 확인합니다. 사용자에게 새 계정 이름과 함께 임시 암호를 제공해야 합니다.  
  
         계정을 만든 후에는 다음 파일에 나열 된 이러한 암호를 찾을 수 있습니다.\UsersOffice365admin newserveruser. 여기서 Office365admin은 서버에서 Office 365을 관리 하는 데 사용 되는 네트워크 계정이 고, newserveruser는 새로운\\\\ 사용자 계정 이름입니다.)  
  
    3.  **다음** 을 클릭하여 사용자 계정을 만듭니다.  
  
4.  사용자에 게 처음으로 속성만 서버에 로그인 하는 데 사용할 새 사용자 계정 및 임시 암호를 알려 서 사용자가 로그인 한 후 암호를 변경 해야 합니다. 사용자를 위한 지침은 [새 Microsoft 온라인 계정 사용을 시작하려면](#BKMK_ToBeginUsingAnOnlineAccount)을 참조하세요.  
  
     온라인 계정에 대 한 암호는 앞으로 진행 되는 사용자 계정과 동기화 되며, Office 365에서 온라인 암호를 변경 하면 안 됩니다.  
  
###  <a name="BKMK_ToCreateaNewUserAccount"></a>온라인 계정이 할당 된 새 사용자 계정을 만들려면  
  
1.  대시보드에서 **사용자**를 클릭합니다.  
  
2.  **사용자 작업**에서 **사용자 계정 추가**를 클릭합니다. 사용자 계정 추가 마법사가 나타납니다.  
  
3.  지침에 따라 사용자 계정을 만듭니다.  
  
4.  **Microsoft Online Services 계정 할당** 페이지에서 사용자에 대한 새 온라인 계정을 만들거나 기존 온라인 계정을 할당합니다.  
  
    -   새 온라인 계정을 만들려면 **새 Microsoft Online Services 계정 만들기 및 이 사용자 계정에 할당**을 클릭하고 Microsoft Online Services 계정의 이름을 입력합니다(기본적으로 사용자 이름이 온라인 ID에 사용됨). 그리고 **다음**을 클릭합니다.  
  
    -   기존 Microsoft 온라인 계정을 할당하려면 **이 사용자 계정에 기존 Microsoft Online Services 계정 할당**을 클릭하고 드롭다운 목록에서 기존 계정을 선택합니다. 그리고 **다음**을 클릭합니다.  
  
    > [!NOTE]
    >  Windows Server Essentials에서 Microsoft Online Services 계정은 마법사와 대시보드 레이블에서 Office 365 계정 이라고 합니다.  
  
5.  지시에 따라 마법사를 완료합니다.  
  
6.  사용자에게 새 온라인 계정으로 Office 365에 로그인하기 전에 사용자 계정 암호를 변경해야 함을 알립니다. 자세한 내용은 [새 Microsoft 온라인 계정 사용을 시작하려면](#BKMK_ToBeginUsingAnOnlineAccount)을 참조하세요.  
  
#### <a name="BKMK_ToAssignAnOnlineAccount"></a>사용자 계정에 온라인 계정을 할당 하려면  
  
1.  대시보드에서 **사용자**를 클릭합니다.  
  
2.  목록에서 사용자 계정을 마우스 오른쪽 단추로 클릭하고 **Microsoft 온라인 계정 할당**을 클릭합니다. Microsoft Online Services 계정 할당 마법사가 나타납니다.  
  
3.  기존 온라인 계정을 할당하거나 사용자에 대한 새 온라인 계정을 만듭니다. 새 계정의 기본 온라인 ID는 사용자 이름입니다. 그리고 **다음** 을 클릭하여 사용자 계정에 온라인 계정을 추가합니다.  
  
4.  마법사의 마지막 페이지에서 정보를 검토하고 **닫기**를 클릭합니다.  
  
5.  사용자에게 새 온라인 계정으로 Office 365에 로그인하기 전에 사용자 계정 암호를 변경해야 함을 알립니다. 자세한 내용은 [새 Microsoft 온라인 계정 사용을 시작하려면](#BKMK_ToBeginUsingAnOnlineAccount)을 참조하세요.  
  
##  <a name="BKMK_SECTION_ManageOnlineAccounts"></a>온라인 계정 관리  
 Windows Server Essentials에서 사용자 계정에 온라인 계정을 추가 하는 경우 계정 수명 주기 내내 두 계정을 함께 관리할 수 있습니다.  
  
###  <a name="BKMK_UnderstandingAccountStatus"></a>온라인 계정 상태 이해  
 사용자 계정이 Microsoft Online Services 계정을 할당하면 계정의 메일 주소가 대시보드 **사용자** 페이지의 **Microsoft 온라인 계정** 열에 표시됩니다. Windows Server Essentials에서 열 레이블은 **Office 365 계정**입니다.  
  
-   메일 주소 옆의 파란색 아이콘은 온라인 계정이 활성 상태임을 나타냅니다. 즉, 계정에 현재 Office 365 라이선스가 있고 사용자는 온라인 ID를 사용 하 여 Office 365에 로그인 할 수 있습니다.  
  
-   전자 메일 주소 옆의 음영 처리 된 아이콘은 라이선스가 더 이상 활성 상태가 아니거나 온라인 계정이 할당 해제 되어 온라인 계정이 비활성 상태임을 나타냅니다 속성만. 사용자의 온라인 계정을 할당 해제 하면 라이선스가 제거 되 고 사용자는 계정을 사용 하 여 Office 365에 로그인 하지 못하게 됩니다. 그러나 서버는 사용자 계정 이름과 Office 365 전자 메일 주소 간의 매핑을 유지 합니다.  
  
###  <a name="BKMK_UnassignOnlineAccount"></a>온라인 계정에 대 한 액세스 제한  
 사용자가 조직을 떠나는 경우 나 Office 365 서비스에 대 한 사용자 액세스를 제한 하려는 경우 어떻게 해야 하나요? 사용자 온라인 계정을 Windows Server Essentials의 사용자 계정과 함께 관리 하는 경우 다음 세 가지 옵션을 사용할 수 있습니다.  
  
-   **온라인 계정 할당을** 취소 하 시겠습니까? 사용자가 서버의 리소스에 대 한 액세스를 방지 하지 않고 Office 365을 사용 하지 않도록 하려면 온라인 계정을 할당 해제 해야 합니다. Office 365 라이선스가 해제 되 고 사용자가 Office 365에 로그인 하지 못하게 됩니다. 그러나 서버는 사용자 계정 이름과 Office 365 전자 메일 주소 간의 매핑을 유지 합니다. 지침은 [사용자 계정에서 온라인 계정 할당 해제를](#BKMK_ToUnassignAnOnlineAccount)참조 하세요.  
  
-   **사용자 계정을 비활성화** 하 시겠습니까? 직원이 일시적으로 또는 영구적으로 떠날 때 사용자 계정을 비활성화 하면 사용자의 온라인 계정도 비활성화 됩니다. 온라인 계정을 사용할 수 없지만 메일을 비롯한 사용자 데이터는 Microsoft Online Services에서 유지됩니다. 지침은 [사용자 계정 관리](Manage-User-Accounts-in-Windows-Server-Essentials.md)에서 [사용자 계정 비활성화](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage6) 를 참조 하세요.  
  
-   **사용자 계정을 제거** 하 시겠습니까? 사용자 계정을 제거 하면 온라인 계정도 Microsoft Online Services에서 제거 됩니다. 지침은 [사용자 계정 관리](Manage-User-Accounts-in-Windows-Server-Essentials.md)에서 [사용자 계정 제거](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Remove) 를 참조 하세요.  
  
    > [!WARNING]
    >  온라인 계정이 제거되면 사용자 데이터에는 Microsoft Online Services의 데이터 보존 정책이 적용됩니다. 직원이 퇴사 한 후에 사용자의 사용자 데이터를 유지 해야 하는 경우 사용자 계정을 제거 하는 대신 비활성화 합니다.  
  
####  <a name="BKMK_ToUnassignAnOnlineAccount"></a>사용자 계정에서 온라인 계정 할당을 취소 하려면  
  
1.  대시보드에서 **사용자**를 클릭합니다.  
  
2.  목록에서 사용자 계정을 마우스 오른쪽 단추로 클릭 한 다음 **Microsoft 온라인 계정 할당** 해제를 클릭 합니다 (Windows Server Essentials에서 **Office 365 계정 할당**해제 클릭).  
  
3.  확인 프롬프트에서 **예**를 클릭합니다.  
  
##  <a name="BKMK_SECTION_ManageEmailAddresses"></a>Exchange Online에 대 한 전자 메일 주소 관리  
 Windows Server Essentials에서 사용자의 온라인 계정에 전자 메일 주소를 추가 하면 사용자가 Exchange Online에서 여러 전자 메일 주소로 전자 메일을 받을 수 있습니다.  
  
###  <a name="BKMK_PROC_AddEmailAliases"></a>사용자의 Microsoft 온라인 계정에 다른 메일 주소를 추가 하려면  
  
1.  Windows Server Essentials 대시보드에서 **사용자**를 클릭 합니다.  
  
2.  목록에서 사용자 계정을 마우스 오른쪽 단추로 클릭하고 **계정 속성 보기**를 클릭합니다.  
  
3.  계정 속성의 **Microsoft 온라인** 탭 (또는 Windows Server Essentials의 **Office 365** 탭)에서 **추가**를 클릭 합니다.  
  
4.  새 메일 별칭을 입력하고 메일 도메인을 선택합니다.  
  
5.  **확인** 을 두 번 클릭합니다.  
  
##  <a name="BKMK_SECTION_ManageDistributionGroups"></a>Exchange Online에 대 한 메일 그룹 관리 (Windows Server Essentials만 해당)  
 Windows Server Essentials 서버를 Office 365와 통합 한 후에는 Windows Server Essentials 대시보드에서 Exchange Online에 대 한 메일 그룹을 만들고 관리할 수 있습니다. **사용자** 페이지에 추가 된 **메일 그룹** 탭에서이 작업을 수행 합니다. Exchange Online 구독이 있는 경우에만 이 탭이 표시됩니다. 이 기능은 Windows Server Essentials에서 사용할 수 없습니다.  
  
 다음 절차에 따라 수행할 수 있는 작업:  
  
-   [메일 그룹 추가](#BKMK_PROCEDURE_AddDistGroup)  
  
-   [메일 그룹의 구성원 변경](#BKMK_ChangeGroupMembers)  
  
-   [사용자의 메일 그룹 멤버 자격 변경](#BKMK_EditUserMemberships)  
  
-   [메일 그룹 제거](#BKMK_RemoveDistributionGroup)  
  
###  <a name="BKMK_PROCEDURE_AddDistGroup"></a>메일 그룹을 추가 하려면  
  
1.  Windows Server Essentials의 대시보드에서 **사용자**를 클릭 한 다음 **메일 그룹** 탭을 클릭 합니다.  
  
2.  **메일 그룹 작업**에서 **메일 그룹 추가**를 클릭합니다.  
  
     새 메일 그룹 추가 마법사가 표시됩니다.  
  
3.  **새 메일 그룹 추가** 페이지에서 다음 정보를 입력하고 **다음**을 클릭합니다.  
  
    -   새 메일 그룹에 대한 그룹 이름, 선택적 설명 및 메일 별칭을 입력합니다.  
  
    -   기본적으로 메일 그룹은 조직 외부 사용자로부터 메일을 받을 수 있습니다. 이 기능을 허용하지 않으려면 해당 옵션을 선택 취소합니다.  
  
4.  **그룹 구성원 추가** 페이지에서 **추가** 단추를 사용하여 온라인 계정이 할당된 활성 사용자 계정 및 기타 메일 그룹을 새 메일 그룹에 추가합니다. 그리고 **다음**을 클릭합니다.  
  
     새 메일 그룹이 Exchange Online에서 만들어집니다.  
  
###  <a name="BKMK_ChangeGroupMembers"></a>메일 그룹의 구성원을 변경 하려면  
  
1.  대시보드에서 **사용자**, **메일 그룹** 탭을 차례로 클릭합니다.  
  
2.  목록에서 메일 그룹을 마우스 오른쪽 단추로 클릭하고 **그룹 구성원 변경**을 클릭합니다.  
  
3.  **추가** 및 **제거** 단추를 사용하여 메일 그룹에서 활성 온라인 계정을 추가하거나 제거합니다. 그리고 나서 **다음**을 클릭하여 Exchange Online에서 메일 그룹 구성원을 업데이트합니다.  
  
###  <a name="BKMK_EditUserMemberships"></a>사용자의 메일 그룹 구성원을 변경 하려면  
  
1.  대시보드에서 **사용자**를 클릭합니다.  
  
2.  목록에서 사용자 계정을 마우스 오른쪽 단추로 클릭하고 **계정 속성 보기**를 클릭합니다.  
  
3.  사용자 계정 속성에서 **메일 그룹** 탭, **편집**을 차례로 클릭합니다.  
  
4.  **그룹 구성원 편집** 상자에서 **추가** 및 **제거** 단추를 사용하여 사용자 계정에 대한 메일 그룹을 추가하거나 제거하고 **닫기**를 클릭합니다.  
  
5.  **확인**을 클릭하여 업데이트된 사용자 계정 속성을 저장합니다.  
  
###  <a name="BKMK_RemoveDistributionGroup"></a>메일 그룹을 제거 하려면  
  
1.  대시보드에서 **사용자**, **메일 그룹** 탭을 차례로 클릭합니다.  
  
2.  목록에서 메일 그룹을 마우스 오른쪽 단추로 클릭하고 **그룹 제거**를 클릭합니다.  
  
3.  확인 프롬프트에서 **그룹 삭제**를 클릭합니다.  
  
     메일 그룹이 Exchange Online에서 제거됩니다.  
  
## <a name="see-also"></a>참조  
  
-   [사용자 계정 관리](Manage-User-Accounts-in-Windows-Server-Essentials.md)  
  
-   [Office 365 관리](Manage-Office-365-in-Windows-Server-Essentials.md)  
  
-   [Microsoft Online Services 관리](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)
