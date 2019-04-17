---
title: "전체 서버 백업-광고 숲 복구"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 9238cb27-0020-42f7-90d6-fcebf7e3c0bc
ms.technology: identity-adfs
ms.openlocfilehash: a86d61536f8b426e1a5258c661d4e53da63d4162
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2017
---
# <a name="ad-forest-recovery---backing-up-the-system-state-data"></a>광고 숲 복구-시스템 상태 데이터를 백업  

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.
 
다음 절차를 사용 하 여 Windows Server 백업 또는 wbadmin.exe 사용 하 여 시스템 상태 백업을 DC에서 수행할 수 있습니다.  
  
## <a name="to-perform-a-system-state-backup-using-windows-server-backup"></a>Windows Server 백업을 사용 하 여 시스템 상태 백업을 수행 하려면  
1. 열기 **서버 관리자**, 클릭 **도구**을 차례로 클릭 하 고 **Windows Server 백업**합니다.
    - Windows Server 2008 R2 및 Windows Server 2008 **시작**를 가리킨 **관리 도구**을 차례로 클릭 하 고 **Windows Server 백업**합니다. 
![백업을 설치합니다](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup1.png) 
2. 라는 메시지가 나타나면에 **사용자 계정 컨트롤** 대화 상자에서 백업을 통신사 자격 증명을 제공 하 고 클릭 한 다음 **확인**합니다.
3. 클릭 **로컬 백업**합니다.
4. 에 **알림** 메뉴를 클릭 **번 백업**합니다.
5. 백업 한 번 마법사에서에 **백업 옵션** 페이지, 클릭 **다른 옵션**을 차례로 클릭 하 고 **다음**합니다.
![백업을 설치합니다](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup3.png)
6. 에 **선택 하 고 백업 구성** 페이지, 클릭 **사용자 지정)**을 차례로 클릭 하 고 **다음**합니다.
7. 에 **백업할 항목 선택** 화면을 클릭 **항목 추가** 선택한 **시스템 상태** 클릭 하 고 **확인**합니다.
    - Windows Server 2008 및 Windows Server 2008 r 2에는 백업에 포함할 볼륨을 선택 합니다. 선택 하는 경우는 **시스템 복구** 확인란을 모두 중요 한 볼륨을 선택 합니다. 
![백업을 설치합니다](media/AD-Forest-Recovery-Backing-up-System-State/systemstatebackup.png)  
8. 에 **종류 목적지를 지정** 페이지, 클릭 **로컬 드라이브** 또는 **Remote 공유 폴더**을 차례로 클릭 하 고 **다음**합니다.  원격 공유 폴더를 백업 하는 경우 다음을 수행 합니다.  
  
 1.  경로 공유 폴더를 입력 합니다.  
 2.  아래에서 **액세스 제어**선택 **상속 하지 않은** 또는 **상속** 백업에 대 한 액세스를 확인을 클릭 한 다음 **다음**합니다.  
 3.  에 **백업에 대 한 사용자 자격 증명을 제공** 대화 상자에서 쓰기 공유 폴더에 권한이 있는 사용자에 대 한 사용자 이름 및 암호를 입력 하 고 클릭 한 다음 **확인**합니다.
9. Windows Server 2008 R2 및 Windows Server 2008 용에 **고급 옵션 지정** 페이지를 선택 하 고 **VSS 복사 백업** 차례로 클릭 하 고 **다음**합니다.
10. 에 **백업이 저장 위치 선택** 페이지 백업 위치를 선택 합니다.  로컬 선택한 경우 드라이브 로컬 드라이브를 선택 하거나 공유 원격 선택한 경우 네트워크 공유를 선택 합니다.
11. 확인 화면에서 클릭 **백업**합니다.
12. 이 완료 되 면 클릭 **닫기**합니다.
13. Windows Server 백업을 닫습니다.

  
## <a name="to-perform-a-system-state-backup-using-wbadminexe"></a>시스템 상태 백업을 Wbadmin.exe를 사용 하 여 수행 하려면  
  
1.  관리자 명령 프롬프트를 열고, 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
    ```  
    wbadmin start systemstatebackup -backuptarget:<targetDrive>:
    ```  
![백업을 설치합니다](media/AD-Forest-Recovery-Backing-up-System-State/systemstatebackup2.png)  

## <a name="next-steps"></a>다음 단계

- [광고 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)
