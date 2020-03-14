---
title: Windows Server Essentials에서 원격 웹 액세스 관리
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
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
ms.openlocfilehash: 3eace9281d9fcdea5262274ac7fb20ec30d30fb4
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322285"
---
# <a name="manage-remote-web-access-in-windows-server-essentials"></a>Windows Server Essentials에서 원격 웹 액세스 관리

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
 
 Windows server essentials의 원격 웹 액세스 또는 windows Server Essentials Experience 역할이 설치 된 Windows Server 2012 r 2에서는 거의 모든 위치에서 응용 프로그램 및 데이터에 액세스 하기 위한 간소화 된 터치 기반의 브라우저 경험을 제공 합니다. 인터넷에 연결 되어 있고 거의 모든 장치를 사용 하 고 있습니다. 원격 웹 액세스 기능을 사용하려면 먼저 원격 액세스 설정 마법사를 사용하여 원격 웹 액세스 기능을 설정한 다음 라우터 및 도메인 이름을 설정해야 합니다.  
  
## <a name="in-this-topic"></a>항목 내용  
  
-   [원격 웹 액세스 설정 및 구성](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [라우터 설정](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [도메인 이름 설정](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [원격 웹 액세스 사용자 지정](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [원격 웹 액세스 문제 해결](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_5)  
  
##  <a name="BKMK_1"></a>원격 웹 액세스 설정 및 구성  
 다음 항목을 통해 원격 웹 액세스를 손쉽게 설정하고 구성할 수 있습니다.  
  
-   [원격 웹 액세스 개요](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Overview)  
  
-   [원격 웹 액세스 설정](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_TurnOnRWA)  
  
-   [지역 변경](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Region)  
  
-   [원격 웹 액세스 권한 관리](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ManagePerms)  
  
-   [원격 웹 액세스 보안](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SecureRWA)  
  
-   [원격 웹 액세스 및 VPN 사용자 관리](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ManageRWAVPN)  
  
###  <a name="BKMK_Overview"></a>원격 웹 액세스 개요  
 사무실에 없을 때 웹 브라우저를 열고 인터넷에 액세스할 수 있는 어디에서 나 원격 웹 액세스에 액세스할 수 있습니다. 원격 웹 액세스에서 다음을 수행할 수 있습니다.  
  
- 서버에 있는 공유 파일 및 폴더에 액세스합니다.  
  
- 서버 및 네트워크의 컴퓨터에 액세스합니다. 이는 사무실에서 컴퓨터 앞에 있는 것처럼 네트워크로 연결된 컴퓨터의 데스크톱에 액세스할 수 있음을 의미합니다.  
  
  원격 웹 액세스는 기본적으로 설정 되어 있지 않습니다. 원격 액세스 설정 마법사를 실행하면 마법사에서 라우터 및 인터넷 연결을 설정하려고 합니다. 원격 웹 액세스 설정 된 후에는 서버에 대 한 도메인 이름을 설정 하 고 원격 웹 액세스를 사용자 지정할 수 있습니다. 라우터를 변경하는 경우 라우터를 다시 설정할 수도 있습니다.  
  
  원격 웹 액세스에 대 한 액세스 권한은 새 사용자 계정을 추가할 때 자동으로 부여 되지 않습니다. 사용자 계정을 추가할 때 공유 폴더, 미디어 라이브러리, 컴퓨터, 홈 페이지 링크, 서버 대시보드에 대한 액세스를 허용하도록 선택할 수 있습니다. 사용자가 원격 웹 액세스를 사용할 수 없도록 지정할 수도 있습니다.  
  
  Windows Server Essentials 대시보드의 **사용자** 탭에 각 사용자 계정에 대 한 원격 웹 액세스 설정이 표시 됩니다. 원격 웹 액세스 설정을 변경 하려면 사용자 계정을 마우스 오른쪽 단추로 클릭 하 고 **계정 속성 보기**를 클릭 합니다.  
  
###  <a name="BKMK_TurnOnRWA"></a>원격 웹 액세스 설정  
 서버 대시보드에서 원격 액세스 설정 마법사를 실행하여 원격 웹 액세스를 설정할 수 있습니다.  
  
##### <a name="to-turn-on-remote-web-access"></a>원격 웹 액세스를 설정하려면  
  
1.  대시보드를 엽니다.  
  
2.  **설정**을 클릭한 다음 **원격 액세스** 탭을 클릭합니다.  
  
3.  **구성**을 클릭합니다. 원격 액세스 설정 마법사가 나타납니다.  
  
4.  **사용할 원격 액세스 기능 선택** 페이지에서 **원격 웹 액세스** 확인란을 선택합니다.  
  
5.  지시에 따라 마법사를 완료합니다.  
  
###  <a name="BKMK_Region"></a>지역 변경  
 Windows Server Essentials에서 지역 설정을 변경하려면 네트워크 관리자여야 합니다.  
  
##### <a name="to-change-the-region-setting"></a>지역 설정을 변경하려면  
  
1.  Windows Server Essentials에 연결된 컴퓨터에서 대시보드를 엽니다.  
  
2.  **설정**을 클릭합니다.  
  
3.  **일반** 탭의 **서버의 국가/지역 위치** 섹션에서 드롭다운 목록을 클릭합니다.  
  
4.  드롭다운 목록에서 새 지역을 선택하고 **적용**을 클릭하여 새 지역 설정을 적용합니다.  
  
###  <a name="BKMK_ManagePerms"></a>원격 웹 액세스 권한 관리  
 Windows Server Essentials에서 사용자 계정을 추가하면 새 사용자는 기본적으로 원격 웹 액세스를 사용할 수 있습니다. 사용자 계정에 대해 원격 웹 액세스를 허용 하지 않도록 선택한 다음 사용자가 원격 웹 액세스 사용 해야 하는 경우 사용자 계정의 속성을 업데이트할 수 있습니다.  
  
##### <a name="to-manage-remote-web-access-permissions-for-a-user-account"></a>사용자 계정에 대한 원격 웹 액세스 권한을 관리하려면  
  
1. 대시보드에 로그온하고 **사용자**를 클릭합니다.  
  
2. 관리할 사용자 계정을 클릭하고 **작업** 창에서 **계정 속성 보기**를 클릭합니다.  
  
3. **속성** 대화 상자에서 **원격 액세스** 탭을 클릭합니다.  
  
4. **원격 액세스** 탭에서 **원격 웹 액세스 허용 및 웹 서비스 응용 프로그램에 액세스** 확인란을 선택하여 사용자가 원격 웹 액세스를 사용하여 서버에 연결할 수 있도록 합니다.  
  
5. **적용**을 클릭한 다음 **확인**을 클릭합니다.  
  
   자세한 내용은 [사용자 계정 관리](Manage-User-Accounts-in-Windows-Server-Essentials.md)를 참조 하세요.  
  
###  <a name="BKMK_SecureRWA"></a>원격 웹 액세스 보안  
 Windows Server Essentials에서는 보안 인증서를 사용하여 소프트웨어와 웹 브라우저 사이에서 교환되는 정보를 보호할 수 있습니다. 컴퓨터에 Connector 소프트웨어를 설치하면 Windows Server Essentials에 대한 보안 인증서가 컴퓨터의 신뢰할 수 있는 인증서 목록에 추가됩니다. 사용자가 사무실에 없을 때 원격 웹 액세스에 액세스하는 가장 좋은 방법은 Connector 소프트웨어가 설치된 휴대용 컴퓨터를 사용하는 것입니다.  
  
> [!WARNING]
>  공공장소나 기타 신뢰할 수 없는 컴퓨터에서 원격 웹 액세스를 사용하는 사용자는 컴퓨터를 두고 자리를 비우기 전이나 세션을 완료했을 때 웹 사이트에서 로그오프했는지 확인해야 합니다.  
  
###  <a name="BKMK_ManageRWAVPN"></a>원격 웹 액세스 및 VPN 사용자 관리  
 VPN을 사용하여 Windows Server Essentials에 연결하고 서버에 저장된 모든 리소스에 액세스할 수 있습니다. 이 기능은 특히 VPN 연결을 통해 호스트된 Windows Server Essentials 서버에 연결하는 데 사용할 수 있는 네트워크 계정으로 설정되는 클라이언트 컴퓨터가 있는 경우 유용합니다. 호스트된 Windows Server Essentials 서버에서 새로 만든 모든 사용자 계정은 처음에 VPN을 사용하여 클라이언트 컴퓨터에 로그온해야 합니다.  
  
##### <a name="to-set-vpn-and-remote-web-access-permissions-for-network-users"></a>네트워크 사용자에 대한 VPN 및 원격 웹 액세스 권한을 설정하려면  
  
1.  대시보드를 엽니다.  
  
2.  탐색 모음에서 **사용자**를 클릭합니다.  
  
3.  사용자 계정 목록에서 데스크톱에 원격으로 액세스할 수 있는 사용 권한을 부여할 사용자 계정을 선택합니다.  
  
4.  **< 사용자 계정\> 작업** 창에서 **속성**을 클릭 합니다.  
  
5.  **< 사용자 계정\> 속성**에서 **원격 액세스** 탭을 클릭 합니다.  
  
6.  **원격 액세스** 탭에서 다음을 수행합니다.  
  
    1.  사용자가 VPN을 사용하여 서버에 연결할 수 있게 하려면 **VPN(가상 사설망) 허용** 확인란을 선택합니다.  
  
    2.  사용자가 원격 웹 액세스를 사용하여 서버에 연결할 수 있게 하려면 **원격 웹 액세스 허용 및 웹 서비스 응용 프로그램에 액세스** 확인란을 선택합니다.  
  
7.  **적용**을 클릭한 다음 **확인**을 클릭합니다.  
  
##  <a name="BKMK_2"></a>라우터 설정  
 원격 웹 액세스를 지원하도록 서버를 구성한 경우 원격 액세스 설정 마법사가 라우터를 설정하려고 시도합니다. 라우터 또는 라우터 설정을 변경한 경우 라우터 설정 마법사를 다시 실행해야 합니다. 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [라우터 설정](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SetUpRouter)  
  
-   [라우터 교체](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ReplaceRouter)  
  
-   [정의 된 네트워크 위치](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_NetworkLocation)  
  
-   [원격 데스크톱 서비스 ActiveX 컨트롤 사용](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ActiveX)  
  
###  <a name="BKMK_SetUpRouter"></a>라우터 설정  
 이 단계를 진행하는 동안 Windows Server Essentials에서 UPnP 명령을 사용하여 라우터를 자동으로 구성합니다. 그러려면 라우터에서 UPnP 표준을 지원하고 라우터에서 UPnP 설정을 사용해야 합니다.  
  
> [!NOTE]
>  네트워크 구성은 Windows Server Essentials에 대해 지원되는 네트워크 요구 사항을 준수해야 합니다. 네트워크에는 라우터가 하나만 있어야 합니다.  
  
 라우터가 도메인 이름 설정 마법사를 통해 설정되지 않은 경우 포트 443을 수동으로 전달해야 합니다. 라우터에서 포트 전달을 설정하는 방법에 대한 자세한 내용은 [라우터 설정](https://social.technet.microsoft.com/wiki/contents/articles/windows-small-business-server-2011-essentials-router-setup.aspx)을 참조하세요.  
  
###  <a name="BKMK_ReplaceRouter"></a>라우터 교체  
 제조업체의 지침에 따라 라우터를 교체 하 고 라우터 설정 마법사를 실행 하 여 새 라우터를 구성 합니다.  
  
##### <a name="to-set-up-your-new-router"></a>새 라우터를 설정하려면  
  
1.  Windows Server Essentials 대시보드에서 **설정**을 클릭합니다.  
  
2.  **원격 액세스** 탭을 클릭하고 **라우터** 섹션에서 **설정**을 클릭합니다. 라우터 설정 마법사가 시작됩니다.  
  
3.  마법사의 지침에 따라 새 라우터 설정을 완료합니다.  
  
###  <a name="BKMK_NetworkLocation"></a>정의 된 네트워크 위치  
 네트워크 위치는 네트워크에 연결할 때 Windows에서 적용하는 네트워크 설정 모음입니다. 설정은 사용하는 네트워크 유형에 따라 달라지고 사용자 지정할 수 있습니다. 네트워크 위치에 대한 설정에 따라 특정 기능(예: 파일 및 프린터 공유, 네트워크 검색 및 공용 폴더 공유)이 켜지거나 꺼져 있는지가 결정됩니다. 네트워크 위치는 여러 네트워크에 연결해야 할 때 유용합니다.  
  
 예를 들어 집과 직장에서 사용하는 노트북 컴퓨터를 소유하고 있을 수 있습니다. 사무실에 있을 때는 사무실 네트워크에 연결합니다. 그러나 집에 돌아오면 랩톱을 사용하여 홈 서버에 저장된 동영상과 음악에 액세스하고 이를 재생합니다. 새 네트워크에 연결하고 위치 유형을 지정하면 Windows에서 해당 위치 유형에 대해 미리 설정된 네트워크 프로필을 할당합니다. 다음에 해당 네트워크에 연결하면 Windows에서 해당 네트워크를 인식하고 올바른 설정을 자동으로 할당합니다. 그러면 컴퓨터에 대한 정보를 보호하도록 도와주는 보안 계층이 추가되고 해당 위치에 필요한 네트워크 기능만 켜집니다.  
  
 네트워크 위치에는 4가지 유형이 있습니다.  
  
-   **홈 네트워크** 홈 네트워크일 경우 또는 네트워크에 있는 사용자와 디바이스를 알고 있고 신뢰할 때 이 네트워크를 선택합니다. 홈 네트워크의 컴퓨터는 홈 그룹에 속할 수 있습니다. 네트워크에 있는 다른 컴퓨터와 디바이스를 볼 수 있고 다른 네트워크 사용자가 내 컴퓨터를 볼 수 있도록 홈 네트워크에 대한 네트워크 검색이 켜집니다.  
  
-   **회사 네트워크** 소규모 또는 기타 직장 네트워크에 대해 이 네트워크를 선택합니다. 네트워크에 있는 다른 컴퓨터와 디바이스를 볼 수 있고 다른 네트워크 사용자가 내 컴퓨터를 볼 수 있도록 하는 네트워크 검색은 기본적으로 켜지지만 홈 그룹을 만들거나 연결할 수 없습니다.  
  
-   **공용 네트워크** 공공장소(예: 커피숍 또는 공항)에 대해 이 네트워크를 선택합니다. 이 위치는 내 컴퓨터가 다른 컴퓨터에 표시되지 않도록 하고 인터넷의 악성 소프트웨어로부터 컴퓨터를 보호하는 데 도움이 되도록 설계되었습니다. 공용 네트워크에서는 홈 그룹을 사용할 수 없고 네트워크 검색이 꺼집니다. 라우터를 사용하지 않고 인터넷에 직접 연결되거나 모바일 광대역 연결이 설정되어 있는 경우에도 이 옵션을 선택해야 합니다.  
  
-   **도메인** 기업 작업 영역 등에 있는 도메인에 대해 이 네트워크를 선택합니다. 이 네트워크 위치 유형은 네트워크 관리자가 제어하며 선택하거나 변경할 수 없습니다.  
  
###  <a name="BKMK_ActiveX"></a>원격 데스크톱 서비스 ActiveX 컨트롤 사용  
 원격 데스크톱 서비스 ActiveX 컨트롤을 사용 하면 원격 웹 액세스를 사용 하 여 다른 컴퓨터에서 인터넷을 통해 홈 또는 업무용 컴퓨터에 액세스할 수 있습니다.  
  
##### <a name="to-enable-remote-desktop-services-activex-controls"></a>원격 데스크톱 서비스 ActiveX 컨트롤을 사용하도록 설정하려면  
  
1.  Internet Explorer에서 **도구**, **인터넷 옵션**을 차례로 클릭합니다.  
  
2.  **보안** 탭에서 **사용자 지정 수준**을 클릭합니다.  
  
3.  **ActiveX 컨트롤 및 플러그 인** 섹션에서 다음을 수행합니다.  
  
    1.  **서명된 ActiveX 컨트롤 다운로드**에서 **프롬프트**를 클릭합니다.  
  
    2.  **ActiveX 컨트롤 및 플러그 인 실행**에서 **사용**을 클릭합니다.  
  
4.  **확인**을 두 번 클릭하여 변경 내용을 적용하고 대화 상자를 닫습니다.  
  
##  <a name="BKMK_3"></a>도메인 이름 설정  
 원격 웹 액세스를 설정한 후에는 Windows Server Essentials를 실행하는 서버의 도메인 이름을 설정할 수 있습니다. 이 단계는 원격 컴퓨터에서 원격 웹 액세스를 사용하려는 경우에 필요합니다. 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [도메인 이름 개요](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_DNOverview)  
  
-   [Microsoft 개인 설정 된 도메인 이름 이해](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_PersonalizedNames)  
  
-   [새 도메인 이름 또는 기존 도메인 이름 사용](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_UseNewName)  
  
-   [도메인 이름 설정](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SetUpName)  
  
-   [도메인 이름 서비스 공급자 선택](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ChooseProvider)  
  
-   [도메인 이름 선택](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ChooseDomainName)  
  
-   [도메인 이름 접두사 선택](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Prefixes)  
  
-   [도메인 이름 확장명 선택](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Extension)  
  
-   [도메인 이름 서비스 업데이트 또는 업그레이드](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_UpdateService)  
  
-   [서버에서 인증서 내보내기 또는 가져오기](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ExportCert)  
  
-   [수동으로 도메인 이름 설정](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SetNameManually)  
  
-   [도메인 이름 서비스 공급자 찾기](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Find)  
  
###  <a name="BKMK_DNOverview"></a>도메인 이름 개요  
 도메인 이름은 인터넷에서 서버를 고유하게 식별합니다. 도메인 이름은 최소한 두 부분인 TLD(최상위 도메인 이름) 및 두 번째 수준 도메인 이름으로 구성됩니다. 예를 들어 contoso.com에서 com은 TLD이 고 contoso는 두 번째 수준 도메인 이름입니다.  
  
 사무실을 비우는 동안 도메인 이름을 사용하여 서버 또는 네트워크의 컴퓨터에 있는 공유 파일에 액세스할 수 있습니다. 자리에 없을 때 서버를 관리할 수도 있습니다. 예를 들어 서버에 대해 contoso.com을 등록합니다. 사무실을 비울 때 랩톱에서 웹 브라우저를 열고 주소 텍스트 상자에 **contoso.com**을 입력하여 Windows Server Essentials에서 설정한 원격 웹 액세스의 인스턴스에 연결할 수 있습니다.  
  
###  <a name="BKMK_PersonalizedNames"></a>Microsoft 개인 설정 된 도메인 이름 이해  
 Microsoft 개인 설정된 도메인 이름에는 다음 기능이 포함됩니다.  
  
- 원격 웹 액세스에 대 한 사용자 지정 도메인 이름 (예: remotewebaccess.com *).* 도메인 이름은 공용 IP 주소와 연결됩니다.  
  
- 공용 IP 주소가 변경 될 경우 도메인 이름을 사용 하는 원격 웹 액세스 중단 되지 않도록 하는 DNS 동적 업데이트 프로토콜 서비스입니다. 일반적으로 조직의 광대역 연결을 위한 Isp (인터넷 서비스 공급자)는 변경 될 수 있는 동적 공용 IP 주소를 제공 합니다.  
  
- 도메인 이름과 연결된 신뢰할 수 있는 인증서.  
  
  Microsoft 개인 설정된 도메인 이름을 서버와 통합하려면 Microsoft 계정(이전 Windows Live ID)이 필요합니다. Microsoft 계정이 없으면 [Microsoft Hotmail](https://login.live.com/) 웹 사이트에서 계정을 등록할 수 있습니다.  
  
> [!IMPORTANT]
>  Windows Live의 Microsoft 계정 암호에는 서버에서 지원하지 않는 특수 문자를 사용할 수 있습니다. Microsoft 개인 설정된 도메인을 사용할 경우 Microsoft 계정 암호에 서버에서 지원하는 문자만 포함되어 있는지 확인합니다. 서버에서는 $, /, ', % 문자 사용을 지원하지 않습니다.  
  
###  <a name="BKMK_UseNewName"></a>새 도메인 이름 또는 기존 도메인 이름 사용  
 Windows Server Essentials를 실행하는 서버에서 도메인 이름을 자동으로 설정하려면 도메인 이름 설정 마법사에 나열된 도메인 이름 서비스 공급자를 사용해야 합니다. 새 도메인 이름을 얻거나 기존 도메인 이름을 사용하도록 선택할 수 있습니다. 다음 작업 중 하나를 수행합니다.  
  
-   마법사에 나열된 도메인 이름 서비스 공급자의 하나에서 새 도메인 이름을 얻으려면 **새 도메인 이름 설정**을 클릭합니다.  
  
-   지원되는 도메인 이름 서비스 공급자의 하나로부터 구매한 기존 도메인 이름이 있으면 도메인 이름 설정 마법사를 사용하여 서버에 대한 도메인 이름을 설정할 수 있습니다. **이미 가지고 있는 도메인 이름 사용**을 클릭하고 **도메인 이름 설정** 텍스트 상자에 도메인 이름을 입력합니다. 도메인 이름 구매에 사용한 사용자 이름과 암호를 입력해야 합니다.  
  
-   Windows Server Essentials에서 지원되지 않는 도메인 이름 서비스 공급자로부터 구매한 기존 도메인 이름이 있을 때 도메인 이름 설정 마법사를 사용하여 서버에 대한 도메인 이름을 설정하려면 도메인 이름을 마법사에 나열된 도메인 이름 서비스 공급자에게 전송합니다. **이미 소유한 도메인 이름 사용**을 클릭 하 **고 도메인 이름 텍스트 상자** 에 도메인 이름을 입력 한 다음 도메인 이름 서비스 공급자 웹 사이트의 지시에 따라 도메인 이름을 전송 합니다.  
  
###  <a name="BKMK_SetUpName"></a>도메인 이름 설정  
 원격 웹 액세스를 켤 때 서버의 인터넷 도메인 이름을 설정할 수 있습니다.  
  
##### <a name="to-set-up-or-manage-an-internet-domain-name"></a>인터넷 도메인 이름을 설정 또는 관리하려면  
  
1.  대시보드를 엽니다.  
  
2.  **서버 설정**, **원격 액세스** 탭을 차례로 클릭합니다.  
  
3.  **도메인 이름** 섹션에서 **설정**을 클릭합니다.  
  
4.  지시에 따라 마법사를 완료합니다. 도메인 이름과 인증서를 아직 가지고 있지 않으면 마법사를 통해 도메인 이름 공급자를 찾아서 도메인 이름과 인증서를 구매하거나 개인 설정된 Microsoft 도메인 이름을 얻을 수 있습니다.  
  
###  <a name="BKMK_ChooseProvider"></a>도메인 이름 서비스 공급자 선택  
 사용할 도메인 이름 확장명을 지원하는 도메인 이름 서비스 공급자를 선택해야 합니다. 도메인 이름 설정 마법사에는 각 공급자의 웹 사이트에 대 한 링크와 함께 사용할 수 있는 정규화 된 공급자 목록이 포함 되어 있습니다. 각 공급자 이름 옆에 있는 **추가 정보** 링크를 클릭 하 여 공급자가 제공 하는 서비스 및 가격에 대 한 정보를 얻습니다.  
  
> [!NOTE]
>  도메인 이름 서비스 공급자에 따라 광범위한 국제 지역에서 서비스를 제공하거나 더 작은 시장에서 서비스를 제공합니다. 이 때문에 일부 공급자가 기본 설정 언어로 번역된 웹 사이트를 제공하지 않을 수도 있습니다.  
  
 도메인 이름을 구매할 때 도메인 이름 서비스 공급자로부터 DNS(Domain Name System) 동적 업데이트 프로토콜 서비스를 함께 구매하는 것을 고려할 수도 있습니다. DNS 동적 업데이트 프로토콜은 네트워크의 IP 주소가 지속적으로 변경될 때 인터넷에서 누구나 로컬 네트워크의 리소스에 대한 액세스 권한을 얻을 수 있게 하는 서비스입니다. 또는 IP 주소가 변경되지 않도록 ISP(인터넷 서비스 공급자)로부터 고정 IP 주소를 구매할 수 있습니다.  
  
###  <a name="BKMK_ChooseDomainName"></a>도메인 이름 선택  
 비즈니스 서버를 고유하게 식별하는 이름을 선택합니다. 예를 들어 비즈니스 이름이 Contoso Ltd이면 Contoso를 선택하여 인터넷에서 홈 또는 비즈니스를 고유하게 식별할 수 있습니다. 도메인 이름을 사용할 수 없으면 해당 이름의 다른 변형이나 완전히 다른 이름을 시도합니다.  
  
 입력한 이름에는 다음을 포함할 수 있습니다.  
  
-   최대 63자  
  
-   문자(영어 또는 번역된 문자), 숫자 또는 하이픈(-). 이름은 문자 또는 숫자로 시작되고 끝나야 합니다.  
  
    > [!NOTE]
    >  도메인 이름은 대/소문자 구분하지 않습니다.  
  
###  <a name="BKMK_Prefixes"></a>도메인 이름 접두사 선택  
 도메인 이름은 계층적 레이블로 구성됩니다.  
  
 **최상위 도메인 확장명** 은 도메인 이름에서 맨 오른쪽 레이블입니다. 예를 들어 www\.contoso.com에서 com은 최상위 도메인 이름 확장명입니다.  
  
 **두 번째 수준 도메인 이름** 은 최상위 도메인 이름 확장명 옆에 있는 레이블입니다. 두 번째 수준 도메인 이름은 회사 이름, 제품 또는 서비스를 기준으로 생성되기도 합니다. 예를 들어 www\.contoso.com에서 contoso는 두 번째 수준 도메인 이름이 고 회사 이름 Contoso Pharmaceuticals에 대해 선택 되었습니다. 두 번째 수준 도메인은 연결된 IP 주소가 있는 호스트 이름이라고도 합니다.  
  
 **도메인 이름 접두사** 는 하위 도메인을 나타냅니다. 하위 도메인 이름을 사용하여 서비스, 디바이스 또는 지역을 식별할 수 있습니다. 예를 들어 Contoso Pharmaceuticals에서는 원격 사용자가 원격 웹 액세스에 로그온하도록 허용하지만 대중들이 웹 사이트를 사용할 수 없도록 하려고 적절한 사용 권한이 있는 사용자만 웹 사이트에 액세스하도록 허용하는 하위 도메인을 만듭니다. Contoso Pharmaceuticals에서는 하위 도메인으로 remote.contoso.com을 설정하고 remote는 도메인 이름 접두사입니다.  
  
> [!TIP]
>  기본값 **Remote**를 도메인 이름의 접두사로 사용하는 것이 좋습니다.  
  
###  <a name="BKMK_Extension"></a>도메인 이름 확장명 선택  
 인터넷 웹 사이트에 대한 도메인 이름을 선택할 때 사용할 도메인 이름 확장명도 지정해야 합니다. 확장명은 도메인 이름의 마지막 마침표 뒤의 문자로 식별됩니다. (확장의 공식 용어는 최상위 도메인 또는 TLD입니다.)  
  
 사용할 수 있는 도메인 확장명에는 두 가지 유형인 일반 및 국가 코드가 있습니다.  
  
#### <a name="generic-top-level-domains"></a>일반 최상위 도메인  
 일반 도메인 확장명의 길이는 문자 3자 이상이고 일반적으로 특정 종류의 조직에서 사용됩니다.  
  
 **일반 최상위 도메인의 예**  
  
|도메인 확장명|설명|  
|----------------------|-----------------|  
|.com|일반적으로 영리 조직에서 사용되지만 누구나 사용할 수 있습니다.|  
|.net|네트워크 인프라 서비스를 제공하는 비즈니스를 위해 설계되었습니다.|  
|.org|원래 비영리 기관 및 다른 일반 최상위 도메인 범주에 속하지 않는 기타 비즈니스에서 사용됩니다. 누구나 사용할 수 있습니다.|  
|.edu|교육 조직에서 사용하도록 제한됩니다.|  
  
#### <a name="country-code-top-level-domains"></a>국가 코드 최상위 도메인  
 이 도메인 확장명의 길이는 문자 2자입니다. 해당 코드와 연결된 국가 또는 지역에 있는 조직에서 사용하도록 설계되었습니다. 일부 국가 코드 최상위 도메인은 해당 국가 또는 지역의 거주자가 사용하도록 제한됩니다. 다른 국가 코드는 누구나 사용할 수 있습니다.  
  
 **국가 코드 최상위 도메인의 예**  
  
|도메인 확장명|설명|  
|----------------------|-----------------|  
|.ca|캐나다의 웹 사이트에서 사용합니다.|  
|.cn|중국의 웹 사이트에서 사용합니다.|  
|.de|독일의 웹 사이트에서 사용합니다.|  
|.co.uk|영국의 웹 사이트에서 사용합니다.|  
  
 최상위 도메인의 전체 목록을 보려면 [Internet Assigned Numbers Authority 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=117438)(영문)를 참조하세요.  
  
#### <a name="if-a-domain-extension-is-not-available-to-select-in-the-set-up-domain-name-wizard"></a>도메인 이름 설정 마법사에서 도메인 확장명을 선택할 수 없는 경우  
 도메인 이름 설정 마법사를 실행하면 마법사에서 시스템 정보를 확인하여 국가 또는 지역을 결정합니다. 그런 다음 마법사에서는 해당 지역의 참여 공급자가 지원하는 도메인 확장명만 표시합니다. 원하는 도메인 확장명이 목록에 표시되지 않을 경우 계속하려면 다른 도메인 확장명을 선택해야 합니다. 마법사에서 반환한 목록에서 확장명을 선택합니다.  
  
###  <a name="BKMK_UpdateService"></a>도메인 이름 서비스 업데이트 또는 업그레이드  
 도메인 이름을 구매했지만 인증서를 구매하지 않았다면 도메인 이름 서비스를 업데이트 또는 업그레이드해야 할 수 있습니다. 도메인 이름 서비스 공급자가 제공하는 도메인 이름에 대한 인증서가 있어야 합니다.  
  
> [!NOTE]
>  도메인 이름 서비스 공급자에게 문의하여 필요한 인증서 유형을 확인합니다. 인증서는 제공되는 저렴한 인증서의 하나일 수 있습니다. 그러나 더 높은 수준 보안 인증서의 설명서와 기능을 검토하여 비즈니스 요구 사항에 더욱 적합한지를 확인해야 합니다.  
  
###  <a name="BKMK_ExportCert"></a>서버에서 인증서 내보내기 또는 가져오기  
 인증서의 백업 복사본을 만들거나 인증서를 다른 서버에서 사용하려면 인증서를 내보내야 합니다. 인증서를 내보내는 방법에 대한 자세한 내용은 [인증서 내보내기](https://go.microsoft.com/fwlink/p/?LinkId=214362)를 참조하세요.  
  
###  <a name="BKMK_SetNameManually"></a>수동으로 도메인 이름 설정  
 이 옵션을 선택하면 서버에서 도메인 이름을 모니터링하거나 유지 관리하지 않으며 구성 문제가 있는 경우 경고를 표시하지 않습니다. 다음 중 하나에 해당하는 경우에도 이 옵션을 고려할 수 있습니다.  
  
- 사용자의 국가 또는 지역에 대해 파트너 도메인 이름 공급자가 나열되지 않는 경우  
  
- 나열된 파트너 도메인 공급자가 도메인 이름 확장명을 지원하지 않는 경우  
  
- 현재 파트너가 아닌 도메인 이름 공급자의 기존 도메인 이름이 있으며 이 도메인 이름을 Windows Server Essentials에서 지원하는 도메인 이름 공급자에게 전송하지 않으려는 경우  
  
- 사용하려는 도메인 이름 확장명이 마법사에 나열되지 않지만 현재 파트너가 아닌 도메인 이름 공급자를 통해 해당 확장명을 사용할 수 있는 경우  
  
  도메인 이름을 수동으로 설정 하도록 선택한 경우 도메인 이름 서비스 공급자를 사용 하 여 도메인에 대 한 A 레코드를 만듭니다.  
  
##### <a name="to-create-an-a-record"></a>A 레코드를 만들려면  
  
1.  호스트 이름 (예: 원격)을 결정 합니다. 이는 도메인 이름 접두사입니다. 도메인 이름 접두사와 사용자의 도메인 이름에는 URL이 정의 되어 원격 웹 액세스 로그온 페이지가 열립니다. 예를 들어 **http://remote.contoso.com** 합니다.  
  
2.  도메인 이름 서비스 공급자 구성 대시보드 (일반적으로 해당 웹 페이지)에서 1 단계에서 결정 한 호스트 이름에 대 한 A 레코드를 만듭니다. A 레코드에 지정한 IP 주소가 라우터의 WAN 쪽 (인터넷 연결 측)의 IP 주소 인지 확인 합니다. WAN IP 주소는 라우터 설명서에서 확인할 수 있습니다.  
  
3.  ISP(인터넷 서비스 공급자)에 문의하여 네트워크의 고정 IP 주소를 구입하는 것이 좋습니다. 그러면 IP 주소가 변경되지 않고 DNS 항목이 만료되지 않습니다.  
  
     ISP에서 고정 IP 주소를 구매하는 옵션이 없는 경우 도메인 이름 서비스 공급자 또는 다른 서비스 공급자를 통해 DNS(Domain Name System) 동적 업데이트 프로토콜 서비스를 구매할 수도 있습니다. DNS 동적 업데이트 프로토콜은 IP 주소가 변경된 경우에도 IP 주소를 도메인 이름으로 확인할 수 있도록 네트워크의 WAN IP 주소를 최신 상태로 유지하는 서비스입니다.  
  
4.  마법사의 메시지에 따라 신뢰할 수 있는 인증서를 가져옵니다. 신뢰할 수 있는 인증서가 없는 경우 마법사에 나열된 지원되는 도메인 이름 공급자 중 하나로부터 인증서를 얻거나 원하는 신뢰할 수 있는 공급자로부터 인증서를 구입할 수 있습니다. 신뢰할 수 있는 인증서에 대한 자세한 내용은 도메인 이름 공급자에게 문의하세요.  
  
###  <a name="BKMK_Find"></a>도메인 이름 서비스 공급자 찾기  
  
##### <a name="to-find-the-domain-name-service-provider-for-your-domain-name"></a>도메인 이름에 대한 도메인 이름 서비스 공급자를 찾으려면  
  
1. 웹 브라우저를 열고 주소 표시줄에 <strong>www.internic.com</strong>을 입력하여 Internic 홈페이지로 이동합니다.  
  
2. Internic 홈페이지에서 **Whois**를 클릭합니다.  
  
3. **Whois** 상자에서 도메인 이름을 입력합니다(예: contoso.com).  
  
4. **Domain** 옵션, **Submit**을 차례로 클릭합니다.  
  
5. 검색 결과에서 도메인 이름 서비스 공급자의 이름이 **Registrar** 아래에 나열됩니다.  
  
##  <a name="BKMK_4"></a>원격 웹 액세스 사용자 지정  
 개인 로고 또는 배경 이미지를 추가하여 원격 웹 액세스 사이트를 사용자 지정할 수 있습니다. 또한 모든 사용자가 이 정보를 사용할 수 있도록 홈 페이지에 링크를 추가할 수도 있습니다. 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [원격 웹 액세스 사용자 지정](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_CustomizeRWA)  
  
-   [배경 및 로고 이미지 사용자 지정](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_CustomizeImages)  
  
-   [원격 웹 액세스 복구](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_RepairRWA)  
  
###  <a name="BKMK_CustomizeRWA"></a>원격 웹 액세스 사용자 지정  
 웹 사이트 제목을 변경하고 배경 이미지와 로고를 변경한 다음 홈페이지에 다른 웹 사이트 링크를 추가하여 원격 웹 액세스를 사용자 지정할 수 있습니다.  
  
##### <a name="to-customize-remote-web-access"></a>원격 웹 액세스를 사용자 지정하려면  
  
1.  대시보드를 엽니다.  
  
2.  **설정**을 클릭한 다음 **원격 액세스** 탭을 클릭합니다.  
  
3.  **웹 사이트 설정** 섹션에서 **사용자 지정**을 클릭합니다.  
  
4.  원격 웹 액세스 사용자 지정을 완료하면 **확인**을 클릭합니다. 원격 웹 액세스에 대한 변경 내용을 테스트합니다.  
  
###  <a name="BKMK_CustomizeImages"></a>배경 및 로고 이미지 사용자 지정  
 이 섹션에서는 원격 웹 액세스를 사용자 지정하는 데 사용할 수 있는 이미지에 대한 정보를 제공합니다.  
  
#### <a name="image-size"></a>이미지 크기  
 **로고 이미지**  
  
 32 x 32픽셀 로고 이미지를 사용하는 것이 좋습니다. 더 큰 이미지는 32 x 32로 축소되고 더 작은 이미지는 32 x 32로 확대되므로 이미지가 왜곡될 수 있습니다.  
  
 **배경 이미지**  
  
 배경 이미지에 대한 크기 제한이 없으므로 최상의 결과를 얻으려면 약 800 x 500픽셀 이미지를 사용하는 것이 좋습니다. 배경 이미지는 로그온 페이지의 가운데(가로 및 세로)에 배치됩니다. 로그온 페이지의 텍스트를 쉽게 읽을 수 있도록 배경 이미지의 가운데 부분은 연한 색으로 표시됩니다.  
  
#### <a name="image-file-types"></a>이미지 파일 형식  
 다음 이미지 파일 형식을 사용하여 기본 배경 및 웹 사이트 로고를 바꿀 수 있습니다.  
  
-   Bitmap (* .bmp, \*.dib, \*rle)  
  
-   GIF(*.gif)  
  
-   PNG(*.png)  
  
-   JPG(*.jpg)  
  
###  <a name="BKMK_RepairRWA"></a>원격 웹 액세스 복구  
 복구 마법사를 사용하여 라우터 또는 도메인 이름에 문제가 있는지 검색하고 문제를 해결할 수 있습니다. 원격 웹 액세스에 대한 문제를 검색하는 방법에는 두 가지가 있습니다.  
  
-   대시보드 서버 설정의 원격 액세스 탭에 빨간색 X가 있는 아이콘이 문제에 대한 설명과 함께 표시됩니다.  
  
-   경고 뷰어의 경고입니다.  
  
> [!NOTE]
>  원격 웹 액세스를 켤 때까지 복구 마법사를 사용할 수 없습니다. 원격 웹 액세스를 켜는 방법에 대한 자세한 내용은 [원격 웹 액세스 설정](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_TurnOnRWA)을 참조하세요.  
  
##### <a name="to-repair-remote-web-access"></a>원격 웹 액세스를 복구하려면  
  
1.  대시보드에 로그온합니다.  
  
2.  **설정**을 클릭한 다음 **원격 액세스** 탭을 클릭합니다.  
  
3.  **복구**를 클릭합니다. **원격 웹 액세스 복구** 마법사가 시작됩니다.  
  
4.  **다음**을 클릭합니다. 마법사에서 원격 웹 액세스를 분석하고 문제를 식별한 다음 문제를 복구하려고 합니다.  
  
5.  마법사가 완료될 때 경고가 표시되면 **다시 시도**를 클릭하여 문제를 다시 복구해 봅니다. 경고가 계속 표시되는 경우 경고에서 문제 및 문제 해결 단계에 대한 추가 정보를 확인하세요.  
  
##  <a name="BKMK_5"></a>원격 웹 액세스 문제 해결  
  
-   [원격 웹 액세스 연결 문제 해결](../support/Troubleshoot-Remote-Web-Access-connectivity-in-Windows-Server-Essentials.md)  
  
-   [방화벽 문제 해결](../support/Troubleshoot-your-firewall-in-Windows-Server-Essentials.md)  
  
-   [원격 액세스 문제 해결](../support/Troubleshoot-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
## <a name="see-also"></a>참고 항목  
  
-   [원격 데스크톱 옵션](Remote-desktop-options.md)  
  
-   [원격 웹 액세스 사용](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [원격 액세스 관리](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)
