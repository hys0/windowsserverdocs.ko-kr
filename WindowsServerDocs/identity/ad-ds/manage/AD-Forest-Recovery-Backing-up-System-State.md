---
title: AD 포리스트 복구-전체 서버 백업
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 9238cb27-0020-42f7-90d6-fcebf7e3c0bc
ms.technology: identity-adds
ms.openlocfilehash: 14aa7abc19573b76ebc144cb6dea5f510b45e269
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369353"
---
# <a name="ad-forest-recovery---backing-up-the-system-state-data"></a>AD 포리스트 복구-시스템 상태 데이터 백업  

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

Windows Server 백업 또는 stsadm.exe를 사용 하 여 DC에서 시스템 상태 백업을 수행 하려면 다음 절차를 따르십시오.  

## <a name="to-perform-a-system-state-backup-using-windows-server-backup"></a>Windows Server 백업를 사용 하 여 시스템 상태 백업을 수행 하려면

1. **서버 관리자**열고 **도구**를 클릭 한 다음 **Windows Server 백업**를 클릭 합니다.
   - Windows Server 2008 R2 및 Windows Server 2008에서 **시작**을 클릭 하 고 **관리 도구**를 가리킨 다음 **Windows Server 백업**를 클릭 합니다. 

   ![백업 설치](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup1.png)

2. 메시지가 표시 되 면 **사용자 계정 컨트롤** 대화 상자에서 백업 운영자 자격 증명을 입력 한 다음 **확인**을 클릭 합니다.
3. **로컬 백업**을 클릭 합니다.
4. **동작** 메뉴에서 **한 번 백업**을 클릭합니다.
5. 한 번 백업 마법사의 **백업 옵션** 페이지에서 **다른 옵션**을 클릭 한 후 **다음**을 클릭 합니다.

   ![백업 설치](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup3.png)

6. **백업 구성 선택** 페이지에서 **사용자 지정**을 클릭 하 고 **다음**을 클릭 합니다.
7. **백업할 항목 선택** 화면에서 **항목 추가** 를 클릭 하 고 **시스템 상태** 를 선택한 다음 **확인**을 클릭 합니다.
   - Windows Server 2008 R2 및 Windows Server 2008에서 백업에 포함할 볼륨을 선택 합니다. **시스템 복구 사용** 확인란을 선택 하면 중요 한 모든 볼륨이 선택 됩니다. 

   ![백업 설치](media/AD-Forest-Recovery-Backing-up-System-State/systemstatebackup.png)  

8. **대상 유형 지정** 페이지에서 **로컬 드라이브** 또는 **원격 공유 폴더**를 클릭 한 후 **다음**을 클릭 합니다.  원격 공유 폴더에 백업 하는 경우 다음을 수행 합니다.  
   - 공유 폴더의 경로를 입력 합니다.
   - **Access Control**에서 상속 또는 **상속** 안 **함** 을 선택 하 여 백업에 대 한 액세스를 확인 한 후 **다음**을 클릭 합니다.  
   - **백업에 대 한 사용자 자격 증명 제공** 대화 상자에서 공유 폴더에 대 한 쓰기 권한이 있는 사용자의 사용자 이름 및 암호를 입력 한 다음 **확인**을 클릭 합니다.

9. Windows Server 2008 R2 및 Windows Server 2008의 경우 **고급 옵션 지정** 페이지에서 **VSS 복사 백업** 을 선택 하 고 **다음**을 클릭 합니다.
10. **백업 대상 선택** 페이지에서 백업 위치를 선택 합니다.  로컬 드라이브를 선택 하 여 로컬 드라이브를 선택 하거나 원격 공유를 선택한 경우 네트워크 공유를 선택 합니다.
11. 확인 화면에서 **백업**을 클릭 합니다.
12. 이 작업이 완료 되 면 **닫기**를 클릭 합니다.
13. Windows Server 백업를 닫습니다.

## <a name="to-perform-a-system-state-backup-using-wbadminexe"></a>Wbadmin를 사용 하 여 시스템 상태 백업을 수행 하려면

관리자 권한 명령 프롬프트를 열고 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
   ```
   wbadmin start systemstatebackup -backuptarget:<targetDrive>:
   ```

   ![백업 설치](media/AD-Forest-Recovery-Backing-up-System-State/systemstatebackup2.png)  

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)
