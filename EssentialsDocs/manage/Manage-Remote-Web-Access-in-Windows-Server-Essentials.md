---
title: "Windows Server Essentials의 원격 Web Access 관리"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f3ea40fa-b6ba-4d66-b754-221ca6271387
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: de01b2fd2395377b6e7b3349b9862eb0e51a59b8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="manage-remote-web-access-in-windows-server-essentials"></a>Windows Server Essentials의 원격 Web Access 관리

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.
 
 원격 Web Access Windows Server Essentials 또는 Windows Server 2012 r 2를 설치 하는 Windows Server Essentials 경험 역할와 응용 프로그램 및 인터넷에 연결 되어 있는 어디에서 나의 데이터에 액세스 하기 위한 및 거의 모든 디바이스를 사용 하 여 능률적인을 쉽게 터치 할 브라우저 환경의 제공 됩니다. 웹에 대 한 원격 액세스 기능을 사용 하려면 먼저 설정 어디서 나 액세스 마법사를 사용 하 여 설정 고 라우터와 도메인 이름을 설정 해야 합니다.  
  
## <a name="in-this-topic"></a>이 항목에서  
  
-   [설정 하 고 구성할 원격 웹 액세스](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [라우터에서 설정](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [도메인 이름 설정](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [원격 웹 액세스를 사용자 지정](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [원격 Web Access 문제 해결](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_5)  
  
##  <a name="BKMK_1"></a>설정 하 고 구성할 원격 웹 액세스  
 다음 항목을 켜고 원격 Web Access 구성 데 도움이 됩니다.  
  
-   [원격 Web Access 개요](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Overview)  
  
-   [원격 Web Access 켜기](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_TurnOnRWA)  
  
-   [지역 변경](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Region)  
  
-   [웹에 대 한 원격 액세스 권한을 관리합니다](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ManagePerms)  
  
-   [보안 원격 웹 액세스](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SecureRWA)  
  
-   [사용자가 원격 Web Access 및 VPN 관리](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ManageRWAVPN)  
  
###  <a name="BKMK_Overview"></a>원격 Web Access 개요  
 사무실 밖에 있을 때 웹 브라우저를 열고 및 원격 Web Access 인터넷에 연결 되어 있는 어디에서 든 액세스할 수 있습니다. 원격 Web access에서 다음을 수행할 수 있습니다.  
  
-   서버에서 파일 및 폴더 공유 액세스 합니다.  
  
-   서버와 네트워크의 컴퓨터에 액세스 합니다. 즉, 경우 사무실 앞에 앉아 있는 것 처럼 데스크톱 네트워크에 연결 된 컴퓨터에 액세스할 수 있습니다.  
  
  원격 Web Access는 기본적으로 켜져 있지 합니다. 설정 어디서 나 액세스 마법사를 실행 하면 마법사 라우터 및 인터넷 연결을 설정 하려고 합니다. 원격 Web Access 켜진 후 서버에 대 한 도메인 이름을 설정 하 고 웹에 대 한 원격 액세스를 사용자 지정할 수 있습니다. 설정할 수도 있습니다 라우터를 다시 라우터를 변경 합니다.  
  
 새 사용자 계정을 추가 하면 Web Access 원격 액세스할 수 있는 권한은 자동으로 부여 되지는 않습니다. 사용자 계정을 추가 하면, 공유 폴더, 미디어 라이브러리, 컴퓨터, 홈페이지 링크 및 대시보드 서버에 대 한 액세스를 허용 하도록 선택할 수 있습니다. 또한 사용자 사용 웹에 대 한 원격 액세스 허용 되지 지정할 수 있습니다.  
  
 원격 Web Access 설정을 각 사용자 계정에 대해에 표시 되는 **사용자** Windows Server Essentials 대시보드의 탭 합니다. Web Access 원격 설정을 변경 하려면 사용자 계정에 마우스 오른쪽 단추로 클릭 한 다음 **계정 속성 보기**합니다.  
  
###  <a name="BKMK_TurnOnRWA"></a>원격 Web Access 켜기  
 웹에 대 한 원격 액세스 대시보드 서버에서 원하는 위치에 액세스 마법사 설정을 실행 하 여 켤 수 있습니다.  
  
##### <a name="to-turn-on-remote-web-access"></a>웹에 대 한 원격 액세스를 켜려면  
  
1.  대시보드를 엽니다.  
  
2.  클릭 **설정**을 차례로 클릭 하 고 있는 **원하는 위치에 액세스** 탭 합니다.  
  
3.  클릭 **구성**합니다. 설정 어디서 나 액세스 마법사 나타납니다.  
  
4.  에 **선택 어디서 나 액세스 기능을 사용 하도록 설정** 페이지를 선택 하 고는 **원격 Web Access** 확인란을 선택 합니다.  
  
5.  마법사를 완료 하 고 지침을 따릅니다.  
  
###  <a name="BKMK_Region"></a>지역 변경  
 Windows Server Essentials의 지역 설정을 변경 하는 네트워크 관리자 여야 합니다.  
  
##### <a name="to-change-the-region-setting"></a>지역 설정을 변경 하려면  
  
1.  Windows Server Essentials에 연결 하는 컴퓨터에서 대시보드를 엽니다.  
  
2.  클릭 **설정**합니다.  
  
3.  에 **일반** 탭을 클릭 하 고 드롭다운 목록에서는 **서버의 국가/지역 위치** 섹션.  
  
4.  드롭다운 목록에서 새로운 영역을 선택한 다음 **적용** 새로운 영역 설정을 적용 합니다.  
  
###  <a name="BKMK_ManagePerms"></a>웹에 대 한 원격 액세스 권한을 관리합니다  
 Windows Server Essentials의 사용자 계정에 추가 하면 새 사용자가 웹에 대 한 원격 액세스를 사용 하 여 기본적으로 수 있습니다. 사용자 계정에 대 한 원격 웹 액세스할 수 있도록 하 고 사용자가 사용 하 여 웹 액세스 원격 해야 찾습니다을 하지 않을 경우 사용자 계정의 속성 업데이트할 수 있습니다.  
  
##### <a name="to-manage-remote-web-access-permissions-for-a-user-account"></a>사용자 계정에 대 한 원격 웹 액세스 권한을 관리  
  
1.  대시보드로 로그온 한 클릭 한 다음 **사용자**합니다.  
  
2.  사용자 계정 관리 및 클릭 한 다음 원하는 클릭 **계정 속성 보기** 에 **작업** 창 합니다.  
  
3.  에 **속성** 대화 상자를 클릭는 **액세스 어디서 나** 탭 합니다.  
  
4.  에 **원하는 위치에 액세스** 탭을 선택 하 고는 **웹 원격 액세스 허용와 웹 서비스 응용 프로그램에 대 한 액세스** 사용자가 사용 하 여 웹 액세스 원격 서버에 연결할 수 있도록 확인란을 선택 합니다.  
  
5.  클릭 **적용**을 차례로 클릭 하 고 **확인**합니다.  
  
 자세한 내용은 참조 [사용자 계정 관리](Manage-User-Accounts-in-Windows-Server-Essentials.md)합니다.  
  
###  <a name="BKMK_SecureRWA"></a>보안 원격 웹 액세스  
 Windows Server Essentials 간에 소프트웨어와 웹 브라우저 교환 되는 정보를 보호 하는 보안 인증서를 사용 합니다. 커넥터 소프트웨어를 컴퓨터에 설치한 경우 Windows Server Essentials의 보안 인증서 컴퓨터에서 신뢰할 수 있는 인증 목록에 추가 됩니다. 사무실 밖에 있을 때 원격 Web Access 액세스할 수 있는 사용자에 대 한 커넥터 소프트웨어가 설치 된 노트북을 사용 하는 가장 좋은 방법은 합니다.  
  
> [!WARNING]
>  컴퓨터에서 자동 이동 하기 전에 로그 오프할 웹 사이트 또는 세션으로 완료 되 면 사용자에 게 공개 위치에서 원격 Web Access 또는 신뢰할 수 없는 다른 컴퓨터를 사용 하 여 확인 해야 합니다.  
  
###  <a name="BKMK_ManageRWAVPN"></a>사용자가 원격 Web Access 및 VPN 관리  
 Windows Server Essentials에 연결 하는 서버에 저장 된 모든 리소스에 액세스 VPN을 사용할 수 있습니다. VPN 연결을 통해 호스팅된 Windows Server Essentials 서버에 연결 하는 데 사용 될 수 있는 네트워크 계정을 설정 하는 클라이언트 컴퓨터 하는 경우 특히 유용 합니다. 모든 새로 만든된 사용자 계정 여 호스팅된 Windows Server Essentials 서버에 처음으로 대 한 클라이언트 컴퓨터에 로그온 할 VPN을 사용 해야 합니다.  
  
##### <a name="to-set-vpn-and-remote-web-access-permissions-for-network-users"></a>VPN 및 웹에 대 한 원격 액세스 권한을 네트워크 사용자에 대 한 설정 하려면  
  
1.  대시보드를 엽니다.  
  
2.  탐색 모음에서 클릭 **사용자**합니다.  
  
3.  사용자 계정의 목록에서 원격 데스크톱에 액세스할 권한을 부여 하려는 사용자 계정을 선택 합니다.  
  
4.  에 **< 사용자 Account\ > 작업** 창 클릭 **속성**합니다.  
  
5.  **< 사용자 Account\ > 속성**를 클릭는 **어디서 나 액세스** 탭 합니다.  
  
6.  에 **어디서 나 액세스** 탭에서 다음을 수행 합니다.  
  
    1.  VPN을 사용 하 여 서버에 연결할 수 있도록 선택는 **허용 개인 VPN (가상)** 확인란을 선택 합니다.  
  
    2.  사용자가 웹에 대 한 원격 액세스를 사용 하 여 서버에 연결할 수 있도록 선택는 **웹 원격 액세스 허용와 웹 서비스 응용 프로그램에 대 한 액세스** 확인란을 선택 합니다.  
  
7.  클릭 **적용**을 차례로 클릭 하 고 **확인**합니다.  
  
##  <a name="BKMK_2"></a>라우터에서 설정  
 서버를 원격 Web access 구성 설정 어디서 나 액세스 마법사 라우터를 설정 하려고 합니다. 라우터 변경 하거나 라우터 설정을 변경할 경우 설정 나만의 라우터 마법사를 다시 실행 해야 합니다. 자세한 내용은 다음 항목을 참조 하십시오.  
  
-   [라우터에서 설정](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SetUpRouter)  
  
-   [라우터 바꾸기](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ReplaceRouter)  
  
-   [네트워크 위치 정의](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_NetworkLocation)  
  
-   [원격 데스크톱 서비스가 ActiveX 컨트롤 사용](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ActiveX)  
  
###  <a name="BKMK_SetUpRouter"></a>라우터에서 설정  
 이 단계 중 Windows Server Essentials 라우터 UPnP 명령을 사용 하 여 자동으로 구성할 하려고 합니다. 이 위해 라우터 UPnP 표준을 지원 해야 및 라우터의 UPnP 설정을 사용 해야 합니다.  
  
> [!NOTE]
>  네트워크 구성 Windows Server Essentials의 지원 되는 네트워크 요구 수행 해야 합니다. 네트워크에서 하나만 라우터 있어야 합니다.  
  
 라우터는 설정 나만의 도메인 이름 마법사도 설정 되지 않은 경우 수동으로 443 포트를 전달 해야 합니다. 라우터에서 포트 전달을 설정 하는 방법에 대 한 내용은 [라우터 설치](https://social.technet.microsoft.com/wiki/contents/articles/windows-small-business-server-2011-essentials-router-setup.aspx)합니다.  
  
###  <a name="BKMK_ReplaceRouter"></a>라우터 바꾸기  
 제조업체의 지침에 따라 라우터를 교체 하 고 설정 나만의 라우터 마법사 새로운 라우터 구성을 실행 합니다.  
  
##### <a name="to-set-up-your-new-router"></a>새 라우터를 설정 하려면  
  
1.  Windows Server Essentials 대시보드에서 클릭 **설정**합니다.  
  
2.  클릭는 **원하는 위치에 액세스** 탭을 선택한 다음는 **라우터** 섹션에서 클릭 **설정**합니다. 설정 나만의 라우터 마법사를 시작합니다.  
  
3.  새 라우터 설정을 완료 하 고 마법사의 지침을 따릅니다.  
  
###  <a name="BKMK_NetworkLocation"></a>네트워크 위치 정의  
 네트워크 위치는 Windows에서 해당 네트워크에 연결 하면 네트워크 설정 모음입니다. 설정을 다를 사용 하는 네트워크의 종류에 따라 지정할 수 있습니다. 네트워크 위치에 대 한 설정을 켜거나 끕니다 (예: 파일 및 프린터 공유, 네트워크 검색, 공용 폴더 공유) 일부 기능은 설정 되어 있는지 여부를 결정 합니다. 네트워크 위치는 서로 다른 네트워크에 연결 하려는 경우 유용 합니다.  
  
 예를 들어 집과 작업에 사용 하는 노트북 컴퓨터를 소유 수 있습니다. 사무실에 있을 때 네트워크에 연결 합니다. 그러나 하는 경우 home을 사용 하면 노트북에 액세스 하 고 동영상 및 홈 서버에 저장 된 음악을 재생 합니다. 새 네트워크에 연결 하 고 위치 종류를 지정 하는 경우 Windows 위치 유형의 사전 설정 된 네트워크 프로필을 할당 합니다. 다음 해당 네트워크에 연결할 때 Windows에서 네트워크를 인식 하 고 자동으로 올바른 설정을 지정. 이렇게 하면 보안 컴퓨터에서 정보를 보호 계층을 추가 하 고 해당 지역에 대 한 해야 하는 네트워크 기능이 켜져 합니다.  
  
 네 가지 유형의 네트워크 위치는 다음과 같습니다.  
  
-   **홈 네트워크** 때 신뢰 하는 사람과 네트워크에서 디바이스 또는 홈 네트워크에 대 한이 네트워크를 선택 합니다. 홈 그룹이 홈 네트워크의 컴퓨터 속할 수 있습니다. 네트워크 검색 네트워크에서 다른 컴퓨터 및 디바이스를 볼 수 있는 다른 네트워크 사용자의 컴퓨터를 볼 수 있게 홈 네트워크에 대 한 켜져 있습니다.  
  
-   **회사 네트워크** 소규모 사무실에 대 한이 네트워크 또는 다른 회사 네트워크를 선택 합니다. 네트워크에서 다른 컴퓨터 및 디바이스를 볼 수 있습니다. 및 기타 네트워크 사용자의 컴퓨터를 볼 수, 네트워크 검색 기본적으로 켜져 있지만 만들거나 홈 그룹에 연결할 수 없습니다.  
  
-   **공용 네트워크** 공공 장소 (예: 커피숍 나 공항)에 대 한이 네트워크를 선택 합니다. 이 위치는 다른 컴퓨터에 표시 되지 않도록 하 여 컴퓨터 유지 하 고 인터넷에서 악성 소프트웨어 로부터 사용자 컴퓨터를 보호 하기 위해 설계 되었습니다. 홈 그룹 공개 네트워크를 사용할 수 있으며 네트워크 검색 꺼져 있습니다. 또한 라우터를 사용 하지 않고 인터넷에 직접 연결 되어 또는 모바일 광대역 연결 되어 있는 경우이 옵션을 선택 해야 합니다.  
  
-   **도메인** 엔터프라이즈 직장에서 등과 같이 도메인에 대 한이 네트워크를 선택 합니다. 이러한 종류의 네트워크 위치는 네트워크 관리자에에서 관리 하 고 선택 하거나 변경할 수 있습니다.  
  
###  <a name="BKMK_ActiveX"></a>원격 데스크톱 서비스가 ActiveX 컨트롤 사용  
 원격 데스크톱 서비스가 ActiveX 컨트롤 웹에 대 한 원격 액세스를 사용 하 여 다른 컴퓨터에서 인터넷을 통해 홈 또는 비즈니스 컴퓨터에 액세스할 수 있습니다.  
  
##### <a name="to-enable-remote-desktop-services-activex-controls"></a>원격 데스크톱 서비스가 ActiveX 컨트롤을 사용 하려면  
  
1.  Internet Explorer 클릭 **도구**을 차례로 클릭 하 고 **인터넷 옵션**합니다.  
  
2.  에 **보안** 탭을 클릭 **사용자 지정 수준**합니다.  
  
3.  에 **ActiveX 컨트롤 및 플러그 인** 섹션 다음을 수행 하세요.  
  
    1.  아래에서 **서명 된 ActiveX 컨트롤 다운로드**, 클릭 **프롬프트**합니다.  
  
    2.  아래에서 **ActiveX 컨트롤 및 플러그 인**, 클릭 **활성화**합니다.  
  
4.  클릭 **확인** 두 번 하 여 변경 내용을 적용 하 고 대화 상자를 닫습니다.  
  
##  <a name="BKMK_3"></a>도메인 이름 설정  
 원격 Web Access 켜진 후 Windows Server Essentials 실행 하는 서버에 대 한 도메인 이름을 설정할 수 있습니다. 원격 컴퓨터에서 원격 Web Access 사용 하려는 경우 필요한 단계입니다. 자세한 내용은 다음 항목을 참조 하십시오.  
  
-   [도메인 이름 개요](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_DNOverview)  
  
-   [이해 개인 설정 된 Microsoft 도메인 이름](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_PersonalizedNames)  
  
-   [사용 하는 새로운 기능이 나 기존 도메인 이름](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_UseNewName)  
  
-   [도메인 이름 설정](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SetUpName)  
  
-   [도메인 이름 서비스 공급자를 선택 합니다.](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ChooseProvider)  
  
-   [도메인 이름 선택](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ChooseDomainName)  
  
-   [도메인 이름 접두사 선택](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Prefixes)  
  
-   [도메인 이름 확장명을 선택 합니다.](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Extension)  
  
-   [업데이트 하거나 도메인 이름 서비스 업그레이드](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_UpdateService)  
  
-   [내보내기 또는 서버의 인증서 가져오기](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ExportCert)  
  
-   [도메인 이름으로 수동으로 설정](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SetNameManually)  
  
-   [사용자 도메인 이름 서비스 공급자 찾기](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Find)  
  
###  <a name="BKMK_DNOverview"></a>도메인 이름 개요  
 도메인 이름 인터넷 서버를 고유 하 게 식별합니다. 두 대 이상의 부분으로 구성 됩니다 도메인 이름: 최상위 도메인 이름 (TLD) 및 두 번째 수준 도메인 이름입니다. 예를 들어 contoso.com, com는는 TLD와 contoso 두 번째 수준 도메인 이름입니다.  
  
 사무실 밖에 라인일 도메인 이름 액세스 서버에서 파일 공유 하거나 네트워크의 컴퓨터에 사용할 수 있습니다. 휴가 때 서버를 관리할 수도 있습니다. 예를 들어 서버에 대 한 contoso.com를 등록합니다. 노트북을 입력 하는 웹 브라우저를 열 수 사무실 밖에 있을 때 **contoso.com** Windows Server Essentials의 설정한 원격 Web Access 인스턴스에 연결 하는 주소 텍스트 상자에 있습니다.  
  
###  <a name="BKMK_PersonalizedNames"></a>이해 개인 설정 된 Microsoft 도메인 이름  
 Microsoft 개인 설정 된 도메인 이름 다음과 같은 기능이 포함 됩니다.  
  
-   웹에 대 한 원격 액세스를 사용자 지정 도메인 이름 (예를 들어, *yourhostname*. remotewebaccess.com). 도메인 이름 공개 IP 주소와 연결 되어 있습니다.  
  
-   DNS 동적 프로토콜 서비스를 업데이트 공개 IP 주소를 변경 하는 경우 도메인 이름을 사용 하 여 웹 액세스 원격 중단 되지 것입니다. 일반적으로 인터넷 서비스 공급자 (Isp) 조직 s 광대역 연결을 위한 변경할 수 있는 공개 동적 IP 주소를 제공 합니다.  
  
-   도메인 이름와 연결 된 신뢰할 수 있는 인증 합니다.  
  
 서버, Microsoft 개인 설정 된 도메인 이름 부합에 (Windows Live ID로 이전의) Microsoft 계정이 필요 합니다. 하나씩에 등록할 수 Microsoft 계정이 없는 경우는 [Microsoft Hotmail](https://login.live.com/) 웹 합니다.  
  
> [!IMPORTANT]
>  Windows Live 특수 문자 서버를 지원 하지 않는 Microsoft 계정 암호에 수 있게 합니다. Microsoft는 개인화 된 도메인을 사용 하는 경우 Microsoft 계정 암호에을 지 원하는 문자만 있는지 확인 합니다. 서버 문자 $의 사용을 지원 하지 않습니다 /, ', % 하 고 있습니다.  
  
###  <a name="BKMK_UseNewName"></a>사용 하는 새로운 기능이 나 기존 도메인 이름  
 Windows Server Essentials 실행 하는 서버에 도메인 이름으로 자동으로 설정 하려면 설정 나만의 도메인 이름 마법사에 나열 되어 있는 도메인 이름 서비스 공급자를 사용 해야 합니다. 새 도메인 이름 하거나 기존 도메인 이름을 사용 하도록 선택할 수 있습니다. 다음 중 하나를 수행 합니다.  
  
-   새 도메인 이름 도메인 중 하나에서 나열 된 이름 서비스 공급자 마법사에서를 받을 클릭 하려는 경우 **새 도메인 이름을 설정 하 고 싶습니다**합니다.  
  
-   지원 되는 도메인 이름 서비스 공급자 중 하나에서 구입한 되는 기존 도메인 이름을 사용 하는 경우 설정 나만의 도메인 이름 마법사 서버에 대 한 도메인 이름을 설정 하려면 사용할 수 있습니다. 클릭 **이미 소유 도메인 이름 사용 하려는 경우**, 다음에 도메인 이름 입력 하 고 있는 **나만의 도메인 이름을 설정** 텍스트 상자 합니다. 사용자 이름 및 암호 도메인 이름 구매 하는 데 사용 되는 제공 해야 합니다.  
  
-   Windows Server Essentials에서 지원 되지 않는 도메인 이름 서비스 공급자 로부터 구매 하는 기존 도메인 이름 있으며 서버에 대 한 도메인 이름을 설정 하려면 설정 나만의 도메인 이름 마법사를 사용 하 여 원하는 경우 도메인 이름 도메인 이름 서비스 공급자 마법사에 나열 된 중 하나를 전송할 수 있습니다. 클릭 **이미 소유 도메인 이름 사용 하려는 경우**, 이름을 입력 하 고 도메인에 있는 **도메인 이름** 텍스트 입력 한 다음 도메인 이름 전송할 도메인 이름 서비스 공급자 s 웹 사이트에서 지침을 따릅니다.  
  
###  <a name="BKMK_SetUpName"></a>도메인 이름 설정  
 웹에 대 한 원격 액세스를 켤 때 인터넷 도메인 이름 서버 설정에 선택할 수 있습니다.  
  
##### <a name="to-set-up-or-manage-an-internet-domain-name"></a>설정 하거나 인터넷 도메인 이름 관리 하려면  
  
1.  대시보드를 엽니다.  
  
2.  클릭 **서버 설정**을 차례로 클릭 하 고 있는 **원하는 위치에 액세스** 탭 합니다.  
  
3.  에 **도메인 이름** 섹션에서 클릭 **설정**합니다.  
  
4.  마법사를 완료 하 고 지침을 따릅니다. 소유 하지 않은 이미 도메인 이름 및 인증서를 도메인 이름 및 인증서를 구매 하는 도메인 이름 공급자 찾도록 마법사 도와 또는 개인 설정 된 Microsoft 도메인 이름 얻을 수 있습니다.  
  
###  <a name="BKMK_ChooseProvider"></a>도메인 이름 서비스 공급자를 선택 합니다.  
 사용 하려는 도메인 이름 확장명을 지 원하는 도메인 이름 서비스 공급자를 선택 해야 합니다. 설정 나만의 도메인 이름 마법사 각 공급자 s 웹 사이트에 대 한 링크를 사용할 수 있는 적격된 공급자 목록이 포함 되어 있습니다. 클릭 하 고 **더 많은 정보** 서비스와 공급자에서 제공 되는 가격 관련 정보를 얻는 각 s 공급자 이름 옆에 있는 링크 합니다.  
  
> [!NOTE]
>  일부 도메인 이름 서비스 공급자 제공 광범위 한 국제 지역 하 고 다른 사람이 더 작은 지역/국가 제공 합니다. 이 때문 일부 공급자에 해당 언어 기본 설정의 번역 하는 웹 사이트를 제공 하지 않을 수 있습니다.  
  
 도메인 이름을 구입 하면 시스템 DNS (도메인 이름) 동적 업데이트 프로토콜 서비스 도메인 이름 서비스 공급자 로부터 구매 고려할 수 있습니다. DNS 동적 업데이트 프로토콜 누구나 인터넷에서 해당 네트워크의 IP 주소 끊임없이 변화 하는 경우에 로컬 네트워크 리소스에 액세스할 수 있는 서비스입니다. 또는 구입할 수 있습니다에서 고정 IP 주소에서 인터넷 서비스 공급자 (ISP) 보장 하기 위해 사용자의 IP 주소를 변경 하지 않습니다.  
  
###  <a name="BKMK_ChooseDomainName"></a>도메인 이름 선택  
 비즈니스 서버에 고유 하 게 식별 이름을 선택 합니다. 예를 들어, 회사 이름을 Contoso Ltd를 고유 하 게 식별 인터넷 홈 또는 비즈니스 서버 Contoso를 선택할 수 있습니다. 도메인 이름에 사용할 수 없는 경우에 해당 이름 또는 무엇 인가 완전히 다른의 다른 변형 해 보세요.  
  
 이름을 입력할 때 다음 포함 될 수 있습니다.  
  
-   최대 63 문자  
  
-   (영어 또는 지역화 된 문자) 문자, 숫자, 또는 하이픈 (-)를 선택 합니다. 이름이 시작 하 고 문자 또는 번호를 종료 해야 합니다.  
  
    > [!NOTE]
    >  도메인 이름은 대/소문자 구분 하지 않습니다.  
  
###  <a name="BKMK_Prefixes"></a>도메인 이름 접두사 선택  
 도메인 이름 계층 레이블을 구성 됩니다.  
  
 **최상위 도메인 확장** 도메인 이름의 맨 오른쪽 레이블입니다. 예를 들어 www.contoso.com, com 최상위 도메인 이름 확장명을은.  
  
 **두 번째 수준 도메인 이름** 최상위 도메인 이름 확장명 옆에 있는 레이블이 합니다. 두 번째 수준 도메인 이름 자주 회사 이름을, 제품 또는 서비스에 따라 만들어집니다. 예를 들어 www.contoso.com, contoso은 도메인 이름 및 금강 회사 이름을 선택 합니다. 두 번째 수준 도메인 호스트 연관 된 IP 주소를 가진 라고도 합니다.  
  
 **도메인 이름 접두사** 하위도 식별 합니다. 하위 도메인 이름 서비스, 디바이스 또는 지역을 식별 하기 위해 사용할 수 있습니다. 예를 들어, 금강에 로그온 원격 웹 액세스 하기 위해 사용자가 원격 허용 하려는 하지 않으려는 웹 사이트에 웹 사이트에 액세스할 수 있는 적절 한 권한이 있는 사용자만 수 있도록 해 주는 하위를 만들, 공개적으로 사용할 수 있습니다. 금강 remote.contoso.com 하위,으로 설정 하 고 원격은 도메인 이름 접두사 합니다.  
  
> [!TIP]
>  기본 설정 사용 하는 것이 좋습니다 **원격** 으로 접두사 도메인 이름입니다.  
  
###  <a name="BKMK_Extension"></a>도메인 이름 확장명을 선택 합니다.  
 인터넷 웹 사이트에 대 한 도메인 이름을 선택 하면도 사용 하려는 도메인 이름 확장명을 지정 해야 합니다. 모든 도메인 이름에 최종 기간에 따라 문자 식별 확장 됩니다. (확장에 대 한 공식 용어 최상위 도메인 또는 TLD입니다.)  
  
 같은 두 가지 유형의 사용할 수 있는 도메인 확장 가지: 일반 및 국가 코드입니다.  
  
#### <a name="generic-top-level-domains"></a>일반 최상위 도메인  
 일반 도메인 확장 길이 다음에 3 개 이상의 문자 있으며 특정 유형의 조직에서 일반적으로 사용 됩니다.  
  
 **몇 가지 일반적인 최상위 도메인**  
  
|도메인 확장|설명|  
|----------------------|-----------------|  
|.com|상용 조직에서 일반적으로 사용 하지만 누구 든 지 사용할 수 있습니다.|  
|.net|네트워크 infrastructure 서비스를 제공 하는 비즈니스 위한 것입니다.|  
|.org|원래 비영리 기관와 다른 일반적인 최상위 도메인 범주에 속하지 않는 기타 비즈니스 사용 합니다. 누구 든 지 사용할 수 있습니다.|  
|.edu|사용 하기 위해 교육 조직에서 제한 됩니다.|  
  
#### <a name="country-code-top-level-domains"></a>최상위 도메인 국가 코드  
 이러한 도메인 확장은 길이 두 개의 문자. 이러한은 조직에 국가 또는 지역과 관련 된 해당 코드를 사용 하도록 설계 되었습니다. 일부 국가 코드 최상위 도메인 시민 해당 국가 또는 지역에서 사용에 대 한 제한 됩니다. 다른 사용자가 사용할 수 있습니다.  
  
 **국가 코드 최상위 도메인 몇 가지**  
  
|도메인 확장|설명|  
|----------------------|-----------------|  
|.ca|캐나다에서 웹 사이트에서|  
|.cn|중국에서 웹 사이트에서|  
|.de|독일의 웹 사이트에서|  
|. co.uk|영국 웹 사이트에서|  
  
 최상위 도메인의 전체 목록은 보려면는 [인터넷 할당 숫자 기관 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=117438)합니다.  
  
#### <a name="if-a-domain-extension-is-not-available-to-select-in-the-set-up-domain-name-wizard"></a>도메인 확장 선택 설정 도메인 이름 마법사에서 사용할 수 없는 경우  
 설정 도메인 이름 마법사를 실행 하면 마법사 해당 국가 또는 지역 확인 하 여 시스템 정보를 살펴봅니다. 마법사 해당 지역에서 참여 공급자 지원 도메인 확장만 표시 됩니다. 원하는 도메인 확장 목록에 표시 되지 않으면, 계속에 대 한 다른 도메인 확장을 선택 해야 합니다. 마법사 반환 하 고 목록에서 확장을 선택 합니다.  
  
###  <a name="BKMK_UpdateService"></a>업데이트 하거나 도메인 이름 서비스 업그레이드  
 도메인 이름 구입한 하지만 인증서를 구매 하지 않은 경우 도메인 이름 서비스 업그레이드 하거나 업데이트 해야 할 수 있습니다. 도메인 이름 서비스 공급자 로부터 도메인 이름에 대 한 인증서가 있어야 합니다.  
  
> [!NOTE]
>  필요한 인증서 종류를 결정 하 도메인 이름 서비스 공급자와 협력 합니다. 인증서 제공 되는 인증서 저렴 한 중 하나가 될 수 있습니다. 그러나 설명서 및 비즈니스 요구 더 나은 충족 하는지 확인 하려면 높은 수준의 보안 인증서의 기능을 검토 해야 합니다.  
  
###  <a name="BKMK_ExportCert"></a>내보내기 또는 서버의 인증서 가져오기  
 인증서의 백업 복사본을 만들 또는 다른 서버에서 사용 하려는 경우 인증서를 내보내야 합니다. 내보내기 인증서에 대 한 정보를 참조 하세요. [내보내려면 인증서](https://go.microsoft.com/fwlink/p/?LinkId=214362)합니다.  
  
###  <a name="BKMK_SetNameManually"></a>도메인 이름으로 수동으로 설정  
 이 옵션을 선택 서버 모니터링 되지 않거나 도메인 이름, 유지 하 고 구성 문제가 있는 경우 하지 경고 않는 것입니다. 다음 중 하나를 하는 경우에이 옵션을 고려할 수 있습니다.  
  
-   파트너 도메인 이름 공급자는 해당 국가 또는 지역에 대 한 나열 됩니다.  
  
-   나열 된 파트너 도메인 공급자 도메인 이름 확장명을 지원 하지 않습니다.  
  
-   파트너, 현재은 도메인 이름 공급자의 기존 도메인 이름을 있고 해당 도메인 이름 Windows Server Essentials 지원 되는 도메인 이름 공급자에 게 전송 하지 않으려는 경우입니다.  
  
-   마법사를 사용 하 여 원하는 도메인 이름 확장명 목록이 표시 되지 않습니다 하지만 확장 파트너 현재은 도메인 이름 공급자에서 사용할 수 있습니다.  
  
 도메인에 대 한 A 기록 만드는 도메인 이름 서비스 공급자와 직접 도메인 이름 설정 하기로 선택한 경우 작동 합니다.  
  
##### <a name="to-create-an-a-record"></a>A 레코드를 만들려면  
  
1.  원격 등 호스트 이름를 결정 합니다. 도메인 이름 접두사입니다. 원격 Web Access 로그온 페이지; 열려는 URL 정의 도메인 이름 접두사 이용 도메인 이름 예를 들어, **http://remote.contoso.com**합니다.  
  
2.  1 단계에서에서 하기로 결정 호스트 이름에 대 한 A 기록을 도메인 이름 서비스 공급자 구성 대시보드 (일반적으로에 해당 웹 페이지)를 만듭니다. 사용자가 지정한 A 기록의 IP 주소 라우터 (쪽 인터넷) WAN 측면에 IP 주소 있는지 확인 합니다. WAN IP 주소를 찾는 라우터 설명서를 참조 하십시오.  
  
3.  인터넷 서비스 공급자 (ISP) 네트워크에 대해 고정 IP 주소를 구매에 문의 하는 것이 좋습니다. 이렇게 DNS 항목이 오래 현상이 되지 않도록 하 고 IP 주소를 변경 하지 않습니다.  
  
     ISP에서 고정 IP 주소를 얻을 수 있는 옵션이 없는 경우 도메인 이름 서비스 공급자 또는 다른 서비스 공급자 로부터 시스템 DNS (도메인 이름) 동적 업데이트 프로토콜 서비스 구매 고려할 수 있습니다. DNS 동적 업데이트 프로토콜 IP 주소를 변경 하는 경우에 IP 주소 도메인 이름으로 확인할 수 있도록 네트워크에 대 한 WAN IP 주소를 최신 상태로 유지 하는 서비스입니다.  
  
4.  묻는 시 신뢰할 수 있는 인증서를 가져옵니다. 신뢰할 수 있는 인증서가 마법사에 나열 된 지원 되는 도메인 이름 공급자 중 하나에서 가져올 또는 사용자가 선택한 신뢰할 수 있는 공급자에서 구입 있습니다. 신뢰할 수 있는 인증에 대 한 자세한 내용은 도메인 이름 공급자에 게 문의 합니다.  
  
###  <a name="BKMK_Find"></a>사용자 도메인 이름 서비스 공급자 찾기  
  
##### <a name="to-find-the-domain-name-service-provider-for-your-domain-name"></a>사용자 도메인 이름 도메인 이름 서비스 공급자를 찾으려면  
  
1.  웹 브라우저를 열고 입력 **www.internic.com** Internic 홈 페이지를 이동 하 여 주소 표시줄에 있습니다.  
  
2.  Internic 홈 페이지, 클릭 **Whois**합니다.  
  
3.  에 **Whois** 상자 도메인 이름 (예를 들어 contoso.com)를 입력 합니다.  
  
4.  클릭 하 고 **도메인** 옵션을 클릭 한 다음 **제출**합니다.  
  
5.  사용자 도메인 이름 서비스 공급자의 이름 아래 검색 결과에서 **관리자**합니다.  
  
##  <a name="BKMK_4"></a>원격 웹 액세스를 사용자 지정  
 개인 로고나 배경 이미지를 추가 하 여 원격 Web Access 사이트를 지정할 수 있습니다. 또한이 정보는 모든 사용자에 게 사용할 수 있도록 링크 홈페이지에 추가할 수 있습니다. 자세한 내용은 다음 항목을 참조 하십시오.  
  
-   [원격 웹 액세스를 사용자 지정](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_CustomizeRWA)  
  
-   [로고 및 배경 이미지를 사용자 지정](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_CustomizeImages)  
  
-   [복구 원격 웹 액세스](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_RepairRWA)  
  
###  <a name="BKMK_CustomizeRWA"></a>원격 웹 액세스를 사용자 지정  
 웹 사이트의 제목 변경 로고가 및 배경 이미지를 변경 하 고 홈페이지의 다른 웹 사이트에 대 한 링크를 추가 하 여 웹에 대 한 원격 액세스를 사용자 지정할 수 있습니다.  
  
##### <a name="to-customize-remote-web-access"></a>웹에 대 한 원격 액세스를 사용자 지정 하려면  
  
1.  대시보드를 엽니다.  
  
2.  클릭 **설정**을 차례로 클릭 하 고 있는 **원하는 위치에 액세스** 탭 합니다.  
  
3.  에 **설정 웹 사이트** 섹션에서 클릭 **지정**합니다.  
  
4.  웹에 대 한 원격 액세스를 마치게 클릭 **확인**합니다. 웹에 대 한 원격 액세스에 변경 내용을 테스트 합니다.  
  
###  <a name="BKMK_CustomizeImages"></a>로고 및 배경 이미지를 사용자 지정  
 이 섹션 웹에 대 한 원격 액세스를 사용자 지정 하는 데 사용할 수 있는 이미지에 대 한 정보를 제공 합니다.  
  
#### <a name="image-size"></a>이미지 크기  
 **로고 이미지**  
  
 밝은 로고 이미지 절대 경로 사용 하는 것이 좋습니다. 이미지를 더 크게 32 x 32로 축소은 및 작은 이미지를 확장 하 여 이미지를 왜곡할 수 있는 32 x 32 합니다.  
  
 **배경 이미지**  
  
 최상의 결과 배경 이미지에 대 한 크기 무제한 상태 약 800 x 500 픽셀 않은 이미지를 사용 하는 것이 좋습니다. 배경 이미지 로그온 페이지 (가로 및 세로) 중앙에 배치 됩니다. 로그온 페이지에서 텍스트를 더 쉽게 읽을 수 있도록 배경 이미지의 센터에 색으로 비치는 빛 있어야 합니다.  
  
#### <a name="image-file-types"></a>이미지 파일 형식  
 배경 및 웹 사이트 기본 로고 바꾸려면 다음 이미지 파일 형식은 사용할 수 있습니다.  
  
-   (*.Bmp, \*.dib, \*.rle) 비트맵  
  
-   GIF (*.gif)  
  
-   PNG (*.png)  
  
-   JPG (*.jpg)  
  
###  <a name="BKMK_RepairRWA"></a>복구 원격 웹 액세스  
 수리 마법사를 통해 검색 및 라우터 또는 도메인 이름 문제가 해결 수 있습니다. 웹에 대 한 원격 액세스 문제를 발견 하는 방법은 두 가지.  
  
-   서버 설정에 액세스 어디서 나 탭 대시보드 아이콘이 문제에 대 한 설명을 빨간색 X가 표시 됩니다.  
  
-   알림을 뷰어에서 경고를 표시 합니다.  
  
> [!NOTE]
>  복구 마법사 웹에 대 한 원격 액세스를 해제할 때까지 제공 되지 않습니다. 원격 Web Access 설정에 대 한 정보를 참조 하세요. [원격 Web Access 켜기](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_TurnOnRWA)합니다.  
  
##### <a name="to-repair-remote-web-access"></a>웹에 대 한 원격 액세스 복구 하려면  
  
1.  대시보드 로그온 합니다.  
  
2.  클릭 **설정**을 차례로 클릭 하 고 있는 **원하는 위치에 액세스** 탭 합니다.  
  
3.  클릭 **복구**합니다. **복구 원격 Web Access** 마법사를 시작 합니다.  
  
4.  클릭 **다음**합니다. 마법사는 Web Access 원격 분석 하 여, 문제를 식별 하 고 문제 복구 하려고 합니다.  
  
5.  마법사를 완료 경고를 받으려면 경우 클릭할 수 있습니다 **다시 시도** 문제가 다시 복구 하려고 합니다. 경고를 받으려면 계속 되 면 문제가 및 문제 해결 단계에 대 한 추가 정보에 대 한 경고를 확인 합니다.  
  
##  <a name="BKMK_5"></a>원격 Web Access 문제 해결  
  
-   [원격 Web Access 연결 문제 해결](../support/Troubleshoot-Remote-Web-Access-connectivity-in-Windows-Server-Essentials.md)  
  
-   [방화벽 문제 해결](../support/Troubleshoot-your-firewall-in-Windows-Server-Essentials.md)  
  
-   [어디서 나 액세스 문제 해결](../support/Troubleshoot-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [원격 데스크톱 옵션](Remote-desktop-options.md)  
  
-   [사용 하 여 원격 웹 액세스](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [액세스를 어디서 나 관리](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)
