---
title: My Server 앱을 사용하여 Windows Server Essentials에 연결
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e40b57f-6917-43ef-92e0-030baa9d2b99
9author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 3c7c5114bbd3aa479e2b6afe807fee2ec8d3d5bb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435878"
---
# <a name="use-the-my-server-app-to-connect-to-windows-server-essentials"></a>My Server 앱을 사용하여 Windows Server Essentials에 연결

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server Essentials 용 My Server 앱을 사용 하 여 리소스에 연결 하 고 노트북, PC 또는 Surface 장치에서 Windows Server Essentials 서버의 간단한 관리 작업을 수행할 수 있습니다. My Server에서 사용자, 장치 및 경보를 관리하고 서버에 있는 공유 파일에 대해 작업할 수 있습니다. 오프라인 상태에서도 My Server에서 최근에 액세스한 파일을 사용하여 계속 작업할 수 있으며 다음 번 연결 시 오프라인으로 변경한 내용이 서버와 자동으로 동기화됩니다.  
  
 서버는 Windows Server Essentials 운영 체제를 실행 하는 경우 원래 My Server 앱을 사용 합니다. 서버는 Windows Server Essentials 운영 체제를 실행 하는 경우 업데이트 된 My Server 2012 R2 앱을 사용 해야 합니다. 두 앱은 모두 [Windows용 앱](https://windows.microsoft.com/windows-8/apps)에서 다운로드할 수 있습니다.  
  
> [!TIP]
> 
>  에 Windows Phone Windows Server Essentials에서 리소스에 액세스 하려면 My Server phone 앱 (예: Windows Server Essentials) 또는 My Server 2012 R2 phone 앱 (예: Windows Server Essentials)를 사용 합니다. My Server phone 앱에 대 한 자세한 내용은 [Windows Phone 용 My Server 앱을 사용](Work-Remotely-in-Windows-Server-Essentials.md#BKMK_2)합니다. My Server 2012 R2 phone 앱에 대한 자세한 내용은 블로그 항목 [My Server 2012 R2 Windows 및 Windows Phone 앱](http://blogs.technet.com/b/sbs/archive/2013/11/19/my-server-2012-r2-windows-and-windows-phone-apps.aspx)을 참조하세요.  
  
## <a name="in-this-topic"></a>이 항목의 내용  
  
-   [My Server 2012 R2의 새로운 기능](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_WhatsNew)  
  
-   [운영 체제 요구 사항](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_OS)  
  
-   [My Server 설치](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_Install)  
  
-   [My Server 사용](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_UseServer)  
  
-   [My Server의 기능](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_Features)  
  
-   [로컬 네트워크에서 서버에 연결 하는 방법](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_ConnectServer)  

>  에 Windows Phone Windows Server Essentials에서 리소스에 액세스 하려면 My Server phone 앱 (예: Windows Server Essentials) 또는 My Server 2012 R2 phone 앱 (예: Windows Server Essentials)를 사용 합니다. My Server phone 앱에 대 한 자세한 내용은 [Windows Phone 용 My Server 앱을 사용](../use/Work-Remotely-in-Windows-Server-Essentials.md#BKMK_2)합니다. My Server 2012 R2 phone 앱에 대한 자세한 내용은 블로그 항목 [My Server 2012 R2 Windows 및 Windows Phone 앱](http://blogs.technet.com/b/sbs/archive/2013/11/19/my-server-2012-r2-windows-and-windows-phone-apps.aspx)을 참조하세요.  
  
## <a name="in-this-topic"></a>이 항목의 내용  
  
-   [My Server 2012 R2의 새로운 기능](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_WhatsNew)  
  
-   [운영 체제 요구 사항](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_OS)  
  
-   [My Server 설치](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_Install)  
  
-   [My Server 사용](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_UseServer)  
  
-   [My Server의 기능](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_Features)  
  
-   [로컬 네트워크에서 서버에 연결 하는 방법](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_ConnectServer)  

  
##  <a name="BKMK_WhatsNew"></a> My Server 2012 R2의 새로운 기능  
 My Server에서 사용할 수 있는 기능 외에도 My Server 2012 R2는 Windows Server Essentials를 사용 하 여 고객에 대 한 다음과 같은 새로운 기능을 제공합니다.  
  
-   **SharePoint Online 팀 사이트 및 라이브러리에 대 한 액세스** -My Server 2012 R2에서 SharePoint Online 라이브러리의 문서를 SharePoint Online 팀 사이트에 액세스 하는 Windows Server Essentials를 사용 하 여 활용 하 여 Microsoft Office 365 통합 합니다.  
  
-   **서버 및 클라이언트 컴퓨터에 대 한 원격 데스크톱 연결** -사용 **원격 연결** 에서 My Server 2012 R2 원격 데스크톱을 사용 하 여 Windows Server Essentials 서버 및 클라이언트 컴퓨터에 연결 합니다.  
  
##  <a name="BKMK_OS"></a> 운영 체제 요구 사항  
 My Server 또는 My Server 2012 R2에서 랩톱, PC 또는 Surface 장치를 사용 하려면 컴퓨터는 다음 운영 체제 중 하나가 있어야 합니다.  Windows 8.1, Windows RT 8.1, Windows 8 또는 Windows 직각  
  
##  <a name="BKMK_Install"></a> My Server 설치  
 [Windows용 앱](https://windows.microsoft.com/windows-8/apps) 스토어에서 해당 My Server 앱을 다운로드할 수 있습니다. 컴퓨터에 Windows 8 또는 Windows RT 운영 체제가 서버 이름을 사용 하 여 인트라넷의 서버에 연결 하려는 경우도 서버에서 인증서를 설치 해야 합니다.  
  
#### <a name="to-install-my-server-or-my-server-2012-r2-on-your-windows-based-laptop-pc-or-surface-device"></a>Windows 기반 노트북, PC 또는 Surface 장치에 My Server 또는 My Server 2012 R2를 설치하려면  
  
1.  Windows 기반 노트북, PC 또는 Surface 장치에 [Windows용 앱](https://windows.microsoft.com/windows-8/apps) 의 해당 My Server 앱을 설치합니다.  
  
    |서버 운영 체제|다운로드|  
    |-----------------------------|--------------|  
    | Windows Server Essentials|[내 서버](https://apps.microsoft.com/webpdp/app/19d94f81-db21-4234-8b49-806694dbbaea)|  
    | Windows Server Essentials|[My Server 2012 R2](https://apps.microsoft.com/webpdp/app/67e86695-bda3-4f32-96c4-2e20e56f1cf3)|  
  
2.  서버 이름을 사용 하 여 인트라넷, Windows Server Essentials 서버에 연결할 수 있게 되기를 원하는 경우 장치에 Windows 8 또는 Windows RT 운영 체제가 기본 CAROOT.cer 인증서를 컴퓨터에서 수행 하 여 설치 다음 p rocedure 합니다. Windows 8.1 및 Windows RT 8.1에서 인증서의 수동 설치 필요 하지 않습니다.  
  
###  <a name="BKMK_InstallCert"></a> Windows 8, Windows 8.1 또는 Windows RT 장치에서 My Server에 대 한 인증서를 설치 하려면  
  
1.  컴퓨터에서 웹 브라우저를 열고 서버의 기본 인증서인 CAROOT.cer을 다운로드합니다. 이렇게 하려면 서버 이름을 대체하여 다음을 입력합니다. 예를 들어 <*서버 이름*>을 **marketing.contoso.com**으로 대체합니다.  
  
     **http://<servername\>/connect/default.aspx?get=caroot.cer**  
  
2.  인증서를 설치합니다.  
  
    1.  **시작** 페이지에서 **파일 탐색기**를 엽니다.  
  
    2.  숨겨진 항목 및 파일 이름 확장명이 표시되는지 확인합니다. **보기** 탭의 **표시/숨기기** 그룹에서 **숨겨진 항목** 및 **파일 이름 확장명** 확인란을 선택합니다.  
  
    3.  방금 다운로드한 CAROOT.cer 파일이 들어 있는 폴더로 이동합니다.  
  
    4.  CAROOT.cer 파일을 마우스 오른쪽 단추로 클릭한 다음 **열기**를 클릭합니다.  
  
    5.  **인증서** 대화 상자에서 **인증서 설치**를 클릭합니다.  
  
    6.  **로컬 컴퓨터**를 설치 위치로 선택하고 **다음**을 클릭합니다.  
  
    7.  **인증서 저장소** 마법사 페이지에서 **모든 인증서를 다음 저장소에 저장**을 선택하고 **찾아보기** 를 사용하여 **신뢰할 수 있는 루트 인증 기관** 저장소를 선택합니다. **마침**을 클릭합니다.  
  
##  <a name="BKMK_UseServer"></a> My Server 사용  
 My Server 또는 My Server 2012 R2 앱을 사용하려면 앱을 열고 기능을 간략히 살펴봅니다.  
  
#### <a name="to-open-my-server-or-my-server-2012-r2"></a>My Server 또는 My Server 2012 R2를 열려면  
  
1.  (Windows Server Essentials) 용 My Server 또는 Windows Server Essentials) (용 My Server 2012 R2에서 엽니다는 **시작** Windows 장치의 페이지입니다.  
  
2.  서버에서 사용자 계정을 사용 하 여 Windows Server Essentials 서버에 로그인 합니다. 서버를 식별하려면  
  
    -   오프-프레미스 환경에서 사용 하 여 서버의 도메인 이름-예를 들어 **marketing.contoso.com**합니다.  
  
    -   이전 예제에서 서버 이름-를 사용 하 여 인트라넷을 통해 온-프레미스를 연결 하는 경우, 서버 이름은 **마케팅**합니다. (온-프레미스에 연결 하는 Windows 8 또는 Windows RT 컴퓨터를 사용 하는 경우이 메서드를 사용 하려면 설치 해야 CAROOT.cer 인증서를 서버에서. 자세한 내용은 [Windows 8, Windows 8.1 또는 Windows RT 장치에서 My Server에 대 한 인증서를 설치 하려면](#BKMK_InstallCert).)  
  
###  <a name="BKMK_Features"></a> My Server의 기능  
 다음 표에서는 My Server 및 My Server 2012 R2 앱의 기능에 대해 설명합니다. 서버의 사용자 계정 유형에 따라 표시되는 항목과 수행할 수 있는 작업이 결정됩니다. 모든 사용자가 공유 리소스로 작업하고, **최근 항목** 표시를 사용자 지정하고, 오프라인 액세스를 위해 최근에 사용한 파일을 캐시할 기간을 결정하고, 유료 연결을 통한 다운로드를 켜거나 끌 수 있습니다. 또한 Windows Server Essentials 서버에서 관리자 경고, 장치 및 사용자가 관리할 수 있습니다. 표준 사용자 계정은 사용자 계정의 속성에 따라 경고를 보고 장치에 연결하는 기능이 보다 제한됩니다. 개별 기능에 대한 요구 사항은 다음 표에 나와 있습니다.  
  
### <a name="features-of-the-my-server-and-my-server-2012-r2-apps-for-windows-server-essentials"></a>Windows Server Essentials용 My Server 및 My Server 2012 R2 앱의 기능  
  
|기능 집합|설명|  
|-----------------|-----------------|  
|경고 관리|-(관리자 전용) 해결 서버에서 경고 또는 작업을 요구 하지 않는 경고를 무시 합니다. 알림 켜기/끄기(**사용 권한** 설정, **알림** 옵션)<br />-(표준 사용자 계정) 네트워크 상태 경고 보기입니다.<br />     **참고:** My Server에서 경고를 보려는 사용자에 대 한 합니다 **사용자는 네트워크 상태 경고를 볼 수 있습니다** 설정을 선택 해야 **일반** 사용자 계정의 설정 합니다. 자세한 내용은 [Manage user accounts using the Dashboard](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage8)를 참조하세요.|  
|장치 관리|(관리자만 해당)<br /><br /> -Windows Server Essentials 서버에 연결할 때 연결 된 각 컴퓨터에 대 한 세부 정보를 볼 **장치** 보기. 오프라인 장치는 회색으로 표시됩니다.<br />-시작 및 연결 된 컴퓨터의 백업을 중지 합니다.<br />-My Server에서 알림 또는 해제를 설정 합니다. (**사용 권한** 설정, **알림** 옵션)<br /><br /> 모든 사용자:<br /><br /> -사용자 계정에 액세스할 수 있는 클라이언트 컴퓨터를 확인 합니다. (**장치** 표시)<br />-해당 컴퓨터에 대 한 경고를 모니터링 합니다. (**경고** 표시)<br />-(My Server 2012 R2만 해당)에서 원격 웹 액세스를 사용 하 여 해당 컴퓨터에 연결 합니다. (**장치** 표시, **원격 연결** 단추)|  
|원격 데스크톱을 사용하여 컴퓨터에 연결|(My Server 2012 R2만 해당) Windows Server Essentials 서버 또는 클라이언트 컴퓨터를 사용 하 여 원격 데스크톱 세션을 엽니다. (**장치** 표시, **원격 연결** 단추)<br /><br /> **참고:** 이 기능을 사용하도록 설정하려면 컴퓨터의 Windows용 앱에서 [원격 데스크톱 앱](https://apps.microsoft.com/webpdp/app/051f560e-5e9b-4dad-8b2e-fa5e0b05a480)을 다운로드하여 설치합니다. 표준 사용자 계정은 로그온할 수 있는 권한이 있는 장치에 연결할 수 있습니다. 사용자가 컴퓨터에 로그온할 수 있게 하려면 사용자 계정의 **컴퓨터 액세스** 탭에 컴퓨터를 추가합니다. 자세한 내용은 [Assign user accounts permission to log on to specific network computers](../manage/Manage-Devices-in-Windows-Server-Essentials.md#BKMK_2)를 참조하세요.|  
|사용자 관리|(관리자만 해당) 사용자 계정의 암호를 변경합니다. 서버에서 사용자의 세션을 종료 합니다. (**사용자** 설정)|  
|공유 파일 작업|<ul><li>업로드 및 다운로드에서에서 파일 공유 파일 (공유 폴더에 액세스할 수는 서버에서), 개인 또는 Windows 8.1 장치, SkyDrive 또는 네트워크 저장소에서. 폴더를 만듭니다. 서버에서 파일을 추가(업로드), 편집 및 삭제합니다.</li><li>파일을 업로드 또는 다운로드하는 동안 전송 상태를 봅니다. 전송을 취소합니다. 파일 충돌을 해결합니다.</li><li>로컬 컴퓨터, 서버, SkyDrive 또는 네트워크 저장소의 파일 및 폴더로 매끄럽게 작업합니다. 파일 목록에는 서버의 공유 폴더와 함께 컴퓨터, SkyDrive 또는 네트워크 저장소에서 최근에 사용한 폴더가 표시되며 해당 위치의 폴더를 탐색할 수 있습니다.</li><li>서버에서 폴더 및 파일을 검색하고 파일을 클릭하여 다운로드한 다음 기본 앱에서 엽니다. 오프라인 모드에서는 오프라인 파일만 검색합니다.</li><li>사진, 음악 및 동영상을 공유합니다. Windows 8 사진, 음악 또는 비디오 플레이어에서 열려는 파일을 클릭 합니다. 또는 **열기** 또는 **연결 프로그램**을 사용하여 다른 앱에서 파일을 엽니다. 일반적인 방법으로, 선택한 앱을 해당 미디어 형식의 기본 앱으로 만들 수 있습니다.<br /><br />     **참고:** 기본적으로 미디어 스트리밍 기능을 사용할 수 없는 경우 Windows Server Essentials 및 Windows Server 2012 R2에서 Windows Server Essentials Experience 역할이 설치 된 자세한 내용은 [디지털 미디어 관리](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md)합니다.<br /><br /> <ul><li>**사진** - **사진** 보기에서 사진을 탭하여 엽니다. 사진을 다시 탭하면 My Server의 미리 보기로 돌아갑니다.</li><li>**음악** - **음악** 보기, 앨범 또는 노래 서버에서 공유를 봅니다. 항목을 탭하여 음악 플레이어에서 엽니다.</li><li>**비디오** -의 미리 보기를 클릭 **비디오** 보기 비디오 플레이어를 엽니다.</li></ul></li></ul>|  
|SharePoint Online 라이브러리 사용|(My Server 2012 R2만 해당) 팀의 SharePoint Online 라이브러리에 파일을 사용 합니다. 팀 사이트를 엽니다. SharePoint Online 섹션: 팀 사이트를 열고 열려는 문서 라이브러리 또는 파일로 드릴다운합니다. 파일을 열 때 로그인 해야 합니다 Office 365 네트워크 계정과 연결 된 Microsoft 온라인 계정을 사용 하 여.)<br /><br /> **참고:** 이 기능을 사용 하는 서버를 Office 365와 통합, Office 365 구독을 SharePoint Online 포함 해야 하며 서버에서 사용자 계정에 연결 된 Microsoft Online Services 계정이 있어야 합니다. Windows Server Essentials와 Office 365 및 SharePoint Online 통합에 대 한 자세한 내용은 [서비스 통합 개요에 대 한 Windows Server Essentials-1 부](http://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-1.aspx) 고 [에 대 한 서비스 통합 개요 Windows Server Essentials-2 부](http://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-2.aspx)합니다.|  
|**최근 항목** 표시 사용자 지정|**최근 항목** 목록에서는 현재 작업 중인 파일에 빠르게 액세스할 수 있습니다. 다음과 같이 변경할 수 있습니다.<br /><br /> -표시할 최근 파일 히스토리의 일 수를 설정 합니다. (**최근 항목** 설정: **최근 항목에 유지할 기간(일)** , 기본값 = 7일)<br />-선택을 취소 합니다 **최근** 더 이상 사용 하 여 작업 중인 파일을 작업 해야 할 경우를 표시 합니다. 이 작업은 캐시에 영향을 주지 않습니다. 여전히 오프라인에서 파일을 사용할 수 있습니다. (**최근 항목** 설정: **지우기** 단추)<br />     **팁:** 사용 하 여 오프 라인 파일에 액세스할 필요가 없는 경우 **모두 지우기** 에 **오프 라인** 캐시에서 파일을 제거 하려면 설정 합니다.|  
|오프라인으로 작업|기본적으로 지난 7일 동안 액세스한 파일은 오프라인에서 사용할 수 있습니다. 서버에 연결할 때마다 오프라인 변경 내용이 서버와 동기화됩니다.<br /><br /> 오프라인 구성을 다음과 같이 변경할 수 있습니다.<br /><br /> -캐시에 작업의 일 수를 변경 합니다. (**오프 라인** My Server에서 설정 **파일** My Server 2012 R2에서 설정 합니다. **캐싱 기간**, 기본값 = 7일)<br />-유료 네트워크를 통한 파일 전송을 허용 하거나 해당 기능을 해제 합니다. 이 기능은 유료 네트워크를 통한 고비용 파일 전송을 방지하기 위해 기본적으로 꺼져 있습니다. (**오프라인** 또는 **파일** 설정: **유료 네트워크를 통한 파일 자동 전송 켜기/끄기**, 기본값 = **끄기**)<br />-가끔 하려는 캐시를 지웁니다. **최근 항목** 또는 **파일** 설정에서 캐시의 크기를 확인한 다음 **지우기** 또는 **모두 지우기** 를 사용하여 캐시를 지웁니다.<br /><br /> **팁:** 오프라인에서 사용할 수 있는 파일을 확인하려면 공유 폴더에서 **모두** 대신 오프라인 캐시 필터를 선택합니다.<br /><br /> **참고:** 기본적으로 캐시는 **최근 항목** 목록에 표시되는 것과 동일한 파일 히스토리를 저장합니다. 캐시를 지우거나 캐시 및 **최근 항목** 표시에 대한 설정이 일치하지 않는 경우 **최근 항목** 목록의 일부 파일을 오프라인에서 사용하지 못할 수 있습니다.|  
|백그라운드 동기화|My Server에 로그온할 때마다 및 서버에 연결된 동안 변경 작업을 수행하면 파일이 서버와 동기화됩니다. 성능을 유지하기 위해 대부분의 폴더에서는 리소스를 많이 사용하는 백그라운드 동기화가 자동으로 수행되지 않습니다. 고비용 전송을 방지하기 위해 3GB 네트워크에서는 백그라운드 동기화가 수행되지 않습니다.<br /><br /> -에 표시 되는 파일 충돌을 해결 합니다 **충돌 하는** 영역의 합니다 **전송 상태** 페이지. 파일 전송을 수행되는 경우 주 화면에 **전송 상태** 및 **경고** 참 메뉴가 표시됩니다.|  
  
##  <a name="BKMK_ConnectServer"></a> 로컬 네트워크에서 서버에 연결 하는 방법  
 Windows Server Essentials에서 Windows Phone, Windows 8 및 Windows 8.1용 My Server 앱을 사용하려면 먼저 장치에 서버 인증서를 설치해야 합니다. 이렇게 하면 로컬 네트워크에서 Windows Server Essentials를 실행하는 서버에 장치가 연결됩니다. 다음 절차에 따라 로컬 네트워크의 서버에 연결하고 Windows 8 또는 Windows 8.1을 실행하는 컴퓨터나 Windows Phone에 서버 인증서를 설치합니다.  
  
#### <a name="to-connect-to-your-server-from-your-windows-phone"></a>Windows Phone에서 서버에 연결하려면  
  
1.  Windows 8 또는 Windows 8.1을 실행하는 Windows Phone에서 Internet Explorer를 엽니다.  
  
2.  주소 표시줄에 입력 **http://<yourservername\>/connect/default.aspx?get=caroot.cer**, 한 다음 Enter를 누릅니다.  
  
3.  caroot.cer 인증서를 설치하라는 메시지가 표시되면 **설치**를 클릭합니다.  
  
4.  인증서 설치가 완료될 때까지 기다립니다.  
  
    > [!NOTE]
    >  인증서 설치가 완료되면 서버 이름 및 네트워크 자격 증명을 사용하여 Windows Phone용 My Server 앱에 로그인할 수 있습니다.  
  
#### <a name="to-connect-to-your-server-in-your-local-network-from-a-computer-running-windows-8-or-windows-81"></a>Windows 8 또는 Windows 8.1을 실행하는 컴퓨터에서 로컬 네트워크의 서버에 연결하려면  
  
1.  Windows 8 또는 Windows 8.1을 실행하는 컴퓨터에서 Internet Explorer를 엽니다.  
  
2.  주소 표시줄에 입력 **http://<yourservername\>/connect/default.aspx?get=caroot.cer**, 한 다음 Enter를 누릅니다.  
  
3.  caroot.cer 인증서를 설치하라는 메시지가 표시되면 **열기**를 클릭합니다.  
  
4.  **인증서** 대화 상자에서 **인증서 설치**를 클릭합니다.  
  
5.  인증서 가져오기 마법사에서 **로컬 컴퓨터** 를 저장소 위치로 선택합니다.  
  
6.  **모든 인증서를 다음 저장소에 저장**을 선택하고 **신뢰할 수 있는 루트 인증 기관** 위치를 찾습니다.  
  
7.  지시에 따라 마법사를 완료합니다.  
  
    > [!NOTE]
    >  인증서 설치가 완료되면 서버 이름 및 네트워크 자격 증명을 사용하여 Windows 8 또는 Windows 8.1용 My Server 앱에 로그인할 수 있습니다.  
  
## <a name="see-also"></a>참조  
  
-   [Windows Server Essentials-1 부에 대 한 서비스 통합 개요](http://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-1.aspx)  
  
-   [Windows Server Essentials-2 부에 대 한 서비스 통합 개요](http://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-2.aspx)  
  
-   [원격 액세스 관리](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](../manage/Manage-Windows-Server-Essentials.md)  
  

-   [원격 작업](Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 사용](Use-Windows-Server-Essentials.md)

-   [원격 작업](../use/Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 사용](../use/Use-Windows-Server-Essentials.md)

