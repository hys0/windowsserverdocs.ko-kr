---
title: '4단계: Windows Server Essentials 마이그레이션을 위해 대상 서버로 설정 및 데이터 이동'
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e143df43-e227-4629-a4ab-9f70d9bf6e84
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d9aea85513e2453c02f6c14fb3f4d708be211d3f
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318752"
---
# <a name="step-4-move-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>4단계: Windows Server Essentials 마이그레이션을 위해 대상 서버로 설정 및 데이터 이동

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

이 섹션에서는 원본 서버에서 데이터 및 설정을 마이그레이션하는 방법에 대한 정보를 제공합니다. 다음과 같이 설정 및 데이터를 대상 서버로 이동합니다.  
  
-   [대상 서버에 데이터 복사](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_CopyData)  
  
-   [네트워크 구성](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_Network)  
  
-   [허용 된 컴퓨터를 사용자 계정에 매핑](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_MapPermittedComputers)  
  
##  <a name="copy-data-to-the-destination-server"></a><a name="BKMK_CopyData"></a>대상 서버에 데이터 복사  
 원본 서버에서 대상 서버로 데이터를 복사하기 전에 다음 작업을 수행합니다.  
  
-   각 폴더에 대한 사용 권한을 비롯하여 원본 서버의 공유 폴더 목록을 검토합니다. 원본 서버에서 마이그레이션할 폴더 구조와 일치하도록 대상 서버에서 폴더를 만들거나 사용자 지정합니다.  
  
-   각 폴더의 크기를 검토하고 대상 서버에 충분한 저장 공간이 있는지 확인합니다.  
  
-   파일을 대상 서버에 복사하는 동안 하드 드라이브에 기록이 수행되지 않도록 원본 서버의 공유 폴더를 모든 사용자에 대해 읽기 전용으로 설정합니다.  
  
-   **클라이언트 컴퓨터 백업** 폴더는 대상 서버로 마이그레이션할 수 없습니다. 서버 마이그레이션 전에 모든 클라이언트 컴퓨터가 정상 상태인지 확인합니다. 서버 마이그레이션 후에는 모든 중요한 클라이언트 컴퓨터의 데이터가 백업되도록 클라이언트 컴퓨터 백업을 구성하고 시작하는 것이 좋습니다.  
  
-   Windows Server Essentials의 폴더 구조 및 백업 메타 데이터 변경 때문에 **파일 히스토리 백업** 폴더는 대상 서버로 직접 마이그레이션할 수 없습니다. 그러나 특정 컴퓨터에서 특정 사용자에 대한 **파일 히스토리 백업** 폴더를 마이그레이션할 수는 있습니다. 이렇게 하려면 해당 사용자 및 컴퓨터의 **파일 히스토리 백업** 폴더에서 **데이터** 폴더를 찾은 후 해당 **데이터** 폴더를 대상 서버의 **파일 히스토리 백업** 폴더에 복사해야 합니다.  
  
#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>원본 서버에서 대상 서버로 데이터를 복사하려면  
  
1. 도메인 관리자로 대상 서버에 로그인한 후 명령 프롬프트 창 또는 Windows PowerShell 명령 프롬프트를 엽니다.  
  
2. 명령 프롬프트 창을 사용하는 경우 다음 명령을 입력하고 Enter 키를 누릅니다.  
  
   `robocopy \\<SourceServerName>\<SharedSourceFolderName> "<PathOfTheDestination>\<SharedDestinationFolderName>" /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`
  
    각 항목이 나타내는 의미는 다음과 같습니다.  
  
   - \<SourceServerName\>은 원본 서버의 이름입니다.  
  
   - \<SharedSourceFolderName\>은 원본 서버의 공유 폴더 이름입니다.  
  
   - \<Paanfto Destination\>는 폴더를 이동 하려는 절대 경로입니다.  
  
   - \<SharedDestinationFolderName\>는 데이터가 복사 될 대상 서버의 폴더입니다.  
  
     `robocopy \\sourceserver\MyData "d:\ServerFolders\MyData" /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`를 예로 들 수 있습니다.  
  
3. Windows PowerShell을 사용하는 경우 다음 명령을 입력하고 Enter 키를 누릅니다.  
  
    `Add-Wssfolder  Path \ -Name  -KeepPermission`  
  
4. 원본 서버에서 마이그레이션하는 각 공유 폴더에 대해 이 프로세스를 반복합니다.  
  
##  <a name="configure-the-network"></a><a name="BKMK_Network"></a>네트워크 구성  
  
#### <a name="to-configure-the-network"></a>네트워크를 구성하려면  
  
1. 대상 서버에서 대시보드를 엽니다.  
  
2. 대시보드 **홈** 페이지에서 **설정**, **원격 액세스 설정**을 차례로 클릭하고 **원격 액세스를 구성하려면 클릭** 옵션을 선택합니다.  
  
3. 원격 액세스 설정 마법사가 나타납니다. 마법사의 지침을 완료하여 라우터 및 도메인 이름을 구성합니다.  
  
   라우터에서 UPnP 프레임워크를 지원하지 않거나 UPnP 프레임워크가 사용되지 않으면 라우터 이름 옆에 노란색 경고 아이콘이 나타날 수 있습니다. 다음 포트가 열려 있으며 대상 서버의 IP 주소로 보내지는지 확인합니다.  
  
-   포트 80: HTTP 웹 트래픽  
  
-   포트 443: HTTPS 웹 트래픽  
  
> [!NOTE]
>  대상 서버에서 공용 도메인 이름을 구성하려면 동적 DNS 업데이트 경쟁을 방지하기 위해 원본 서버에서 도메인 이름을 해제해야 합니다.  
  
##  <a name="map-permitted-computers-to-user-accounts"></a><a name="BKMK_MapPermittedComputers"></a>허용 된 컴퓨터를 사용자 계정에 매핑  
 이전 버전의 Windows Small Business Server 또는 Windows Server Essentials에서 마이그레이션된 각 사용자 계정은 하나 이상의 컴퓨터에 매핑되어야 합니다.  
  
#### <a name="to-map-user-accounts-to-computers"></a>사용자 계정을 컴퓨터에 매핑하려면  
  
1.  Windows Server Essentials 대시보드를 엽니다.  
  
2.  탐색 모음에서 **사용자**를 클릭합니다.  
  
3.  사용자 계정 목록에서 사용자 계정을 마우스 오른쪽 단추로 클릭하고 **계정 속성 보기**를 클릭합니다.  
  
4.  **원격 액세스** 탭을 클릭하고 **원격 웹 액세스 허용 및 웹 서비스 응용 프로그램에 액세스**을 클릭합니다.  
  
5.  **공유 폴더**, **컴퓨터**, **홈 페이지 링크** 및 **적용**을 차례로 클릭합니다.  
  
6.  **컴퓨터 액세스** 탭을 클릭하고 액세스를 허용할 컴퓨터 이름을 클릭합니다.  
  
7.  각 사용자 계정에 대해 3, 4, 5, 6단계를 반복합니다.  
  
> [!NOTE]
>  클라이언트 컴퓨터의 구성을 변경할 필요가 없습니다. 자동으로 구성됩니다.  
  
> [!NOTE]
>  마이그레이션을 완료하고 나서 대상 서버에서 첫 번째 새 사용자 계정을 만들 때 문제가 발생하면 추가한 사용자 계정을 제거하고 다시 만듭니다.  
  
## <a name="next-steps"></a>다음 단계  
 설정 및 데이터를 대상 서버로 이동했습니다. 이제 [5 단계: Windows Server Essentials 마이그레이션을 위해 대상 서버에서 폴더 리디렉션 사용](Step-5--Enable-folder-redirection-on-the-Destination-Server-for-Windows-Server-Essentials-migration.md)으로 이동 합니다.  
  

모든 단계를 보려면 [Windows Server Essentials로 마이그레이션](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)을 참조 하세요.

