---
title: "4 단계: Windows Server Essentials 대상 서버 마이그레이션 설정 및 데이터 이동"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e143df43-e227-4629-a4ab-9f70d9bf6e84
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: db1169a5415039498718a7988c711d068945b4b7
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="step-4-move-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>4 단계: Windows Server Essentials 대상 서버 마이그레이션 설정 및 데이터 이동

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

이 섹션 원본 서버에서 데이터 마이그레이션 및 설정에 대 한 정보를 제공합니다. 다음과 같이 대상 서버 설정 및 데이터 이동 합니다.  
  
-   [대상 서버에 데이터를 복사](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_CopyData)  
  
-   [네트워크를 구성](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_Network)  
  
-   [사용자 계정에 허용 된 컴퓨터 지도](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_MapPermittedComputers)  
  
##  <a name="BKMK_CopyData"></a>대상 서버에 데이터를 복사  
 대상 서버에 데이터 소스 서버에서 복사 하기 전에 다음과 같은 작업을 수행 합니다.  
  
-   각 폴더에 대 한 권한을 포함 하 여 원본 서버의 공유 폴더 목록을 검토 합니다. 만들거나 폴더 원본 서버에서 마이그레이션하는 폴더 구조 일치 하도록 대상 서버에 사용자 지정 합니다.  
  
-   각 폴더의 크기를 검토 하 고 대상 서버에 충분 한 공간이 있는지 확인 합니다.  
  
-   원본 서버의 공유 폴더 만들기 Read-only 모든 사용자에 대해 없는 필기 하는 동안 하드 드라이브에 장소를 수행할 수 있도록 복사할 파일 대상 서버에 있습니다.  
  
-   **클라이언트 컴퓨터 백업** 폴더 대상 서버로 마이그레이션할 수 없습니다. 서버 마이그레이션 하기 전에 모든 클라이언트 컴퓨터 올바르게 작동 하는지 확인 합니다. 서버 마이그레이션 후 것이 좋습니다 구성 하 고 모든 중요 한 클라이언트 컴퓨터에 대 한 데이터를 백업는 되도록 컴퓨터 백업을 클라이언트를 시작 합니다.  
  
-   **파일 히스토리를 백업** 폴더 Windows Server Essentials의 폴더 및 백업 구조 메타 데이터 변경 했기 때문에 대상 서버에 직접 마이그레이션할 수 없습니다. 그러나 마이그레이션할 수는 **파일 히스토리를 백업** 특정 컴퓨터에서 특정 사용자를 위한 폴더 합니다. 이렇게 하기 위해 찾아야는 **데이터** 폴더에 있는 **파일 히스토리를 백업** 폴더 해당 사용자와 컴퓨터에 복사 하는 **데이터** 폴더를는 **파일 히스토리를 백업** 대상 서버의 폴더 합니다.  
  
#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>원본 서버에서 대상 서버에 데이터를 복사 하려면  
  
1.  도메인 관리자로 대상 서버에에 로그인 한 다음 명령 프롬프트 창이 나 Windows PowerShell 명령 프롬프트를 엽니다.  
  
2.  명령 프롬프트 창을 사용 하는 경우 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
    `robocopy \\<SourceServerName>\<SharedSourceFolderName> "<PathOfTheDestination>\<SharedDestinationFolderName>" /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`
  
     위치:  
  
    -   \ < SourceServerName\ >은 원본 서버의 이름입니다.  
  
    -   \ < SharedSourceFolderName\ >은 원본 서버에서 공유 된 폴더의 이름입니다.  
  
    -   \ < PathOfTheDestination\ > 절대 경로 폴더를 이동 하려면 사용자는  
  
    -   \ < SharedDestinationFolderName\ >는 데이터가 복사 대상 서버에 폴더  
  
     예를 들어, `robocopy \\sourceserver\MyData "d:\ServerFolders\MyData" /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`합니다.  
  
3.  Windows PowerShell를 사용 하는 경우 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
     `Add-Wssfolder  Path \ -Name  -KeepPermission`  
  
4.  원본 서버에서 마이그레이션하는 각 공유 폴더에 대 한이 프로세스를 반복 합니다.  
  
##  <a name="BKMK_Network"></a>네트워크를 구성  
  
#### <a name="to-configure-the-network"></a>네트워크를 구성  
  
1.  대상 서버의 대시보드를 엽니다.  
  
2.  대시보드에서 **홈** 페이지, 클릭 **설치**, 클릭 **어디서 나 액세스를 설정**, 다음 선택 하 고는 **구성 원하는 위치에 액세스 하려면 클릭** 옵션 합니다.  
  
3.  어디서 나 액세스 마법사 설정 표시 됩니다. 도메인 이름 및 라우터 구성 하 고 마법사의 지침을 완료 합니다.  
  
 라우터 UPnP framework를 지원 하지 않는 경우 또는 UPnP 프레임 워크를 사용 하지 않는 경우 라우터에 이름 옆에 노란색 경고 아이콘이 나타날 수 있습니다. 다음 포트 열기 되며 대상 서버의 IP 주소를 전달 하는 것이 있는지 확인 합니다.  
  
-   포트 80: HTTP 웹 교통량  
  
-   HTTPS 웹 교통 포트 443:  
  
> [!NOTE]
>  공용 도메인 이름 대상 서버의 구성 하려면 거래법 동적 DNS 업데이트 되지 않도록 하 여 원본 서버에서 도메인 이름을 해제 해야 합니다.  
  
##  <a name="BKMK_MapPermittedComputers"></a>사용자 계정에 허용 된 컴퓨터 지도  
 마이그레이션 Small Business Server Windows 또는 Windows Server Essentials의 이전 버전의 각 사용자 계정 하나 이상의 컴퓨터에 매핑됩니다 해야 합니다.  
  
#### <a name="to-map-user-accounts-to-computers"></a>컴퓨터에 사용자 계정이 지도로  
  
1.  Windows Server Essentials 대시보드를 엽니다.  
  
2.  탐색 모음에서 클릭 **사용자**합니다.  
  
3.  사용자 계정의 목록에서 사용자 계정 마우스 클릭 한 다음 **계정 속성 보기**합니다.  
  
4.  클릭 하 고 **원하는 위치에 액세스** 탭을 클릭 한 다음 **웹 원격 액세스 허용와 웹 서비스 응용 프로그램에 대 한 액세스**합니다.  
  
5.  클릭 **공유 폴더**, 클릭**컴퓨터**, 클릭 **홈페이지 링크**을 차례로 클릭 하 고 **적용**합니다.  
  
6.  클릭 하 고 **컴퓨터 액세스** 탭을 선택한 다음 액세스 허용 하려면 컴퓨터의 이름을 클릭 합니다.  
  
7.  각 사용자 계정에 대 한 3, 4, 5, 6 단계를 반복 합니다.  
  
> [!NOTE]
>  클라이언트 컴퓨터 구성 변경할 필요가 없습니다. 자동으로 구성 되어 있습니다.  
  
> [!NOTE]
>  대상 서버에서 첫 번째 새 사용자 계정을 만들 때 문제가 발생 하는 경우 마이그레이션을 완료 한 후 사용자 계정이 추가한 제거한 다음 다시 만들어야 합니다.  
  
## <a name="next-steps"></a>다음 단계  
 대상 서버 설정 및 데이터 옮겼습니다. 지금 이동 [5 단계: Windows Server Essentials 대상 서버 마이그레이션에 폴더 리디렉션을 사용](Step-5--Enable-folder-redirection-on-the-Destination-Server-for-Windows-Server-Essentials-migration.md)합니다.  
  

모든 단계를 참조 [Windows Server essentials 마이그레이션](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)합니다.

