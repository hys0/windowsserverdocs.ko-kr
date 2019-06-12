---
title: Windows Server Essentials에서 디지털 미디어 재생
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f570492-ee21-471b-92c1-3fd9bfb84f55
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f38d234768d40903615145954f1215546119344a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435944"
---
# <a name="play-digital-media-in-windows-server-essentials"></a>Windows Server Essentials에서 디지털 미디어 재생

>적용 대상: Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

디지털 미디어는 디지털 방식으로 압축된 오디오, 비디오 및 사진 콘텐츠를 나타냅니다.  Windows Server Essentials로 인해 네트워크에 연결 된 컴퓨터와 일부 네트워크 서버에 저장 된 디지털 미디어 파일을 재생 하려면 디지털 미디어 장치를 사용 하 고 연결 합니다.  
  
 다음 항목에 액세스 하 고 Windows Server Essentials에 저장 된 디지털 미디어 파일을 재생 하는 방법에 대 한 정보를 제공 합니다.  
  

-   [디지털 미디어 개요](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [재생 및 공유 디지털 미디어](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [원격 위치에서 공유 디지털 미디어 파일 재생](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [서버에 디지털 미디어 파일 추가](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [다운로드 형식 옵션](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [간편한 파일 업로드 도구](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [공유 디지털 미디어 보기 및 찾아보기](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_7)  

-   [디지털 미디어 개요](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [재생 및 공유 디지털 미디어](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [원격 위치에서 공유 디지털 미디어 파일 재생](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [서버에 디지털 미디어 파일 추가](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [다운로드 형식 옵션](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [간편한 파일 업로드 도구](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [공유 디지털 미디어 보기 및 찾아보기](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_7)  

  
##  <a name="BKMK_1"></a> 디지털 미디어 개요  
 디지털 미디어는 인코딩된(디지털 방식으로 압축된) 오디오, 비디오 및 사진 콘텐츠를 나타냅니다. 콘텐츠 인코딩을 통해 Windows Media 파일과 같은 오디오 및 비디오 입력을 디지털 미디어 파일로 변환합니다. 디지털 미디어는 인코딩되고 나면 컴퓨터에서 손쉽게 조작, 배포 및 재생할 수 있고 컴퓨터 네트워크를 통해 손쉽게 전송됩니다.  
  
 디지털 미디어 유형의 예는 다음과 같습니다. WMA(Windows Media 오디오), WMV(Windows Media 비디오), MP3, JPEG, AVI. Windows Media Player에서 지원되는 디지털 미디어 유형에 대한 자세한 내용은 [Windows Media Player에서 지원되는 파일 형식](https://support.microsoft.com/kb/316992)을 참조하세요.  
  
### <a name="why-would-i-want-to-stream-my-digital-media"></a>디지털 미디어를 스트리밍하려는 이유  
 많은 사람들이 Windows Server Essentials의 공유 폴더에 음악, 비디오 및 사진을 저장합니다. 다음과 같은 작업을 수행할 수 있습니다.  
  
-   **비디오 보기**. 서버를 사용하여 비디오 및 녹화된 TV 프로그램의 광범위한 모음을 네트워크의 컴퓨터 및 기타 재생 장치에 저장하고 스트리밍할 수 있습니다. Windows Media Player를 사용하여 Xbox 360 또는 컴퓨터에 비디오를 스트리밍할 수 있습니다.  
  
-   **음악 재생**. **음악** 공유 폴더에 대한 미디어 공유를 켜면 Windows Media Connect를 지원하는 장치에서 음악에 액세스할 수 있습니다. 공유 기능을 켜고 나면 사용자 계정을 사용하도록 설정하고 **음악** 공유 폴더에서 스트리밍하도록 구성할 필요가 없습니다.  
  
-   **사진 슬라이드 쇼 제공**. 서버의 **사진** 공유 폴더에 디지털 사진을 저장하고 집이나 사무실에 있는 TV에 연결된 Xbox 360 또는 컴퓨터에서 디지털 사진에 액세스할 수 있습니다. TV를 대형 사진 프레임으로 전환하는 것처럼 사진 슬라이드 쇼를 볼 수 있습니다.  
  
### <a name="sharing-copy-protected-media"></a>복사 방지된 미디어 공유  
  Windows Server Essentials 복사 방지 된 미디어를 공유 하는 것을 지원 하지 않습니다. 여기에는 온라인 음악 스토어를 통해 구매한 음악이 포함됩니다.  
  
 복사 방지된 미디어는 미디어를 구매할 때 사용한 컴퓨터나 장치에서만 재생할 수 있습니다. 복사 방지를 사용하면 미디어를 서버로 복사하고 서버에서 재생하더라도 두 대 이상의 컴퓨터 또는 장치에서 미디어를 재생할 수 없습니다. 그러나 Windows Server Essentials에 복사 방지 된 미디어를 저장할 수 있으며 컴퓨터 또는 장치 구매 하는 데에 미디어 재생을 계속 합니다.  
  
##  <a name="BKMK_2"></a> 재생 및 공유 디지털 미디어  
 네트워크를 설정하고 컴퓨터와 미디어 장치를 서버 네트워크에 연결하고 나면 서버에서 저장 및 공유하는 디지털 미디어 파일을 검색할 수 있습니다.  
  
> [!NOTE]
>  Windows Server Essentials와 호환 되는 디지털 미디어 플레이어/수신 장치의의 현재 목록에 대 한 참조를 [Windows 호환성 센터](https://www.microsoft.com/windows/compatibility/CompatCenter/Home)합니다.  
  
 다음 방법의 하나를 사용하여 서버에 저장된 디지털 미디어 파일을 검색 및 재생할 수 있습니다.  
  

-   [검색 및 네트워크에서 컴퓨터 또는 디지털 media player에서 Windows Server Essentials의 미디어 파일 재생](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)  
  
-   [Windows Media Player, Xbox 360 또는 네트워크에서 네트워크에 연결 된 디지털 미디어 플레이어를 Windows Server Essentials의 미디어 파일 보내기](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SendToDevice)  

-   [검색 및 네트워크에서 컴퓨터 또는 디지털 media player에서 Windows Server Essentials의 미디어 파일 재생](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)  
  
-   [Windows Media Player, Xbox 360 또는 네트워크에서 네트워크에 연결 된 디지털 미디어 플레이어를 Windows Server Essentials의 미디어 파일 보내기](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SendToDevice)  

  
###  <a name="BKMK_2.1"></a> 검색 및 네트워크에서 컴퓨터 또는 디지털 media player에서 Windows Server Essentials의 미디어 파일 재생  
 장치에 Windows Server Essentials 네트워크에 가입 하는 경우 검색 하 고 다음 방법 중 하나에서 디지털 미디어 파일을 재생할 수 있습니다.:  
  

-   [검색 및 Windows Media Center를 실행 하는 컴퓨터에서 미디어 파일 재생](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_WMC)  
  
-   [검색 및 Windows Media Player를 사용 하 여 Windows를 실행 하는 컴퓨터에서 미디어 파일 재생](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_MWP)  
  
-   [검색 및 Xbox 360을 사용 하 여 미디어 파일 재생](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Xbox)  
  
-   [검색 및 기타 디지털 미디어 플레이어 또는 Windows Server Essentials와 호환 되는 수신기를 사용 하 여 미디어 파일 재생](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Other)  
  
-   [검색 및 실행 패드의 공유 폴더 기능을 사용 하 여 미디어 파일 재생](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SharedFolders)  
  
-   [검색 및 원격 웹 액세스를 사용 하 여 공유 미디어 재생](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_RWA2)  

-   [검색 및 Windows Media Center를 실행 하는 컴퓨터에서 미디어 파일 재생](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_WMC)  
  
-   [검색 및 Windows Media Player를 사용 하 여 Windows를 실행 하는 컴퓨터에서 미디어 파일 재생](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_MWP)  
  
-   [검색 및 Xbox 360을 사용 하 여 미디어 파일 재생](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Xbox)  
  
-   [검색 및 기타 디지털 미디어 플레이어 또는 Windows Server Essentials와 호환 되는 수신기를 사용 하 여 미디어 파일 재생](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Other)  
  
-   [검색 및 실행 패드의 공유 폴더 기능을 사용 하 여 미디어 파일 재생](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SharedFolders)  
  
-   [검색 및 원격 웹 액세스를 사용 하 여 공유 미디어 재생](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_RWA2)  

  
####  <a name="BKMK_WMC"></a> 검색 및 Windows Media Center를 실행 하는 컴퓨터에서 미디어 파일 재생  
  
1.  **시작**, **모든 프로그램**, **Windows Media Center**를 차례로 클릭합니다.  
  
2.  **Windows Media Center** 페이지에서 검색할 미디어 유형으로 스크롤하고 미디어 라이브러리를 클릭합니다.  
  
3.  원하는 파일을 수동으로 검색하거나, **검색** 을 클릭하고 찾으려는 파일의 이름을 입력합니다.  
  
4.  미디어 파일 이미지를 클릭하여 파일을 확인하고 재생합니다.  
  
####  <a name="BKMK_MWP"></a> 검색 및 Windows Media Player를 사용 하 여 Windows를 실행 하는 컴퓨터에서 미디어 파일 재생  
  
-   컴퓨터 또는 미디어 장치에서 **Windows Media Player** 를 열고 미디어 라이브러리를 검색합니다.  
  
    > [!NOTE]
    >  검색 단계는 사용 중인 Windows Media Player 버전에 따라 달라집니다. 자세한 내용은 해당 버전에 대한 도움말을 참조하세요.  
  
####  <a name="BKMK_Xbox"></a> 검색 및 Xbox 360을 사용 하 여 미디어 파일 재생  
  
1.  유선 또는 무선 연결을 사용하여 Xbox 360 콘솔을 홈 네트워크에 연결합니다.  
  
2.  Windows Server Essentials를 실행 하는 컴퓨터에서 미디어 공유 설정 합니다. 자세한 내용은 항목을 참조 하세요 [미디어 스트리밍을 켜거나 끌](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)합니다.  
  
3.  Xbox 360 콘솔을 사용하여 디지털 미디어 파일을 재생하려면:  
  
    1.  **내 Xbox**로 이동하고 보거나 재생하려는 미디어 유형에 따라 **비디오 라이브러리**, **음악 라이브러리**또는 **사진 라이브러리**를 선택합니다.  
  
    2.  서버 이름을 선택합니다.  
  
        > [!NOTE]
        >  서버 이름이 목록에 없으면 **컴퓨터**를 선택하고 **연결 테스트**를 클릭합니다.  
  
    3.  파일 목록을 찾아보고 재생할 항목을 선택합니다.  
  
####  <a name="BKMK_Other"></a> 검색 및 기타 디지털 미디어 플레이어 또는 Windows Server Essentials와 호환 되는 수신기를 사용 하 여 미디어 파일 재생  
  
1.  [Windows 호환성 센터](https://www.microsoft.com/windows/compatibility/CompatCenter/Home) 로 이동하여 사용 중인 호환 장치 목록에 디지털 미디어 플레이어 또는 수신기가 표시되는지 확인합니다.  
  
2.  사용 중인 디지털 미디어 플레이어에 따라 검색 단계가 달라지므로 자세한 지침은 장치에 대한 도움말을 참조하세요.  
  
####  <a name="BKMK_SharedFolders"></a> 검색 및 실행 패드의 공유 폴더 기능을 사용 하 여 미디어 파일 재생  
  
1.  Windows Server Essentials 실행 패드에 로그인 합니다.  
  
2.  실행 패드에서 **공유 폴더**를 클릭합니다. Windows 탐색기 창이 열리고 서버에 있는 공유 폴더가 표시됩니다.  
  
3.  **검색** 상자에 미디어 파일의 이름을 입력합니다. 검색 쿼리 결과가 표시됩니다.  
  
    > [!NOTE]
    >  필요한 경우 공유 폴더를 두 번 클릭하여 폴더 콘텐츠를 찾아볼 수도 있습니다.  
  
####  <a name="BKMK_RWA2"></a> 검색 및 원격 웹 액세스를 사용 하 여 공유 미디어 재생  
  
1.  원격 웹 액세스에 로그온합니다.  
  
2.  **공유 폴더**를 클릭합니다. 웹 페이지의 **공유 폴더** 섹션에는 서버에 있는 공유 폴더 목록이 표시됩니다.  
  
3.  폴더를 두 번 클릭하여 폴더 콘텐츠를 확인합니다.  
  
###  <a name="BKMK_SendToDevice"></a> Windows Media Player, Xbox 360 또는 네트워크에서 네트워크에 연결 된 디지털 미디어 플레이어를 Windows Server Essentials의 미디어 파일 보내기  
 **Windows Media Player**를 사용하여 원하는 미디어 파일을 검색합니다. 미디어 파일을 마우스 오른쪽 단추로 클릭하고 **재생**을 클릭하여 미디어 파일을 네트워크로 연결된 미디어 장치로 보냅니다.  
  
##  <a name="BKMK_3"></a> 원격 위치에서 공유 디지털 미디어 파일 재생  
 원격 웹 액세스를 사용 하 여 Windows Server Essentials 네트워크에서 멀리 있을 때 미디어 파일을 재생할 수 있습니다. 이동 전화, 원격 컴퓨터 또는 디지털 미디어 플레이어를 사용하여 서버에 저장한 공유 미디어 파일을 검색하고 재생할 수 있습니다.  
  
#### <a name="to-play-shared-media-files-when-you-are-away-from-the-network"></a>네트워크에서 멀리 있을 때 공유 미디어 파일을 재생하려면  
  
1. 인터넷 브라우저를 엽니다.  
  
2. 원격 웹 액세스 웹 사이트로 이동합니다. 형식 **https://<YourDomainName\>/원격** 한 다음 Enter 키를 눌러 확인 하 고 인터넷 브라우저의 주소 표시줄에 있습니다.  
  
   > [!NOTE]
   >  *< YourDomainName\>*  자리 표시자입니다. 입력할 주소 모양은 이므로 서버에 고유한 이름이 됩니다 **https://contoso.com/remote** 합니다. 도메인 이름을 잘 모르면 서버에서 원격 액세스 기능이 설정될 때 도메인 이름을 선택한 관리자에게 문의하세요. 자세한 내용은 [Turn on Remote Web Access](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_TurnOnRWA)를 참조하세요.  
  
3. 원격 웹 액세스 로그인 페이지에서 사용자 계정 이름과 암호를 입력하고 화살표를 클릭합니다.  
  
4. 원하는 방법으로 재생할 미디어 파일을 검색합니다.  
  
   > [!NOTE]
   > 
   >  다양 한에 대 한 정보에 대 한 검색 방법, 참조 [검색 하는 컴퓨터 또는 디지털 media player 네트워크에서의 Windows Server Essentials의 미디어 파일 재생](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)합니다.  
   > 
   >  다양 한에 대 한 정보에 대 한 검색 방법, 참조 [검색 하는 컴퓨터 또는 디지털 media player 네트워크에서의 Windows Server Essentials의 미디어 파일 재생](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)합니다.  

  
5. 미디어 파일 이름이 나타나면 파일 이름을 클릭하여 미디어를 재생합니다.  
  
##  <a name="BKMK_4"></a> 서버에 디지털 미디어 파일 추가  

 서버 관리자 서버에 직접 액세스 하거나 대시보드에 로그인 하 여 원격 웹 액세스 사이트를 사용 하 여 미디어 라이브러리의 공유 폴더에 디지털 미디어를 추가할 수 있습니다. 다른 사용자를 사용 하 여 서버에 미디어 파일에 추가할 수는 **공유 폴더** 실행 패드, 원격 웹 액세스 사이트를 사용 하 여 또는 Windows Phone 용 My Server 앱을 사용 하 여에 연결 합니다. 미디어 재생에 대한 자세한 내용은 [디지털 미디어 재생 및 공유](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)를 참조하세요.  

 서버 관리자 서버에 직접 액세스 하거나 대시보드에 로그인 하 여 원격 웹 액세스 사이트를 사용 하 여 미디어 라이브러리의 공유 폴더에 디지털 미디어를 추가할 수 있습니다. 다른 사용자를 사용 하 여 서버에 미디어 파일에 추가할 수는 **공유 폴더** 실행 패드, 원격 웹 액세스 사이트를 사용 하 여 또는 Windows Phone 용 My Server 앱을 사용 하 여에 연결 합니다. 미디어 재생에 대한 자세한 내용은 [디지털 미디어 재생 및 공유](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)를 참조하세요.  

  
> [!NOTE]
>  Windows Phone용 내 서버 앱을 사용하여 서버에 미디어 파일을 업로드할 수도 있습니다. [Windows Phone 스토어](http://www.windowsphone.com/store/app/my-server/6c2f98d5-6fcf-4e1d-b8b1-cde62ea1a94a)에서 My Server 앱을 다운로드할 수 있습니다. Windows Phone My Server 앱에 대 한 자세한 내용은 블로그 게시물을 참조 하세요 [Windows Server Essentials 용 My Server phone 앱](http://blogs.technet.com/b/sbs/archive/2012/09/18/my-server-phone-app-for-windows-server-2012-essentials.aspx)합니다.  
  
#### <a name="to-add-digital-media-files-to-shared-folders-on-the-server"></a>서버의 공유 폴더에 디지털 미디어 파일을 추가하려면  
  
1.  다음 방법의 하나를 사용하여 서버에 로그인합니다.  
  

    1.  원격 웹 액세스에 로그온 하는 방법에 대 한 내용은 [Use Remote Web Access](Use-Remote-Web-Access-in-Windows-Server-Essentials.md)합니다.  

    1.  원격 웹 액세스에 로그온 하는 방법에 대 한 내용은 [Use Remote Web Access](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)합니다.  

  
    2.  실행 패드에 로그인 하는 방법에 대 한 내용은 [실행 패드 개요](../manage/Overview-of-the-Launchpad-in-Windows-Server-Essentials.md)합니다.  
  
2.  추가할 미디어에 대한 폴더를 검색하고 클릭합니다.  
  
3.  서버의 해당 공유 폴더에 추가할 미디어 파일을 복사 후 붙여넣거나 끌어서 놓습니다.  
  
##  <a name="BKMK_5"></a> 다운로드 형식 옵션  
 파일을 다운로드하기 위한 두 가지 옵션이 있습니다. 이러한 옵션은 Windows 기반 컴퓨터에 여러 파일 또는 폴더를 다운로드하는 경우에만 사용할 수 있습니다.  
  
 다운로드 요구 사항에 맞는 다음 옵션을 선택합니다.  
  
- **압축 된 ZIP 파일 (.zip)**  
  
   파일을 압축하면 원본 파일보다 더 작은 압축 버전 파일이 생성됩니다. 압축 버전 파일에는 .zip 파일 이름 확장명이 있습니다. 압축으로 크기가 최대한 감소하는 파일 형식은 텍스트 기반 파일 형식(예: .txt, .doc, .xls) 및 압축되지 않은 파일 형식을 사용하는 그래픽 파일(예: .bmp)입니다. 일부 그래픽 파일(예: .jpg 및 .gif 파일)은 이미 압축을 사용하고 압축으로 파일 크기가 거의 감소하지 않습니다. 또한 많은 그래픽이 포함된 Word 문서는 대부분 텍스트인 문서만큼 크기가 많이 감소하지 않습니다.  
  
  > [!NOTE]
  >  이 옵션은 국제 파일 이름에 대한 제한된 지원을 제공합니다.  
  
- **자동 압축 풀기 실행 파일 (.exe)**  
  
   자동 압축 풀기 실행 파일은 압축된 파일과 압축 풀기(실행 파일) 프로그램을 결합하는 다운로드할 수 있는 파일입니다. 실행 프로그램을 실행하면 압축된 파일의 압축이 자동으로 풀립니다. 이 방법은 받는 사람에게 적합한 압축 풀기 유틸리티가 있는지에 관계없이 압축된 데이터를 배포하는 일반적인 방법입니다.  
  
  > [!NOTE]
  >  이 옵션은 유니코드 문자를 지원합니다.  
  
  실제 다운로드가 시작되기 전에 exe 또는 zip 파일이 생성됩니다. 다운로드되는 파일 개수 및 총 파일 크기에 따라 몇 분이 걸릴 수 있습니다. 다운로드 파일이 생성되고 나면 파일 다운로드는 백그라운드에서 수행됩니다. 따라서 다운로드 프로세스가 완료되는 동안 작업을 계속할 수 있습니다.  
  
##  <a name="BKMK_6"></a> 간편한 파일 업로드 도구  
 간편한 파일 업로드 도구는 Windows Server Essentials 서버의 파일을 업로드 하는 프로세스를 간소화 합니다. 간편한 파일 업로드 도구에 원하는 만큼 단일 일괄 처리는 Windows Server Essentials 서버의 공유 폴더에 업로드할 파일을 추가할 수 있습니다. 자세한 내용은 블로그 게시물 [원격 웹 액세스 파일 공유 이해](http://blogs.technet.com/b/sbs/archive/2012/04/19/understanding-remote-web-access-file-sharing.aspx)(영문)를 참조하세요.  
  
##  <a name="BKMK_7"></a> 공유 디지털 미디어 보기 및 찾아보기  
 대시보드, 실행 패드, 원격 웹 액세스 웹 사이트 또는 Windows Phone용 내 서버 앱을 사용하여 리소스를 보거나 찾아볼 수 있습니다.  
  
#### <a name="to-view-and-browse-shared-media-from-the-dashboard"></a>대시보드에서 공유 미디어를 보고 찾아보려면  
  
1.  서버 대시보드를 엽니다.  
  
2.  기본 탐색 모음에서 **저장소**를 클릭합니다.  
  
3.  **서버 폴더** 탭을 클릭합니다. 서버 폴더 목록이 표시됩니다.  
  
4.  폴더를 두 번 클릭하여 폴더 콘텐츠를 확인합니다.  
  
#### <a name="to-view-and-browse-shared-media-using-the-launchpad-from-a-network-computer"></a>네트워크 컴퓨터에서 실행 패드를 사용하여 공유 미디어를 보고 찾아보려면  
  
1.  실행 패드에 로그인합니다.  
  
2.  **공유 폴더**를 클릭합니다. Windows 탐색기가 열리고 서버에 있는 공유 폴더 목록이 표시됩니다.  
  
3.  폴더를 두 번 클릭하여 폴더 콘텐츠를 확인합니다.  
  
#### <a name="to-view-and-browse-shared-media-using-remote-web-access"></a>원격 웹 액세스를 사용하여 공유 미디어를 보고 찾아보려면  
  
1.  원격 웹 액세스에 로그온합니다.  
  
2.  **공유 폴더**를 클릭합니다. 웹 페이지의 **공유 폴더** 섹션에는 서버에 있는 공유 폴더 목록이 표시됩니다.  
  
3.  폴더를 두 번 클릭하여 폴더 콘텐츠를 확인합니다.  
  
## <a name="see-also"></a>참조  
  
-   [디지털 미디어 관리](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md)  
  

-   [연결](Get-Connected-in-Windows-Server-Essentials.md)  
  
-   [공유 폴더 사용](Use-Shared-Folders-in-Windows-Server-Essentials.md)  
  
-   [원격 작업](Work-Remotely-in-Windows-Server-Essentials.md)

-   [연결](../use/Get-Connected-in-Windows-Server-Essentials.md)  
  
-   [공유 폴더 사용](../use/Use-Shared-Folders-in-Windows-Server-Essentials.md)  
  
-   [원격 작업](../use/Work-Remotely-in-Windows-Server-Essentials.md)

