---
title: "Windows Server Essentials 사용자에 대 한 온라인 계정 관리"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="manage-online-accounts-for-windows-server-essentials-users"></a>Windows Server Essentials 사용자에 대 한 온라인 계정 관리

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

Windows Server Essentials 서버에 Microsoft Office 365와 통합 하는 경우 대시보드에서 온라인 계정을 사용자 계정 함께 관리할 수 있습니다. 이 항목에서 하면 자가 알아봅니다 대시보드에서 사용자가 Microsoft Online Services 계정을 관리 하 여 얻을 수 있는, 만들고, 대시보드에서 온라인 계정을 관리 하는 방법 이메일 주소 및 메일 그룹 대시보드에서 Exchange Online을 관리 하는 방법.  

  
> [!NOTE]
>  Windows Server Essentials의 계정을 Microsoft 온라인 서비스를 관리 하려면 서버 Office 365와 통합 해야 합니다. 자세한 내용은 [Office 365 관리](Manage-Office-365-in-Windows-Server-Essentials.md)합니다.  
  
> [!IMPORTANT]
>  하는 경우 Windows Server Essentials의 온라인 계정을 관리 하 하면에 익숙한 표시 라고 하는 Microsoft Online Services 계정을 *Office 365 계정이*합니다. Windows Server Essentials의 대시보드에서 레이블을로 변경 된 *Microsoft Online Services 계정*, 또는 *온라인 Microsoft 계정* 간단히 합니다. 계정과 절차는 동일 합니다. 만 레이블이 변경 합니다. 대부분의 절차가이 항목의 사용 기간 *온라인 계정*합니다.  
  
## <a name="in-this-topic"></a>이 항목에서  
  
-   [대시보드에서 온라인 내 계정의 관리 해야 하나요?](#BKMK_WhyManageOnlineAccounts)  
  
-   [온라인 계정 만들기](#BKMK_SECTION_CreateOnlineAccounts)  
  
-   [온라인 계정 관리](#BKMK_SECTION_ManageOnlineAccounts)  
  
-   [Exchange Online에 대 한 메일 주소를 관리](#BKMK_SECTION_ManageEmailAddresses)  
  
-   [Exchange Online에 대 한 메일 그룹 관리](#BKMK_SECTION_ManageDistributionGroups)  
  
##  <a name="BKMK_WhyManageOnlineAccounts"></a>대시보드에서 온라인 내 계정의 관리 해야 하나요?  
 대시보드 Microsoft Online Services 계정을 사용자 계정에 할당를 사용 하 여 계정 암호는 자동으로 동기화 하 고 사용자 계정의 수명 동안 함께 계정이 두 개를 유지할 수 있습니다.  
  
 서버에서 및 Office 365에 리소스에 액세스 하는 동일한 암호를 사용할 수 있는 사용자를 위해 편리한입니다. 및 리소스에 Office 365 사내 리소스에 대 한 해야 하는 동일한 암호 요구 사항에 대 한 액세스를 적용할 수 있습니다.  
  
### <a name="how-does-password-synchronization-work"></a>암호 동기화는 어떻게 작동 하나요?  
 대시보드 Microsoft Online Services 계정을 사용자 계정에 할당를 사용 하 여 사용자 계정 암호 사용자 s 온라인 계정으로 자동으로 동기화 됩니다. 즉, 사용자에만 서버와 Office 365에 모두 리소스에 액세스 하는 데 단일 암호가 필요 합니다. 또한, 사용자 계정 및 온라인 s 사용자 ID 이름이 같은 사용할 수 있습니다.  
  
 암호 동기화 즉시 하 고 자동으로 사용자가 도메인에 가입 하는 컴퓨터 또는 웹에 대 한 원격 액세스를 사용 하 여 해당 사용자 계정의 암호를 변경할 때 발생 합니다.  
  
> [!IMPORTANT]
>  Windows Server Essentials와 Office 365 통합 되어, 사용자가 Office 365 포털에서 온라인 Microsoft 계정에 대 한 암호를 하지 변경 해야 합니다. 그러면이 암호 동기화를 중단 됩니다.  
  
### <a name="simplified-account-creation"></a>간소화 된 계정 만들기  
 대시보드에서 온라인 초기 계정을 만들 때 다른 이점이 있습니다. 모든 작업을 단일으로 사용자에 대 한 온라인 계정을 만들 수 있습니다. 반면에 직원에 게 사용 하는 경우 Office 365, 이미 고 새로운 Windows Server Essentials 서버 설정에서 만들 수 있습니다의 모든 사용자 계정이 단일 동작을 사용 하 여 온라인 계정을 합니다. 자세한 내용은 참조 [온라인 계정 만들기](#BKMK_SECTION_CreateOnlineAccounts)합니다.  
  
### <a name="manage-email-addresses-and-distribution-groups-from-the-dashboard"></a>메일 주소 및 메일 그룹 대시보드에서 관리  
 메일 주소 및 메일 그룹 대시보드에서 Exchange Online을 관리할 수 있습니다. 그리고 조직의 인터넷 도메인 메일 주소에 사용할 수 있습니다. 에서 수행할 수 있는이 모든 대시보드, Office 365에 로그인 하지 않고 합니다. (하면을 할 Windows Server Essentials을 사용 하 여 메일 그룹 대시보드에서 관리할 수 있습니다. 이 기능이 지원 되지 않습니다 Windows Server Essentials의.) 자세한 내용은 참조 [관리 메일 주소를 Exchange Online](#BKMK_SECTION_ManageEmailAddresses) 및 [Exchange Online에 대 한 메일 그룹 관리](#BKMK_SECTION_ManageDistributionGroups)합니다.  
  
### <a name="manage-the-user-account-and-online-account-together"></a>함께 사용자 계정 및 온라인 계정 관리  
 및 계정의 수명 전반에 걸쳐 사용자 계정 함께 한 온라인 계정을 관리할 수 있습니다. 사용자 계정이 비활성화 하면 온라인 계정은 또한 비활성화 Microsoft Online Services에 있습니다. 사용자 계정을 제거 하는 경우 온라인 계정도 제거 됩니다. 자세한 내용은 참조 [온라인 계정 관리](#BKMK_SECTION_ManageOnlineAccounts)합니다.  
  
##  <a name="BKMK_SECTION_CreateOnlineAccounts"></a>온라인 계정 만들기  
 서버에 Office 365와 통합 하면 대시보드에서 사용자 용 Microsoft Online Services 계정을 만들 수는 있습니다. 자 하는 많은 유연성 온라인 계정 만들기 합니다. 새로운 Office 365 구독을 사용 하는 경우 대량-계정을 만들 수 있습니다 온라인 모든 사용자에 대 한 합니다. Office 365에 이미 온라인 계정의 만든 경우 걱정 하지 마세요. 새 서버 설정, 있습니다 수 만드는 경우 사용자 계정 서버에서 온라인 계정 가져와서 합니다. 및 기존 사용자 계정에 한 온라인 계정을 추가 하면 각 사용자 계정을 만들 때 또는 새 또는 된 기존 온라인 계정 지정할 수 있습니다.  
  
 **요구 사항을 사용권** 사용자 라이선스는 사용자가 만든 각 온라인 계정에 대 한 해야 합니다. 검사는 **Office 365** 개수 사용자 라이선스 Office 365 구독을 통해 사용할 수 있는지 대시보드에서 페이지 합니다. 더 많은 사용자 라이선스를 추가 하려는 경우 자를 열 수 Office 365 구독 된 데이터를 지우는 Office 365의 합니다.  
  
 **사용자에 대 한 후속** 사용자 다음에 로그인 할 때 사용자 계정의 암호를 변경 하는 데 사용자 계정에 대 한 온라인 계정을 추가 하면 됩니다. 자녀가 온라인 계정에 새 암호 즉시 동기화 됩니다. 그 후 자녀가 온라인 id Office 365에 로그인 할 암호를 사용할 수 있습니다.  
  
> [!IMPORTANT]
>  강조 하 고 사용자에 게 Office 365에서 자녀가 온라인 계정 암호 변경 하지 해야 합니다. 사용자 계정에 대 한 암호를 변경 될 때마다 암호를 자동으로 변경 됩니다. Office 365에서 온라인 암호를 변경 하는 경우 암호 동기화 중단 됩니다.  
  
 이 섹션의 절차를 사용:  
  
-   [기존 사용자 계정에 대 한 온라인 계정을 대량 만들기](#BKMK_ToBulkCreateOnlineAccounts)  
  
-   [Microsoft Online Services 계정에서 사용자 계정을 가져오기](#BKMK_ToImportUserAccounts)  
  
-   [새 사용자 계정에 할당 온라인 계정을 사용 하 여 만들기](#BKMK_ToCreateaNewUserAccount)  
  
-   [한 온라인 계정을 사용자 계정에 할당](#BKMK_ToAssignAnOnlineAccount)  
  
> [!NOTE]
>  표시 하면 Windows Server Essentials을 사용 하 여 *Office 365 계정이* 대신 *Microsoft Online Services 계정* 이 절차 전체 합니다. 프로세스는 같지만 용어 Windows Server Essentials의 변경 합니다.  
  
###  <a name="BKMK_ToBulkCreateOnlineAccounts"></a>대량 만드는 기존 사용자 계정에 대 한 온라인 계정을  
  
1.  관리자 권한 서버에에 로그인 하 고 Windows Server Essentials 대시보드 엽니다.  
  
2.  대시보드에서 열고는 **사용자** 페이지 합니다.  
  
3.  **사용자가 작업**, 클릭 **추가 Microsoft 온라인 계정**합니다.  
  
     **Microsoft Online Services 추가 계정** 페이지 마법사의 모든 사용자 계정에 온라인 Microsoft 계정이 없는 표시 됩니다. 기본적으로 모든 계정이 선택 됩니다 및 사용자 이름을 Microsoft 온라인 id 추천 Office 365를 구독 하 고 사용자 정의 인터넷 도메인 연결할 경우 그 도메인 기본적으로 사용 됩니다.  
  
4.  에 **Microsoft Online Services 추가 계정** 페이지에서 계정을 만들 수 있는 검토 합니다. 예를 들어, 사용자가 이미 다른 온라인 ID 가진 한 온라인 계정을 고 메일 주소를 사용 하려는 도메인 선택 되어 있는지 확인 확인 합니다. 변경 필요한 모든 것 완료, 클릭 **다음**합니다.  
  
5.  에 **지정 Microsoft 온라인 서비스 라이선스** 페이지를 선택 하 고 Office 365 서비스에 사용자가 사용 합니다. 클릭 하면 **다음**, 계정 만들기를 시작 합니다.  
  
    > [!NOTE]
    >  각 온라인 계정에 대 한에서 Office 365 서비스 라이선스가 있어야 합니다. 사용 가능한 사용자 라이선스를 확인 하 고, 필요한 경우 열 수 구독에서 라이선스를 추가 하 고 **Office 365** 대시보드에서 페이지 합니다.  
  
6.  온라인 Microsoft 계정 이제 있는 사용자에 게 알립니다. Office 365에 로그인 할 수를 해당 네트워크 사용자 계정의 암호를 변경 해야 있습니다. 자세한 내용은 [새로운 온라인 Microsoft 계정 사용을 시작 하려면](#BKMK_ToBeginUsingAnOnlineAccount)합니다.  
  
###  <a name="BKMK_ToBeginUsingAnOnlineAccount"></a>새 온라인 Microsoft 계정 사용을 시작 하려면  
  
1.  네트워크 사용자 계정으로 컴퓨터에 로그인 합니다.  
  
2.  사용자 계정의 암호를 변경 합니다. 시작 하려면 Ctrl + Alt + delete를 누르고 **는 암호가 변경**합니다.  
  
     암호를 변경 하는 경우 암호 온라인 새로운 계정으로 동기화 됩니다. 이제 Office 365에 로그인 하는 동일한 암호를 사용할 수 있습니다.  
  
3.  [Office 365에 로그인](https://login.microsoftonline.com/login.srf?wa=wsignin1.0&rpsnv=3&ct=1398981834&rver=6.1.6206.0&wp=MBI_SSL&wreply=https:%2F%2Foutlook.office365.com%2Fowa%2F&id=260563&CBCXT=out) 새 온라인 ID 사용자와 사용자 계정 암호를 사용 하 여 합니다.  
  
    > [!IMPORTANT]
    >  Office 365에서 온라인 계정 암호를 변경 하지 않습니다. 암호 동기화는이 중단 됩니다. 온라인 암호 될 때마다 암호를 변경 하 여 네트워크 사용자 계정에 대 한 업데이트 됩니다.  
  
###  <a name="BKMK_ToImportUserAccounts"></a>기존 계정을 온라인에서 사용자 계정 가져오려면  
  
1.  대시보드에서 열고는 **사용자** 페이지 합니다.  
  
2.  **사용자가 작업**, 클릭 **Office 365에서 계정이 가져오기**합니다.  
  
     다음 페이지 표시 서버에 사용자 계정이 없는 Office 365 구독에 대 한 모든 온라인 계정 합니다. 기본적으로 모든 계정이 선택 됩니다 및 사용자 이름에 대 한 온라인 ID이 좋습니다.  
  
3.  사용자 계정을 만들려면 다음과 같습니다.  
  
    1.  제안 된 사용자 계정에 필요한 변경 합니다.  
  
    2.  필요에 따라 사용자 계정에 할당 될 임시 암호를 볼 수 있는 링크를 클릭 합니다. 자녀의 새 계정 이름 함께 임시 암호를 사용자에 게 제공 해야 합니다.  
  
         (하면 자 찾기 이러한 암호가이 파일에 나열 된 계정을 만든 후: *SystemDrive*\Users\\*Office365admin*\\*NewServerUser*.txt 어디 *Office365admin* 서버에 Office 365를 관리 하는 데 사용 되는 네트워크 계정 및 *NewServerUser* 새 사용자 계정 이름입니다.)  
  
    3.  클릭 **다음** 사용자 계정을 만들 수 있습니다.  
  
4.  사용자를 게 알립니다 새로운 사용자 계정 및 임시 암호에 대 한 첫 번째 시간 œ 서버에 로그인 할 사용할지 및에 로그인 한 후 암호를 변경 해야 합니다. 사용자를 위한 지침을 참조 하세요. [새로운 온라인 Microsoft 계정 사용을 시작 하려면](#BKMK_ToBeginUsingAnOnlineAccount)합니다.  
  
     앞으로 사용자 계정과 온라인 자신의 계정에 대 한 암호를 동기화 할 및 Office 365에서 자녀가 온라인 암호를 변경 하지 않아야 알고 있더라도 해야 합니다.  
  
###  <a name="BKMK_ToCreateaNewUserAccount"></a>새 사용자 계정에 할당 한 온라인 계정을 만들  
  
1.  클릭 하 고 대시보드에서 **사용자**합니다.  
  
2.  **사용자가 작업**, 클릭 **사용자 계정을 추가**합니다. 추가 사용자 계정 마법사 나타납니다.  
  
3.  사용자 계정 만들기 지침을 따릅니다.  
  
4.  에 **Microsoft Online Services 계정을** 페이지 만들거나 새 온라인 지정 된 기존 온라인 계정 또는 사용자 계정 다음과 같습니다.  
  
    -   새로운 온라인 계정을 만들려면 클릭 **새로운 Microsoft Online Services 계정을 만들고이 사용자 계정에 할당**, 온라인 서비스 Microsoft 계정에 대해 이름을 입력 하 고 (기본적으로 사용자 이름을 사용에 대 한 온라인 ID). 클릭 한 다음 **다음**합니다.  
  
    -   기존 온라인 Microsoft 계정에 할당 하려면 클릭 **기존 Microsoft Online Services 계정을이 사용자 계정에 할당**, 기존 계정을 드롭다운 목록에서 선택 합니다. 클릭 한 다음 **다음**합니다.  
  
    > [!NOTE]
    >  Windows Server Essentials Microsoft Online Services 계정을 마법사 및 대시보드 레이블에서 Office 365 계정 이라고 합니다.  
  
5.  마법사를 완료 하 고 지침을 따릅니다.  
  
6.  온라인 새로운 계정으로 Office 365에 로그인 수 전에 해당 사용자 계정 암호를 변경 해야 하는 사용자를 게 알립니다. 자세한 내용은 [새로운 온라인 Microsoft 계정 사용을 시작 하려면](#BKMK_ToBeginUsingAnOnlineAccount)합니다.  
  
#### <a name="BKMK_ToAssignAnOnlineAccount"></a>한 온라인 계정을 사용자 계정에 할당 하려면  
  
1.  클릭 하 고 대시보드에서 **사용자**합니다.  
  
2.  사용자 계정 목록에서 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **온라인 Microsoft 계정에 할당**합니다. 할당 Microsoft Online Services 계정 마법사 나타납니다.  
  
3.  지정 된 기존 온라인 계정 또는 사용자에 대 한 새 앨범 만들기. 새 계정에 대 한 기본 온라인 ID 사용자 이름입니다. 클릭 한 다음 **다음** 온라인 계정을 사용자 계정에 추가 합니다.  
  
4.  마법사의 마지막 페이지에서 정보를 검토 한 다음 클릭 **닫기**합니다.  
  
5.  온라인 새로운 계정으로 Office 365에 로그인 수 전에 해당 사용자 계정 암호를 변경 해야 하는 사용자를 게 알립니다. 자세한 내용은 [새로운 온라인 Microsoft 계정 사용을 시작 하려면](#BKMK_ToBeginUsingAnOnlineAccount)합니다.  
  
##  <a name="BKMK_SECTION_ManageOnlineAccounts"></a>온라인 계정 관리  
 Windows Server Essentials의 사용자 계정에 한 온라인 계정을 추가 하면 함께 계정 s 수명 주기 동안 두 계정 모두 관리할 수 있습니다.  
  
###  <a name="BKMK_UnderstandingAccountStatus"></a>온라인 계정 상태를 이해  
 Microsoft Online Services 계정을 사용자 계정에 할당 하면 해당 계정의 메일 주소에 표시는 **온라인 Microsoft 계정** 열에는 **사용자** 대시보드의 페이지 합니다. (Windows Server Essentials 열 레이블은 **Office 365 계정이**.)  
  
-   메일 주소 옆의 파란색 아이콘 온라인 계정이 활성화 되어 나타냅니다. 즉, 계정에 현재 Office 365 라이선스 및 사용자 온라인 ID를 사용 하 여 Office 365에 로그인 할 수 있습니다.  
  
-   메일 주소 옆에 있는 회색으로 표시 된 아이콘 온라인 계정 나타냅니다 때문에 비활성 œ 하거나 라이선스는 더 이상 활성화 또는 온라인 계정에 할당 된 되었습니다. 사용자 s 온라인 계정 할당 라이선스 제거 되 고 사용자가 계정을 사용 하 여 Office 365에 로그인 차단 됩니다. 그러나 서버에서 사용자 계정 이름을와 Office 365 메일 주소가 매핑을 유지합니다.  
  
###  <a name="BKMK_UnassignOnlineAccount"></a>온라인 계정에 대 한 액세스를 제한  
 사용자가, 조직 또는 Office 365 서비스에 사용자의 액세스를 제한 하려면 어떻게 해야 할까요? Windows Server Essentials에서 계정의 사용자와 사용자가 온라인 계정을 관리 하는 경우 세 가지 옵션이 있습니다.  
  
-   **온라인 계정 해제** 있나요? 사용자가 Office 365를 사용 하 여 서버에 리소스에 대 한 액세스를 방지를 않고도 유지 하려는 경우 온라인 계정 할당 해제 해야 합니다. Office 365 라이선스를 해제 하 고 사용자가 Office 365에 로그인 차단 됩니다. 그러나 서버에서 사용자 계정 이름을와 Office 365 메일 주소가 매핑을 유지합니다. 자세한 내용은 [한 온라인 계정을 사용자 계정에서 할당 하지 않으려면](#BKMK_ToUnassignAnOnlineAccount)합니다.  
  
-   **사용자 계정이 비활성화** 있나요? 일시적으로 또는 영구적으로 직원 잎 때문에 사용자 계정이 비활성화 하면 사용자 s 온라인 계정 또한 비활성화 됩니다. 온라인 계정을 사용할 수 없으며 되지만 사용자 데이터를 포함 하 여 메일, Microsoft Online Services에 유지 됩니다. 자세한 내용은 [사용자 계정이 비활성화](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage6) 에 [사용자 계정 관리](Manage-User-Accounts-in-Windows-Server-Essentials.md)합니다.  
  
-   **사용자 계정을 제거** 있나요? 사용자 계정을 제거 하면, Microsoft Online Services에서도 온라인 계정 제거 됩니다. 자세한 내용은 [사용자 계정을 제거](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Remove) 에 [사용자 계정 관리](Manage-User-Accounts-in-Windows-Server-Essentials.md)합니다.  
  
    > [!WARNING]
    >  한 온라인 계정을 제거 되 면 사용자 데이터는 따릅니다 데이터 보존 정책 Microsoft Online Services에 주의 해야 합니다. 직원이 벗어나면 사람의 사용자 데이터를 유지 해야 하는 경우 제거 하는 대신 사용자 계정이 비활성화 합니다.  
  
####  <a name="BKMK_ToUnassignAnOnlineAccount"></a>사용자 계정에서 온라인 계정 해제 하려면  
  
1.  클릭 하 고 대시보드에서 **사용자**합니다.  
  
2.  사용자 계정 목록에서 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **온라인 Microsoft 계정에 할당 해제** (Windows Server Essentials 클릭 **Office 365 계정이 해제**).  
  
3.  명령 프롬프트에 클릭 **예**합니다.  
  
##  <a name="BKMK_SECTION_ManageEmailAddresses"></a>Exchange Online에 대 한 메일 주소를 관리  
 Windows Server Essentials의 온라인 s 사용자 계정에 메일 주소를 추가 하 여 사용자에 게 Exchange 온라인에서 여러 이메일 주소 메일을 수신 허용할 수 있습니다.  
  
###  <a name="BKMK_PROC_AddEmailAliases"></a>사용자 s 온라인 Microsoft 계정에 추가 이메일 주소를 추가 하려면  
  
1.  Windows Server Essentials 대시보드에서 클릭 **사용자**합니다.  
  
2.  사용자 계정 목록에서 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **계정 속성 보기**합니다.  
  
3.  에 **Microsoft 온라인** 계정 속성을 탭 (또는 **Office 365** Windows Server Essentials의 탭)를 클릭 **추가**합니다.  
  
4.  새 메일 별칭 입력 한 다음 메일 도메인을 선택 합니다.  
  
5.  클릭 **확인** 두 번 합니다.  
  
##  <a name="BKMK_SECTION_ManageDistributionGroups"></a>Exchange Online (Windows Server Essentials에만 해당)에 대 한 메일 그룹 관리  
 Windows Server Essentials 서버 Office 365와 통합 하면 만들 수 있으며 Windows Server Essentials 대시보드에서 온라인 거래소에 대 한 메일 그룹 관리. 자 하면이 작업을 **메일 그룹** 탭에 추가 되는 **사용자** 페이지 합니다. 이 탭 Exchange Online 구독 하는 경우에 표시 됩니다. 이 기능은 Windows Server Essentials에서 사용할 수 없습니다.  
  
 다음 절차를 사용 하 여 다음과 같습니다.  
  
-   [메일 추가](#BKMK_PROCEDURE_AddDistGroup)  
  
-   [메일 그룹의 회원 변경](#BKMK_ChangeGroupMembers)  
  
-   [사용자의 메일 그룹 구성원 변경](#BKMK_EditUserMemberships)  
  
-   [그룹 메일 제거](#BKMK_RemoveDistributionGroup)  
  
###  <a name="BKMK_PROCEDURE_AddDistGroup"></a>메일 그룹을 추가 하려면  
  
1.  Windows Server Essentials의 대시보드에서 클릭 **사용자**을 차례로 클릭 하 고 있는 **메일 그룹** 탭 합니다.  
  
2.  **작업 메일을 그룹화**, 클릭 **메일 그룹 추가**합니다.  
  
     추가 새 메일 그룹 마법사 나타납니다.  
  
3.  에 **메일 그룹을 새로 추가** 페이지 다음 정보를 입력 한 다음 클릭 **다음**:  
  
    -   새 메일 그룹에 대 한 그룹 이름, 면 설명 및 메일 별칭을 입력 합니다.  
  
    -   기본적으로 메일 그룹 조직 외부에 있는 사용자의 메일을 받을 수 있습니다. 이 허용 하지 않으려면 해당 옵션 선택을 취소 합니다.  
  
4.  에 **그룹 구성원을 추가** 페이지에서 사용 하는 **추가** 단추, 할당 된 온라인 계정이 활성 사용자 계정을 추가 하 고 새 메일 그룹에 다른 메일을 그룹화 합니다. 클릭 한 다음 **다음**합니다.  
  
     새 메일 그룹 Exchange Online 생성 됩니다.  
  
###  <a name="BKMK_ChangeGroupMembers"></a>메일 그룹의 회원 변경 하려면  
  
1.  대시보드에서 클릭 **사용자가**을 차례로 클릭 하 고는 **메일 그룹** 탭 합니다.  
  
2.  목록에서 메일 그룹 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **그룹 구성원 변경**합니다.  
  
3.  사용 하는 **추가** 및 **제거** 단추를 추가 하거나 메일 그룹에서 온라인 활성 계정을 제거 합니다. 클릭 한 다음 **다음** Exchange Online에서 메일 그룹 구성원 업데이트할 수 있습니다.  
  
###  <a name="BKMK_EditUserMemberships"></a>사용자의 메일 그룹 구성원을 변경 하려면  
  
1.  클릭 하 고 대시보드에서 **사용자**합니다.  
  
2.  사용자 계정 목록에서 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **계정 속성 보기**합니다.  
  
3.  사용자 계정 속성 클릭는 **메일 그룹** 탭을 클릭 한 다음 **편집**합니다.  
  
4.  에 **편집 그룹 구성원** 상자를 사용 하는 **추가** 및 **제거** 단추를 추가 하거나 메일 그룹 사용자 계정에서 제거 클릭 한 다음 **닫기**합니다.  
  
5.  클릭 **확인** 업데이트 사용자 계정 속성 저장할 수 있습니다.  
  
###  <a name="BKMK_RemoveDistributionGroup"></a>그룹 메일을 제거 하려면  
  
1.  대시보드에서 클릭 **사용자가**을 차례로 클릭 하 고는 **메일 그룹** 탭 합니다.  
  
2.  목록에서 메일 그룹 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **그룹 제거**합니다.  
  
3.  명령 프롬프트에 클릭 **그룹 삭제**합니다.  
  
     메일 그룹 Exchange Online에서 제거 됩니다.  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [사용자 계정 관리](Manage-User-Accounts-in-Windows-Server-Essentials.md)  
  
-   [Office 365 관리](Manage-Office-365-in-Windows-Server-Essentials.md)  
  
-   [Microsoft Online Services 관리](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)
