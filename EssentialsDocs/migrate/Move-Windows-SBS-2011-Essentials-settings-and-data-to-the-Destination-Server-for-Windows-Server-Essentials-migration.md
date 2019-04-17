---
title: "Windows Server Essentials 대상 서버 마이그레이션 SBS 2011 Windows Essentials 설정 및 데이터 이동"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47548994-9fa0-42e0-afa4-c2ccbd063acb
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 80ef8a196f70a77e149dc8defaacf20a82d576e7
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="move-windows-sbs-2011-essentials-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Windows Server Essentials 대상 서버 마이그레이션 SBS 2011 Windows Essentials 설정 및 데이터 이동

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

다음과 같이 대상 서버 설정 및 데이터 이동 합니다.  
  

1.  [대상 서버에 데이터를 복사](Move-Windows-SBS-2011-Essentials-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_CopyData)  
  
2.  [사용자 계정 Active Directory (선택 사항) Windows Server Essentials 대시보드를 가져오기](Move-Windows-SBS-2011-Essentials-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_ImportADaccounts)  
  
3.  [네트워크를 구성](Move-Windows-SBS-2011-Essentials-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_Network)  
  
4.  [사용자 계정에 허용 된 컴퓨터 지도](Move-Windows-SBS-2011-Essentials-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_MapPermittedComputers)  
 
##  <a name="BKMK_CopyData"></a>대상 서버에 데이터를 복사  
 대상 서버에 데이터 소스 서버에서 복사 하기 전에 다음과 같은 작업을 수행 합니다.  
  
-   각 폴더에 대 한 권한을 포함 하 여 원본 서버의 공유 폴더 목록을 검토 합니다. 만들거나 폴더 원본 서버에서 마이그레이션하는 폴더 구조 일치 하도록 대상 서버에 사용자 지정 합니다.  
  
-   각 폴더의 크기를 검토 하 고 대상 서버에 충분 한 공간이 있는지 확인 합니다.  
  
-   확인 원본 서버의 공유 폴더 읽기 전용 모든 사용자에 대해 대상 서버에 파일을 복사 하는 동안 없이 쓰기 드라이브에 장소를 될 수 있도록 합니다.  
  
#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>원본 서버에서 대상 서버에 데이터를 복사 하려면  
  
1.  도메인 관리자로 대상 서버에 로그인 한 다음 명령을 창을 엽니다.  
  
2.  명령 프롬프트에서 다음 명령을 입력 하 고 enter 다음과 같습니다.  
  
    `robocopy \\<SourceServerName> \<SharedSourceFolderName> \\<DestinationServerName> \<SharedDestinationFolderName> /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`  
  
     위치:
     - \ < SourceServerName\ >은 원본 서버의 이름입니다.
     - \ < SharedSourceFolderName\ >은 원본 서버에서 공유 된 폴더의 이름입니다.
     - \ < DestinationServerName\ >는 대상 폴더의 이름
     - \ < SharedDestinationFolderName\ >는 공유 폴더 대상 서버의 데이터 복사할 수 있습니다.  
        
3.  원본 서버에서 마이그레이션하는 각 공유 폴더를 이전 단계를 반복 합니다.  
  
##  <a name="BKMK_ImportADaccounts"></a>사용자 계정 Active Directory (선택 사항) Windows Server Essentials 대시보드를 가져오기  
 기본적으로 원본 서버의 만든 모든 사용자 계정에서 Windows Server Essentials 대시보드도 이동 자동으로 않습니다. 그러나 자동 마이그레이션 Active Directory 사용자 계정의 모든 속성 마이그레이션 요구 사항을 충족 하지 않는 경우 되지 것입니다. 사용자 Active Directory를 가져오려면 다음 Windows PowerShell cmdlet에 사용할 수 있습니다.  
  
#### <a name="to-import-an-active-directory-user-account-to-the-windows-server-essentials-dashboard"></a>Windows Server Essentials 대시보드 Active Directory 사용자 계정 가져오려면  
  
1.  대상 서버 도메인 관리자 권한으로 로그온 합니다.  
  
2.  Windows PowerShell을 관리자 권한으로 엽니다.  
  
3.  다음 cmdlet 실행 여기서 `[AD username]` 가져올 Active Directory 사용자 계정 이름입니다.  
  
     `Import-WssUser  SamAccountName [AD username]`  
  
##  <a name="BKMK_Network"></a>네트워크를 구성  
  
#### <a name="to-configure-the-network"></a>네트워크를 구성  
  
1.  대상 서버의 대시보드를 엽니다.  
  
2.  대시보드에서 **홈** 페이지, 클릭 **설치**, 클릭 **어디서 나 액세스를 설정**, 다음 선택 하 고는 **구성 원하는 위치에 액세스 하려면 클릭** 옵션 합니다.  
  
3.  도메인 이름 및 라우터 구성 하 고 마법사의 지침을 완료 합니다.  
  
 라우터 UPnP framework를 지원 하지 않는 경우 또는 UPnP 프레임 워크를 사용 하지 않는 경우 라우터에 이름 옆에 노란색 경고 아이콘이 나타날 수 있습니다. 다음 포트 열기 되며 대상 서버의 IP 주소를 전달 하는 것이 있는지 확인 합니다.  
  
-   포트 80: HTTP 웹 교통량  
  
-   HTTPS 웹 교통 포트 443:  
  
##  <a name="BKMK_MapPermittedComputers"></a>사용자 계정에 허용 된 컴퓨터 지도  
 각 사용자 계정에서 Windows 작은 Business Server 2011 Essentials 마이그레이션 하나 이상의 컴퓨터에 매핑됩니다 해야 합니다.  
  
#### <a name="to-map-user-accounts-to-computers"></a>컴퓨터에 사용자 계정이 지도로  
  
1.  Windows Server Essentials 대시보드를 엽니다.  
  
2.  탐색 모음에서 클릭 **사용자**합니다.  
  
3.  사용자 계정의 목록에서 사용자 계정 마우스 클릭 한 다음 **계정 속성 보기**합니다.  
  
4.  클릭 하 고 **원하는 위치에 액세스** 탭을 클릭 한 다음 **웹 원격 액세스 허용와 웹 서비스 응용 프로그램에 대 한 액세스**합니다.  
  
5.  선택 **공유 폴더**, **컴퓨터**선택 **홈페이지 링크**을 차례로 클릭 하 고 **적용**합니다.  
  
6.  클릭 하 고 **컴퓨터 액세스** 탭을 선택한 다음 액세스 허용 하려면 컴퓨터의 이름을 클릭 합니다.  
  
7.  각 사용자 계정에 대 한 3, 4, 5, 6 단계를 반복 합니다.  
  
> [!NOTE]
>  클라이언트 컴퓨터 구성 변경할 필요가 없습니다. 자동으로 구성 되어 있습니다.  
  
> [!NOTE]
>  대상 서버에서 첫 번째 새 사용자 계정을 만들 때 문제가 발생 하는 경우 마이그레이션을 완료 한 후 사용자 계정이 추가한 제거한 다음 다시 만들어야 합니다.
