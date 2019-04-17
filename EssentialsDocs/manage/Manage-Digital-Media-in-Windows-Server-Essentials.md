---
title: "Windows Server Essentials에서 디지털 미디어 관리"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 6906c1dafc6d4131e07c008b9db47ebebe9b7770
ms.sourcegitcommit: 5c8d8acc59d61756377c9c4e459a47a9ab555b39
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="manage-digital-media-in-windows-server-essentials"></a>Windows Server Essentials에서 디지털 미디어 관리

>적용 대상: Windows Server 2012 R2 Essentials, Windows Server 2012 필수 패키지

다음 항목 스트리밍 서버 기능 미디어에 토론 하 고 설정 하 고 네트워크에 스트리밍 미디어를 사용 하는 방법을 설명 합니다.  
  
> [!NOTE]
>  기본적으로 스트리밍 미디어 기능 사용할 수 없는 경우 Windows Server Essentials 및 Windows Server 2012 r 2와 Windows Server Essentials 경험 역할이 설치 다음 버전에서는 기능 스트리밍 미디어를 추가 하려면 [Windows Server Essentials 미디어 팩 다운로드 및 설치](https://www.microsoft.com/download/details.aspx?id=40837) Microsoft 다운로드 센터에서 합니다.  
  
-   [디지털 미디어 개요](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [대시보드를 사용 하 여 미디어 서버 관리](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [스트리밍 미디어를 작동 방식](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [켜기 또는 끄기 스트리밍 미디어](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [디지털 미디어 파일 서버에 추가](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [허용 하거나 서버에서 미디어 라이브러리에 대 한 액세스를 제한](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [미디어 라이브러리 이름 바꾸기](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_8)  
  
-   [디지털 미디어 공유를 중지합니다](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_9)  
  
-   [블록 SMB (서버 메시지) 프로토콜을 사용 하 여 액세스 공유 파일 서버에 미디어 장치 사용](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_10)  
  
-   [일반적인 프로세서 및 지 원하는 비디오 프로필](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_CommonProcessors)  
  
-   [미디어 파일 형식에는 알려진된 문제가](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_KnownIssues)  
  
##  <a name="BKMK_1"></a>디지털 미디어 개요  
 디지털 미디어 오디오, 비디오 및 사진 콘텐츠 인코딩된 (압축 디지털)를 가리킵니다. 인코딩 콘텐츠는 Windows Media 파일 등을 디지털 미디어 파일에 대 한 오디오 및 비디오 입력 변환 포함 됩니다. 디지털 미디어 인코드됩니다 후 것 수 수 조작할 배포 쉽고 컴퓨터에서 재생 하 고 쉽게 컴퓨터가 네트워크를 통해 전송 될 때 합니다.  
  
 디지털 미디어 유형의 예로: 오디오 WMA (Windows Media), Windows Media 비디오 (WMV), MP3, JPEG, 및 AVI 합니다. Windows Media Player에서 지원 되는 디지털 미디어 형식에 대 한 내용은 [파일 형식에 의해 지원 Windows Media Player](https://support.microsoft.com/kb/316992).  
  
### <a name="why-would-i-want-to-stream-my-digital-media"></a>디지털 미디어 스트리밍하려면 표시 하는 이유  
 많은 사람들이 Windows Server Essentials의 공유 폴더에서 음악, 동영상 및 사진을 저장합니다. 다음을 수행할 수 있습니다.  
  
-   **동영상을 시청**합니다. 서버에 저장 하 고 스트림 대용량 동영상 컬렉션을 사용할 수 하 고 녹화 된 TV 프로그램 컴퓨터나 기타 재생에 디바이스 네트워크에서 합니다. Windows Media Player를 사용 하 여 Xbox 360 또는 컴퓨터 비디오를 스트리밍할 수 있습니다.  
  
-   **음악을 재생**합니다. 미디어 공유에 대 한 켜기는 **음악** 공유 폴더를 지 원하는 Windows Media 연결 하는 장치에서 음악에 액세스할 수 있습니다. 사용 하거나, 모든 사용자 계정에서 스트림할 구성 필요가 없습니다는 **음악** 공유 폴더 공유 켜진 후 합니다.  
  
-   **사진 슬라이드 쇼를 표시**합니다. 디지털 사진에 저장할 수는 **사진** 서버 폴더를 공유 하 고 다음 집 이나 사무실에서 TV에 연결 하는 Xbox 360 또는 된 컴퓨터에서 액세스 합니다. 많은 사진 액자에 TV를 설정 하는 비슷합니다 사진 슬라이드 쇼를 볼 수 있습니다.  
  
###  <a name="BKMK_1.5"></a>복사 암호로 보호 된 미디어 공유  
  Windows Server Essentials 복사 암호로 보호 된 미디어를 공유 하는 것을 지원 하지 않습니다. 온라인 음악 스토어를 통해 구입한 음악을 포함 됩니다.  
  
 컴퓨터 또는 것을 구매 하는 데 사용 하는 디바이스에만 다시 Copy-protected 미디어를 재생할 수 있습니다. 복사 방지 미디어 서버에 복사한 여기에서 재생 하는 경우에 컴퓨터 또는 디바이스에 둘 이상의 미디어 재생 수 없습니다. 그러나 복사 암호로 보호 된 미디어 Windows Server Essentials에 저장할 수 있으며 컴퓨터 또는 것을 구매 하는 데 사용 하는 장치에 미디어 재생을 계속 합니다.  
  
##  <a name="BKMK_2"></a>대시보드를 사용 하 여 미디어 서버 관리  
  Windows Server Essentials을 사용 하면 Windows Server Essentials 대시보드 사용 하 여 일반적인 관리 작업을 수행할 수 있습니다. **미디어** 서버 탭 **설정** 대시보드의 페이지에서 다음을 제공 합니다.  
  
|섹션|기능|  
|-------------|-------------------|  
|미디어 서버|**켜기 / 끄기** 단추 켜거나 스트리밍 미디어를 끌 수 있습니다.|  
|스트리밍 동영상 품질|드롭다운 화살표를 사용 하면 비디오 품질 서버에서 재생 되는 비디오 스트리밍 선택할 수 있습니다.|  
|미디어 라이브러리|미디어 라이브러리의 이름을 표시합니다. 기본 이름 라이브러리의 라고 **디지털 미디어 라이브러리**, 스트리밍 미디어를 켤 때 생성 되는 합니다. 미디어 라이브러리 이름을 변경 하려면 [미디어 라이브러리의 이름을 바꿉니다](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_8)합니다. 클릭 하면 **지정** 미디어 라이브러리를 공유 하는 폴더를 사용자 지정할 수 있습니다.|  
  
 자세한 내용은 참조 [허용 서버에서 미디어 라이브러리에 대 한 액세스를 제한 하거나](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6) 및 [복사 암호로 보호 된 미디어 공유](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1.5)합니다.  
  
##  <a name="BKMK_3"></a>스트리밍 미디어를 작동 방식  
 Windows Server Essentials의 기능 스트리밍 미디어는 것이 네트워크에 연결 된 컴퓨터에 대 한 가능 및 네트워크에 연결 된 디지털 미디어 장치도 서버에 저장 된 디지털 미디어 파일을 재생 합니다.  
  
 미디어 서버를 켜면 미디어 라이브러리를 공유 하는 콘텐츠 서버에서 스트리밍 미디어를 받을 수 있는 네트워크의 디바이스에서 플레이 대 한 제공 됩니다. 대부분 디지털 미디어 파일의 종류를 스트리밍할 수 있습니다. 가장 일반적인 유형의 스트리밍할 수 있는 파일 중 일부는 다음과 같습니다.  
  
-   Windows Media 형식 (.asf,.wma,.wmv,.wm)  
  
-   오디오 Visual 인터리브 (.avi)  
  
-   움직이는 사진을 전문가 그룹 (.mpeg,.mpg,.mp3)  
  
-   Windows (.wav)에 대 한 오디오  
  
-   CD 오디오 트랙 (.cda)  
  
 파일을 재생, 간단 하 게 음악을 찾는, 비디오 또는 사진 공유 폴더를 두 번 클릭 파일을를 콘텐츠를 컴퓨터에 서버에서 스트림 되며 재생 합니다. 찾기 및 서버에 저장 된 디지털 미디어 파일을 재생 하는 방법에 대 한 정보를 참조 하세요. [디지털 미디어 재생](../use/Play-Digital-Media-in-Windows-Server-Essentials.md)합니다.  
  
 미디어로 스트리밍할 하려면 다음 하드웨어가 필요 합니다.  
  
-   유선 또는 무선 사설망  
  
-   네트워크 또는 디지털 미디어 수신기 (네트워크에 연결 된 디지털 미디어 플레이어 라고도 함) 라고 하는 디바이스의 다른 컴퓨터 합니다. 디지털 미디어 수신기 컴퓨터를 사용 하 여 제어할 수 있는 유선 또는 무선 네트워크에 연결 된 하드웨어 디바이스는? 다른 방으로에서 컴퓨터 이름과 컴퓨터가 있는 경우에 있습니다.  
  
 자세한 내용은 참조 [켜기 또는 끄기 스트리밍 미디어](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)합니다.  
  
##  <a name="BKMK_4"></a>켜기 또는 끄기 스트리밍 미디어  
 컴퓨터, 휴대폰, 텔레비전, 디지털 미디어 수신기, Windows Media Center (Xbox 360 포함) 및 기타 개인 전자 장치에 대 한 extender 음악, 동영상 및 Windows Server Essentials의 사진을 스트리밍을 파일 모든 지원 되는 디지털 미디어 receiver (DMR)을 통해 공유할 수 있습니다.  
  
 Windows Server Essentials와 호환 되는 디지털 미디어 디바이스의 최신 목록에 대 한 참조는 [Windows 호환성 센터](https://www.microsoft.com/windows/compatibility/CompatCenter/Home)합니다.  
  
### <a name="enabling-media-sharing"></a>공유 미디어 사용  
 Windows Server Essentials에 저장 된 미디어를 공유 하려면 스트리밍 미디어를 켭니다. 스트리밍 미디어 꺼져 기본적으로 있습니다.  
  
####  <a name="BKMK_2.5"></a>미디어 스트리밍 켜거나 끄려면  
  
1.  Windows Server Essentials 대시보드를 엽니다.  
  
2.  클릭 **설정**, 클릭 **미디어**, 하 고 다음 중 하나를 수행 합니다.  
  
    -   클릭 **켜기** 공유 미디어 라이브러리 서버에 저장 된 파일을 모두 시작 합니다.  
  
    -   클릭 **끄기** 미디어 라이브러리 서버에 저장 된 파일을 모두 공유를 중지 합니다.  
  
3.  미디어 라이브러리에 추가 된 폴더를 공유 하려면 클릭 **사용자 지정**를 선택한 다음 **예** 미디어 라이브러리에 포함 하지 않을 각 공유 폴더 합니다.  
  
4.  클릭 **확인** 변경 내용을 저장 합니다.  
  
 Windows Media Player에서 지원 되는 디지털 미디어 형식에 대 한 정보를 참조 하세요. [파일 형식 Windows Media Player에서 지원](https://support.microsoft.com/kb/316992)합니다.  
  
 자세한 내용은 참조 [허용 서버에서 미디어 라이브러리에 대 한 액세스를 제한 하거나](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)합니다.  
  
##  <a name="BKMK_5"></a>디지털 미디어 파일 서버에 추가  
 서버 관리자는 직접 서버에 액세스 하거나 대시보드에 로그인 할 원격 Web Access 사이트를 사용 하 여 디지털 미디어 미디어 라이브러리의 공유 폴더를 추가할 수 있습니다. 다른 사용자가 사용 하 여 서버에 미디어 파일을 추가할 수 있는 **공유 폴더** 또는 Windows Phone에 대 한 서버에 사용할 앱을 사용 하 여 원격 Web Access 사이트를 사용 하 여 실행 패드에 연결 합니다. 미디어 재생에 대 한 정보를 참조 하세요. [디지털 미디어 재생](../use/Play-Digital-Media-in-Windows-Server-Essentials.md)합니다.  
  
> [!NOTE]
>  또한 Windows Phone에 대 한 서버에 사용할 앱을 사용 하 여 미디어 파일 서버에 업로드할 수 있습니다. 내 서버에서 앱을 다운로드할 수 있는 [Windows Phone 스토어](http://www.windowsphone.com/store/app/my-server/6c2f98d5-6fcf-4e1d-b8b1-cde62ea1a94a)합니다. Windows phone의 내 서버 앱에 대 한 자세한 내용은 블로그 게시물을 참조 [Windows Server essentials 휴대폰 앱 내 서버](http://blogs.technet.com/b/sbs/archive/2012/09/18/my-server-phone-app-for-windows-server-2012-essentials.aspx)합니다.  
  
#### <a name="to-add-digital-media-files-to-shared-folders-on-the-server"></a>디지털 미디어 파일 서버에 공유 폴더를 추가 하려면  
  
1.  다음 방법 중 하나를 사용 하 여 서버에에 로그인 합니다.  
  
    1.  웹에 대 한 원격 액세스에 로그인에 대 한 정보를 참조 하세요. [로그온 원격 Web Access](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1)합니다.  
  
    2.  로그인 실행 패드에 대 한 내용은 [실행 패드 개요](Overview-of-the-Launchpad-in-Windows-Server-Essentials.md)합니다.  
  
2.  검색 하 고 추가할 미디어에 대 한 폴더를 클릭 합니다.  
  
3.  복사 및 붙여넣기를 또는 끌어서 놓기 원하는 미디어 파일 서버에 적절 한 공유 폴더에 추가 합니다.  
  
##  <a name="BKMK_6"></a>허용 하거나 서버에서 미디어 라이브러리에 대 한 액세스를 제한  
  
-   네 미리 정의 된 폴더를 만듭니다 미디어 공유 켜면: 음악, 사진, 동영상 및 녹화 된 TV 합니다. 서버에서 preexists 이러한 폴더 중 하나 기존 폴더 공유 폴더를 공유 미디어로 다시 사용 됩니다. 모든 기존 폴더의 미디어 콘텐츠 및 사용자 권한을 그대로 유지 하 고 네트워크의 모든 사용자와 공유 됩니다.  
  
-   미디어 라이브러리 공유 공유 폴더를 설정 하기 전에 모든 종류의 공유 폴더를 설정 하는 사용자 계정 액세스를 무시 미디어 라이브러리 공유를 알고 있어야 합니다. 예를 들어 미디어 라이브러리 공유를 켜면는 **사진** 폴더를 공유 하 고 설정 하 고 **사진** 공유 폴더를 **액세스** 사용자 계정 이름을 Bobby 합니다. Bobby에서 디지털 미디어 스트리밍할 여전히 수는 **동영상** 공유 폴더를 지원 되는 디지털 미디어 플레이어 또는 DMR 합니다. 이러한 방식으로 스트리밍할 하지 않으려는 경우 디지털 미디어를 사용 하는 경우 켜져 미디어 라이브러리 공유 하지 않은 폴더에 파일을 저장 합니다.  
  
-   미디어 라이브러리 공유 공유 폴더를 설정 하는 경우 모든 지원 되는 디지털 미디어 플레이어 또는 Windows Server Essentials 네트워크에 액세스할 수 있는 DMR 공유 폴더에서 디지털 미디어도 액세스할 수 있습니다. 예를 들어, 무선 네트워크가 보안 되지 않은 경우 해당 폴더에 디지털 미디어 잠재적으로 액세스할 수 무선 네트워크가 범위 내에 있는 합니다. 미디어 라이브러리 공유 켜기 전에 무선 네트워크 보안을 유지 있는지 확인 합니다. 자세한 내용은 무선 액세스 포인트에 대 한 설명서를 참조 하세요.  
  
##  <a name="BKMK_8"></a>미디어 라이브러리 이름 바꾸기  
 미디어 라이브러리의 기본 이름은 **디지털 미디어 서버**합니다. Windows Server Essentials의 스트리밍 미디어를 켤 때 생성 됩니다. 스트리밍 미디어에 대 한 자세한 내용은 참조 [켜기 또는 끄기 스트리밍 미디어에](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.5)합니다. 대시보드 서버를 사용 하 여 언제 든 지 미디어 라이브러리 이름을 수정할 수 있습니다.  
  
#### <a name="to-rename-the-media-library"></a>미디어 라이브러리의 이름을 바꾸려면  
  
1.  대시보드 서버를 엽니다. 클릭 대시보드는 실행 패드에서를 열려면 **대시보드**서버 암호를 입력 하 고 로그인에 있는 화살표를 클릭 합니다.  
  
2.  대시보드 서버에서 **설정**합니다.  
  
3.  에 **설정** 페이지, 클릭는 **미디어** 탭 합니다.  
  
4.  에 **미디어 라이브러리** 의 섹션은 **미디어 설정** 페이지, 미디어 라이브러리의 이름을 클릭 합니다.  
  
5.  에 **미디어 라이브러리 이름 변경** 대화 상자에서 미디어 라이브러리의 새 이름을 입력 한 다음 **확인**합니다.  
  
##  <a name="BKMK_9"></a>디지털 미디어 공유를 중지합니다  
 서버 관리자 Windows Server Essentials 실행 하는 서버의 공유 폴더에 저장 된 디지털 미디어 공유를 중지할 수 있습니다.  
  
#### <a name="to-stop-sharing-media-in-shared-folders"></a>미디어 공유 폴더의 공유를 중지 하려면  
  
1.  대시보드 서버를 엽니다.  
  
2.  대시보드에서 **Home** 페이지, 클릭 **설치**, 클릭 **미디어 서버 설정**을 차례로 클릭 하 고 **미디어 Server를 설정 하려면 클릭 하세요**합니다.  
  
3.  에 **미디어** 설정 페이지를 선택할 수 있습니다 다음 옵션 중 하나 다음과 같습니다.  
  
    -   클릭 **끄기** 서버에 저장 된 파일을 모두 공유를 중지 합니다.  
  
    -   클릭 **사용자 지정**를 선택한 다음 **아니요** 특정 폴더 공유를 중지 하려는 합니다.  
  
4.  클릭 **적용** 또는 **확인** 변경 내용을 저장 합니다.  
  
##  <a name="BKMK_10"></a>블록 SMB (서버 메시지) 프로토콜을 사용 하 여 액세스 공유 파일 서버에 미디어 장치 사용  
 블록 SMB (서버 메시지) 네트워크 파일 및 공유 하는 대신 DLNA (에 대 한 액세스 스트리밍 미디어)를 사용 하는 장치 Guest 계정을 정품 인증 해야 합니다. 이렇게 하면 디바이스 또는 사용자에 네트워크의 공유 폴더 인증 없이 내용을 볼 수 있습니다.  
  
> [!CAUTION]
>  Guest 계정을 사용 하도록 설정 하면 기본적으로 서버에서 공유 리소스에 액세스할 수 누구나 합니다.  
  
##  <a name="BKMK_CommonProcessors"></a>일반적인 프로세서 및 지 원하는 비디오 프로필  
 Windows Server Essentials 서버에서 미디어 스트리밍하려면 다른 네트워크에 연결 된 장치 (예: 디지털 미디어 플레이어) 또는 Media Center extender (예: Xbox 360)는 Windows 7 또는 Windows 8 운영 체제를 실행 하는 컴퓨터에 사용할 수 있습니다. 네트워크를 사용 하지 않은 서버에 저장 된 파일을 재생할 원격 웹 Access 미디어 플레이어를 사용 합니다.  
  
 카멜레온 200 높일 사이의 m b 10 p s 데이터 전송 속도 필요합니다. 컴퓨터 및 디바이스를 인식 하 고 플레이할 수 있는 서식이 미디어를 사용 해야 합니다. 지원 되지 않는 같은 미디어 형식 하므로 컴퓨터 및 디바이스에 대 한 있는 미디어 파일을 재생 하는 방법이 있어야 합니다.  
  
  Windows Server Essentials 코드 변환 지원 컴퓨터나 디바이스의 기능을 결정 하 고 다음 동적으로 변환 지원 되지 않는 비디오 파일 지원 되는 것에 포함 되어 있습니다. 일반적으로 Windows Media Player 12는 Windows 7 또는 Windows 8을 실행 하는 컴퓨터에서 콘텐츠를 재생할 수, 네트워크에 연결 된 장치에서 콘텐츠 서버에서 재생 됩니다.  
  
 코드 변환을 위해 형식 및 비트 전송률 매우 서버 프로세서 성능에 따라 달라 집니다. Windows 체험 지의 일환으로 프로세서 성능 식별 됩니다. 성능 점수 서버를 확인 하려면 다음 중 하나를 수행 합니다.  
  
-   로 이동 하는 네트워크를 실행 컴퓨터에서 Windows 7 또는 Windows 8 서버와 같은 프로세서가 **제어판**, 클릭 **성능 정보 및 도구**, 다음에 정보를 검토 하 고 있는 **속도의 컴퓨터 성능을 향상 하 고** 페이지 합니다.  
  
-   프로세서가 제조업체에 문의 합니다.  
  
 최상의 사용자 환경에 대 한 서버 프로세서를 사용자에 게 적합 한 해상도 품질 스트리밍 동영상을 선택 합니다. 서버 비트 전송률 이러한 설정 중 하나에 자동으로 조정 됩니다.  
  
-   **낮은** 프로세서 점수는 3.6 보다 작은 경우 합니다.  
  
-   **보통** 프로세서 점수 3.6 하 고 보다 작은 4.2 이상인 경우 합니다.  
  
-   **높은** 프로세서 점수 4.2 및 미만 6.0 이상인 경우 합니다.  
  
-   **최상의** 프로세서 점수 6.0 이상인 경우 합니다.  
  
 서버에 하는 것 보다 더 많은 처리 능력을 필요로 하는 해상도 스트리밍 동영상을 선택 하면 버퍼가 및 서버에서 미디어 스트리밍 도중 경유지 발생할 수 있습니다.  
  
> [!NOTE]
>  Hd 스트리밍하려면 원격 웹 액세스를 통해 영상 통화 해야와 점수는 6.0 이상 프로세서.  
  
##  <a name="BKMK_KnownIssues"></a>미디어 파일 형식에는 알려진된 문제가  
 원격 Web access에서 스트리밍 미디어 기능은 Windows Media Player 12 네트워크 공유 서비스를 사용 합니다. 원격 Web Access 미디어 스트리밍 오디오, 비디오 및 사진 파일 형식 Windows Media Player 12 및 Silverlight 4에서 지원 되는 지원 합니다.  
  
 다음 표에서 파일 형식이 나와 스트리밍 웹에 대 한 원격 액세스 미디어에서 지원 되는 합니다. 있는 경우 미디어 파일 테이블에 포함 되어 있지 않은 서버의 형식, 스트리밍 웹에 대 한 원격 액세스 미디어를 통해 스트리밍할 수 없습니다.  
  
|파일 형식|파일 이름 확장명|  
|---------------|-------------------------|  
|3GPP 파일|.3gp,.3gpp,.3g2,.3gp2|  
|오디오 데이터 전송 ADTS (Stream) 오디오 파일|.adts,.adt|  
|AU 오디오 파일|.au,.snd|  
|오디오 파일 형식 AIFF (Interchange) 오디오 파일|.aif,.aifc,.aiff|  
|AVCHD 파일|.m2ts,.m2t,.mts|  
|CD 오디오 디스크|.cda|  
|DVD-비디오 디스크|.vob|  
|JPEG 그림 파일|.jpg|  
|MP3 오디오 파일|.mp3,.m3u|  
|MPEG 비디오 파일|.mpeg,.mpg,.m1v,.mpa,.mpe,.mp4,.mp4v,.m4v,.m4a, 및.mov|  
|Windows 오디오 및 비디오 파일|.avi,.wav|  
|Windows Media 오디오 및 비디오 파일|.asf,.asx,.wax,.wm,.wma,.wmd,.wmp,.wmv,.wmx,.wpl, 및.wvx|  
  
> [!NOTE]
>  이 표에 나열 되는 파일 형식을 사용할 수 없는 경우 파일이 Windows Media Player에서 지원 되지 않는 코덱을 사용 하 여 인코딩된도 수 있습니다.  
  
 지원 되는 파일 형식에 대 한 자세한 내용은 참조 [파일 형식 Windows Media Player에서 지원](https://go.microsoft.com/fwlink/p/?LinkID=196118) 및 [미디어 형식을, 프로토콜 및 로그 필드 지원](https://go.microsoft.com/fwlink/p/?LinkId=203339) silverlight 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [디지털 미디어 재생](../use/Play-Digital-Media-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)
