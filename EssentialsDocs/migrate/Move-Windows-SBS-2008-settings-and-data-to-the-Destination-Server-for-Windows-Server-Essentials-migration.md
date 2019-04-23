---
title: Windows Server Essentials 마이그레이션을 위해 대상 서버에 Windows SBS 2008 설정 및 데이터 이동
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4950469d-d800-430d-8d10-53bafc4a9932
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 14a9ab8b4cc18f9c71af6207b854f34af3fa3d17
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843914"
---
# <a name="move-windows-sbs-2008-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Windows Server Essentials 마이그레이션을 위해 대상 서버에 Windows SBS 2008 설정 및 데이터 이동

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

다음과 같이 설정 및 데이터를 대상 서버로 이동합니다.  
  

1.  [대상 서버에 데이터 복사](Move-Windows-SBS-2008-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_CopyData)  
  
2.  [(선택 사항) Windows Server Essentials 대시보드에 Active Directory 사용자 계정 가져오기](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_ImportADaccounts)  
  
3.  [원본 서버에서 DHCP 서버 역할을 라우터로 이동](Move-Windows-SBS-2008-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_MoveDHCP)  
  
4.  [네트워크 구성](Move-Windows-SBS-2008-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_Network)  
  
5.  [(선택 사항) 레거시 Active Directory 그룹 정책 개체 제거](Move-Windows-SBS-2008-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_RemoveLegacyADGPO)  
  
6.  [사용자 계정에 허용 되는 컴퓨터 매핑](Move-Windows-SBS-2008-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_MapPermittedComputers)  
  
##  <a name="BKMK_CopyData"></a> 대상 서버에 데이터 복사  
 원본 서버에서 대상 서버로 데이터를 복사하기 전에 다음 작업을 수행합니다.  
  
-   각 폴더에 대한 사용 권한을 비롯하여 원본 서버의 공유 폴더 목록을 검토합니다. 원본 서버에서 마이그레이션할 폴더 구조와 일치하도록 대상 서버에서 폴더를 만들거나 사용자 지정합니다.  
  
-   각 폴더의 크기를 검토하고 대상 서버에 충분한 저장 공간이 있는지 확인합니다.  
  
-   파일을 대상 서버에 복사하는 동안 드라이브에서 쓰기를 수행할 수 있도록 원본 서버에서 공유 폴더를 모든 사용자에게 읽기 전용으로 설정합니다.  
  
#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>원본 서버에서 대상 서버로 데이터를 복사하려면  
  
1.  도메인 관리자로 대상 서버에 로그온하고 명령 창을 엽니다.  
  
2.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다.  
  
    `robocopy \\<SourceServerName> \<SharedSourceFolderName> \\<DestinationServerName> \<SharedDestinationFolderName> /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`  
  
     각 항목이 나타내는 의미는 다음과 같습니다.
     - \<SourceServerName\> 원본 서버의 이름
     - \<SharedSourceFolderName\> 원본 서버의 공유 폴더의 이름
     - \<DestinationServerName\> 대상 서버의 이름
     - \<SharedDestinationFolderName\> 데이터를 복사할 대상 서버의 공유 폴더입니다.  
  
3.  원본 서버에서 마이그레이션할 각 공유 폴더에 대해 이전 단계를 반복합니다.  
  
##  <a name="BKMK_ImportADaccounts"></a> (선택 사항) Windows Server Essentials 대시보드에 Active Directory 사용자 계정 가져오기  
 기본적으로 원본 서버에서 만든 모든 사용자 계정은 Windows Server Essentials의 대시보드로 자동으로 마이그레이션됩니다. 그러나 일부 속성이 마이그레이션 요구 사항을 충족하지 않으면 Active Directory 사용자 계정의 자동 마이그레이션이 실패합니다. 다음 Windows PowerShell cmdlet을 사용하여 Active Directory 사용자를 가져올 수 있습니다.  
  
#### <a name="to-import-an-active-directory-user-account-to-the-windows-server-essentials-dashboard"></a>Active Directory 사용자 계정을 Windows Server Essentials 대시보드를 가져오려면  
  
1.  도메인 관리자로 대상 서버에 로그온합니다.  
  
2.  관리자 권한으로 Windows PowerShell을 엽니다.  
  
3.  다음 cmdlet을 실행합니다. 여기서 `[AD username]` 은 가져오려는 Active Directory 사용자 계정의 이름입니다.  
  
     `Import-WssUser  SamAccountName [AD username]`  
  
##  <a name="BKMK_MoveDHCP"></a> 원본 서버에서 DHCP 서버 역할을 라우터로 이동  
 원본 서버에서 DHCP 역할을 실행하고 있으면 다음 단계를 수행하여 DHCP 역할을 라우터로 이동합니다.  
  
#### <a name="to-move-the-dhcp-role-from-the-source-server-to-the-router"></a>원본 서버에서 라우터로 DHCP 역할을 이동하려면  
  
1.  다음과 같이 원본 서버에서 DHCP 서비스를 끕니다.  
  
    1.  원본 서버에서 **시작**, **관리 도구**, **서비스**를 차례로 클릭합니다.  
  
    2.  현재 실행 중인 서비스 목록에서 **DHCP 서버**를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
    3.  **시작 유형**으로 **사용 안 함**을 선택합니다.  
  
    4.  서비스를 중지합니다.  
  
2.  라우터에서 DHCP 역할을 켭니다.  
  
    1.  라우터 설명서의 지침에 따라 라우터에서 DHCP 역할을 켭니다.  
  
    2.  원본 서버에서 발급된 IP 주소를 동일하게 유지하려면 라우터 설명서의 지침에 따라 라우터의 DHCP 범위를 원본 서버의 DHCP 범위와 동일하게 구성합니다.  
  
        > [!IMPORTANT]
        >  대상 서버에 대한 라우터에서 고정 IP 또는 DHCP 예약을 설정하지 않았고 DHCP 범위가 원본 서버와 다르면 라우터에서 대상 서버에 대한 새 IP 주소를 발급할 수 있습니다. 이 문제가 발생하면 라우터의 대상 서버의 새 IP 주소를 전달하도록 포트 전달 규칙을 다시 설정합니다.  
  
##  <a name="BKMK_Network"></a> 네트워크 구성  
 DHCP 역할을 라우터로 이동하고 나서 대상 서버에서 네트워크 설정을 구성합니다.  
  
#### <a name="to-configure-the-network"></a>네트워크를 구성하려면  
  
1.  대상 서버에서 대시보드를 엽니다.  
  
2.  대시보드 **홈** 페이지에서 **설정**, **원격 액세스 설정**을 차례로 클릭하고 **원격 액세스를 구성하려면 클릭** 옵션을 선택합니다.  
  
3.  마법사의 지침을 완료하여 라우터 및 도메인 이름을 구성합니다.  
  
 라우터에서 UPnP 프레임워크를 지원하지 않거나 UPnP 프레임워크가 사용되지 않으면 라우터 이름 옆에 노란색 경고 아이콘이 나타날 수 있습니다. 다음 포트가 열려 있으며 대상 서버의 IP 주소로 보내지는지 확인합니다.  
  
-   포트 80: HTTP 웹 트래픽  
  
-   포트 443: HTTPS 웹 트래픽  
  
> [!NOTE]
>  두 번째 서버에서 온-프레미스 Exchange Server를 설정한 경우 포트 25(SMTP)가 열려 있고 온-프레미스 Exchange Server의 IP 주소로 리디렉션되는지 확인해야 합니다.  
  
##  <a name="BKMK_RemoveLegacyADGPO"></a> (선택 사항) 레거시 Active Directory 그룹 정책 개체 제거  
 그룹 정책 개체 (Gpo)를 Windows Server Essentials에 대 한 업데이트 됩니다. 이 GPO는 Windows SBS 2008 GPO의 하위 집합입니다. Windows Server Essentials에 대 한 여러 Windows SBS 2008 Gpo 및 Windows Management Instrumentation (WMI) 필터는 Windows Server Essentials Gpo 및 WMI 필터를 사용 하 여 충돌을 방지 하려면 수동으로 삭제 해야 합니다.  
  
> [!NOTE]
>  원래 Windows SBS 2008 그룹 정책 개체를 수정한 경우 복사본을 다른 위치에 저장하고 Windows SBS 2008에서 삭제해야 합니다.  
  
#### <a name="to-remove-old-group-policy-objects-from-windows-sbs-2008"></a>Windows SBS 2008에서 이전 그룹 정책 개체를 제거하려면  
  
1.  관리자 계정으로 원본 서버에 로그온합니다.  
  
2.  **시작**을 클릭한 다음 **서버 관리**를 클릭합니다.  
  
3.  탐색 창에서 클릭 **Advanced Management**, 클릭 **그룹 정책 관리**를 클릭 하 고 **포리스트: * * * < YourDomainName\>* 합니다.  
  
4.  클릭 **도메인**, 클릭 *< YourDomainName\>* 를 클릭 하 고 **그룹 정책 개체**합니다.  
  
5.  **Small Business Server 감사 정책**을 마우스 오른쪽 단추로 클릭하고 **삭제**, **확인**을 차례로 클릭합니다.  
  
6.  5단계를 반복하여 네트워크에 적용된 다음 GPO를 삭제합니다.  
  
    -   Small Business Server 클라이언트 컴퓨터  
  
    -   Small Business Server 도메인 암호 정책  
  
         강력한 암호를 적용 하도록 Windows Server Essentials에서 암호 정책을 구성 하는 것이 좋습니다. 암호 정책을 구성하려면 대시보드를 사용하여 기본 도메인 정책에 구성을 씁니다. Windows SBS 2008에서와 마찬가지로 암호 정책 구성은 Small Business Server 도메인 암호 정책 개체에 기록되지 않습니다.  
  
    -   Small Business Server 인터넷 연결 방화벽  
  
    -   Small Business Server 잠금 정책  
  
    -   Small Business Server 원격 지원 정책  
  
    -   Small Business Server Windows 방화벽  
  
    -   Small Business Server Update Services 클라이언트 컴퓨터 정책  
  
         이 GPO는 Windows SBS 2008 R2에서 마이그레이션하는 경우 표시됩니다.  
  
    -   Small Business Server Update Services 공용 설정 정책  
  
         이 GPO는 Windows SBS 2008 R2에서 마이그레이션하는 경우 표시됩니다.  
  
    -   Small Business Server Update Services 서버 컴퓨터 정책  
  
         이 GPO는 Windows SBS 2008 R2에서 마이그레이션하는 경우 표시됩니다.  
  
7.  모든 GPO가 삭제되었는지 확인합니다.  
  
#### <a name="to-remove-wmi-filters-from-windows-sbs-2008"></a>Windows SBS 2008에서 WMI 필터를 제거하려면  
  
1.  관리자 계정으로 원본 서버에 로그온합니다.  
  
2.  **시작**을 클릭한 다음 **서버 관리**를 클릭합니다.  
  
3.  탐색 창에서 클릭 **Advanced Management**, 클릭 **그룹 정책 관리**를 클릭 하 고 **포리스트: * * * < YourNetworkDomainName\>*  
  
4.  클릭 **도메인**, 클릭 *< YourNetworkDomainName\>* 를 클릭 하 고 **WMI 필터**합니다.  
  
5.  **PostSP2**를 마우스 오른쪽 단추로 클릭하고 **삭제**, **예**를 차례로 클릭합니다.  
  
6.  **PreSP2**를 마우스 오른쪽 단추로 클릭하고 **삭제**, **예**를 차례로 클릭합니다.  
  
7.  이러한 세 가지 WMI 필터가 삭제되었는지 확인합니다.  
  
##  <a name="BKMK_MapPermittedComputers"></a> 사용자 계정에 허용 되는 컴퓨터 매핑  
 Windows SBS 2008에서는 사용자가 원격 웹 액세스에 연결하면 네트워크에 있는 모든 컴퓨터가 표시됩니다. 여기에는 사용자에게 액세스 권한이 없는 컴퓨터가 포함될 수 있습니다. Windows Server Essentials에서 사용자 원격 웹 액세스에 표시할 컴퓨터를 명시적으로 할당 되어야 합니다. Windows SBS 2008에서 마이그레이션된 각 사용자 계정을 하나 이상의 컴퓨터에 매핑해야 합니다.  
  
#### <a name="to-map-user-accounts-to-computers"></a>사용자 계정을 컴퓨터에 매핑하려면  
  
1.  Windows Server Essentials 대시보드를 엽니다.  
  
2.  탐색 모음에서 **사용자**를 클릭합니다.  
  
3.  사용자 계정 목록에서 사용자 계정을 마우스 오른쪽 단추로 클릭하고 **계정 속성 보기**를 클릭합니다.  
  
4.  **원격 액세스** 탭을 클릭하고 **원격 웹 액세스 허용 및 웹 서비스 응용 프로그램에 액세스**을 클릭합니다.  
  
5.  **공유 폴더**, **컴퓨터**, **홈페이지 링크**를 차례로 선택하고 **적용**을 클릭합니다.  
  
6.  **컴퓨터 액세스** 탭을 클릭하고 액세스를 허용할 컴퓨터 이름을 클릭합니다.  
  
7.  각 사용자 계정에 대해 3, 4, 5, 6단계를 반복합니다.  
  
> [!NOTE]
>  클라이언트 컴퓨터의 구성을 변경할 필요가 없습니다. 자동으로 구성됩니다.  
  
> [!NOTE]
>  마이그레이션을 완료하고 나서 대상 서버에서 첫 번째 새 사용자 계정을 만들 때 문제가 발생하면 추가한 사용자 계정을 제거하고 다시 만듭니다.
