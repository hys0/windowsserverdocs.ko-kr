---
title: Windows Server Essentials에서 원격 웹 액세스 사용
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47ea21a0-5e05-4b4b-8fa4-338c82601276
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f6a5d6fd42c5cd7e92821e1157748054c741ef04
ms.sourcegitcommit: 0e3c2473a54f915d35687d30d1b4b1ac2bae4068
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68914682"
---
# <a name="use-remote-web-access-in-windows-server-essentials"></a>Windows Server Essentials에서 원격 웹 액세스 사용

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
  
  원격 웹 액세스은 인터넷에 연결 된 곳에서 웹 브라우저를 통해 네트워크의 파일/폴더 및 컴퓨터에 액세스할 수 있도록 하는 Windows Server Essentials의 기능입니다. 
  
  원격 웹 액세스를 사용하면 자리를 비울 때 Windows Server Essentials 네트워크에 연결된 상태를 유지할 수 있습니다. 원격 웹 액세스에 로그온 할 때 Windows Server Essentials 네트워크의 컴퓨터에 연결 하 고, 대시보드를 열어 Windows Server Essentials 네트워크를 관리 하 고, 서버의 모든 공유 폴더와 미디어 파일에 액세스할 수 있습니다.  
  
 이 항목은 다음과 같은 섹션으로 구성됩니다.  
  

-   [원격 웹 액세스에 연결](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Connect)  
  
-   [파일 및 폴더 공유](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SharedFolders)  
  
-   [모바일 장치에서 연결](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ConnectMobile)  
  
##  <a name="BKMK_Connect"></a>원격 웹 액세스에 연결  
  
-   [원격 웹 액세스에 로그온](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [컴퓨터에 원격으로 액세스](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1.5)  

-   [원격 웹 액세스에 연결](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Connect)  
  
-   [파일 및 폴더 공유](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SharedFolders)  
  
-   [모바일 장치에서 연결](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ConnectMobile)  
  
##  <a name="BKMK_Connect"></a>원격 웹 액세스에 연결  
  
-   [원격 웹 액세스에 로그온](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [컴퓨터에 원격으로 액세스](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1.5)  

  
###  <a name="BKMK_1"></a>원격 웹 액세스에 로그온  
 로컬 또는 원격 컴퓨터에서 원격 웹 액세스에 로그온 할 때 Windows Server Essentials를 실행 하는 서버의 리소스와 네트워크의 컴퓨터에서 리소스에 액세스할 수 있습니다.  
  
##### <a name="to-log-on-to-remote-web-access-from-a-network-computer"></a>네트워크 컴퓨터에서 원격 웹 액세스에 로그온하려면  
  
1.  웹 브라우저를 열고 주소 표시줄에 **https://** _<\>서버 이름_ **/remote** 를 입력 한 다음 enter 키를 누릅니다.  
  
    > [!NOTE]
    >  S가 https에 포함 되어 있는지 확인 합니다.  
  
2.  원격 웹 액세스 로그온 페이지에서 텍스트 상자에 사용자 이름과 암호를 입력 한 다음 화살표를 클릭 합니다.  
  
##### <a name="to-log-on-to-remote-web-access-from-a-remote-computer"></a>원격 컴퓨터에서 원격 웹 액세스에 로그온하려면  
  
1.  웹 브라우저를 열고 주소 표시줄에 **https://** _<\>_ **/remote** 를 입력 한 다음 enter 키를 누릅니다.  
  
    > [!NOTE]
    >  도메인 이름 정보에 대해서는 네트워크 관리자에게 문의하세요. S가 https에 포함 되어 있는지 확인 합니다.  
  
2.  원격 웹 액세스 로그온 페이지에서 텍스트 상자에 사용자 이름과 암호를 입력 한 다음 화살표를 클릭 합니다.  
  
###  <a name="BKMK_1.5"></a>컴퓨터에 원격으로 액세스  
 사무실에 없을 때 웹 브라우저를 사용 하 여 원격 웹 액세스 사이트에 로그온 하 여 Windows Server Essentials 대시보드, 공유 폴더 및 네트워크의 컴퓨터에 원격으로 액세스할 수 있습니다.  
  
 대시보드에 연결하면 사무실에 있는 것처럼 Windows Server Essentials를 관리할 수 있습니다. 사용자 계정 추가, 공유 폴더 추가, 공유 폴더 액세스 설정과 같은 일반적인 관리 작업을 모두 수행할 수 있습니다. 네트워크의 컴퓨터에 연결하면 사무실에서 컴퓨터 앞에 있는 것처럼 데스크톱에 액세스할 수 있습니다.  
  
 **상태** 열에는 네트워크의 컴퓨터에 연결할 수 있는지가 표시되고 다음 값이 포함될 수 있습니다.  
  
-   **사용 가능**  
  
     컴퓨터가 켜져 있고 원격 연결에 사용할 수 있습니다. 이 상태가 표시되더라도 타사 방화벽이 연결을 차단하면 이 컴퓨터에 연결하지 못할 수 있습니다.  
  
-   **오프 라인 또는 절전 모드**  
  
     컴퓨터가 꺼져 있거나 절전 모드 또는 최대 절전 모드에 있습니다. 컴퓨터가 오프라인이거나 절전 모드이면 컴퓨터를 사용할 수 있을 때 알 수 있도록 상태가 실시간으로 업데이트됩니다.  
  
-   **지원 되지 않는 운영 체제**  
  
     컴퓨터의 운영 체제에서 원격 데스크톱을 지원하지 않습니다. 변경 사항이 있으면 서버에서 이 상태가 업데이트되는 데 최대 6시간이 걸릴 수 있습니다.  
  
-   **연결 사용 안 함**  
  
     컴퓨터 연결이 방화벽으로 차단되거나 원격 데스크톱이 컴퓨터 또는 그룹 정책에서 사용 안 함으로 설정되었습니다. 변경 사항이 있으면 서버에서 이 상태가 업데이트되는 데 최대 6시간이 걸릴 수 있습니다.  
  
#### <a name="to-connect-to-a-computer-on-your-network"></a>네트워크에 있는 컴퓨터에 연결하려면  
 **장치** 탭에서 컴퓨터 이름을 클릭합니다. **사용 가능** 상태의 컴퓨터만 선택할 수 있습니다.  
  
#### <a name="to-connect-to-the-server-dashboard"></a>서버 대시보드에 연결하려면  
 **장치** 탭에서 서버 이름을 클릭합니다. **사용 가능** 상태의 컴퓨터만 선택할 수 있습니다. 대시보드를 사용하려면 서버에서 관리자의 사용자 계정과 암호를 제공할 수 있어야 합니다.  
  
##  <a name="BKMK_SharedFolders"></a>파일 및 폴더 공유  
  

-   [원격 웹 액세스에서 파일 업로드 및 다운로드](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_UploadRWA)  
  
-   [원격 웹 액세스에서 파일 및 폴더 만들기, 이름 바꾸기, 이동, 삭제 또는 복사](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_2)  

-   [원격 웹 액세스에서 파일 업로드 및 다운로드](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_UploadRWA)  
  
-   [원격 웹 액세스에서 파일 및 폴더 만들기, 이름 바꾸기, 이동, 삭제 또는 복사](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_2)  

  
###  <a name="BKMK_UploadRWA"></a>원격 웹 액세스에서 파일 업로드 및 다운로드  
 원격 웹 액세스 **공유 폴더** 탭에서 다음을 수행할 수 있습니다.  
  
-   컴퓨터에서 Windows Server Essentials로 파일을 업로드(전송)할 수 있습니다.  
  
    > [!NOTE]
    >  원격 웹 액세스에 폴더가 아니라 파일만 업로드할 수 있습니다. 서버의 **공유 폴더**에 컴퓨터와 같은 파일 및 폴더 계층 구조를 포함하려면 원격 웹 액세스에서 서버에 폴더를 만들고 만든 폴더에 파일을 업로드해야 합니다. 서버 폴더를 만드는 방법에 대한 자세한 내용은 [Add or move a server folder](../manage/Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_5)을 참조하세요.  
  
-   Windows Server Essentials에서 컴퓨터로 파일과 폴더를 다운로드(수신)합니다.  
  
-   Windows Server Essentials의 공유 폴더 내에 폴더를 만듭니다.  
  

-   Windows Server Essentials에서 파일과 폴더를 이동, 삭제하고 이름을 바꿉니다. 자세한 내용은 [원격 웹 액세스에서 파일 및 폴더 만들기, 이름 바꾸기, 이동, 삭제 또는 복사](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_2)를 참조 하세요.  

-   Windows Server Essentials에서 파일과 폴더를 이동, 삭제하고 이름을 바꿉니다. 자세한 내용은 [원격 웹 액세스에서 파일 및 폴더 만들기, 이름 바꾸기, 이동, 삭제 또는 복사](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_2)를 참조 하세요.  

  
#### <a name="upload-files"></a>파일 업로드  
  
###### <a name="to-upload-files"></a>파일을 업로드하려면  
  
1. 원격 웹 액세스에서 **공유 폴더** 탭을 클릭한 다음 공유 폴더 링크를 클릭합니다. 해당 공유 폴더에 있는 파일 및 폴더 목록이 표시됩니다.  
  
2. 파일과 폴더의 공유 폴더 목록에서 파일을 업로드할 폴더를 클릭한 다음 **업로드**를 클릭합니다.  
  
3. 표준 업로드 도구가 로드되지 않았으면 **표준 업로드 방법 사용**을 클릭합니다.  
  
4. **찾아보기**  를 클릭하여 컴퓨터에서 파일을 찾습니다.  
  
5. 컴퓨터에서 폴더를 탐색하여 업로드할 파일을 찾고 **열기**를 클릭합니다.  
  
6. 업로드할 파일에 대해 2단계와 3단계를 반복합니다.  
  
7. 업로드할 파일을 모두 추가했으면 **업로드**를 클릭합니다.  
  
   간편한 파일 업로드 도구는 Windows Server Essentials를 실행하는 서버에서 파일을 업로드하는 프로세스를 간소화합니다. 끌어서 놓기 기능을 사용하여 간편한 파일 업로드 도구에 원하는 만큼 파일을 추가한 다음 서버의 공유 폴더에 업로드할 수 있습니다.  
  
> [!NOTE]
>  여러 파일 업로드 기능은 HTML5와 호환되는 웹 브라우저에서 기본적으로 지원됩니다. 이 도구는 웹 브라우저에서 HTML5를 지원하지 않을 때만 필요합니다.  
  
###### <a name="to-upload-files-using-the-easy-file-upload-tool"></a>간편한 파일 업로드 도구를 사용하여 파일을 업로드하려면  
  
1.  원격 웹 액세스에서 **공유 폴더** 탭을 클릭한 다음 공유 폴더 링크를 클릭합니다. 해당 공유 폴더에 있는 파일 및 폴더 목록이 표시됩니다.  
  
2.  파일과 폴더의 공유 폴더 목록에서 파일을 업로드할 폴더를 클릭한 다음 **업로드**를 클릭합니다. 업로드할 대상 폴더가 없으면 **새 폴더**를 클릭하고 대화 상자에서 새 폴더의 이름을 입력한 다음 **확인**을 클릭합니다.  
  
3.  Windows Server Solutions 추가 기능을 실행해야 할 수 있습니다. 실행해야 하면 화면 위쪽에 있는 노란색 줄무늬를 클릭하고 **추가 기능** 실행을 클릭한 다음 대화 상자에서 **실행**을 클릭합니다.  
  
4.  간편한 파일 업로드 도구가 로드되지 않았으면 **간편한 파일 업로드 도구 사용**을 클릭합니다.  
  
5.  Windows 탐색기에서 간편한 파일 업로드 도구로 파일을 끌어서 놓거나 **찾아보기**를 클릭하여 파일을 선택합니다.  
  
6.  선택한 폴더에 업로드할 파일을 모두 추가했으면 **업로드**를 클릭합니다.  
  
7.  파일이 성공적으로 업로드되면 **닫기**를 클릭합니다.  
  
#### <a name="download-files-or-folders"></a>파일 또는 폴더 다운로드  
  
###### <a name="to-download-a-single-file"></a>단일 파일을 다운로드하려면  
  
1. 원격 웹 액세스에서 **공유 폴더** 탭을 클릭한 다음 공유 폴더 링크를 클릭합니다. 해당 공유 폴더에 있는 파일 및 폴더 목록이 표시됩니다.  
  
2. 공유 폴더 파일 목록에서 홈 컴퓨터에 다운로드하려는 파일 옆의 확인란을 클릭합니다.  
  
3. **다운로드**를 클릭하여 다운로드를 시작합니다.  
  
4. **파일 다운로드** 대화 상자에서 **저장**을 클릭하여 컴퓨터에 파일을 저장합니다.  
  
5. **다른 이름으로 저장** 대화 상자에서 파일을 저장할 위치를 선택하고 **저장**을 클릭합니다. 단일 파일은 다운로드되기 전에 압축되지 않습니다.  
  
   여러 파일 또는 폴더를 다운로드하기 위한 두 가지 옵션이 있습니다. 필요에 맞는 옵션을 선택합니다.  
  
> [!NOTE]
>  이러한 옵션은 컴퓨터에 여러 파일 또는 폴더를 다운로드하는 경우에만 사용할 수 있습니다.  
  
- **자동 압축 풀기 실행 파일 (.exe)**  
  
  > [!NOTE]
  >   이 섹션은 Windows Server Essentials를 실행 하는 서버에 적용 됩니다.  
  
   자동 압축 풀기 실행 파일은 압축된 파일과 압축 풀기(실행 파일) 프로그램을 결합하는 다운로드할 수 있는 파일입니다. 실행 프로그램을 실행하면 압축된 파일의 압축이 자동으로 풀립니다(자동 압축 풀기). 이 방법은 받는 사람에게 적합한 압축 풀기 유틸리티가 있는지에 관계없이 압축된 데이터를 배포하는 일반적인 방법입니다.  
  
  > [!NOTE]
  >  이 옵션은 유니코드 문자를 지원합니다.  
  
- **Windows 압축 폴더 (.zip)**  
  
   파일을 압축하면 원본 파일보다 더 작은 압축 버전 파일이 생성됩니다. 압축 버전 파일에는 .zip 파일 이름 확장명이 있습니다. 압축으로 크기가 최대한 감소하는 파일 형식은 텍스트 기반 파일 형식(예: .txt, .doc, .xls) 및 압축되지 않은 파일 형식을 사용하는 그래픽 파일(예: .bmp)입니다. 일부 그래픽 파일(예: .jpg 및 .gif 파일)은 이미 압축을 사용하고 압축으로 파일 크기가 거의 감소하지 않습니다. 또한 많은 그래픽이 포함된 Word 문서는 대부분 텍스트인 문서만큼 크기가 많이 감소하지 않습니다.  
  
  > [!NOTE]
  >  이 옵션은 Windows Server Essentials에서 국가별 파일 이름에 대 한 제한 된 지원을 제공 합니다.  
  
  실제 다운로드가 시작되기 전에 exe 또는 zip 파일이 생성됩니다. 다운로드되는 파일 개수 및 총 파일 크기에 따라 몇 분이 걸릴 수 있습니다. 다운로드 파일이 생성되고 나면 파일 다운로드는 백그라운드에서 수행됩니다. 따라서 다운로드 프로세스가 완료되는 동안 작업을 계속할 수 있습니다.  
  
###### <a name="to-download-multiple-files-or-folders"></a>여러 파일 또는 폴더를 다운로드하려면  
  
1.  원격 웹 액세스에서 **공유 폴더** 탭을 클릭한 다음 공유 폴더 링크를 클릭합니다. 해당 공유 폴더에 있는 파일 및 폴더 목록이 표시됩니다.  
  
2.  공유 폴더 파일 목록에서 홈 컴퓨터에 다운로드하려는 파일 또는 폴더 옆의 확인란을 클릭합니다.  
  
3.  **다운로드**를 클릭하여 다운로드를 시작합니다.  
  
4.  **다운로드 형식 선택** 대화 상자에서 원하는 다운로드 형식 옵션을 선택하고 **확인**을 클릭합니다. 압축 파일이 선택한 형식 옵션으로 준비됩니다.  
  
5.  **파일 다운로드** 대화 상자에서 **저장**을 클릭하여 컴퓨터에 파일을 저장합니다.  
  
6.  **다른 이름으로 저장** 대화 상자에서 파일을 저장할 위치를 선택하고 **저장**을 클릭합니다.  
  
#### <a name="retrieve-compressed-files-downloaded-to-your-computer"></a>컴퓨터에 다운로드된 압축 파일 검색  
  
> [!NOTE]
>   이 섹션은 Windows Server Essentials를 실행 하는 서버에 적용 됩니다.  
  
 다운로드할 파일 또는 폴더 여러 개를 선택하면 자동 압축 풀기 압축 실행 파일(.exe) 또는 압축(.zip) 파일을 받을 수 있습니다.  
  
###### <a name="to-retrieve-a-file-from-the-compressed-exe-file"></a>압축(.exe) 파일에서 파일을 검색하려면  
  
1.  컴퓨터에서 압축 파일을 두 번 클릭하여 엽니다.  
  
2.  지침에 따라 컴퓨터의 폴더에 파일을 추출합니다.  
  
###### <a name="to-retrieve-a-file-from-the-compressed-zip-file"></a>압축(.zip) 파일에서 파일을 검색하려면  
  
1.  컴퓨터에서 압축 파일을 두 번 클릭하여 엽니다.  
  
2.  검색할 파일을 선택하고 저장할 컴퓨터의 폴더로 파일을 끌어서 놓습니다.  
  
    > [!NOTE]
    >  타사 파일 압축 프로그램을 사용하는 경우 해당 프로그램에 대한 절차에 따라 압축 파일에서 파일을 추출합니다.  
  
###  <a name="BKMK_2"></a>원격 웹 액세스에서 파일 및 폴더 만들기, 이름 바꾸기, 이동, 삭제 또는 복사  
 원격 웹 액세스를 사용하여 기존 공유 폴더에 새 폴더를 만들고, 파일 및 폴더 이름을 바꾸고, 파일과 폴더를 이동 및 복사하고, 서버에서 파일과 폴더를 삭제할 수 있습니다.  
  
> [!NOTE]
>  Windows Server Essentials를 실행하는 서버에서 새 공유 폴더를 추가하려면 대시보드를 사용해야 합니다. 원격 웹 액세스에서 서버 콘솔에 연결하려면 **컴퓨터** 탭에서 서버 이름을 클릭하고 **연결**을 클릭한 다음 서버 로그온 지침에 따릅니다. 정책을 만드는 방법에 대한 자세한 내용은 [Add or move a server folder](../manage/Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_5)을 참조하세요.  
  
##### <a name="to-create-a-new-folder"></a>새 폴더를 만들려면  
  
1.  원격 웹 액세스에서 **공유 폴더** 탭을 클릭한 다음 공유 폴더 링크를 클릭합니다. 해당 공유 폴더에 있는 파일 및 폴더 목록이 표시됩니다.  
  
2.  작업 표시줄에서 **새 폴더**를 클릭합니다.  
  
3.  폴더 이름을 입력하고 **확인**을 클릭합니다.  
  
##### <a name="to-rename-a-file-or-folder"></a>파일 또는 폴더의 이름을 바꾸려면  
  
1.  원격 웹 액세스에서 **공유 폴더** 탭을 클릭한 다음 공유 폴더 링크를 클릭합니다. 해당 공유 폴더에 있는 파일 및 폴더 목록이 표시됩니다.  
  
2.  이름을 바꿀 파일 또는 폴더를 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 클릭합니다.  
  
3.  텍스트 상자에 새 이름을 입력하고 **확인**을 클릭합니다.  
  
##### <a name="to-move-files-or-folders"></a>파일 또는 폴더를 이동하려면  
  
1.  원격 웹 액세스에서 **공유 폴더** 탭을 클릭한 다음 공유 폴더 링크를 클릭합니다. 해당 공유 폴더에 있는 파일 및 폴더 목록이 표시됩니다.  
  
2.  이동할 파일 또는 폴더 옆의 확인란을 선택하고 선택한 파일 또는 폴더의 하나를 마우스 오른쪽 단추로 클릭한 다음 **잘라내기**를 클릭합니다.  
  
3.  파일 또는 폴더를 이동할 대상 폴더를 마우스 오른쪽 단추로 클릭하고 **붙여넣기**를 클릭합니다.  
  
##### <a name="to-delete-a-file-or-folder"></a>파일 또는 폴더를 삭제하려면  
  
1.  원격 웹 액세스에서 **공유 폴더** 탭을 클릭한 다음 공유 폴더 링크를 클릭합니다. 해당 공유 폴더에 있는 파일 및 폴더 목록이 표시됩니다.  
  
2.  삭제할 파일 또는 폴더 옆의 확인란을 선택하고 선택한 파일 또는 폴더의 하나를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
3.  선택한 파일 및 폴더를 삭제하도록 확인하려면 **예**를 클릭합니다.  
  
##### <a name="to-copy-files-or-folders"></a>파일 또는 폴더를 복사하려면  
  
1.  원격 웹 액세스에서 **공유 폴더** 탭을 클릭한 다음 공유 폴더 링크를 클릭합니다. 해당 공유 폴더에 있는 파일 및 폴더 목록이 표시됩니다.  
  
2.  복사할 파일 또는 폴더 옆의 확인란을 선택하고 선택한 파일 또는 폴더의 하나를 마우스 오른쪽 단추로 클릭한 다음 **복사**를 클릭합니다.  
  
3.  파일 또는 폴더를 복사할 대상 폴더를 마우스 오른쪽 단추로 클릭하고 **붙여넣기**를 클릭합니다.  
  
##  <a name="BKMK_ConnectMobile"></a>모바일 장치에서 연결  
  

-   [모바일 장치에서 원격 웹 액세스 사용](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_8)  
  
-   [모바일 장치에 대해 지원 되는 웹 브라우저](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_9)  

-   [모바일 장치에서 원격 웹 액세스 사용](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_8)  
  
-   [모바일 장치에 대해 지원 되는 웹 브라우저](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_9)  

  
###  <a name="BKMK_8"></a>모바일 장치에서 원격 웹 액세스 사용  
 스마트 폰에서 원격 웹 액세스에 로그온하여 서버의 공유 폴더에 있는 파일과 폴더를 볼 수 있습니다.  
  
> [!NOTE]
>  [Windows Phone Marketplace](http://www.windowsphone.com/apps/6c2f98d5-6fcf-4e1d-b8b1-cde62ea1a94a) 에서 Windows Server Essentials용 My Server 앱을 다운로드하고 사용하여 서버에 저장된 공유 폴더와 미디어 파일에 액세스할 수도 있습니다.  
  
##### <a name="to-log-on-to-remote-web-access-from-a-mobile-device"></a>모바일 장치에서 원격 웹 액세스에 로그온하려면  
  
1.  웹 브라우저를 열고 주소 표시줄에 **https://** _< 도메인\>이름_ **/remote** 을 입력 합니다.  S가 https에 포함 되어 있는지 확인 합니다.  
  
2.  원격 웹 액세스 로그온 페이지에서 텍스트 상자에 사용자 이름과 암호를 입력 한 다음 화살표를 클릭 합니다. 원격 웹 액세스의 모바일 버전에 로그온됩니다.  
  
##### <a name="to-switch-to-the-desktop-version-of-remote-web-access"></a>원격 웹 액세스의 데스크톱 버전으로 전환하려면  
  
1.  웹 브라우저를 열고 주소 표시줄에 **https://** _< 도메인\>이름_ **/remote** 을 입력 합니다.  S가 https에 포함 되어 있는지 확인 합니다.  
  
2.  원격 웹 액세스 로그온 페이지에서 텍스트 상자에 사용자 이름과 암호를 입력 하 고 **데스크톱 버전 보기**를 클릭 한 다음 화살표를 클릭 합니다. 원격 웹 액세스의 데스크톱 버전에 로그온됩니다.  
  
##### <a name="to-return-to-the-mobile-version-of-remote-web-access"></a>원격 웹 액세스의 모바일 버전으로 돌아가려면  
  
1. 로그 오프 합니다.  
  
2. 웹 브라우저를 열고 주소 표시줄에 **https://** _<\>_ 를 입력 합니다. S가 https에 포함 되어 있는지 확인 합니다.  
  
3. 원격 웹 액세스의 모바일 버전이 표시 됩니다. 원격 웹 액세스 로그온 페이지에서 텍스트 상자에 사용자 이름과 암호를 입력 한 다음 화살표를 클릭 합니다. 원격 웹 액세스의 모바일 버전에 로그온 되어 있습니다.  
  
   서버의 공유 폴더에서 파일과 폴더를 검색할 수 있습니다.  
  
###  <a name="BKMK_9"></a>모바일 장치에 대해 지원 되는 웹 브라우저  
 모바일 장치에 대해 지원되는 웹 브라우저는 다음과 같습니다.  
  
-   Internet Explorer Mobile 6.0 이상  
  
-   Safari  
  
-   Blackberry  
  
-   Symbian 6.0 이상  
  
-   Android  
  
-   Google Chrome  
  
-   Firefox  
  
## <a name="see-also"></a>참조  
  
-   [원격 웹 액세스 관리](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  

-   [원격으로 작업](Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 사용](Use-Windows-Server-Essentials.md)

-   [원격으로 작업](../use/Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 사용](../use/Use-Windows-Server-Essentials.md)

