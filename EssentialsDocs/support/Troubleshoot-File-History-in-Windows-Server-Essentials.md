---
title: Windows Server Essentials의 파일 히스토리 문제 해결
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: ed062945-27e9-4572-b1bb-6c8cf1b9c2f4
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: fbdc74b8c0d2ce6db619e4d4ad646a92eb859bc3
ms.sourcegitcommit: 56ac7cf3f4bbcc5175f140d2df5f37cc42ba76d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85217483"
---
# <a name="troubleshoot-file-history-in-windows-server-essentials"></a>Windows Server Essentials의 파일 히스토리 문제 해결

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials 
  
## <a name="troubleshoot-issues-with-user-file-history-backups"></a>사용자 파일 히스토리 백업과 관련된 문제 해결  
 Windows Server Essentials를 실행하는 서버에 추가된 사용자 또는 컴퓨터에 대한 파일 히스토리 백업을 관리하는 동안 다음과 같은 문제가 발생할 수 있습니다.  
  
### <a name="file-history-data-is-not-automatically-deleted"></a>파일 히스토리 데이터가 자동으로 삭제되지 않음  
 다음과 같은 경우 파일 히스토리 데이터가 자동으로 삭제되지 않을 수 있습니다.  
  
- 사용자 계정을 삭제할 때 사용자 계정의 파일 히스토리 데이터를 삭제 하지 않고 데이터를 수동으로 삭제 하도록 선택 합니다.  
  
- 파일 히스토리 데이터를 삭제하려고 할 때 파일 히스토리 데이터가 다른 프로세스에서 사용 중입니다.  
  
  이 문제를 해결하려면 다음 절차에 따라 파일 히스토리를 수동으로 삭제해야 합니다.  
  
####  <a name="to-manually-delete-file-history-backups-for-a-user-or-a-computer"></a><a name="BKMK_manuallyDelete"></a>사용자 또는 컴퓨터에 대 한 파일 히스토리 백업을 수동으로 삭제 하려면  
  
1.  관리자 권한으로 서버에 로그온합니다.  
  
2.  관리자 권한으로 파일 탐색기를 실행합니다.  
  
3.  파일 히스토리 백업 폴더로 이동합니다. 기본 위치는 C:\ServerFolders\File History Backups입니다.  
  
4.  파일 히스토리 백업을 저장하는 공유 폴더를 삭제합니다.  
  
    -   사용자에 대 한 파일 히스토리를 삭제 하려면 사용자 이름을 가진 파일 히스토리 백업 자식 폴더를 삭제 합니다.  
  
    -   컴퓨터에 대한 파일 히스토리를 삭제하려면 컴퓨터 이름을 가진 파일 히스토리 백업 자식 폴더를 삭제합니다. 예를 들어 사용자가 새 노트북에 대 한 작업 <을 시작한 후 MyComputer01를 사용 <중지 한 경우에는 MyComputer02를 사용 하 여 사용자가 \> \> \\ \> \\ \> 모든 파일 및 폴더를 새 노트북으로 전송 했으며 나중에 파일 기록이 필요 하지 않은 사용자를 확인 한 후 MyAccount<MyComputer01에서 C:\serverfolders\file 파일 히스토리<백업을 삭제할 수 있습니다.  
  
### <a name="cannot-apply-file-history-setting-to-a-new-user"></a>새 사용자에게 파일 히스토리 설정을 적용할 수 없음  
 사용자 이름이 Windows Server Essentials에서 삭제된 사용자의 사용자 이름과 동일한 새 사용자를 추가하는 경우 Windows Server Essentials에서 새 사용자의 파일 히스토리를 저장할 폴더를 만들려고 할 때 이름 충돌 때문에 새 사용자에 대한 파일 히스토리 구성이 실패할 수 있습니다. 이 문제를 해결하려면 삭제된 사용자에 대한 파일 히스토리 폴더의 이름을 바꿀 수 있습니다.  
  
##### <a name="to-locate-user-file-history-on-the-server"></a>서버에서 사용자 파일 히스토리를 찾으려면  
  
1.  관리자 권한으로 서버에 로그온합니다.  
  
2.  Windows Server Essentials 대시보드에서 **스토리지**를 클릭합니다.  
  
3.  **서버 폴더** 탭에서 파일 히스토리 백업 폴더의 위치를 적어둡니다. 기본 위치 는%SystemDrive%\ServerFolders\File History 백업 \\ 입니다.  
  
##### <a name="to-resolve-file-history-issues-for-a-new-user-with-a-name-conflict"></a>이름 충돌이 있는 새 사용자에 대한 파일 히스토리 문제를 해결하려면  
  
1.  관리자 권한으로 서버에 로그온합니다.  
  
2.  관리자 권한으로 파일 탐색기를 실행합니다.  
  
3.  파일 히스토리 백업 폴더로 이동합니다. 기본 위치는 C:\ServerFolders\File History Backups입니다.  
  
     파일 히스토리 백업 폴더에는 Windows Server Essentials에 추가된 각 사용자 계정에 대한 하위 폴더가 있습니다. 예를 들어 John Smith 사용자에 대한 파일 히스토리는 File History Backups\JohnSmith 하위 폴더에 저장됩니다.  
  
4.  삭제 한 사용자에 대 한 하위 폴더의 이름을 바꿉니다. 예를 들어 사용자 ** < *이름*>_Deleted**합니다. 사용자의 파일 히스토리가 더 이상 필요하지 않은 경우 폴더를 삭제할 수 있습니다.  

5. 이제 새 사용자를 추가할 수 있습니다. 자세한 내용은 사용자 계정 추가를 참조 하세요. 에서 [사용자 계정 관리](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md)를 사용 합니다.  
  
### <a name="a-user-account-was-removed-but-the-users-file-history-remains"></a>사용자 계정을 제거했는데 사용자의 파일 히스토리가 남아 있음  
 네트워크 관리자가 서버에서 사용자 또는 컴퓨터를 제거하지만 나중에 사용할 수 있도록 파일 히스토리 백업을 유지하기로 선택하는 경우도 있습니다. 파일 히스토리가 더 이상 필요하지 않은 경우 서버의 공유 폴더에서 사용자 또는 컴퓨터에 대한 File History Backups 폴더를 제거합니다. 이렇게 하려면 [To manually delete File History backups for a user or a computer](../support/Troubleshoot-File-History-in-Windows-Server-Essentials.md#BKMK_manuallyDelete)을 참조하세요.  

  
## <a name="see-also"></a>참고 항목  
  
-   [클라이언트 백업 관리](../manage/Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md)  

-   [Windows Server Essentials 지원](../support/Support-Windows-Server-Essentials.md)

