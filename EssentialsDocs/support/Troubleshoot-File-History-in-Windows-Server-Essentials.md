---
title: "Windows Server Essentials의 파일 히스토리 문제 해결"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed062945-27e9-4572-b1bb-6c8cf1b9c2f4
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 34442565b54b089064c1fa19317a24f591e44fda
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="troubleshoot-file-history-in-windows-server-essentials"></a>Windows Server Essentials의 파일 히스토리 문제 해결

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다. 
  
## <a name="troubleshoot-issues-with-user-file-history-backups"></a>사용자 파일 히스토리를 백업 문제 해결  
 사용자 또는 Windows Server Essentials 실행 하는 서버에 추가 된 컴퓨터에 대 한 백업을 파일 히스토리를 관리 하는 동안 다음과 같은 문제가 발생할 수 있습니다.  
  
### <a name="file-history-data-is-not-automatically-deleted"></a>파일 히스토리 데이터는 자동으로 삭제 되지  
 하는 경우 파일 히스토리 데이터 자동으로 삭제 되지 않을 수 있습니다.  
  
-   사용자 계정을 삭제 하는 경우 사용자 계정의 파일 히스토리 데이터를 삭제 하지 않는 선택 하 고 데이터를 삭제 하 여 수동으로 옵트아웃 (opt).  
  
-   파일 히스토리 데이터를 삭제 하려는 파일 히스토리 데이터는 다른 프로세스에서 사용에서 됩니다.  
  
 이 문제를 해결 하려면 수동으로 다음 절차를 사용 하 여 파일 히스토리를 삭제 해야 합니다.  
  
####  <a name="BKMK_manuallyDelete"></a>수동으로 사용자 또는 컴퓨터에 대 한 파일 히스토리 백업을 삭제 하려면  
  
1.  서버에 관리자 권한으로 로그온 합니다.  
  
2.  파일 탐색기 관리자 권한으로 실행 합니다.  
  
3.  파일 히스토리를 백업 폴더로 이동 합니다. 기본 위치는 C:\ServerFolders\File 기록 백업 합니다.  
  
4.  파일 히스토리 백업을 저장 하는 공유 폴더를 삭제 합니다.  
  
    -   사용자의 파일 히스토리를 삭제 하려면 사용자 s 이름이 지정 된 파일 히스토리 백업 하위 폴더를 삭제 합니다.  
  
    -   컴퓨터에 대 한 파일 히스토리를 삭제 하려면 컴퓨터 이름이 파일 히스토리 백업 하위 폴더를 삭제 합니다. 예를 들어, 사용자가 새로운 랩톱 < MyComputer02\ >에서 작업을 시작한 많이 후 < MyComputer01\ > 하드웨어가 경우 C:\ServerFolders\File 기록 Backups\\ < MyAccount\ > 삭제 것 \\ < MyComputer01\ > 모든 파일 및 폴더의 새로운 노트북으로 전송에 있 및 파일 히스토리에 대 한 불필요 나중에 사용자와 확인 합니다.  
  
### <a name="cannot-apply-file-history-setting-to-a-new-user"></a>파일 히스토리 설정 새 사용자에 게 적용할 수 없습니다.  
 사용자 이름이 Windows Server Essentials에서 삭제 된 사용자의 사용자 이름 동일 새 사용자를 추가 하면, Windows Server Essentials 새 사용자의 파일 히스토리를 저장할 폴더를 만들 하려고 할 때 새 사용자의 파일 히스토리 구성을 충돌 하는 때문에 실패할 수 있습니다. 이 문제를 해결 하려면 삭제 된 사용자의 파일 히스토리 폴더 이름을 바꿀 수 있습니다.  
  
##### <a name="to-locate-user-file-history-on-the-server"></a>서버에서 사용자의 파일 히스토리를 찾을 수  
  
1.  서버에 관리자 권한으로 로그온 합니다.  
  
2.  Windows Server Essentials 대시보드에서 클릭 **저장소**합니다.  
  
3.  에 **서버 폴더** 탭에서 파일 히스토리를 백업 폴더의 위치를 확인 합니다. 기본 위치 기록을 Backups\\ %SystemDrive%\ServerFolders\File입니다.  
  
##### <a name="to-resolve-file-history-issues-for-a-new-user-with-a-name-conflict"></a>새 사용자 이름이 충돌 파일 기록 문제를 해결 하려면  
  
1.  서버에 관리자 권한으로 로그온 합니다.  
  
2.  파일 탐색기 관리자 권한으로 실행 합니다.  
  
3.  파일 히스토리를 백업 폴더로 이동 합니다. 기본 위치는 C:\ServerFolders\File 기록 백업 합니다.  
  
     파일 히스토리를 백업 폴더 Windows Server Essentials에 추가 된 각 사용자 계정에 대 한 하위 폴더를 있습니다. 예를 들어, 파일 히스토리 John 홍 사용자에 대 한 파일 히스토리 Backups\JohnSmith 하위 폴더에 저장 됩니다.  
  
4.  예를 들어, 삭제 된 사용자의 하위 폴더 이름을 바꿀 **<*사용자 이름*> _Deleted * *. 사용자의 파일 히스토리를 더 이상 필요 하면 폴더를 삭제할 수 없습니다.  
  

5.  이제 새 사용자를 추가할 수 있습니다. 사용자 계정 추가 참조 하십시오. [사용자 계정 관리](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md)합니다.  
  
### <a name="a-user-account-was-removed-but-the-users-file-history-remains"></a>사용자 계정을 제거 그대로 사용자의 파일 히스토리  
 경우에 따라 네트워크 관리자 서버에서 사용자 또는 컴퓨터 제거 되지만 파일 히스토리를 나중에 사용에 대 한 백업으로 유지 하려면 선택할 수 있습니다. 파일 히스토리를 더 이상 필요 서버의 공유 폴더에서 사용자 또는 컴퓨터에 대 한 파일 히스토리를 백업 폴더를 제거 합니다. 이 위해 표시 [수동으로 사용자 또는 컴퓨터에 대 한 파일 히스토리 백업을 삭제 하려면](Troubleshoot-File-History-in-Windows-Server-Essentials.md#BKMK_manuallyDelete)합니다.  

5.  이제 새 사용자를 추가할 수 있습니다. 사용자 계정 추가 참조 하십시오. [사용자 계정 관리](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md)합니다.  
  
### <a name="a-user-account-was-removed-but-the-users-file-history-remains"></a>사용자 계정을 제거 그대로 사용자의 파일 히스토리  
 경우에 따라 네트워크 관리자 서버에서 사용자 또는 컴퓨터 제거 되지만 파일 히스토리를 나중에 사용에 대 한 백업으로 유지 하려면 선택할 수 있습니다. 파일 히스토리를 더 이상 필요 서버의 공유 폴더에서 사용자 또는 컴퓨터에 대 한 파일 히스토리를 백업 폴더를 제거 합니다. 이 위해 표시 [수동으로 사용자 또는 컴퓨터에 대 한 파일 히스토리 백업을 삭제 하려면](../support/Troubleshoot-File-History-in-Windows-Server-Essentials.md#BKMK_manuallyDelete)합니다.  

  
## <a name="see-also"></a>참조 하십시오  
  
-   [클라이언트 백업 관리](../manage/Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md)  
  

-   [Windows Server Essentials 지원](Support-Windows-Server-Essentials.md)

-   [Windows Server Essentials 지원](../support/Support-Windows-Server-Essentials.md)

