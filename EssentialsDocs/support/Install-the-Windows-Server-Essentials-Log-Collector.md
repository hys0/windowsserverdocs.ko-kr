---
title: Windows Server Essentials 로그 수집기 설치
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: d271c54f-1ffa-464e-afa5-27b8df61854e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ecffbfd3157720ad2762ba77d528af05e5abf53f
ms.sourcegitcommit: 56ac7cf3f4bbcc5175f140d2df5f37cc42ba76d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85217543"
---
# <a name="install-the-windows-server-essentials-log-collector"></a>Windows Server Essentials 로그 수집기 설치

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server Essentials 로그 수집기 설치 마법사에서 로그 수집기를 실행 패드 추가 기능으로 설치 합니다. 네트워크 컴퓨터 또는 서버나 이 둘 모두에서 로그 수집기를 설치하고 사용할 수 있습니다. 설치하고 나면 로그 수집기가 대시보드에 표시됩니다.  
  
###  <a name="to-install-the-log-collector"></a><a name="BKMK_ToInstall"></a>로그 수집기를 설치 하려면  
  
1.  로그 수집기 설치 패키지를 서버 또는 네트워크의 컴퓨터에 다운로드합니다.  
  
    > [!NOTE]
    > [Windows Server Essentials 로그 수집기 설치 패키지를 다운로드](https://www.microsoft.com/download/details.aspx?id=34821)합니다.  
  
2.  로그 수집기 아이콘을 두 번 클릭합니다.  
  
3.  네트워크 컴퓨터에서 설치를 실행 중이면 메시지가 표시될 때 서버 관리자 자격 증명을 입력합니다.  
  
4.  Microsoft 소프트웨어 사용 조건에 동의하려면 선택합니다.  
  
5.  서버에만 로그 수집기를 설치하려면 **서버에만** 확인란을 선택합니다. 모든 네트워크 컴퓨터에 로그 수집기를 설치하려면 **서버 및 네트워크에 있는 모든 컴퓨터에** 확인란을 선택합니다.  
  
6.  **추가 기능 설치**를 클릭합니다.  
  
###  <a name="reinstalling-the-log-collector"></a><a name="BKMK_Reinstall"></a>로그 수집기 다시 설치  
 로그 수집기를 다시 설치해야 한다면 서버 및 네트워크에 있는 네트워크 컴퓨터에서 로그 수집기를 제거하고 다시 설치해야 합니다. 대시보드를 통해 서버에서 로그 수집기를 제거하면 모든 네트워크 컴퓨터에서 로그 수집기가 자동으로 제거됩니다.  
  
##### <a name="to-uninstall-and-reinstall-the-log-collector"></a>로그 수집기를 제거하고 다시 설치하려면  
  
1.  대시보드를 엽니다.  
  
2.  **추가 기능** 탭을 클릭하고 목록에서 **로그 수집기**를 선택한 다음 **제거**를 클릭합니다.

3.  이전 절차 [로그 수집기를 설치하려면](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_ToInstall)의 단계를 수행하여 로그 수집기를 다운로드하고 설치합니다.   
  
### <a name="manually-install-the-log-collector"></a>수동으로 로그 수집기 설치  
 설치 마법사에서 로그 수집기를 설치하지 못하면 다음 절차에 따라 단일 컴퓨터에 로그 수집기를 설치할 수 있습니다.  
  
##### <a name="to-manually-install-the-log-collector"></a>로그 수집기를 수동으로 설치하려면  
  
1.  다운로드 한 설치 파일의 확장명을 .wax에서 .cab로 바꿉니다.  
  
2.  설치 파일 이름을 두 번 클릭합니다.  
  
3.  메시지가 표시되면 **확인**을 클릭합니다.  
  
4.  ' .Msi '로 끝나는 파일 이름을 두 번 클릭 하 고 파일을 추출할 폴더를 선택 합니다.  
  
5.  추출된 파일이 포함된 폴더로 이동하고 설치 파일을 두 번 클릭하여 마법사를 통해 설치를 완료합니다.
