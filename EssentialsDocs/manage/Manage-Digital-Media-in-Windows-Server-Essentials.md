---
title: Windows Server Essentials에서 디지털 미디어 관리
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9378bffa-487c-43ca-9ec3-7e7864d2dd9a
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 87ec5218455672cbfd2bc1d77244fd263b91362c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433306"
---
# <a name="manage-digital-media-in-windows-server-essentials"></a>Windows Server Essentials에서 디지털 미디어 관리

>적용 대상: Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

다음 항목에서는 서버의 미디어 스트리밍 기능에 대해 설명하고 네트워크에서 미디어 스트리밍을 설정 및 사용하는 방법을 설명합니다.  
  
> [!NOTE]
>  기본적으로 미디어 스트리밍 기능을 사용할 수 없는 경우 Windows Server Essentials 및 Windows Server 2012 R2에서 Windows Server Essentials Experience 역할이 설치 된 이러한 버전에 미디어 스트리밍 기능을 추가하려면 Microsoft 다운로드 센터에서 [Windows Server Essentials 미디어 팩을 다운로드 및 설치](https://www.microsoft.com/download/details.aspx?id=40837) 합니다.  
  
-   [디지털 미디어 개요](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [대시보드를 사용 하 여 미디어 서버 관리](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [미디어 스트리밍의 작동 방식](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [미디어 스트리밍을 켜거나 끌](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [서버에 디지털 미디어 파일 추가](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [서버의 미디어 라이브러리에 대 한 액세스를 제한 또는 허용](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [미디어 라이브러리 이름 바꾸기](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_8)  
  
-   [디지털 미디어 공유 중지](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_9)  
  
-   [서버 메시지 블록 (SMB) 프로토콜을 사용 하 여 서버의 공유 파일에 액세스 하는 미디어 장치 사용](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_10)  
  
-   [일반 프로세서 및 지원 되는 비디오 프로필](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_CommonProcessors)  
  
-   [미디어 파일 형식 사용 하 여 알려진된 문제](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_KnownIssues)  
  
##  <a name="BKMK_1"></a> 디지털 미디어 개요  
 디지털 미디어는 인코딩된(디지털 방식으로 압축된) 오디오, 비디오 및 사진 콘텐츠를 나타냅니다. 콘텐츠 인코딩을 통해 Windows Media 파일과 같은 오디오 및 비디오 입력을 디지털 미디어 파일로 변환합니다. 디지털 미디어는 인코딩되고 나면 컴퓨터에서 손쉽게 조작, 배포 및 재생할 수 있고 컴퓨터 네트워크를 통해 손쉽게 전송됩니다.  
  
 디지털 미디어 유형의 예는 다음과 같습니다. WMA(Windows Media 오디오), WMV(Windows Media 비디오), MP3, JPEG, AVI. Windows Media Player에서 지원되는 디지털 미디어 유형에 대한 자세한 내용은 [Windows Media Player에서 지원되는 파일 형식](https://support.microsoft.com/kb/316992)을 참조하세요.  
  
### <a name="why-would-i-want-to-stream-my-digital-media"></a>디지털 미디어를 스트리밍하려는 이유  
 많은 사람들이 Windows Server Essentials의 공유 폴더에 음악, 비디오 및 사진을 저장합니다. 다음과 같은 작업을 수행할 수 있습니다.  
  
-   **비디오 보기**. 서버를 사용하여 비디오 및 녹화된 TV 프로그램의 광범위한 모음을 네트워크의 컴퓨터 및 기타 재생 장치에 저장하고 스트리밍할 수 있습니다. Windows Media Player를 사용하여 Xbox 360 또는 컴퓨터에 비디오를 스트리밍할 수 있습니다.  
  
-   **음악 재생**. **음악** 공유 폴더에 대한 미디어 공유를 켜면 Windows Media Connect를 지원하는 장치에서 음악에 액세스할 수 있습니다. 공유 기능을 켜고 나면 사용자 계정을 사용하도록 설정하고 **음악** 공유 폴더에서 스트리밍하도록 구성할 필요가 없습니다.  
  
-   **사진 슬라이드 쇼 제공**. 서버의 **사진** 공유 폴더에 디지털 사진을 저장하고 집이나 사무실에 있는 TV에 연결된 Xbox 360 또는 컴퓨터에서 디지털 사진에 액세스할 수 있습니다. TV를 대형 사진 프레임으로 전환하는 것처럼 사진 슬라이드 쇼를 볼 수 있습니다.  
  
###  <a name="BKMK_1.5"></a> 복사 방지 된 미디어 공유  
  Windows Server Essentials 복사 방지 된 미디어를 공유 하는 것을 지원 하지 않습니다. 여기에는 온라인 음악 스토어를 통해 구매한 음악이 포함됩니다.  
  
 복사 방지된 미디어는 미디어를 구매할 때 사용한 컴퓨터나 장치에서만 재생할 수 있습니다. 복사 방지를 사용하면 미디어를 서버로 복사하고 서버에서 재생하더라도 두 대 이상의 컴퓨터 또는 장치에서 미디어를 재생할 수 없습니다. 그러나 Windows Server Essentials에 복사 방지 된 미디어를 저장할 수 있으며 컴퓨터 또는 장치 구매 하는 데에 미디어 재생을 계속 합니다.  
  
##  <a name="BKMK_2"></a> 대시보드를 사용 하 여 미디어 서버 관리  
  Windows Server Essentials를 Windows Server Essentials 대시보드를 사용 하 여 일반적인 관리 작업을 수행할 수 있습니다. 대시보드 서버 **설정** 페이지의 **미디어** 탭에서는 다음을 제공합니다.  
  
|섹션|기능|  
|-------------|-------------------|  
|미디어 서버|**켜기/끄기** 단추를 사용하여 미디어 스트리밍을 켜거나 끌 수 있습니다.|  
|비디오 스트리밍 품질|드롭다운 화살표를 사용하여 서버에서 재생되는 비디오의 비디오 스트리밍 품질을 선택할 수 있습니다.|  
|미디어 라이브러리|미디어 라이브러리의 이름을 표시합니다. 라이브러리의 기본 이름은 **디지털 미디어 라이브러리**이며, 미디어 스트리밍을 켤 때 생성됩니다. 미디어 라이브러리 이름을 변경하려면 [미디어 라이브러리 이름 바꾸기](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_8)를 참조하세요. **사용자 지정**을 클릭하여 미디어 라이브러리로 공유되는 폴더를 사용자 지정할 수 있습니다.|  
  
 자세한 내용은 [Allow or restrict access to a media library on the server](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6) 및 [Sharing copy-protected media](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1.5)을 참조하세요.  
  
##  <a name="BKMK_3"></a> 미디어 스트리밍의 작동 방식  
 미디어 스트리밍 기능 Windows Server Essentials에서 네트워크에 연결 된 컴퓨터에 대 한 가능한와 일부 네트워크로 연결 된 디지털 미디어 장치 서버에 저장 된 디지털 미디어 파일을 재생할 수 있습니다.  
  
 미디어 서버를 켜면 미디어 라이브러리에서 공유하는 콘텐츠를 서버에서 스트리밍 미디어를 수신할 수 있는 네트워크의 장치에서 재생할 수 있습니다. 대부분 디지털 미디어 파일 형식을 스트리밍할 수 있습니다. 스트리밍할 수 있는 더욱 일반적인 일부 파일 형식은 다음과 같습니다.  
  
- Windows Media 형식(.asf, .wma, .wmv, .wm)  
  
- Audio Visual Interleave(.avi)  
  
- Moving Pictures Experts Group(.mpeg, .mpg, .mp3)  
  
- Windows용 오디오(.wav)  
  
- CD 오디오 트랙(.cda)  
  
  파일을 재생하려면 공유 폴더에서 노래, 동영상 또는 사진을 찾고 파일을 두 번 클릭하면 콘텐츠가 서버에서 컴퓨터로 스트리밍되고 재생됩니다. 찾기 및 서버에 저장 된 디지털 미디어 파일을 재생 하는 방법에 대 한 정보를 참조 하세요 [Play Digital Media](../use/Play-Digital-Media-in-Windows-Server-Essentials.md)합니다.  
  
  미디어를 스트리밍하려면 다음 하드웨어가 필요합니다.  
  
- 유선 또는 무선 프라이빗 네트워크  
  
- 네트워크의 다른 컴퓨터 또는 디지털 미디어 수신기(네트워크 디지털 미디어 플레이어 라고도 함). 디지털 미디어 수신기는 컴퓨터를 사용 하 여 제어할 수 있는 유선 또는 무선 네트워크에 연결 하는 하드웨어 장치? 컴퓨터가 다른 방에 하는 경우에 합니다.  
  
  자세한 내용은 [미디어 스트리밍을 켜거나 끌](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)합니다.  
  
##  <a name="BKMK_4"></a> 미디어 스트리밍을 켜거나 끌  
 모든 지원 되는 디지털 미디어 수신기 (DMR) 컴퓨터, 휴대폰, 텔레비전, 디지털 미디어 수신기, extender (Xbox를 포함 하는 Windows Media Center 용 파일을 스트리밍하여 음악, 동영상 및 사진을 Windows Server Essentials를 공유할 수 있습니다. 360), 기타 개인용 전자 장치와 합니다.  
  
 Windows Server Essentials와 호환 되는 디지털 미디어 장치의 현재 목록에 대해서는 [Windows 호환성 센터](https://www.microsoft.com/windows/compatibility/CompatCenter/Home)합니다.  
  
### <a name="enabling-media-sharing"></a>미디어 공유 사용  
 Windows Server Essentials에 저장 된 미디어를 공유 하려면 미디어 스트리밍을 켜야 합니다. 기본적으로 미디어 스트리밍은 꺼져 있습니다.  
  
####  <a name="BKMK_2.5"></a> 미디어 스트리밍을 켜거나를 설정 하려면  
  
1. Windows Server Essentials 대시보드를 엽니다.  
  
2. **설정**, **미디어**를 차례로 클릭하고 다음의 하나를 수행합니다.  
  
   -   서버의 미디어 라이브러리에 저장된 모든 파일의 공유를 시작하려면 **켜기**를 클릭합니다.  
  
   -   서버의 미디어 라이브러리에 저장된 모든 파일의 공유를 중지하려면 **끄기**를 클릭합니다.  
  
3. 미디어 라이브러리의 폴더를 추가로 공유하려면 **사용자 지정**을 클릭하고 미디어 라이브러리에 포함할 각 공유 폴더에 대해 **예**를 선택합니다.  
  
4. **확인** 을 클릭하여 변경 내용을 저장합니다.  
  
   Windows Media Player에서 지원되는 디지털 미디어 유형에 대한 자세한 내용은 [Windows Media Player에서 지원되는 파일 형식](https://support.microsoft.com/kb/316992)을 참조하세요.  
  
   자세한 내용은 [서버의 미디어 라이브러리에 대한 액세스 허용 또는 제한](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)을 참조하세요.  
  
##  <a name="BKMK_5"></a> 서버에 디지털 미디어 파일 추가  
 서버 관리자 서버에 직접 액세스 하거나 대시보드에 로그인 하 여 원격 웹 액세스 사이트를 사용 하 여 미디어 라이브러리의 공유 폴더에 디지털 미디어를 추가할 수 있습니다. 다른 사용자를 사용 하 여 서버에 미디어 파일에 추가할 수는 **공유 폴더** 실행 패드, 원격 웹 액세스 사이트를 사용 하 여 또는 Windows Phone 용 My Server 앱을 사용 하 여에 연결 합니다. 미디어 재생에 대 한 내용은 [Play Digital Media](../use/Play-Digital-Media-in-Windows-Server-Essentials.md)합니다.  
  
> [!NOTE]
>  Windows Phone용 내 서버 앱을 사용하여 서버에 미디어 파일을 업로드할 수도 있습니다. [Windows Phone 스토어](http://www.windowsphone.com/store/app/my-server/6c2f98d5-6fcf-4e1d-b8b1-cde62ea1a94a)에서 My Server 앱을 다운로드할 수 있습니다. Windows phone 용 My Server 앱에 대 한 자세한 내용은 블로그 게시물을 참조 하세요 [Windows Server Essentials 용 My Server phone 앱](http://blogs.technet.com/b/sbs/archive/2012/09/18/my-server-phone-app-for-windows-server-2012-essentials.aspx)합니다.  
  
#### <a name="to-add-digital-media-files-to-shared-folders-on-the-server"></a>서버의 공유 폴더에 디지털 미디어 파일을 추가하려면  
  
1.  다음 방법의 하나를 사용하여 서버에 로그인합니다.  
  
    1.  원격 웹 액세스에 로그온하는 방법에 대한 자세한 내용은 [원격 웹 액세스에 로그온](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1)을 참조하세요.  
  
    2.  실행 패드에 로그인 하는 방법에 대 한 내용은 [실행 패드 개요](Overview-of-the-Launchpad-in-Windows-Server-Essentials.md)합니다.  
  
2.  추가할 미디어에 대한 폴더를 검색하고 클릭합니다.  
  
3.  서버의 해당 공유 폴더에 추가할 미디어 파일을 복사 후 붙여넣거나 끌어서 놓습니다.  
  
##  <a name="BKMK_6"></a> 서버의 미디어 라이브러리에 대 한 액세스를 제한 또는 허용  
  
-   미디어 공유를 켜면 4개의 미리 정의된 폴더인 음악, 사진, 동영상 및 녹화된 TV가 생성됩니다. 이러한 폴더가 서버에 이미 있으면 기존 폴더가 미디어 공유용 공유 폴더로 다시 사용됩니다. 모든 기존 폴더의 미디어 콘텐츠와 사용자 권한은 유지 되 고 모든 네트워크 사용자와 공유 합니다.  
  
-   공유 폴더에 대한 미디어 라이브러리 공유를 켜기 전에 미디어 라이브러리 공유에서는 공유 폴더에 대해 설정한 모든 사용자 계정 액세스 유형을 무시한다는 점을 알고 있어야 합니다. 예를 들어 **사진** 공유 폴더에 대한 미디어 라이브러리 공유를 켜고 Bobby라는 사용자 계정에 대해 **사진** 공유 폴더를 **권한 없음** 으로 설정한다고 가정합니다. Bobby는 **동영상** 공유 폴더에서 모든 지원되는 디지털 미디어 플레이어 또는 DMR로 디지털 미디어를 계속 스트리밍할 수 있습니다. 이런 방식으로 스트리밍하지 않으려는 디지털 미디어가 있으면 미디어 라이브러리 공유가 꺼져 있는 폴더에 파일을 저장합니다.  
  
-   공유 폴더에 대 한 미디어 라이브러리 공유에서 설정한 경우 모든 지원 되는 디지털 미디어 플레이어 또는 dmr로 Windows Server Essentials 네트워크에 액세스할 수 있는 디지털 미디어는 공유 폴더에도 액세스할 수 있습니다. 예를 들어 보유한 무선 네트워크에 보안을 적용하지 않으면 무선 네트워크 범위 안에 있는 누구나 해당 폴더의 디지털 미디어에 액세스할 수 있게 됩니다. 미디어 라이브러리 공유를 켜기 전에 무선 네트워크에 보안을 적용해야 합니다. 자세한 내용은 무선 액세스 지점에 대한 설명서를 참조하세요.  
  
##  <a name="BKMK_8"></a> 미디어 라이브러리 이름 바꾸기  
 미디어 라이브러리의 기본 이름은 **디지털 미디어 서버**입니다. Windows Server Essentials에서 미디어 스트리밍을 켤 때 생성 됩니다. 미디어 스트리밍을 켜는 방법에 대 한 자세한 내용은 참조 [여 미디어 스트리밍을 켜거나 끌](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.5)합니다. 서버 대시보드를 사용하여 언제든지 미디어 라이브러리 이름을 수정할 수 있습니다.  
  
#### <a name="to-rename-the-media-library"></a>미디어 라이브러리 이름을 바꾸려면  
  
1.  서버 대시보드를 엽니다. 실행 패드에서 대시보드를 열려면 **대시보드**를 클릭하고 서버 암호를 입력한 다음 화살표를 클릭하여 로그인합니다.  
  
2.  서버 대시보드에서 **설정**을 클릭합니다.  
  
3.  **설정** 페이지에서 **미디어** 탭을 클릭합니다.  
  
4.  **미디어 설정** 페이지의 **미디어 라이브러리** 섹션에서 미디어 라이브러리의 이름을 클릭합니다.  
  
5.  **미디어 라이브러리 이름 변경** 대화 상자에서 미디어 라이브러리에 대한 새 이름을 입력하고 **확인**을 클릭합니다.  
  
##  <a name="BKMK_9"></a> 디지털 미디어 공유 중지  
 서버 관리자 Windows Server Essentials를 실행 하는 서버의 공유 폴더에 저장 된 디지털 미디어 공유를 중지할 수 있습니다.  
  
#### <a name="to-stop-sharing-media-in-shared-folders"></a>공유 폴더에 있는 미디어의 공유를 중지하려면  
  
1.  서버 대시보드를 엽니다.  
  
2.  대시보드 **홈** 페이지에서 **설정**, **미디어 서버 설정**, **미디어 서버를 설정하려면 클릭**을 차례로 클릭합니다.  
  
3.  **미디어** 설정 페이지에서 다음 옵션의 하나를 선택할 수 있습니다.  
  
    -   서버에 저장된 모든 파일의 공유를 중지하려면 **끄기** 를 클릭합니다.  
  
    -   **사용자 지정**을 클릭하고 공유를 중지할 특정 폴더에 대해 **아니요** 를 선택합니다.  
  
4.  **적용** 또는 **확인** 을 클릭하여 변경 내용을 저장합니다.  
  
##  <a name="BKMK_10"></a> 서버 메시지 블록 (SMB) 프로토콜을 사용 하 여 서버의 공유 파일에 액세스 하는 미디어 장치 사용  
 네트워크 파일 및 공유 액세스에 대해 미디어 스트리밍용 DLNA가 아니라 SMB(Server Message Block)를 사용하는 장치에서는 게스트 계정을 활성화해야 합니다. 이렇게 하면 네트워크에 있는 모든 장치나 사용자가 인증 없이 공유 폴더의 콘텐츠를 볼 수 있습니다.  
  
> [!CAUTION]
>  게스트 계정을 사용하도록 설정하면 누구나 기본적으로 서버의 공유 리소스에 액세스할 수 있습니다.  
  
##  <a name="BKMK_CommonProcessors"></a> 일반 프로세서 및 지원 되는 비디오 프로필  
 Windows Server Essentials 서버에서 미디어를 스트리밍하려면 Windows 7 또는 Windows 8 운영 체제 또는 다른 네트워크 장치 (예: 디지털 미디어 플레이어) 또는 Media Center extender (예: Xbox 360) 실행 하는 컴퓨터를 사용할 수 있습니다. 네트워크에서 멀리 있을 경우 원격 웹 액세스 미디어 플레이어를 사용하여 서버에 저장된 파일을 재생합니다.  
  
 200KBps에서 10MBps 사이의 데이터 전송 속도가 필요합니다. 컴퓨터와 장치에서 인식하고 재생할 수 있는 미디어 형식을 사용해야 합니다. 모든 장치에서 같은 미디어 형식을 지원하는 것은 아니므로 컴퓨터와 장치에서 보유한 미디어 파일을 재생할 방법이 있어야 합니다.  
  
  Windows Server Essentials에 컴퓨터 또는 장치의 기능을 확인 한 다음 지원에 지원 되지 않는 비디오 파일을 동적으로 변환 하는 트랜스 코딩 지원이 포함 되어 있습니다. 일반적으로 Windows 7 또는 Windows 8을 실행 중인 컴퓨터에서 Windows Media Player 12로 콘텐츠를 재생할 수 있으면 서버의 콘텐츠가 네트워크로 연결된 장치에서 재생됩니다.  
  
 트랜스코딩을 위해 선택된 형식과 비트 전송률은 서버 프로세서 성능에 따라 달라집니다. 프로세서 성능은 Windows 체험 지수의 일부로 식별됩니다. 서버의 성능 점수를 확인하려면 다음의 하나를 수행합니다.  
  
- Windows 7 또는 Windows 8을 서버와 동일한 프로세서를 실행 하는 네트워크 컴퓨터를 이동 하는 **Control Panel**, 클릭 **성능 정보 및 도구**에서 정보를 검토 하 고는 **속도 및 컴퓨터의 성능을 향상** 페이지입니다.  
  
- 프로세서 제조업체에 문의하세요.  
  
  사용자 환경을 최적화하려면 서버 프로세서에 적합한 비디오 스트리밍 해상도 품질을 선택합니다. 비트 전송률이 다음 설정의 하나로 자동으로 조정됩니다.  
  
- **느림** 프로세서 점수가 3.6보다 작은 경우.  
  
- **보통** 프로세서 점수가 3.6보다 크고 4.2보다 작은 경우.  
  
- **빠름** 프로세서 점수가 4.2보다 크고 6.0보다 작은 경우.  
  
- **최상** 프로세서 점수가 6.0보다 큰 경우.  
  
  서버에서 제공하는 것보다 더 큰 처리 성능이 필요한 비디오 스트리밍 해상도를 선택하면 서버에서 미디어를 스트리밍하는 동안 버퍼링이 발생하고 재생이 중지될 수 있습니다.  
  
> [!NOTE]
>  원격 웹 액세스를 통해 고화질 동영상을 스트리밍하려면 점수가 6.0 이상인 프로세서가 필요합니다.  
  
##  <a name="BKMK_KnownIssues"></a> 미디어 파일 형식 사용 하 여 알려진된 문제  
 원격 웹 액세스의 미디어 스트리밍 기능은 Windows Media Player 12 네트워크 공유 서비스를 사용합니다. 원격 웹 액세스 미디어 스트리밍은 Windows Media Player 12 및 Silverlight 4에서 지원되는 오디오, 동영상 및 사진 파일을 지원합니다.  
  
 다음 표에는 원격 웹 액세스 미디어 스트리밍에서 지원되는 파일 형식이 나와 있습니다. 표에 포함되지 않은 미디어 파일 형식이 서버에 있으면 원격 웹 액세스 미디어 스트리밍을 통해 미디어 파일을 스트리밍할 수 없습니다.  
  
|파일 형식|파일 이름 확장명|  
|---------------|-------------------------|  
|3GPP 파일|.3gp, .3gpp, .3g2 및 .3gp2|  
|ADTS(Audio Data Transport Stream) 오디오 파일|.adts 및 .adt|  
|AU 오디오 파일|.au 및 .snd|  
|AIFF(Audio Interchange File Format) 오디오 파일|.aif, .aifc 및 .aiff|  
|AVCHD 파일|.m2ts, .m2t 및 .mts|  
|CD 오디오 디스크|.cda|  
|DVD 비디오 디스크|.vob|  
|JPEG 사진 파일|.jpg|  
|MP3 오디오 파일|.mp3 및 .m3u|  
|MPEG 비디오 파일|.mpeg, .mpg, .m1v, .mpa, .mpe, .mp4, .mp4v, .m4v, .m4a 및 .mov|  
|Windows 오디오 및 비디오 파일|.avi 및 .wav|  
|Windows Media 오디오 및 비디오 파일|.asf, .asx, .wax, .wm, .wma, .wmd, .wmp, .wmv, .wmx, .wpl 및 .wvx|  
  
> [!NOTE]
>  이 표에 나열된 파일 형식을 사용할 수 없다면 Windows Media Player에서 지원되지 않는 코덱으로 파일을 인코딩할 수도 있습니다.  
  
 지원되는 파일 형식에 대한 자세한 내용은 [Windows Media Player에서 지원되는 파일 형식](https://go.microsoft.com/fwlink/p/?LinkID=196118) 및 Silverlight에 대한 [지원되는 미디어 형식, 프로토콜 및 로그 필드](https://go.microsoft.com/fwlink/p/?LinkId=203339) 를 참조하세요.  
  
## <a name="see-also"></a>참조  
  
-   [디지털 미디어 재생](../use/Play-Digital-Media-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)
