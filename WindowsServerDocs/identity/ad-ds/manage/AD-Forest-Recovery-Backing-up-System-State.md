---
title: AD 포리스트 복구-전체 서버 백업
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 9238cb27-0020-42f7-90d6-fcebf7e3c0bc
ms.technology: identity-adds
ms.openlocfilehash: a5306960bb2dca3849bdb4fc7304781af3f25335
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815874"
---
# <a name="ad-forest-recovery---backing-up-the-system-state-data"></a>AD 포리스트 복구-시스템 상태 데이터 백업  

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

Windows Server Backup 또는 wbadmin.exe를 사용 하 여 DC의 시스템 상태 백업을 수행 하려면 다음 절차를 따르십시오.  

## <a name="to-perform-a-system-state-backup-using-windows-server-backup"></a>Windows Server Backup을 사용 하 여 시스템 상태 백업을 수행 하려면

1. 오픈 **서버 관리자**, 클릭 **도구**를 클릭 하 고 **Windows Server Backup**합니다.
   - Windows Server 2008 R2 및 Windows Server 2008에서 클릭 **시작**, 가리킨 **관리 도구**를 클릭 하 고 **Windows Server Backup**합니다. 

   ![백업 설치](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup1.png)

2. 메시지가 나타나면 합니다 **사용자 계정 컨트롤** 대화 상자에서 백업 운영자 자격 증명을 제공 하 고 클릭 **확인**합니다.
3. 클릭 **로컬 백업**합니다.
4. **동작** 메뉴에서 **한 번 백업**을 클릭합니다.
5. 백업 되 면 마법사에서에 **백업 옵션** 페이지에서 **다양 한 옵션**를 클릭 하 고 **다음**합니다.

   ![백업 설치](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup3.png)

6. 에 **백업 구성 선택** 페이지에서 클릭 **사용자 지정)** 를 클릭 하 고 **다음**합니다.
7. 에 **백업할 항목 선택** 화면에서 클릭 **항목 추가** 선택한 **시스템 상태** 클릭 **확인**합니다.
   - Windows Server 2008 R2 및 Windows Server 2008에서 백업에 포함할 볼륨을 선택 합니다. 선택 하는 경우는 **시스템 복구를 사용 하도록 설정** 확인란을 선택 된 모든 중요 한 볼륨입니다. 

   ![백업 설치](media/AD-Forest-Recovery-Backing-up-System-State/systemstatebackup.png)  

8. 에 **대상 유형 지정** 페이지에서 **로컬 드라이브** 또는 **원격 공유 폴더**, 클릭 하 고 **다음**.  원격 공유 폴더를 백업 하는 경우 다음을 수행 합니다.  
   - 공유 폴더의 경로를 입력 합니다.
   - 아래 **액세스 제어**를 선택 **상속 하지 않습니다** 또는 **상속** 백업에 대 한 액세스를 확인 한 다음 클릭 **다음**합니다.  
   - 에 **백업에 대 한 사용자 자격 증명 제공** 대화 상자에서 공유 폴더에 대 한 쓰기 권한이 사용자에 대 한 사용자 이름 및 암호를 제공 하 고 클릭 **확인**합니다.

9. Windows Server 2008 R2 및 Windows Server 2008에는 **고급 옵션 지정** 페이지에서 **VSS 복사본 백업을** 클릭 하 고 **다음**합니다.
10. 에 **백업 대상 선택** 페이지, 백업 위치를 선택 합니다.  선택한 로컬 경우 드라이브는 로컬 드라이브를 선택 하는 또는 원격를 선택한 경우 공유 네트워크 공유를 선택 합니다.
11. 확인 화면에서 클릭 **백업**합니다.
12. 이 작업이 완료 되 면 클릭 **닫기**합니다.
13. Windows Server Backup을 닫습니다.

## <a name="to-perform-a-system-state-backup-using-wbadminexe"></a>Wbadmin.exe를 사용 하 여 시스템 상태 백업을 수행 하려면

관리자 권한 명령 프롬프트를 열고, 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
   ```
   wbadmin start systemstatebackup -backuptarget:<targetDrive>:
   ```

   ![백업 설치](media/AD-Forest-Recovery-Backing-up-System-State/systemstatebackup2.png)  

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md)
