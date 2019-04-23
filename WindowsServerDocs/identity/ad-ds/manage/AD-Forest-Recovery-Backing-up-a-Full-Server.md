---
title: AD 포리스트 복구-전체 서버 백업
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.technology: identity-adds
ms.openlocfilehash: fec8de8ea1dadb392f6a3bd1c881e8df2266f404
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846524"
---
# <a name="ad-forest-recovery---backing-up-a-full-server"></a>AD 포리스트 복구-전체 서버 백업  

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

다른 하드웨어 또는 다른 운영 체제 인스턴스로 복원할 수 때문에 포리스트 복구를 준비 하려면 전체 서버 백업은 것이 좋습니다.  Windows Server Backup을 사용 하 여 서버의 전체 백업을 수행할 수 있습니다. 

## <a name="windows-server-backup"></a>Windows Server 백업

Windows Server Backup은 기본적으로 설치 되지 않았습니다. Windows Server 2016 및 Windows Server 2012 R2에서는 다음 단계를 수행 하 여 설치 합니다.

>[!NOTE]
>단계를 Windows Server 2016 및 Windows Server 2012 R2 간에 약간 달라질 수 있습니다 주의 하십시오.

Windows Server 2008 및 Windows Server 2008 R2에 설치 하는 단계를 참조 하세요 [Windows Server Backup 설치](https://technet.microsoft.com/library/cc771232.aspx)합니다.  

### <a name="to-install-windows-server-backup"></a>Windows Server Backup을 설치 하려면

1. 오픈 **서버 관리자** 누릅니다 **역할 및 기능 추가**합니다.
2. 에 **역할 및 추가 기능 마법사** 클릭 **다음**합니다.
3. 에 **설치 유형을** 화면에서 기본값을 그대로 두고 **역할 기반 또는 기능 기반 설치** 클릭 **다음**합니다.
4. 에 **서버 선택** 화면에서 클릭 **다음**합니다.
5. 에 **서버 역할** 화면 클릭 **다음**합니다.
6. 에 **기능** 화면에서 **Windows Server Backup** 누릅니다 **다음**
   ![백업 설치](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup2.png)
7. **설치**를 클릭합니다.
8. 설치가 완료 되 면 클릭 **닫기**합니다.

### <a name="to-perform-a-backup-with-windows-server-backup"></a>Windows Server Backup을 사용 하 여 백업을 수행 하려면

1. 오픈 **서버 관리자**, 클릭 **도구**를 클릭 하 고 **Windows Server Backup**합니다.
   - Windows Server 2008 R2 및 Windows Server 2008에서 클릭 **시작**, 가리킨 **관리 도구**를 클릭 하 고 **Windows Server Backup**합니다.

   ![백업 설치](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup1.png) 

2. 메시지가 나타나면 합니다 **사용자 계정 컨트롤** 대화 상자에서 백업 운영자 자격 증명을 제공 하 고 클릭 **확인**합니다.
3. 클릭 **로컬 백업**합니다.
4. **동작** 메뉴에서 **한 번 백업**을 클릭합니다.
5. 백업 되 면 마법사에서에 **백업 옵션** 페이지에서 **다양 한 옵션**를 클릭 하 고 **다음**합니다.

   ![백업 설치](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup3.png)

6. 에 **백업 구성 선택** 페이지에서 **(권장) 하는 전체 서버**를 클릭 하 고 **다음**합니다.
7. 에 **대상 유형 지정** 페이지에서 **로컬 드라이브** 또는 **원격 공유 폴더**, 클릭 하 고 **다음**.
8. 에 **백업 대상 선택** 페이지, 백업 위치를 선택 합니다.  선택한 로컬 경우 드라이브는 로컬 드라이브를 선택 하는 또는 원격를 선택한 경우 공유 네트워크 공유를 선택 합니다.
9. 확인 화면에서 클릭 **백업**합니다.

   ![백업 설치](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup4.png)

10. 이 작업이 완료 되 면 클릭 **닫기**합니다.
11. Windows Server Backup을 닫습니다.

>[!NOTE]
>오류 메시지가 없는 백업 저장소 위치를 사용할 수 있는지를 받게 되 면 선택 된 볼륨 중 하나를 제외 하거나 새 볼륨 또는 원격 공유를 추가 해야 합니다.
>선택한 볼륨은 백업할 항목 목록에도 포함 되어 경고 메시지가 표시를 가져온 경우 제거 하 고 클릭 여부를 결정할 **확인**합니다.

## <a name="using-wbadminexe-to-backup-a-windows-server"></a>Wbadmin.exe를 사용 하 여 windows server를 백업 하려면

Wbadmin.exe를 백업 하 고 명령 프롬프트에서 운영 체제, 볼륨, 파일, 폴더 및 응용 프로그램을 복원할 수 있는 명령줄 유틸리티는입니다.

### <a name="to-perform-a-full-server-backup-using-wbadminexe"></a>Wbadmin.exe를 사용 하 여 전체 서버 백업을 수행 하려면
  
- 관리자 권한 명령 프롬프트를 열고, 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  

   ```
   wbadmin start backup -backuptarget:<Drive_letter_to store_backup>: -include:<Drive_letter_to_include>:
   ```

   ![백업 설치](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup5.png)

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md)
